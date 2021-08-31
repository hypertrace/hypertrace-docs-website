---
title: What is Hypertrace?
subtitle: >-
  Hypertrace is an open source, real-time, distributed tracing & observability platform
excerpt: >-
  Hypertrace converts distributed trace data into relevant insight for everyone. Infrastructure teams can identify which services are causing overload. Service teams can diagnose why a specific user's request failed, or which applications put their service objectives at risk. Deployment teams can know if a new version is causing a problem.
template: docs

---
Hypertrace is a real-time observability platform that helps teams make sense of
their production requests and trends within their network.

Hypertrace converts distributed trace data into relevant insight for everyone.
Using Hypertrace your infrastructure team can identify the services that are causing an overload. Your service
team can diagnose why a specific user's request failed, or which applications
put their service objectives at risk. Deployment teams can know if a new
version is causing a problem.

Hypertrace is an open source licensed product that accepts all major tracing data formats. This would help you to try it without changing your application.


# Features

Hypertrace is open source and includes features commonly present in distributed
tracing systems such as a cloud-native backend and a UI. Hypertrace goes beyond and 
includes features that are usually available in commercial products. Hypertrace, for example, provides you with no additional configuration, service graph and metrics aggregation in real time, custom dashboards, and sophisticated path-based analysis. 

The following tables provides a high-level overview of the basic and some important features that Traceable provides.

## Basic features

| Feature                 | Description                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------- |
| Trace UI                | Visualization for a request's path through services and any backends, including context, errors, and delays  |
| Application Flow UI     | Service graph visulatization of all the traced traffic in your network                                     |
| Cloud Native Deployment | Kubernetes cluster with Helm Charts to install and manage                                         |


## Notable features
The below features are available by default in Hypertrace, but are not usually included in Open Source distributed tracing systems.

| Feature                 | Description                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| Dashboard UI            | Global health including most frequently called endpoints, services, and backends              |
| Services UI             | Service owners can see health and latency overview of their endpoints and corresponding dependencies |
| Backend UI              | Owners of backends like MySQL or Redis can quickly identify slow queries and identify trends |
| Built-in Rosetta Stone  | Natively understands all major trace data formats like OpenTelemetry, Jaeger, and Zipkin |
| Sampling unnecessary    | Native design to ingest 100% request traces. No need for a sampling collector.        |
| Real-time processing    | Using stream processing, application flow and metrics aggregate automatically.           |

***
