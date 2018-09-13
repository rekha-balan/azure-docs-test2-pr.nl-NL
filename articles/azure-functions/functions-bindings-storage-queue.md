---
title: Azure Functions Storage queue bindings | Microsoft Docs
description: Understand how to use Azure Storage triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/18/2017
ms.author: chrande, glenga
ms.openlocfilehash: bf9bd2a1b5acdf5a4a4f862bef693f8c60c63a33
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671771"
---
# <a name="azure-functions-storage-queue-bindings"></a><span data-ttu-id="98203-104">Azure Functions Storage queue bindings</span><span class="sxs-lookup"><span data-stu-id="98203-104">Azure Functions Storage queue bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="98203-105">This article explains how to configure and code Azure Storage queue bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="98203-105">This article explains how to configure and code Azure Storage queue bindings in Azure Functions.</span></span> <span data-ttu-id="98203-106">Azure Functions supports trigger and output bindings for Azure Storage queues.</span><span class="sxs-lookup"><span data-stu-id="98203-106">Azure Functions supports trigger and output bindings for Azure Storage queues.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="storage-queue-trigger"></a><span data-ttu-id="98203-107">Storage Queue trigger</span><span class="sxs-lookup"><span data-stu-id="98203-107">Storage Queue trigger</span></span>
<span data-ttu-id="98203-108">The Azure Storage queue trigger enables you to monitor a storage queue for new messages and react to them.</span><span class="sxs-lookup"><span data-stu-id="98203-108">The Azure Storage queue trigger enables you to monitor a storage queue for new messages and react to them.</span></span> 

<span data-ttu-id="98203-109">The Storage queue trigger to a function use the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="98203-109">The Storage queue trigger to a function use the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>",
    "type": "queueTrigger",
    "direction": "in"
}
```

<span data-ttu-id="98203-110">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="98203-110">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="98203-111">In the Azure portal, you can configure this app setting in the **Integrate** tab when you create a storage account or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="98203-111">In the Azure portal, you can configure this app setting in the **Integrate** tab when you create a storage account or select an existing one.</span></span> <span data-ttu-id="98203-112">To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).</span><span class="sxs-lookup"><span data-stu-id="98203-112">To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).</span></span>

<span data-ttu-id="98203-113">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine-tune storage queue triggers.</span><span class="sxs-lookup"><span data-stu-id="98203-113">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine-tune storage queue triggers.</span></span>  

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="98203-114">Handling poison queue messages</span><span class="sxs-lookup"><span data-stu-id="98203-114">Handling poison queue messages</span></span>
<span data-ttu-id="98203-115">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span><span class="sxs-lookup"><span data-stu-id="98203-115">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="98203-116">If all five attempts fail, Functions adds a message to a Storage queue named *&lt;originalqueuename>-poison*.</span><span class="sxs-lookup"><span data-stu-id="98203-116">If all five attempts fail, Functions adds a message to a Storage queue named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="98203-117">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span><span class="sxs-lookup"><span data-stu-id="98203-117">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="98203-118">To handle poison messages manually, you can get the number of times a message has been picked up for processing by checking `dequeueCount` (see [Queue trigger metadata](#meta)).</span><span class="sxs-lookup"><span data-stu-id="98203-118">To handle poison messages manually, you can get the number of times a message has been picked up for processing by checking `dequeueCount` (see [Queue trigger metadata](#meta)).</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="98203-119">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="98203-119">Trigger usage</span></span>
<span data-ttu-id="98203-120">In C# functions, you bind to the input message by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="98203-120">In C# functions, you bind to the input message by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="98203-121">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger binding](#trigger).</span><span class="sxs-lookup"><span data-stu-id="98203-121">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger binding](#trigger).</span></span> <span data-ttu-id="98203-122">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="98203-122">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="98203-123">The queue message can be deserialized to any of the following types:</span><span class="sxs-lookup"><span data-stu-id="98203-123">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="98203-124">[Object](https://msdn.microsoft.com/library/system.object.aspx) - used for JSON serialized messages.</span><span class="sxs-lookup"><span data-stu-id="98203-124">[Object](https://msdn.microsoft.com/library/system.object.aspx) - used for JSON serialized messages.</span></span> <span data-ttu-id="98203-125">When you declare a custom input type, the runtime tries to deserialize the JSON object.</span><span class="sxs-lookup"><span data-stu-id="98203-125">When you declare a custom input type, the runtime tries to deserialize the JSON object.</span></span> 
* <span data-ttu-id="98203-126">String</span><span class="sxs-lookup"><span data-stu-id="98203-126">String</span></span>
* <span data-ttu-id="98203-127">Byte array</span><span class="sxs-lookup"><span data-stu-id="98203-127">Byte array</span></span>
* <span data-ttu-id="98203-128">[CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) (C# only)</span><span class="sxs-lookup"><span data-stu-id="98203-128">[CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) (C# only)</span></span>

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="98203-129">Queue trigger metadata</span><span class="sxs-lookup"><span data-stu-id="98203-129">Queue trigger metadata</span></span>
<span data-ttu-id="98203-130">You can get queue metadata in your function by using these variable names:</span><span class="sxs-lookup"><span data-stu-id="98203-130">You can get queue metadata in your function by using these variable names:</span></span>

* <span data-ttu-id="98203-131">expirationTime</span><span class="sxs-lookup"><span data-stu-id="98203-131">expirationTime</span></span>
* <span data-ttu-id="98203-132">insertionTime</span><span class="sxs-lookup"><span data-stu-id="98203-132">insertionTime</span></span>
* <span data-ttu-id="98203-133">nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="98203-133">nextVisibleTime</span></span>
* <span data-ttu-id="98203-134">id</span><span class="sxs-lookup"><span data-stu-id="98203-134">id</span></span>
* <span data-ttu-id="98203-135">popReceipt</span><span class="sxs-lookup"><span data-stu-id="98203-135">popReceipt</span></span>
* <span data-ttu-id="98203-136">dequeueCount</span><span class="sxs-lookup"><span data-stu-id="98203-136">dequeueCount</span></span>
* <span data-ttu-id="98203-137">queueTrigger (another way to retrieve the queue message text as a string)</span><span class="sxs-lookup"><span data-stu-id="98203-137">queueTrigger (another way to retrieve the queue message text as a string)</span></span>

<span data-ttu-id="98203-138">See how to use the queue metadata in [Trigger sample](#triggersample)</span><span class="sxs-lookup"><span data-stu-id="98203-138">See how to use the queue metadata in [Trigger sample](#triggersample)</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="98203-139">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="98203-139">Trigger sample</span></span>
<span data-ttu-id="98203-140">Suppose you have the following function.json, that defines a Storage queue trigger:</span><span class="sxs-lookup"><span data-stu-id="98203-140">Suppose you have the following function.json, that defines a Storage queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"",
            "type": "queueTrigger",
            "direction": "in"
        }
    ]
}
```

<span data-ttu-id="98203-141">See the language-specific sample that retrieves and logs queue metadata.</span><span class="sxs-lookup"><span data-stu-id="98203-141">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="98203-142">C#</span><span class="sxs-lookup"><span data-stu-id="98203-142">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="98203-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="98203-143">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="98203-144">Trigger sample in C#</span><span class="sxs-lookup"><span data-stu-id="98203-144">Trigger sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="98203-145">Trigger sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="98203-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-queue-output-binding"></a><span data-ttu-id="98203-146">Storage Queue output binding</span><span class="sxs-lookup"><span data-stu-id="98203-146">Storage Queue output binding</span></span>
<span data-ttu-id="98203-147">The Azure Storage queue output binding enables you to write messages to a Storage queue in your function.</span><span class="sxs-lookup"><span data-stu-id="98203-147">The Azure Storage queue output binding enables you to write messages to a Storage queue in your function.</span></span> 

<span data-ttu-id="98203-148">The Storage queue output for a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="98203-148">The Storage queue output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
    "queueName": "<Name of queue to write to>",
    "connection":"<Name of app setting - see below>",
  "type": "queue",
  "direction": "out"
}
```

<span data-ttu-id="98203-149">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="98203-149">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="98203-150">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="98203-150">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span></span> <span data-ttu-id="98203-151">To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).</span><span class="sxs-lookup"><span data-stu-id="98203-151">To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="98203-152">Output usage</span><span class="sxs-lookup"><span data-stu-id="98203-152">Output usage</span></span>
<span data-ttu-id="98203-153">In C# functions, you write a queue message by using the named `out` parameter in your function signature, like `out <T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="98203-153">In C# functions, you write a queue message by using the named `out` parameter in your function signature, like `out <T> <name>`.</span></span> <span data-ttu-id="98203-154">In this case, `T` is the data type that you want to serialize the message into, and `paramName` is the name you specified in the [output binding](#output).</span><span class="sxs-lookup"><span data-stu-id="98203-154">In this case, `T` is the data type that you want to serialize the message into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="98203-155">In Node.js functions, you access the output using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="98203-155">In Node.js functions, you access the output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="98203-156">You can output a queue message using any of the data types in your code:</span><span class="sxs-lookup"><span data-stu-id="98203-156">You can output a queue message using any of the data types in your code:</span></span>

