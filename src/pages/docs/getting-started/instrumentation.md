---
title: Instrumentation
weight: 2
template: docs
---
## Introduction
Your application must be instrumented before it can send tracing and monitoring data to hypertrace using any supported collector including OpenTracing, OpenCensus, Jaeger and zipkin.  Let's see what is instrumentation and how you can instrument your application for distributed tracing. 

### What is Instrumentation?
As per the paper titles *Software Instrumentation* by Torsten Kempf, Kingshuk Karuri
and Lei Gao, *Software instrumentation is a technique that is widely used in software profiling, performance analysis, optimization, testing, error detection, and virtualization. Instrumentation, which involves adding extra code to an application for monitoring some program behavior, can be performed either statically (i.e., at compile time) or dynamically (i.e., at runtime).*

### Agent vs Library

| Agent                                                                                                                                                                                                                          | Library                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Black-box approach                                                                                                                                                                                                             | White-box approach                                                                                                                                                                       |
| Agent-based instrumentation relies on some sort of external process to track your application processes at runtime.                                                                                                            | A library-based instrumentation approach can be characterized by its reliance on an application-level dependency on some shared, standardized code that is used throughout its services. |
| Agents can be an external process or monitoring service that injects code into your service or some sort of in-process agent that is imported to the runtime environment of a process and uses a system of user-defined rules. | This approach generally relies on developers to write instrumentation code.                                                                                                              |

## Let's get started with Instrumentation with example
### Learning objectives
- Learn to create some python flask api based microservices and make them call each other. 
- Learn to instrument basic microservice app
- Learn to deploy microservice application with kubernetes. 

### Tools we will be using
1. Python
2. Flask: Flask is a popular, extensible web microframework for building web applications with Python.
3. Kubernetes

### Let's understand application flow and code

This application is based on sample application available [here](https://github.com/MohamedMSaeed/tracing_flask_zipkin). 

Architecture for our final application will look something like below:

![](https://miro.medium.com/max/1400/1*fJBmBYPBrCVwbbfDucCmtw.png)

#### How it works?

We have 3 flask API's here. API-1 communicates with API-2 and API-3 and API-2 talks to API-3. We are trying to implement classic microservices scenario here. Let's look a bit into those API's:

1. API-1

```python
@app.before_request
def log_request_info():
    app.logger.debug('Headers: %s', request.headers)
    app.logger.debug('Body: %s', request.get_data())


@zipkin_client_span(service_name='api_01', span_name='call_api_02')
def call_api_02():
    headers = create_http_headers()
    # k8s does not allow underscores in the service name
    requests.get('http://api-02:5000/', headers=headers)
    return 'OK'


@zipkin_client_span(service_name='api_01', span_name='call_api_03_FROM_01')
def call_api_03():
    headers = create_http_headers()
    requests.get('http://api-03:5000/', headers=headers)
    return 'OK'

```

API-1 here as expected accepts the requests and calls API-2 and API-3 as expected.

2. API-2

```python

@zipkin_client_span(service_name='api_02', span_name='call_api_03')
def call_api_03():
    headers = create_http_headers()
    requests.get('http://api-03:5000/', headers=headers)
    return 'OK'

```

API-2 here calls API-3.

3. API-3

```python
@zipkin_client_span(service_name='api_03', span_name='sleep_api_03')
def sleep():
    time.sleep(2)
    return 'OK'

```

API-3 is very lazy and it just sleeps!

4. Span Handler

You can use create span handler as follows:
```python
def default_handler(encoded_span):
    body = encoded_span
    app.logger.debug("body %s", body)
    # return requests.post(
    #     "http://zipkin:9411/api/v1/spans",
    #     data=body,
    #     headers={'Content-Type': 'application/x-thrift'},
    # )

    # return requests.post(
    #     "http://zipkin:9411/api/v2/spans",
    #     data=body,
    #     headers={'Content-Type': 'application/json'},
    # )

    return requests.post(
        "http://oc-collector.hypertrace:9411/api/v2/spans",
        data=body,
        headers={'Content-Type': 'application/json'},
    )
```

5. Defining attributes

You can set attributes you want in spans using module `ZipkinAttrs` from `py_zipkin` as follows
```python
zipkin_attrs=ZipkinAttrs(
            trace_id=request.headers['X-B3-TraceID'],
            # Start a new SERVER span whose parent is the span in the headers
            span_id=generate_random_64bit_string(),
            parent_span_id=request.headers['X-B3-SpanID'],
            flags=1,
            is_sampled=request.headers['X-B3-Sampled'],
        )
```

So, Now we have flask apps and we know the flow, how should we deply our apps?

Let's create a dockerfile which will help us to build docker container to run the app!

```python
From python:3.7

COPY ./requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install -r requirements.txt

COPY . /app

ENTRYPOINT [ "python" ]

CMD [ "app.py" ]
```

once we run docker build for each app we will get docker images for each microservice or API. We can create a kubernetes deployment with this apps and get this app runnning with kubernetes but first thing we need for this is yaml file. 

Let's start creating yaml file:

```python 
apiVersion: v1
kind: Namespace
metadata:
  name: simple-python

# app_01
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: simplepython
  namespace: simple-python
spec:
  replicas: 1
  selector:
    matchLabels:
      app: simplepython
  template:
    metadata:
      labels:
        app: simplepython
    spec:
      containers:
      - name: simplepython
        image: python_app_01:0.1.0
---
apiVersion: v1
kind: Service
metadata:
  name: api-01
  namespace: simple-python
spec:
  type: ClusterIP
  selector:
    app: simplepython
  ports:
  - name: http
    port: 5000
    targetPort: 5000
---
apiVersion: v1
kind: Service
metadata:
  name: simplepython-external
  namespace: simple-python
spec:
  type: LoadBalancer
  selector:
    app: simplepython
  ports:
  - name: simplepython-external-port
    port: 5001
    targetPort: 5000
```

Similary you can add API-2 and API-3 and you have your yaml file ready.

Now just go to your console and run `kubectl apply -f deploy.yaml` once all pods are up and running access API-1 at `localhost:5001` and you have successfully deployed your first microservice app!

Was it fun? 

Learn more about microservices at microservices.io and if you want to checkout more cool and complex samples you can visit our colletion of best microservices below:

1. [Online Boutique Demo](https://github.com/JBAhire/HyperTrace-samples/blob/master/blog/onlineboutique.md)
2. [Sock shop demo](https://github.com/JBAhire/HyperTrace-samples/blob/master/blog/sockshop.md)
3. [TODO list demo](https://github.com/JBAhire/HyperTrace-samples/blob/master/blog/todolist.md)
4. [HotROD app](https://github.com/JBAhire/HyperTrace-samples/blob/master/blog/hotrod.md)

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/getting-started/instrumentation.md">
<button type="button">Edit</button></a>

***
