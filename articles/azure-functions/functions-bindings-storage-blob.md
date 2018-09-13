---
title: Azure Functions Storage blob bindings | Microsoft Docs
description: Understand how to use Azure Storage triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: chrande, glenga
ms.openlocfilehash: 7b4ae9281bca20949c37b2c797e4a1a677665929
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660966"
---
# <a name="azure-functions-storage-blob-bindings"></a><span data-ttu-id="d43c0-104">Azure Functions Storage blob bindings</span><span class="sxs-lookup"><span data-stu-id="d43c0-104">Azure Functions Storage blob bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d43c0-105">This article explains how to configure and code Azure Storage blob bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d43c0-105">This article explains how to configure and code Azure Storage blob bindings in Azure Functions.</span></span> <span data-ttu-id="d43c0-106">Azure Functions supports trigger, input, and output bindings for Azure Storage blobs.</span><span class="sxs-lookup"><span data-stu-id="d43c0-106">Azure Functions supports trigger, input, and output bindings for Azure Storage blobs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="d43c0-107">A [blob only storage account](../storage/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span><span class="sxs-lookup"><span data-stu-id="d43c0-107">A [blob only storage account](../storage/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="d43c0-108">Azure Functions requires a general-purpose storage account to use with blobs.</span><span class="sxs-lookup"><span data-stu-id="d43c0-108">Azure Functions requires a general-purpose storage account to use with blobs.</span></span> 
> 
> 

<a name="trigger"></a>

## <a name="storage-blob-trigger"></a><span data-ttu-id="d43c0-109">Storage blob trigger</span><span class="sxs-lookup"><span data-stu-id="d43c0-109">Storage blob trigger</span></span>
<span data-ttu-id="d43c0-110">The Azure Storage blob trigger lets you monitor a storage container for new and updated blobs and run your function code when changes are detected.</span><span class="sxs-lookup"><span data-stu-id="d43c0-110">The Azure Storage blob trigger lets you monitor a storage container for new and updated blobs and run your function code when changes are detected.</span></span> 

<span data-ttu-id="d43c0-111">The Storage blob trigger to a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="d43c0-111">The Storage blob trigger to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection":"<Name of app setting - see below>"
}
```

<span data-ttu-id="d43c0-112">Note the following:</span><span class="sxs-lookup"><span data-stu-id="d43c0-112">Note the following:</span></span>

* <span data-ttu-id="d43c0-113">For `path`, see [Name patterns](#pattern) to find out how to format blob name patterns.</span><span class="sxs-lookup"><span data-stu-id="d43c0-113">For `path`, see [Name patterns](#pattern) to find out how to format blob name patterns.</span></span>
* <span data-ttu-id="d43c0-114">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="d43c0-114">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="d43c0-115">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="d43c0-115">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span></span> <span data-ttu-id="d43c0-116">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d43c0-116">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="d43c0-117">When running on a Consumption plan, if a Function App has gone idle, there can be be up to a 10-minute day in processing new blobs.</span><span class="sxs-lookup"><span data-stu-id="d43c0-117">When running on a Consumption plan, if a Function App has gone idle, there can be be up to a 10-minute day in processing new blobs.</span></span> <span data-ttu-id="d43c0-118">Once the Function App is running, blobs are processed more quickly.</span><span class="sxs-lookup"><span data-stu-id="d43c0-118">Once the Function App is running, blobs are processed more quickly.</span></span> <span data-ttu-id="d43c0-119">To avoid this initial delay, either use a regular App Service Plan with Always On enabled or use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span><span class="sxs-lookup"><span data-stu-id="d43c0-119">To avoid this initial delay, either use a regular App Service Plan with Always On enabled or use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> 

<span data-ttu-id="d43c0-120">Also, see one of the following subheadings for more information:</span><span class="sxs-lookup"><span data-stu-id="d43c0-120">Also, see one of the following subheadings for more information:</span></span>

* [<span data-ttu-id="d43c0-121">Name patterns</span><span class="sxs-lookup"><span data-stu-id="d43c0-121">Name patterns</span></span>](#pattern)
* [<span data-ttu-id="d43c0-122">Blob receipts</span><span class="sxs-lookup"><span data-stu-id="d43c0-122">Blob receipts</span></span>](#receipts)
* [<span data-ttu-id="d43c0-123">Handling poison blobs</span><span class="sxs-lookup"><span data-stu-id="d43c0-123">Handling poison blobs</span></span>](#poison)

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="d43c0-124">Name patterns</span><span class="sxs-lookup"><span data-stu-id="d43c0-124">Name patterns</span></span>
<span data-ttu-id="d43c0-125">You can specify a blob name pattern in the `path` property.</span><span class="sxs-lookup"><span data-stu-id="d43c0-125">You can specify a blob name pattern in the `path` property.</span></span> <span data-ttu-id="d43c0-126">For example:</span><span class="sxs-lookup"><span data-stu-id="d43c0-126">For example:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="d43c0-127">This path would find a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code would be `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-127">This path would find a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code would be `Blob1`.</span></span>

