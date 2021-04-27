---
title: Instrumentation
excerpt: Learn about instrumentation in this section. 
template: docs
---

Instrumentation assists you in monitoring or measuring the performance and state of an application. Hypertrace supports all standard instrumentation libraries and agents so if your application is already instrumented with OpenTelemetry, Jaeger or Zipkin, Hypertrace will work out of the box with your application telemetry data. 

## Instrumentation with Hypertrace agents
Hypertrace also provides open-source OpenTelemetry based agents for some popular languages and we are adding more languages going ahead. These agents can work with any platform that supports OpenTelemetry.

If you want to learn more about Hypertrace agents, please follow the guides below. 
- [Java Agent](https://docs.hypertrace.org/instrumentation/java-agent/)
- [Go Agent](https://docs.hypertrace.org/instrumentation/go-agent/)
- [Python Agent](https://docs.hypertrace.org/instrumentation/python-agent/)

Though we recommend using Hypertrace Agent if you are getting started with Hypertrace and want best experience but it's not necessary. As long as you are using any open-standard for instrumentation, Hypertrace will be help you understand your application. 

## Instrumentation with OpenTelemetry
OpenTelemetry is a collection of tools, APIs, and SDKs. You can use it to instrument, generate, collect, and export telemetry data (metrics, logs, and traces) for analysis in order to understand your software's performance and behavior. OpenTelemetry provides vendor-agnostic or vendor-neutral way to collect and export telemetry data. OpenTelemetry supports both Auto Instrumentation as well as Manual Instrumentation. 

You can read more about OpenTelemetry instrumentation [here](https://opentelemetry.io/docs/concepts/instrumenting/). Below is the list of list of all language specific SDKs of OpenTelemetry. 

- [Java](https://github.com/open-telemetry/opentelemetry-java-instrumentation)
- [Go](https://github.com/open-telemetry/opentelemetry-go)
- [Python](https://github.com/open-telemetry/opentelemetry-python)
- [NodeJS](https://github.com/open-telemetry/opentelemetry-js)
- [C++](https://github.com/open-telemetry/opentelemetry-cpp)
- [.NET](https://github.com/open-telemetry/opentelemetry-dotnet-instrumentation)

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/blob/master/src/pages/instrumentation/index.md">
<button type="button">Edit</button></a>

***

