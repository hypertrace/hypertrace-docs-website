---
title: Getting Started
excerpt: In this section you'll find basic information about Libris and how to use it.
template: docs
---
### Requirements
- `Docker desktop` (version 2.2.x and above) with `Kubernetes` enabled.
- Minimum resources for Docker: (2 CPUs, 4GB Memory).
Following is the snapshot of resources used of a typical hypertrace standalone deployment.

    | Resource          | Requests        | Limits        |
    |-------------------| ---------------:| -------------:|
    | cpu               | 1850m (46%)     | 2700m (67%)   |
    | memory            | 4084Mi (41%)    | 6472Mi (65%)  |
    | ephemeral-storage | 0 (0%)          | 0 (0%)        |


- `Helm` (version 3.2.x and above)
- Bash
- Ineternet connectivity to pull the hypertrace helm charts and docker images
- Basic understanding of kubernetes and helm

## Instrumentation
Your application must be instrumented before it can send tracing and monitoring data to any currently supported backend including OpenTracing, OpenCensus, Jaeger and zipkin. 

***

Here are the articles in this section:
