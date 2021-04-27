---
title: Data Collection
weight: 2
template: docs
---

# OpenTelemetry Collector Architecture

This document describes the architecture design and implementation of OpenTelemetry Collector. As [Hypertrace collector](https://github.com/hypertrace/hypertrace-collector) is based on [OpenTelemetry collector](), the basic configurations and architecture for collector remains the same. 

## Summary

OpenTelemetry Collector is an executable that allows to receive telemetry data, optionally transform it and send the data further.

The Collector supports several popular open-source protocols for telemetry data receiving and sending as well as offering a pluggable architecture for adding more protocols.

Data receiving, transformation and sending is done using Pipelines. The Collector can be configured to have one or more Pipelines. Each Pipeline includes a set of Receivers that receive the data, a series of optional Processors that get the data from receivers and transform it and a set of Exporters which get the data from the Processors and send it further outside the Collector. The same receiver can feed data to multiple Pipelines and multiple pipelines can feed data into the same Exporter.

## Pipelines

Pipeline defines a path the data follows in the Collector starting from reception, then further processing or modification and finally exiting the Collector via exporters.

Pipelines can operate on 2 telemetry data types: traces and metrics. The data type is a property of the pipeline defined by its configuration. Receivers, exporters and processors used in a pipeline must support the particular data type otherwise `ErrDataTypeIsNotSupported` will be reported when the configuration is loaded. A pipeline can be depicted the following way:

![Pipelines](https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector/main/docs/images/design-pipelines.png)

There can be one or more receivers in a pipeline. Data from all receivers is pushed to the first processor, which performs a processing on it and then pushes it to the next processor (or it may drop the data, e.g. if it is a “sampling” processor) and so on until the last processor in the pipeline pushes the data to the exporters. Each exporter gets a copy of each data element. The last processor uses a `FanOutConnector` to fan out the data to multiple exporters.

The pipeline is constructed during Collector startup based on pipeline definition in the config file.

A pipeline configuration typically looks like this:

```yaml
service:
  pipelines: # section that can contain multiple subsections, one per pipeline
    traces:  # type of the pipeline
      receivers: [otlp, jaeger, zipkin]
      processors: [memory_limiter, batch]
      exporters: [otlp, jaeger, zipkin]
```

The above example defines a pipeline for “traces” type of telemetry data, with 3 receivers, 2 processors and 3 exporters.

### Receivers

Receivers typically listen on a network port and receive telemetry data. Usually one receiver is configured to send received data to one pipeline, however it is also possible to configure the same receiver to send the same received data to multiple pipelines. This can be done by simply listing the same receiver in the “receivers” key of several pipelines:

```yaml
receivers:
  opencensus:
    endpoint: "0.0.0.0:55678"

service:
  pipelines:
    traces:  # a pipeline of “traces” type
      receivers: [opencensus]
      processors: [memory_limiter, batch]
      exporters: [jaeger]
    traces/2:  # another pipeline of “traces” type
      receivers: [opencensus]
      processors: [batch]
      exporters: [opencensus]
```

In the above example “opencensus” receiver will send the same data to pipeline “traces” and to pipeline “traces/2”. (Note: the configuration uses composite key names in the form of `type[/name]` as defined in [this document](https://docs.google.com/document/d/1NeheFG7DmcUYo_h2vLtNRlia9x5wOJMlV4QKEK05FhQ/edit#)).

When the Collector loads this config the result will look like this (part of processors and exporters are omitted from the diagram for brevity):


![Receivers](https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector/main/docs/images/design-receivers.png)

Important: when the same receiver is referenced in more than one pipeline the Collector will create only one receiver instance at runtime that will send the data to `FanOutConnector` which in turn will send the data to the first processor of each pipeline. The data propagation from receiver to `FanOutConnector` and then to processors is via synchronous function call. This means that if one processor blocks the call the other pipelines that are attached to this receiver will be blocked from receiving the same data and the receiver itself will stop processing and forwarding newly received data.

### Exporters

Exporters typically forward the data they get to a destination on a network (but they can also send it elsewhere, e.g “logging” exporter writes the telemetry data to a local file).

The configuration allows to have multiple exporters of the same type, even in the same pipeline. For example one can have 2 “opencensus” exporters defined each one sending to a different opencensus endpoint, e.g.:

```yaml
exporters:
  opencensus/1:
    endpoint: "example.com:14250"
  opencensus/2:
    endpoint: "0.0.0.0:14250"
```

Usually an exporter gets the data from one pipeline, however it is possible to configure multiple pipelines to send data to the same exporter, e.g.:

```yaml
exporters:
  jaeger:
    protocols:
      grpc:
        endpoint: "0.0.0.0:14250"

service:
  pipelines:
    traces:  # a pipeline of “traces” type
      receivers: [zipkin]
      processors: [memory_limiter]
      exporters: [jaeger]
    traces/2:  # another pipeline of “traces” type
      receivers: [otlp]
      processors: [batch]
      exporters: [jaeger]
```

In the above example “jaeger” exporter will get data from pipeline “traces” and from pipeline “traces/2”. When the Collector loads this config the result will look like this (part of processors and receivers are omitted from the diagram for brevity):


![Exporters](https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector/main/docs/images/design-exporters.png)

### Processors

A pipeline can contain sequentially connected processors. The first processor gets the data from one or more receivers that are configured for the pipeline, the last processor sends the data to one or more exporters that are configured for the pipeline. All processors between the first and last receive the data strictly only from one preceding processor and send data strictly only to the succeeding processor.

Processors can transform the data before forwarding it (i.e. add or remove attributes from spans), they can drop the data simply by deciding not to forward it (this is for example how “sampling” processor works), they can also generate new data (this is how for example how a “persistent-queue” processor can work after Collector restarts by reading previously saved data from a local file and forwarding it on the pipeline).

The same name of the processor can be referenced in the “processors” key of multiple pipelines. In this case the same configuration will be used for each of these processors however each pipeline will always gets its own instance of the processor. Each of these processors will have its own state, the processors are never shared between pipelines. For example if “batch” processor is used in several pipelines each pipeline will have its own batch processor (although the batch processor will be configured exactly the same way if the reference the same key in the config file). As an example, given the following config:

```yaml
processors:
  batch:
    send_batch_size: 10000
    timeout: 10s

service:
  pipelines:
    traces:  # a pipeline of “traces” type
      receivers: [zipkin]
      processors: [batch]
      exporters: [jaeger]
    traces/2:  # another pipeline of “traces” type
      receivers: [otlp]
      processors: [batch]
      exporters: [otlp]
```

When the Collector loads this config the result will look like this:


![Processors](https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector/main/docs/images/design-processors.png)

Note that each “batch” processor is an independent instance, although both are configured the same way, i.e. each have a send_batch_size of 10000.

To read more infromation about how you can run collector as Agent or Standalone collector please read the documentation [here](https://github.com/open-telemetry/opentelemetry-collector/blob/main/docs/design.md).

#### References
- [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector/)
- [OpenTelemetry Collector documentation](https://github.com/open-telemetry/opentelemetry-collector/blob/main/docs/)

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/arch/data-collection.md">
<button type="button">Edit</button></a>

***
