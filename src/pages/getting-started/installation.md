---
title: Installation
weight: 1
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

<div class="note">
  <strong>Note:</strong> 
  If you want more detailed information about deploying Hypertrace on various cloud platforms with different profiles, please check <a src=https://docs.hypertrace.org/deployments>Deployment Docs.</a>
</div>

### Configuration

| Key                  | Description                                                                                                   | Allowed values       |
|----------------------|---------------------------------------------------------------------------------------------------------------|----------------------|
| `HT_DOCKER_REGISTRY` | Public Docker repository.                                                                                     |                      |
| `HT_HELM_REGISTRY`   | Public Helm repository.                                                                                       |                      |
| `HT_PROFILE`         | Profile is size of your deployment. (Memory, No. of CPU's, etc.).                                             | mini, medium, large  |
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

## Hypertrace

Once your Hypertrace installation is successful you can navigate to `http://localhost` to access the Hypertarce UI. It looks something like this!

| ![space-1.jpg](https://s3.amazonaws.com/hypertrace-docs/dashboard-1.png) | 
|:--:| 
| *Hypertrace Dashboard* |

You can't experience all this functionalities Hypertrace is offering unless you start with sending trace data to it. So why not jump to [Quick Start](https://docs.hypertrace.org/getting-started/quick-start/) section in documentation and see how you can get started with using Hypertrace!


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/getting-started/installation.md">
<button type="button">Edit</button></a>

***
