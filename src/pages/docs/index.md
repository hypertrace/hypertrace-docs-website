---
title: What is Hypertrace?
template: docs
---
Hypertrace is a highly scalable distributed tracing and observability platform designed to ingest and analyze large volumes of production trace data. OpenTelemetry-based agents collect and send observability data directly from applications to Hypertrace for analysis. Data visualizations, reports, and dashboards are available in a web-based console to assist in monitoring cloud-native applications and resolving application and service performance problems.

# Hypertrace: Features
Hypertrace is a highly scalable open source platform with many of the same features as other distributed tracing platforms. Its real distninction, however, is that it offers advanced features out-of-the-box, which are typically found only in commercial products. 

## Advanced Distributed Tracing features:
- Flowmaps and metrics for Services
- Flowmaps and metrics for APIs. APIs detected automatically. 
- API host (or Domain) level metrics and traces
- API Analytics with slice & dice for APIs
- Flow map supported at scale. Other distributed tracing projects support flowmap for dev & test only. For production, you'd need to run separate Spark jobs to generate a dependency graph.
- Basic APM product around Services and APIs
- Flexible query interface to build your own UIs
- OLAP store is pluggable with abstractions (need to add request handlers in QueryService)

## Basic Distributed Tracing Features:
- Monitor
    - Distributed Tracing & Correlation - End-to-end distributed tracing of all internal microservice/backend calls triggered by the edge API calls and web transactions
    - Application Flow Mapping - Real-time discovery and visualization of end-to-end application topology
- Trace
    - Web Transaction Monitoring - Monitor all web transactions at Web Proxies
    - Microservice Monitoring - Monitor all internal micro-ervice calls
    - Backends Monitoring - Monitor all calls to backend systems like databases or third-party services
    - End User Monitoring - Monitor end-user calls
- Identify 
    - Trace Filtering & Visualizations - Search & visualize any traces
    - Advanced Slice & Dice - Create your own aggregation and grouping of traces

## Feature details:

### Aggregations
Hypertrace Explorer provides multiple parameters to help you aggregate your API and trace searches. Combine parameters together to give you aggregations based on very specific criteria. 

### Slice and dice
Hypertrace provides the ability to slice and dice traces to derive advanced insights. 

### Highly Scalabile
Unlike most of the current open source solutions Hypertrace supports scaling out-of-the box. It can scale for large production grade deployments. You can rely on Hypertrace to scale to your business needs. 

### Native suppport to send and receive traces from OpenCesnus, Jaeger, Zipkin and OpenTelemetry 
If your application is already instrumented for tracing with Jaeger, Zipkin or any other platform that supports and relies on OpenTracing API? No worries! Hypertrace can consume these traces in hypertrace with bunch of different functionalities available out-of-the box.

### Multiple storage backends
Hypertrace supports all major backends by default. 

### UI to fall in love with
Hypertrace comes with a beautiful & modern UI which makes it more informative and useful for analysing your application.

### Cloud Native Deployment
Deploy Hypertrace on any kubernetes cluster with helm charts and an installation script

### Observability & Multiple APM features
Hypertrace provides many observability metrics in it's dashboard and throughout the platform as needed. Hypertrace supports multiple APM features out-of-the-box such as detecting frontend or customer services in your application automatically.

### Multiple ways to build and use
There are multiple ways to build or deploy hypertrace. And a team of engineers to answer you questions online.


## Comparison: Hypertrace vs. Other open-source tracing solutions
| Other open soure products           | Hypertrace                                                                                                                                                                                      |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| High Scalability                    | Flow map at scale. Jaeger only supports the flowmap with all-in-one setup, which isn’t production scale. For production, one needs to run separate Spark jobs to generate the dependency graph. |
| Native support for OpenTracing      | APIs detected automatically. Flowmaps and metrics for APIs.                                                                                                                                     |
| Multiple storage backends           | Metrics and flowmaps for Services                                                                                                                                                               |
| Modern Web UI                       | API host (or Domain) level metrics and traces                                                                                                                                                   |
| Cloud Native Deployment             | Basic APM product around Services and APIs                                                                                                                                                      |
| Observability                       | API Analytics with slice & dice around APIs                                                                                                                                                     |
| Backwards compatibility with Zipkin | Flexible query interface to build your own UIs                                                                                                                                                  |
|                                     | OLAP store is pluggable with abstractions (need to add request handlers in QueryService)                                                                                                        |
|                                     | Scales out of the box                                                                                                                                                                           |
