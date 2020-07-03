---
title: Python Jaeger Exporter
weight: 2.1
template: docs
---
### Introduction
Jaeger, inspired by Dapper and OpenZipkin, is a distributed tracing system released as open source by Uber Technologies.
It is used for monitoring and troubleshooting microservices-based distributed systems, including:

* Distributed context propagation
* Distributed transaction monitoring
* Root cause analysis
* Service dependency analysis
* Performance / latency optimization

OpenCensus Python has support for this exporter available through package [opencensus.trace.exporters.jaeger_exporter](https://github.com/census-instrumentation/opencensus-python/blob/master/opencensus/trace/exporters/jaeger_exporter.py)



### Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Jaeger endpoint available to receive traces
 
```python
#!/usr/bin/env python

from opencensus.ext.jaeger.trace_exporter import JaegerExporter
from opencensus.trace.tracer import Tracer

def main():
    je = JaegerExporter(
        service_name="service-b",
        host_name="localhost",
        agent_port=6831,
        endpoint="/api/traces")

    tracer = Tracer(exporter=je)
    with tracer.span(name="doingWork") as span:
        for i in range(10):
            pass

if __name__ == "__main__":
    main()
```
 
### Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost).

### Project link
You can find out more about the Jaeger project at [https://www.jaegertracing.io/](https://www.jaegertracing.io/)


[Edit this page](https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/python/py-jaeger.md)