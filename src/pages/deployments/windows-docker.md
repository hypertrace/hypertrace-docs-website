---
title: Windows 10
weight: 7
excerpt: Deploying Hypertrace on Windows 10 using Helm
template: docs
---

## Deploying Hypertrace on Windows 10 using Helm:
- `git clone https://github.com/hypertrace/hypertrace.git`
- `cd hypertrace/kubernetes`
- Go to the hypertrace-helm directory.
- Create namespace `hypertrace` by executing `kubectl create ns hypertrace`.
- make sure you are using docker-desktop or any kubernetes context appropriate for platform you are using. You can check your context using `kubectl config current-context`.
- Replace `StorageClass` in `values.yaml` in `clusters/dev` with your StorageClass. Find your storageclass using `kubectl get sc`. Ex for Docker for Desktop it will be `docker-dekstop` and for Minikube it will be `standard` etc.
- Run `helm repo update`
- Run `helm upgrade hypertrace-data-services ./data-services -f ./data-services/values.yaml -f ./clusters/dev/values.yaml --install -n hypertrace --wait --timeout 15m`
- Run `helm dependency update ./platform-services`
- Run `helm upgrade hypertrace-platform-services ./platform-services -f ./platform-services/values.yaml -f ./clusters/dev/values.yaml --install -n hypertrace --wait --timeout 15m`
- Check if you have all pods running using `kubectl get pods -n hypertrace`
- In case your pods are pending troubleshoot with `kubectl describe pods -n hypertrace`. The most common issues with pods pending are insufficient resources (CPU, memory) or used host port. You can find common issues [here.](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/#:~:text=If%20a%20Pod%20is%20stuck,or%20another%20that%20prevent%20scheduling.&text=If%20you%20do%20require%20hostPort,nodes%20in%20your%20Kubernetes%20cluster.)


### Verify installation

- Verify Helm Charts. Successful installation should have the release status as deployed for both `data-services` and `platform-services` as below.
    ``` shell script
    $ helm list --namespace=hypertrace --kube-context=docker-desktop               
     NAME                        	NAMESPACE 	REVISION	UPDATED                             	STATUS  	CHART                             	APP VERSION
     hypertrace-data-services    	hypertrace	1       	2020-06-24 22:19:46.827523 +0530 IST	deployed	hypertrace-data-services-0.1.0    	0.1.0
     hypertrace-platform-services	hypertrace	1       	2020-06-24 22:21:33.41217 +0530 IST 	deployed	hypertrace-platform-services-0.1.0	0.1.0
    ```
### Uninstall
- Run `kubectl delete ns hypertrace`

You can check out [installation](https://docs.hypertrace.org/getting-started/) doc to read more about ports and other configs. 

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/windows-docker.md">
<button type="button">Edit</button></a>

***
