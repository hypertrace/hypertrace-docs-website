---
title: Docker compose
weight: 2
template: docs
---

### Issue 1: 
Do you observe an error related to an unhealthy container during startup?
like eg.`ERROR: for hypertrace-federated-service Container "2c1c01fd3b59" is unhealthy`

#### Reason: 
lack of resources
Our stack is dependent on pinot and it is a CPU heavy during startup. The depends_on has a max wait time of 1 min.

#### Solution:
Set your resources to a minimum 3 CPUs/4GB and re-run `docker-compose up` .

### Issue 2:
Do you see any exception in `hypertrace-federated-service` container or ingestion pipeline container logs?

### Reason
Probably, you might not have the latest images pulled locally.

####  Solution:
Run `docker-compose pull` to fetch the latest images, and bring up the stack fully. For that first do `docker-compose down --remove-orphans` and run `docker-compose up`.

### Issue 3:
How to clean up your docker-compose setup?

#### Solution:
Once you stop docker-compose, please do `docker-compose down` so it will remove all the containers related to it along with the network. In case you have any orphan containers do `docker-compose down --remove-orphans`. 

### Issue 4:
You have some dangling images or unclean docker environment. 

#### Solution:
Do `docker system prune` and then run `docker-compose up`.

### Issue 5
How do I force recreate an entire stack?

### Solution
Use this command to re-create all containers - `docker-compose up --force-recreate`