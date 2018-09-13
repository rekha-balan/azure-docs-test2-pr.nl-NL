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
# <a name="azure-functions-storage-queue-bindings"></a>Azure Functions Storage queue bindings
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

This article explains how to configure and code Azure Storage queue bindings in Azure Functions. Azure Functions supports trigger and output bindings for Azure Storage queues.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="storage-queue-trigger"></a>Storage Queue trigger
The Azure Storage queue trigger enables you to monitor a storage queue for new messages and react to them. 

The Storage queue trigger to a function use the following JSON objects in the `bindings` array of function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>",
    "type": "queueTrigger",
    "direction": "in"
}
```

`connection` must contain the name of an app setting that contains a storage connection string. In the Azure portal, you can configure this app setting in the **Integrate** tab when you create a storage account or select an existing one. To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).

[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine-tune storage queue triggers.  

### <a name="handling-poison-queue-messages"></a>Handling poison queue messages
When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try. If all five attempts fail, Functions adds a message to a Storage queue named *&lt;originalqueuename>-poison*. You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed. 

To handle poison messages manually, you can get the number of times a message has been picked up for processing by checking `dequeueCount` (see [Queue trigger metadata](#meta)).

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Trigger usage
In C# functions, you bind to the input message by using a named parameter in your function signature, like `<T> <name>`.
Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger binding](#trigger). In Node.js functions, you access the input blob data using `context.bindings.<name>`.

The queue message can be deserialized to any of the following types:

* [Object](https://msdn.microsoft.com/library/system.object.aspx) - used for JSON serialized messages. When you declare a custom input type, the runtime tries to deserialize the JSON object. 
* String
* Byte array
* [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) (C# only)

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Queue trigger metadata
You can get queue metadata in your function by using these variable names:

* expirationTime
* insertionTime
* nextVisibleTime
* id
* popReceipt
* dequeueCount
* queueTrigger (another way to retrieve the queue message text as a string)

See how to use the queue metadata in [Trigger sample](#triggersample)

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Trigger sample
Suppose you have the following function.json, that defines a Storage queue trigger:

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

See the language-specific sample that retrieves and logs queue metadata.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Trigger sample in C# #
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

### <a name="trigger-sample-in-nodejs"></a>Trigger sample in Node.js

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

## <a name="storage-queue-output-binding"></a>Storage Queue output binding
The Azure Storage queue output binding enables you to write messages to a Storage queue in your function. 

The Storage queue output for a function uses the following JSON objects in the `bindings` array of function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
    "queueName": "<Name of queue to write to>",
    "connection":"<Name of app setting - see below>",
  "type": "queue",
  "direction": "out"
}
```

`connection` must contain the name of an app setting that contains a storage connection string. In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one. To manually create this app setting, see [Manage App Service settings](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings).

<a name="outputusage"></a>

## <a name="output-usage"></a>Output usage
In C# functions, you write a queue message by using the named `out` parameter in your function signature, like `out <T> <name>`. In this case, `T` is the data type that you want to serialize the message into, and `paramName` is the name you specified in the [output binding](#output). In Node.js functions, you access the output using `context.bindings.<name>`.

You can output a queue message using any of the data types in your code:

* Any [Object](https://msdn.microsoft.com/library/system.object.aspx): `out MyCustomType paramName`  
Used for JSON serialization.  When you declare a custom output type, the runtime tries to serialize the object into JSON. If the output parameter is null when the function exits, the runtime creates a queue message as a null object.
* String: `out string paramName`  
Used for test messages. The runtime creates message only when the string parameter is non-null when the function exits.
* Byte array: `out byte[]` 

These additional output types are supported a C# function:

* [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx): `out CloudQueueMessage` 
* `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.

<a name="outputsample"></a>

## <a name="output-sample"></a>Output sample
Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), a Storage blob input, and a Storage blob output:

Example *function.json* for a storage queue output binding that uses a manual trigger and writes the input to a queue message:

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

See the language-specific sample that writes an output queue message for each input queue message.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Output sample in C# #

```cs
public static void Run(string input, out string myQueueItem, TraceWriter log)
{
    myQueueItem = "New message: " + input;
}
```

Or, to send multiple messages,

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

### <a name="output-sample-in-nodejs"></a>Output sample in Node.js

```javascript
module.exports = function(context) {
    // Define a new message for the myQueueItem output binding.
    context.bindings.myQueueItem = "new message";
    context.done();
};
```

Or, to send multiple messages,

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Next steps

For an example of a function that uses aStorage queue triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

