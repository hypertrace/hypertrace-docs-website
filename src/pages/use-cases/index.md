---
title: Use Cases
excerpt: >-
  Hypertrace supports many observability use cases, here are several to consider.
template: docs
---
## Root cause analysis
Customers contact you with a request or application ID that failed. Hypertrace
can show all the services, endpoints and backends that request hit along the
way, contextualizing any errors that occurred. When a root cause becomes
evident, you can drill into that endpoint or backend and see if the problem was
overall or specific to that request. Hypertrace points you at the root cause
faster.

<hr />


## Watch roll-outs
Upgrades can mean new services are involved, possibly impacting existing teams.
During an upgrade, service and backend teams can see how their performance
compares to the last hour and query to see if an upgraded or new service is
causing slow requests.

<hr />


## Understand if performance is better
Anyone in a DevOps role can validate if a change made something better or worse,
by viewing similar traces. Traces can show if calls are indeed parallel or if
caches are in use. Further, "top call" ranking can help teams focus on endpoints
that need the most work.

<hr />


## Monitor microservice dependency
Hypertrace aggregates traces, which allows it to know the source of traffic.
Service and backend views include upstream services. Service owners can see
everything calling them or query to track-down everything they call, even if it
is several layers deep into the network.

<hr />


## Observability
Hypertrace UI includes a global dashboard as well as service and backend
specific views. Together, these allow different teams with different goals to be
on the same page with regards to overall performance. As top calls are ranked,
those looking at any scope can learn what's different now vs an hour or a week
ago.

<hr />



<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/use-cases/index.md">
<button type="button">Edit</button></a>

***


