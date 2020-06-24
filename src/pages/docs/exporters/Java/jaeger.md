---
title: Jaeger
weight: 2
template: docs
---
# Jaeger Exporter

## Introduction
Jaeger, inspired by Dapper and OpenZipkin, is a distributed tracing system released as open source by Uber Technologies.
It is used for monitoring and troubleshooting microservices-based distributed systems, including:

* Distributed context propagation
* Distributed transaction monitoring
* Root cause analysis
* Service dependency analysis
* Performance / latency optimization

OpenCensus Java has support for this exporter available through package [io.opencensus.exporter.trace.jaeger](https://www.javadoc.io/doc/io.opencensus/opencensus-exporter-trace-jaeger)


## Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Jaeger endpoint available to receive traces

If using Maven, add these to your `pom.xml` file
```xml
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <opencensus.version>0.15.0</opencensus.version> <!-- The OpenCensus version to use -->
</properties>

<dependencies>
  <dependency>
    <groupId>io.opencensus</groupId>
    <artifactId>opencensus-api</artifactId>
    <version>${opencensus.version}</version>
  </dependency>
  <dependency>
    <groupId>io.opencensus</groupId>
    <artifactId>opencensus-exporter-trace-jaeger</artifactId>
    <version>${opencensus.version}</version>
  </dependency>
  <dependency>
    <groupId>io.opencensus</groupId>
    <artifactId>opencensus-impl</artifactId>
    <version>${opencensus.version}</version>
    <scope>runtime</scope>
  </dependency>
</dependencies>
```

```java
package io.opencensus.tutorial.jaeger;

import io.opencensus.exporter.trace.jaeger.JaegerTraceExporter;

public class JaegerTutorial {
    public static void main(String ...args) throws Exception {
        JaegerTraceExporter.createAndRegister("http://127.0.0.1:14268/api/traces", "service-b");
    }
}
```

## Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost).

## Project link
You can find out more about the Jaeger project at [https://www.jaegertracing.io/](https://www.jaegertracing.io/)
