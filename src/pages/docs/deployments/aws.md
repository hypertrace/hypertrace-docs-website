---
title: AWS EKS
weight: 3
template: docs
---

## Deploying hypertrace on AWS EKS using helm:

1. Clone the hypertrace-helm repo on you local machine using `git clone https://github.com/Traceableai/hypertrace-helm.git`
2. Go to the hypertrace-helm directory and run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- Default configuration will work for docker for dekstop deployment which we are discussing in this section. 
- You can choose from `mini`, `medium` and `large` profile according to your cluster types. each one has appropriate resources allocated to it.
- Below configuration uses `large` profile. 

Default configuration is as follows:
```bash
HT_DOCKER_REGISTRY=traceableai-docker.jfrog.io
HT_HELM_REGISTRY=https://traceableai.jfrog.io/traceableai/helm
# Set install profile using `HT_PROFILE` (It can be `mini`, `medium` and `large`). Please use `standalone` for local deployment.
HT_PROFILE=large
#  Set `HT_CLOUD_PROVIDER` to cloud provider you are deploying HT on (currently you can set it to `gcp` or `aws`)
HT_CLOUD_PROVIDER=aws
# TODO: Cleanup username,password and email configuration after moving artifacts to public repository
DOCKER_USERNAME=${DOCKER_USERNAME}
DOCKER_PASSWORD=${DOCKER_PASSWORD}
DOCKER_EMAIL=${DOCKER_USERNAME}@traceable.ai

# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT="YOUR_EKS_CLUSTER_CONTEXT"
# Kubernetes namespace to deploy hypertrace
HT_KUBE_NAMESPACE=hypertrace
HT_ENABLE_DEBUG=false
# Helm install wait timeout.
# Installation time generally depends time to pull multiple hypertrace images from the repository.
# Set it higher value if the connection is slower.
# Units in minutes
HT_INSTALL_TIMEOUT=10
```
In case of any issue, install hypertrace in debug mode to get more logs and traces to identify the rootcause.
- Set `HT_ENABLE_DEBUG` to `true` in `./config/hypertrace.properties`
- Debug `bash -x ./hypertrace.sh install`

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

You can check out [installation]() doc to read more about ports and other configs. 


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/docs/deployments/aws.md">
<button type="button">Edit</button></a>