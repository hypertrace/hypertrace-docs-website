---
title: Minikube
weight: 2
template: docs
---

## Deploying Hypertrace on Minikube using Helm:

- [Join the Hypertrace Workspace](https://www.hypertrace.org/get-started) on Slack
- Download and unzip or unpack the installer file from the 'Early-Access' Slack channel 
- You have to make some changes in config file as per the [configuration](#Configuration) section below.
- Go to the Hypertrace-helm directory and run `./hypertrace.sh install`

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- Default configuration will work for Docker for Dekstop deployment which we are discussing in this section. 
- use `dev` profile while installing on minkube on local setup. 

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=dev
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_ENV=minikube
# Kubernetes context to deploy Hypertrace
HT_KUBE_CONTEXT=minikube
# Kubernetes context to deploy Hypertrace
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

## Note: 
Services of type `LoadBalancer` (In our case hypertrace-oc-collector and hypertrace-ui) can be exposed via the `minikube tunnel` command. It **must** be run in a separate terminal window to keep the LoadBalancer running. Ctrl-C in the terminal can be used to terminate the process at which time the network routes will be cleaned up.

Ref: https://minikube.sigs.k8s.io/docs/handbook/accessing/#using-minikube-tunnel 

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

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/minikube.md">
<button type="button">Edit</button></a>

***
