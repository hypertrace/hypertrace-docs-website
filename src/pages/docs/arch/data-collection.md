---
title: Data Collection
weight: 2
template: docs
---

## Receivers

This receiver receives spans from instrumented applications and translates them into the internal span types that are then sent to the collector/exporters.

### 1. OpenCensus Receiver:
The OpenCensus receiver for the agent can receive trace export calls via HTTP/JSON in addition to gRPC. The HTTP/JSON address is the same as gRPC as the protocol is recognized and processed accordingly.

The HTTP/JSON endpoint can also optionally CORS, which is enabled by specifying a list of allowed CORS origins in the cors_allowed_origins field:
```
receivers:
  opencensus:
    address: "localhost:55678"
    cors_allowed_origins:
    - http://test.com
    # Origins can have wildcards with *, use * by itself to match any origin.
    - https://*.example.com  
```

### 2. Jaeger
This receiver receives spans from Jaeger collector HTTP and Thrift uploads and translates them into the internal span types that are then sent to the collector/exporters.

Its address can be configured in the YAML configuration file under section "receivers", subsection "jaeger" and fields "collector_http_port", "collector_thrift_port".

Here, Thrift is an interface definition language and binary communication protocol used for defining and creating services for numerous languages. It forms a remote procedure call (RPC) framework and was developed at Facebook for "scalable cross-language services development".

For example:
```
receivers:
  jaeger:
    collector_thrift_port: 14267
    collector_http_port: 14268
```

### 3. Zipkin
This receiver receives spans from Zipkin (V1 and V2) HTTP uploads and translates them into the internal span types that are then sent to the collector/exporters.

Its address can be configured in the YAML configuration file under section "receivers", subsection "zipkin" and field "address". The syntax of the field "address" is `[address|host]:<port-number>.`

For example:
```
receivers:
  zipkin:
    address: "127.0.0.1:9411"
```

### 4. Prometheus
This receiver is a drop-in replacement for getting Prometheus to scrape your services. Just like you would write in a YAML configuration file before starting Prometheus, such as with:
```
prometheus --config.file=prom.yaml
```
you can copy and paste that same configuration under section
```
receivers:
  prometheus:
    config:
```
such as:
```
receivers:
    prometheus:
      config:
        scrape_configs:
          - job_name: 'opencensus_service'
            scrape_interval: 5s
            static_configs:
              - targets: ['localhost:8889']

          - job_name: 'jdbc_apps'
            scrape_interval: 3s
            static_configs:
              - targets: ['localhost:9777']
```

## Exporters
An exporter is how you send data to one or more backends/destinations. One or more exporters can be configured. By default, no exporters are configured on the Service (either the Agent or Collector).

A basic example of all available exporters is provided below. For detailed exporter configuration, please see the exporter README.md.
```yaml
exporters:
  opencensus:
    headers: {"X-test-header": "test-header"}
    compression: "gzip"
    cert-pem-file: "server_ca_public.pem" # optional to enable TLS
    endpoint: "127.0.0.1:55678"
    reconnection-delay: 2s

  jaeger:
    collector_endpoint: "http://127.0.0.1:14268/api/traces"

  kafka:
    brokers: ["127.0.0.1:9092"]
    topic: "opencensus-spans"

  stackdriver:
    project: "my-project-id" # optional, defaults to agent project if run on GCP
    enable_tracing: true

  zipkin:
    endpoint: "http://127.0.0.1:9411/api/v2/spans"

  aws-xray:
    region: "us-west-2"
    default_service_name: "verifiability_agent"
    version: "latest"
    buffer_size: 200

  honeycomb:
    write_key: "739769d7-e61c-42ec-82b9-3ee88dfeff43"
    dataset_name: "dc8_9"
```