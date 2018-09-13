---
title: JavaScript developer reference for Azure Functions | Microsoft Docs
description: Understand how to develop Azure Functions using JavaScript.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/06/2017
ms.author: chrande, glenga
ms.openlocfilehash: 060e1145246952c18f89e1088ed28ffb0036e6c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551488"
---
# <a name="azure-functions-javascript-developer-guide"></a>Azure Functions JavaScript developer guide
> [!div class="op_single_selector"]
> * [C# script](functions-reference-csharp.md)
> * [F# script](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

The JavaScript experience for Azure Functions makes it easy to export a function, which is passed a `context` object for communicating with the runtime and for receiving and sending data via bindings.

This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).

## <a name="exporting-a-function"></a>Exporting a function
All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it. This function must always include a `context` object.

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

Bindings of `direction === "in"` are passed along as function arguments, meaning you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs). This functionality is convenient when you only have a trigger with no additional inputs, as you can predictably access your trigger data without referencing your `context` object.

The arguments are always passed along to the function in the order they occur in *function.json*, even if you don't specify them in your exports statement. For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.

All bindings, regardless of direction, are also passed along on the `context` object (see below). 

## <a name="context-object"></a>context object
The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.

The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log` which are required to correctly use the runtime. You can name the object whatever you like (i.e. `ctx` or `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>context.bindings property

```
context.bindings
```
Returns a named object that contains all your input and output data. For instance, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>context.done method
```
context.done([err],[propertyBag])
```

Informs the runtime that your code has finished. You must call `context.done` or the runtime never knows that your function is complete and the execution will time out. 

The `context.done` method allows you to pass back a user-defined error to the runtime, as well as a property bag of properties which will overwrite the properties on the `context.bindings` object.

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>context.log method  

```
context.log(message)
```
Allows you to write to the streaming console logs at the default trace level. There are additional logging methods available on `context.log` that let you write to the console log at other trace levels:


| Method                 | Description                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Writes to error level logging, or lower.   |
| **warn(_message_)**    | Writes to warning level logging, or lower. |
| **info(_message_)**    | Writes to info level logging, or lower.    |
| **verbose(_message_)** | Writes to verbose level logging.           |

The following example writes to the console at the warning trace level:

```javascript
context.log.warn("Something has happened."); 
```
You can set the trace level threshold for logging in the host.json file, or turn it off.  For more information on how to write to the logs, see the next section.

## <a name="writing-trace-output-to-the-console"></a>Writing trace output to the console 

In Functions, you use the `context.log` methods to write trace output to the console. At this point, you cannot use `console.log` to write to the console.

When you call `context.log()` your message is written to the console at the default trace level, which is the _info_ trace level. The following code writes to the console at the info trace level:

```javascript
context.log({hello: 'world'});  
```

This is equivalent to the following code:

```javascript
context.log.info({hello: 'world'});  
```

The following code writes to the console at the error level:

```javascript
context.log.error("An error has occurred.");  
```

Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.  


All `context.log` methods support the same parameter format supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format). Consider the following code that writes to the console using the default trace level:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

This same code can also be written in the following format:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a>Configure the trace level for console logging

Functions lets you define the threshold trace level for writing to the console. This makes it easy to control the way traces are written to the console from your functions. Use the `tracing.consoleLevel` property in the host.json file to set the threshold for all traces written to the console. This setting applies to all functions in your function app. The following example sets the trace threshold to enable verbose logging:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Values of **consoleLevel** correspond to the names of the `context.log` methods. To disable all trace logging to the console, set **consoleLevel** to _off_. For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>HTTP triggers and bindings

HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.  

### <a name="request-object"></a>Request object

The `request` object has the following properties:

| Property      | Description                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | An object that contains the body of the request.               |
| _headers_     | An object that contains the request headers.                   |
| _method_      | The HTTP method of the request.                                |
| _originalUrl_ | The URL of the request.                                        |
| _params_      | An object that contains the routing parameters of the request. |
| _query_       | An object that contains the query parameters.                  |
| _rawBody_     | The body of the message as a string.                           |


### <a name="response-object"></a>Response object

The `response` object has the following properties:

| Property  | Description                                               |
| --------- | --------------------------------------------------------- |
| _body_    | An object that contains the body of the response.         |
| _headers_ | An object that contains the response headers.             |
| _isRaw_   | Indicates that formatting is skipped for the response.    |
| _status_  | The HTTP status code of the response.                     |

### <a name="accessing-the-request-and-response"></a>Accessing the request and response 

When working with HTTP triggers, there are three ways that you can access the HTTP request and response objects:

+ From the named input and output bindings. In this way, the HTTP trigger and bindings work the same as any other binding. The following example sets the response object using a named `response` binding. 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ From `req` and `res` properties on the `context` object. In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern. The following example shows how to access the `req` and `res` objects on the `context`:

    ```javascript
    // You can access your http request off of the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Calling `context.done()`. There is a special kind of HTTP binding that returns the response that is passed to the `context.done()` method. The following HTTP output binding defines a `$return` output parameter:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    This output binding expects you to supply the response when you call `done()` as follows:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version--package-management"></a>Node Version & Package Management
The node version is currently locked at `6.5.0`. We're investigating adding support for more versions and making it configurable.

The following steps let you include packages in your function app: 

1. Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.

2. Click **Debug Console > CMD**.

3. Navigate to `D:\home\site\wwwroot`, then drag your package.json file onto the **wwwroot** folder in the top half of the page.  

    There are other ways to upload files to your function app. For more information, see [How to update function app files](functions-reference.md#a-idfileupdatea-how-to-update-function-app-files). 

4. After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**. This downloads the packages indicated in the package.json file and restarts the function app.

After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example.

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

You should define a `package.json` file at the root of your function app. This lets all functions in the app shared the same cached packages, which gives the best performance. When there are version conflicts, you can resolve the conflict by adding a `package.json` file in the folder of a specific function.  

## <a name="environment-variables"></a>Environment variables
To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>Considerations for JavaScript Functions

You should be aware of the following items when working with JavaScript functions.

### <a name="choose-single-core-app-service-plans"></a>Choose single-core App Service plans

When creating a function app that uses App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores. Today, Functions runs JavaScript functions more efficiently on single-core VMs; using larger VMs will not produce the expected performance improvements. When needed, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale. For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescriptcoffeescript-support"></a>TypeScript/CoffeeScript support
There isn't, yet, any direct support for auto-compiling TypeScript/CoffeeScript via the runtime, so that would all need to be handled outside the runtime, at deployment time. 

## <a name="next-steps"></a>Next steps
For more information, see the following resources:

* [Best Practices for Azure Functions](functions-best-practices.md)
* [Azure Functions developer reference](functions-reference.md)
* [Azure Functions C# developer reference](functions-reference-csharp.md)
* [Azure Functions F# developer reference](functions-reference-fsharp.md)
* [Azure Functions triggers and bindings](functions-triggers-bindings.md)

