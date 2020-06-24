---
title: comparison
weight: 2
template: docs
---

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
