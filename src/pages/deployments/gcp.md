---
title: GCP GKE
weight: 4
template: docs
---

## Deploying hypertrace on GCP GKE using helm:

1. Clone the hypertrace-helm repo on you local machine using `git clone https://github.com/Traceableai/hypertrace-helm.git`
2. Go to the hypertrace-helm directory and run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- Default configuration will work for docker for dekstop deployment which we are discussing in this section. 
- You can choose from `mini`, `medium` and `large` profile according to your cluster types. each one has appropriate resources allocated to it.
- Below configuration uses `large` profile. 

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=mini
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_CLOUD_PROVIDER=gcp
<<<<<<< HEAD
=======
# TODO: Cleanup username,password and email configuration after moving artifacts to public repository
DOCKER_USERNAME=${DOCKER_USERNAME}
DOCKER_PASSWORD=${DOCKER_PASSWORD}

>>>>>>> 4d9619c9901777bc6a79c1c2468654096f12c71c
# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT=gke_dataservices-0001_us-west1-b_saas-dave
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

You can check out [installation]() doc to read more about ports and other configs. 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/gcp.md">
<button type="button">Edit</button></a>

***
