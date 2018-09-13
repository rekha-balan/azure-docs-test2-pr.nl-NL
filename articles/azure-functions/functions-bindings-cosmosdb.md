---
title: Azure Cosmos DB bindings for Functions 1.x
description: Understand how to use Azure Cosmos DB triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.service: azure-functions; cosmos-db
ms.devlang: multiple
ms.topic: reference
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: 50a8e491998b37a7ffebd5551cf755e8a9ca738a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857990"
---
# <a name="azure-cosmos-db-bindings-for-azure-functions-1x"></a><span data-ttu-id="b64ff-104">Azure Cosmos DB bindings for Azure Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="b64ff-104">Azure Cosmos DB bindings for Azure Functions 1.x</span></span>

> [!div class="op_single_selector" title1="Select the version of the Azure Functions runtime you are using: "]
> * [Version 1 - GA](functions-bindings-cosmosdb.md)
> * [Version 2 - Preview](functions-bindings-cosmosdb-v2.md)

<span data-ttu-id="b64ff-107">This article explains how to work with [Azure Cosmos DB](..\cosmos-db\serverless-computing-database.md) bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b64ff-107">This article explains how to work with [Azure Cosmos DB](..\cosmos-db\serverless-computing-database.md) bindings in Azure Functions.</span></span> <span data-ttu-id="b64ff-108">Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b64ff-108">Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.</span></span>

> [!NOTE]
> This article is for Azure Functions 1.x.  For information about how to use these bindings in Functions 2.x, see [Azure Cosmos DB bindings for Azure Functions 2.x](functions-bindings-cosmosdb-v2.md).
>
>This binding was originally named DocumentDB. In Functions version 1.x, only the trigger was renamed Cosmos DB; the input binding, output binding, and NuGet package retain the DocumentDB name.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-apis"></a><span data-ttu-id="b64ff-113">Supported APIs</span><span class="sxs-lookup"><span data-stu-id="b64ff-113">Supported APIs</span></span>

[!INCLUDE [SQL API support only](../../includes/functions-cosmosdb-sqlapi-note.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="b64ff-114">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="b64ff-114">Packages - Functions 1.x</span></span>

<span data-ttu-id="b64ff-115">The Azure Cosmos DB bindings for Functions version 1.x are provided in the [Microsoft.Azure.WebJobs.Extensions.DocumentDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB) NuGet package, version 1.x.</span><span class="sxs-lookup"><span data-stu-id="b64ff-115">The Azure Cosmos DB bindings for Functions version 1.x are provided in the [Microsoft.Azure.WebJobs.Extensions.DocumentDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB) NuGet package, version 1.x.</span></span> <span data-ttu-id="b64ff-116">Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.DocumentDB) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="b64ff-116">Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.DocumentDB) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="trigger"></a><span data-ttu-id="b64ff-117">Trigger</span><span class="sxs-lookup"><span data-stu-id="b64ff-117">Trigger</span></span>

<span data-ttu-id="b64ff-118">The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](../cosmos-db/change-feed.md) to listen for inserts and updates across partitions.</span><span class="sxs-lookup"><span data-stu-id="b64ff-118">The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](../cosmos-db/change-feed.md) to listen for inserts and updates across partitions.</span></span> <span data-ttu-id="b64ff-119">The change feed publishes inserts and updates, not deletions.</span><span class="sxs-lookup"><span data-stu-id="b64ff-119">The change feed publishes inserts and updates, not deletions.</span></span>

## <a name="trigger---example"></a><span data-ttu-id="b64ff-120">Trigger - example</span><span class="sxs-lookup"><span data-stu-id="b64ff-120">Trigger - example</span></span>

<span data-ttu-id="b64ff-121">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="b64ff-121">See the language-specific example:</span></span>

