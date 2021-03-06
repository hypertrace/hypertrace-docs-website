---
title: AWS AMI
weight: 8
template: docs
---
## Getting started with Hypertrace using AMI

1. Go to [AWS EC2 console](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#Instances:sort=dnsName) and click on launch instance.
    - Search for Hypertrace and click on Hypertrace AMI.
    - Go with default configurartions on `Instance Details` page and `add storage` page.
    - In `security group` settings, you can only open nodeport and other ports which you want to access after checking in instance or for now you can go with `all TCP` ports open (which is not recommended in security perspective but considering this is test instance you can do that if you want.)
    - Click on `Review and launch` 
2. Once your instance is ready, click on a connect button on the dashboard and follow the instructions to SSH into your instance.
6. The instace you just setup is a Ubuntu VM running Hypertrace on Microk8s.
7. Run `kubectl get services -n hypertrace`
8. Look for the hypertrace UI service. 
9. Look for the port of UI service which will be 5 digits (9000:30332 in this case 30332)
10. Find your EC2 instance IP from console and go to `Instance IP: Port` to see UI

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/ami.md">
<button type="button">Edit</button></a>

***
