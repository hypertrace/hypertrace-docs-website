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
version is causing a problem. Security teams can see non-complaint communication
and audit accordingly.

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

## Basic Distributed Tracing Features:

| Category | Features                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Monitor**  | Distributed Tracing & Correlation - End-to-end distributed tracing of all internal microservice/backend calls triggered by the edge API calls and web transactions. |
|          | Application Flow Mapping - Real-time discovery and visualization of end-to-end application topology.                                                                 |
| **Trace**    | Web Transaction Monitoring - Monitor all web transactions at Web Proxies.                                                                                            |
|          | Microservice Monitoring - Monitor all internal micro-service calls.                                                                                                  |
|          | Backend Monitoring - Monitor all calls to backend systems like databases or third-party services.                                                                  |
|          | End User Monitoring - Monitor end-user calls.                                                                                                                        |
| **Identify** | Trace Filtering & Visualizations - Search & visualize any traces.                                                                                                   |
|          | Advanced Slice & Dice - Create your own aggregation and grouping of traces                                                                                          |

## Advanced Distributed Tracing Features:
- Flowmaps and metrics for Services & APIs. APIs are detected automatically.
- API host (or Domain) level metrics and traces.
- API Analytics with slice & dice for APIs.
- Flow map supported at scale and helps discovering non-compliant commnunication.
- Basic APM product around Services and APIs.
- Flexible query interface to build your own UIs
- OLAP store is pluggable with abstractions (need to add request handlers in QueryService).


## Feature Table
| Feature                                | Description                                                                                                                                            |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Aggregations                           | Hypertrace Explorer provides multiple parameters to help you aggregate your API and trace searches                                                     |
| Slice & dice                         | Hypertrace provides the ability to slice and dice traces to derive advanced insights                                                                  |
| Supports scalable real-time processing                        | Unlike most of the current open source solutions Hypertrace supports efficient and scalable real-time stream processing. |
| Native suppport for various collectors | Send and receive traces from OpenCesnus, Jaeger, Zipkin and OpenTelemetry                                                                             |
| Cloud Native Deployment                | Deploy Hypertrace on any Kubernetes cluster with Helm Charts and an installation script                                                               |
| Observability & Multiple APM features  | Hypertrace provides many observability metrics in it's dashboard and throughout the platform as needed and also provides some basic APM features      |


## Comparison: Hypertrace vs. Other open source distributed tracing platforms
| Other open source platforms                                   | Hypertrace                                                                                             |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Scalable but you need to change configs for major deployment. | Scales out of the box                                                                                  |
| Limited observability features.                                | Includes many observability features - metrics, details, plus limited APM features.                 |
| Cloud Native Deployment.                                       | Installation script deployes to laptop/on-prem or cloud.                |
| Backwards compatibility with other tracing solutions.          | Supports all available open source tracing solutions.                               |
| Basic DAGs for application flow.                               | Includes modern flow map at scale with features like ability to discover non-compliant. commnunication.                         |
| No way to get detailed insights for single service.            | Flowmaps and metrics for Services & APIs .                           |


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/index.md">
<button type="button">Edit</button></a>

***
