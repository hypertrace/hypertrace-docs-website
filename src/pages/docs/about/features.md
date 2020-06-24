---
title: Features
weight: 1
template: docs
---

# Hypertrace Features
Hypertrace is highly efficeint platform and it comes up with many features out of the box. Hypertrace has some key benefits over other platforms. Some of the value propositions of hypertrace as compared to similar open source offerings are as follows:
- Flow map at scale. Jaeger only supports the flowmap with all-in-one setup, which isn’t production scale. For production, one needs to run separate Spark jobs to generate the dependency graph.
- APIs detected automatically. Flowmaps and metrics for APIs.
- Metrics and flowmaps for Services
- API host (or Domain) level metrics and traces
- Basic APM product around Services and APIs 
- API Analytics with slice & dice around APIs
- Flexible query interface to build your own UIs
- OLAP store is pluggable with abstractions (need to add request handlers in QueryService)

On high level here are some features we are looking at:

- Discover Mapping
    - Distributed Tracing & Correlation - End-to-end distributed tracing of all internal microservice/backend calls triggered by the edge API calls and web transactions
    - Application Flow Mapping - Real-time discovery and visualization of end-to-end application topology
- Monitor
    - Web Transaction Monitoring - Monitor all web transactions at Web Proxies
    - Microservice Monitoring - Monitor all internal micro-service calls
    - Backends Monitoring - Monitor all calls to backend systems like databases or third-party services
    - End User Monitoring - Monitor end-user calls
- Explore (or perhaps Visualize or Investigate)
    - Trace Filtering & Visualizations - Search & visualize any traces
    - Advanced Slice & Dice - Create any aggregation and grouping of traces

Let's look at some features in details:

## 1. Aggregations
Hypertrace explorer provides you bunch of different ways to aggregate your API's and traces. The Search bar has so many different parameteres you can search on and you can even use multiple parameters which will give you aggregations based on specific criteria. 

## 2. Slice and dice
Hypertrace provides you ability to slice and dice traces to derive advanced insights. 

## 3. High Scalability
Unlike most of the current open source solutions Hypertrace supports scaling out-of-the box and it can scale for large production level deployments. You can rely on Hypertrace to scale according to your business needs. 

## 4. Native suppport for different OpenCesnus, Jaeger, Zipkin and OpenTelemetry to send and receive traces
So you have your application already instrumented for tracing with Jaeger, Zipkin or any other platform that supports and relies on OpenTracing API? No worries! Hypertrace can identify traces from this platforms and can show these traces in hypertrace with bunch of different functionalities available out-of-the box.

## 5. Multiple storage backends
Hypertrace supports all major backend by default. 

## 6. UI you can fall in love with
Hypertrace comes with a beutiful & Modern UI which makes every UI component more informative and useful for analysing your application.

## 7. Coud Native Deployments
Hypertrace backend is distributed as a kubernetes deployment with helm charts and installation script.

## 8. Observability & Multiple APM features
Hypertrace has variour observability metrics on dashboard as well as at various places throughout the platform wherever you will need to look at them. Hypertrace supports multiple APM features out of the box like it detects frontend or customer in your application automatically.

## 9. Multiple ways to build and use
There are multiple ways you can build or deploy hypertrace and you can find details in Installation docs. 
