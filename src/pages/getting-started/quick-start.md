---
title: Quick Start
weight: 2
template: docs
---

The best part in getting started with Hypertrace is that it's really quick! If you are already using a tracing system, you can start today. Hypertrace accepts all major data formats: Jaeger, OpenTracing, Zipkin, you name it. Even if you aren’t tracing yet, we have a bunch of sample apps you can start with, and a [chat room](https://hypertrace.slack.com) of excited people who want to meet you. Here we will tell you how you can get started with Online Boutique sample app which is one of our trace enabled sample applications.

### Sample app: Online Boutique (created by Google Cloud)

Online Boutique is one of our trace enabled sample applications. It includes typical ecommerce functionality, including a product catalog and a way for customers to check out in different currencies This application uses different languages to highlight the diversity in micro service architecture: Golang, C++, C#, Python, Java and other programming languages. Whatever your application is written in, you can see its requests in Hypertrace.

If you want to start your own online boutique, sorry! This doesn’t include authentication, credit card processing and features in the real world! However, we can use this to understand hypertrace and get you started with distributed tracing. 

#### Deployment instructions

Use pre-built public container images that are easy to deploy by deploying the release manifest directly to an existing K8s cluster.

**Prerequisite**: A running Kubernetes cluster (local or cloud).

1. `git clone https://github.com/hypertrace/hypertrace-samples.git`
2. `cd online-boutique-demo`
2. Run `kubectl apply -f ./release/kubernetes-manifests.yaml` to deploy the sample app.
3. Run `kubectl get pods` to confirm pods are in a Ready state.
4. Find the `NodePort` of your application, then visit the application at `localhost:nodeport` in your
   browser to confirm installation. 

   ```sh
   kubectl get service/frontend-external
   ```
#### Architecture

**Online Boutique** is composed of many microservices written in different languages that talk to each other over gRPC.

| ![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/architecture-diagram.png) | 
|:--:| 
| *Microservices Architecture* |


#### This is how your application will look like!

| Home Page                                                                                                         | Checkout Screen                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [![Screenshot of store homepage](https://s3.amazonaws.com/fininity.tech/online-boutique-frontend-1-min.png)]() | [![Screenshot of checkout screen](https://s3.amazonaws.com/fininity.tech/DT/online-boutique-frontend-2.png)]() |


#### This is how your tracing data will look like on Hypertrace! 

You can check out [UI & Platform overview](https://hypertrace-docs.netlify.app/docs/platform-ui/) section to get more details on features and see insights of online boutique app using Hypertrace. 

<div class="note">
  <strong>Note:</strong> 
  If you want to try more samples with Hypertrace visit our blog post on <a src=https://github.com/hypertrace/hypertrace-samples>Best microservice sample apps</a>.
</div>


<div class="important">
  <strong>Important:</strong> 
  Are you facing any issue with this? Let's discuss it on <a src=https://hypertrace.slack.com/>Slack</a>.
</div>

### Other samples:
1. [Horod application](/hotrod/README.md)
2. [todo-list-application](/todo-list-application/README.md)

Are you still confused with **Instrumentation** jargon? Ahh! We have you covered! Jump to [Instrumentation](https://hypertrace-docs.netlify.app/docs/getting-started/instrumentation/) section which will tell you about what is instrumentation and how you can get started with instrumenting your application! 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/getting-started/quick-start.md">
<button type="button">Edit</button></a>

***
