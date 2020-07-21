---
title: Deployments
excerpt: This section will help you deploy Hypertrace on various cloud platforms, Docker for Desktop, and more
template: docs
---

Hypertrace is deployed using Helm Charts, which means you can deploy it to almost any Kubernetes environment. You can deploy it on your local machine using Docker for Desktop with Kubernets enabled, or any cloud-based Kubernetes service, or a managed Cloud that supportes Kubernetes such as OpenShift and Cloud Foundry. This section will provide you the resources to help you deploy Hypertrace.

## What is Helm?
Helm is the package manager for Kubernetes. It streamlines installing and managing Kubernetes applications. We can use a single Helm chart to deploy anything from a simple pod to a complex application. 

Helm has detailed documentation which you can find at [helm.sh/docs](https://helm.sh/docs/). For detailed information about installing Helm on different platforms you can visit [helm.sh/docs/intro/install](https://helm.sh/docs/intro/install/). 


## Hypertrace-helm
We provide Helm charts for all services needed to run Hypertrace. They are grouped into two categories: Data services and Platform services:

- The `platform-services` category includes services that are primarily Hypertrace code. These services handle span collection, trace generation, trace enrichment, views etc.
- The `data-services` category includes third party technologies such as Flink and Pinot. These services handle storage and real-time analysis functionality.

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/index.md">
<button type="button">Edit</button></a>

***

Here are the articles in this section:
