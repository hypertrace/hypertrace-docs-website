---
title: Docker compose
weight: 2
template: docs
---

### Issue 1
Do you see the below error on the first startup?

![space-1.jpg](https://s3.amazonaws.com/fininity.tech/DT/docker-compose-error.png) 


#### Reason:
It is because we start all our containers in parallel. And, few things are still running in the background like `pinot` and `config-bootstrapper` job.
#### Solution:
you can use the below query to check the status of stack full availability:
```
wget -qO- http://localhost:2020/graphql\?query\=\{metadata\{name\}\} 
```

Once, the above query returns results, you can refresh/reload UI.
Even if it keeps failing for more than a `2 mins`, you check the status of
`config-bootstrapper` and `pinot` as below:

- `docker ps -a | grep config-bootstrapper`
- `docker ps -a | grep pinot`

<hr />



### Issue 2
Do you see any exception in `hypertrace-federated-service` container or ingestion pipeline container logs?
#### Reason
Probably, you might not have the latest images pulled locally.
####  Solution:
Run `docker-compose pull` to fetch the latest images, and bring up the stack fully. For that first do `docker-compose down --remove-orphans` and run `docker-compose up`.

<hr />

### Issue 3
How to clean up your docker-compose setup?
#### Solution:
- Once you stop docker-compose, please do `docker-compose down` so it will remove all the containers related to it along with the network. 
- In case you have any orphan containers do `docker-compose down --remove-orphans`. 

<hr />

### Issue 4
You have some dangling images or unclean docker environment. 
#### Solution:
Do `docker system prune` and then run `docker-compose up`.

<hr />

### Issue 5
How do I force recreate an entire stack?
#### Solution
Use this command to re-create all containers - `docker-compose up --force-recreate`

<hr />

### Issue 6
Do you observe an error related to an unhealthy container during startup?
like eg.`ERROR: for hypertrace-federated-service Container "2c1c01fd3b59" is unhealthy`
#### Reason: 
In this case, mostly the reson can be lack of resources. The depends_on has a max wait time of 1 min.
#### Solution:
- Check your docker resources, Hyertrace needs minimum 3 CPUs/4GB so if you have any other containers running you might have to increase resource allocation accrodingly. 
- re-run `docker-compose -f docker-compose.yml up`

<hr />


### Issue 6
On windows, you got error saying `image operating system "linux" cannot be used on this platform`.
#### Reason: 
In this case, your docker host might be running windows daemon which only runs windows-containers. 
#### Solution:
In order to run Linux containers, you need to make sure Docker is using the Linux daemon. You can toggle this by selecting Switch to Linux Containers from the action menu when clicking on the Docker whale icon in the system tray. If you see Switch to Windows Containers, then you are already targeting the Linux daemon. 

| ![space-1.jpg](https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/media/switchdaemon.png) | 
|:--:| 
| *Switch Daemons to use Linux containers* |


read more about docker for windows issues and troubleshooting here: https://docs.docker.com/docker-for-windows/troubleshoot/

<hr />