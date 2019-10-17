---
id: step by step guide
title: Step by step guide
sidebar_label: Step by step guide
---
## Step by Step Guide

### Prerequisites

1. [Node.js 10.6](https://nodejs.org/es/download/)
2. [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools)
3. [.NET Core](https://www.microsoft.com/net/download)
4. [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)

### Installation

```shell
npm install
func extensions install
```

Visit [NuGet page](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) for more info about the package versions.


## Development

### Login on Azure

```shell
$ az login
```

### Creating new functions

```shell
$ func new
```

### Local server

**Pull environment variables from Azure**

```shell
$ func azure functionapp fetch ThorFunctionsDev
```

**Start the server**

```shell
$ func host start
```

**Run Test**

```shell
$ npm run test
```
**Debug Test**
- First, insert a new line in your test where you think it might be failing and type ```debugger;```. This will serve as a break point for the debugger to stop at.
- Open up Chrome and type in the address bar : chrome://inspect
- Click on "Open dedicated DevTools for Node"

```shell
$ npm run test:debug
```

**Run Lint check**

```shell
$ npm run lint
```

**Fix Lint errors**

```shell
$ npm run lint:fix
```

### Calling back-office systems

A helper library is included in this project to facilitate making requests to back-office systems. A **client certificate** is required to use the API Gateway. This is deployed as part of the [infrastructure provisioning](https://fala.cl/falabella/thor/deployment/terraform) and it's available to the Azure Functions as environment variables.

**Code example**

```javascript
const ApiGateway = require('../lib/ApiGateway/Request');
const { GATEWAY_CERT, GATEWAY_KEY, GATEWAY_HOSTNAME_FACL } = process.env;

// GATEWAY_CERT = <client certificate>
// GATEWAY_KEY = <client certificate key>
// GATEWAY_HOSTNAME_FACL = chile.falabella.sandbox.onpremise.services

module.exports = function(context, req) {
  const gateway = new ApiGateway(GATEWAY_HOSTNAME_FACL, GATEWAY_CERT, GATEWAY_KEY);
  const path = '/atg5/rest/model/falabella/rest/common/CommonActor/get-order-detail-by-orderId';
  const data = JSON.stringify({ 'orderId': 4526330189 });

  gateway.post(path, data, { 'Content-type': 'application/json' })
      .then(res => {
        context.res = {
          body: res
        };
        context.done();
      })
      .catch(context.done);
};

```

### Function Handlers

[**TargetValidator**](shared/target-validator/index.js)

_Receives a funtion name string and check whether the message contains a TargetFunction parameter and if it is the same to continue processing the message._ 

```
  new AzureMiddleware()
    .use(targetValidator(FUNCTION_NAME))  
```
