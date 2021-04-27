---
title: Python Instrumentation
subtitle: Instrument your Go application with Hypertrace Python agent or OpenTelemetry Python agent. 
weight: 3
template: docs
---

## Instrument your Python application with Hypertrace Python agent

Hypertrace Python agent is the Hypertrace's distribution of [OpenTelemetry Python agent](https://github.com/open-telemetry/opentelemetry-python).

| ![space-1.jpg](https://raw.githubusercontent.com/hypertrace/pythonagent/main/images/HyperTrace%20Agent%20Architecture.jpg) | 
|:--:| 
| *Hypertrace Python Agent* |


### Supported frameworks and modules
This agent supports these frameworks and adds following capabilities:

* capture request and response headers
* capture request and response bodies
* context propagation/tracing

| Module/Framework | Description | Python Versions Tested/Supported|
|------|-------------| ---------------|
| [flask](https://flask.palletsprojects.com/en/1.1.x/api)|A micro web framework written in Python.| Python 3.7, 3.8, 3.9|
| [grpc](https://grpc.github.io/grpc/python/)|Python GRPC library.| Python 3.7, 3.8, 3.9|
| [mysql-connector](https://dev.mysql.com/doc/connector-python/en/)| Python MySQL database client library.| Python 3.7, 3.8, 3.9|
| [psycopg2/postgresql](https://www.psycopg.org/docs/)|Python Postgresql database client library. | Python 3.8, 3.9|
| [requests](https://docs.python-requests.org/en/master/)|Python HTTP client library.| Python 3.7, 3.8, 3.9|
| [aiohttp](https://docs.aiohttp.org/en/stable/)|Python async HTTP client library.| Python 3.7, 3.8, 3.9|

### Geting started
Currently, this agent does not support auto-instrumentation. That will be available in a future release. In the meantime, the following code snippet must be added to the entry point of your python application.

* Install the hypertrace python agent:
```
pip install git+https://github.com/hypertrace/pythonagent.git@main
```
* Enter your github.com username and password when prompted.
* Add the following to your app's entrypoint python file:
``` python
from hypertrace.agent import Agent


# Code snippet here represents the current initialization logic
# 
# Only add the register functions for instrumentation modules your
# application uses

logger.info('Initializing agent.')
agent = Agent()
agent.registerFlaskApp(app) # app is your Flask application object
agent.registerMySQL()
agent.registerPostgreSQL()
agent.registerRequests()
agent.registerAioHttp()
agent.registerGrpcServer()

# End initialization logic for Python Agent

```

### Configure using Environment Variables

| Name | Description |
|------|-------------|
| HT_SERVICE_NAME | Identifies the service/process running e.g. "my service" |
| HT_REPORTING_ENDPOINT | Represents the endpoint for reporting the traces For ZIPKIN reporter type use http://api.traceable.ai:9411/api/v2/spans For OTLP reporter type use http://api.traceable.ai:4317 |
| HT_REPORTING_SECURE | When `true`, connects to endpoints over TLS. |
| HT_REPORTING_TOKEN | User specific token to access Traceable API |
| HT_DATA_CAPTURE_HTTP_HEADERS_REQUEST | When `false` it disables the capture for the request in a client/request operation |
| HT_DATA_CAPTURE_HTTP_HEADERS_RESPONSE | When `false` it disables the capture for the response in a client/request operation |
| HT_DATA_CAPTURE_HTTP_BODY_REQUEST | When `false` it disables the capture for the request in a client/request operation |
| HT_DATA_CAPTURE_HTTP_BODY_RESPONSE | When `false` it disables the capture for the response in a client/request operation |
| HT_DATA_CAPTURE_RPC_METADATA_REQUEST | When `false` it disables the capture for the request in a client/request operation |
| HT_DATA_CAPTURE_RPC_METADATA_RESPONSE | When `false` it disables the capture for the response in a client/request operation |
| HT_DATA_CAPTURE_RPC_BODY_REQUEST | When `false` it disables the capture for the request in a client/request operation |
| HT_DATA_CAPTURE_RPC_BODY_RESPONSE | When `false` it disables the capture for the response in a client/request operation |
| HT_DATA_CAPTURE_BODY_MAX_SIZE_BYTES | Maximum size of captured body in bytes. Default should be 131_072 (128 KiB). |
| HT_PROPAGATION_FORMATS | List the supported propagation formats e.g. `HT_PROPAGATION_FORMATS="B3,TRACECONTEXT"`. |
| HT_ENABLED | When `false`, disables the agent. |
| HT_LOG_LEVEL | Represents log level. |
| HT_TRACES_EXPORTER | Collector to export traces to e.g `Zipkin`. |
| HT_ENABLE_CONSOLE_SPAN_EXPORTER| Enable the Console Span Exporter for debugging purposes.|
| HT_CONFIG_FILE | When `HT_CONFIG_FILE` is specified in the environment configuartion information is loaded from that location. |

## Instrument your Python application with OpenTelemetry Python 

### Getting started
You will need to install OpenTelemetry API and SDK to get started with instrumentation. To install OpenTelemetry Python API and SDK run:

```
pip install opentelemetry-api
pip install opentelemetry-sdk
```
- The API package provides the interfaces required by the application owner, as well as some helper logic to load implementations.

- The SDK provides an implementation of those interfaces. The implementation is designed to be generic and extensible enough that in many situations, the SDK is sufficient.

Once installed, you can use the packages to emit spans from your application. A span represents an action within your application that you want to instrument, such as an HTTP request or a database call. Once instrumented, you can extract helpful information such as how long the action took. You can also add arbitrary attributes to the span that provide more insight for debugging.

```python
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import (
    ConsoleSpanExporter,
    SimpleSpanProcessor,
)

provider = TracerProvider()
processor = SimpleSpanProcessor(ConsoleSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)


tracer = trace.get_tracer(__name__)

with tracer.start_as_current_span("foo"):
    with tracer.start_as_current_span("bar"):
        with tracer.start_as_current_span("baz"):
            print("Hello world from OpenTelemetry Python!")
```

When you run the program, you can see traces printed on your console like below. 

```
$ python tracing_example.py
{
    "name": "baz",
    "context": {
        "trace_id": "0xb51058883c02f880111c959f3aa786a2",
        "span_id": "0xb2fa4c39f5f35e13",
        "trace_state": "{}"
    },
    "kind": "SpanKind.INTERNAL",
    "parent_id": "0x77e577e6a8813bf4",
    "start_time": "2020-05-07T14:39:52.906272Z",
    "end_time": "2020-05-07T14:39:52.906343Z",
    "status": {
        "status_code": "OK"
    },
    "attributes": {},
    "events": [],
    "links": []
}
{
    "name": "bar",
    "context": {
        "trace_id": "0xb51058883c02f880111c959f3aa786a2",
        "span_id": "0x77e577e6a8813bf4",
        "trace_state": "{}"
    },
    "kind": "SpanKind.INTERNAL",
    "parent_id": "0x3791d950cc5140c5",
    "start_time": "2020-05-07T14:39:52.906230Z",
    "end_time": "2020-05-07T14:39:52.906601Z",
    "status": {
        "status_code": "OK"
    },
    "attributes": {},
    "events": [],
    "links": []
}
{
    "name": "foo",
    "context": {
        "trace_id": "0xb51058883c02f880111c959f3aa786a2",
        "span_id": "0x3791d950cc5140c5",
        "trace_state": "{}"
    },
    "kind": "SpanKind.INTERNAL",
    "parent_id": null,
    "start_time": "2020-05-07T14:39:52.906157Z",
    "end_time": "2020-05-07T14:39:52.906743Z",
    "status": {
        "status_code": "OK"
    },
    "attributes": {},
    "events": [],
    "links": []
}
```

## Auto Instrument your Python application using OpenTelemetry Python 

Auto-instrumentation is simple, easy, and doesn't require many code changes so it's one of the simplest and best ways to instrument your Python applications. You only need to install a few Python packages to successfully instrument your application's code.

You can find more details as well as examples around Python OpenTelemetry auto-instrumentation [here](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples/auto-instrumentation). 

