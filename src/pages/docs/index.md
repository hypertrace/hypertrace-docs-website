---
title: What is Hypertrace?
template: docs
---
Hypertrace is a highly scalable distributed tracing and observability platform designed to ingest and analyze large volumes of production trace data. OpenTelemetry-based agents collect and send observability data directly from applications to Hypertrace for analysis. Data visualizations, reports, and dashboards are available in a web-based console to assist in monitoring cloud-native applications and resolving application and service performance problems.

# Hypertrace: Features
Hypertrace is a highly scalable open source platform with many of the same features as other distributed tracing platforms. Its real distninction, however, is that it offers advanced features out-of-the-box, which are typically found only in commercial products. 

## Basic Distributed Tracing Features:

| Category | Features                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monitor  | Distributed Tracing & Correlation - End-to-end distributed tracing of all internal microservice/backend calls triggered by the edge API calls and web transactions. |
|          | Application Flow Mapping - Real-time discovery and visualization of end-to-end application topology                                                                 |
|          |                                                                                                                                                                     |
| Trace    | Web Transaction Monitoring - Monitor all web transactions at Web Proxies                                                                                            |
|          | Microservice Monitoring - Monitor all internal micro-ervice calls.                                                                                                  |
|          | Backends Monitoring - Monitor all calls to backend systems like databases or third-party services.                                                                  |
|          | End User Monitoring - Monitor end-user calls                                                                                                                        |
|          |                                                                                                                                                                     |
| Identify | Trace Filtering & Visualizations - Search & visualize any traces.                                                                                                   |
|          | Advanced Slice & Dice - Create your own aggregation and grouping of traces                                                                                          |

## Advanced Distributed Tracing features:
- Flowmaps and metrics for Services
- Flowmaps and metrics for APIs. APIs detected automatically. 
- API host (or Domain) level metrics and traces
- API Analytics with slice & dice for APIs
- Flow map supported at scale. Other distributed tracing projects support flowmap for dev & test only. For production, you'd need to run separate Spark jobs to generate a dependency graph.
- Basic APM product around Services and APIs
- Flexible query interface to build your own UIs
- OLAP store is pluggable with abstractions (need to add request handlers in QueryService)


## Feature Table
| Feature                                | Description                                                                                                                                            |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Aggregations                           | Hypertrace Explorer provides multiple parameters to help you aggregate your API and trace searches                                                     |
| Slice and dice                         | Hypertrace provides the ability to slice and dice traces to derive advanced insights.                                                                  |
| Highly Scalable                        | Unlike most of the current open source solutions Hypertrace supports scaling out-of-the box. It can even scale for large production grade deployments. |
| Native suppport for various collectors | send and receive traces from OpenCesnus, Jaeger, Zipkin and OpenTelemetry.                                                                             |
| Multiple storage backends              | Hypertrace supports all major backends by default.                                                                                                     |
| Beautiful UI                           | Hypertrace comes with a beautiful & modern UI which makes it more informative and useful for analysing your application.                               |
| Cloud Native Deployment                | Deploy Hypertrace on any kubernetes cluster with helm charts and an installation script.                                                               |
| Observability & Multiple APM features  | Hypertrace provides many observability metrics in it's dashboard and throughout the platform as needed and also provides some basic APM features.      |


## Comparison: Hypertrace vs. Other open-source tracing solutions
| Other open source platforms                                   | Hypertrace                                                                                             |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| scalable but you need to change configs for major deployment. | Scales out of the box                                                                                  |
| Native support for OpenTracing                                | Support for OpenTracing API, OpenCensus, OpenTelemetry and other open source collectors and exporters. |
| Multiple storage backends                                     | OLAP store is pluggable with abstractions (need to add request handlers in QueryService)               |
| Modern Web UI based on React                                  | Modern Web UI based on custom framework Hyperdash                                                      |
| Limited observability features                                | Comes with bunch of observability metrics and details along with limited APM features.                 |
| Cloud Native Deployment                                       | Single installation script which will help you install on any platform, cloud or local.                |
| Backwards compatibility with other tracing solutions          | Supports possibly all open source tracing solutions available as of now.                               |
| Basic DAGs for application flow                               | Comes with modern flow map at scale with features like panning and scaling.                            |
| No way to get detailed insights for single service.           | A complete microservices section will give you details about each service.                             |

