---
title: Getting Started
excerpt: Get started with Hypertrace using Docker Desktop (using Docker Compose or Docker with Kubernetes)
template: docs
---
## Quick start with Docker Desktop

### Running Hypertrace with Docker Compose


---
<iframe width="680" height="380" src="https://www.youtube.com/embed/85jfOMqlf-w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope" allowfullscreen></iframe>

---
`Note`: This video shows end-to-end installation of Hypertrace on Docker Desktop.

#### Requirements:
- [docker-engine](https://docs.docker.com/engine/install/) (17.12.0+)
- [docker-compose](https://docs.docker.com/compose/install/) (1.21.0 +)
- **We recommend you change the [Docker Desktop default settings](https://hypertrace-docs.s3.amazonaws.com/docker-desktop.png) from `2 GB` of memory to `4 GB` of memory, and set CPUs to at least 3 CPUs.** 

| ![space-1.jpg](https://hypertrace-docs.s3.amazonaws.com/docker-desktop.png) | 
|:--:| 
| *Docker Desktop resource allocation* |

#### Start Hypertrace

`Note`: If reporting a problem, please include the output of `docker stats --no-stream`.

Use your terminal window to start Hypertrace with git and docker-compose up:

```
git clone https://github.com/hypertrace/hypertrace.git
cd hypertrace/docker
docker-compose -f docker-compose.yml pull
docker-compose -f docker-compose.yml up --force-recreate
```

This will start all services required for Hypertrace. Once you see 'Stack is up after [x] attempts', you can view the Hypertrace UI at http://localhost:2020. The UI isn't useful without data. To send data to Hypertrace, run an app, such as the sample app below. 

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-3.png) | 
|:--:| 
| *Hypertrace Dashboard* |

`Note`: If reporting a problem, please include the output of `docker stats --no-stream`.

#### Start the Sample App

- The sample app has two services: frontend and backend. They both report trace data to Hypertrace. To setup the sample app, you need to start the sample app with:
```
docker-compose -f docker-compose-zipkin-example.yml up
```
- You can view the sample app at http://localhost:8081. Refresh the sample app page multiple times to generate sample requests. Then go back to the Hypertrace UI and click the 'Refresh' button at the top. You should now see sample requests in the Explorer section. 

- Note: You can start Hypertrace AND the sample app together with: 
```
docker-compose -f docker-compose.yml -f docker-compose-zipkin-example.yml up
```


### Troubleshooting

Issues? Answers to common installation problems can be found at [Troubleshooting Docker Compose](https://docs.hypertrace.org/troubleshooting/docker-compose/).

#### Stop Hypertrace

Use a terminal window to stop Hypertrace:

```
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


## Deploy in production with Kubernetes

We support helm charts to simplify deploying Hypertrace in Kubernetes environment, maybe on your on-premise server or cloud instance! 

Please refer to the [deployments section](https://docs.hypertrace.org/deployments/) in our documentation which lists the steps to deploy Hypertrace on different Kubernetes flavors across different operating systems and cloud providers. You can find the Helm Charts and installation scripts with more details [here](https://github.com/hypertrace/hypertrace/tree/main/kubernetes).

Note: We have created `hypertrace-ingester` and `hypertrace-service` to simplify local deployment and quick-start with Hypertrace. As of now, we don't support them for production because of some limitations and some unreliabiliy with scaling. So, we will encourage you to deploy individual components for staging as well as production deployments. 

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/getting-started/index.md">
<button type="button">Edit</button></a>


***
