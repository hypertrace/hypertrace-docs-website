---
title: Deployments
excerpt: >-
  To make it easy to write documentation in plain Markdown, most UI components
  are styled using Markdown elements with few additional CSS classes.
template: docs
---

There are bunch of different ways to deploy hypertarce. You can deploy on local machine using docker for desktop or you can use any cloud based kubernetes service and deploy hypertrace on it. We are using helm charts to deploy hypertrace. This section will help you learning about helm charts along with resources to help you deploy hypertrace on GKE and EKS.

## What is helm?
Helm is the package manager for Kubernetes. It streamlines installing and managing Kubernetes applications. We can use a single helm chart to deploy anything from simple pod to a complex application. 

Helm has pretty detailed documentation which you can find over [here](https://helm.sh/docs/). For detailed information about installing helm on different platforms you can visit [here](https://helm.sh/docs/intro/install/). 


## Hypertrace-helm

You can find hypertrace helm repo here: https://github.com/Traceableai/hypertrace-helm 

Helm repo contains charts for different services which are as follows:
- Zookeeper
- Kafka
- Avro schema registry
- Istio
- Prometheus operator
- Kafka Exporter
- Kafka Manager
- ElasticSearch
- Logstash
- Mongo
- Pinot
- Local volume provisioner
- Metric server

We have divided this services into two categories namely data services and platform services:

- All open services/technologies (zookeeper, kafka, schema registry, pinot, mongo) are grouped into data-services. These services acts as data-store for Hypertrace.
- All other microservices which deals with traces like span collection, trace generation, trace enrichment, views etc. forms another group, platform-services. 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/index.md">
<button type="button">Edit</button></a>
***

Here are the articles in this section:
