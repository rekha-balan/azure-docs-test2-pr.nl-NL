---
title: Azure Functions Service Bus triggers and bindings | Microsoft Docs
description: Understand how to use Azure Service Bus triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: chrande; glenga
ms.openlocfilehash: 6644f6b879e48787249111c5e02b75b963f1e1cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563304"
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="8abae-104">Azure Functions Service Bus bindings</span><span class="sxs-lookup"><span data-stu-id="8abae-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="8abae-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8abae-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> <span data-ttu-id="8abae-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span><span class="sxs-lookup"><span data-stu-id="8abae-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="8abae-107">Service Bus trigger</span><span class="sxs-lookup"><span data-stu-id="8abae-107">Service Bus trigger</span></span>
<span data-ttu-id="8abae-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span><span class="sxs-lookup"><span data-stu-id="8abae-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="8abae-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="8abae-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="8abae-110">*queue* trigger:</span><span class="sxs-lookup"><span data-stu-id="8abae-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="8abae-111">*topic* trigger:</span><span class="sxs-lookup"><span data-stu-id="8abae-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="8abae-112">Note the following:</span><span class="sxs-lookup"><span data-stu-id="8abae-112">Note the following:</span></span>

* <span data-ttu-id="8abae-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Hub namespace, then specify the name of the app setting in the `connection` property in your trigger.</span><span class="sxs-lookup"><span data-stu-id="8abae-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Hub namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="8abae-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="8abae-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="8abae-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span><span class="sxs-lookup"><span data-stu-id="8abae-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="8abae-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="8abae-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="8abae-117">For `accessRights`, available values are `manage` and `listen`.</span><span class="sxs-lookup"><span data-stu-id="8abae-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="8abae-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span><span class="sxs-lookup"><span data-stu-id="8abae-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="8abae-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span><span class="sxs-lookup"><span data-stu-id="8abae-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="8abae-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span><span class="sxs-lookup"><span data-stu-id="8abae-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="8abae-121">Trigger behavior</span><span class="sxs-lookup"><span data-stu-id="8abae-121">Trigger behavior</span></span>
* <span data-ttu-id="8abae-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span><span class="sxs-lookup"><span data-stu-id="8abae-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="8abae-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="8abae-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="8abae-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="8abae-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="8abae-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span><span class="sxs-lookup"><span data-stu-id="8abae-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="8abae-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span><span class="sxs-lookup"><span data-stu-id="8abae-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="8abae-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span><span class="sxs-lookup"><span data-stu-id="8abae-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="8abae-128">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="8abae-128">Trigger usage</span></span>
<span data-ttu-id="8abae-129">This section shows you how to use your Service Hub trigger in your function code.</span><span class="sxs-lookup"><span data-stu-id="8abae-129">This section shows you how to use your Service Hub trigger in your function code.</span></span> 

<span data-ttu-id="8abae-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span><span class="sxs-lookup"><span data-stu-id="8abae-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="8abae-131">`string` - useful for string messages</span><span class="sxs-lookup"><span data-stu-id="8abae-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="8abae-132">`byte[]` - useful for binary data</span><span class="sxs-lookup"><span data-stu-id="8abae-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="8abae-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span><span class="sxs-lookup"><span data-stu-id="8abae-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="8abae-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span><span class="sxs-lookup"><span data-stu-id="8abae-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="8abae-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="8abae-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="8abae-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span><span class="sxs-lookup"><span data-stu-id="8abae-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="8abae-137">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="8abae-137">Trigger sample</span></span>
<span data-ttu-id="8abae-138">Suppose you have the following function.json:</span><span class="sxs-lookup"><span data-stu-id="8abae-138">Suppose you have the following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="8abae-139">See the language-specific sample that processes a Service Bus queue message.</span><span class="sxs-lookup"><span data-stu-id="8abae-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="8abae-140">C#</span><span class="sxs-lookup"><span data-stu-id="8abae-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="8abae-141">F#</span><span class="sxs-lookup"><span data-stu-id="8abae-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="8abae-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="8abae-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="8abae-143">Trigger sample in C#</span><span class="sxs-lookup"><span data-stu-id="8abae-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="8abae-144">Trigger sample in F#</span><span class="sxs-lookup"><span data-stu-id="8abae-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="8abae-145">Trigger sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="8abae-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="8abae-146">Service Bus output binding</span><span class="sxs-lookup"><span data-stu-id="8abae-146">Service Bus output binding</span></span>
<span data-ttu-id="8abae-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="8abae-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="8abae-148">*queue* output:</span><span class="sxs-lookup"><span data-stu-id="8abae-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="8abae-149">*topic* output:</span><span class="sxs-lookup"><span data-stu-id="8abae-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>"
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="8abae-150">Note the following:</span><span class="sxs-lookup"><span data-stu-id="8abae-150">Note the following:</span></span>

