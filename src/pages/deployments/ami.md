---
title: AWS AMI
weight: 7
template: docs
---
## Getting started with Hypertrace using AMI

1. Go to AWS EC2 console and click on launch instance
2. Search for hypertrace and clock on hypertrace AMI
3. Choose instance `t2.xlarge` or `t2.2xlarge`
4. Proceed to next steps and complete configurations for security groups and other things. At the end launch instance
5. Once your instance is ready. Ssh into it. 
6. It’s a ubuntu VM
7. Do `kubectl get services -n hypertrace`
8. Look for hypertrace UI service. 
9. Look for nodeport of UI service which will be 5 digit one(9000:30332 in this case 30332 will be nodeport)
10. Find your EC2 instance Ip from console and go to `Instance IP: Node Port` to see UI

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/ami.md">
<button type="button">Edit</button></a>

***