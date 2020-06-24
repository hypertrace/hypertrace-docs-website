---
title: Java Agent
weight: 1
template: docs
---
# Hypertrace: Java Agent
## Introduction

This describes the features and architecture of the Java Agent
Features

The agent is essentially a plugin system with core services and additional capabilities for:

    Hot Reload - Ability to upgrade an agent without requiring a JVM restart
    Hot Pluggable - Ability to add plugins dynamically and reload them without requiring a JVM restart


## Architecture

https://api.media.atlassian.com/file/4cb2fa31-df67-4156-81d3-1821ceac9002/image?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJkNGI3NjlhNS0zZDg2LTRkODEtOGJlOC0wZjYwMDZmZjk4OWIiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjRjYjJmYTMxLWRmNjctNDE1Ni04MWQzLTE4MjFjZWFjOTAwMiI6WyJyZWFkIl19LCJleHAiOjE1OTI4Mjk3MjksIm5iZiI6MTU5MjgyNjY2OX0.za0D_L9kUDwU0CR5Cqv1r1NPw7O0LAoEqIRTXCYUHfM&client=d4b769a5-3d86-4d81-8be8-0f6006ff989b&name=java-agent-arch-1.jpg&max-age=2940&height=400


[Engineering > Java Agent > java-agent-arch-1.jpg]



### The agent is basically made up of a CORE component that contains agent services and extension points
- Core - this is the main kernel that orchestrates the core services, plugins manager and other dependency injection services
- Service - the core provides certain services like managed thread pools, lifecycle management, dependency injection and plugins management
- Extension Point - these are interfaces that can be extended via plugins
- Extension - an extension implements an extension point and is typically provided by plugins
- Plugin - a plugin is essentially a package that can provide an extension. Examples include instrumentation, tracing, health-check, reporting etc


## Bootstrap Sequence Flow
- The attach (Remote or Local) typically happens on the main application thread that is associated with the system/app classloader
- On attach the AgentLoader will create a new daemon Control Thread. The control thread will always be available and will provide a command shell/http endpoint for admin/interrogation
- Next the control thread will initialize the AgentLogger. It will load the necessary logging implementation jars in a separate classloader. This is done to provide for the capability to upgrade this if needed. Details TBD
- Next the bootstrap jars are added to the Bootstrap classloader search path as these will be needed by classes loaded by Bootstrap loader
- Next the Agent Kernel (CORE) is loaded. 
    - Core services like lifecycle manager, plugin manager, thread pools etc are loaded 
    - the plugin manager will initiate loading of various plugins in separate class loaders 
- Next the Kernel (Dependency Injector Service) will inject any dependencies
- The Plugin manager will start watching for any updates for the plugins


## Upgrade Flow

The following is a very high level sketch at this time and details will be updated as progress is made
- If a plugin needs to be upgraded the plugin manager will automatically handle that by firing any listeners so that any other components in the agent can clean up i.e. null any strong references to any of the resources that belong to the plugin so that it can be unloaded and garbage collected. It will then reload a new version in a separate classloader and fire any listeners so that any client code can start using the new plugin
- If we need to upgrade the Agent CORE module then the Control thread can be informed and it will trigger a unload of CORE and all plugins and reload CORE and plugins
- If we need to upgrade the logging implementation then the Control Thread will manage the upgrade
- If we need to upgrade the Control thread then it can load a new implementation of the Control Thread and kill itself.
- To upgrade classes in bootstrap we will need to introduce new classes and have all the dependents use the new classes. We can't unload classes from bootstrap as the Bootstrap loader needs to be closed and unloaded which is not possible. For this reason we must keep the bootstrap classes to a bare minimum so that their footprint is minimal


## Current Modules
#### agent-loader

Entry point to the java agent. It has the premain() and agentmain() methods which the JVM uses to hook into the agent. It also loads the rest of the agent modules.

#### app-data-collector

Collects information about libraries and classes loaded by the application and sends it to the entity data service

#### bootstrap

Classes that are required to bootstrap the agent. For example logging.
#### core

Classes that are common across modules.
#### custom-data-collectors

Custom Instrumentation Configuration
#### custom-data-collectors-ot

A copy of custom-data-collectors module that is OpenTracing based. Any new instrumentation changes should go in here.
#### instrumentation

