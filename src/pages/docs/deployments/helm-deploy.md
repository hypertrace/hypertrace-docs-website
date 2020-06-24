---
title: Helm 
weight: 1
template: docs
---
## What is helm?
Helm is the package manager for Kubernetes. It streamlines installing and managing Kubernetes applications. We can use a single helm chart to deploy anything from simple pod to a complex application. 

Helm has pretty detailed documentation which you can find over here: https://helm.sh/docs/

## Installing helm

You can install helm using package managers or script or you can even download binary versions manually from the the release and install. 

### Install using script:

```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```

### Install using Package Managers:
#### 1. Homebrew (macOS)

```
# install
brew install helm

# Upgrade
brew upgrade helm

```
#### 2. Chocolatey (Windows)

```
choco install kubernetes-helm
```

#### 3. Apt (Debian/Ubuntu)

```
curl https://helm.baltorepo.com/organization/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

### 4. Snap

```
sudo snap install helm --classic
```

For detailed information about installation you can use helm installation documentation [here](https://helm.sh/docs/intro/install/). 

## Hypertrace-helm

You can find hypertrace helm repo here: https://github.com/Traceableai/hypertrace-helm 

Helm repo contains charts for different services which are as follows:
- Zookeeper
- Kafka
- Avro schema registry
- Istio
- Prometheus operator
- Kafka Exporter
- Kafka Manager
- ElasticSearch
- Logstash
- Kibana
- Fliebeat
- Mongo
- Pinot
- Local volume provisioner
- Metric server

We have divided this services into two categories namely data services and platform services:

- All open services/technologies (zookeeper, kafka, schema registry, pinot, mongo) are grouped into data-services. These services acts as data-store for Hypertrace.
- All other microservices which deals with traces like span collection, trace generation, trace enrichment, views etc. forms another group, platform-services. 

## Deploying hypertrace on docker for desktop using helm:

1. Clone the hypertrace-helm repo on you local machine using `git clone https://github.com/Traceableai/hypertrace-helm.git`
2. Go to the hypertrace-helm directory and run `./standalone.sh install`

You can check out [installtion]() doc to read more about ports and other configs. 


