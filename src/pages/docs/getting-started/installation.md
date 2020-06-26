---
title: Installation
weight: 1
template: docs
---
## Hypertrace: Installation
Get up and running with hypertrace in your local environment

### How it works
Deploys Hypertrace platform in `docker-desktop` context and under the namespace `hypertrace`.

### Ports used
Following ports are opened and used by Hypertrace. Make sure these ports are available before we proceed with installation.
- `80` - Used by Hypertrace UI
- `55678` - Opencensus collector
- `14267` - Jaeger thrift collector
- `14268` - Jaeger HTTP collector
- `9411` - Zipkin collector

In case of any port collisions, users can modify the following properties in helm file (`platform-services/values.yaml`).
- `ingress.hosts[].paths[].port` -  To change UI port 
- `hypertrace-oc-collector.service.ports[].targetPort` - To change collector ports

### Install
- Clone the repository from github.
- Customize the configuration under `./config/hypertrace.properties` as needed. Default configuration works for most of the setups.
- Run `./standalone.sh install`

In case of any issue, install hypertrace in debug mode to get more logs and traces to identify the rootcause.
- Set `ENABLE_DEBUG` to `true` in `./config/hypertrace.properties`
- Debug `bash -x ./standalone.sh install`

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
- Run `./standalone.sh uninstall`

### Troubleshooting
- ###### Error: release hypertrace-data-services failed, and has been uninstalled due to atomic being set: timed out waiting for the condition
    Installation failed due to timeout. May be due to slower connection to pull the hypertrace docker images. Increase timeout configuration `INSTALL_TIMEOUT` in `config/hypertrace.properties`
    
    If the problem persists even after sufficient timeout, check if some services in hung pending state for long. 
    This is a known [ docker issue ](https://github.com/docker/for-mac/issues/2990).
    Issues gets fixed by rebooting `Docker desktop` and reinstalling hypertrace.
    ```shell script
     $ kubectl get services --context=docker-desktop --namespace=hypertrace
    NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                          AGE
    attribute-service            ClusterIP      10.108.115.193   <none>        9012/TCP                                                         5m14s
    bootstrap                    ClusterIP      10.97.13.134     <none>        9092/TCP                                                         8m32s
    entity-service               ClusterIP      10.96.159.110    <none>        50061/TCP                                                        5m14s
    gateway-service              ClusterIP      10.110.55.131    <none>        50071/TCP                                                        5m14s
    hypertrace-graphql-service   ClusterIP      10.107.17.146    <none>        23431/TCP                                                        5m14s
    hypertrace-oc-collector      LoadBalancer   10.109.173.246   <pending>     55678:32553/TCP,14268:32604/TCP,14267:30295/TCP,9411:32753/TCP   5m14s
    hypertrace-ui                LoadBalancer   10.100.55.219    <pending>     80:32631/TCP                                                     5m14s
    kafka-broker                 ClusterIP      None             <none>        9092/TCP                                                         8m33s
    pinot-controller             ClusterIP      None             <none>        9000/TCP                                                         8m33s
    pinot-servicemanager         ClusterIP      None             <none>        9000/TCP,8098/TCP,8099/TCP                                       8m33s
    pinot-servicemanager-svc     ClusterIP      10.96.130.44     <none>        9000/TCP,8098/TCP,8099/TCP                                       8m33s
    query-service                ClusterIP      10.106.114.19    <none>        8090/TCP                                                         5m14s
    schema-registry-service      ClusterIP      10.100.216.76    <none>        8081/TCP                                                         8m33s
    zookeeper                    ClusterIP      10.107.169.223   <none>        2181/TCP                                                         8m33s
    zookeeper-headless           ClusterIP      None             <none>        2888/TCP,3888/TCP                                                8m33s
    ```


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