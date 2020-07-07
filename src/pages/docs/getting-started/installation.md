---
title: Installation
weight: 1
template: docs
---
## About Installation
- The default installation uses Helm Charts to deploy Hypertrace.
- Hypertrace supports collection of traces from different tracers like OpenTracing, OpenCensus, Jaeger and zipkin.

### Requirements
- `docker desktop` or any other `kubernetes` enabled docker environment.
- Minimum resources: (2 CPUs, 4GB Memory).
- `Helm` (version 3.2.x and above)
- Bash


### How it works
Deploys Hypertrace platform in `docker-desktop` or any cloud platform context, under the namespace `hypertrace`.

### Install
- Clone the repository from github.
- Customize the configuration under `./config/hypertrace.properties` as needed. Default configuration will work for standalone deployment on docker for desktop.
- Run `./hypertrace.sh install`

In case of any issue, install hypertrace in debug mode to get more logs and traces to identify the rootcause.
- Set `HT_ENABLE_DEBUG` to `true` in `./config/hypertrace.properties`
- Debug `bash -x ./hypertrace.sh install`


### Configuration

| Key                  | Description                                                                                                   | Allowed values       |
|----------------------|---------------------------------------------------------------------------------------------------------------|----------------------|
| `HT_DOCKER_REGISTRY` | Public docker repository.                                                                                     |                      |
| `HT_HELM_REGISTRY`   | Public helm repository.                                                                                       |                      |
| `HT_PROFILE`         | Profile is size of your deployment. (Memory, No. of CPU's, etc.).                                             | mini, medium, large  |
| `HT_CLOUD_PROVIDER`  | Cloud platform you are deploying hypertrace on.                                                               | aws, gcp, azure      |
| `HT_KUBE_CONTEXT`    | Kubernetes context to deploy hypertrace.                                                                      | specific to platform |
| `HT_KUBE_NAMESPACE`  | Kubernetes namespace to deploy hypertrace.                                                                    | hypertrace           |
| `HT_ENABLE_DEBUG`    | In case of any issue, install hypertrace in debug mode to get more logs and traces to identify the rootcause. | true, false          |
| `HT_INSTALL_TIMEOUT` | Helm install wait timeout.                                                                                    | in minutes           |

### Uninstall
- Run `./hypertrace.sh uninstall`

## Hypertrace

Once your hypertrace installation is successful you can navigate to `http://localhost` to access Hypertarce UI. It looks something like this!

| ![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/Hypertrace.png) | 
|:--:| 
| *Hypertrace homepage* |

You can access variety of functionalities including Observability Dashboard, Application flow, Microservices, Web Transactions and Explorer which can help you in troubleshooting!

### Ports

Before we get started more about hypertrace let's see ports it occupies:

| Port  | Service                 |
|-------|-------------------------|
| 80    | Used by Hypertrace UI   |
| 55678 | Opencensus collector    |
| 14267 | Jaeger thrift collector |
| 14268 | Jaeger HTTP collector   |
| 9411  | Zipkin collector        |


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/getting-started/installation.md">
<button type="button">Edit</button></a>

***
