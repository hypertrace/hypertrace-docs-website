---
title: Go Jaeger
template: page
---
# Jaeger Exporter

## Introduction
Jaeger, inspired by Dapper and OpenZipkin, is a distributed tracing system released as open source by Uber Technologies.
It is used for monitoring and troubleshooting microservices-based distributed systems, including:

* Distributed context propagation
* Distributed transaction monitoring
* Root cause analysis
* Service dependency analysis
* Performance / latency optimization

OpenCensus Go has support for this exporter available through package [contrib.go.opencensus.io/exporter/jaeger](https://godoc.org/contrib.go.opencensus.io/exporter/jaeger)


## Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Jaeger endpoint available to receive traces
```go
package main

import (
	"log"

	"contrib.go.opencensus.io/exporter/jaeger"
	"go.opencensus.io/trace"
)

func main() {
	// Port details: https://www.jaegertracing.io/docs/getting-started/
	agentEndpointURI := "localhost:6831"
	collectorEndpointURI := "http://localhost:14268/api/traces"

	je, err := jaeger.NewExporter(jaeger.Options{
		AgentEndpoint:          agentEndpointURI,
		CollectorEndpoint:      collectorEndpointURI,
		ServiceName:            "demo",
	})
	if err != nil {
		log.Fatalf("Failed to create the Jaeger exporter: %v", err)
	}

	// And now finally register it as a Trace Exporter
	trace.RegisterExporter(je)
}
```
## Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost](http://localhost)

## Project link
You can find out more about the Jaeger project at [https://www.jaegertracing.io/](https://www.jaegertracing.io/)
