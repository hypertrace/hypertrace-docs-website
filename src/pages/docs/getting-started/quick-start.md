---
title: Quick Start
weight: 2
template: docs
---

## Quick start with Hypertrace

The best part is that if you are already using a tracing system, you can start today. Hypertrace accepts all major data formats: Jaeger, OpenTracing, Zipkin, you name it. Even if you aren’t tracing yet, we have a bunch of sample apps you can start with, and a chat room of excited people who want to meet you. Here we will tell you how you can get started with Online Boutique sample app which is one of our trace enabled sample applications.

### Sample app: Online Boutique (created by Google Cloud)

Online Boutique is a cloud-native microservices demo app consisting of 10 microservices. Microservices are written in Go, c#, Python, Java and functions as an e-commerce website app where users can browse items, add them to a shopping cart, and checkout.

This demo has services such as Product catalog, Recommendation, Shopping Cart, Checkout page, Payment, Shipping and more. It isn't built to operate as a real world ecommerce platform which can have so many reasons to fail but this makes a good, familiar use case for demo purposes.

#### Deployment instructions

Use pre-built public container images that are easy to deploy by deploying the [release manifest](./release) directly to an existing K8s cluster.

**Prerequisite**: A running Kubernetes cluster (local or cloud).

1. Clone this repository, and go to the repository directory
2. Run `kubectl apply -f ./release/kubernetes-manifests.yaml` to deploy the sample app.
3. Run `kubectl get pods` to confirm pods are in a Ready state.
4. Find the `NodePort` of your application, then visit the application at `localhost:nodeport` in your
   browser to confirm installation. 

   ```sh
   kubectl get service/frontend-external
   ```

#### This is how your application will look like!

| Home Page                                                                                                         | Checkout Screen                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [![Screenshot of store homepage](https://s3.amazonaws.com/fininity.tech/online-boutique-frontend-1-min.png)]() | [![Screenshot of checkout screen](https://s3.amazonaws.com/fininity.tech/DT/online-boutique-frontend-2.png)]() |


#### This is how your tracing data will look like on Hypertrace! 

You can check for [UI & Platform overview](https://hypertrace-docs.netlify.app/docs/platform-ui/) section to get more details on features and see insights of online boutique app using Hypertrace. 


#### Architecture

**Online Boutique** is composed of many microservices written in different languages that talk to each other over gRPC.

| ![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/architecture-diagram.png) | 
|:--:| 
| *Microservices Architecture* |

### Service Description Table

| Service                                              | Language      | Description                                                                                                                       |
| ---------------------------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [frontend](./src/frontend)                           | Go            | Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically. |
| [cartservice](./src/cartservice)                     | C#            | Stores the items in the user's shopping cart in Redis and retrieves it.                                                           |
| [productcatalogservice](./src/productcatalogservice) | Go            | Provides the list of products from a JSON file and ability to search products and get individual products.                        |
| [currencyservice](./src/currencyservice)             | Node.js       | Converts one currency to another. Uses real values fetched from European Central Bank. It's the highest QPS service. |
| [paymentservice](./src/paymentservice)               | Node.js       | Charges the given credit card (mock) with the given amount and returns a transaction ID.                                     |
| [shippingservice](./src/shippingservice)             | Go            | Gives shipping cost estimates based on the shopping cart items. Ships items to the given address (mock)                                 |
| [emailservice](./src/emailservice)                   | Python        | Sends users an order confirmation email (mock).                                                                                   |
| [checkoutservice](./src/checkoutservice)             | Go            | Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification.                            |
| [recommendationservice](./src/recommendationservice) | Python        | Recommends other products based on shopping cart items.                                                                      |
| [adservice](./src/adservice)                         | Java          | Provides text ads based on given context words.                                                                                   |
| [loadgenerator](./src/loadgenerator)                 | Python/Locust | Continuously sends requests imitating realistic user shopping flows to the frontend.                                              |


<div class="note">
  <strong>Note:</strong> 
  If you want to try more samples with Hypertrace visit our blog post on <a src=https://github.com/hypertrace/best-microservices-sample-apps>Best microservice sample apps</a>.
</div>


<div class="important">
  <strong>Important:</strong> 
  Are you facing any issue with this? Let's discuss it on <a src=https://hypertrace.slack.com/>Slack</a>.
</div>


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/getting-started/quick-start.md">
<button type="button">Edit</button></a>

***