<span data-ttu-id="d43c0-128">Another example:</span><span class="sxs-lookup"><span data-stu-id="d43c0-128">Another example:</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="d43c0-129">This path would also find a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code would be *original-Blob1* and *txt*.</span><span class="sxs-lookup"><span data-stu-id="d43c0-129">This path would also find a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code would be *original-Blob1* and *txt*.</span></span>

<span data-ttu-id="d43c0-130">You can restrict the file type of blobs by using a fixed value for the file extension.</span><span class="sxs-lookup"><span data-stu-id="d43c0-130">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="d43c0-131">For example:</span><span class="sxs-lookup"><span data-stu-id="d43c0-131">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="d43c0-132">In this case, only *.png* blobs in the *samples* container trigger the function.</span><span class="sxs-lookup"><span data-stu-id="d43c0-132">In this case, only *.png* blobs in the *samples* container trigger the function.</span></span>

<span data-ttu-id="d43c0-133">Curly braces are special characters in name patterns.</span><span class="sxs-lookup"><span data-stu-id="d43c0-133">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="d43c0-134">To specify blob names that have curly braces in the name, double the curly braces.</span><span class="sxs-lookup"><span data-stu-id="d43c0-134">To specify blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="d43c0-135">For example:</span><span class="sxs-lookup"><span data-stu-id="d43c0-135">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="d43c0-136">This path would find a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code would be *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="d43c0-136">This path would find a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span> 

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="d43c0-137">Blob receipts</span><span class="sxs-lookup"><span data-stu-id="d43c0-137">Blob receipts</span></span>
<span data-ttu-id="d43c0-138">The Azure Functions runtime makes sure that no blob trigger function gets called more than once for the same new or updated blob.</span><span class="sxs-lookup"><span data-stu-id="d43c0-138">The Azure Functions runtime makes sure that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="d43c0-139">It does so by maintaining *blob receipts* to determine if a given blob version has been processed.</span><span class="sxs-lookup"><span data-stu-id="d43c0-139">It does so by maintaining *blob receipts* to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="d43c0-140">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (specified by the `AzureWebJobsStorage` app setting).</span><span class="sxs-lookup"><span data-stu-id="d43c0-140">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (specified by the `AzureWebJobsStorage` app setting).</span></span> <span data-ttu-id="d43c0-141">A blob receipt has the following information:</span><span class="sxs-lookup"><span data-stu-id="d43c0-141">A blob receipt has the following information:</span></span>

