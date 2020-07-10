---
title: Installation issues
weight: 1
template: docs
---
- ## Port collision
In case of any port collisions, users can modify the following properties in helm file (platform-services/values.yaml).

- `ingress.hosts[].paths[].port` - To change UI port
- `oc-collector.service.ports[].targetPort` - To change collector ports

- ## General issues
In case of any issue, install hypertrace in debug mode to get more logs and traces to identify the rootcause.
- Set `HT_ENABLE_DEBUG` to `true` in `./config/hypertrace.properties`
- Debug `bash -x ./hypertrace.sh install`

- ## Error: release hypertrace-data-services failed, and has been uninstalled due to atomic being set: timed out waiting for the condition
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

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/troubleshooting/installation.md">
<button type="button">Edit</button></a>

***
