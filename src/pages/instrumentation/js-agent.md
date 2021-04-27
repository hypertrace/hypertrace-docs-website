---
title: Javascript Instrumentation
subtitle: Instrument your Javascript application with OpenTelemetry JS. 
weight: 4
template: docs
---

## Instrument you JS application with OpenTelemetry JS

To get started with instrumenting your JS application, you have to do following three steps. 
- Install the required OpenTelemetry libraries
- Initialize a global [tracer](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md#tracer)
- Initialize and register a [span exporter](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/sdk.md#span-exporter)

Let's understand the process with NodeJS example. 

### Instrument NodeJS application
Let's consider the sample application like below:

- app.js
```javascript
"use strict";
const PORT = process.env.PORT || "8080";
const express = require("express");
const app = express();
const { countAllRequests } = require("./monitoring");
app.use(countAllRequests());
app.get("/", (req, res) => { res.send("Hello World"); });
app.listen(parseInt(PORT, 10), () => { console.log(`Listening for requests on http://localhost:${PORT}`); });
```

To get started with instrumentation, first you need to add following dependencies in your `package.json` file and run `npm install`.

- package.json
```json
{
  "dependencies": {
    "@opentelemetry/core": "^0.12.0",
    "@opentelemetry/metrics": "^0.12.0",
    "@opentelemetry/node": "^0.12.0",
    "@opentelemetry/plugin-express": "^0.10.0",
    "@opentelemetry/plugin-http": "^0.12.0",
    "@opentelemetry/plugin-https": "^0.12.0",
    "express": "^4.17.1"
  }
}
```
Then, we will be using following file to add initializer/ Tracer provider and console exporter. 

- tracing.js
```javascript
'use strict';
const { LogLevel } = require("@opentelemetry/core");
const { NodeTracerProvider } = require("@opentelemetry/node");
const { SimpleSpanProcessor, ConsoleSpanExporter } = require("@opentelemetry/tracing");
const provider = new NodeTracerProvider({ logLevel: LogLevel.ERROR });
provider.register();
provider.addSpanProcessor(new SimpleSpanProcessor(new ConsoleSpanExporter()));
console.log("tracing initialized");
```
If you run your application now with `node -r ./tracing.js app.js`, it will create and propagate traces over HTTP. If an already instrumented service that supports Trace Context headers calls your application using HTTP, and you call another application using HTTP, the Trace Context headers will be correctly propagated. `Console exporter` will export spans to console. 

Once you run `node -r ./tracing.js app.js` , add some load to the app, e.g. `curl http://localhost:8080`. 

Visit Hypertrace dashboard on `http://<Hypertrace IP Address>:2020` to see trace data and insights. 

### Instrument Browser application with OpenTelemetry JS

If you want to instrument your application in HTML & javascript, follow the steps in OpenTelemetry JS browser app instrumentation documentation [here](https://opentelemetry.io/docs/js/getting_started/browser/).

#### References
- [OpenTelemetry JS](https://github.com/open-telemetry/opentelemetry-js)
- [OpenTelemtry JS documentation](https://opentelemetry.io/docs/js/)
- [OpenTelemetry JS for Browser applications](https://opentelemetry.io/docs/js/getting_started/browser/)
- [OpenTelemtry JS for NodeJS applications](https://opentelemetry.io/docs/js/getting_started/nodejs/)
- [OpenTelemetry JS examples](https://github.com/open-telemetry/opentelemetry-js/tree/main/examples)

***

<a href="https://github.com/hypertrace/hypertrace-docs-website/blob/master/src/pages/instrumentation/js-agent.md">
<button type="button">Edit</button></a>

***