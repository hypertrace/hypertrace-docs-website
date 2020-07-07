---
title: What is Hypertrace?
template: docs

---
Hypertrace is a highly scalable distributed tracing and observability platform designed to ingest and analyze large volumes of production trace data. Various open source and enterprise agents and tracers collect and send observability data directly from applications to Hypertrace for analysis. Data visualizations, reports, and dashboards are available in a web-based console to assist in monitoring cloud-native applications and resolving application and service performance problems.

# Features
Hypertrace is a highly scalable open source platform with many of the same features as other distributed tracing platforms. Its real distninction, however, is that it offers advanced features out-of-the-box, which are typically found only in commercial products. 

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

## Advanced Distributed Tracing features:
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
