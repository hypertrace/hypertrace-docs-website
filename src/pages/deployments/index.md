---
title: Deployments
excerpt: This section will help you in deploying hypertrace on various cloud platforms as well as managed kubernetes services. 
template: docs
---

There are bunch of different ways to deploy hypertarce. You can deploy on local machine using docker for desktop or you can use any cloud based kubernetes service and deploy hypertrace on it. We are using helm charts to deploy hypertrace. This section will help you learning about helm charts along with resources to help you deploy hypertrace on GKE and EKS.

## What is helm?
Helm is the package manager for Kubernetes. It streamlines installing and managing Kubernetes applications. We can use a single helm chart to deploy anything from simple pod to a complex application. 

Helm has pretty detailed documentation which you can find over [here](https://helm.sh/docs/). For detailed information about installing helm on different platforms you can visit [here](https://helm.sh/docs/intro/install/). 


## Hypertrace-helm
We provide Helm charts for all services needed for a Hypertrace installation. We have divided this services into two categories namely data services and platform services:

- The `data-services` category includes third party technologies such as Flink and Pinot. These services handle storage and real-time analysis functionality.
- The `platform-services` category includes Hypertrace code. This services handle span collection, trace generation, trace enrichment, views etc.

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/index.md">
<button type="button">Edit</button></a>

***

Here are the articles in this section:
