---
title: Work with triggers and bindings in Azure Functions | Microsoft Docs
description: Learn how to use triggers and bindings in Azure Functions to connect your code execution to online events and cloud-based services.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/14/2017
ms.author: donnam
ms.openlocfilehash: ed0ade96cc1cf6afc82787133d3fbcf874c43e0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671591"
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="75ad4-104">Azure Functions triggers and bindings concepts</span><span class="sxs-lookup"><span data-stu-id="75ad4-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="75ad4-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span><span class="sxs-lookup"><span data-stu-id="75ad4-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="75ad4-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span><span class="sxs-lookup"><span data-stu-id="75ad4-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="75ad4-107">Features that are common to all bindings are described here.</span><span class="sxs-lookup"><span data-stu-id="75ad4-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="75ad4-108">Overview</span><span class="sxs-lookup"><span data-stu-id="75ad4-108">Overview</span></span>

<span data-ttu-id="75ad4-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span><span class="sxs-lookup"><span data-stu-id="75ad4-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="75ad4-110">A *trigger* defines how a function is invoked.</span><span class="sxs-lookup"><span data-stu-id="75ad4-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="75ad4-111">A function must have exactly one trigger.</span><span class="sxs-lookup"><span data-stu-id="75ad4-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="75ad4-112">Triggers have associated data, which is usually the payload that triggered the function.</span><span class="sxs-lookup"><span data-stu-id="75ad4-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="75ad4-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="75ad4-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span><span class="sxs-lookup"><span data-stu-id="75ad4-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="75ad4-115">Bindings are optional and a function can have multiple input and output bindings.</span><span class="sxs-lookup"><span data-stu-id="75ad4-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="75ad4-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span><span class="sxs-lookup"><span data-stu-id="75ad4-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="75ad4-117">Data coming from services simply become input values for your function code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="75ad4-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span><span class="sxs-lookup"><span data-stu-id="75ad4-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="75ad4-119">Or, if you need to output multiple values, use a helper object.</span><span class="sxs-lookup"><span data-stu-id="75ad4-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="75ad4-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span><span class="sxs-lookup"><span data-stu-id="75ad4-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="75ad4-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span><span class="sxs-lookup"><span data-stu-id="75ad4-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="75ad4-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span><span class="sxs-lookup"><span data-stu-id="75ad4-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="75ad4-123">You can edit this file by changing to the **Advanced editor**.</span><span class="sxs-lookup"><span data-stu-id="75ad4-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="75ad4-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="75ad4-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="75ad4-125">Example: queue trigger and table output binding</span><span class="sxs-lookup"><span data-stu-id="75ad4-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="75ad4-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="75ad4-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="75ad4-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span><span class="sxs-lookup"><span data-stu-id="75ad4-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="75ad4-128">A queue trigger requires the following information in the **Integrate** tab:</span><span class="sxs-lookup"><span data-stu-id="75ad4-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="75ad4-129">The name of the app setting that contains the storage account connection string for the queue</span><span class="sxs-lookup"><span data-stu-id="75ad4-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="75ad4-130">The queue name</span><span class="sxs-lookup"><span data-stu-id="75ad4-130">The queue name</span></span>
* <span data-ttu-id="75ad4-131">The identifier in your code to read the contents of the queue message, such as `order`.</span><span class="sxs-lookup"><span data-stu-id="75ad4-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="75ad4-132">To write to Azure Table Storage, use an output binding with the following details:</span><span class="sxs-lookup"><span data-stu-id="75ad4-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="75ad4-133">The name of the app setting that contains the storage account connection string for the table</span><span class="sxs-lookup"><span data-stu-id="75ad4-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="75ad4-134">The table name</span><span class="sxs-lookup"><span data-stu-id="75ad4-134">The table name</span></span>
* <span data-ttu-id="75ad4-135">The identifier in your code to create output items, or the return value from the function.</span><span class="sxs-lookup"><span data-stu-id="75ad4-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="75ad4-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span><span class="sxs-lookup"><span data-stu-id="75ad4-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="75ad4-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="75ad4-138">Here is the *function.json* that corresponds to the preceding code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="75ad4-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span><span class="sxs-lookup"><span data-stu-id="75ad4-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="75ad4-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span><span class="sxs-lookup"><span data-stu-id="75ad4-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="75ad4-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="75ad4-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="75ad4-142">Binding direction</span><span class="sxs-lookup"><span data-stu-id="75ad4-142">Binding direction</span></span>

<span data-ttu-id="75ad4-143">All triggers and bindings have a `direction` property:</span><span class="sxs-lookup"><span data-stu-id="75ad4-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="75ad4-144">For triggers, the direction is always `in`</span><span class="sxs-lookup"><span data-stu-id="75ad4-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="75ad4-145">Input and output bindings use `in` and `out`</span><span class="sxs-lookup"><span data-stu-id="75ad4-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="75ad4-146">Some bindings support a special direction `inout`.</span><span class="sxs-lookup"><span data-stu-id="75ad4-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="75ad4-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span><span class="sxs-lookup"><span data-stu-id="75ad4-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="75ad4-148">Using the function return type to return a single output</span><span class="sxs-lookup"><span data-stu-id="75ad4-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="75ad4-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span><span class="sxs-lookup"><span data-stu-id="75ad4-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="75ad4-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span><span class="sxs-lookup"><span data-stu-id="75ad4-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="75ad4-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span><span class="sxs-lookup"><span data-stu-id="75ad4-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in the second parameter to context.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="resolving-app-settings"></a><span data-ttu-id="75ad4-152">Resolving app settings</span><span class="sxs-lookup"><span data-stu-id="75ad4-152">Resolving app settings</span></span>
<span data-ttu-id="75ad4-153">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span><span class="sxs-lookup"><span data-stu-id="75ad4-153">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="75ad4-154">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span><span class="sxs-lookup"><span data-stu-id="75ad4-154">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="75ad4-155">App settings are also useful whenever you want to change configuration based on the environment.</span><span class="sxs-lookup"><span data-stu-id="75ad4-155">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="75ad4-156">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span><span class="sxs-lookup"><span data-stu-id="75ad4-156">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="75ad4-157">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="75ad4-157">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="75ad4-158">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span><span class="sxs-lookup"><span data-stu-id="75ad4-158">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="75ad4-159">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span><span class="sxs-lookup"><span data-stu-id="75ad4-159">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="75ad4-160">Trigger metadata properties</span><span class="sxs-lookup"><span data-stu-id="75ad4-160">Trigger metadata properties</span></span>

<span data-ttu-id="75ad4-161">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span><span class="sxs-lookup"><span data-stu-id="75ad4-161">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="75ad4-162">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75ad4-162">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="75ad4-163">For example, a queue trigger supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="75ad4-163">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="75ad4-164">QueueTrigger - triggering message content if a valid string</span><span class="sxs-lookup"><span data-stu-id="75ad4-164">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="75ad4-165">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="75ad4-165">DequeueCount</span></span>
* <span data-ttu-id="75ad4-166">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="75ad4-166">ExpirationTime</span></span>
* <span data-ttu-id="75ad4-167">Id</span><span class="sxs-lookup"><span data-stu-id="75ad4-167">Id</span></span>
* <span data-ttu-id="75ad4-168">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="75ad4-168">InsertionTime</span></span>
* <span data-ttu-id="75ad4-169">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="75ad4-169">NextVisibleTime</span></span>
* <span data-ttu-id="75ad4-170">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="75ad4-170">PopReceipt</span></span>

<span data-ttu-id="75ad4-171">Details of metadata properties for each trigger are described in the corresponding reference topic.</span><span class="sxs-lookup"><span data-stu-id="75ad4-171">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="75ad4-172">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span><span class="sxs-lookup"><span data-stu-id="75ad4-172">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="75ad4-173">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="75ad4-173">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="75ad4-174">The queue message would contain the blob filename to trigger on.</span><span class="sxs-lookup"><span data-stu-id="75ad4-174">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="75ad4-175">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-175">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="75ad4-176">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span><span class="sxs-lookup"><span data-stu-id="75ad4-176">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="75ad4-177">Binding expressions and patterns</span><span class="sxs-lookup"><span data-stu-id="75ad4-177">Binding expressions and patterns</span></span>

<span data-ttu-id="75ad4-178">One of the most powerful features of triggers and bindings is *binding expressions*.</span><span class="sxs-lookup"><span data-stu-id="75ad4-178">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="75ad4-179">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-179">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="75ad4-180">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="75ad4-180">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="75ad4-181">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span><span class="sxs-lookup"><span data-stu-id="75ad4-181">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="75ad4-182">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="75ad4-182">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="75ad4-183">Here is the *function.json* definition:</span><span class="sxs-lookup"><span data-stu-id="75ad4-183">Here is the *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="75ad4-184">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span><span class="sxs-lookup"><span data-stu-id="75ad4-184">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="75ad4-185">This parameter can also be used in function code.</span><span class="sxs-lookup"><span data-stu-id="75ad4-185">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="75ad4-186">Random GUIDs</span><span class="sxs-lookup"><span data-stu-id="75ad4-186">Random GUIDs</span></span>
<span data-ttu-id="75ad4-187">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span><span class="sxs-lookup"><span data-stu-id="75ad4-187">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="75ad4-188">The following example uses this to generate a unique blob name:</span><span class="sxs-lookup"><span data-stu-id="75ad4-188">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="75ad4-189">Bind to custom input properties in a binding expression</span><span class="sxs-lookup"><span data-stu-id="75ad4-189">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="75ad4-190">Binding expressions can also reference properties that are defined in the trigger payload itself.</span><span class="sxs-lookup"><span data-stu-id="75ad4-190">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="75ad4-191">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span><span class="sxs-lookup"><span data-stu-id="75ad4-191">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="75ad4-192">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span><span class="sxs-lookup"><span data-stu-id="75ad4-192">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="75ad4-193">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span><span class="sxs-lookup"><span data-stu-id="75ad4-193">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="75ad4-194">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span><span class="sxs-lookup"><span data-stu-id="75ad4-194">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="next-steps"></a><span data-ttu-id="75ad4-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="75ad4-195">Next steps</span></span>
<span data-ttu-id="75ad4-196">For more information on a specific binding, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="75ad4-196">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="75ad4-197">HTTP and webhooks</span><span class="sxs-lookup"><span data-stu-id="75ad4-197">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="75ad4-198">Timer</span><span class="sxs-lookup"><span data-stu-id="75ad4-198">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="75ad4-199">Queue storage</span><span class="sxs-lookup"><span data-stu-id="75ad4-199">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="75ad4-200">Blob storage</span><span class="sxs-lookup"><span data-stu-id="75ad4-200">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="75ad4-201">Table storage</span><span class="sxs-lookup"><span data-stu-id="75ad4-201">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="75ad4-202">Event Hub</span><span class="sxs-lookup"><span data-stu-id="75ad4-202">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="75ad4-203">Service Bus</span><span class="sxs-lookup"><span data-stu-id="75ad4-203">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="75ad4-204">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="75ad4-204">DocumentDB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="75ad4-205">SendGrid</span><span class="sxs-lookup"><span data-stu-id="75ad4-205">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="75ad4-206">Twilio</span><span class="sxs-lookup"><span data-stu-id="75ad4-206">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="75ad4-207">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="75ad4-207">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="75ad4-208">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="75ad4-208">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="75ad4-209">External file</span><span class="sxs-lookup"><span data-stu-id="75ad4-209">External file</span></span>](functions-bindings-external-file.md)
