---
title: Azure Cosmos DB bindings for Functions 2.x (Preview)
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
ms.openlocfilehash: ea1403ed8afe6e84a3118d891e8c2d34b390d158
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870012"
---
# <a name="azure-cosmos-db-bindings-for-azure-functions-2x-preview"></a><span data-ttu-id="1be9b-104">Azure Cosmos DB bindings for Azure Functions 2.x (Preview)</span><span class="sxs-lookup"><span data-stu-id="1be9b-104">Azure Cosmos DB bindings for Azure Functions 2.x (Preview)</span></span>

> [!div class="op_single_selector" title1="Select the version of the Azure Functions runtime you are using: "]
> * [Version 1 - GA](functions-bindings-cosmosdb.md)
> * [Version 2 - Preview](functions-bindings-cosmosdb-v2.md)

<span data-ttu-id="1be9b-107">This article explains how to work with [Azure Cosmos DB](..\cosmos-db\serverless-computing-database.md) bindings in Azure Functions 2.x.</span><span class="sxs-lookup"><span data-stu-id="1be9b-107">This article explains how to work with [Azure Cosmos DB](..\cosmos-db\serverless-computing-database.md) bindings in Azure Functions 2.x.</span></span> <span data-ttu-id="1be9b-108">Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1be9b-108">Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.</span></span>

> [!NOTE]
> This article is for [Azure Functions version 2.x](functions-versions.md), which is in Preview.  For information about how to use these bindings in Functions 1.x, see [Azure Cosmos DB bindings for Azure Functions 1.x](functions-bindings-cosmosdb.md).
>
> This binding was originally named DocumentDB. In Functions version 2.x, the trigger, bindings, and package are all named Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-apis"></a><span data-ttu-id="1be9b-113">Supported APIs</span><span class="sxs-lookup"><span data-stu-id="1be9b-113">Supported APIs</span></span>

[!INCLUDE [SQL API support only](../../includes/functions-cosmosdb-sqlapi-note.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="1be9b-114">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="1be9b-114">Packages - Functions 2.x</span></span>

<span data-ttu-id="1be9b-115">The Azure Cosmos DB bindings for Functions version 2.x are provided in the [Microsoft.Azure.WebJobs.Extensions.CosmosDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="1be9b-115">The Azure Cosmos DB bindings for Functions version 2.x are provided in the [Microsoft.Azure.WebJobs.Extensions.CosmosDB](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB) NuGet package, version 3.x.</span></span> <span data-ttu-id="1be9b-116">Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="1be9b-116">Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="trigger"></a><span data-ttu-id="1be9b-117">Trigger</span><span class="sxs-lookup"><span data-stu-id="1be9b-117">Trigger</span></span>

<span data-ttu-id="1be9b-118">The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](../cosmos-db/change-feed.md) to listen for inserts and updates across partitions.</span><span class="sxs-lookup"><span data-stu-id="1be9b-118">The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](../cosmos-db/change-feed.md) to listen for inserts and updates across partitions.</span></span> <span data-ttu-id="1be9b-119">The change feed publishes inserts and updates, not deletions.</span><span class="sxs-lookup"><span data-stu-id="1be9b-119">The change feed publishes inserts and updates, not deletions.</span></span>

## <a name="trigger---example"></a><span data-ttu-id="1be9b-120">Trigger - example</span><span class="sxs-lookup"><span data-stu-id="1be9b-120">Trigger - example</span></span>

<span data-ttu-id="1be9b-121">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="1be9b-121">See the language-specific example:</span></span>

* [<span data-ttu-id="1be9b-122">C#</span><span class="sxs-lookup"><span data-stu-id="1be9b-122">C#</span></span>](#trigger---c-example)
* [<span data-ttu-id="1be9b-123">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="1be9b-123">C# script (.csx)</span></span>](#trigger---c-script-example)
* [<span data-ttu-id="1be9b-124">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1be9b-124">JavaScript</span></span>](#trigger---javascript-example)
* [<span data-ttu-id="1be9b-125">Java</span><span class="sxs-lookup"><span data-stu-id="1be9b-125">Java</span></span>](#trigger---java-example)

[<span data-ttu-id="1be9b-126">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-126">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---c-example"></a><span data-ttu-id="1be9b-127">Trigger - C# example</span><span class="sxs-lookup"><span data-stu-id="1be9b-127">Trigger - C# example</span></span>

<span data-ttu-id="1be9b-128">The following example shows a [C# function](functions-dotnet-class-library.md) that is invoked when there are inserts or updates in the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-128">The following example shows a [C# function](functions-dotnet-class-library.md) that is invoked when there are inserts or updates in the specified database and collection.</span></span>

```cs
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;

namespace CosmosDBSamplesV2
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

[<span data-ttu-id="1be9b-129">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-129">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---c-script-example"></a><span data-ttu-id="1be9b-130">Trigger - C# script example</span><span class="sxs-lookup"><span data-stu-id="1be9b-130">Trigger - C# script example</span></span>

<span data-ttu-id="1be9b-131">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-131">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-132">The function writes log messages when Cosmos DB records are modified.</span><span class="sxs-lookup"><span data-stu-id="1be9b-132">The function writes log messages when Cosmos DB records are modified.</span></span>

<span data-ttu-id="1be9b-133">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-133">Here's the binding data in the *function.json* file:</span></span>

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

<span data-ttu-id="1be9b-134">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-134">Here's the C# script code:</span></span>
 
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

[<span data-ttu-id="1be9b-135">Skip trigger examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-135">Skip trigger examples</span></span>](#trigger---attributes)

### <a name="trigger---javascript-example"></a><span data-ttu-id="1be9b-136">Trigger - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="1be9b-136">Trigger - JavaScript example</span></span>

<span data-ttu-id="1be9b-137">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-137">The following example shows a Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-138">The function writes log messages when Cosmos DB records are modified.</span><span class="sxs-lookup"><span data-stu-id="1be9b-138">The function writes log messages when Cosmos DB records are modified.</span></span>

<span data-ttu-id="1be9b-139">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-139">Here's the binding data in the *function.json* file:</span></span>

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

<span data-ttu-id="1be9b-140">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-140">Here's the JavaScript code:</span></span>

```javascript
    module.exports = function (context, documents) {
      context.log('First document Id modified : ', documents[0].id);

      context.done();
    }
```

### <a name="trigger---java-example"></a><span data-ttu-id="1be9b-141">Trigger - Java example</span><span class="sxs-lookup"><span data-stu-id="1be9b-141">Trigger - Java example</span></span>

<span data-ttu-id="1be9b-142">The following example shows a Cosmos DB trigger binding in *function.json* file and a [Java function](functions-reference-java.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-142">The following example shows a Cosmos DB trigger binding in *function.json* file and a [Java function](functions-reference-java.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-143">The function is involved when there are inserts or updates in the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-143">The function is involved when there are inserts or updates in the specified database and collection.</span></span>

```json
{
    "type": "cosmosDBTrigger",
    "name": "items",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "AzureCosmosDBConnection",
    "databaseName": "ToDoList",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": false
}
```

<span data-ttu-id="1be9b-144">Here's the Java code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-144">Here's the Java code:</span></span>

```java
    @FunctionName("cosmosDBMonitor")
    public void cosmosDbProcessor(
        @CosmosDBTrigger(name = "items",
            databaseName = "ToDoList",
            collectionName = "Items",
            leaseCollectionName = "leases",
            reateLeaseCollectionIfNotExists = true,
            connectionStringSetting = "AzureCosmosDBConnection") String[] items,
            final ExecutionContext context ) {
                context.getLogger().info(items.length + "item(s) is/are changed.");
            }
```


<span data-ttu-id="1be9b-145">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger` annotation on parameters whose value would come from Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1be9b-145">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger` annotation on parameters whose value would come from Cosmos DB.</span></span>  <span data-ttu-id="1be9b-146">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span><span class="sxs-lookup"><span data-stu-id="1be9b-146">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span></span> 

## <a name="trigger---c-attributes"></a><span data-ttu-id="1be9b-147">Trigger - C# attributes</span><span class="sxs-lookup"><span data-stu-id="1be9b-147">Trigger - C# attributes</span></span>

<span data-ttu-id="1be9b-148">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-148">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.</span></span>

<span data-ttu-id="1be9b-149">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="1be9b-149">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="1be9b-150">For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration).</span><span class="sxs-lookup"><span data-stu-id="1be9b-150">For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration).</span></span> <span data-ttu-id="1be9b-151">Here's a `CosmosDBTrigger` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="1be9b-151">Here's a `CosmosDBTrigger` attribute example in a method signature:</span></span>

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

<span data-ttu-id="1be9b-152">For a complete example, see [Trigger - C# example](#trigger---c-example).</span><span class="sxs-lookup"><span data-stu-id="1be9b-152">For a complete example, see [Trigger - C# example](#trigger---c-example).</span></span>


## <a name="trigger---configuration"></a><span data-ttu-id="1be9b-153">Trigger - configuration</span><span class="sxs-lookup"><span data-stu-id="1be9b-153">Trigger - configuration</span></span>

<span data-ttu-id="1be9b-154">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-154">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger` attribute.</span></span>

|<span data-ttu-id="1be9b-155">function.json property</span><span class="sxs-lookup"><span data-stu-id="1be9b-155">function.json property</span></span> | <span data-ttu-id="1be9b-156">Attribute property</span><span class="sxs-lookup"><span data-stu-id="1be9b-156">Attribute property</span></span> |<span data-ttu-id="1be9b-157">Description</span><span class="sxs-lookup"><span data-stu-id="1be9b-157">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="1be9b-158">**type**</span><span class="sxs-lookup"><span data-stu-id="1be9b-158">**type**</span></span> || <span data-ttu-id="1be9b-159">Must be set to `cosmosDBTrigger`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-159">Must be set to `cosmosDBTrigger`.</span></span> |
|<span data-ttu-id="1be9b-160">**direction**</span><span class="sxs-lookup"><span data-stu-id="1be9b-160">**direction**</span></span> || <span data-ttu-id="1be9b-161">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-161">Must be set to `in`.</span></span> <span data-ttu-id="1be9b-162">This parameter is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1be9b-162">This parameter is set automatically when you create the trigger in the Azure portal.</span></span> |
|<span data-ttu-id="1be9b-163">**name**</span><span class="sxs-lookup"><span data-stu-id="1be9b-163">**name**</span></span> || <span data-ttu-id="1be9b-164">The variable name used in function code that represents the list of documents with changes.</span><span class="sxs-lookup"><span data-stu-id="1be9b-164">The variable name used in function code that represents the list of documents with changes.</span></span> | 
|<span data-ttu-id="1be9b-165">**connectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-165">**connectionStringSetting**</span></span>|<span data-ttu-id="1be9b-166">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-166">**ConnectionStringSetting**</span></span> | <span data-ttu-id="1be9b-167">The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored.</span><span class="sxs-lookup"><span data-stu-id="1be9b-167">The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored.</span></span> |
|<span data-ttu-id="1be9b-168">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-168">**databaseName**</span></span>|<span data-ttu-id="1be9b-169">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-169">**DatabaseName**</span></span>  | <span data-ttu-id="1be9b-170">The name of the Azure Cosmos DB database with the collection being monitored.</span><span class="sxs-lookup"><span data-stu-id="1be9b-170">The name of the Azure Cosmos DB database with the collection being monitored.</span></span> |
|<span data-ttu-id="1be9b-171">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-171">**collectionName**</span></span> |<span data-ttu-id="1be9b-172">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-172">**CollectionName**</span></span> | <span data-ttu-id="1be9b-173">The name of the collection being monitored.</span><span class="sxs-lookup"><span data-stu-id="1be9b-173">The name of the collection being monitored.</span></span> |
|<span data-ttu-id="1be9b-174">**leaseConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-174">**leaseConnectionStringSetting**</span></span> | <span data-ttu-id="1be9b-175">**LeaseConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-175">**LeaseConnectionStringSetting**</span></span> | <span data-ttu-id="1be9b-176">(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-176">(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection.</span></span> <span data-ttu-id="1be9b-177">When not set, the `connectionStringSetting` value is used.</span><span class="sxs-lookup"><span data-stu-id="1be9b-177">When not set, the `connectionStringSetting` value is used.</span></span> <span data-ttu-id="1be9b-178">This parameter is automatically set when the binding is created in the portal.</span><span class="sxs-lookup"><span data-stu-id="1be9b-178">This parameter is automatically set when the binding is created in the portal.</span></span> <span data-ttu-id="1be9b-179">The connection string for the leases collection must have write permissions.</span><span class="sxs-lookup"><span data-stu-id="1be9b-179">The connection string for the leases collection must have write permissions.</span></span>|
|<span data-ttu-id="1be9b-180">**leaseDatabaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-180">**leaseDatabaseName**</span></span> |<span data-ttu-id="1be9b-181">**LeaseDatabaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-181">**LeaseDatabaseName**</span></span> | <span data-ttu-id="1be9b-182">(Optional) The name of the database that holds the collection used to store leases.</span><span class="sxs-lookup"><span data-stu-id="1be9b-182">(Optional) The name of the database that holds the collection used to store leases.</span></span> <span data-ttu-id="1be9b-183">When not set, the value of the `databaseName` setting is used.</span><span class="sxs-lookup"><span data-stu-id="1be9b-183">When not set, the value of the `databaseName` setting is used.</span></span> <span data-ttu-id="1be9b-184">This parameter is automatically set when the binding is created in the portal.</span><span class="sxs-lookup"><span data-stu-id="1be9b-184">This parameter is automatically set when the binding is created in the portal.</span></span> |
|<span data-ttu-id="1be9b-185">**leaseCollectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-185">**leaseCollectionName**</span></span> | <span data-ttu-id="1be9b-186">**LeaseCollectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-186">**LeaseCollectionName**</span></span> | <span data-ttu-id="1be9b-187">(Optional) The name of the collection used to store leases.</span><span class="sxs-lookup"><span data-stu-id="1be9b-187">(Optional) The name of the collection used to store leases.</span></span> <span data-ttu-id="1be9b-188">When not set, the value `leases` is used.</span><span class="sxs-lookup"><span data-stu-id="1be9b-188">When not set, the value `leases` is used.</span></span> |
|<span data-ttu-id="1be9b-189">**createLeaseCollectionIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="1be9b-189">**createLeaseCollectionIfNotExists**</span></span> | <span data-ttu-id="1be9b-190">**CreateLeaseCollectionIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="1be9b-190">**CreateLeaseCollectionIfNotExists**</span></span> | <span data-ttu-id="1be9b-191">(Optional) When set to `true`, the leases collection is automatically created when it doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="1be9b-191">(Optional) When set to `true`, the leases collection is automatically created when it doesn't already exist.</span></span> <span data-ttu-id="1be9b-192">The default value is `false`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-192">The default value is `false`.</span></span> |
|<span data-ttu-id="1be9b-193">**leasesCollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="1be9b-193">**leasesCollectionThroughput**</span></span>| <span data-ttu-id="1be9b-194">**LeasesCollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="1be9b-194">**LeasesCollectionThroughput**</span></span>| <span data-ttu-id="1be9b-195">(Optional) Defines the amount of Request Units to assign when the leases collection is created.</span><span class="sxs-lookup"><span data-stu-id="1be9b-195">(Optional) Defines the amount of Request Units to assign when the leases collection is created.</span></span> <span data-ttu-id="1be9b-196">This setting is only used When `createLeaseCollectionIfNotExists` is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-196">This setting is only used When `createLeaseCollectionIfNotExists` is set to `true`.</span></span> <span data-ttu-id="1be9b-197">This parameter is  automatically set when the binding is created using the portal.</span><span class="sxs-lookup"><span data-stu-id="1be9b-197">This parameter is  automatically set when the binding is created using the portal.</span></span>
|<span data-ttu-id="1be9b-198">**leaseCollectionPrefix**</span><span class="sxs-lookup"><span data-stu-id="1be9b-198">**leaseCollectionPrefix**</span></span>| <span data-ttu-id="1be9b-199">**LeaseCollectionPrefix**</span><span class="sxs-lookup"><span data-stu-id="1be9b-199">**LeaseCollectionPrefix**</span></span>| <span data-ttu-id="1be9b-200">(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes.</span><span class="sxs-lookup"><span data-stu-id="1be9b-200">(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes.</span></span>
|<span data-ttu-id="1be9b-201">**feedPollDelay**</span><span class="sxs-lookup"><span data-stu-id="1be9b-201">**feedPollDelay**</span></span>| <span data-ttu-id="1be9b-202">**FeedPollDelay**</span><span class="sxs-lookup"><span data-stu-id="1be9b-202">**FeedPollDelay**</span></span>| <span data-ttu-id="1be9b-203">(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained.</span><span class="sxs-lookup"><span data-stu-id="1be9b-203">(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained.</span></span> <span data-ttu-id="1be9b-204">Default is 5000 (5 seconds).</span><span class="sxs-lookup"><span data-stu-id="1be9b-204">Default is 5000 (5 seconds).</span></span>
|<span data-ttu-id="1be9b-205">**leaseAcquireInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-205">**leaseAcquireInterval**</span></span>| <span data-ttu-id="1be9b-206">**LeaseAcquireInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-206">**LeaseAcquireInterval**</span></span>| <span data-ttu-id="1be9b-207">(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances.</span><span class="sxs-lookup"><span data-stu-id="1be9b-207">(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances.</span></span> <span data-ttu-id="1be9b-208">Default is 13000 (13 seconds).</span><span class="sxs-lookup"><span data-stu-id="1be9b-208">Default is 13000 (13 seconds).</span></span>
|<span data-ttu-id="1be9b-209">**leaseExpirationInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-209">**leaseExpirationInterval**</span></span>| <span data-ttu-id="1be9b-210">**LeaseExpirationInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-210">**LeaseExpirationInterval**</span></span>| <span data-ttu-id="1be9b-211">(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition.</span><span class="sxs-lookup"><span data-stu-id="1be9b-211">(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="1be9b-212">If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance.</span><span class="sxs-lookup"><span data-stu-id="1be9b-212">If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance.</span></span> <span data-ttu-id="1be9b-213">Default is 60000 (60 seconds).</span><span class="sxs-lookup"><span data-stu-id="1be9b-213">Default is 60000 (60 seconds).</span></span>
|<span data-ttu-id="1be9b-214">**leaseRenewInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-214">**leaseRenewInterval**</span></span>| <span data-ttu-id="1be9b-215">**LeaseRenewInterval**</span><span class="sxs-lookup"><span data-stu-id="1be9b-215">**LeaseRenewInterval**</span></span>| <span data-ttu-id="1be9b-216">(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance.</span><span class="sxs-lookup"><span data-stu-id="1be9b-216">(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance.</span></span> <span data-ttu-id="1be9b-217">Default is 17000 (17 seconds).</span><span class="sxs-lookup"><span data-stu-id="1be9b-217">Default is 17000 (17 seconds).</span></span>
|<span data-ttu-id="1be9b-218">**checkpointFrequency**</span><span class="sxs-lookup"><span data-stu-id="1be9b-218">**checkpointFrequency**</span></span>| <span data-ttu-id="1be9b-219">**CheckpointFrequency**</span><span class="sxs-lookup"><span data-stu-id="1be9b-219">**CheckpointFrequency**</span></span>| <span data-ttu-id="1be9b-220">(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints.</span><span class="sxs-lookup"><span data-stu-id="1be9b-220">(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints.</span></span> <span data-ttu-id="1be9b-221">Default is always after a successful Function call.</span><span class="sxs-lookup"><span data-stu-id="1be9b-221">Default is always after a successful Function call.</span></span>
|<span data-ttu-id="1be9b-222">**maxItemsPerInvocation**</span><span class="sxs-lookup"><span data-stu-id="1be9b-222">**maxItemsPerInvocation**</span></span>| <span data-ttu-id="1be9b-223">**MaxItemsPerInvocation**</span><span class="sxs-lookup"><span data-stu-id="1be9b-223">**MaxItemsPerInvocation**</span></span>| <span data-ttu-id="1be9b-224">(Optional) When set, it customizes the maximum amount of items received per Function call.</span><span class="sxs-lookup"><span data-stu-id="1be9b-224">(Optional) When set, it customizes the maximum amount of items received per Function call.</span></span>

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a><span data-ttu-id="1be9b-225">Trigger - usage</span><span class="sxs-lookup"><span data-stu-id="1be9b-225">Trigger - usage</span></span>

<span data-ttu-id="1be9b-226">The trigger requires a second collection that it uses to store _leases_ over the partitions.</span><span class="sxs-lookup"><span data-stu-id="1be9b-226">The trigger requires a second collection that it uses to store _leases_ over the partitions.</span></span> <span data-ttu-id="1be9b-227">Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.</span><span class="sxs-lookup"><span data-stu-id="1be9b-227">Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.</span></span>

>[!IMPORTANT]
> If multiple functions are configured to use a Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix` for each function. Otherwise, only one of the functions will be triggered. For information about the prefix, see the [Configuration section](#trigger---configuration).

<span data-ttu-id="1be9b-231">The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself.</span><span class="sxs-lookup"><span data-stu-id="1be9b-231">The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself.</span></span> <span data-ttu-id="1be9b-232">If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.</span><span class="sxs-lookup"><span data-stu-id="1be9b-232">If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.</span></span>

## <a name="input"></a><span data-ttu-id="1be9b-233">Input</span><span class="sxs-lookup"><span data-stu-id="1be9b-233">Input</span></span>

<span data-ttu-id="1be9b-234">The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function.</span><span class="sxs-lookup"><span data-stu-id="1be9b-234">The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function.</span></span> <span data-ttu-id="1be9b-235">The document ID or query parameters can be determined based on the trigger that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="1be9b-235">The document ID or query parameters can be determined based on the trigger that invokes the function.</span></span> 

## <a name="input---examples"></a><span data-ttu-id="1be9b-236">Input - examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-236">Input - examples</span></span>

<span data-ttu-id="1be9b-237">See the language-specific examples that read a single document by specifying an ID value:</span><span class="sxs-lookup"><span data-stu-id="1be9b-237">See the language-specific examples that read a single document by specifying an ID value:</span></span>

* [<span data-ttu-id="1be9b-238">C#</span><span class="sxs-lookup"><span data-stu-id="1be9b-238">C#</span></span>](#input---c-examples)
* [<span data-ttu-id="1be9b-239">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="1be9b-239">C# script (.csx)</span></span>](#input---c-script-examples)
* [<span data-ttu-id="1be9b-240">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1be9b-240">JavaScript</span></span>](#input---javascript-examples)
* [<span data-ttu-id="1be9b-241">F#</span><span class="sxs-lookup"><span data-stu-id="1be9b-241">F#</span></span>](#input---f-examples)
* [<span data-ttu-id="1be9b-242">Java</span><span class="sxs-lookup"><span data-stu-id="1be9b-242">Java</span></span>](#input---java-examples)

[<span data-ttu-id="1be9b-243">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-243">Skip input examples</span></span>](#input---attributes)

### <a name="input---c-examples"></a><span data-ttu-id="1be9b-244">Input - C# examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-244">Input - C# examples</span></span>

<span data-ttu-id="1be9b-245">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="1be9b-245">This section contains the following examples:</span></span>

* [<span data-ttu-id="1be9b-246">Queue trigger, look up ID from JSON</span><span class="sxs-lookup"><span data-stu-id="1be9b-246">Queue trigger, look up ID from JSON</span></span>](#queue-trigger-look-up-id-from-json-c)
* [<span data-ttu-id="1be9b-247">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="1be9b-247">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-c)
* [<span data-ttu-id="1be9b-248">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="1be9b-248">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-c)
* [<span data-ttu-id="1be9b-249">HTTP trigger, look up ID from route data, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="1be9b-249">HTTP trigger, look up ID from route data, using SqlQuery</span></span>](#http-trigger-look-up-id-from-route-data-using-sqlquery-c)
* [<span data-ttu-id="1be9b-250">HTTP trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="1be9b-250">HTTP trigger, get multiple docs, using SqlQuery</span></span>](#http-trigger-get-multiple-docs-using-sqlquery-c)
* [<span data-ttu-id="1be9b-251">HTTP trigger, get multiple docs, using DocumentClient</span><span class="sxs-lookup"><span data-stu-id="1be9b-251">HTTP trigger, get multiple docs, using DocumentClient</span></span>](#http-trigger-get-multiple-docs-using-documentclient-c)

<span data-ttu-id="1be9b-252">The examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="1be9b-252">The examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV2
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="1be9b-253">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-253">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-json-c"></a><span data-ttu-id="1be9b-254">Queue trigger, look up ID from JSON (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-254">Queue trigger, look up ID from JSON (C#)</span></span>

<span data-ttu-id="1be9b-255">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-255">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-256">The function is triggered by a queue message that contains a JSON object.</span><span class="sxs-lookup"><span data-stu-id="1be9b-256">The function is triggered by a queue message that contains a JSON object.</span></span> <span data-ttu-id="1be9b-257">The queue trigger parses the JSON into an object named `ToDoItemLookup`, which contains the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-257">The queue trigger parses the JSON into an object named `ToDoItemLookup`, which contains the ID to look up.</span></span> <span data-ttu-id="1be9b-258">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-258">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
namespace CosmosDBSamplesV2
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

namespace CosmosDBSamplesV2
{
    public static class DocByIdFromJSON
    {
        [FunctionName("DocByIdFromJSON")]
        public static void Run(
            [QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
            [CosmosDB(
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

[<span data-ttu-id="1be9b-259">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-259">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-c"></a><span data-ttu-id="1be9b-260">HTTP trigger, look up ID from query string (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-260">HTTP trigger, look up ID from query string (C#)</span></span>

<span data-ttu-id="1be9b-261">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-261">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-262">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-262">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-263">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-263">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;

namespace CosmosDBSamplesV2
{
    public static class DocByIdFromQueryString
    {
        [FunctionName("DocByIdFromQueryString")]
        public static IActionResult Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
                HttpRequest req,
            [CosmosDB(
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
            return new OkResult();
        }
    }
}
```

[<span data-ttu-id="1be9b-264">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-264">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-c"></a><span data-ttu-id="1be9b-265">HTTP trigger, look up ID from route data (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-265">HTTP trigger, look up ID from route data (C#)</span></span>

<span data-ttu-id="1be9b-266">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-266">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-267">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-267">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-268">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-268">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;

namespace CosmosDBSamplesV2
{
    public static class DocByIdFromRouteData
    {
        [FunctionName("DocByIdFromRouteData")]
        public static IActionResult Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", 
                Route = "todoitems/{id}")]HttpRequest req,
            [CosmosDB(
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
            return new OkResult();
        }
    }
}
```

[<span data-ttu-id="1be9b-269">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-269">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-using-sqlquery-c"></a><span data-ttu-id="1be9b-270">HTTP trigger, look up ID from route data, using SqlQuery (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-270">HTTP trigger, look up ID from route data, using SqlQuery (C#)</span></span>

<span data-ttu-id="1be9b-271">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-271">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-272">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-272">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-273">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-273">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span> 

<span data-ttu-id="1be9b-274">The example shows how to use a binding expression in the `SqlQuery` parameter.</span><span class="sxs-lookup"><span data-stu-id="1be9b-274">The example shows how to use a binding expression in the `SqlQuery` parameter.</span></span> <span data-ttu-id="1be9b-275">You can pass route data to the `SqlQuery` parameter as shown, but currently [you can't pass query string values](https://github.com/Azure/azure-functions-host/issues/2554#issuecomment-392084583).</span><span class="sxs-lookup"><span data-stu-id="1be9b-275">You can pass route data to the `SqlQuery` parameter as shown, but currently [you can't pass query string values](https://github.com/Azure/azure-functions-host/issues/2554#issuecomment-392084583).</span></span>


```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;

namespace CosmosDBSamplesV2
{
    public static class DocByIdFromRouteDataUsingSqlQuery
    {
        [FunctionName("DocByIdFromRouteDataUsingSqlQuery")]
        public static IActionResult Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", 
                Route = "todoitems2/{id}")]HttpRequest req,
            [CosmosDB("ToDoItems", "Items", 
                ConnectionStringSetting = "CosmosDBConnection", 
                SqlQuery = "select * from ToDoItems r where r.id = {id}")]
                IEnumerable<ToDoItem> toDoItems,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");

            foreach (ToDoItem toDoItem in toDoItems)
            {
                log.Info(toDoItem.Description);
            }
            return new OkResult();
        }
    }
}
```

[<span data-ttu-id="1be9b-276">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-276">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-sqlquery-c"></a><span data-ttu-id="1be9b-277">HTTP trigger, get multiple docs, using SqlQuery (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-277">HTTP trigger, get multiple docs, using SqlQuery (C#)</span></span>

<span data-ttu-id="1be9b-278">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-278">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span></span> <span data-ttu-id="1be9b-279">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1be9b-279">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="1be9b-280">The query is specified in the `SqlQuery` attribute property.</span><span class="sxs-lookup"><span data-stu-id="1be9b-280">The query is specified in the `SqlQuery` attribute property.</span></span>

```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;

namespace CosmosDBSamplesV2
{
    public static class DocsBySqlQuery
    {
        [FunctionName("DocsBySqlQuery")]
        public static IActionResult Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
                HttpRequest req,
            [CosmosDB(
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
            return new OkResult();
        }
    }
}

```

[<span data-ttu-id="1be9b-281">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-281">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-documentclient-c"></a><span data-ttu-id="1be9b-282">HTTP trigger, get multiple docs, using DocumentClient (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-282">HTTP trigger, get multiple docs, using DocumentClient (C#)</span></span>

<span data-ttu-id="1be9b-283">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-283">The following example shows a [C# function](functions-dotnet-class-library.md) that retrieves a list of documents.</span></span> <span data-ttu-id="1be9b-284">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1be9b-284">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="1be9b-285">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-285">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span></span> <span data-ttu-id="1be9b-286">The `DocumentClient` instance could also be used for write operations.</span><span class="sxs-lookup"><span data-stu-id="1be9b-286">The `DocumentClient` instance could also be used for write operations.</span></span>

```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System;
using System.Linq;
using System.Threading.Tasks;

namespace CosmosDBSamplesV2
{
    public static class DocsByUsingDocumentClient
    {
        [FunctionName("DocsByUsingDocumentClient")]
        public static async Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", 
                Route = null)]HttpRequest req,
            [CosmosDB(
                databaseName: "ToDoItems",
                collectionName: "Items",
                ConnectionStringSetting = "CosmosDBConnection")] DocumentClient client,
            TraceWriter log)
        {
            log.Info("C# HTTP trigger function processed a request.");

            var searchterm = req.Query["searchterm"];
            if (string.IsNullOrWhiteSpace(searchterm))
            {
                return (ActionResult)new NotFoundResult();
            }

            Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");

            log.Info($"Searching for: {searchterm}");

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
            return new OkResult();
        }
    }
}
```

[<span data-ttu-id="1be9b-287">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-287">Skip input examples</span></span>](#input---attributes)

### <a name="input---c-script-examples"></a><span data-ttu-id="1be9b-288">Input - C# script examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-288">Input - C# script examples</span></span>

<span data-ttu-id="1be9b-289">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="1be9b-289">This section contains the following examples:</span></span>

* [<span data-ttu-id="1be9b-290">Queue trigger, look up ID from string</span><span class="sxs-lookup"><span data-stu-id="1be9b-290">Queue trigger, look up ID from string</span></span>](#queue-trigger-look-up-id-from-string-c-script)
* [<span data-ttu-id="1be9b-291">Queue trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="1be9b-291">Queue trigger, get multiple docs, using SqlQuery</span></span>](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)
* [<span data-ttu-id="1be9b-292">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="1be9b-292">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-c-script)
* [<span data-ttu-id="1be9b-293">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="1be9b-293">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-c-script)
* [<span data-ttu-id="1be9b-294">HTTP trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="1be9b-294">HTTP trigger, get multiple docs, using SqlQuery</span></span>](#http-trigger-get-multiple-docs-using-sqlquery-c-script)
* [<span data-ttu-id="1be9b-295">HTTP trigger, get multiple docs, using DocumentClient</span><span class="sxs-lookup"><span data-stu-id="1be9b-295">HTTP trigger, get multiple docs, using DocumentClient</span></span>](#http-trigger-get-multiple-docs-using-documentclient-c-script)

<span data-ttu-id="1be9b-296">The HTTP trigger examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="1be9b-296">The HTTP trigger examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV2
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="1be9b-297">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-297">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-string-c-script"></a><span data-ttu-id="1be9b-298">Queue trigger, look up ID from string (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-298">Queue trigger, look up ID from string (C# script)</span></span>

<span data-ttu-id="1be9b-299">The following example shows a Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-299">The following example shows a Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-300">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="1be9b-300">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="1be9b-301">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-301">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocument",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "partitionKey": "{partition key value}",
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```
<span data-ttu-id="1be9b-302">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-302">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-303">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-303">Here's the C# script code:</span></span>

```cs
    using System;

    // Change input document contents using Azure Cosmos DB input binding 
    public static void Run(string myQueueItem, dynamic inputDocument)
    {   
      inputDocument.text = "This has changed.";
    }
```

[<span data-ttu-id="1be9b-304">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-304">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-get-multiple-docs-using-sqlquery-c-script"></a><span data-ttu-id="1be9b-305">Queue trigger, get multiple docs, using SqlQuery (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-305">Queue trigger, get multiple docs, using SqlQuery (C# script)</span></span>

<span data-ttu-id="1be9b-306">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-306">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-307">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span><span class="sxs-lookup"><span data-stu-id="1be9b-307">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span>

<span data-ttu-id="1be9b-308">The queue trigger provides a parameter `departmentId`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-308">The queue trigger provides a parameter `departmentId`.</span></span> <span data-ttu-id="1be9b-309">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span><span class="sxs-lookup"><span data-stu-id="1be9b-309">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> 

<span data-ttu-id="1be9b-310">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-310">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "documents",
    "type": "cosmosDB",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connectionStringSetting": "CosmosDBConnection"
}
```

<span data-ttu-id="1be9b-311">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-311">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-312">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-312">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-313">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-313">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-c-script"></a><span data-ttu-id="1be9b-314">HTTP trigger, look up ID from query string (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-314">HTTP trigger, look up ID from query string (C# script)</span></span>

<span data-ttu-id="1be9b-315">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-315">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-316">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-316">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-317">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-317">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="1be9b-318">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-318">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "in",
      "Id": "{Query.id}"
    }
  ],
  "disabled": true
}
```

<span data-ttu-id="1be9b-319">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-319">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-320">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-320">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-c-script"></a><span data-ttu-id="1be9b-321">HTTP trigger, look up ID from route data (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-321">HTTP trigger, look up ID from route data (C# script)</span></span>

<span data-ttu-id="1be9b-322">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-322">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-323">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-323">The function is triggered by an HTTP request that uses route data to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-324">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-324">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="1be9b-325">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-325">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "in",
      "Id": "{id}"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="1be9b-326">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-326">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-327">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-327">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-sqlquery-c-script"></a><span data-ttu-id="1be9b-328">HTTP trigger, get multiple docs, using SqlQuery (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-328">HTTP trigger, get multiple docs, using SqlQuery (C# script)</span></span>

<span data-ttu-id="1be9b-329">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-329">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span></span> <span data-ttu-id="1be9b-330">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1be9b-330">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="1be9b-331">The query is specified in the `SqlQuery` attribute property.</span><span class="sxs-lookup"><span data-stu-id="1be9b-331">The query is specified in the `SqlQuery` attribute property.</span></span>

<span data-ttu-id="1be9b-332">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-332">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
      "name": "toDoItems",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "in",
      "sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="1be9b-333">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-333">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-334">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-334">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-get-multiple-docs-using-documentclient-c-script"></a><span data-ttu-id="1be9b-335">HTTP trigger, get multiple docs, using DocumentClient (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-335">HTTP trigger, get multiple docs, using DocumentClient (C# script)</span></span>

<span data-ttu-id="1be9b-336">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-336">The following example shows a [C# script function](functions-reference-csharp.md) that retrieves a list of documents.</span></span> <span data-ttu-id="1be9b-337">The function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1be9b-337">The function is triggered by an HTTP request.</span></span> <span data-ttu-id="1be9b-338">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-338">The code uses a `DocumentClient` instance provided by the Azure Cosmos DB binding to read a list of documents.</span></span> <span data-ttu-id="1be9b-339">The `DocumentClient` instance could also be used for write operations.</span><span class="sxs-lookup"><span data-stu-id="1be9b-339">The `DocumentClient` instance could also be used for write operations.</span></span>

<span data-ttu-id="1be9b-340">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-340">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
      "name": "client",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "inout"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="1be9b-341">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-341">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-342">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-342">Skip input examples</span></span>](#input---attributes)

### <a name="input---javascript-examples"></a><span data-ttu-id="1be9b-343">Input - JavaScript examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-343">Input - JavaScript examples</span></span>

<span data-ttu-id="1be9b-344">This section contains the following examples that read a single document by specifying an ID value from various sources:</span><span class="sxs-lookup"><span data-stu-id="1be9b-344">This section contains the following examples that read a single document by specifying an ID value from various sources:</span></span>

* [<span data-ttu-id="1be9b-345">Queue trigger, look up ID from JSON</span><span class="sxs-lookup"><span data-stu-id="1be9b-345">Queue trigger, look up ID from JSON</span></span>](#queue-trigger-look-up-id-from-string-javascript)
* [<span data-ttu-id="1be9b-346">HTTP trigger, look up ID from query string</span><span class="sxs-lookup"><span data-stu-id="1be9b-346">HTTP trigger, look up ID from query string</span></span>](#http-trigger-look-up-id-from-query-string-javascript)
* [<span data-ttu-id="1be9b-347">HTTP trigger, look up ID from route data</span><span class="sxs-lookup"><span data-stu-id="1be9b-347">HTTP trigger, look up ID from route data</span></span>](#http-trigger-look-up-id-from-route-data-javascript)
* [<span data-ttu-id="1be9b-348">Queue trigger, get multiple docs, using SqlQuery</span><span class="sxs-lookup"><span data-stu-id="1be9b-348">Queue trigger, get multiple docs, using SqlQuery</span></span>](#queue-trigger-get-multiple-docs-using-sqlquery-javascript)

[<span data-ttu-id="1be9b-349">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-349">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-look-up-id-from-json-javascript"></a><span data-ttu-id="1be9b-350">Queue trigger, look up ID from JSON (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1be9b-350">Queue trigger, look up ID from JSON (JavaScript)</span></span>

<span data-ttu-id="1be9b-351">The following example shows a Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-351">The following example shows a Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-352">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="1be9b-352">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="1be9b-353">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-353">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocumentIn",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger_payload_property}",
    "partitionKey": "{queueTrigger_payload_property}",
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "in"
},
{
    "name": "inputDocumentOut",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": false,
    "partitionKey": "{queueTrigger_payload_property}",
    "connectionStringSetting": "MyAccount_COSMOSDB",
    "direction": "out"
}
```
<span data-ttu-id="1be9b-354">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-354">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-355">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-355">Here's the JavaScript code:</span></span>

```javascript
    // Change input document contents using Azure Cosmos DB input binding, using context.bindings.inputDocumentOut
    module.exports = function (context) {   
    context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
    context.bindings.inputDocumentOut.text = "This was updated!";
    context.done();
    };
```

[<span data-ttu-id="1be9b-356">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-356">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-query-string-javascript"></a><span data-ttu-id="1be9b-357">HTTP trigger, look up ID from query string (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1be9b-357">HTTP trigger, look up ID from query string (JavaScript)</span></span>

<span data-ttu-id="1be9b-358">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-358">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-359">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-359">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-360">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-360">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="1be9b-361">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-361">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
      "name": "toDoItem",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "in",
      "Id": "{Query.id}"
    }
  ],
  "disabled": true
}
```

<span data-ttu-id="1be9b-362">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-362">Here's the JavaScript code:</span></span>

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

[<span data-ttu-id="1be9b-363">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-363">Skip input examples</span></span>](#input---attributes)

#### <a name="http-trigger-look-up-id-from-route-data-javascript"></a><span data-ttu-id="1be9b-364">HTTP trigger, look up ID from route data (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1be9b-364">HTTP trigger, look up ID from route data (JavaScript)</span></span>

<span data-ttu-id="1be9b-365">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-365">The following example shows a [JavaScript function](functions-reference-node.md) that retrieves a single document.</span></span> <span data-ttu-id="1be9b-366">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-366">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-367">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-367">That ID is used to retrieve a `ToDoItem` document from the specified database and collection.</span></span>

<span data-ttu-id="1be9b-368">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-368">Here's the *function.json* file:</span></span>

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
      "type": "cosmosDB",
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

<span data-ttu-id="1be9b-369">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-369">Here's the JavaScript code:</span></span>

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

[<span data-ttu-id="1be9b-370">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-370">Skip input examples</span></span>](#input---attributes)

#### <a name="queue-trigger-get-multiple-docs-using-sqlquery-javascript"></a><span data-ttu-id="1be9b-371">Queue trigger, get multiple docs, using SqlQuery (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1be9b-371">Queue trigger, get multiple docs, using SqlQuery (JavaScript)</span></span>

<span data-ttu-id="1be9b-372">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-372">The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-373">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span><span class="sxs-lookup"><span data-stu-id="1be9b-373">The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span>

<span data-ttu-id="1be9b-374">The queue trigger provides a parameter `departmentId`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-374">The queue trigger provides a parameter `departmentId`.</span></span> <span data-ttu-id="1be9b-375">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span><span class="sxs-lookup"><span data-stu-id="1be9b-375">A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> 

<span data-ttu-id="1be9b-376">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-376">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "documents",
    "type": "cosmosDB",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
    "connectionStringSetting": "CosmosDBConnection"
}
```

<span data-ttu-id="1be9b-377">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-377">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-378">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-378">Here's the JavaScript code:</span></span>

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

[<span data-ttu-id="1be9b-379">Skip input examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-379">Skip input examples</span></span>](#input---attributes)

<a name="infsharp"></a>

### <a name="input---f-examples"></a><span data-ttu-id="1be9b-380">Input - F# examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-380">Input - F# examples</span></span>

<span data-ttu-id="1be9b-381">The following example shows a Cosmos DB input binding in a *function.json* file and a [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-381">The following example shows a Cosmos DB input binding in a *function.json* file and a [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-382">The function reads a single document and updates the document's text value.</span><span class="sxs-lookup"><span data-stu-id="1be9b-382">The function reads a single document and updates the document's text value.</span></span>

<span data-ttu-id="1be9b-383">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-383">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "inputDocument",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger}",
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "in"
}
```

<span data-ttu-id="1be9b-384">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-384">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-385">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-385">Here's the F# code:</span></span>

```fsharp
    (* Change input document contents using Azure Cosmos DB input binding *)
    open FSharp.Interop.Dynamic
    let Run(myQueueItem: string, inputDocument: obj) =
    inputDocument?text <- "This has changed."
```

<span data-ttu-id="1be9b-386">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="1be9b-386">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="1be9b-387">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="1be9b-387">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

### <a name="input---java-examples"></a><span data-ttu-id="1be9b-388">Input - Java examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-388">Input - Java examples</span></span>

<span data-ttu-id="1be9b-389">The following example shows a Java function that retrieves a single document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-389">The following example shows a Java function that retrieves a single document.</span></span> <span data-ttu-id="1be9b-390">The function is triggered by a HTTP request that uses a query string to specify the ID to look up.</span><span class="sxs-lookup"><span data-stu-id="1be9b-390">The function is triggered by a HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="1be9b-391">That ID is used to retrieve a ToDoItem document from the specified database and collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-391">That ID is used to retrieve a ToDoItem document from the specified database and collection.</span></span>

<span data-ttu-id="1be9b-392">Here's the Java code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-392">Here's the Java code:</span></span>

```java
@FunctionName("getItem")
public String cosmosDbQueryById(
    @HttpTrigger(name = "req",
                  methods = {HttpMethod.GET},
                  authLevel = AuthorizationLevel.ANONYMOUS) Optional<String> dummy,
    @CosmosDBInput(name = "database",
                      databaseName = "ToDoList",
                      collectionName = "Items",
                      leaseCollectionName = "",
                      id = "{Query.id}"
                      connectionStringSetting = "AzureCosmosDBConnection") Optional<String> item,
    final ExecutionContext context
 ) {
    return item.orElse("Not found");
 }
 ```

<span data-ttu-id="1be9b-393">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput` annotation on function parameters whose value would come from Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1be9b-393">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput` annotation on function parameters whose value would come from Cosmos DB.</span></span>  <span data-ttu-id="1be9b-394">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span><span class="sxs-lookup"><span data-stu-id="1be9b-394">This annotation can be used with native Java types, POJOs, or nullable values using Optional<T>.</span></span> 

## <a name="input---attributes"></a><span data-ttu-id="1be9b-395">Input - attributes</span><span class="sxs-lookup"><span data-stu-id="1be9b-395">Input - attributes</span></span>

<span data-ttu-id="1be9b-396">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-396">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) attribute.</span></span>

<span data-ttu-id="1be9b-397">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="1be9b-397">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="1be9b-398">For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).</span><span class="sxs-lookup"><span data-stu-id="1be9b-398">For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).</span></span> 

## <a name="input---configuration"></a><span data-ttu-id="1be9b-399">Input - configuration</span><span class="sxs-lookup"><span data-stu-id="1be9b-399">Input - configuration</span></span>

<span data-ttu-id="1be9b-400">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDB` attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-400">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDB` attribute.</span></span>

|<span data-ttu-id="1be9b-401">function.json property</span><span class="sxs-lookup"><span data-stu-id="1be9b-401">function.json property</span></span> | <span data-ttu-id="1be9b-402">Attribute property</span><span class="sxs-lookup"><span data-stu-id="1be9b-402">Attribute property</span></span> |<span data-ttu-id="1be9b-403">Description</span><span class="sxs-lookup"><span data-stu-id="1be9b-403">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="1be9b-404">**type**</span><span class="sxs-lookup"><span data-stu-id="1be9b-404">**type**</span></span>     || <span data-ttu-id="1be9b-405">Must be set to `cosmosDB`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-405">Must be set to `cosmosDB`.</span></span>        |
|<span data-ttu-id="1be9b-406">**direction**</span><span class="sxs-lookup"><span data-stu-id="1be9b-406">**direction**</span></span>     || <span data-ttu-id="1be9b-407">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-407">Must be set to `in`.</span></span>         |
|<span data-ttu-id="1be9b-408">**name**</span><span class="sxs-lookup"><span data-stu-id="1be9b-408">**name**</span></span>     || <span data-ttu-id="1be9b-409">Name of the binding parameter that represents the document in the function.</span><span class="sxs-lookup"><span data-stu-id="1be9b-409">Name of the binding parameter that represents the document in the function.</span></span>  |
|<span data-ttu-id="1be9b-410">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-410">**databaseName**</span></span> |<span data-ttu-id="1be9b-411">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-411">**DatabaseName**</span></span> |<span data-ttu-id="1be9b-412">The database containing the document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-412">The database containing the document.</span></span>        |
|<span data-ttu-id="1be9b-413">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-413">**collectionName**</span></span> |<span data-ttu-id="1be9b-414">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-414">**CollectionName**</span></span> | <span data-ttu-id="1be9b-415">The name of the collection that contains the document.</span><span class="sxs-lookup"><span data-stu-id="1be9b-415">The name of the collection that contains the document.</span></span> |
|<span data-ttu-id="1be9b-416">**id**</span><span class="sxs-lookup"><span data-stu-id="1be9b-416">**id**</span></span>    | <span data-ttu-id="1be9b-417">**Id**</span><span class="sxs-lookup"><span data-stu-id="1be9b-417">**Id**</span></span> | <span data-ttu-id="1be9b-418">The ID of the document to retrieve.</span><span class="sxs-lookup"><span data-stu-id="1be9b-418">The ID of the document to retrieve.</span></span> <span data-ttu-id="1be9b-419">This property supports [binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="1be9b-419">This property supports [binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span> <span data-ttu-id="1be9b-420">Don't set both the **id** and **sqlQuery** properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-420">Don't set both the **id** and **sqlQuery** properties.</span></span> <span data-ttu-id="1be9b-421">If you don't set either one, the entire collection is retrieved.</span><span class="sxs-lookup"><span data-stu-id="1be9b-421">If you don't set either one, the entire collection is retrieved.</span></span> |
|<span data-ttu-id="1be9b-422">**sqlQuery**</span><span class="sxs-lookup"><span data-stu-id="1be9b-422">**sqlQuery**</span></span>  |<span data-ttu-id="1be9b-423">**SqlQuery**</span><span class="sxs-lookup"><span data-stu-id="1be9b-423">**SqlQuery**</span></span>  | <span data-ttu-id="1be9b-424">An Azure Cosmos DB SQL query used for retrieving multiple documents.</span><span class="sxs-lookup"><span data-stu-id="1be9b-424">An Azure Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="1be9b-425">The property supports runtime bindings, as in this example: `SELECT * FROM c where c.departmentId = {departmentId}`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-425">The property supports runtime bindings, as in this example: `SELECT * FROM c where c.departmentId = {departmentId}`.</span></span> <span data-ttu-id="1be9b-426">Don't set both the **id** and **sqlQuery** properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-426">Don't set both the **id** and **sqlQuery** properties.</span></span> <span data-ttu-id="1be9b-427">If you don't set either one, the entire collection is retrieved.</span><span class="sxs-lookup"><span data-stu-id="1be9b-427">If you don't set either one, the entire collection is retrieved.</span></span>|
|<span data-ttu-id="1be9b-428">**connectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-428">**connectionStringSetting**</span></span>     |<span data-ttu-id="1be9b-429">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-429">**ConnectionStringSetting**</span></span>|<span data-ttu-id="1be9b-430">The name of the app setting containing your Azure Cosmos DB connection string.</span><span class="sxs-lookup"><span data-stu-id="1be9b-430">The name of the app setting containing your Azure Cosmos DB connection string.</span></span>        |
|<span data-ttu-id="1be9b-431">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="1be9b-431">**partitionKey**</span></span>|<span data-ttu-id="1be9b-432">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="1be9b-432">**PartitionKey**</span></span>|<span data-ttu-id="1be9b-433">Specifies the partition key value for the lookup.</span><span class="sxs-lookup"><span data-stu-id="1be9b-433">Specifies the partition key value for the lookup.</span></span> <span data-ttu-id="1be9b-434">May include binding parameters.</span><span class="sxs-lookup"><span data-stu-id="1be9b-434">May include binding parameters.</span></span>|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="input---usage"></a><span data-ttu-id="1be9b-435">Input - usage</span><span class="sxs-lookup"><span data-stu-id="1be9b-435">Input - usage</span></span>

<span data-ttu-id="1be9b-436">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span><span class="sxs-lookup"><span data-stu-id="1be9b-436">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 

<span data-ttu-id="1be9b-437">In JavaScript functions, updates are not made automatically upon function exit.</span><span class="sxs-lookup"><span data-stu-id="1be9b-437">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="1be9b-438">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span><span class="sxs-lookup"><span data-stu-id="1be9b-438">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="1be9b-439">See the [JavaScript example](#input---javascript-example).</span><span class="sxs-lookup"><span data-stu-id="1be9b-439">See the [JavaScript example](#input---javascript-example).</span></span>

## <a name="output"></a><span data-ttu-id="1be9b-440">Output</span><span class="sxs-lookup"><span data-stu-id="1be9b-440">Output</span></span>

<span data-ttu-id="1be9b-441">The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span><span class="sxs-lookup"><span data-stu-id="1be9b-441">The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span></span> 

## <a name="output---examples"></a><span data-ttu-id="1be9b-442">Output - examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-442">Output - examples</span></span>

<span data-ttu-id="1be9b-443">See the language-specific examples:</span><span class="sxs-lookup"><span data-stu-id="1be9b-443">See the language-specific examples:</span></span>

* [<span data-ttu-id="1be9b-444">C#</span><span class="sxs-lookup"><span data-stu-id="1be9b-444">C#</span></span>](#output---c-examples)
* [<span data-ttu-id="1be9b-445">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="1be9b-445">C# script (.csx)</span></span>](#output---c-script-examples)
* [<span data-ttu-id="1be9b-446">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1be9b-446">JavaScript</span></span>](#output---javascript-examples)
* [<span data-ttu-id="1be9b-447">F#</span><span class="sxs-lookup"><span data-stu-id="1be9b-447">F#</span></span>](#output---f-examples)
* [<span data-ttu-id="1be9b-448">Java</span><span class="sxs-lookup"><span data-stu-id="1be9b-448">Java</span></span>](#output---java-example)

<span data-ttu-id="1be9b-449">See also the [input example](#input---c-examples) that uses `DocumentClient`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-449">See also the [input example](#input---c-examples) that uses `DocumentClient`.</span></span>

[<span data-ttu-id="1be9b-450">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-450">Skip output examples</span></span>](#output---attributes)

### <a name="ouput---c-examples"></a><span data-ttu-id="1be9b-451">Ouput - C# examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-451">Ouput - C# examples</span></span>

<span data-ttu-id="1be9b-452">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="1be9b-452">This section contains the following examples:</span></span>

* <span data-ttu-id="1be9b-453">Queue trigger, write one doc</span><span class="sxs-lookup"><span data-stu-id="1be9b-453">Queue trigger, write one doc</span></span>
* <span data-ttu-id="1be9b-454">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="1be9b-454">Queue trigger, write docs using IAsyncCollector</span></span>

<span data-ttu-id="1be9b-455">The examples refer to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="1be9b-455">The examples refer to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV2
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

[<span data-ttu-id="1be9b-456">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-456">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-one-doc-c"></a><span data-ttu-id="1be9b-457">Queue trigger, write one doc (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-457">Queue trigger, write one doc (C#)</span></span>

<span data-ttu-id="1be9b-458">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a document to a database, using data provided in message from Queue storage.</span><span class="sxs-lookup"><span data-stu-id="1be9b-458">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a document to a database, using data provided in message from Queue storage.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System;

namespace CosmosDBSamplesV2
{
    public static class WriteOneDoc
    {
        [FunctionName("WriteOneDoc")]
        public static void Run(
            [QueueTrigger("todoqueueforwrite")] string queueMessage,
            [CosmosDB(
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

[<span data-ttu-id="1be9b-459">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-459">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-docs-using-iasynccollector-c"></a><span data-ttu-id="1be9b-460">Queue trigger, write docs using IAsyncCollector (C#)</span><span class="sxs-lookup"><span data-stu-id="1be9b-460">Queue trigger, write docs using IAsyncCollector (C#)</span></span>

<span data-ttu-id="1be9b-461">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a collection of documents to a database, using data provided in a queue message JSON.</span><span class="sxs-lookup"><span data-stu-id="1be9b-461">The following example shows a [C# function](functions-dotnet-class-library.md) that adds a collection of documents to a database, using data provided in a queue message JSON.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Threading.Tasks;

namespace CosmosDBSamplesV2
{
    public static class WriteDocsIAsyncCollector
    {
        [FunctionName("WriteDocsIAsyncCollector")]
        public static async Task Run(
            [QueueTrigger("todoqueueforwritemulti")] ToDoItem[] toDoItemsIn,
            [CosmosDB(
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

[<span data-ttu-id="1be9b-462">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-462">Skip output examples</span></span>](#output---attributes)

### <a name="output---c-script-examples"></a><span data-ttu-id="1be9b-463">Output - C# script examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-463">Output - C# script examples</span></span>

<span data-ttu-id="1be9b-464">This section contains the following examples:</span><span class="sxs-lookup"><span data-stu-id="1be9b-464">This section contains the following examples:</span></span>

* <span data-ttu-id="1be9b-465">Queue trigger, write one doc</span><span class="sxs-lookup"><span data-stu-id="1be9b-465">Queue trigger, write one doc</span></span>
* <span data-ttu-id="1be9b-466">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="1be9b-466">Queue trigger, write docs using IAsyncCollector</span></span>

[<span data-ttu-id="1be9b-467">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-467">Skip output examples</span></span>](#output---attributes)

#### <a name="queue-trigger-write-one-doc-c-script"></a><span data-ttu-id="1be9b-468">Queue trigger, write one doc (C# script)</span><span class="sxs-lookup"><span data-stu-id="1be9b-468">Queue trigger, write one doc (C# script)</span></span>

<span data-ttu-id="1be9b-469">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-469">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-470">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="1be9b-470">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-471">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="1be9b-471">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-472">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-472">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

<span data-ttu-id="1be9b-473">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-473">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-474">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-474">Here's the C# script code:</span></span>

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

#### <a name="queue-trigger-write-docs-using-iasynccollector"></a><span data-ttu-id="1be9b-475">Queue trigger, write docs using IAsyncCollector</span><span class="sxs-lookup"><span data-stu-id="1be9b-475">Queue trigger, write docs using IAsyncCollector</span></span>

<span data-ttu-id="1be9b-476">To create multiple documents, you can bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span><span class="sxs-lookup"><span data-stu-id="1be9b-476">To create multiple documents, you can bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<span data-ttu-id="1be9b-477">This example refers to a simple `ToDoItem` type:</span><span class="sxs-lookup"><span data-stu-id="1be9b-477">This example refers to a simple `ToDoItem` type:</span></span>

```cs
namespace CosmosDBSamplesV2
{
    public class ToDoItem
    {
        public string Id { get; set; }
        public string Description { get; set; }
    }
}
```

<span data-ttu-id="1be9b-478">Here's the function.json file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-478">Here's the function.json file:</span></span>

```json
{
  "bindings": [
    {
      "name": "toDoItemsIn",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "todoqueueforwritemulti",
      "connectionStringSetting": "AzureWebJobsStorage"
    },
    {
      "type": "cosmosDB",
      "name": "toDoItemsOut",
      "databaseName": "ToDoItems",
      "collectionName": "Items",
      "connectionStringSetting": "CosmosDBConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="1be9b-479">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-479">Here's the C# script code:</span></span>

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

[<span data-ttu-id="1be9b-480">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-480">Skip output examples</span></span>](#output---attributes)

### <a name="output---javascript-examples"></a><span data-ttu-id="1be9b-481">Output - JavaScript examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-481">Output - JavaScript examples</span></span>

<span data-ttu-id="1be9b-482">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-482">The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-483">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="1be9b-483">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-484">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="1be9b-484">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-485">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-485">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```

<span data-ttu-id="1be9b-486">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-486">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-487">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-487">Here's the JavaScript code:</span></span>

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

[<span data-ttu-id="1be9b-488">Skip output examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-488">Skip output examples</span></span>](#output---attributes)

### <a name="output---f-examples"></a><span data-ttu-id="1be9b-489">Output - F# examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-489">Output - F# examples</span></span>

<span data-ttu-id="1be9b-490">The following example shows an Azure Cosmos DB output binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1be9b-490">The following example shows an Azure Cosmos DB output binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="1be9b-491">The function uses a queue input binding for a queue that receives JSON in the following format:</span><span class="sxs-lookup"><span data-stu-id="1be9b-491">The function uses a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-492">The function creates Azure Cosmos DB documents in the following format for each record:</span><span class="sxs-lookup"><span data-stu-id="1be9b-492">The function creates Azure Cosmos DB documents in the following format for each record:</span></span>

```json
{
    "id": "John Henry-123456",
    "name": "John Henry",
    "employeeId": "123456",
    "address": "A town nearby"
}
```

<span data-ttu-id="1be9b-493">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1be9b-493">Here's the binding data in the *function.json* file:</span></span>

```json
{
    "name": "employeeDocument",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": true,
    "connectionStringSetting": "MyAccount_COSMOSDB",     
    "direction": "out"
}
```
<span data-ttu-id="1be9b-494">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1be9b-494">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="1be9b-495">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="1be9b-495">Here's the F# code:</span></span>

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

<span data-ttu-id="1be9b-496">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span><span class="sxs-lookup"><span data-stu-id="1be9b-496">This example requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="1be9b-497">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="1be9b-497">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

## <a name="output---java-examples"></a><span data-ttu-id="1be9b-498">Output - Java examples</span><span class="sxs-lookup"><span data-stu-id="1be9b-498">Output - Java examples</span></span>

<span data-ttu-id="1be9b-499">The following example shows a Java function that adds a document to a database with data from a message in Queue storage.</span><span class="sxs-lookup"><span data-stu-id="1be9b-499">The following example shows a Java function that adds a document to a database with data from a message in Queue storage.</span></span>

```java
@FunctionName("getItem")
@CosmosDBOutput(name = "database", databaseName = "ToDoList", collectionName = "Items", connectionStringSetting = "AzureCosmosDBConnection")
public String cosmosDbQueryById(
     @QueueTrigger(name = "msg", queueName = "myqueue-items", connection = "AzureWebJobsStorage") String message,
     final ExecutionContext context
)  {
     return "{ id: " + System.currentTimeMillis() + ", Description: " + message + " }";
   }
```

<span data-ttu-id="1be9b-500">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput` annotation on parameters that will be written to Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1be9b-500">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput` annotation on parameters that will be written to Cosmos DB.</span></span>  <span data-ttu-id="1be9b-501">The annotation parameter type should be OutputBinding<T>, where T is either a native Java type or a POJO.</span><span class="sxs-lookup"><span data-stu-id="1be9b-501">The annotation parameter type should be OutputBinding<T>, where T is either a native Java type or a POJO.</span></span>


## <a name="output---attributes"></a><span data-ttu-id="1be9b-502">Output - attributes</span><span class="sxs-lookup"><span data-stu-id="1be9b-502">Output - attributes</span></span>

<span data-ttu-id="1be9b-503">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/master/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-503">In [C# class libraries](functions-dotnet-class-library.md), use the [CosmosDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/master/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) attribute.</span></span>

<span data-ttu-id="1be9b-504">The attribute's constructor takes the database name and collection name.</span><span class="sxs-lookup"><span data-stu-id="1be9b-504">The attribute's constructor takes the database name and collection name.</span></span> <span data-ttu-id="1be9b-505">For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration).</span><span class="sxs-lookup"><span data-stu-id="1be9b-505">For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration).</span></span> <span data-ttu-id="1be9b-506">Here's a `CosmosDB` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="1be9b-506">Here's a `CosmosDB` attribute example in a method signature:</span></span>

```csharp
    [FunctionName("QueueToDocDB")]        
    public static void Run(
        [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
        [CosmosDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
    {
        ...
    }
```

<span data-ttu-id="1be9b-507">For a complete example, see [Output - C# example](#output---c-example).</span><span class="sxs-lookup"><span data-stu-id="1be9b-507">For a complete example, see [Output - C# example](#output---c-example).</span></span>

## <a name="output---configuration"></a><span data-ttu-id="1be9b-508">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="1be9b-508">Output - configuration</span></span>

<span data-ttu-id="1be9b-509">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDB` attribute.</span><span class="sxs-lookup"><span data-stu-id="1be9b-509">The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDB` attribute.</span></span>

|<span data-ttu-id="1be9b-510">function.json property</span><span class="sxs-lookup"><span data-stu-id="1be9b-510">function.json property</span></span> | <span data-ttu-id="1be9b-511">Attribute property</span><span class="sxs-lookup"><span data-stu-id="1be9b-511">Attribute property</span></span> |<span data-ttu-id="1be9b-512">Description</span><span class="sxs-lookup"><span data-stu-id="1be9b-512">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="1be9b-513">**type**</span><span class="sxs-lookup"><span data-stu-id="1be9b-513">**type**</span></span>     || <span data-ttu-id="1be9b-514">Must be set to `cosmosDB`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-514">Must be set to `cosmosDB`.</span></span>        |
|<span data-ttu-id="1be9b-515">**direction**</span><span class="sxs-lookup"><span data-stu-id="1be9b-515">**direction**</span></span>     || <span data-ttu-id="1be9b-516">Must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="1be9b-516">Must be set to `out`.</span></span>         |
|<span data-ttu-id="1be9b-517">**name**</span><span class="sxs-lookup"><span data-stu-id="1be9b-517">**name**</span></span>     || <span data-ttu-id="1be9b-518">Name of the binding parameter that represents the document in the function.</span><span class="sxs-lookup"><span data-stu-id="1be9b-518">Name of the binding parameter that represents the document in the function.</span></span>  |
|<span data-ttu-id="1be9b-519">**databaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-519">**databaseName**</span></span> | <span data-ttu-id="1be9b-520">**DatabaseName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-520">**DatabaseName**</span></span>|<span data-ttu-id="1be9b-521">The database containing the collection where the document is created.</span><span class="sxs-lookup"><span data-stu-id="1be9b-521">The database containing the collection where the document is created.</span></span>     |
|<span data-ttu-id="1be9b-522">**collectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-522">**collectionName**</span></span> |<span data-ttu-id="1be9b-523">**CollectionName**</span><span class="sxs-lookup"><span data-stu-id="1be9b-523">**CollectionName**</span></span>  | <span data-ttu-id="1be9b-524">The name of the collection where the document is created.</span><span class="sxs-lookup"><span data-stu-id="1be9b-524">The name of the collection where the document is created.</span></span> |
|<span data-ttu-id="1be9b-525">**createIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="1be9b-525">**createIfNotExists**</span></span>  |<span data-ttu-id="1be9b-526">**CreateIfNotExists**</span><span class="sxs-lookup"><span data-stu-id="1be9b-526">**CreateIfNotExists**</span></span>    | <span data-ttu-id="1be9b-527">A boolean value to indicate whether the collection is created when it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="1be9b-527">A boolean value to indicate whether the collection is created when it doesn't exist.</span></span> <span data-ttu-id="1be9b-528">The default is *false* because new collections are created with reserved throughput, which has cost implications.</span><span class="sxs-lookup"><span data-stu-id="1be9b-528">The default is *false* because new collections are created with reserved throughput, which has cost implications.</span></span> <span data-ttu-id="1be9b-529">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1be9b-529">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>  |
|<span data-ttu-id="1be9b-530">**partitionKey**</span><span class="sxs-lookup"><span data-stu-id="1be9b-530">**partitionKey**</span></span>|<span data-ttu-id="1be9b-531">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="1be9b-531">**PartitionKey**</span></span> |<span data-ttu-id="1be9b-532">When `CreateIfNotExists` is true, defines the partition key path for the created collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-532">When `CreateIfNotExists` is true, defines the partition key path for the created collection.</span></span>|
|<span data-ttu-id="1be9b-533">**collectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="1be9b-533">**collectionThroughput**</span></span>|<span data-ttu-id="1be9b-534">**CollectionThroughput**</span><span class="sxs-lookup"><span data-stu-id="1be9b-534">**CollectionThroughput**</span></span>| <span data-ttu-id="1be9b-535">When `CreateIfNotExists` is true, defines the [throughput](../cosmos-db/set-throughput.md) of the created collection.</span><span class="sxs-lookup"><span data-stu-id="1be9b-535">When `CreateIfNotExists` is true, defines the [throughput](../cosmos-db/set-throughput.md) of the created collection.</span></span>|
|<span data-ttu-id="1be9b-536">**connectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-536">**connectionStringSetting**</span></span>    |<span data-ttu-id="1be9b-537">**ConnectionStringSetting**</span><span class="sxs-lookup"><span data-stu-id="1be9b-537">**ConnectionStringSetting**</span></span> |<span data-ttu-id="1be9b-538">The name of the app setting containing your Azure Cosmos DB connection string.</span><span class="sxs-lookup"><span data-stu-id="1be9b-538">The name of the app setting containing your Azure Cosmos DB connection string.</span></span>        |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a><span data-ttu-id="1be9b-539">Output - usage</span><span class="sxs-lookup"><span data-stu-id="1be9b-539">Output - usage</span></span>

<span data-ttu-id="1be9b-540">By default, when you write to the output parameter in your function, a document is created in your database.</span><span class="sxs-lookup"><span data-stu-id="1be9b-540">By default, when you write to the output parameter in your function, a document is created in your database.</span></span> <span data-ttu-id="1be9b-541">This document has an automatically generated GUID as the document ID.</span><span class="sxs-lookup"><span data-stu-id="1be9b-541">This document has an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="1be9b-542">You can specify the document ID of the output document by specifying the `id` property in the JSON object passed to the output parameter.</span><span class="sxs-lookup"><span data-stu-id="1be9b-542">You can specify the document ID of the output document by specifying the `id` property in the JSON object passed to the output parameter.</span></span> 

> [!Note]  
> When you specify the ID of an existing document, it gets overwritten by the new output document. 

## <a name="exceptions-and-return-codes"></a><span data-ttu-id="1be9b-544">Exceptions and return codes</span><span class="sxs-lookup"><span data-stu-id="1be9b-544">Exceptions and return codes</span></span>

| <span data-ttu-id="1be9b-545">Binding</span><span class="sxs-lookup"><span data-stu-id="1be9b-545">Binding</span></span> | <span data-ttu-id="1be9b-546">Reference</span><span class="sxs-lookup"><span data-stu-id="1be9b-546">Reference</span></span> |
|---|---|
| <span data-ttu-id="1be9b-547">CosmosDB</span><span class="sxs-lookup"><span data-stu-id="1be9b-547">CosmosDB</span></span> | [<span data-ttu-id="1be9b-548">CosmosDB Error Codes</span><span class="sxs-lookup"><span data-stu-id="1be9b-548">CosmosDB Error Codes</span></span>](https://docs.microsoft.com/rest/api/cosmos-db/http-status-codes-for-cosmosdb) |

## <a name="next-steps"></a><span data-ttu-id="1be9b-549">Next steps</span><span class="sxs-lookup"><span data-stu-id="1be9b-549">Next steps</span></span>

> [!div class="nextstepaction"]
> [Go to a quickstart that uses a Cosmos DB trigger](functions-create-cosmos-db-triggered-function.md)

> [!div class="nextstepaction"]
> [Learn more about serverless database computing with Cosmos DB](..\cosmos-db\serverless-computing-database.md)

> [!div class="nextstepaction"]
> [Learn more about Azure functions triggers and bindings](functions-triggers-bindings.md)
