---
title: What is Hypertrace?
template: docs

---
Hypertrace is a real-time observability platform that helps teams make sense of
their production requests and trends within their network.

Hypertrace converts distributed trace data into relevant insight for everyone.
Infrastructure teams can identify which services are causing overload. Service
teams can diagnose why a specific user's request failed, or which applications
put their service objectives at risk. Deployment teams can know if a new
version is causing a problem.

Hypertrace is open source licensed and accepts all major tracing data formats.
This means you can try it without changing your applications!

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) |
|:--:|
| *Hypertrace* |


# Features

Hypertrace is open source and includes features commonly present in distributed
tracing systems such as a cloud-native backend and a UI. Hypertrace goes beyond,
including features usually left to commercial products, such as real-time
processing, custom dashboards and sophisticated path-based analysis!

As many are new to tracing, we'll review basic features first, then the advanced features usually only available in commercial products:

## Basic features:

| Feature                 | Description                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------- |
| Trace UI                | Visualizes a request's path through services and any backends, including context, errors and delays  |
| Application Flow UI     | Visualize an service graph of all traced traffic in your network                                     |
| Cloud Native Deployment | Kubernetes cluster with Helm Charts to install and manage it                                         |


## Notable features:
The below features are available by default in Hypertrace, but are not usually included in Open Source distributed tracing systems.

| Feature                 | Description                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| Dashboard UI            | Global health including most frequently called endpoints, services and backends              |
| Services UI             | Service owners see health and latency overview of their endpoints and dependencies           |
| Backends UI             | Owners of backends like MySQL or Redis can quickly identify slow queries and identify trends |
| Built-in Rosetta Stone  | Natively understands all major trace data formats including Jaeger, OpenTelemetry and Zipkin |
| Sampling unnecessary    | Designed to ingest 100% of request traces natively. No need for a sampling collector.        |
| Real-time processing    | Application flow and metrics aggregate automatically, using stream processing.               |


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/index.md">
<button type="button">Edit</button></a>

***
