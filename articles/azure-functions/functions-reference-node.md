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
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="3899f-104">Azure Functions JavaScript developer guide</span><span class="sxs-lookup"><span data-stu-id="3899f-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [C# script](functions-reference-csharp.md)
> * [F# script](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

<span data-ttu-id="3899f-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span><span class="sxs-lookup"><span data-stu-id="3899f-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="3899f-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3899f-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="3899f-110">Exporting a function</span><span class="sxs-lookup"><span data-stu-id="3899f-110">Exporting a function</span></span>
<span data-ttu-id="3899f-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span><span class="sxs-lookup"><span data-stu-id="3899f-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="3899f-112">This function must always include a `context` object.</span><span class="sxs-lookup"><span data-stu-id="3899f-112">This function must always include a `context` object.</span></span>

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

<span data-ttu-id="3899f-113">Bindings of `direction === "in"` are passed along as function arguments, meaning you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span><span class="sxs-lookup"><span data-stu-id="3899f-113">Bindings of `direction === "in"` are passed along as function arguments, meaning you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="3899f-114">This functionality is convenient when you only have a trigger with no additional inputs, as you can predictably access your trigger data without referencing your `context` object.</span><span class="sxs-lookup"><span data-stu-id="3899f-114">This functionality is convenient when you only have a trigger with no additional inputs, as you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="3899f-115">The arguments are always passed along to the function in the order they occur in *function.json*, even if you don't specify them in your exports statement.</span><span class="sxs-lookup"><span data-stu-id="3899f-115">The arguments are always passed along to the function in the order they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="3899f-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="3899f-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="3899f-117">All bindings, regardless of direction, are also passed along on the `context` object (see below).</span><span class="sxs-lookup"><span data-stu-id="3899f-117">All bindings, regardless of direction, are also passed along on the `context` object (see below).</span></span> 

## <a name="context-object"></a><span data-ttu-id="3899f-118">context object</span><span class="sxs-lookup"><span data-stu-id="3899f-118">context object</span></span>
<span data-ttu-id="3899f-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span><span class="sxs-lookup"><span data-stu-id="3899f-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="3899f-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log` which are required to correctly use the runtime.</span><span class="sxs-lookup"><span data-stu-id="3899f-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log` which are required to correctly use the runtime.</span></span> <span data-ttu-id="3899f-121">You can name the object whatever you like (i.e. `ctx` or `c`).</span><span class="sxs-lookup"><span data-stu-id="3899f-121">You can name the object whatever you like (i.e. `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="3899f-122">context.bindings property</span><span class="sxs-lookup"><span data-stu-id="3899f-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="3899f-123">Returns a named object that contains all your input and output data.</span><span class="sxs-lookup"><span data-stu-id="3899f-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="3899f-124">For instance, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span><span class="sxs-lookup"><span data-stu-id="3899f-124">For instance, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

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

### <a name="contextdone-method"></a><span data-ttu-id="3899f-125">context.done method</span><span class="sxs-lookup"><span data-stu-id="3899f-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="3899f-126">Informs the runtime that your code has finished.</span><span class="sxs-lookup"><span data-stu-id="3899f-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="3899f-127">You must call `context.done` or the runtime never knows that your function is complete and the execution will time out.</span><span class="sxs-lookup"><span data-stu-id="3899f-127">You must call `context.done` or the runtime never knows that your function is complete and the execution will time out.</span></span> 

<span data-ttu-id="3899f-128">The `context.done` method allows you to pass back a user-defined error to the runtime, as well as a property bag of properties which will overwrite the properties on the `context.bindings` object.</span><span class="sxs-lookup"><span data-stu-id="3899f-128">The `context.done` method allows you to pass back a user-defined error to the runtime, as well as a property bag of properties which will overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="3899f-129">context.log method</span><span class="sxs-lookup"><span data-stu-id="3899f-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="3899f-130">Allows you to write to the streaming console logs at the default trace level.</span><span class="sxs-lookup"><span data-stu-id="3899f-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="3899f-131">There are additional logging methods available on `context.log` that let you write to the console log at other trace levels:</span><span class="sxs-lookup"><span data-stu-id="3899f-131">There are additional logging methods available on `context.log` that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="3899f-132">Method</span><span class="sxs-lookup"><span data-stu-id="3899f-132">Method</span></span>                 | <span data-ttu-id="3899f-133">Description</span><span class="sxs-lookup"><span data-stu-id="3899f-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="3899f-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3899f-134">**error(_message_)**</span></span>   | <span data-ttu-id="3899f-135">Writes to error level logging, or lower.</span><span class="sxs-lookup"><span data-stu-id="3899f-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="3899f-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3899f-136">**warn(_message_)**</span></span>    | <span data-ttu-id="3899f-137">Writes to warning level logging, or lower.</span><span class="sxs-lookup"><span data-stu-id="3899f-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="3899f-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3899f-138">**info(_message_)**</span></span>    | <span data-ttu-id="3899f-139">Writes to info level logging, or lower.</span><span class="sxs-lookup"><span data-stu-id="3899f-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="3899f-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3899f-140">**verbose(_message_)**</span></span> | <span data-ttu-id="3899f-141">Writes to verbose level logging.</span><span class="sxs-lookup"><span data-stu-id="3899f-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="3899f-142">The following example writes to the console at the warning trace level:</span><span class="sxs-lookup"><span data-stu-id="3899f-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="3899f-143">You can set the trace level threshold for logging in the host.json file, or turn it off.</span><span class="sxs-lookup"><span data-stu-id="3899f-143">You can set the trace level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="3899f-144">For more information on how to write to the logs, see the next section.</span><span class="sxs-lookup"><span data-stu-id="3899f-144">For more information on how to write to the logs, see the next section.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="3899f-145">Writing trace output to the console</span><span class="sxs-lookup"><span data-stu-id="3899f-145">Writing trace output to the console</span></span> 

<span data-ttu-id="3899f-146">In Functions, you use the `context.log` methods to write trace output to the console.</span><span class="sxs-lookup"><span data-stu-id="3899f-146">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="3899f-147">At this point, you cannot use `console.log` to write to the console.</span><span class="sxs-lookup"><span data-stu-id="3899f-147">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="3899f-148">When you call `context.log()` your message is written to the console at the default trace level, which is the _info_ trace level.</span><span class="sxs-lookup"><span data-stu-id="3899f-148">When you call `context.log()` your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="3899f-149">The following code writes to the console at the info trace level:</span><span class="sxs-lookup"><span data-stu-id="3899f-149">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="3899f-150">This is equivalent to the following code:</span><span class="sxs-lookup"><span data-stu-id="3899f-150">This is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="3899f-151">The following code writes to the console at the error level:</span><span class="sxs-lookup"><span data-stu-id="3899f-151">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="3899f-152">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span><span class="sxs-lookup"><span data-stu-id="3899f-152">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="3899f-153">All `context.log` methods support the same parameter format supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="3899f-153">All `context.log` methods support the same parameter format supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="3899f-154">Consider the following code that writes to the console using the default trace level:</span><span class="sxs-lookup"><span data-stu-id="3899f-154">Consider the following code that writes to the console using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="3899f-155">This same code can also be written in the following format:</span><span class="sxs-lookup"><span data-stu-id="3899f-155">This same code can also be written in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="3899f-156">Configure the trace level for console logging</span><span class="sxs-lookup"><span data-stu-id="3899f-156">Configure the trace level for console logging</span></span>

<span data-ttu-id="3899f-157">Functions lets you define the threshold trace level for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="3899f-157">Functions lets you define the threshold trace level for writing to the console.</span></span> <span data-ttu-id="3899f-158">This makes it easy to control the way traces are written to the console from your functions.</span><span class="sxs-lookup"><span data-stu-id="3899f-158">This makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="3899f-159">Use the `tracing.consoleLevel` property in the host.json file to set the threshold for all traces written to the console.</span><span class="sxs-lookup"><span data-stu-id="3899f-159">Use the `tracing.consoleLevel` property in the host.json file to set the threshold for all traces written to the console.</span></span> <span data-ttu-id="3899f-160">This setting applies to all functions in your function app.</span><span class="sxs-lookup"><span data-stu-id="3899f-160">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="3899f-161">The following example sets the trace threshold to enable verbose logging:</span><span class="sxs-lookup"><span data-stu-id="3899f-161">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="3899f-162">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span><span class="sxs-lookup"><span data-stu-id="3899f-162">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="3899f-163">To disable all trace logging to the console, set **consoleLevel** to _off_.</span><span class="sxs-lookup"><span data-stu-id="3899f-163">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="3899f-164">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="3899f-164">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="3899f-165">HTTP triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="3899f-165">HTTP triggers and bindings</span></span>

<span data-ttu-id="3899f-166">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span><span class="sxs-lookup"><span data-stu-id="3899f-166">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="3899f-167">Request object</span><span class="sxs-lookup"><span data-stu-id="3899f-167">Request object</span></span>

<span data-ttu-id="3899f-168">The `request` object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="3899f-168">The `request` object has the following properties:</span></span>

| <span data-ttu-id="3899f-169">Property</span><span class="sxs-lookup"><span data-stu-id="3899f-169">Property</span></span>      | <span data-ttu-id="3899f-170">Description</span><span class="sxs-lookup"><span data-stu-id="3899f-170">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="3899f-171">_body_</span><span class="sxs-lookup"><span data-stu-id="3899f-171">_body_</span></span>        | <span data-ttu-id="3899f-172">An object that contains the body of the request.</span><span class="sxs-lookup"><span data-stu-id="3899f-172">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="3899f-173">_headers_</span><span class="sxs-lookup"><span data-stu-id="3899f-173">_headers_</span></span>     | <span data-ttu-id="3899f-174">An object that contains the request headers.</span><span class="sxs-lookup"><span data-stu-id="3899f-174">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="3899f-175">_method_</span><span class="sxs-lookup"><span data-stu-id="3899f-175">_method_</span></span>      | <span data-ttu-id="3899f-176">The HTTP method of the request.</span><span class="sxs-lookup"><span data-stu-id="3899f-176">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="3899f-177">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="3899f-177">_originalUrl_</span></span> | <span data-ttu-id="3899f-178">The URL of the request.</span><span class="sxs-lookup"><span data-stu-id="3899f-178">The URL of the request.</span></span>                                        |
| <span data-ttu-id="3899f-179">_params_</span><span class="sxs-lookup"><span data-stu-id="3899f-179">_params_</span></span>      | <span data-ttu-id="3899f-180">An object that contains the routing parameters of the request.</span><span class="sxs-lookup"><span data-stu-id="3899f-180">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="3899f-181">_query_</span><span class="sxs-lookup"><span data-stu-id="3899f-181">_query_</span></span>       | <span data-ttu-id="3899f-182">An object that contains the query parameters.</span><span class="sxs-lookup"><span data-stu-id="3899f-182">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="3899f-183">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="3899f-183">_rawBody_</span></span>     | <span data-ttu-id="3899f-184">The body of the message as a string.</span><span class="sxs-lookup"><span data-stu-id="3899f-184">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="3899f-185">Response object</span><span class="sxs-lookup"><span data-stu-id="3899f-185">Response object</span></span>

<span data-ttu-id="3899f-186">The `response` object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="3899f-186">The `response` object has the following properties:</span></span>

| <span data-ttu-id="3899f-187">Property</span><span class="sxs-lookup"><span data-stu-id="3899f-187">Property</span></span>  | <span data-ttu-id="3899f-188">Description</span><span class="sxs-lookup"><span data-stu-id="3899f-188">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="3899f-189">_body_</span><span class="sxs-lookup"><span data-stu-id="3899f-189">_body_</span></span>    | <span data-ttu-id="3899f-190">An object that contains the body of the response.</span><span class="sxs-lookup"><span data-stu-id="3899f-190">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="3899f-191">_headers_</span><span class="sxs-lookup"><span data-stu-id="3899f-191">_headers_</span></span> | <span data-ttu-id="3899f-192">An object that contains the response headers.</span><span class="sxs-lookup"><span data-stu-id="3899f-192">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="3899f-193">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="3899f-193">_isRaw_</span></span>   | <span data-ttu-id="3899f-194">Indicates that formatting is skipped for the response.</span><span class="sxs-lookup"><span data-stu-id="3899f-194">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="3899f-195">_status_</span><span class="sxs-lookup"><span data-stu-id="3899f-195">_status_</span></span>  | <span data-ttu-id="3899f-196">The HTTP status code of the response.</span><span class="sxs-lookup"><span data-stu-id="3899f-196">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="3899f-197">Accessing the request and response</span><span class="sxs-lookup"><span data-stu-id="3899f-197">Accessing the request and response</span></span> 

<span data-ttu-id="3899f-198">When working with HTTP triggers, there are three ways that you can access the HTTP request and response objects:</span><span class="sxs-lookup"><span data-stu-id="3899f-198">When working with HTTP triggers, there are three ways that you can access the HTTP request and response objects:</span></span>

+ <span data-ttu-id="3899f-199">From the named input and output bindings.</span><span class="sxs-lookup"><span data-stu-id="3899f-199">From the named input and output bindings.</span></span> <span data-ttu-id="3899f-200">In this way, the HTTP trigger and bindings work the same as any other binding.</span><span class="sxs-lookup"><span data-stu-id="3899f-200">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="3899f-201">The following example sets the response object using a named `response` binding.</span><span class="sxs-lookup"><span data-stu-id="3899f-201">The following example sets the response object using a named `response` binding.</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="3899f-202">From `req` and `res` properties on the `context` object.</span><span class="sxs-lookup"><span data-stu-id="3899f-202">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="3899f-203">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span><span class="sxs-lookup"><span data-stu-id="3899f-203">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="3899f-204">The following example shows how to access the `req` and `res` objects on the `context`:</span><span class="sxs-lookup"><span data-stu-id="3899f-204">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off of the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="3899f-205">Calling `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="3899f-205">Calling `context.done()`.</span></span> <span data-ttu-id="3899f-206">There is a special kind of HTTP binding that returns the response that is passed to the `context.done()` method.</span><span class="sxs-lookup"><span data-stu-id="3899f-206">There is a special kind of HTTP binding that returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="3899f-207">The following HTTP output binding defines a `$return` output parameter:</span><span class="sxs-lookup"><span data-stu-id="3899f-207">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="3899f-208">This output binding expects you to supply the response when you call `done()` as follows:</span><span class="sxs-lookup"><span data-stu-id="3899f-208">This output binding expects you to supply the response when you call `done()` as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version--package-management"></a><span data-ttu-id="3899f-209">Node Version & Package Management</span><span class="sxs-lookup"><span data-stu-id="3899f-209">Node Version & Package Management</span></span>
<span data-ttu-id="3899f-210">The node version is currently locked at `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="3899f-210">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="3899f-211">We're investigating adding support for more versions and making it configurable.</span><span class="sxs-lookup"><span data-stu-id="3899f-211">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="3899f-212">The following steps let you include packages in your function app:</span><span class="sxs-lookup"><span data-stu-id="3899f-212">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="3899f-213">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3899f-213">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="3899f-214">Click **Debug Console > CMD**.</span><span class="sxs-lookup"><span data-stu-id="3899f-214">Click **Debug Console > CMD**.</span></span>

3. <span data-ttu-id="3899f-215">Navigate to `D:\home\site\wwwroot`, then drag your package.json file onto the **wwwroot** folder in the top half of the page.</span><span class="sxs-lookup"><span data-stu-id="3899f-215">Navigate to `D:\home\site\wwwroot`, then drag your package.json file onto the **wwwroot** folder in the top half of the page.</span></span>  

    <span data-ttu-id="3899f-216">There are other ways to upload files to your function app.</span><span class="sxs-lookup"><span data-stu-id="3899f-216">There are other ways to upload files to your function app.</span></span> <span data-ttu-id="3899f-217">For more information, see [How to update function app files](functions-reference.md#a-idfileupdatea-how-to-update-function-app-files).</span><span class="sxs-lookup"><span data-stu-id="3899f-217">For more information, see [How to update function app files](functions-reference.md#a-idfileupdatea-how-to-update-function-app-files).</span></span> 

4. <span data-ttu-id="3899f-218">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span><span class="sxs-lookup"><span data-stu-id="3899f-218">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span> <span data-ttu-id="3899f-219">This downloads the packages indicated in the package.json file and restarts the function app.</span><span class="sxs-lookup"><span data-stu-id="3899f-219">This downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="3899f-220">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="3899f-220">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example.</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="3899f-221">You should define a `package.json` file at the root of your function app.</span><span class="sxs-lookup"><span data-stu-id="3899f-221">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="3899f-222">This lets all functions in the app shared the same cached packages, which gives the best performance.</span><span class="sxs-lookup"><span data-stu-id="3899f-222">This lets all functions in the app shared the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="3899f-223">When there are version conflicts, you can resolve the conflict by adding a `package.json` file in the folder of a specific function.</span><span class="sxs-lookup"><span data-stu-id="3899f-223">When there are version conflicts, you can resolve the conflict by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="3899f-224">Environment variables</span><span class="sxs-lookup"><span data-stu-id="3899f-224">Environment variables</span></span>
<span data-ttu-id="3899f-225">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span><span class="sxs-lookup"><span data-stu-id="3899f-225">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="3899f-226">Considerations for JavaScript Functions</span><span class="sxs-lookup"><span data-stu-id="3899f-226">Considerations for JavaScript Functions</span></span>

<span data-ttu-id="3899f-227">You should be aware of the following items when working with JavaScript functions.</span><span class="sxs-lookup"><span data-stu-id="3899f-227">You should be aware of the following items when working with JavaScript functions.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="3899f-228">Choose single-core App Service plans</span><span class="sxs-lookup"><span data-stu-id="3899f-228">Choose single-core App Service plans</span></span>

<span data-ttu-id="3899f-229">When creating a function app that uses App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span><span class="sxs-lookup"><span data-stu-id="3899f-229">When creating a function app that uses App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="3899f-230">Today, Functions runs JavaScript functions more efficiently on single-core VMs; using larger VMs will not produce the expected performance improvements.</span><span class="sxs-lookup"><span data-stu-id="3899f-230">Today, Functions runs JavaScript functions more efficiently on single-core VMs; using larger VMs will not produce the expected performance improvements.</span></span> <span data-ttu-id="3899f-231">When needed, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span><span class="sxs-lookup"><span data-stu-id="3899f-231">When needed, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="3899f-232">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3899f-232">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescriptcoffeescript-support"></a><span data-ttu-id="3899f-233">TypeScript/CoffeeScript support</span><span class="sxs-lookup"><span data-stu-id="3899f-233">TypeScript/CoffeeScript support</span></span>
<span data-ttu-id="3899f-234">There isn't, yet, any direct support for auto-compiling TypeScript/CoffeeScript via the runtime, so that would all need to be handled outside the runtime, at deployment time.</span><span class="sxs-lookup"><span data-stu-id="3899f-234">There isn't, yet, any direct support for auto-compiling TypeScript/CoffeeScript via the runtime, so that would all need to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3899f-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="3899f-235">Next steps</span></span>
<span data-ttu-id="3899f-236">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="3899f-236">For more information, see the following resources:</span></span>

* [<span data-ttu-id="3899f-237">Best Practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3899f-237">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="3899f-238">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="3899f-238">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="3899f-239">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="3899f-239">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="3899f-240">Azure Functions F# developer reference</span><span class="sxs-lookup"><span data-stu-id="3899f-240">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="3899f-241">Azure Functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="3899f-241">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

