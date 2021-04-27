---
title: Java Instrumentation
subtitle: Instrument your Java application with Hypertrace Java agent or OpenTelemetry Java agent. 
weight: 1
template: docs
---

## Instrument your Java application with Hypertrace Java agent

[Hypertrace Java agent](https://github.com/hypertrace/javaagent) is Hypertrace's distribution of [OpenTelemetry Java agent](https://github.com/open-telemetry/opentelemetry-java-instrumentation).

### Supported Libraries and Frameworks

This agent supports [these frameworks](https://github.com/open-telemetry/opentelemetry-java-instrumentation#supported-java-libraries-and-frameworks)
and adds following capabilities:
* capture request and response headers
* capture request and response bodies
* server request headers/bodies evaluation in agent filter that can result in request blocking.
    The filter implementation will be pluggable.

List of supported frameworks with additional capabilities:

| Library/Framework                                                                                      | Versions        |
|--------------------------------------------------------------------------------------------------------|-----------------|
| [Apache HttpAsyncClient](https://hc.apache.org/index.html)                                             | 4.1+            |
| [Apache HttpClient](https://hc.apache.org/index.html)                                                  | 4.0+            |
| [gRPC](https://github.com/grpc/grpc-java)                                                              | 1.5+            |
| [JAX-RS Client](https://javaee.github.io/javaee-spec/javadocs/javax/ws/rs/client/package-summary.html) | 2.0+            |
| [Micronaut](https://micronaut.io/)  (basic support via Netty)                                          | 1.0+            |
| [Netty](https://github.com/netty/netty)                                                                | 4.0+            |
| [OkHttp](https://github.com/square/okhttp/)                                                            | 3.0+            |
| [Servlet](https://javaee.github.io/javaee-spec/javadocs/javax/servlet/package-summary.html)            | 2.3+            |
| [Spark Web Framework](https://github.com/perwendel/spark)                                              | 2.3+            |
| [Spring Webflux](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/reactive/package-summary.html)       | 5.0+            |
| [Vert.x](https://vertx.io)                                                                             | 3.0+ (4 not supported yet) |
| [Struts](https://struts.apache.org/)                                                                   | 2.3+            |

#### Adding custom filter implementation

Custom filter implementations can be added via `FilterProvider` SPI (Java service loader).
The providers can be disabled at startup via `ht.filter.provider.<provider-class-name>.disabled=true`.

### Run & Configure

Download the [latest version](https://github.com/hypertrace/javaagent/releases/latest/download/hypertrace-agent-all.jar).

```bash
HT_EXPORTING_ENDPOINT=http://localhost:9411/api/v2/spans java -javaagent:javaagent/build/libs/hypertrace-agent-<version>-all.jar -jar app.jar
```

By default the agent uses Zipkin exporter.

The configuration precedence order 
1. OpenTelemetry Agent's trace config file `OTEL_TRACE_CONFIG`/`otel.trace.config`
2. OpenTelemetry system properties and env variables
3. Hypertrace configuration with the following precedence order:
   1. system properties 
   2. environment variables, TODO add link to agent-config repo
   3. [configuration file](https://github.com/hypertrace/javaagent/blob/main/example-config.yaml), specified `HT_CONFIG_FILE=example-config.yaml`

### Disable instrumentation at startup

Instrumentations can be disabled by `-Dotel.instrumentation.<instrumentation-name>.enabled=false`.

The following instrumentation names disable only Hypertrace instrumentations, not core OpenTelemetry:

* `ht` - all Hypertrace instrumentations
* `servlet-ht` - Servlet, Spark Web
* `okhttp-ht` - Okhttp
* `grpc-ht` - gRPC

The Hypertrace instrumentations use also the core OpenTelemetry instrumentation names so for example
`-Dotel.instrumentation.servlet.enabled=false` disables all servlet instrumentations including core
OpenTelemetry and Hypertrace.

---

## Instrument your Java application with OpenTelemetry Java agent

### Supported Libraries and Frameworks

We support an impressively huge number of [libraries and frameworks](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md#libraries---frameworks) and
a majority of the most popular [application servers](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md#application-servers) right out of the box!
[Click here to see the full list](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md) and to learn more about
[disabled instrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md#disabled-instrumentations)
and how to [suppress unwanted instrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/suppressing-instrumentation.md).

### Manually instrumenting

For most users, the out-of-the-box instrumentation is completely sufficient and nothing more has to
be done.  Sometimes, however, users wish to add attributes to the otherwise automatic spans,
or they might want to manually create spans for their own custom code.

[See here for detailed instructions](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/manual-instrumentation.md).

### Run & Configure

Download the [latest version](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent-all.jar).

This package includes the instrumentation agent as well as
instrumentations for all supported libraries and all available data exporters.
The package provides a completely automatic, out-of-the-box experience.

Enable the instrumentation agent using the `-javaagent` flag to the JVM.
```
java -javaagent:path/to/opentelemetry-javaagent-all.jar \
     -jar myapp.jar
```
By default, the OpenTelemetry Java agent uses
[OTLP exporter](https://github.com/open-telemetry/opentelemetry-java/tree/master/exporters/otlp)
configured to send data to
[OpenTelemetry collector](https://github.com/open-telemetry/opentelemetry-collector/blob/master/receiver/otlpreceiver/README.md)
at `http://localhost:4317`.

Configuration parameters are passed as Java system properties (`-D` flags) or
as environment variables. See [the configuration documentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/agent-config.md)
for the full list of configuration items. For example:
```
java -javaagent:path/to/opentelemetry-javaagent-all.jar \
     -Dotel.resource.attributes=service.name=your-service-name \
     -Dotel.traces.exporter=zipkin \
     -jar myapp.jar
```

The agent is [highly configurable](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/agent-config.md)!  Many aspects of the agent's behavior can be configured for your needs, such as exporter choice, exporter config (like where data is sent), trace context propagation headers, and much more. [Click here to see the detailed list of configuration environment variables and system properties](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/agent-config.md).


#### References
- 