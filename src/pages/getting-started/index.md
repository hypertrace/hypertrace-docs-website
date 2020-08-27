---
title: Getting Started
excerpt: Get started with Hypertrace using Docker Desktop (using Docker Compose or Docker with Kubernetes)
template: docs
---
## Quick start with Docker Desktop

### Running Hypertrace with Docker Compose

**Note:** *We recommend you change the Docker Desktop default settings from `2 GB` of memory to at least `4 GB` of memory, and set CPUs to at least 3* 

#### Start Hypertrace

Use your terminal window to start Hypertrace with docker-compose up

```
git clone https://github.com/hypertrace/hypertrace.git
cd hypertrace/docker
docker-compose -f docker-compose.yml pull
docker-compose -f docker-compose.yml up --force-recreate
```

This will start all services required for Hypertrace. Once you see the service hypertrace-ui start, you can view the Hypertrace UI at http://localhost:2020. The UI isn't useful without data. To send data to Hypertrace, run an app, such as the sample app below. 

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) | 
|:--:| 
| *Hypertrace Dashboard* |

#### Start the Sample App

- The sample app has two services: frontend and backend. They both report trace data to Hypertrace. To setup the sample app, you need to start Frontend, Backend and Hypertrace. You can start the sample app with:
```
docker-compose -f docker-compose-zipkin-example.yml up
```
- You can start Hypertrace AND the sample app together with: 
```
docker-compose -f docker-compose.yml -f docker-compose-zipkin-example.yml up
```
- You can view the sample app at http://localhost:8081. Refresh the sample app page multiple times to generate sample requests. Then go back to the Hypertrace UI and click refresh. You should now see sample requests in the Explorer section. 

### Troubleshooting

Issues? Answers to common installation problems can be found at [Troubleshooting Docker Compose](https://docs.hypertrace.org/troubleshooting/docker-compose/).

#### Stop Hypertrace

Use your terminal window to stop Hypertrace with docker-compose down

```
cntrl-c
docker-compose -f docker-compose.yml down
// docker-compose -f docker-compose.yml -f docker-compose-zipkin-example.yml down
```

#### Ports

Here are the default Hypertrace ports:

| Port  | Service                 |
|-------|-------------------------|
| 2020  | Used by Hypertrace UI   |
| 8081  | Sample App   |
| 14267 | Jaeger thrift collector |
| 14268 | Jaeger HTTP collector   |
| 9411  | Zipkin collector        |



## Running Hypertrace in Kubernetes
Want to deploy using Helm in Docker Desktop with Kubernetes? View our [Kubernetes Deployment Guide](https://docs.hypertrace.org/getting-started/kubernetes/). The [deployments](https://docs.hypertrace.org/deployments/) section provides step-by-step instructions for deploying Hypertrace in different Kubernetes environments, operating systems and cloud providers. You can find the Helm Charts and installation script along with more details [here](https://github.com/hypertrace/hypertrace).

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/getting-started/index.md">
<button type="button">Edit</button></a>


***
