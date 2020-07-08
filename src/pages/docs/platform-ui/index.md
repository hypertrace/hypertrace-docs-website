---
title: UI and Platform Overview
excerpt: >-
  Libris is a Unibit theme created for project documentations. You can use it
  for your project.
template: docs
---
## Hypertrace Dashboard

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) | 
|:--:| 


| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-2.png) | 
|:--:| 
| *Hypertrace Dashboard* |

On the Hypertrace dashboard you can see different observability metrics such as Errors, Error Rates, and Deployment events [what is a development event?]. And beneath that, you can see Top API requests and errors. If you click on an API, you can see more details about the API, such as average latency, calls per minute and other metrics.

Similarly there is another panel for Top Services where you can see which service is getting the greatest number of requests, or which have higher deployment events. If you click on the service you can see which APIs are available from each particular service, traces for those APIs, as well as metrics. 


## Application flow 

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/flow.png) | 
|:--:| 
| *Application Flow with Hypertrace* |

Application Flow gives you an overview of the services in your applications, and the flow of traces between them. In this example, you can see the frontend is sending requests to the ad service, checkout service, shipping service and the product catalog services. And if you hover over a service, Hypertrace will highlight the trace path and other details so you can confirm that it is acting the way they are supposed to act.

## Services
| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/services.png) | 
|:--:| 
| *List of all services in application with Hypertrace* |

Services section in hypertrace shows you all the services your application has and if you increase timeframe you can even see list of all services sent traces to hypertrace in last few hours or even days. 

## Service details

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/service-dash.png) | 
|:--:| 
| *Frontend microservice details with Hypertrace* |

In the microservices tab you will see all of the microservices from your application listed (obviously). Clicking on a microservice gives you an overview of that microservice. For example, clicking on the frontend service will display an overview of its overall performance metrics, a chart of its recent calls, errors and avg latency, a service profile, as well as a service graph diagram of the services it sends requests to, and the top APIs. 

Next, on the APIs tab, you will see a list of all of the APIs contained by the frontend microservice. Clicking on one of the APIs lets you drill down into that API. For example, clicking on /cart will display an overview that looks similar to the microservice overview, but with details specific to the /cart API. 


## Traces

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/traces.png) | 
|:--:| 
| *Tracing with Hypertrace* |

On the Traces tab you can see a list of traces. There can be millions of traces, so search is an important feature. There are many parameters you can search on, such as tag, status, duration, apiTraceid, apiName, etc. You can combine parameters to help you narrow down your search. For example you might want to search for a specific apiName where the trace took more than 100 ms. To do this you would specify apName = /cart, duration >= 100.     
If you click on any of the traces you will see the classic waterfall graph which shows how a trace proceeds through it’s sequence from one request to the next. Here you can see a list of requests made by a /cart trace, in the order that each request was made, and with the duration of each request. This could help you discover exactly which call in the full trace caused the slow response. 


## Explorer

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/explore.png) | 
|:--:| 
| *Hypertrace Explorer* |

As with most Distributed Tracing platforms, the Hypertrace Explorer helps you identify problems in your application. It starts by showing you the number of calls per time frame. And Explorer comes with many searchable parameters. For example you can specify a startTime and endTime to search for an error your customer said they experienced. 
As you can see, Hypertrace has been collecting traces from the sample application. You can use the timeline feature to see some metrics for predetermined time periods. You can also set your own custom time range. 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/platform-ui/index.md">
<button type="button">Edit</button></a>

***

Here are the articles in this section:
