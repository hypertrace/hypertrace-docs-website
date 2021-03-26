---
title: Licenses
excerpt: Hypertrace Core is a basic distributed tracing platform. Hypertrace Community Edition, is a combination of Hypertrace Core, plus additional features created by the developers at Traceable Inc. 
template: docs
---
## What license does Hypertrace use?
Hypertrace is two components: Hypertrace Core & [Hypertrace Community Edition](https://github.com/hypertrace/hypertrace). Hypertrace Core is a basic distributed tracing platform and data collection agents. Hypertrace Community Edition, is a combination of Hypertrace Core, plus additional features created by the developers at Traceable Inc.  

Here is a description of each of their licenses. 

![space-1.jpg](https://raw.githubusercontent.com/hypertrace/hypertrace-docs-website/4445a39b36ff521c83f85600185cd5b0b4054988/static/images/hypertrace-components-by-license.png)

## Hypertrace Core (including data collection agents)

Hypertrace Core is fully licensed under the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0). As with any software with an Apache 2.0 license, all users have all of [the essential freedoms](https://www.gnu.org/philosophy/free-sw.html.en). In summary, you have:<br />
- The freedom to run the program as you wish, for any purpose (freedom 0).<br />
- The freedom to study how the program works, and change it so it does your computing as you wish (freedom 1). Access to the source code is a precondition for this.<br />
- The freedom to redistribute copies so you can help others (freedom 2).<br />
- The freedom to distribute copies of your modified versions to others (freedom 3). By doing this you can give the whole community a chance to benefit from your changes. Access to the source code is a precondition for this.<br />

We hope and expect that users will find Hypertrace Core useful and that they will build new and innovative solutions with it. 

<hr />

## Hypertrace Community Edition
Traceable is a SaaS security product built on top of distributed tracing. While building Traceable, we ended up building a complete distributed tracing platform, including data collection agents. We didn’t see any projects that offered the features we had so we decided to release it so others could benefit from it too. And thus Hypertrace was born. 

We wanted to open source  the features in Hypertrace Community Edition as well, but ensure that we can sustain the business investment Traceable built on top of it. The Traceable Community License lets us invest heavily in code that we distribute for free but at the same time protect Traceable. The Confluent Community License is the best example of how this can be achieved and we decided to base our license on it.

Hypertrace Community Edition is licensed under a source available license called the [Traceable Community License version 1.0](https://github.com/hypertrace/hypertrace/blob/main/LICENSE). It is almost a word for word copy of the Confluent Community License version 1.0. The only distinguishable difference between the two licenses is the name of the company offering the license, the products they refer to, and the cities where legal issues must be resolved. 

<hr />

## FAQ

Confluent also has a nice FAQ covering common questions and their rationale, so we've borrowed from theirs and added some details that are specific to Hypertrace.

<hr />

## What is covered under the Traceable Community License?
Traceable is licencing some of the components of Hypertrace Community Edition with a source-available license.

## Tell me what this means
We are committed to an Open Core model.  Open Core means the core of Hypertace Community—Hypertrace Core—is open source and available under the Apache 2.0 license, while certain features of Hypertrace Community Edition are available under the Traceable Community License.

Under the Traceable Community License, you can access the source code and modify or redistribute it; there is only one thing you cannot do, and that is use it to make a competing SaaS offering. Here is the exact language:

“Excluded Purpose” is making available any software-as-a-service, platform-as-a-service, infrastructure-as-a-service or other similar online service that competes with Traceable products or services that provide the Software.

For example, it does not allow hosting of Hypertrace Metrics, Application Flow, Advanced Slice & Dice or other software licensed under the Traceable Community License as online service offerings that compete with Traceable SaaS products or services that provide the same software.  If you are not doing what is excluded, this license will not affect you.

## Will Traceable continue to contribute to Hypertrace Core?
Absolutely. Traceable will continue to make contributions to the development, maintenance and improvement of Hypertrace Core, licensed under Apache 2.0. Hypertrace Core remains the core of Hypertrace Community Edition & Traceable products.

## Why did we do this?
We think it is a necessary step. This lets us invest heavily in both open source and source available code that we distribute for free, while sustaining a business that funds this investment.

We aren’t alone in looking at alternative licensing mechanisms. Other companies have recently sought new open core licensing options. This license is almost a word for word copy of the Traceable Community License version 1.0.  

## Can I download, modify, or redistribute the code?
Yes. The code is all available on GitHub and the license permits it.

## Can I embed Traceable Community software in software I distribute?
Yes, you can.

## Can I embed Traceable Community software in a SaaS offering I create?
Yes, provided the SaaS offering does not fall within the “Excluded Purpose” discussed above.

## Is Traceable Community License open source?
Strictly speaking it is not open source. It is “source-available.” Many people use the phrase “open source” in a loose sense to mean that you can freely download, modify, and redistribute the code, and those things are all true of the code under the Traceable Community License. However, in the strictest sense “open source” means a license approved by the Open Source Initiative (“OSI”) which meets a particular set of criteria. The Traceable Community License is not approved by the OSI and likely would not be as it excludes the use case of creating a SaaS offering of the code. Because of this, we will not refer to the Traceable Community License or any code released under it as open source.

## What if I create a competing service but give it away for free. Is that “competitive?”
Yes. That’s just a competitive product with a price of zero. “Competitive” means that a product or service is an economic substitute.

## I’m confused about what use cases are competitive. What if future Traceable products compete with mine?
Let’s go through a specific example. Say that you are building a SaaS eCommerce Storefront and you want to include Application Flow in the implementation of that offering. Of course you can do that. This service does not compete with any Traceable product that “provides the software”. Note that this would be true, even if in the future Traceable had its own hotel booking product (not likely!). The excluded purpose for Application Flow is limited to competition with Traceable’s SaaS offering of Application Flow.

## My company has a policy against using code with a non-commercial restriction. What should I do?
The Traceable Community License is not a “non-commercial” license restriction. It only prevents one narrow kind of excluded purpose, which is using our software in a competing SaaS offering.

## I’d like to customize some of the Traceable Community software. Can I?
Yes. The Excluded Purpose does not restrict the creation of modifications.

## Why didn’t Traceable use AGPL?
AGPL is too aggressive for our customers who need to redistribute commercial products.  If you put AGPL code in a distributed program, you have to open source the whole program. We want you to be able to embed our code in proprietary applications, change it and not worry about open sourcing any of your changes. We don’t think that proprietary applications are bad, and we think it’s great if you use Traceable Community software to create them.

## Does the Traceable Community License impose a general prohibition against competing with Traceable?
A: It does not. The excluded purpose is the following:

“Making available any software-as-a-service, platform-as-a-service, infrastructure-as-a-service or other similar online service that competes with Traceable products or services that provide the software”

This may be easier to understand with a specific example. Say “the software” that you are licensing is Hypertrace Community. Then the excluded purpose for your use of Hypertrace Community could be read as

“Making available any software-as-a-service, platform-as-a-service, infrastructure-as-a-service or other similar online service that competes with Traceable products or services that provide [Hypertrace Community]”.

In other words, it’s a limitation on your use of [Hypertrace Community] to compete with our [Hypertrace Community] offering. You are not forbidden from competing with other products Traceable has or may have in the future that you have not licensed under the Traceable Community License.

<hr />

We feel this approach is best practice for an Open Core software project. If you believe norms have changed or there is a better alternative, please let us know on <a href="https://twitter.com/HypertraceOrg">Twitter</a> or in our <a href="https://join.slack.com/t/hypertrace/shared_invite/zt-mwobjb29-9aGNnH9yBJ8JL79E5mmq_A">Hypertrace Community workspace</a> on Slack. 

<hr />

<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/licensing/index.md">
<button type="button">Edit</button></a>

***
