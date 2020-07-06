---
title: Python Zipkin Exporter
weight: 2.2
template: docs
---
### Introduction
Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures.

It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

OpenCensus Python has support for this exporter available through package [opencensus.trace.exporters.zipkin_exporter](https://census-instrumentation.github.io/opencensus-python/trace/api/zipkin_exporter.html)


### Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Zipkin endpoint available to receive traces
 
```python
#!/usr/bin/env python

from opencensus.ext.zipkin.trace_exporter import ZipkinExporter
from opencensus.trace.tracer import Tracer

def main():
    ze = ZipkinExporter(
        service_name="service-a",
        host_name="localhost",
        port=9411,
        endpoint="/api/v2/spans")

    tracer = Tracer(exporter=ze)
    with tracer.span(name="doingWork") as span:
        for i in range(10):
            pass

if __name__ == "__main__":
    main()
```
 

### Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost).

### Project link
You can find out more about the Zipkin project at [https://zipkin.io/](https://zipkin.io/)


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/go/py-jaeger.md">
<button type="button">Edit</button></a>