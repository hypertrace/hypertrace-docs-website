---
title: Java Zipkin Exporter
weight: 1.3
template: docs
---
### Introduction
Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures.

It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

OpenCensus Java has support for this exporter available through package [io.opencensus.exporter.trace.zipkin](https://www.javadoc.io/doc/io.opencensus/opencensus-exporter-trace-zipkin)


### Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Zipkin endpoint available to receive traces

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
    <artifactId>opencensus-exporter-trace-zipkin</artifactId>
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

Instrument your code with the following snippet:
 
```java
package io.opencensus.tutorial.zipkin;

import io.opencensus.exporter.trace.zipkin.ZipkinTraceExporter;

public class ZipkinTutorial {
    public static void main(String ...args) throws Exception {
        ZipkinTraceExporter.createAndRegister("http://localhost:9411/api/v2/spans", "service-a");
    }
}
```
 
## #Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost).

### Project link
You can find out more about the Zipkin project at [https://zipkin.io/](https://zipkin.io/)

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/go/java-zipkin.md">
<button type="button">Edit</button></a>
***
