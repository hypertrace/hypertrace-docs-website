---
title: AWS AMI
weight: 7
template: docs
---
## Getting started with Hypertrace using AMI

1. Go to the <a href="https://console.aws.amazon.com/ec2/v2/">EC2 Dashboard in the AWS Management Console</a> and click "Launch instance"
2. Search for Hypertrace. Select Hypertrace AMI within Community AMIs
3. Choose a `t2.xlarge` or `t2.2xlarge` instance
4. Proceed to 'Configure instance details' and complete the steps to launch the instance. Don't forget to save your SSH key.
5. Once your instance is ready. SSH into it with the key you downloaded. 
6. It may take 5 minutes to initialize. 
7. Do `kubectl get services -n hypertrace`
8. Look for hypertrace UI service. 
9. Look for nodeport of UI service which will be 5 digit one(9000:30332 in this case 30332 will be nodeport)
10. Find your EC2 instance IP from console and go to `Instance IP: Node Port` to see UI

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/deployments/ami.md">
<button type="button">Edit</button></a>

***
