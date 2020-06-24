---
title: Installation
weight: 1
template: docs
---
# Hypertrace: Installation
Get up and running with hypertrace in your local environment

## Deploying hypertrace
There are two ways to deploy hypertrace on your system. You can either use readily available shellscript to install or you can use use classic step by step installtion!

### Easy way:
1. Clone the hypertrace-helm repo on you local machine using `git clone https://github.com/Traceableai/hypertrace-helm.git`
2. Go to the hypertrace-helm directory and run `./standalone.sh install`

### Let's build from the source way:

- Awaiting for the access and response for team.

### We believe you don't need this and work in direction to ensure you won't but in case needed a way to uninstall:

- Go to hypertrace-helm directory and run `./standalone.sh uninstall `

## Hypertrace

Once your hypertrace installation is successful you can navigate to `http://localhost` to access Hypertarce UI. It looks something like this!

| ![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/Hypertrace.png) | 
|:--:| 
| *Hypertrace homepage* |

You can access variety of functionalities including Observability Dashboard, Application flow, Microservices, Web Transactions and Explorer which can help you in troubleshooting!

### Ports

Before we get started more about hypertrace let's see ports it occupies:

| Port  | Service                 |
|-------|-------------------------|
| 80    | Used by Hypertrace UI   |
| 55678 | Opencensus collector    |
| 14267 | Jaeger thrift collector |
| 14268 | Jaeger HTTP collector   |
| 9411  | Zipkin collector        |

In case of any port collisions, users can modify the following properties in helm file (platform-services/values.yaml).

- `ingress.hosts[].paths[].port` - To change UI port
- `oc-collector.service.ports[].targetPort` - To change collector ports