* <span data-ttu-id="d43c0-142">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="d43c0-142">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyBlob")</span></span>
* <span data-ttu-id="d43c0-143">The container name</span><span class="sxs-lookup"><span data-stu-id="d43c0-143">The container name</span></span>
* <span data-ttu-id="d43c0-144">The blob type ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="d43c0-144">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="d43c0-145">The blob name</span><span class="sxs-lookup"><span data-stu-id="d43c0-145">The blob name</span></span>
* <span data-ttu-id="d43c0-146">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="d43c0-146">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="d43c0-147">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span><span class="sxs-lookup"><span data-stu-id="d43c0-147">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="d43c0-148">Handling poison blobs</span><span class="sxs-lookup"><span data-stu-id="d43c0-148">Handling poison blobs</span></span>
<span data-ttu-id="d43c0-149">When a blob trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given blob.</span><span class="sxs-lookup"><span data-stu-id="d43c0-149">When a blob trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given blob.</span></span> <span data-ttu-id="d43c0-150">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="d43c0-150">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="d43c0-151">The queue message for poison blobs is a JSON object that contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="d43c0-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="d43c0-152">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span><span class="sxs-lookup"><span data-stu-id="d43c0-152">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="d43c0-153">BlobType ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="d43c0-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="d43c0-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="d43c0-154">ContainerName</span></span>
* <span data-ttu-id="d43c0-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="d43c0-155">BlobName</span></span>
* <span data-ttu-id="d43c0-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="d43c0-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="d43c0-157">Blob polling for large containers</span><span class="sxs-lookup"><span data-stu-id="d43c0-157">Blob polling for large containers</span></span>
<span data-ttu-id="d43c0-158">If the blob container watched by the binding contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span><span class="sxs-lookup"><span data-stu-id="d43c0-158">If the blob container watched by the binding contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="d43c0-159">This process is not real time.</span><span class="sxs-lookup"><span data-stu-id="d43c0-159">This process is not real time.</span></span> <span data-ttu-id="d43c0-160">A function might not get triggered until several minutes or longer after the blob is created.</span><span class="sxs-lookup"><span data-stu-id="d43c0-160">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="d43c0-161">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis.</span><span class="sxs-lookup"><span data-stu-id="d43c0-161">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis.</span></span> <span data-ttu-id="d43c0-162">There is no guarantee that all events are captured.</span><span class="sxs-lookup"><span data-stu-id="d43c0-162">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="d43c0-163">Under some conditions, logs may be missed.</span><span class="sxs-lookup"><span data-stu-id="d43c0-163">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="d43c0-164">If the speed and reliability limitations of blob triggers for large containers are not acceptable for your application, the recommended method is to create a [queue message](../storage/storage-dotnet-how-to-use-queues.md) when you create the blob, and use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span><span class="sxs-lookup"><span data-stu-id="d43c0-164">If the speed and reliability limitations of blob triggers for large containers are not acceptable for your application, the recommended method is to create a [queue message](../storage/storage-dotnet-how-to-use-queues.md) when you create the blob, and use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d43c0-165">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="d43c0-165">Trigger usage</span></span>
<span data-ttu-id="d43c0-166">In C# functions, you bind to the input blob data by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-166">In C# functions, you bind to the input blob data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d43c0-167">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="d43c0-167">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="d43c0-168">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-168">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d43c0-169">The blob can be deserialized into any of the following types:</span><span class="sxs-lookup"><span data-stu-id="d43c0-169">The blob can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="d43c0-170">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized blob data.</span><span class="sxs-lookup"><span data-stu-id="d43c0-170">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized blob data.</span></span>
  <span data-ttu-id="d43c0-171">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span><span class="sxs-lookup"><span data-stu-id="d43c0-171">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="d43c0-172">String - useful for text blob data.</span><span class="sxs-lookup"><span data-stu-id="d43c0-172">String - useful for text blob data.</span></span>

<span data-ttu-id="d43c0-173">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the blob data using that type:</span><span class="sxs-lookup"><span data-stu-id="d43c0-173">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the blob data using that type:</span></span>

* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="d43c0-174">Other types deserialized by [ICloudBlobStreamBinder](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md#icbsb)</span><span class="sxs-lookup"><span data-stu-id="d43c0-174">Other types deserialized by [ICloudBlobStreamBinder](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md#icbsb)</span></span> 

## <a name="trigger-sample"></a><span data-ttu-id="d43c0-175">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="d43c0-175">Trigger sample</span></span>
<span data-ttu-id="d43c0-176">Suppose you have the following function.json, that defines a Storage blob trigger:</span><span class="sxs-lookup"><span data-stu-id="d43c0-176">Suppose you have the following function.json, that defines a Storage blob trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":""
        }
    ]
}
```

<span data-ttu-id="d43c0-177">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span><span class="sxs-lookup"><span data-stu-id="d43c0-177">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="d43c0-178">C#</span><span class="sxs-lookup"><span data-stu-id="d43c0-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d43c0-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="d43c0-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="d43c0-180">Trigger usage in C#</span><span class="sxs-lookup"><span data-stu-id="d43c0-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

``` 
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="d43c0-181">Trigger usage in Node.js</span><span class="sxs-lookup"><span data-stu-id="d43c0-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```

