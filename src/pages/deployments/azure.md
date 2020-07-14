---
title: Azure AKS
weight: 5
template: docs
---

## Deploying hypertrace on Azure Kubernetes Service using helm:

- [Join the Hypertrace Workspace](https://www.hypertrace.org/get-started) on Slack
- Download and unzip or unpack the installer file from the 'Early-Access' Slack channel 
- Go to the Hypertrace-helm directory and run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- Default configuration will work for docker for dekstop deployment which we are discussing in this section. 
- You can choose from `dev`, `mini` and `standard` profile according to your cluster types. each one has appropriate resources allocated to it.
- Below configuration uses `large` profile. 

### Note: 
In AKS, 4 initial StorageClasses are created:
- `default` - Uses Azure StandardSSD storage to create a Managed Disk. The reclaim policy indicates that the underlying Azure Disk is deleted when the persistent volume that used it is deleted.
- `managed-premium` - Uses Azure Premium storage to create Managed Disk. The reclaim policy again indicates that the underlying Azure Disk is deleted when the persistent volume that used it is deleted.
- `azurefile` - Uses Azure Standard storage to create an Azure File Share. The reclaim policy indicates that the underlying Azure File Share is deleted when the persistent volume that used it is deleted.
- `azurefile-premium` - Uses Azure Premium storage to create an Azure File Share. The reclaim policy indicates that the underlying Azure File Share is deleted when the persistent volume that used it is deleted.

We are using `default` class for our deployment. 

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=mini
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_CLOUD_PROVIDER=azure
# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT=`Your azure context`
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

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/azure.md">
<button type="button">Edit</button></a>

***
