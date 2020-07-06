---
title: Installation
weight: 1
template: docs
---
## Hypertrace: Installation
- We are using Helm charts to deploy Hypertrace distributed tracing platform.
- Hypertrace supports collection of traces from different tracers like OpenTracing, OpenCensus, Jaeger and zipkin.

### Requirements
- `Docker desktop` (version 2.2.x and above) with `Kubernetes` enabled.
- Minimum resources for Docker: (2 CPUs, 4GB Memory).
Following is the snapshot of resources used of a typical hypertrace standalone deployment.

    | Resource          | Requests        | Limits        |
    |-------------------| ---------------:| -------------:|
    | cpu               | 1850m (46%)     | 2700m (67%)   |
    | memory            | 4084Mi (41%)    | 6472Mi (65%)  |
    | ephemeral-storage | 0 (0%)          | 0 (0%)        |


- `Helm` (version 3.2.x and above)
- Bash
- Ineternet connectivity to pull the hypertrace helm charts and docker images
- Basic understanding of kubernetes and helm

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

### Verify installation

- Verify helm charts. Successful installation should have the release status as deployed for both `data-services` and `platform-services` as below.
    ``` shell script
    $ helm list --namespace=hypertrace --kube-context=docker-desktop               
     NAME                        	NAMESPACE 	REVISION	UPDATED                             	STATUS  	CHART                             	APP VERSION
     hypertrace-data-services    	hypertrace	1       	2020-06-24 22:19:46.827523 +0530 IST	deployed	hypertrace-data-services-0.1.0    	0.1.0
     hypertrace-platform-services	hypertrace	1       	2020-06-24 22:21:33.41217 +0530 IST 	deployed	hypertrace-platform-services-0.1.0	0.1.0
    ```

- Verify kuberbetes pod. Successful installation should not have any pods crashing.
    ```shell script
    $ kubectl get pods --namespace=hypertrace --context=docker-desktop             
    NAME                                                         READY   STATUS      RESTARTS   AGE
    all-views-creation-job-x92tp                                 0/1     Completed   0          31m
    all-views-generator-5c9dd64b8-mmgk2                          1/1     Running     0          30m
    attribute-config-bootstrapper-9qhw2                          0/1     Completed   0          29m
    attribute-service-85f5c7bc44-bsrpm                           1/1     Running     0          30m
    domain-event-view-creation-job-6n6l4                         0/1     Completed   0          31m
    entity-config-bootstrapper-vhvqw                             0/1     Completed   0          29m
    entity-service-85d57b7f5c-2rl7t                              1/1     Running     0          30m
    gateway-service-59c884b77d-vhmsb                             1/1     Running     0          30m
    hypertrace-graphql-service-7b6c4b8697-hhc9w                  1/1     Running     0          30m
    hypertrace-oc-collector-7f8c988f57-7v9bn                     1/1     Running     0          30m
    hypertrace-trace-enricher-75b7b4c788-bc69f                   1/1     Running     0          30m
    hypertrace-trace-enricher-kafka-topics-creator-czk9j         0/1     Completed   0          31m
    hypertrace-ui-b545969c4-79clg                                1/1     Running     0          30m
    jaeger-spans-kafka-topic-creator-79h9q                       0/1     Completed   0          31m
    jaeger-to-raw-spans-converter-569c898cb9-9sxpc               1/1     Running     0          30m
    kafka-0                                                      1/1     Running     0          33m
    mongo-0                                                      1/1     Running     0          33m
    pinot-servicemanager-0                                       1/1     Running     0          33m
    query-service-748bc798c4-std6f                               1/1     Running     0          30m
    raw-spans-from-jaeger-spans-topic-creator-9dpsc              0/1     Completed   0          31m
    raw-spans-grouper-74bdb8d4d9-bwcps                           1/1     Running     0          30m
    schema-registry-68484cd986-lbsb5                             1/1     Running     1          33m
    structured-traces-from-raw-spans-kafka-topic-creator-njxs7   0/1     Completed   0          30m
    view-generation-kafka-topics-creator-lslsk                   0/5     Completed   0          30m
    zookeeper-0                                                  1/1     Running     0          33m
    ```

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

In case of any port collisions, users can modify the following properties in helm file (platform-services/values.yaml).

- `ingress.hosts[].paths[].port` - To change UI port
- `oc-collector.service.ports[].targetPort` - To change collector ports

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/getting-started/installation.md">
<button type="button">Edit</button></a>