Instrumentation logic for the various frameworks. We use ByteBuddy to execute the instrumentation and transformation. (See https://bytebuddy.net/#/) . The classes in here are divided into RuleAppliers, Advices and Interceptors

RuleAppliers apply instrumentation rules based on class and method matches

Advices are used to hook up the Interceptors into the method's entry and exit by ByteBuddy.

Interceptors contain the logic to start and stop spans, propagate and extract the tracing context, and also capture data.
#### instrumentation-ot

A copy of the instrumentation module above but OpenTracing based. Any new instrumentation changes should go in here.
#### jaeger-exporter

Exports spans that are in thrift format. Works in conjunction with the OpenCensus tracer at the moment.
#### logging-span-exporter

An exporter that just logs the spans sent out. Could be useful for debugging and needs to be updated to handle new OpenTracing implementation
#### opentracing-impl

An interface for OpenTracing implementation.
#### ot-tracer

Our implementation of an OpenTracing based tracer.
#### tracer

OpenCensus based tracer. We are currently in the process of replacing this with our own implementation of OpenTracing.
#### zipkin-span-reporter

Report zipkin formatted spans to a zipkin endpoint. Since we are fixed on using Jaeger, we dont use this module.
#### test modules

For example test-apps, test-servlet3, test-spring etc. These contain applications that use various frameworks and you can use them to sanity check your instrumentation for a framework. So if you add support for a framework, you can add an app that uses that framework and add the "-javaagent" JAVA_OPTION when running the application.
## Building the Java Agent

Once you have cloned the repo, run `./gradlew build`. If you want a clean build `./gradlew clean build`. After this you should have built each module and the jar will be `<module-name>/build/libs`. The directory `build/modules` will contain the modules that the agent loads. For now you should use only (core-0.1.73-SNAPSHOT.jar,custom-data-collectors-ot-0.1.73-SNAPSHOT.jar,instrumentation_ot-0.1.73-SNAPSHOT.jar,ot-tracer-0.1.73-SNAPSHOT.jar). 0.1.73-SNAPSHOT is the version when these were built. You should delete the rest when you want to use the javaagent. We are in the process of refactoring our instrumentation to use a custom OpenTracing implementation that's why we have this inconvenience.

If you are making changes and rebuilding the agent, you can go to the build.gradle.kts of the modules that you are not using, look for and comment out "dependsOn("deployModule")". This will avoid copying over this module jar to "build/modules" directory. For our purposes(transitioning from OpenCensus to Custom OpenTracing) these are:
```java

app-data-collector/build.gradle.kts
custom-data-collectors/build.gradle.kts
instrumentation/build.gradle.kts
jaeger-exporter/build.gradle.kts
logging-span-exporter/build.gradle.kts
tracer/build.gradle.kts
zipkin-span-reporter/build.gradle.kts
```
## Running a sample Java Application with the agent
### Java Agent Config

The Java Agent consumes a JSON config file with settings such as traces endpoint(jaeger collector), logging and reporting configuration and any other custom tags the customer would want to append to the spans. Here is a sample agent config:

```json
{
  "additional_span_attributes":{
    "cluster_name":"test-cluster",
    "service_name":"tim-spring-sanity",
	"custom_tag_1": "custom-value-1"
  },
  "enabled":true,
  "reporting":{
    "access_key":"",
    "address":"https://saas.traceable.ai",
    "backoff_delay_ms":3000,
    "config_url":"https://saas.traceable.ai/api/config",
    "events_url":"https://saas.traceable.ai:443/api/events",
    "metrics_url":"https://saas.traceable.ai/api/metrics",
    "queue_size":100,
    "retry_on_failure":true,
    "traces_url":"http://localhost:14268/api/traces"
  },
  "service_name":"tim-spring-sanity"
}
```
The config above the root level "service_name" is what the jaeger exporter. For now it is required. So is "traces_url" in reporting.
### From CommandLine
```
#java -javaagent:<agent-loader-build-dir>/libs/agent-loader.jar=traceableBootJarPath=<bootstrap-build-dir>/libs/bootstrap-SNAPSHOT.jar,traceableModulesDir=<modules-dir>,traceableConfigFile=<agent-config-location>/agent_config.json -cp ./build/libs/SimpleJavaProject-1.0.jar com.timtest.demo.Main

# For example
java -javaagent:/Users/tim.mwangi/traceable/javaagent/agent-loader/build/libs/agent-loader.jar=traceableBootJarPath=/Users/tim.mwangi/traceable/javaagent/bootstrap/build/libs/bootstrap.jar,traceableModulesDir=/Users/tim.mwangi/traceable/javaagent/build/modules,traceableConfigFile=/Users/tim.mwangi/traceable/notes/agent_config.json -cp ./build/libs/SimpleJavaProject-1.0.jar com.timtest.demo.Main
```
### From Intellij

Once you have configured your intellij project to run as an Application (Run → Edit Configurations → + → Application), add the "-javaagent" to the "VM Options".
```
-javaagent:<agent-loader-build-dir>/libs/agent-loader.jar=traceableBootJarPath=<bootstrap-build-dir>/libs/bootstrap.jar,traceableModulesDir=<modules-dir>,traceableConfigFile=<agent-config-location>/agent_config.json
```
## Async Patterns
### Activate - Deactivate 

In this pattern the parent span essentially has async segments that continue the parent span and when the last segment ends the parent span also finishes or ends.

SOLUTION: We can support this by simple reference counting i.e. whenever an async task is created we increment reference count of parent by 1. When an async task is finished it reduces the reference count and when it reaches zero the parent span is finished. 


### Fire and Forget 

On the first thread the parent creates async tasks that simply add a reference to the parent. The parent and child are independent and can finish on their own 

```java
final Span parent = tracer.scopeManager().active().span();

executor.submit(
new Runnable() {
@Override
public void run() {
try (Scope child =
	tracer
	.buildSpan("received")
	.addReference(References.FOLLOWS_FROM, parent.context())
	.withTag(Tags.SPAN_KIND.getKey(), Tags.SPAN_KIND_CONSUMER)
	.startActive(true)) {
}
```
### Request/Operation Handler

In this patten server frameworks typically have handlers per operation/request and can be executed on different threads. A good example is event loop based architectures like Vertx

```java
For example: https://www.javatips.net/api/vert.x-master/src/main/java/io/vertx/core/http/impl/ServerConnection.java

processMessage(Object msg){
}

Here we can manually start and stop spans and use some context object to correlate. We will also need to understand the logic inside the loop to track. For example in the above code we have :


if (msg instanceof HttpObject) {

else if (msg instanceof HttpRequest) {

else if (msg instanceof HttpContent) {


So we can check if the obj is HttpRequest for the first time and cache the serverConnection and span created for the request. 

On subsequent calls we can either skip or capture any additional data like we can add a log to the span by correlating the obj with the serverConnection object.


We can then instrument ServerConnection.handleEnd() to mark the end of the span and remove the serverConnection object. 
```

### Custom Data Collectors

Besides built in instrumentations that produce span/trace data, we also want the ability to allow configuration based data collection such as:

- Adding attributes to span that already exists in context of a method
- Ability to create new entry and exit spans, and context propagation

The configuration is meant to be not Java agent specific, and will be used for other agents as well.

Proto specification for the configuration (DRAFT, this will evolve as implementation goes on):
```java
syntax = "proto3";

// TODO move out of agent
option java_package = "ai.traceable.agent.modules.customdatacollectors";

message DataCollectors {
    repeated AttributeCollectors add_attributes_to_existing_spans = 1;

    // TODO custom entry span

    // TODO custom exit span
}

message AttributeCollectors {

    // Which method to gather data from
    Instrumentation method = 1;
    // What data from the method to collect
    repeated Attribute attributes = 2;
}

message Attribute {
    string key = 1;
    GetterChain value = 2;
}

message Instrumentation {
    // full class name including namespace/package name etc.
    string class_name = 1;
    string method_name = 2;
    // TODO add match type to support instrument interface impls etc.
    // TODO How about method overloads? starts_with ends_with matching?
}

message GetterChain {
    StartingObject starting_object = 1;
    repeated Getter getters = 2;
}

message StartingObject {
    enum StartingObjectType {
        THIS = 0;
        ARGUMENT = 1;
    }
    StartingObjectType starting_object_type = 2;

    // ignored if it's of type This
    int32 argument_index = 3;
}

message Getter {
    enum GetterType {
        METHOD_CALL = 0;
        FIELD = 1;
        ARRAY_INDEX = 2;
    }
    GetterType getter_type = 1;
    string name = 2;
    int32 array_index = 3;
    // TODO optimize with oneof?
}

```

Reference: https://traceableai.atlassian.net/wiki/spaces/Engineering/pages/6881281/Java+Agent#JavaAgent-Introduction 




 