<a name="input"></a>

## <a name="storage-blob-input-binding"></a><span data-ttu-id="d43c0-182">Storage Blob input binding</span><span class="sxs-lookup"><span data-stu-id="d43c0-182">Storage Blob input binding</span></span>
<span data-ttu-id="d43c0-183">The Azure Storage blob input binding enables you to use a blob from a storage container in your function.</span><span class="sxs-lookup"><span data-stu-id="d43c0-183">The Azure Storage blob input binding enables you to use a blob from a storage container in your function.</span></span> 

<span data-ttu-id="d43c0-184">The Storage blob input to a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="d43c0-184">The Storage blob input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "blob",
  "direction": "in"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

<span data-ttu-id="d43c0-185">Note the following:</span><span class="sxs-lookup"><span data-stu-id="d43c0-185">Note the following:</span></span>

* <span data-ttu-id="d43c0-186">`path` must contain the container name and the blob name.</span><span class="sxs-lookup"><span data-stu-id="d43c0-186">`path` must contain the container name and the blob name.</span></span> <span data-ttu-id="d43c0-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a blob in the `samples-workitems` container with a name that matches the blob name specified in the trigger message.</span><span class="sxs-lookup"><span data-stu-id="d43c0-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a blob in the `samples-workitems` container with a name that matches the blob name specified in the trigger message.</span></span>   
* <span data-ttu-id="d43c0-188">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="d43c0-188">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="d43c0-189">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="d43c0-189">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="d43c0-190">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d43c0-190">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span></span> 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="d43c0-191">Input usage</span><span class="sxs-lookup"><span data-stu-id="d43c0-191">Input usage</span></span>
<span data-ttu-id="d43c0-192">In C# functions, you bind to the input blob data by using a named parameter in your function signature, like `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-192">In C# functions, you bind to the input blob data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d43c0-193">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span><span class="sxs-lookup"><span data-stu-id="d43c0-193">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="d43c0-194">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-194">In Node.js functions, you access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d43c0-195">The blob can be deserialized into any of the following types:</span><span class="sxs-lookup"><span data-stu-id="d43c0-195">The blob can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="d43c0-196">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized blob data.</span><span class="sxs-lookup"><span data-stu-id="d43c0-196">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized blob data.</span></span>
  <span data-ttu-id="d43c0-197">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span><span class="sxs-lookup"><span data-stu-id="d43c0-197">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="d43c0-198">String - useful for text blob data.</span><span class="sxs-lookup"><span data-stu-id="d43c0-198">String - useful for text blob data.</span></span>

<span data-ttu-id="d43c0-199">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the blob data using that type:</span><span class="sxs-lookup"><span data-stu-id="d43c0-199">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the blob data using that type:</span></span>

* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="d43c0-200">Input sample</span><span class="sxs-lookup"><span data-stu-id="d43c0-200">Input sample</span></span>
<span data-ttu-id="d43c0-201">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), a Storage blob input, and a Storage blob output:</span><span class="sxs-lookup"><span data-stu-id="d43c0-201">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), a Storage blob input, and a Storage blob output:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="d43c0-202">See the language-specific sample that copies the input blob to the output blob.</span><span class="sxs-lookup"><span data-stu-id="d43c0-202">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="d43c0-203">C#</span><span class="sxs-lookup"><span data-stu-id="d43c0-203">C#</span></span>](#incsharp)
* [<span data-ttu-id="d43c0-204">Node.js</span><span class="sxs-lookup"><span data-stu-id="d43c0-204">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="input-usage-in-c"></a><span data-ttu-id="d43c0-205">Input usage in C#</span><span class="sxs-lookup"><span data-stu-id="d43c0-205">Input usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

``` 
-->

<a name="innodejs"></a>

### <a name="input-usage-in-nodejs"></a><span data-ttu-id="d43c0-206">Input usage in Node.js</span><span class="sxs-lookup"><span data-stu-id="d43c0-206">Input usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

<a name="output"></a>

## <a name="storage-blob-output-binding"></a><span data-ttu-id="d43c0-207">Storage Blob output binding</span><span class="sxs-lookup"><span data-stu-id="d43c0-207">Storage Blob output binding</span></span>
<span data-ttu-id="d43c0-208">The Azure Storage blob output binding enables you to write blobs to a Storage container in your function.</span><span class="sxs-lookup"><span data-stu-id="d43c0-208">The Azure Storage blob output binding enables you to write blobs to a Storage container in your function.</span></span> 

<span data-ttu-id="d43c0-209">The Storage blob output for a function uses the following JSON objects in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="d43c0-209">The Storage blob output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "blob",
  "direction": "out",
  "path": "<Path of input blob - see below>",
  "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="d43c0-210">Note the following:</span><span class="sxs-lookup"><span data-stu-id="d43c0-210">Note the following:</span></span>

* <span data-ttu-id="d43c0-211">`path` must contain the container name and the blob name to write to.</span><span class="sxs-lookup"><span data-stu-id="d43c0-211">`path` must contain the container name and the blob name to write to.</span></span> <span data-ttu-id="d43c0-212">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a blob in the `samples-workitems` container with a name that matches the blob name specified in the trigger message.</span><span class="sxs-lookup"><span data-stu-id="d43c0-212">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a blob in the `samples-workitems` container with a name that matches the blob name specified in the trigger message.</span></span>   
* <span data-ttu-id="d43c0-213">`connection` must contain the name of an app setting that contains a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="d43c0-213">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="d43c0-214">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span><span class="sxs-lookup"><span data-stu-id="d43c0-214">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a storage account or selects an existing one.</span></span> <span data-ttu-id="d43c0-215">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d43c0-215">To manually create this app setting, see [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d43c0-216">Output usage</span><span class="sxs-lookup"><span data-stu-id="d43c0-216">Output usage</span></span>
<span data-ttu-id="d43c0-217">In C# functions, you bind to the output blob by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span><span class="sxs-lookup"><span data-stu-id="d43c0-217">In C# functions, you bind to the output blob by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="d43c0-218">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d43c0-218">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d43c0-219">You can write to the output blob using any of the following types:</span><span class="sxs-lookup"><span data-stu-id="d43c0-219">You can write to the output blob using any of the following types:</span></span>

* <span data-ttu-id="d43c0-220">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span><span class="sxs-lookup"><span data-stu-id="d43c0-220">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="d43c0-221">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span><span class="sxs-lookup"><span data-stu-id="d43c0-221">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="d43c0-222">If the output parameter is null when the function exits, the Functions runtime creates a blob as a null object.</span><span class="sxs-lookup"><span data-stu-id="d43c0-222">If the output parameter is null when the function exits, the Functions runtime creates a blob as a null object.</span></span>
* <span data-ttu-id="d43c0-223">String - (`out string paramName`) useful for text blob data.</span><span class="sxs-lookup"><span data-stu-id="d43c0-223">String - (`out string paramName`) useful for text blob data.</span></span> <span data-ttu-id="d43c0-224">the Functions runtime creates a blob only if the string parameter is non-null when the function exits.</span><span class="sxs-lookup"><span data-stu-id="d43c0-224">the Functions runtime creates a blob only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="d43c0-225">In C# functions you can also output to any of the following types:</span><span class="sxs-lookup"><span data-stu-id="d43c0-225">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="d43c0-226">Output sample</span><span class="sxs-lookup"><span data-stu-id="d43c0-226">Output sample</span></span>
<span data-ttu-id="d43c0-227">See [input sample](#inputsample).</span><span class="sxs-lookup"><span data-stu-id="d43c0-227">See [input sample](#inputsample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43c0-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="d43c0-228">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

