---
title: Docker for Desktop
weight: 1
template: docs
---

For deploying Hypertrace on Docker Desktop using Docker Compose, see [Getting Started](https://docs.hypertrace.org/getting-started/)

## Deploying Hypertrace on Docker Desktop using Helm:
- `git clone https://github.com/hypertrace/hypertrace.git`
- `cd hypertrace/kubernetes`
- You have to make some changes in config file as per the [configuration](#Configuration) section below.
- Run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- The default configuration will work for the Docker for Dekstop deployment as discussed in this section. 
- Use the `dev` profile while installing in Docker for Desktop. It is optimized for that purpose. 

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=dev
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_ENV=docker-desktop
# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT=docker-desktop
# Kubernetes context to deploy hypertrace
HT_KUBE_NAMESPACE=hypertrace
# Helm install wait timeout.
# Installation time generally depends time to pull multiple Hypertrace images from the repository.
# Set it higher value if the connection is slower.
# Units in minutes
HT_INSTALL_TIMEOUT=10
# Flag to debug installation issues
# Allowed values: {true, false}
HT_ENABLE_DEBUG=false
```
In case of any issue, install Hypertrace in debug mode to get more logs and traces to identify the rootcause.
- Set `HT_ENABLE_DEBUG` to `true` in `./config/hypertrace.properties`
- Debug `bash -x ./hypertrace.sh install`

### Verify installation

- Verify Helm Charts. Successful installation should have the release status as deployed for both `data-services` and `platform-services` as below.
    ``` shell script
    $ helm list --namespace=hypertrace --kube-context=docker-desktop               
     NAME                        	NAMESPACE 	REVISION	UPDATED                             	STATUS  	CHART                             	APP VERSION
     hypertrace-data-services    	hypertrace	1       	2020-06-24 22:19:46.827523 +0530 IST	deployed	hypertrace-data-services-0.1.0    	0.1.0
     hypertrace-platform-services	hypertrace	1       	2020-06-24 22:21:33.41217 +0530 IST 	deployed	hypertrace-platform-services-0.1.0	0.1.0
    ```
### Uninstall
- Run `./hypertrace.sh uninstall`

You can check out [installation](https://docs.hypertrace.org/getting-started/) doc to read more about ports and other configs. 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/docker.md">
<button type="button">Edit</button></a>

***
