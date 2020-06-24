---
title: About
excerpt: >-
  Libris is a Unibit theme created for project documentations. You can use it
  for your project.
template: docs
---

# Introduction
It's been a while since we started moving from monolithic applications to microservices based architecture. When you look at systems today you will find that this modern distributed services are large, complex, and increasingly built upon other similarly complex distributed services. 

Most of the tech giants including companies like Amazon, Netflix, started to build their systems using a monolithic architecture because back in the time it was much faster to set up a monolith and get the business moving. But over the time as business or product matures, with growing system the code gets more and more complicated. maturing projects or fat growth. With the system’s growth, the code gets more complicated. They all faced this problem and looked at microservices as a solution. One of the biggest benefits of microservices is that each microservice can be developed, scaled, and deployed separately. You can replace or upgrade any part of system independently. Everyone started adopting microservices and here we are today looking at complex modern architectures. 

![](https://divante.com/blog/wp-content/uploads/2019/07/Frame-25.png)
*Image by [divante.com](https://divante.com/blog/10-companies-that-implemented-the-microservice-architecture-and-paved-the-way-for-others/)*

What do you think the above images are? No! they are not some fancy circles or death star. They are structures of microservices at Amazon and Netflix respectively. This might have gave you idea about level of complexity we are talking here!

You can't simply go ahead and use traditional machine-centric monitoring and tracing mechanisms for management and development tasks in such a complex environments specifically because they are not effective and they cannot provide a coherent view of the work done by a distributed service’s nodes and dependencies. Because of this, tools that aid in understanding system behavior and reasoning about performance issues are invaluable in such a complex environment. 

## Introducing Distributed Tracing!

There are multiple tools developed by multiple communities and developers to solve this problem and we will be looking at one such tool, *Distributed Tracing* ! Distributed tracing, also called distributed request tracing, is particularly well-suited to debugging and monitoring modern distributed software architectures, such as microservices. It helps pinpoint where failures occur and what causes sub-optimal performance.

**Distributed tracing** is the idea of tracing a network request as it travels through your services, as it would be in a microservices-based architecture. One of the main reason you may want to do this is to troubleshoot or monitor the latency of a request as it travels through the different services.

Distributed tracing requires the software developers to add instrumentation to the code of an application. That instrumentation provides information so that the administrator can analyze performance and the developer can debug the operations of complex software.

If you want to know more about Distributed Tracing terminology, please visit this [page](Terminology.md).


# What is Hypertrace?
Hypertrace is a highly scalable distributed tracing and observability platform designed to ingest and analyze large volumes of production trace data. OpenTelemetry-based agents collect and send observability data directly from applications to Hypertrace for analysis. Data visualizations, reports, and dashboards are available in a web-based console to assist in monitoring cloud-native applications and resolving application and service performance problems.


***

Here are the articles in this section:
