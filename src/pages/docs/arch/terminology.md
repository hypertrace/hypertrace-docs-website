---
title: Terminology
weight: 1
template: docs
---
Hypertrace supports OpenTracing standard which is being followed by most of the Distributed tracing platforms available in market. It gives Hypertrace ability to fetch traces from all available collectors and work as a single aggregator. 

Let's start with undertsanding some basic terms around distributed tracing as per the [specifications](https://github.com/opentracing/specification/edit/master/specification.md) defined by OpenTracing.

### Spans
The “span” is the primary building block or a logical unit of a distributed trace, representing an individual unit of work done in a distributed system.

Each component of the distributed system contributes a span - a named, timed operation representing a piece of the workflow. Multiple spans assemble to become a trace. Each span has it's own `operation name` along with a `start and finish timestamp`, `A set key:value span Tags`, `A set key:value span logs ` and `A SpanContext`. 

#### Tags
Tags are key:value pairs that enable user-defined annotation of spans in order to query, filter, and comprehend trace data.

#### Logs
Logs are key:value pairs that are useful for capturing span-specific logging messages and other debugging or informational output from the application itself. 

#### SpanContext
Each SpanContext encapsulates the following state:

- Any OpenTracing-implementation-dependent state (for example, trace and span ids) needed to refer to a distinct Span across a process boundary
- Baggage Items, which are just key:value pairs that cross process boundaries

### Traces
**Traces** in OpenTracing are defined implicitly by their **Spans**. In particular, a **Trace** can be thought of as a directed acyclic graph (DAG) of **Spans**, where the edges between **Spans** are called **References**.

For example, the following is an example **Trace** made up of 8 **Spans**:

~~~
Causal relationships between Spans in a single Trace


        [Span A]  ←←←(the root span)
            |
     +------+------+
     |             |
 [Span B]      [Span C] ←←←(Span C is a `ChildOf` Span A)
     |             |
 [Span D]      +---+-------+
               |           |
           [Span E]    [Span F] >>> [Span G] >>> [Span H]
                                       ↑
                                       ↑
                                       ↑
                         (Span G `FollowsFrom` Span F)

~~~
Sometimes it's easier to visualize **Traces** with a time axis as in the
diagram below:

~~~
Temporal relationships between Spans in a single Trace


––|–––––––|–––––––|–––––––|–––––––|–––––––|–––––––|–––––––|–> time

 [Span A···················································]
   [Span B··············································]
      [Span D··········································]
    [Span C········································]
         [Span E·······]        [Span F··] [Span G··] [Span H··]
~~~

### Collector

Collector receives traces from various agents in our case Hypertrace can collect traces from Jaeger, Zipkin, OpenCensus and OpenTelemetry agents. 

### Ingester
Ingester is a service that reads from Kafka topic and writes to another storage backend (Cassandra, Elasticsearch).

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/arch/terminology.md">
<button type="button">Edit</button></a>
***
