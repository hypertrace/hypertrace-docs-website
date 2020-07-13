---
title: Getting Started
excerpt: In this section you'll find basic information about Hypertrace and how to use it.
template: docs
---

## Overview
Hypertrace installation script uses Helm Charts to deploy Hypertrace on Kubernetes. If you are already using a tracing system, you can start today. Hypertrace accepts all major data formats: Jaeger, OpenTracing, Zipkin, you name it. Once you complete Installation you can see traces from your already instrumented application in Hypertrace. 

---
<iframe width="680" height="380" src="https://www.youtube.com/embed/hmMpa3Xp6Go" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope" allowfullscreen></iframe> 

---

### Requirements
- `Docker Desktop` or `Kubernetes` (version 1.5 and above).
- Minimum resources: (2 CPUs, 4GB Memory).
- `Helm` (version 3.2.x and above)
- Bash

### Install
- Git Clone the <a href="https://github.com/hypertrace/hypertrace">Hypertrace</a> repository. 
- Update the config properties under `./config/hypertrace.properties` as needed. The default config will work for a standalone deployment on Docker for Desktop.
- Run `./hypertrace.sh install`


#### Note: If you want more detailed information about deploying Hypertrace on various cloud platforms with different profiles, please check [Deployment Docs](https://docs.hypertrace.org/deployments).

### Configuration

| Key                  | Description                                                                                                   | Allowed values       |
|----------------------|---------------------------------------------------------------------------------------------------------------|----------------------|
| `HT_PROFILE`         | Profile is size of your deployment. (Memory, No. of CPU's, etc.).                                             | Dev, Mini, Standard  |
| `HT_CLOUD_PROVIDER`  | Cloud platform you are deploying Hypertrace on.                                                               | aws, gcp, azure      |
| `HT_KUBE_CONTEXT`    | Kubernetes context to deploy Hypertrace.                                                                      | specific to platform |
| `HT_KUBE_NAMESPACE`  | Kubernetes namespace to deploy Hypertrace.                                                                    | hypertrace           |
| `HT_ENABLE_DEBUG`    | In case of any issue, install Hypertrace in debug mode to get more logs and traces to identify the rootcause. | true, false          |
| `HT_INSTALL_TIMEOUT` | Helm install wait timeout.                                                                                    | in minutes           |

### Uninstall
- Run `./hypertrace.sh uninstall`

### Ports

Here are the default Hypertrace ports: (You can notice that you don't need to change anything to get started with Zipkin, Jaeger and OpenCensus collector to get started with Hypertrace.)

| Port  | Service                 |
|-------|-------------------------|
| 80    | Used by Hypertrace UI   |
| 55678 | Opencensus collector    |
| 14267 | Jaeger thrift collector |
| 14268 | Jaeger HTTP collector   |
| 9411  | Zipkin collector        |

In case of any port collisions, users can modify the following properties in helm file (`platform-services/values.yaml`).
- `ingress.hosts[].paths[].port` -  To change UI port 
- `hypertrace-oc-collector.service.ports[].targetPort` - To change collector ports

## Verifying Hypertrace UI

Once your Hypertrace installation is successful you can navigate to`http://localhost:9000` or IP address for hypertrace-ui service to access the Hypertarce UI. It looks something like this!

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) | 
|:--:| 
| *Hypertrace Dashboard* |

## Sending data to Hypertrace
Now you know things are running, let's get some data into Hypertrace. If your applications already send trace data, you can configure them to send data to Hypertrace using the default ports for Jaeger, OpenCensus or Zipkin. If you are just getting started, try out our [demo app](https://docs.hypertrace.org/sample-app/]). Once you have data in Hypertrace, you are ready to [explore its advanced features](https://docs.hypertrace/org/platform-ui/). 


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/getting-started/index.md">
<button type="button">Edit</button></a>


