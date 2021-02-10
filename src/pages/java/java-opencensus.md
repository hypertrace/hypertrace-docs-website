---
title: Java OpenCensus Exporter
weight: 1.1
template: docs
---
### Introduction
The OpenCensus Agent exporter aka "ocagent-exporter" enables Java applications to send the observability signals
that they've collected using OpenCensus to the [OpenCensus Agent](https://github.com/census-instrumentation/opencensus-service)

This exporter connects and sends observability signals via a single HTTP/2 stream and gRPC with Protocol Buffers
to the OpenCensus Agent. If unspecified, this exporter tries to connect to the OpenCensus Agent on port `55678`.

### Purpose
It converts OpenCensus Stats and Traces into OpenCensus Proto Metrics and Traces which are then sent to the OpenCensus Agent.
Therefore programs no longer have to enable the traditional backends' exporters for every single application.

For example, some backends like Prometheus require opening a unique port per application. This port is what they'll pull stats from.
If you have 10,000 microservices that all each export to Prometheus, you already have to manually and uniquely create
at least 10,000 unique ports. Uniquely creating a port will not only exhaust your file descriptors but it also becomes
cumbersome and error prone to do.

With the ocagent-exporter, instead the stats are uploaded to the OpenCensus Agent and from there,
the agent is singly scraped by Prometheus.

As you can see from above, this not only scales your application's resource allocation but also scales your development speed
and liberates you from complex batching deployments. It also ensures that your applications can be kept light, that the agent's
deployment can safely be restarted flexibly.

The same thing happens for traces.

### Add the dependencies to your project

For Maven add to your pom.xml:
```
<dependencies>
  <dependency>
    <groupId>io.opencensus</groupId>
    <artifactId>opencensus-exporter-metrics-ocagent</artifactId>
    <version>0.20.0</version>
  </dependency>
  <dependency>
    <groupId>io.opencensus</groupId>
    <artifactId>opencensus-exporter-trace-ocagent</artifactId>
    <version>0.20.0</version>
  </dependency>
</dependencies>
```
For Gradle add to your dependencies:

```
compile 'io.opencensus:opencensus-exporter-metrics-ocagent:0.20.0'
compile 'io.opencensus:opencensus-exporter-trace-ocagent:0.20.0'
```

### Register the exporter

An exporter can be started by invoking `createAndRegister()`, whose signature is:
```java
OcAgentMetricsExporter.createAndRegister(OcAgentMetricsExporterConfiguration.builder().build());
OcAgentTraceExporter.createAndRegister(OcAgentTraceExporterConfiguration.builder().build());
```

### Options
Options allow you to customize the exporter.
Options use a builder pattern which allows optional functional options.
```java
OcAgentTraceExporterConfiguration.builder().setEndPoint("localhost:55678").setUseInsecure(true).build();
```

#### Custom address
This option allows one to talk to an OpenCensus Agent running on a customized address.
The customized address could be anything that is resolvable by
[io.grpc.NameResolver](https://grpc.io/grpc-java/javadoc/io/grpc/NameResolver.html).

```
OcAgentMetricsExporterConfiguration.builder().setEndPoint("zookeeper://zk.example.com:9900/ocagent").build();
OcAgentTraceExporterConfiguration.builder().setEndPoint("zookeeper://zk.example.com:9900/ocagent").build();
```

#### Insecure
This option allows one to talk to the OpenCensus Agent without mutual TLS.

This option is mutually exclusive to [SSL Context](#ssl-context). If both are set, an IllegalArgumentException will be thrown.

It can be enabled like this
```
OcAgentMetricsExporterConfiguration.builder().setUseInsecure(true).build();
OcAgentTraceExporterConfiguration.builder().setUseInsecure(true).build();
```

#### SSL Context
Alternatively you can configure the exporter to talk to the OpenCensus Agent with TLS.

This option is mutually exclusive to [Insecure](#insecure). If both are set, an IllegalArgumentException will be thrown.

It can be enabled like this
```
OcAgentMetricsExporterConfiguration.builder().setSslContext(SslContext.defaultClientProvider()).build();
OcAgentTraceExporterConfiguration.builder().setSslContext(SslContext.defaultClientProvider()).build();
```

#### Service name
This option allows one to set the service name of the caller by using setServiceName.

It can be enabled like this
```
OcAgentMetricsExporterConfiguration.builder().setServiceName("my own service").build();
OcAgentTraceExporterConfiguration.builder().setServiceName("my own service").build();
```

#### Reconnection period
This option defines the amount of time for a failed connection, that the exporter takes before a reconnection attempt to the agent.

The option's name is setRetryInterval.

Here is an example for how to tell it to attempt reconnecting on fail, after 10 seconds.
```
OcAgentMetricsExporterConfiguration.builder().setRetryInterval(Duration.create(10, 0)).build();
OcAgentTraceExporterConfiguration.builder().setRetryInterval(Duration.create(10, 0)).build();
```

### References

Resource|URL
---|---
OCAgent Metrics Exporter Javadoc|[io.opencensus.exporter.metrics.ocagent](https://www.javadoc.io/doc/io.opencensus/opencensus-exporter-metrics-ocagent/)
OCAgent Trace Exporter Javadoc|[io.opencensus.exporter.trace.ocagent](https://www.javadoc.io/doc/io.opencensus/opencensus-exporter-trace-ocagent/)
Source code|[Metrics exporter on Github](https://github.com/census-instrumentation/opencensus-java/tree/master/exporters/metrics/ocagent), [Trace exporter on Github](https://github.com/census-instrumentation/opencensus-java/tree/master/exporters/trace/ocagent)
OpenCensus Agent|[Agent homepage](/service/components/agent)
gRPC NameResolver|[io.grpc.NameResolver](https://grpc.io/grpc-java/javadoc/io/grpc/NameResolver.html)


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/go/java-opencensus.md">
<button type="button">Edit</button></a>

***
