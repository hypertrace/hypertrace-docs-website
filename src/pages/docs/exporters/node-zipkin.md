---
title: Zipkin
weight: 2
template: docs
---
# Zipkin Exporter

## Introduction
Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures.

It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

OpenCensus Node.js has support for this exporter available, distributed through NPM package [@opencensus/exporter-zipkin](https://www.npmjs.com/package/@opencensus/exporter-zipkin)

## Installing the exporter
You can install OpenCensus Zipkin Exporter by running these steps:

```bash
npm install @opencensus/nodejs
npm install @opencensus/exporter-zipkin
```

## Creating the exporter
Now let's use the Zipkin exporter:

```js
const tracing = require('@opencensus/nodejs');
const { ZipkinTraceExporter } = require('@opencensus/exporter-zipkin');

// Add your zipkin url (ex http://localhost:9411/api/v2/spans)
// and application name to the Zipkin options
const zipkinOptions = {
  url: 'your-zipkin-url',
  serviceName: 'your-application-name'
};

const exporter = new ZipkinTraceExporter(zipkinOptions);
tracing.registerExporter(exporter).start();
```

## Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost).

## Project link
You can find out more about the Zipkin project at [https://zipkin.io/](https://zipkin.io/)
