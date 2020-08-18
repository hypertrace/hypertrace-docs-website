---
title: Getting Started
excerpt: In this section you'll find basic information about Hypertrace and how to use it.
template: docs
---
## Quick start with Hypertrace using Docker

### Running Hypertrace with docker-compose

**Note:** *It is recommended to change default memory for docker from `2GiB` to `4GiB` and default CPU's to 3 to get Hypertrace up and running.* 

#### Start Hypertrace

If you want to see Hypertrace in action, you can quickly start Hypertrace via Docker.

```
git clone https://github.com/hypertrace/hypertrace.git
cd hypertrace/docker
docker-compose pull
docker-compose -f docker-compose.yml up
```

This will start all services required for Hypertrace. Once you see the service hypertrace-ui start, you can visit Hypertrace UI at http://localhost:2020 . 

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) | 
|:--:| 
| *Hypertrace Dashboard* |

If you are facing any issues with docker-compose setup, we have listed down common issues and resolutions [here](https://docs.hypertrace.org/troubleshooting/docker-compose/).


#### Ports

Here are the default Hypertrace ports:

| Port  | Service                 |
|-------|-------------------------|
| 2020  | Used by Hypertrace UI   |
| 14267 | Jaeger thrift collector |
| 14268 | Jaeger HTTP collector   |
| 9411  | Zipkin collector        |


#### Sample application
- The example app has two services: frontend and backend. They both report trace data to Hypertrace. To setup the demo, you need to start Frontend, Backend and Hypertrace. 
- You can start sample by running `docker-compose -f docker/examples/docker-compose.yml up` if you have hypertrace running already. 
- You can start sample app with Hypertrace using `docker-compose -f docker/docker-compose.yml -f docker/examples/docker-compose.yml up`.
- Example app will be served at http://localhost:8081 . You can visit app to generate some sample requests or simply run `run.sh` which will generate bunch of requests for you! 


## Deploying with Kubernetes
You can refer to [kubernetes deployment guide](https://docs.hypertrace.org/getting-started/kubernetes/) to deploy using helm on docker-dektop with Kubernetes. [deployments](https://docs.hypertrace.org/deployments/) section lists down steps for deploying Hypertrace on different Kubernetes flavors along different operating systems along with all major cloud providers. You can find the helm charts and installation script along with more details [here](https://github.com/hypertrace/hypertrace).

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/index.md">
<button type="button">Edit</button></a>


***
