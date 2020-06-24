---
title: Instrumentation
excerpt: >-
  Libris is a Unibit theme created for project documentations. You can use it
  for your project.
template: docs
---
# Introduction
You might have came across this word several times in documentation. Let's discuss why we need to instrument our app in the first place and then we can discuss how you can instrument your app for tracing. 

## What is Instrumentation?
As per the paper titles *Software Instrumentation* by Torsten Kempf, Kingshuk Karuri
and Lei Gao, *Software instrumentation is a technique that is widely used in software profiling, performance analysis, optimization, testing, error detection, and virtualization. Instrumentation, which involves adding extra code to an application for monitoring some program behavior, can be performed either statically (i.e., at compile time) or dynamically (i.e., at runtime).*

Let's consider you have a software or app with multiple services connected to each other or mulitple API's talking to each other if your application relies on managed services. We can considering this all sevices or API's as boxes that talk to each other using RPC calls. 

So if you're writing some software or have already deployed software, you can think of instrumentation as something that will assist you in monitoring or measuring the performance and state of an application. There are various techniques to instrument your application. Static instrumentation techniques range from simple manual techniques to compiler/assembler‐based instrumentation and link‐time or post‐link executable editing. Dynamic instrumentation techniques are often more complex to implement than the static ones, but they can track dynamically linked libraries and indirect branches that are difficult to handle through static instrumentation.

To make it simpler we are looking at Agent based instrumentation and library based intrumentation. 

A library-based instrumentation approach can be characterized by its reliance on an application-level dependency on some shared, standardized library that is used throughout its services and it generally relies on developers to write instrumentation code. Agent-based instrumentation relies on some sort of external process or processes to instrument processes at runtime. Agent can be external process or monitoring service that injects code into your service or some sort of in-process agent that is imported to the runtime environment of a process and uses a system of user-defined rules. When we look into it in a way we can observe that agent based instrumentation is more of a black box approach whereas library based instrumentation is more analogues to white box implementation. 

## Why Instrumentation?
1. Profiling, performance analysis, and programoptimization
2. Programming error detection and debugging.
3. Virtualization
4. Software quality assurance and testing

## How to instrument the application to work with hypertrace?
Hypertrace supports multiple exporters as it can receive traces which are being sent to Jaeger collector, zipkin collector or opencensus collector port out of the box. So, if your application is already implemented for any of these then you are ready to rock with hypertarce. Even if your application is instrumented for any framework that uses OpenTracing API, we are good to go with hypertrace with minimal to no code changes in most cases. 

If your application is not instrumented at all (which is kinda hard to find case this days), You can instrument using some auto-instrumentation agents which can inject code in your service or will use some sort of in-process agent that is imported to the runtime environment of a process and uses a system of user-defined rules. OpenTelemetry supports auto instrumentation and you can send traces from OpenTelemetry to collectors that hypertrace support and use it with hypertrace as of now. We also have java-agent which will help you in instrumenting your code. 




***

Here are the articles in this section:
