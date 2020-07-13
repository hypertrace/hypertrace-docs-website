---
title: AWS EKS
weight: 3
template: docs
---

## Deploying hypertrace on AWS EKS using helm:

1. Clone the Hypertrace-helm repo on you local machine using `git clone https://github.com/Traceableai/hypertrace-helm.git`
2. Go to the Hypertrace-helm directory and run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed. 
- You can choose from `dev`, `mini` and `standard` profile according to your cluster types. each one has appropriate resources allocated to it.
- Below configuration uses `mini` profile. 

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=mini
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_CLOUD_PROVIDER=aws
# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT=`Your eks context`
# Kubernetes context to deploy hypertrace
HT_KUBE_NAMESPACE=hypertrace
# Helm install wait timeout.
# Installation time generally depends time to pull multiple hypertrace images from the repository.
# Set it higher value if the connection is slower.
# Units in minutes
HT_INSTALL_TIMEOUT=10
# Flag to debug installation issues
# Allowed values: {true, false}
HT_ENABLE_DEBUG=false
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

### Uninstall
- Run `./hypertrace.sh uninstall`

You can check out [installation](https://docs.hypertrace.org/getting-started/) doc to read more about ports and other configs. 


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/aws.md">
<button type="button">Edit</button></a>

***