* <span data-ttu-id="8abae-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Hub namespace, then specify the name of the app setting in the `connection` property in your output binding.</span><span class="sxs-lookup"><span data-stu-id="8abae-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Hub namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="8abae-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="8abae-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="8abae-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span><span class="sxs-lookup"><span data-stu-id="8abae-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="8abae-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="8abae-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="8abae-155">For `accessRights`, available values are `manage` and `listen`.</span><span class="sxs-lookup"><span data-stu-id="8abae-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="8abae-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span><span class="sxs-lookup"><span data-stu-id="8abae-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="8abae-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span><span class="sxs-lookup"><span data-stu-id="8abae-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="8abae-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span><span class="sxs-lookup"><span data-stu-id="8abae-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="8abae-159">Output usage</span><span class="sxs-lookup"><span data-stu-id="8abae-159">Output usage</span></span>
<span data-ttu-id="8abae-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span><span class="sxs-lookup"><span data-stu-id="8abae-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="8abae-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="8abae-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="8abae-162">Functions deserializes the object into a JSON message.</span><span class="sxs-lookup"><span data-stu-id="8abae-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="8abae-163">If the output value is null when the function exits, Functions creates the message with a null object.</span><span class="sxs-lookup"><span data-stu-id="8abae-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="8abae-164">`string` - Parameter definition looks like `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="8abae-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="8abae-165">If the parameter value is non-null when the function exits, Functions creates a message.</span><span class="sxs-lookup"><span data-stu-id="8abae-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="8abae-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="8abae-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="8abae-167">If the parameter value is non-null when the function exits, Functions creates a message.</span><span class="sxs-lookup"><span data-stu-id="8abae-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="8abae-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="8abae-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="8abae-169">If the parameter value is non-null when the function exits, Functions creates a message.</span><span class="sxs-lookup"><span data-stu-id="8abae-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="8abae-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="8abae-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="8abae-171">A message is created when you call the `Add` method.</span><span class="sxs-lookup"><span data-stu-id="8abae-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="8abae-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="8abae-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="8abae-173">Output sample</span><span class="sxs-lookup"><span data-stu-id="8abae-173">Output sample</span></span>
<span data-ttu-id="8abae-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span><span class="sxs-lookup"><span data-stu-id="8abae-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="8abae-175">See the language-specific sample that sends a message to the service bus queue.</span><span class="sxs-lookup"><span data-stu-id="8abae-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="8abae-176">C#</span><span class="sxs-lookup"><span data-stu-id="8abae-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="8abae-177">F#</span><span class="sxs-lookup"><span data-stu-id="8abae-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="8abae-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="8abae-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="8abae-179">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="8abae-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="8abae-180">Or, to create multiple messages:</span><span class="sxs-lookup"><span data-stu-id="8abae-180">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="8abae-181">Output sample in F#</span><span class="sxs-lookup"><span data-stu-id="8abae-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="8abae-182">Output sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="8abae-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="8abae-183">Or, to create multiple messages:</span><span class="sxs-lookup"><span data-stu-id="8abae-183">Or, to create multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="8abae-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="8abae-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

