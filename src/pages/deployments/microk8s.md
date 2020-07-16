---
title: MicroK8S
weight: 3
template: docs
---

## Deploying hypertrace on minikube using helm:

- [Join the Hypertrace Workspace](https://www.hypertrace.org/get-started) on Slack
- Download and unzip or unpack the installer file from the 'Early-Access' Slack channel 
- You have to make some changes in config file as per the [configuration](#Configuration) section below.
- Go to the Hypertrace-helm directory and run `./hypertrace.sh install`

## Note:
- As default in `Microk8s` you can use only services like `NodePort` and `ClusterIP`.
- With your setup you can use `NodePort`, `ClusterIP with Ingress` or `MetalLB`. 
- We are using `ClusterIP with Ingress` so you have to remember to enable **ingress and dns addons** in _Microk8s_. 
- It can be done by `$microk8s.enable dns ingress`.
- So once the installation is complete you can access service which uses `LoadBalancer`, in our case _hypertrace-oc-collector_ and _hypertrace-ui_ can be accessed using combination `YourIP:NodePort` where `NodePort` is specific to service. 

## Configuration
- You can customize the configuration under `./config/hypertrace.properties` as needed.
- Default configuration will work for docker for dekstop deployment which we are discussing in this section. 
- use `dev` profile while installing on microk8s on local setup.

Default configuration is as follows:
```bash
# Name of the profile
# Allowed values: {dev, mini, standard}
HT_PROFILE=dev
# Cloud provider name
# Allowed values: {docker-desktop, gcp, aws}
HT_ENV=microk8s
# Kubernetes context to deploy hypertrace
HT_KUBE_CONTEXT=micork8s
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

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/minikube.md">
<button type="button">Edit</button></a>

***
