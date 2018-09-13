---
title: Azure Functions Mobile Apps bindings | Microsoft Docs
description: Understand how to use Azure Mobile Apps bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553316"
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="03253-104">Azure Functions Mobile Apps bindings</span><span class="sxs-lookup"><span data-stu-id="03253-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="03253-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="03253-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="03253-106">Azure Functions supports input and output bindings for Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="03253-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="03253-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span><span class="sxs-lookup"><span data-stu-id="03253-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="03253-108">Mobile Apps input binding</span><span class="sxs-lookup"><span data-stu-id="03253-108">Mobile Apps input binding</span></span>
<span data-ttu-id="03253-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span><span class="sxs-lookup"><span data-stu-id="03253-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="03253-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span><span class="sxs-lookup"><span data-stu-id="03253-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="03253-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="03253-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="03253-112">Note the following:</span><span class="sxs-lookup"><span data-stu-id="03253-112">Note the following:</span></span>

* <span data-ttu-id="03253-113">`id` can be static, or it can be based on the trigger that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="03253-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="03253-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span><span class="sxs-lookup"><span data-stu-id="03253-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="03253-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span><span class="sxs-lookup"><span data-stu-id="03253-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="03253-116">The function uses this URL to construct the required REST operations against your mobile app.</span><span class="sxs-lookup"><span data-stu-id="03253-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="03253-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span><span class="sxs-lookup"><span data-stu-id="03253-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="03253-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="03253-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="03253-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span><span class="sxs-lookup"><span data-stu-id="03253-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="03253-120">This API key must not be shared with your mobile app clients.</span><span class="sxs-lookup"><span data-stu-id="03253-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="03253-121">It should only be distributed securely to service-side clients, like Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="03253-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="03253-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span><span class="sxs-lookup"><span data-stu-id="03253-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="03253-123">This safeguards your sensitive information.</span><span class="sxs-lookup"><span data-stu-id="03253-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="03253-124">Input usage</span><span class="sxs-lookup"><span data-stu-id="03253-124">Input usage</span></span>
<span data-ttu-id="03253-125">This section shows you how to use your Mobile Apps input binding in your function code.</span><span class="sxs-lookup"><span data-stu-id="03253-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="03253-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span><span class="sxs-lookup"><span data-stu-id="03253-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="03253-127">When the record is not found, the parameter is `null`.</span><span class="sxs-lookup"><span data-stu-id="03253-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="03253-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span><span class="sxs-lookup"><span data-stu-id="03253-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="03253-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span><span class="sxs-lookup"><span data-stu-id="03253-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="03253-130">You cannot modify a record in Node.js.</span><span class="sxs-lookup"><span data-stu-id="03253-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="03253-131">Input sample</span><span class="sxs-lookup"><span data-stu-id="03253-131">Input sample</span></span>
<span data-ttu-id="03253-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span><span class="sxs-lookup"><span data-stu-id="03253-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="03253-133">See the language-specific sample that uses the input record from the binding.</span><span class="sxs-lookup"><span data-stu-id="03253-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="03253-134">The C# and F# samples also modify the record's `text` property.</span><span class="sxs-lookup"><span data-stu-id="03253-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="03253-135">C#</span><span class="sxs-lookup"><span data-stu-id="03253-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="03253-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="03253-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="03253-137">Input sample in C#</span><span class="sxs-lookup"><span data-stu-id="03253-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="03253-138">Input sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="03253-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="03253-139">Mobile Apps output binding</span><span class="sxs-lookup"><span data-stu-id="03253-139">Mobile Apps output binding</span></span>
<span data-ttu-id="03253-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span><span class="sxs-lookup"><span data-stu-id="03253-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="03253-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="03253-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="03253-142">Note the following:</span><span class="sxs-lookup"><span data-stu-id="03253-142">Note the following:</span></span>

* <span data-ttu-id="03253-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span><span class="sxs-lookup"><span data-stu-id="03253-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="03253-144">The function uses this URL to construct the required REST operations against your mobile app.</span><span class="sxs-lookup"><span data-stu-id="03253-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="03253-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span><span class="sxs-lookup"><span data-stu-id="03253-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="03253-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="03253-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="03253-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span><span class="sxs-lookup"><span data-stu-id="03253-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="03253-148">This API key must not be shared with your mobile app clients.</span><span class="sxs-lookup"><span data-stu-id="03253-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="03253-149">It should only be distributed securely to service-side clients, like Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="03253-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="03253-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span><span class="sxs-lookup"><span data-stu-id="03253-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="03253-151">This safeguards your sensitive information.</span><span class="sxs-lookup"><span data-stu-id="03253-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="03253-152">Output usage</span><span class="sxs-lookup"><span data-stu-id="03253-152">Output usage</span></span>
<span data-ttu-id="03253-153">This section shows you how to use your Mobile Apps output binding in your function code.</span><span class="sxs-lookup"><span data-stu-id="03253-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="03253-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span><span class="sxs-lookup"><span data-stu-id="03253-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="03253-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span><span class="sxs-lookup"><span data-stu-id="03253-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="03253-156">Output sample</span><span class="sxs-lookup"><span data-stu-id="03253-156">Output sample</span></span>
<span data-ttu-id="03253-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span><span class="sxs-lookup"><span data-stu-id="03253-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="03253-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span><span class="sxs-lookup"><span data-stu-id="03253-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="03253-159">C#</span><span class="sxs-lookup"><span data-stu-id="03253-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="03253-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="03253-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="03253-161">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="03253-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="03253-162">Output sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="03253-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="03253-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="03253-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

