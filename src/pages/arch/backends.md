---
title: Storage Backends
weight: 3
template: docs
---

## Introduction
We are using real-time OLAP store for backend. Currently we are relying on Apache Pinot but you can plug in Druid if you want or even some Relational DB store with minimal to no code changes. We are trying to make this process more simpler going ahead. 

## Apache Pinot
Pinot is a real-time distributed OLAP datastore, built to deliver scalable real-time analytics with low latency. It can ingest from batch data sources (such as Hadoop HDFS, Amazon S3, Azure ADLS, Google Cloud Storage) as well as stream data sources (such as Apache Kafka). 

Pinot was built by engineers at LinkedIn and Uber and is designed to scale up and out with no upper bound. Performance always remains constant based on the size of your cluster and an expected query per second (QPS) threshold.

Pinot is designed to deliver low latency queries on large datasets. In order to achieve this performance, Pinot stores data in a columnar format and adds additional indices to perform fast filtering, aggregation and group by.

Raw data is broken into small data shards and each shard is converted into a unit known as a segment. One or more segments together form a table, which is the logical container for querying Pinot using SQL/PQL.

### Key Features:
- A column-oriented database with various compression schemes such as Run Length, Fixed Bit Length
- Pluggable indexing technologies - Sorted Index, Bitmap Index, Inverted Index, Star-Tree Index
- Ability to optimize query/execution plan based on query and segment metadata
- Near real time ingestion from Kafka and batch ingestion from Hadoop
- SQL like language that supports selection, aggregation, filtering, group by, order by, distinct queries on fact data
- Support for multivalued fields
- Horizontally scalable and fault tolerant

Because of the design choices made to achieve these goals, there are certain limitations present in Pinot:

- Pinot is not a replacement for database i.e it cannot be used as source of truth store, cannot mutate data
- While Pinot supports text search, its not a replacement for search engine i.e relevance is not supported
- Query cannot span across multiple tables - Use Presto-Pinot connector to achieve joins and other features

Pinot works very well for querying time series data with lots of Dimensions and Metrics. Example - Query (profile views, ad campaign performance, etc.) in an analytical fashion (who viewed this profile in the last weeks, how many ads were clicked per campaign).

### Resources:
1. Apache pinot: https://pinot.apache.org/
2. GitHub: https://github.com/apache/incubator-pinot 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/arch/backends.md">
<button type="button">Edit</button></a>

***
