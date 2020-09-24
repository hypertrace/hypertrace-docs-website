---
title: Sample App
excerpt: The Online Boutique sample app will help you get started with Hypertrace. 
template: docs
---

The best part in getting started with Hypertrace is that it's really quick! If you are already using a tracing system, you can start today. Hypertrace accepts all major data formats: Jaeger, OpenTracing, Zipkin, you name it. Even if you aren’t tracing yet, we have a bunch of sample apps you can start with, and a [chat room](https://www.hypertrace.org/get-started) on Slack) of excited people who want to meet you. Here we will tell you how you can get started with Online Boutique sample app which is one of our trace enabled sample applications.

### Sample app: Online Boutique (created by Google Cloud)

Online Boutique is one of our trace enabled sample apps. It includes typical ecommerce functionality, including: a product catalog, shopping cart, and a way for customers to check-out using different currencies. This application uses different languages to highlight the diversity in microservice architecture: Golang, C++, C#, Python, Java and other programming languages. Whatever your application is written in, you can see its requests in Hypertrace.

If you want to start your own online boutique, just add user authentication, payment processing and you're in business! It also makes a great way to learn about Hypertrace and to get started with distributed tracing. 

#### Deployment instructions

Use pre-built Docker images and a release manifest that is easy to deploy to an existing K8s cluster.

**Prerequisite**: A running Kubernetes cluster (local or cloud).

1. `git clone https://github.com/hypertrace/hypertrace-samples.git`
2. `cd online-boutique-demo`
2. `kubectl apply -f ./release/kubernetes-manifests.yaml`
3. Confirm pods are in a ready state `kubectl get pods` 
4. Find the `NodePort` of your application, then visit the application at `localhost:nodeport` in your
   browser to confirm installation. 

   ```sh
   kubectl get service/frontend-external
   ```

#### Architecture

**Online Boutique** is composed of microservices written in multiple languages that talk to each other over gRPC.

| ![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/architecture-diagram.png) | 
|:--:| 
| *Microservices Architecture* |


#### This is how your application will look like!

| Home Page                                                                                                         | Checkout Screen                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [![Screenshot of store homepage](https://s3.amazonaws.com/fininity.tech/online-boutique-frontend-1-min.png)]() | [![Screenshot of checkout screen](https://s3.amazonaws.com/fininity.tech/DT/online-boutique-frontend-2.png)]() |


#### This is how your tracing data will look like on Hypertrace! 

Check out the [UI & Platform overview](https://docs.hypertrace.org/platform-ui/) section to get more details and insights about how the Online Boutique uses Hypertrace. 


#### Are you facing any issue with this? Let us know in [Slack](https://www.hypertrace.org/get-started).

### Other sample apps:
1. [HotROD application](https://github.com/hypertrace/hypertrace-samples/tree/master/hotrod)
2. [todo-list-application](https://github.com/hypertrace/hypertrace-samples/tree/master/todo-list-application)

Are you still confused with **Instrumentation** jargon? We have you covered! Check out the [Instrumentation](https://docs.hypertrace.org/instrumentation/) section which will help you instrument your application! 

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/sample-app/index.md">
<button type="button">Edit</button></a>


***