* <span data-ttu-id="98203-157">Any [Object](https://msdn.microsoft.com/library/system.object.aspx): `out MyCustomType paramName`</span><span class="sxs-lookup"><span data-stu-id="98203-157">Any [Object](https://msdn.microsoft.com/library/system.object.aspx): `out MyCustomType paramName`</span></span>  
<span data-ttu-id="98203-158">Used for JSON serialization.</span><span class="sxs-lookup"><span data-stu-id="98203-158">Used for JSON serialization.</span></span>  <span data-ttu-id="98203-159">When you declare a custom output type, the runtime tries to serialize the object into JSON.</span><span class="sxs-lookup"><span data-stu-id="98203-159">When you declare a custom output type, the runtime tries to serialize the object into JSON.</span></span> <span data-ttu-id="98203-160">If the output parameter is null when the function exits, the runtime creates a queue message as a null object.</span><span class="sxs-lookup"><span data-stu-id="98203-160">If the output parameter is null when the function exits, the runtime creates a queue message as a null object.</span></span>
* <span data-ttu-id="98203-161">String: `out string paramName`</span><span class="sxs-lookup"><span data-stu-id="98203-161">String: `out string paramName`</span></span>  
<span data-ttu-id="98203-162">Used for test messages.</span><span class="sxs-lookup"><span data-stu-id="98203-162">Used for test messages.</span></span> <span data-ttu-id="98203-163">The runtime creates message only when the string parameter is non-null when the function exits.</span><span class="sxs-lookup"><span data-stu-id="98203-163">The runtime creates message only when the string parameter is non-null when the function exits.</span></span>
* <span data-ttu-id="98203-164">Byte array: `out byte[]`</span><span class="sxs-lookup"><span data-stu-id="98203-164">Byte array: `out byte[]`</span></span> 

<span data-ttu-id="98203-165">These additional output types are supported a C# function:</span><span class="sxs-lookup"><span data-stu-id="98203-165">These additional output types are supported a C# function:</span></span>

* <span data-ttu-id="98203-166">[CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx): `out CloudQueueMessage`</span><span class="sxs-lookup"><span data-stu-id="98203-166">[CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx): `out CloudQueueMessage`</span></span> 
* <span data-ttu-id="98203-167">`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span><span class="sxs-lookup"><span data-stu-id="98203-167">`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="98203-168">Output sample</span><span class="sxs-lookup"><span data-stu-id="98203-168">Output sample</span></span>
<span data-ttu-id="98203-169">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), a Storage blob input, and a Storage blob output:</span><span class="sxs-lookup"><span data-stu-id="98203-169">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), a Storage blob input, and a Storage blob output:</span></span>

<span data-ttu-id="98203-170">Example *function.json* for a storage queue output binding that uses a manual trigger and writes the input to a queue message:</span><span class="sxs-lookup"><span data-stu-id="98203-170">Example *function.json* for a storage queue output binding that uses a manual trigger and writes the input to a queue message:</span></span>

```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "queue",
      "name": "myQueueItem",
      "queueName": "myqueue",
      "connection": "my_storage_connection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="98203-171">See the language-specific sample that writes an output queue message for each input queue message.</span><span class="sxs-lookup"><span data-stu-id="98203-171">See the language-specific sample that writes an output queue message for each input queue message.</span></span>

* [<span data-ttu-id="98203-172">C#</span><span class="sxs-lookup"><span data-stu-id="98203-172">C#</span></span>](#outcsharp)
* [<span data-ttu-id="98203-173">Node.js</span><span class="sxs-lookup"><span data-stu-id="98203-173">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="98203-174">Output sample in C#</span><span class="sxs-lookup"><span data-stu-id="98203-174">Output sample in C#</span></span> #

```cs
public static void Run(string input, out string myQueueItem, TraceWriter log)
{
    myQueueItem = "New message: " + input;
}
```

<span data-ttu-id="98203-175">Or, to send multiple messages,</span><span class="sxs-lookup"><span data-stu-id="98203-175">Or, to send multiple messages,</span></span>

```cs
public static void Run(string input, ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Message 1: " + input);
    myQueueItem.Add("Message 2: " + "Some other message.");
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="98203-176">Output sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="98203-176">Output sample in Node.js</span></span>

```javascript
module.exports = function(context) {
    // Define a new message for the myQueueItem output binding.
    context.bindings.myQueueItem = "new message";
    context.done();
};
```

<span data-ttu-id="98203-177">Or, to send multiple messages,</span><span class="sxs-lookup"><span data-stu-id="98203-177">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="98203-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="98203-178">Next steps</span></span>

<span data-ttu-id="98203-179">For an example of a function that uses aStorage queue triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="98203-179">For an example of a function that uses aStorage queue triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

