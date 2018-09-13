---
title: Azure Functions Event Hub bindings | Microsoft Docs
description: Understand how to use Azure Event Hub bindings in Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/02/2016
ms.author: wesmc
ms.openlocfilehash: 0bfbfd3828aacdee0b6630ced034f2c1e0451abd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563770"
---
# <a name="azure-functions-event-hub-bindings"></a><span data-ttu-id="46585-104">Azure Functions Event Hub bindings</span><span class="sxs-lookup"><span data-stu-id="46585-104">Azure Functions Event Hub bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="46585-105">This article explains how to configure and code [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="46585-105">This article explains how to configure and code [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="46585-106">Azure Functions supports trigger and output bindings for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="46585-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="46585-107">If you are new to Azure Event Hubs, see the [Azure Event Hub overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="46585-107">If you are new to Azure Event Hubs, see the [Azure Event Hub overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="46585-108">Event Hub trigger</span><span class="sxs-lookup"><span data-stu-id="46585-108">Event Hub trigger</span></span>
<span data-ttu-id="46585-109">Use the Event Hub trigger to respond to an event sent to an event hub event stream.</span><span class="sxs-lookup"><span data-stu-id="46585-109">Use the Event Hub trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="46585-110">You must have read access to the event hub to set up the trigger.</span><span class="sxs-lookup"><span data-stu-id="46585-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="46585-111">The Event Hub trigger to a function uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="46585-111">The Event Hub trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the Event Hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="46585-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-what-is-event-hubs.md#event-consumers) used to subscribe to events in the hub.</span><span class="sxs-lookup"><span data-stu-id="46585-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-what-is-event-hubs.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="46585-113">If omitted, the `$Default` consumer group is used.</span><span class="sxs-lookup"><span data-stu-id="46585-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="46585-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span><span class="sxs-lookup"><span data-stu-id="46585-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="46585-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span><span class="sxs-lookup"><span data-stu-id="46585-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="46585-116">This connection string must have at least read permissions to activate the trigger.</span><span class="sxs-lookup"><span data-stu-id="46585-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="46585-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hub triggers.</span><span class="sxs-lookup"><span data-stu-id="46585-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hub triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="46585-118">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="46585-118">Trigger usage</span></span>
<span data-ttu-id="46585-119">When an Event Hub trigger function is triggered, the message that triggers it is passed into the function as a string.</span><span class="sxs-lookup"><span data-stu-id="46585-119">When an Event Hub trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="46585-120">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="46585-120">Trigger sample</span></span>
<span data-ttu-id="46585-121">Suppose you have the following Event Hub trigger in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="46585-121">Suppose you have the following Event Hub trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="46585-122">See the language-specific sample that logs the message body of the event hub trigger.</span><span class="sxs-lookup"><span data-stu-id="46585-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="46585-123">C#</span><span class="sxs-lookup"><span data-stu-id="46585-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="46585-124">F#</span><span class="sxs-lookup"><span data-stu-id="46585-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="46585-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="46585-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="46585-126">Trigger sample in C#</span><span class="sxs-lookup"><span data-stu-id="46585-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="46585-127">Trigger sample in F#</span><span class="sxs-lookup"><span data-stu-id="46585-127">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="46585-128">Trigger sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="46585-128">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hub-output-binding"></a><span data-ttu-id="46585-129">Event Hub output binding</span><span class="sxs-lookup"><span data-stu-id="46585-129">Event Hub output binding</span></span>
<span data-ttu-id="46585-130">Use the Event Hub output binding to write events to an event hub event stream.</span><span class="sxs-lookup"><span data-stu-id="46585-130">Use the Event Hub output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="46585-131">You must have send permission to an event hub to write events to it.</span><span class="sxs-lookup"><span data-stu-id="46585-131">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="46585-132">The output binding uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="46585-132">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="46585-133">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span><span class="sxs-lookup"><span data-stu-id="46585-133">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="46585-134">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span><span class="sxs-lookup"><span data-stu-id="46585-134">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="46585-135">This connection string must have send permissions to send the message to the event stream.</span><span class="sxs-lookup"><span data-stu-id="46585-135">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="46585-136">Output usage</span><span class="sxs-lookup"><span data-stu-id="46585-136">Output usage</span></span>
<span data-ttu-id="46585-137">This section shows you how to use your Event Hub output binding in your function code.</span><span class="sxs-lookup"><span data-stu-id="46585-137">This section shows you how to use your Event Hub output binding in your function code.</span></span>

<span data-ttu-id="46585-138">You can output messages to the configured event hub with the following parameter types:</span><span class="sxs-lookup"><span data-stu-id="46585-138">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="46585-139">`ICollector<string>` (to output multiple messages)</span><span class="sxs-lookup"><span data-stu-id="46585-139">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="46585-140">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="46585-140">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="46585-141">Output sample</span><span class="sxs-lookup"><span data-stu-id="46585-141">Output sample</span></span>
<span data-ttu-id="46585-142">Suppose you have the following Event Hub output binding in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="46585-142">Suppose you have the following Event Hub output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="46585-143">See the language-specific sample that writes an event to the even stream.</span><span class="sxs-lookup"><span data-stu-id="46585-143">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="46585-144">C#</span><span class="sxs-lookup"><span data-stu-id="46585-144">C#</span></span>](#outcsharp)
* [<span data-ttu-id="46585-145">F#</span><span class="sxs-lookup"><span data-stu-id="46585-145">F#</span></span>](#outfsharp)
* [<span data-ttu-id="46585-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="46585-146">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="46585-147">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="46585-147">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="46585-148">Or, to create multiple messages:</span><span class="sxs-lookup"><span data-stu-id="46585-148">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="46585-149">Output sample in F#</span><span class="sxs-lookup"><span data-stu-id="46585-149">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="46585-150">Output sample for Node.js</span><span class="sxs-lookup"><span data-stu-id="46585-150">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="46585-151">Or, to send multiple messages,</span><span class="sxs-lookup"><span data-stu-id="46585-151">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="46585-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="46585-152">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