* [<span data-ttu-id="b64ff-122">C#</span><span class="sxs-lookup"><span data-stu-id="b64ff-122">C#</span></span>](#trigger---c-example)
* [<span data-ttu-id="b64ff-123">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="b64ff-123">C# script (.csx)</span></span>](#trigger---c-script-example)
* [<span data-ttu-id="b64ff-124">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b64ff-124">JavaScript</span></span>](#trigger---javascript-example)

[<span data-ttu-id="b64ff-125">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-125">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---c-example"></a><span data-ttu-id="b64ff-126">Trigger - C# example</span><span class="sxs-lookup"><span data-stu-id="b64ff-126">Trigger - C# example</span></span>

<span data-ttu-id="b64ff-127">The following example shows a [C# function](functions-dotnet-class-library.md) that is invoked when there are inserts or updates in the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-127">The following example shows a [C# function](functions-dotnet-class-library.md) that is invoked when there are inserts or updates in the specified database and collection.</span></span>

```cs
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;

namespace CosmosDBSamplesV1
{
    public static class CosmosTrigger
    {
        [FunctionName("CosmosTrigger")]
        public static void Run([CosmosDBTrigger(
            databaseName: "ToDoItems",
            collectionName: "Items",
            ConnectionStringSetting = "CosmosDBConnection",
            LeaseCollectionName = "leases",
            CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents, 
            TraceWriter log)
        {
            if (documents != null && documents.Count > 0)
            {
                log.Info($"Documents modified: {documents.Count}");
                log.Info($"First document Id: {documents[0].Id}");
            }
        }
    }
}
```

[<span data-ttu-id="b64ff-128">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-128">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---c-script-example"></a><span data-ttu-id="b64ff-129">Trigger - C# script example</span><span class="sxs-lookup"><span data-stu-id="b64ff-129">Trigger - C# script example</span></span>

<span data-ttu-id="b64ff-130">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-130">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-131">The function writes log messages when Cosmos DB records are modified.</span><span class="sxs-lookup"><span data-stu-id="b64ff-131">The function writes log messages when Cosmos DB records are modified.</span></span>

<span data-ttu-id="b64ff-132">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-132">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "type": "cosmosDBTrigger",
    "name": "documents",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "<connection-app-setting>",
    "databaseName": "Tasks",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": true
}
```

<span data-ttu-id="b64ff-133">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-133">Here's the C# script code:</span></span>
 
```cs 
    #r "Microsoft.Azure.Documents.Client"
    
    using System;
    using Microsoft.Azure.Documents;
    using System.Collections.Generic;
    

    public static void Run(IReadOnlyList<Document> documents, TraceWriter log)
    {
      log.Verbose("Documents modified " + documents.Count);
      log.Verbose("First document Id " + documents[0].Id);
    }
```

[<span data-ttu-id="b64ff-134">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-134">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---javascript-example"></a><span data-ttu-id="b64ff-135">Trigger - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="b64ff-135">Trigger - JavaScript example</span></span>

<span data-ttu-id="b64ff-136">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-136">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-137">The function writes log messages when Cosmos DB records are modified.</span><span class="sxs-lookup"><span data-stu-id="b64ff-137">The function writes log messages when Cosmos DB records are modified.</span></span>

<span data-ttu-id="b64ff-138">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-138">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "type": "cosmosDBTrigger",
    "name": "documents",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "<connection-app-setting>",
    "databaseName": "Tasks",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": true
}
```

<span data-ttu-id="b64ff-139">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-139">Here's the JavaScript code:</span></span>

```javascript
    module.exports = function (context, documents) {
      context.log('First document Id modified : ', documents[0].id);

      context.done();
    }
```

## <a name="trigger---attributes"></a><span data-ttu-id="b64ff-140">Trigger - attributes</span><span class="sxs-lookup"><span data-stu-id="b64ff-140">Trigger - attributes</span></span>

<span data-ttu-id="b64ff-141">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-141">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.</span></span>

<span data-ttu-id="b64ff-142">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="b64ff-142">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="b64ff-143">For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration).</span><span class="sxs-lookup"><span data-stu-id="b64ff-143">For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration).</span></span> <span data-ttu-id="b64ff-144">Here's a `CosmosDBTrigger` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="b64ff-144">Here's a `CosmosDBTrigger` attribute example in a method signature:</span></span>

```csharp
    [FunctionName("DocumentUpdates")]
    public static void Run(
        [CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
    IReadOnlyList<Document> documents,
        TraceWriter log)
    {
        ...
    }
```

<span data-ttu-id="b64ff-145">For a complete example, see [Trigger - C# example](#trigger---c-example).</span><span class="sxs-lookup"><span data-stu-id="b64ff-145">For a complete example, see [Trigger - C# example](#trigger---c-example).</span></span>

## <a name="trigger---configuration"></a><span data-ttu-id="b64ff-146">Trigger - configuration</span><span class="sxs-lookup"><span data-stu-id="b64ff-146">Trigger - configuration</span></span>

<span data-ttu-id="b64ff-147">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-147">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger` attribute.</span></span>

|<span data-ttu-id="b64ff-148">function.json property</span><span class="sxs-lookup"><span data-stu-id="b64ff-148">function.json property</span></span> | <span data-ttu-id="b64ff-149">Attribute property</span><span class="sxs-lookup"><span data-stu-id="b64ff-149">Attribute property</span></span> |<span data-ttu-id="b64ff-150">Description</span><span class="sxs-lookup"><span data-stu-id="b64ff-150">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="b64ff-151">**type**</span><span class="sxs-lookup"><span data-stu-id="b64ff-151">**type**</span></span> || <span data-ttu-id="b64ff-152">Must be set to `cosmosDBTrigger`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-152">Must be set to `cosmosDBTrigger`.</span></span> |
|<span data-ttu-id="b64ff-153">**direction**</span><span class="sxs-lookup"><span data-stu-id="b64ff-153">**direction**</span></span> || <span data-ttu-id="b64ff-154">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-154">Must be set to `in`.</span></span> <span data-ttu-id="b64ff-155">This parameter is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b64ff-155">This parameter is set automatically when you create the trigger in the Azure portal.</span></span> |
|<span data-ttu-id="b64ff-156">**name**</span><span class="sxs-lookup"><span data-stu-id="b64ff-156">**name**</span></span> || <span data-ttu-id="b64ff-157">The variable name used in function code that represents the list of documents with changes.</span><span class="sxs-lookup"><span data-stu-id="b64ff-157">The variable name used in function code that represents the list of documents with changes.</span></span> | 
|<span data-ttu-id="b64ff-158">**connectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-158">**connectionStringSetting**</span></span>|<span data-ttu-id="b64ff-159">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-159">**ConnectionStringSetting**</span></span> | <span data-ttu-id="b64ff-160">The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored.</span><span class="sxs-lookup"><span data-stu-id="b64ff-160">The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored.</span></span> |
|<span data-ttu-id="b64ff-161">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-161">**databaseName**</span></span>|<span data-ttu-id="b64ff-162">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-162">**DatabaseName**</span></span>  | <span data-ttu-id="b64ff-163">The name of the Azure Cosmos DB database with the collection being monitored.</span><span class="sxs-lookup"><span data-stu-id="b64ff-163">The name of the Azure Cosmos DB database with the collection being monitored.</span></span> |
|<span data-ttu-id="b64ff-164">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-164">**collectionName**</span></span> |<span data-ttu-id="b64ff-165">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-165">**CollectionName**</span></span> | <span data-ttu-id="b64ff-166">The name of the collection being monitored.</span><span class="sxs-lookup"><span data-stu-id="b64ff-166">The name of the collection being monitored.</span></span> |
|<span data-ttu-id="b64ff-167">**leaseConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-167">**leaseConnectionStringSetting**</span></span> | <span data-ttu-id="b64ff-168">**LeaseConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-168">**LeaseConnectionStringSetting**</span></span> | <span data-ttu-id="b64ff-169">(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-169">(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection.</span></span> <span data-ttu-id="b64ff-170">When not set, the `connectionStringSetting` value is used.</span><span class="sxs-lookup"><span data-stu-id="b64ff-170">When not set, the `connectionStringSetting` value is used.</span></span> <span data-ttu-id="b64ff-171">This parameter is automatically set when the binding is created in the portal.</span><span class="sxs-lookup"><span data-stu-id="b64ff-171">This parameter is automatically set when the binding is created in the portal.</span></span> <span data-ttu-id="b64ff-172">The connection string for the leases collection must have write permissions.</span><span class="sxs-lookup"><span data-stu-id="b64ff-172">The connection string for the leases collection must have write permissions.</span></span>|
|<span data-ttu-id="b64ff-173">**leaseDatabaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-173">**leaseDatabaseName**</span></span> |<span data-ttu-id="b64ff-174">**LeaseDatabaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-174">**LeaseDatabaseName**</span></span> | <span data-ttu-id="b64ff-175">(Optional) The name of the database that holds the collection used to store leases.</span><span class="sxs-lookup"><span data-stu-id="b64ff-175">(Optional) The name of the database that holds the collection used to store leases.</span></span> <span data-ttu-id="b64ff-176">When not set, the value of the `databaseName` setting is used.</span><span class="sxs-lookup"><span data-stu-id="b64ff-176">When not set, the value of the `databaseName` setting is used.</span></span> <span data-ttu-id="b64ff-177">This parameter is automatically set when the binding is created in the portal.</span><span class="sxs-lookup"><span data-stu-id="b64ff-177">This parameter is automatically set when the binding is created in the portal.</span></span> |
|<span data-ttu-id="b64ff-178">**leaseCollectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-178">**leaseCollectionName**</span></span> | <span data-ttu-id="b64ff-179">**LeaseCollectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-179">**LeaseCollectionName**</span></span> | <span data-ttu-id="b64ff-180">(Optional) The name of the collection used to store leases.</span><span class="sxs-lookup"><span data-stu-id="b64ff-180">(Optional) The name of the collection used to store leases.</span></span> <span data-ttu-id="b64ff-181">When not set, the value `leases` is used.</span><span class="sxs-lookup"><span data-stu-id="b64ff-181">When not set, the value `leases` is used.</span></span> |
|<span data-ttu-id="b64ff-182">**createLeaseCollectionIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="b64ff-182">**createLeaseCollectionIfNotExists**</span></span> | <span data-ttu-id="b64ff-183">**CreateLeaseCollectionIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="b64ff-183">**CreateLeaseCollectionIfNotExists**</span></span> | <span data-ttu-id="b64ff-184">(Optional) When set to `true`, the leases collection is automatically created when it doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="b64ff-184">(Optional) When set to `true`, the leases collection is automatically created when it doesn't already exist.</span></span> <span data-ttu-id="b64ff-185">The default value is `false`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-185">The default value is `false`.</span></span> |
|<span data-ttu-id="b64ff-186">**leasesCollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="b64ff-186">**leasesCollectionThroughput**</span></span>| <span data-ttu-id="b64ff-187">**LeasesCollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="b64ff-187">**LeasesCollectionThroughput**</span></span>| <span data-ttu-id="b64ff-188">(Optional) Defines the amount of Request Units to assign when the leases collection is created.</span><span class="sxs-lookup"><span data-stu-id="b64ff-188">(Optional) Defines the amount of Request Units to assign when the leases collection is created.</span></span> <span data-ttu-id="b64ff-189">This setting is only used When `createLeaseCollectionIfNotExists` is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-189">This setting is only used When `createLeaseCollectionIfNotExists` is set to `true`.</span></span> <span data-ttu-id="b64ff-190">This parameter is  automatically set when the binding is created using the portal.</span><span class="sxs-lookup"><span data-stu-id="b64ff-190">This parameter is  automatically set when the binding is created using the portal.</span></span>
|<span data-ttu-id="b64ff-191">**leaseCollectionPrefix**</span><span class="sxs-lookup"><span data-stu-id="b64ff-191">**leaseCollectionPrefix**</span></span>| <span data-ttu-id="b64ff-192">**LeaseCollectionPrefix**</span><span class="sxs-lookup"><span data-stu-id="b64ff-192">**LeaseCollectionPrefix**</span></span>| <span data-ttu-id="b64ff-193">(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes.</span><span class="sxs-lookup"><span data-stu-id="b64ff-193">(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes.</span></span>
|<span data-ttu-id="b64ff-194">**feedPollDelay**</span><span class="sxs-lookup"><span data-stu-id="b64ff-194">**feedPollDelay**</span></span>| <span data-ttu-id="b64ff-195">**FeedPollDelay**</span><span class="sxs-lookup"><span data-stu-id="b64ff-195">**FeedPollDelay**</span></span>| <span data-ttu-id="b64ff-196">(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained.</span><span class="sxs-lookup"><span data-stu-id="b64ff-196">(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained.</span></span> <span data-ttu-id="b64ff-197">Default is 5000 (5 seconds).</span><span class="sxs-lookup"><span data-stu-id="b64ff-197">Default is 5000 (5 seconds).</span></span>
|<span data-ttu-id="b64ff-198">**leaseAcquireInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-198">**leaseAcquireInterval**</span></span>| <span data-ttu-id="b64ff-199">**LeaseAcquireInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-199">**LeaseAcquireInterval**</span></span>| <span data-ttu-id="b64ff-200">(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances.</span><span class="sxs-lookup"><span data-stu-id="b64ff-200">(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances.</span></span> <span data-ttu-id="b64ff-201">Default is 13000 (13 seconds).</span><span class="sxs-lookup"><span data-stu-id="b64ff-201">Default is 13000 (13 seconds).</span></span>
|<span data-ttu-id="b64ff-202">**leaseExpirationInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-202">**leaseExpirationInterval**</span></span>| <span data-ttu-id="b64ff-203">**LeaseExpirationInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-203">**LeaseExpirationInterval**</span></span>| <span data-ttu-id="b64ff-204">(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition.</span><span class="sxs-lookup"><span data-stu-id="b64ff-204">(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="b64ff-205">If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance.</span><span class="sxs-lookup"><span data-stu-id="b64ff-205">If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance.</span></span> <span data-ttu-id="b64ff-206">Default is 60000 (60 seconds).</span><span class="sxs-lookup"><span data-stu-id="b64ff-206">Default is 60000 (60 seconds).</span></span>
|<span data-ttu-id="b64ff-207">**leaseRenewInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-207">**leaseRenewInterval**</span></span>| <span data-ttu-id="b64ff-208">**LeaseRenewInterval**</span><span class="sxs-lookup"><span data-stu-id="b64ff-208">**LeaseRenewInterval**</span></span>| <span data-ttu-id="b64ff-209">(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance.</span><span class="sxs-lookup"><span data-stu-id="b64ff-209">(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance.</span></span> <span data-ttu-id="b64ff-210">Default is 17000 (17 seconds).</span><span class="sxs-lookup"><span data-stu-id="b64ff-210">Default is 17000 (17 seconds).</span></span>
|<span data-ttu-id="b64ff-211">**checkpointFrequency**</span><span class="sxs-lookup"><span data-stu-id="b64ff-211">**checkpointFrequency**</span></span>| <span data-ttu-id="b64ff-212">**CheckpointFrequency**</span><span class="sxs-lookup"><span data-stu-id="b64ff-212">**CheckpointFrequency**</span></span>| <span data-ttu-id="b64ff-213">(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints.</span><span class="sxs-lookup"><span data-stu-id="b64ff-213">(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints.</span></span> <span data-ttu-id="b64ff-214">Default is always after a successful Function call.</span><span class="sxs-lookup"><span data-stu-id="b64ff-214">Default is always after a successful Function call.</span></span>
|<span data-ttu-id="b64ff-215">**maxItemsPerInvocation**</span><span class="sxs-lookup"><span data-stu-id="b64ff-215">**maxItemsPerInvocation**</span></span>| <span data-ttu-id="b64ff-216">**MaxItemsPerInvocation**</span><span class="sxs-lookup"><span data-stu-id="b64ff-216">**MaxItemsPerInvocation**</span></span>| <span data-ttu-id="b64ff-217">(Optional) When set, it customizes the maximum amount of items received per Function call.</span><span class="sxs-lookup"><span data-stu-id="b64ff-217">(Optional) When set, it customizes the maximum amount of items received per Function call.</span></span>

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a><span data-ttu-id="b64ff-218">Trigger - usage</span><span class="sxs-lookup"><span data-stu-id="b64ff-218">Trigger - usage</span></span>

<span data-ttu-id="b64ff-219">The trigger requires a second collection that it uses to store _leases_ over the partitions.</span><span class="sxs-lookup"><span data-stu-id="b64ff-219">The trigger requires a second collection that it uses to store _leases_ over the partitions.</span></span> <span data-ttu-id="b64ff-220">Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.</span><span class="sxs-lookup"><span data-stu-id="b64ff-220">Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.</span></span>

>[!IMPORTANT]
> If multiple functions are configured to use a Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix` for each function. Otherwise, only one of the functions will be triggered. For information about the prefix, see the [Configuration section](#trigger---configuration).

<span data-ttu-id="b64ff-224">The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself.</span><span class="sxs-lookup"><span data-stu-id="b64ff-224">The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself.</span></span> <span data-ttu-id="b64ff-225">If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.</span><span class="sxs-lookup"><span data-stu-id="b64ff-225">If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.</span></span>

## <a name="input"></a><span data-ttu-id="b64ff-226">Input</span><span class="sxs-lookup"><span data-stu-id="b64ff-226">Input</span></span>

<span data-ttu-id="b64ff-227">The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function.</span><span class="sxs-lookup"><span data-stu-id="b64ff-227">The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function.</span></span> <span data-ttu-id="b64ff-228">The document ID or query parameters can be determined based on the trigger that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="b64ff-228">The document ID or query parameters can be determined based on the trigger that invokes the function.</span></span>

## <a name="input---examples"></a><span data-ttu-id="b64ff-229">Input - examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-229">Input - examples</span></span>

<span data-ttu-id="b64ff-230">See the language-specific examples that read a single document by specifying an ID value:</span><span class="sxs-lookup"><span data-stu-id="b64ff-230">See the language-specific examples that read a single document by specifying an ID value:</span></span>

* [<span data-ttu-id="b64ff-231">C#</span><span class="sxs-lookup"><span data-stu-id="b64ff-231">C#</span></span>](#input---c-examples)
* [<span data-ttu-id="b64ff-232">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="b64ff-232">C# script (.csx)</span></span>](#input---c-script-examples)
* [<span data-ttu-id="b64ff-233">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b64ff-233">JavaScript</span></span>](#input---javascript-examples)
* [<span data-ttu-id="b64ff-234">F#</span><span class="sxs-lookup"><span data-stu-id="b64ff-234">F#</span></span>](#input---f-examples)

[<span data-ttu-id="b64ff-235">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-235">Skip input examples</span></span>](#input---attributes)

### <a name="input---c-examples"></a><span data-ttu-id="b64ff-236">Input - C# examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-236">Input - C# examples</span></span>

<span data-ttu-id="b64ff-237">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-237">This section contains the following examples:</span></span>

* [<span data-ttu-id="b64ff-238">Queue trigger, look up ID from JSON</span><span class="sxs-lookup"><span data-stu-id="b64ff-238">Queue trigger, look up ID from JSON</span></span>](#queue-trigger-look-up-id-from-json-c)
* [<span data-ttu-id="b64ff-239">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="b64ff-239">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-c)
* [<span data-ttu-id="b64ff-240">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="b64ff-240">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-c)
* [<span data-ttu-id="b64ff-241">HTTP trigger, look up ID from route data, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="b64ff-241">HTTP trigger, look up ID from route data, using SqlQuery</span></span>](#http-trigger-look-up-id-from-route-data-using-sqlquery-c)
* [<span data-ttu-id="b64ff-242">HTTP trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="b64ff-242">HTTP trigger, get multiple docs, using SqlQuery</span></span>](#http-trigger-get-multiple-docs-using-sqlquery-c)
* [<span data-ttu-id="b64ff-243">HTTP trigger, get multiple docs, using DocumentClient</span><span class="sxs-lookup"><span data-stu-id="b64ff-243">HTTP trigger, get multiple docs, using DocumentClient</span></span>](#http-trigger-get-multiple-docs-using-documentclient-c)

<span data-ttu-id="b64ff-244">The examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="b64ff-244">The examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV1
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="b64ff-245">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-245">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-json-c"></a><span data-ttu-id="b64ff-246">Queue trigger, look up ID from JSON (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-246">Queue trigger, look up ID from JSON (C#)</span></span>

<span data-ttu-id="b64ff-247">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-247">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-248">The function is triggered by a queue message that contains a JSON object.</span><span class="sxs-lookup"><span data-stu-id="b64ff-248">The function is triggered by a queue message that contains a JSON object.</span></span> <span data-ttu-id="b64ff-249">The queue trigger parses the JSON into an object named `ToDoItemLookup`, which contains the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-249">The queue trigger parses the JSON into an object named `ToDoItemLookup`, which contains the ID to look up.</span></span> <span data-ttu-id="b64ff-250">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-250">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
namespace CosmosDBSamplesV1
{
    public class ToDoItemLookup
    {
        public string ToDoItemId { get; set; }
    }
}
```

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;

namespace CosmosDBSamplesV1
{
    public static class DocByIdFromJSON
    {
        [FunctionName("DocByIdFromJSON")]
        public static void Run(
            [QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection", 
                Id = "{ToDoItemId}")]ToDoItem toDoItem,
            TraceWriter log)
        {
            log.Info($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId}");

            if (toDoItem == null)
            {
                log.Info($"ToDo item not found");
            }
            else
            {
                log.Info($"Found ToDo item, Description={toDoItem.Description}");
            }
        }
    }
}
```

[<span data-ttu-id="b64ff-251">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-251">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-c"></a><span data-ttu-id="b64ff-252">HTTP trigger, look up ID from query string (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-252">HTTP trigger, look up ID from query string (C#)</span></span>

<span data-ttu-id="b64ff-253">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-253">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-254">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-254">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-255">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-255">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;

namespace CosmosDBSamplesV1
{
    public static class DocByIdFromQueryString
    {
        [FunctionName("DocByIdFromQueryString")]
        public static HttpResponseMessage Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection", 
                Id = "{Query.id}")] ToDoItem toDoItem,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");
            if (toDoItem == null)
            {
                log.Info($"ToDo item not found");
            }
            else
            {
                log.Info($"Found ToDo item, Description={toDoItem.Description}");
            }
            return req.CreateResponse(HttpStatusCode.OK);
        }
    }
}
```

[<span data-ttu-id="b64ff-256">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-256">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-c"></a><span data-ttu-id="b64ff-257">HTTP trigger, look up ID from route data (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-257">HTTP trigger, look up ID from route data (C#)</span></span>

<span data-ttu-id="b64ff-258">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-258">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-259">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-259">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-260">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-260">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;

namespace CosmosDBSamplesV1
{
    public static class DocByIdFromRouteData
    {
        [FunctionName("DocByIdFromRouteData")]
        public static HttpResponseMessage Run(
            [HttpTrigger(
                AuthorizationLevel.Anonymous, "get", "post", 
                Route = "todoitems/{id}")]HttpRequestMessage req,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection", 
                Id = "{id}")] ToDoItem toDoItem,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");

            if (toDoItem == null)
            {
                log.Info($"ToDo item not found");
            }
            else
            {
                log.Info($"Found ToDo item, Description={toDoItem.Description}");
            }
            return req.CreateResponse(HttpStatusCode.OK);
        }
    }
}
```

[<span data-ttu-id="b64ff-261">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-261">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-using-sqlquery-c"></a><span data-ttu-id="b64ff-262">HTTP trigger, look up ID from route data, using SqlQuery (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-262">HTTP trigger, look up ID from route data, using SqlQuery (C#)</span></span>

<span data-ttu-id="b64ff-263">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-263">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-264">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-264">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-265">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-265">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;

namespace CosmosDBSamplesV1
{
    public static class DocByIdFromRouteDataUsingSqlQuery
    {
        [FunctionName("DocByIdFromRouteDataUsingSqlQuery")]
        public static HttpResponseMessage Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", 
                Route = "todoitems2/{id}")]HttpRequestMessage req,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection", 
                SqlQuery = "select * from ToDoItems r where r.id = {id}")] IEnumerable<ToDoItem> toDoItems,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");
            foreach (ToDoItem toDoItem in toDoItems)
            {
                log.Info(toDoItem.Description);
            }
            return req.CreateResponse(HttpStatusCode.OK);
        }
    }
}
```

[<span data-ttu-id="b64ff-266">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-266">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-sqlquery-c"></a><span data-ttu-id="b64ff-267">HTTP trigger, get multiple docs, using SqlQuery (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-267">HTTP trigger, get multiple docs, using SqlQuery (C#)</span></span>

<span data-ttu-id="b64ff-268">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-268">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span></span> <span data-ttu-id="b64ff-269">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b64ff-269">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="b64ff-270">The query is specified in the `SqlQuery` attribute property.</span><span class="sxs-lookup"><span data-stu-id="b64ff-270">The query is specified in the `SqlQuery` attribute property.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;

namespace CosmosDBSamplesV1
{
    public static class DocsBySqlQuery
    {
        [FunctionName("DocsBySqlQuery")]
        public static HttpResponseMessage Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
                HttpRequestMessage req,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection", 
                SqlQuery = "SELECT top 2 * FROM c order by c._ts desc")]
                IEnumerable<ToDoItem> toDoItems,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");
            foreach (ToDoItem toDoItem in toDoItems)
            {
                log.Info(toDoItem.Description);
            }
            return req.CreateResponse(HttpStatusCode.OK);
        }
    }
}
```

[<span data-ttu-id="b64ff-271">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-271">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-documentclient-c"></a><span data-ttu-id="b64ff-272">HTTP trigger, get multiple docs, using DocumentClient (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-272">HTTP trigger, get multiple docs, using DocumentClient (C#)</span></span>

<span data-ttu-id="b64ff-273">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-273">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span></span> <span data-ttu-id="b64ff-274">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b64ff-274">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="b64ff-275">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-275">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span></span> <span data-ttu-id="b64ff-276">The `DocumentClient` instance could also be used for write operations.</span><span class="sxs-lookup"><span data-stu-id="b64ff-276">The `DocumentClient` instance could also be used for write operations.</span></span>

```cs
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

namespace CosmosDBSamplesV1
{
    public static class DocsByUsingDocumentClient
    {
        [FunctionName("DocsByUsingDocumentClient")]
        public static async Task<HttpResponseMessage> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection")] DocumentClient client,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");

            Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
            string searchterm = req.GetQueryNameValuePairs()
                .FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
                .Value;

            if (searchterm == null)
            {
                return req.CreateResponse(HttpStatusCode.NotFound);
            }

            log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
            IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
                .Where(p => p.Description.Contains(searchterm))
                .AsDocumentQuery();

            while (query.HasMoreResults)
            {
                foreach (ToDoItem result in await query.ExecuteNextAsync())
                {
                    log.Info(result.Description);
                }
            }
            return req.CreateResponse(HttpStatusCode.OK);
        }
    }
}
```

[<span data-ttu-id="b64ff-277">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-277">Skip input examples</span></span>](#input---attributes)

### <a name="input---c-script-examples"></a><span data-ttu-id="b64ff-278">Input - C# script examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-278">Input - C# script examples</span></span>

<span data-ttu-id="b64ff-279">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-279">This section contains the following examples:</span></span>

* [<span data-ttu-id="b64ff-280">Queue trigger, look up ID from string</span><span class="sxs-lookup"><span data-stu-id="b64ff-280">Queue trigger, look up ID from string</span></span>](#queue-trigger-look-up-id-from-string-c-script)
* [<span data-ttu-id="b64ff-281">Queue trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="b64ff-281">Queue trigger, get multiple docs, using SqlQuery</span></span>](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)
* [<span data-ttu-id="b64ff-282">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="b64ff-282">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-c-script)
* [<span data-ttu-id="b64ff-283">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="b64ff-283">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-c-script)
* [<span data-ttu-id="b64ff-284">HTTP trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="b64ff-284">HTTP trigger, get multiple docs, using SqlQuery</span></span>](#http-trigger-get-multiple-docs-using-sqlquery-c-script)
* [<span data-ttu-id="b64ff-285">HTTP trigger, get multiple docs, using DocumentClient</span><span class="sxs-lookup"><span data-stu-id="b64ff-285">HTTP trigger, get multiple docs, using DocumentClient</span></span>](#http-trigger-get-multiple-docs-using-documentclient-c-script)

<span data-ttu-id="b64ff-286">The HTTP trigger examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="b64ff-286">The HTTP trigger examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV1
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="b64ff-287">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-287">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-string-c-script"></a><span data-ttu-id="b64ff-288">Queue trigger, look up ID from string (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-288">Queue trigger, look up ID from string (C# script)</span></span>

<span data-ttu-id="b64ff-289">The following example shows a Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-289">The following example shows a Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-290">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="b64ff-290">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="b64ff-291">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-291">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "partitionKey": "{partition key value}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```
<span data-ttu-id="b64ff-292">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-292">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-293">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-293">Here's the C# script code:</span></span>

```cs
    using System;

    // Change input document contents using Azure Cosmos DB input binding 
    public static void Run(string myQueueItem, dynamic inputDocument)
    {   
      inputDocument.text = "This has changed.";
    }
```

[<span data-ttu-id="b64ff-294">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-294">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-get-multiple-docs-using-sqlquery-c-script"></a><span data-ttu-id="b64ff-295">Queue trigger, get multiple docs, using SqlQuery (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-295">Queue trigger, get multiple docs, using SqlQuery (C# script)</span></span>

<span data-ttu-id="b64ff-296">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-296">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-297">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span><span class="sxs-lookup"><span data-stu-id="b64ff-297">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span>

<span data-ttu-id="b64ff-298">The queue trigger provides a parameter `departmentId`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-298">The queue trigger provides a parameter `departmentId`.</span></span> <span data-ttu-id="b64ff-299">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span><span class="sxs-lookup"><span data-stu-id="b64ff-299">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> 

<span data-ttu-id="b64ff-300">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-300">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connection": "CosmosDBConnection"
}
```

<span data-ttu-id="b64ff-301">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-301">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-302">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-302">Here's the C# script code:</span></span>

```csharp
    public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
    {   
        foreach (var doc in documents)
        {
            // operate on each document
        }    
    }

    public class QueuePayload
    {
        public string departmentId { get; set; }
    }
```

[<span data-ttu-id="b64ff-303">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-303">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-c-script"></a><span data-ttu-id="b64ff-304">HTTP trigger, look up ID from query string (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-304">HTTP trigger, look up ID from query string (C# script)</span></span>

<span data-ttu-id="b64ff-305">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-305">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-306">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-306">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-307">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-307">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="b64ff-308">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-308">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "in",
      "Id": "{Query.id}"
    }
  ],
  "disabled": true
}
```

<span data-ttu-id="b64ff-309">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-309">Here's the C# script code:</span></span>

```cs
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    if (toDoItem == null)
    {
         log.Info($"ToDo item not found");
    }
    else
    {
        log.Info($"Found ToDo item, Description={toDoItem.Description}");
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

[<span data-ttu-id="b64ff-310">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-310">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-c-script"></a><span data-ttu-id="b64ff-311">HTTP trigger, look up ID from route data (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-311">HTTP trigger, look up ID from route data (C# script)</span></span>

<span data-ttu-id="b64ff-312">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-312">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-313">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-313">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-314">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-314">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="b64ff-315">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-315">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ],
      "route":"todoitems/{id}"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "in",
      "Id": "{id}"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="b64ff-316">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-316">Here's the C# script code:</span></span>

```cs
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    if (toDoItem == null)
    {
         log.Info($"ToDo item not found");
    }
    else
    {
        log.Info($"Found ToDo item, Description={toDoItem.Description}");
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

[<span data-ttu-id="b64ff-317">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-317">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-sqlquery-c-script"></a><span data-ttu-id="b64ff-318">HTTP trigger, get multiple docs, using SqlQuery (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-318">HTTP trigger, get multiple docs, using SqlQuery (C# script)</span></span>

<span data-ttu-id="b64ff-319">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-319">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span></span> <span data-ttu-id="b64ff-320">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b64ff-320">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="b64ff-321">The query is specified in the `SqlQuery` attribute property.</span><span class="sxs-lookup"><span data-stu-id="b64ff-321">The query is specified in the `SqlQuery` attribute property.</span></span>

<span data-ttu-id="b64ff-322">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-322">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "toDoItems",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "in",
      "sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="b64ff-323">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-323">Here's the C# script code:</span></span>

```cs
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, IEnumerable<ToDoItem> toDoItems, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    foreach (ToDoItem toDoItem in toDoItems)
    {
        log.Info(toDoItem.Description);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

[<span data-ttu-id="b64ff-324">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-324">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-documentclient-c-script"></a><span data-ttu-id="b64ff-325">HTTP trigger, get multiple docs, using DocumentClient (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-325">HTTP trigger, get multiple docs, using DocumentClient (C# script)</span></span>

<span data-ttu-id="b64ff-326">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-326">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span></span> <span data-ttu-id="b64ff-327">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b64ff-327">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="b64ff-328">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-328">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span></span> <span data-ttu-id="b64ff-329">The `DocumentClient` instance could also be used for write operations.</span><span class="sxs-lookup"><span data-stu-id="b64ff-329">The `DocumentClient` instance could also be used for write operations.</span></span>

<span data-ttu-id="b64ff-330">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-330">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "client",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "inout"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="b64ff-331">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-331">Here's the C# script code:</span></span>

```cs
#r "Microsoft.Azure.Documents.Client"

using System.Net;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, DocumentClient client, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
    string searchterm = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
        .Value;

    if (searchterm == null)
    {
        return req.CreateResponse(HttpStatusCode.NotFound);
    }

    log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
    IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
        .Where(p => p.Description.Contains(searchterm))
        .AsDocumentQuery();

    while (query.HasMoreResults)
    {
        foreach (ToDoItem result in await query.ExecuteNextAsync())
        {
            log.Info(result.Description);
        }
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

[<span data-ttu-id="b64ff-332">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-332">Skip input examples</span></span>](#input---attributes)

### <a name="input---javascript-examples"></a><span data-ttu-id="b64ff-333">Input - JavaScript examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-333">Input - JavaScript examples</span></span>

<span data-ttu-id="b64ff-334">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-334">This section contains the following examples:</span></span>

* [<span data-ttu-id="b64ff-335">Queue trigger, look up ID from JSON</span><span class="sxs-lookup"><span data-stu-id="b64ff-335">Queue trigger, look up ID from JSON</span></span>](#queue-trigger-look-up-id-from-string-javascript)
* [<span data-ttu-id="b64ff-336">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="b64ff-336">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-javascript)
* [<span data-ttu-id="b64ff-337">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="b64ff-337">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-javascript)
* [<span data-ttu-id="b64ff-338">Queue trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="b64ff-338">Queue trigger, get multiple docs, using SqlQuery</span></span>](#queue-trigger-get-multiple-docs-using-sqlquery-javascript)

[<span data-ttu-id="b64ff-339">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-339">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-json-javascript"></a><span data-ttu-id="b64ff-340">Queue trigger, look up ID from JSON (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b64ff-340">Queue trigger, look up ID from JSON (JavaScript)</span></span>

<span data-ttu-id="b64ff-341">The following example shows a Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-341">The following example shows a Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-342">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="b64ff-342">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="b64ff-343">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-343">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocumentIn",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger_payload_property}",
    "partitionKey": "{queueTrigger_payload_property}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
},
{
    "name": "inputDocumentOut",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": false,
    "partitionKey": "{queueTrigger_payload_property}",
    "connection": "MyAccount_COSMOSDB",
    "direction": "out"
}
```
<span data-ttu-id="b64ff-344">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-344">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-345">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-345">Here's the JavaScript code:</span></span>

```javascript
    // Change input document contents using Azure Cosmos DB input binding, using context.bindings.inputDocumentOut
    module.exports = function (context) {   
    context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
    context.bindings.inputDocumentOut.text = "This was updated!";
    context.done();
    };
```

[<span data-ttu-id="b64ff-346">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-346">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-javascript"></a><span data-ttu-id="b64ff-347">HTTP trigger, look up ID from query string (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b64ff-347">HTTP trigger, look up ID from query string (JavaScript)</span></span>

<span data-ttu-id="b64ff-348">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-348">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-349">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-349">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-350">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-350">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="b64ff-351">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-351">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "in",
      "Id": "{Query.id}"
    }
  ],
  "disabled": true
}
```

<span data-ttu-id="b64ff-352">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-352">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, req, toDoItem) {
    context.log('JavaScript queue trigger function processed work item');
    if (!toDoItem)
    {
        context.log("ToDo item not found");
    }
    else
    {
        context.log("Found ToDo item, Description=" + toDoItem.Description);
    }

    context.done();
};
```

[<span data-ttu-id="b64ff-353">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-353">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-javascript"></a><span data-ttu-id="b64ff-354">HTTP trigger, look up ID from route data (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b64ff-354">HTTP trigger, look up ID from route data (JavaScript)</span></span>

<span data-ttu-id="b64ff-355">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-355">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span></span> <span data-ttu-id="b64ff-356">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="b64ff-356">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="b64ff-357">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-357">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="b64ff-358">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-358">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in",
      "methods": [
        "get",
        "post"
      ],
      "route":"todoitems/{id}"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    },
    {
      "type": "documentDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "in",
      "Id": "{id}"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="b64ff-359">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-359">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, req, toDoItem) {
    context.log('JavaScript queue trigger function processed work item');
    if (!toDoItem)
    {
        context.log("ToDo item not found");
    }
    else
    {
        context.log("Found ToDo item, Description=" + toDoItem.Description);
    }

    context.done();
};
```

[<span data-ttu-id="b64ff-360">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-360">Skip input examples</span></span>](#input---attributes)



#### <a name="queue-trigger-get-multiple-docs-using-sqlquery-javascript"></a><span data-ttu-id="b64ff-361">Queue trigger, get multiple docs, using SqlQuery (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="b64ff-361">Queue trigger, get multiple docs, using SqlQuery (JavaScript)</span></span>

<span data-ttu-id="b64ff-362">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-362">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-363">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span><span class="sxs-lookup"><span data-stu-id="b64ff-363">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span>

<span data-ttu-id="b64ff-364">The queue trigger provides a parameter `departmentId`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-364">The queue trigger provides a parameter `departmentId`.</span></span> <span data-ttu-id="b64ff-365">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span><span class="sxs-lookup"><span data-stu-id="b64ff-365">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> 

<span data-ttu-id="b64ff-366">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-366">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connection": "CosmosDBConnection"
}
```

<span data-ttu-id="b64ff-367">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-367">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-368">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-368">Here's the JavaScript code:</span></span>

```javascript
    module.exports = function (context, input) {    
        var documents = context.bindings.documents;
        for (var i = 0; i < documents.length; i++) {
            var document = documents[i];
            // operate on each document
        }       
        context.done();
    };
```

[<span data-ttu-id="b64ff-369">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-369">Skip input examples</span></span>](#input---attributes)

<a name="infsharp"></a>

### <a name="input---f-examples"></a><span data-ttu-id="b64ff-370">Input - F# examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-370">Input - F# examples</span></span>

<span data-ttu-id="b64ff-371">The following example shows a Cosmos DB input binding in a *function.json* file and a [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-371">The following example shows a Cosmos DB input binding in a *function.json* file and a [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-372">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="b64ff-372">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="b64ff-373">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-373">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "connection": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```

<span data-ttu-id="b64ff-374">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-374">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-375">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-375">Here's the F# code:</span></span>

```fsharp
    (* Change input document contents using Azure Cosmos DB input binding *)
    open FSharp.Interop.Dynamic
    let Run(myQueueItem: string, inputDocument: obj) =
    inputDocument?text <- "This has changed."
```

<span data-ttu-id="b64ff-376">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="b64ff-376">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
    "frameworks": {
        "net46": {
            "dependencies": {
                "Dynamitey": "1.0.2",
                "FSharp.Interop.Dynamic": "3.0.0"
            }
        }
    }
}
```

<span data-ttu-id="b64ff-377">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="b64ff-377">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

## <a name="input---attributes"></a><span data-ttu-id="b64ff-378">Input - attributes</span><span class="sxs-lookup"><span data-stu-id="b64ff-378">Input - attributes</span></span>

<span data-ttu-id="b64ff-379">In [C# class libraries](functions-dotnet-class-library.md), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-379">In [C# class libraries](functions-dotnet-class-library.md), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.</span></span>

<span data-ttu-id="b64ff-380">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="b64ff-380">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="b64ff-381">For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).</span><span class="sxs-lookup"><span data-stu-id="b64ff-381">For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).</span></span> 

## <a name="input---configuration"></a><span data-ttu-id="b64ff-382">Input - configuration</span><span class="sxs-lookup"><span data-stu-id="b64ff-382">Input - configuration</span></span>

<span data-ttu-id="b64ff-383">The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB` attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-383">The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB` attribute.</span></span>

|<span data-ttu-id="b64ff-384">function.json property</span><span class="sxs-lookup"><span data-stu-id="b64ff-384">function.json property</span></span> | <span data-ttu-id="b64ff-385">Attribute property</span><span class="sxs-lookup"><span data-stu-id="b64ff-385">Attribute property</span></span> |<span data-ttu-id="b64ff-386">Description</span><span class="sxs-lookup"><span data-stu-id="b64ff-386">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="b64ff-387">**type**</span><span class="sxs-lookup"><span data-stu-id="b64ff-387">**type**</span></span>     || <span data-ttu-id="b64ff-388">Must be set to `documentdb`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-388">Must be set to `documentdb`.</span></span>        |
|<span data-ttu-id="b64ff-389">**direction**</span><span class="sxs-lookup"><span data-stu-id="b64ff-389">**direction**</span></span>     || <span data-ttu-id="b64ff-390">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-390">Must be set to `in`.</span></span>         |
|<span data-ttu-id="b64ff-391">**name**</span><span class="sxs-lookup"><span data-stu-id="b64ff-391">**name**</span></span>     || <span data-ttu-id="b64ff-392">Name of the binding parameter that represents the document in the function.</span><span class="sxs-lookup"><span data-stu-id="b64ff-392">Name of the binding parameter that represents the document in the function.</span></span>  |
|<span data-ttu-id="b64ff-393">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-393">**databaseName**</span></span> |<span data-ttu-id="b64ff-394">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-394">**DatabaseName**</span></span> |<span data-ttu-id="b64ff-395">The database containing the document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-395">The database containing the document.</span></span>        |
|<span data-ttu-id="b64ff-396">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-396">**collectionName**</span></span> |<span data-ttu-id="b64ff-397">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-397">**CollectionName**</span></span> | <span data-ttu-id="b64ff-398">The name of the collection that contains the document.</span><span class="sxs-lookup"><span data-stu-id="b64ff-398">The name of the collection that contains the document.</span></span> |
|<span data-ttu-id="b64ff-399">**id**</span><span class="sxs-lookup"><span data-stu-id="b64ff-399">**id**</span></span>    | <span data-ttu-id="b64ff-400">**Id**</span><span class="sxs-lookup"><span data-stu-id="b64ff-400">**Id**</span></span> | <span data-ttu-id="b64ff-401">The ID of the document to retrieve.</span><span class="sxs-lookup"><span data-stu-id="b64ff-401">The ID of the document to retrieve.</span></span> <span data-ttu-id="b64ff-402">This property supports [binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="b64ff-402">This property supports [binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span> <span data-ttu-id="b64ff-403">Don't set both the **id** and **sqlQuery** properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-403">Don't set both the **id** and **sqlQuery** properties.</span></span> <span data-ttu-id="b64ff-404">If you don't set either one, the entire collection is retrieved.</span><span class="sxs-lookup"><span data-stu-id="b64ff-404">If you don't set either one, the entire collection is retrieved.</span></span> |
|<span data-ttu-id="b64ff-405">**sqlQuery**</span><span class="sxs-lookup"><span data-stu-id="b64ff-405">**sqlQuery**</span></span>  |<span data-ttu-id="b64ff-406">**SqlQuery**</span><span class="sxs-lookup"><span data-stu-id="b64ff-406">**SqlQuery**</span></span>  | <span data-ttu-id="b64ff-407">An Azure Cosmos DB SQL query used for retrieving multiple documents.</span><span class="sxs-lookup"><span data-stu-id="b64ff-407">An Azure Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="b64ff-408">The property supports runtime bindings, as in this example: `SELECT * FROM c where c.departmentId = {departmentId}`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-408">The property supports runtime bindings, as in this example: `SELECT * FROM c where c.departmentId = {departmentId}`.</span></span> <span data-ttu-id="b64ff-409">Don't set both the **id** and **sqlQuery** properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-409">Don't set both the **id** and **sqlQuery** properties.</span></span> <span data-ttu-id="b64ff-410">If you don't set either one, the entire collection is retrieved.</span><span class="sxs-lookup"><span data-stu-id="b64ff-410">If you don't set either one, the entire collection is retrieved.</span></span>|
|<span data-ttu-id="b64ff-411">**connection**</span><span class="sxs-lookup"><span data-stu-id="b64ff-411">**connection**</span></span>     |<span data-ttu-id="b64ff-412">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-412">**ConnectionStringSetting**</span></span>|<span data-ttu-id="b64ff-413">The name of the app setting containing your Azure Cosmos DB connection string.</span><span class="sxs-lookup"><span data-stu-id="b64ff-413">The name of the app setting containing your Azure Cosmos DB connection string.</span></span>        |
|<span data-ttu-id="b64ff-414">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="b64ff-414">**partitionKey**</span></span>|<span data-ttu-id="b64ff-415">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="b64ff-415">**PartitionKey**</span></span>|<span data-ttu-id="b64ff-416">Specifies the partition key value for the lookup.</span><span class="sxs-lookup"><span data-stu-id="b64ff-416">Specifies the partition key value for the lookup.</span></span> <span data-ttu-id="b64ff-417">May include binding parameters.</span><span class="sxs-lookup"><span data-stu-id="b64ff-417">May include binding parameters.</span></span>|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="input---usage"></a><span data-ttu-id="b64ff-418">Input - usage</span><span class="sxs-lookup"><span data-stu-id="b64ff-418">Input - usage</span></span>

<span data-ttu-id="b64ff-419">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span><span class="sxs-lookup"><span data-stu-id="b64ff-419">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 

<span data-ttu-id="b64ff-420">In JavaScript functions, updates are not made automatically upon function exit.</span><span class="sxs-lookup"><span data-stu-id="b64ff-420">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="b64ff-421">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span><span class="sxs-lookup"><span data-stu-id="b64ff-421">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="b64ff-422">See the [JavaScript example](#input---javascript-example).</span><span class="sxs-lookup"><span data-stu-id="b64ff-422">See the [JavaScript example](#input---javascript-example).</span></span>

## <a name="output"></a><span data-ttu-id="b64ff-423">Output</span><span class="sxs-lookup"><span data-stu-id="b64ff-423">Output</span></span>

<span data-ttu-id="b64ff-424">The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span><span class="sxs-lookup"><span data-stu-id="b64ff-424">The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span></span> 

## <a name="output---examples"></a><span data-ttu-id="b64ff-425">Output - examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-425">Output - examples</span></span>

<span data-ttu-id="b64ff-426">See the language-specific examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-426">See the language-specific examples:</span></span>

* [<span data-ttu-id="b64ff-427">C#</span><span class="sxs-lookup"><span data-stu-id="b64ff-427">C#</span></span>](#output---c-examples)
* [<span data-ttu-id="b64ff-428">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="b64ff-428">C# script (.csx)</span></span>](#output---c-script-examples)
* [<span data-ttu-id="b64ff-429">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b64ff-429">JavaScript</span></span>](#output---javascript-examples)
* [<span data-ttu-id="b64ff-430">F#</span><span class="sxs-lookup"><span data-stu-id="b64ff-430">F#</span></span>](#output---f-examples)

<span data-ttu-id="b64ff-431">See also the [input example](#input---c-examples) that uses `DocumentClient`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-431">See also the [input example](#input---c-examples) that uses `DocumentClient`.</span></span>

[<span data-ttu-id="b64ff-432">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-432">Skip output examples</span></span>](#output---attributes)

### <a name="ouput---c-examples"></a><span data-ttu-id="b64ff-433">Ouput - C# examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-433">Ouput - C# examples</span></span>

<span data-ttu-id="b64ff-434">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-434">This section contains the following examples:</span></span>

* <span data-ttu-id="b64ff-435">Queue trigger, write one doc</span><span class="sxs-lookup"><span data-stu-id="b64ff-435">Queue trigger, write one doc</span></span>
* <span data-ttu-id="b64ff-436">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="b64ff-436">Queue trigger, write docs using IAsyncCollector</span></span>

<span data-ttu-id="b64ff-437">The examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="b64ff-437">The examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV1
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="b64ff-438">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-438">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-one-doc-c"></a><span data-ttu-id="b64ff-439">Queue trigger, write one doc (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-439">Queue trigger, write one doc (C#)</span></span>

<span data-ttu-id="b64ff-440">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a document to a database, using data provided in message from Queue storage.</span><span class="sxs-lookup"><span data-stu-id="b64ff-440">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a document to a database, using data provided in message from Queue storage.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System;

namespace CosmosDBSamplesV1
{
    public static class WriteOneDoc
    {
        [FunctionName("WriteOneDoc")]
        public static void Run(
            [QueueTrigger("todoqueueforwrite")] string queueMessage,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection")]out dynamic document,
            TraceWriter log)
        {
            document = new { Description = queueMessage, id = Guid.NewGuid() };

            log.Info($"C# Queue trigger function inserted one row");
            log.Info($"Description={queueMessage}");
        }
    }
}
```

[<span data-ttu-id="b64ff-441">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-441">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-docs-using-iasynccollector-c"></a><span data-ttu-id="b64ff-442">Queue trigger, write docs using IAsyncCollector (C#)</span><span class="sxs-lookup"><span data-stu-id="b64ff-442">Queue trigger, write docs using IAsyncCollector (C#)</span></span>

<span data-ttu-id="b64ff-443">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a collection of documents to a database, using data provided in a queue message JSON.</span><span class="sxs-lookup"><span data-stu-id="b64ff-443">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a collection of documents to a database, using data provided in a queue message JSON.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Threading.Tasks;

namespace CosmosDBSamplesV1
{
    public static class WriteDocsIAsyncCollector
    {
        [FunctionName("WriteDocsIAsyncCollector")]
        public static async Task Run(
            [QueueTrigger("todoqueueforwritemulti")] ToDoItem[] toDoItemsIn,
            [DocumentDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection")]
                IAsyncCollector<ToDoItem> toDoItemsOut,
            TraceWriter log)
        {
            log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");

            foreach (ToDoItem toDoItem in toDoItemsIn)
            {
                log.Info($"Description={toDoItem.Description}");
                await toDoItemsOut.AddAsync(toDoItem);
            }
        }
    }
}
```

[<span data-ttu-id="b64ff-444">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-444">Skip output examples</span></span>](#output---attributes)

### <a name="output---c-script-examples"></a><span data-ttu-id="b64ff-445">Output - C# script examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-445">Output - C# script examples</span></span>

<span data-ttu-id="b64ff-446">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="b64ff-446">This section contains the following examples:</span></span>

* <span data-ttu-id="b64ff-447">Queue trigger, write one doc</span><span class="sxs-lookup"><span data-stu-id="b64ff-447">Queue trigger, write one doc</span></span>
* <span data-ttu-id="b64ff-448">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="b64ff-448">Queue trigger, write docs using IAsyncCollector</span></span>

[<span data-ttu-id="b64ff-449">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-449">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-one-doc-c-script"></a><span data-ttu-id="b64ff-450">Queue trigger, write one doc (C# script)</span><span class="sxs-lookup"><span data-stu-id="b64ff-450">Queue trigger, write one doc (C# script)</span></span>

<span data-ttu-id="b64ff-451">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-451">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-452">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="b64ff-452">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-453">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="b64ff-453">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-454">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-454">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

<span data-ttu-id="b64ff-455">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-455">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-456">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-456">Here's the C# script code:</span></span>

```cs
    #r "Newtonsoft.Json"

    using Microsoft.Azure.WebJobs.Host;
    using Newtonsoft.Json.Linq;

    public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
    {
      log.Info($"C# Queue trigger function processed: {myQueueItem}");

      dynamic employee = JObject.Parse(myQueueItem);

      employeeDocument = new {
        id = employee.name + "-" + employee.employeeId,
        name = employee.name,
        employeeId = employee.employeeId,
        address = employee.address
      };
    }
```

#### <a name="queue-trigger-write-docs-using-iasynccollector"></a><span data-ttu-id="b64ff-457">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="b64ff-457">Queue trigger, write docs using IAsyncCollector</span></span>

<span data-ttu-id="b64ff-458">To create multiple documents, you can bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span><span class="sxs-lookup"><span data-stu-id="b64ff-458">To create multiple documents, you can bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<span data-ttu-id="b64ff-459">This example refers to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="b64ff-459">This example refers to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV1
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

<span data-ttu-id="b64ff-460">Here's the function.json file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-460">Here's the function.json file:</span></span>

```json
{
  "bindings": [
    {
      "name": "toDoItemsIn",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "todoqueueforwritemulti",
      "connection": "AzureWebJobsStorage"
    },
    {
      "type": "documentDB",
      "name": "toDoItemsOut",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connection": "CosmosDBConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="b64ff-461">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-461">Here's the C# script code:</span></span>

```cs
using System;

public static async Task Run(ToDoItem[] toDoItemsIn, IAsyncCollector<ToDoItem> toDoItemsOut, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");

    foreach (ToDoItem toDoItem in toDoItemsIn)
    {
        log.Info($"Description={toDoItem.Description}");
        await toDoItemsOut.AddAsync(toDoItem);
    }
}
```

[<span data-ttu-id="b64ff-462">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-462">Skip output examples</span></span>](#output---attributes)

### <a name="output---javascript-examples"></a><span data-ttu-id="b64ff-463">Output - JavaScript examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-463">Output - JavaScript examples</span></span>

<span data-ttu-id="b64ff-464">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-464">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-465">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="b64ff-465">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-466">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="b64ff-466">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-467">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-467">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

<span data-ttu-id="b64ff-468">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-468">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-469">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-469">Here's the JavaScript code:</span></span>

```javascript
    module.exports = function (context) {

      context.bindings.employeeDocument = JSON.stringify({ 
        id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
        name: context.bindings.myQueueItem.name,
        employeeId: context.bindings.myQueueItem.employeeId,
        address: context.bindings.myQueueItem.address
      });

      context.done();
    };
```

[<span data-ttu-id="b64ff-470">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-470">Skip output examples</span></span>](#output---attributes)

### <a name="output---f-examples"></a><span data-ttu-id="b64ff-471">Output - F# examples</span><span class="sxs-lookup"><span data-stu-id="b64ff-471">Output - F# examples</span></span>

<span data-ttu-id="b64ff-472">The following example shows an Azure Cosmos DB output binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="b64ff-472">The following example shows an Azure Cosmos DB output binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="b64ff-473">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="b64ff-473">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-474">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="b64ff-474">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="b64ff-475">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="b64ff-475">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "documentDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connection": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```
<span data-ttu-id="b64ff-476">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="b64ff-476">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="b64ff-477">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="b64ff-477">Here's the F# code:</span></span>

```fsharp
    open FSharp.Interop.Dynamic
    open Newtonsoft.Json

    type Employee = {
      id: string
      name: string
      employeeId: string
      address: string
    }

    let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
      log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
      let employee = JObject.Parse(myQueueItem)
      employeeDocument <-
        { id = sprintf "%s-%s" employee?name employee?employeeId
          name = employee?name
          employeeId = employee?employeeId
          address = employee?address }
```

<span data-ttu-id="b64ff-478">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="b64ff-478">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
    "frameworks": {
        "net46": {
          "dependencies": {
            "Dynamitey": "1.0.2",
            "FSharp.Interop.Dynamic": "3.0.0"
           }
        }
    }
}
```

<span data-ttu-id="b64ff-479">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="b64ff-479">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

## <a name="output---attributes"></a><span data-ttu-id="b64ff-480">Output - attributes</span><span class="sxs-lookup"><span data-stu-id="b64ff-480">Output - attributes</span></span>

<span data-ttu-id="b64ff-481">In [C# class libraries](functions-dotnet-class-library.md), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-481">In [C# class libraries](functions-dotnet-class-library.md), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.</span></span>

<span data-ttu-id="b64ff-482">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="b64ff-482">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="b64ff-483">For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration).</span><span class="sxs-lookup"><span data-stu-id="b64ff-483">For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration).</span></span> <span data-ttu-id="b64ff-484">Here's a `DocumentDB` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="b64ff-484">Here's a `DocumentDB` attribute example in a method signature:</span></span>

```csharp
    [FunctionName("QueueToDocDB")]        
    public static void Run(
        [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
        [DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
    {
        ...
    }
```

<span data-ttu-id="b64ff-485">For a complete example, see [Output - C# example](#output---c-example).</span><span class="sxs-lookup"><span data-stu-id="b64ff-485">For a complete example, see [Output - C# example](#output---c-example).</span></span>

## <a name="output---configuration"></a><span data-ttu-id="b64ff-486">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="b64ff-486">Output - configuration</span></span>

<span data-ttu-id="b64ff-487">The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB` attribute.</span><span class="sxs-lookup"><span data-stu-id="b64ff-487">The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB` attribute.</span></span>

|<span data-ttu-id="b64ff-488">function.json property</span><span class="sxs-lookup"><span data-stu-id="b64ff-488">function.json property</span></span> | <span data-ttu-id="b64ff-489">Attribute property</span><span class="sxs-lookup"><span data-stu-id="b64ff-489">Attribute property</span></span> |<span data-ttu-id="b64ff-490">Description</span><span class="sxs-lookup"><span data-stu-id="b64ff-490">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="b64ff-491">**type**</span><span class="sxs-lookup"><span data-stu-id="b64ff-491">**type**</span></span>     || <span data-ttu-id="b64ff-492">Must be set to `documentdb`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-492">Must be set to `documentdb`.</span></span>        |
|<span data-ttu-id="b64ff-493">**direction**</span><span class="sxs-lookup"><span data-stu-id="b64ff-493">**direction**</span></span>     || <span data-ttu-id="b64ff-494">Must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="b64ff-494">Must be set to `out`.</span></span>         |
|<span data-ttu-id="b64ff-495">**name**</span><span class="sxs-lookup"><span data-stu-id="b64ff-495">**name**</span></span>     || <span data-ttu-id="b64ff-496">Name of the binding parameter that represents the document in the function.</span><span class="sxs-lookup"><span data-stu-id="b64ff-496">Name of the binding parameter that represents the document in the function.</span></span>  |
|<span data-ttu-id="b64ff-497">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-497">**databaseName**</span></span> | <span data-ttu-id="b64ff-498">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-498">**DatabaseName**</span></span>|<span data-ttu-id="b64ff-499">The database containing the collection where the document is created.</span><span class="sxs-lookup"><span data-stu-id="b64ff-499">The database containing the collection where the document is created.</span></span>     |
|<span data-ttu-id="b64ff-500">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-500">**collectionName**</span></span> |<span data-ttu-id="b64ff-501">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="b64ff-501">**CollectionName**</span></span>  | <span data-ttu-id="b64ff-502">The name of the collection where the document is created.</span><span class="sxs-lookup"><span data-stu-id="b64ff-502">The name of the collection where the document is created.</span></span> |
|<span data-ttu-id="b64ff-503">**createIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="b64ff-503">**createIfNotExists**</span></span>  |<span data-ttu-id="b64ff-504">**CreateIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="b64ff-504">**CreateIfNotExists**</span></span>    | <span data-ttu-id="b64ff-505">A boolean value to indicate whether the collection is created when it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="b64ff-505">A boolean value to indicate whether the collection is created when it doesn't exist.</span></span> <span data-ttu-id="b64ff-506">The default is *false* because new collections are created with reserved throughput, which has cost implications.</span><span class="sxs-lookup"><span data-stu-id="b64ff-506">The default is *false* because new collections are created with reserved throughput, which has cost implications.</span></span> <span data-ttu-id="b64ff-507">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b64ff-507">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>  |
|<span data-ttu-id="b64ff-508">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="b64ff-508">**partitionKey**</span></span>|<span data-ttu-id="b64ff-509">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="b64ff-509">**PartitionKey**</span></span> |<span data-ttu-id="b64ff-510">When `CreateIfNotExists` is true, defines the partition key path for the created collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-510">When `CreateIfNotExists` is true, defines the partition key path for the created collection.</span></span>|
|<span data-ttu-id="b64ff-511">**collectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="b64ff-511">**collectionThroughput**</span></span>|<span data-ttu-id="b64ff-512">**CollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="b64ff-512">**CollectionThroughput**</span></span>| <span data-ttu-id="b64ff-513">When `CreateIfNotExists` is true, defines the [throughput](../cosmos-db/set-throughput.md) of the created collection.</span><span class="sxs-lookup"><span data-stu-id="b64ff-513">When `CreateIfNotExists` is true, defines the [throughput](../cosmos-db/set-throughput.md) of the created collection.</span></span>|
|<span data-ttu-id="b64ff-514">**connection**</span><span class="sxs-lookup"><span data-stu-id="b64ff-514">**connection**</span></span>    |<span data-ttu-id="b64ff-515">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="b64ff-515">**ConnectionStringSetting**</span></span> |<span data-ttu-id="b64ff-516">The name of the app setting containing your Azure Cosmos DB connection string.</span><span class="sxs-lookup"><span data-stu-id="b64ff-516">The name of the app setting containing your Azure Cosmos DB connection string.</span></span>        |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a><span data-ttu-id="b64ff-517">Output - usage</span><span class="sxs-lookup"><span data-stu-id="b64ff-517">Output - usage</span></span>

<span data-ttu-id="b64ff-518">By default, when you write to the output parameter in your function, a document is created in your database.</span><span class="sxs-lookup"><span data-stu-id="b64ff-518">By default, when you write to the output parameter in your function, a document is created in your database.</span></span> <span data-ttu-id="b64ff-519">This document has an automatically generated GUID as the document ID.</span><span class="sxs-lookup"><span data-stu-id="b64ff-519">This document has an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="b64ff-520">You can specify the document ID of the output document by specifying the `id` property in the JSON object passed to the output parameter.</span><span class="sxs-lookup"><span data-stu-id="b64ff-520">You can specify the document ID of the output document by specifying the `id` property in the JSON object passed to the output parameter.</span></span> 

> [!Note]  
> When you specify the ID of an existing document, it gets overwritten by the new output document. 

## <a name="exceptions-and-return-codes"></a><span data-ttu-id="b64ff-522">Exceptions and return codes</span><span class="sxs-lookup"><span data-stu-id="b64ff-522">Exceptions and return codes</span></span>

| <span data-ttu-id="b64ff-523">Binding</span><span class="sxs-lookup"><span data-stu-id="b64ff-523">Binding</span></span> | <span data-ttu-id="b64ff-524">Reference</span><span class="sxs-lookup"><span data-stu-id="b64ff-524">Reference</span></span> |
|---|---|
| <span data-ttu-id="b64ff-525">CosmosDB</span><span class="sxs-lookup"><span data-stu-id="b64ff-525">CosmosDB</span></span> | [<span data-ttu-id="b64ff-526">CosmosDB Error Codes</span><span class="sxs-lookup"><span data-stu-id="b64ff-526">CosmosDB Error Codes</span></span>](https://docs.microsoft.com/rest/api/cosmos-db/http-status-codes-for-cosmosdb) |

## <a name="next-steps"></a><span data-ttu-id="b64ff-527">Next steps</span><span class="sxs-lookup"><span data-stu-id="b64ff-527">Next steps</span></span>

> [!div class="nextstepaction"]
> [Go to a quickstart that uses a Cosmos DB trigger](functions-create-cosmos-db-triggered-function.md)

> [!div class="nextstepaction"]
> [Learn more about serverless database computing with Cosmos DB](..\cosmos-db\serverless-computing-database.md)

> [!div class="nextstepaction"]
> [Learn more about Azure functions triggers and bindings](functions-triggers-bindings.md)
