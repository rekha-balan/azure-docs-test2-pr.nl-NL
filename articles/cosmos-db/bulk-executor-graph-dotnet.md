---
title: Using the graph BulkExecutor .NET library to perform bulk operations in Azure Cosmos DB Gremlin API
description: Learn how to use the BulkExecutor library to massively import graph data into an Azure Cosmos DB Gremlin API container.
services: cosmos-db
keywords: graph, gremlin, bulk, bulkexecutor, migration, data, cosmosdb, cosmos, database, import
author: luisbosquez
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.devlang: na
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: 39abf6d6da8a8035cf486ceb30b9c21186bbb925
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857930"
---
# <a name="using-the-graph-bulkexecutor-net-library-to-perform-bulk-operations-in-azure-cosmos-db-gremlin-api"></a><span data-ttu-id="2b849-104">Using the graph BulkExecutor .NET library to perform bulk operations in Azure Cosmos DB Gremlin API</span><span class="sxs-lookup"><span data-stu-id="2b849-104">Using the graph BulkExecutor .NET library to perform bulk operations in Azure Cosmos DB Gremlin API</span></span>

<span data-ttu-id="2b849-105">This tutorial provides instructions about using Azure CosmosDB's BulkExecutor .NET library to import and update graph objects into an Azure Cosmos DB Gremlin API container.</span><span class="sxs-lookup"><span data-stu-id="2b849-105">This tutorial provides instructions about using Azure CosmosDB's BulkExecutor .NET library to import and update graph objects into an Azure Cosmos DB Gremlin API container.</span></span> <span data-ttu-id="2b849-106">This process makes use of the Graph class in the [BulkExecutor library](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-overview) to create Vertex and Edge objects programmatically to then insert multiple of them per network request.</span><span class="sxs-lookup"><span data-stu-id="2b849-106">This process makes use of the Graph class in the [BulkExecutor library](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-overview) to create Vertex and Edge objects programmatically to then insert multiple of them per network request.</span></span> <span data-ttu-id="2b849-107">This behavior is configurable through the BulkExecutor library to make optimal use of both database and local memory resources.</span><span class="sxs-lookup"><span data-stu-id="2b849-107">This behavior is configurable through the BulkExecutor library to make optimal use of both database and local memory resources.</span></span>

<span data-ttu-id="2b849-108">As opposed to sending Gremlin queries to a database, where the command is evaluated and then executed one at a time, using the BulkExecutor library will instead require to create and validate the objects locally.</span><span class="sxs-lookup"><span data-stu-id="2b849-108">As opposed to sending Gremlin queries to a database, where the command is evaluated and then executed one at a time, using the BulkExecutor library will instead require to create and validate the objects locally.</span></span> <span data-ttu-id="2b849-109">After creating the objects, the library allows you to send graph objects to the database service sequentially.</span><span class="sxs-lookup"><span data-stu-id="2b849-109">After creating the objects, the library allows you to send graph objects to the database service sequentially.</span></span> <span data-ttu-id="2b849-110">Using this method, data ingestion speeds can be increased up to 100x, which makes it an ideal method for initial data migrations or periodical data movement operations.</span><span class="sxs-lookup"><span data-stu-id="2b849-110">Using this method, data ingestion speeds can be increased up to 100x, which makes it an ideal method for initial data migrations or periodical data movement operations.</span></span> <span data-ttu-id="2b849-111">Learn more by visiting the GitHub page of the [Azure Cosmos DB Graph BulkExecutor sample application](https://aka.ms/graph-bulkexecutor-sample).</span><span class="sxs-lookup"><span data-stu-id="2b849-111">Learn more by visiting the GitHub page of the [Azure Cosmos DB Graph BulkExecutor sample application](https://aka.ms/graph-bulkexecutor-sample).</span></span>

## <a name="bulk-operations-with-graph-data"></a><span data-ttu-id="2b849-112">Bulk operations with graph data</span><span class="sxs-lookup"><span data-stu-id="2b849-112">Bulk operations with graph data</span></span>

<span data-ttu-id="2b849-113">The [BulkExecutor library](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph?view=azure-dotnet) contains a `Microsoft.Azure.CosmosDB.BulkExecutor.Graph` namespace to provide functionality for creating and importing graph objects.</span><span class="sxs-lookup"><span data-stu-id="2b849-113">The [BulkExecutor library](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph?view=azure-dotnet) contains a `Microsoft.Azure.CosmosDB.BulkExecutor.Graph` namespace to provide functionality for creating and importing graph objects.</span></span> 

<span data-ttu-id="2b849-114">The following process outlines how data migration can be used for a Gremlin API container:</span><span class="sxs-lookup"><span data-stu-id="2b849-114">The following process outlines how data migration can be used for a Gremlin API container:</span></span>
1. <span data-ttu-id="2b849-115">Retrieve records from the data source.</span><span class="sxs-lookup"><span data-stu-id="2b849-115">Retrieve records from the data source.</span></span>
2. <span data-ttu-id="2b849-116">Construct `GremlinVertex` and `GremlinEdge` objects from the obtained records and add them into an `IEnumerable` data structure.</span><span class="sxs-lookup"><span data-stu-id="2b849-116">Construct `GremlinVertex` and `GremlinEdge` objects from the obtained records and add them into an `IEnumerable` data structure.</span></span> <span data-ttu-id="2b849-117">In this part of the application the logic to detect and add relationships should be implemented, in case the data source is not a graph database.</span><span class="sxs-lookup"><span data-stu-id="2b849-117">In this part of the application the logic to detect and add relationships should be implemented, in case the data source is not a graph database.</span></span>
3. <span data-ttu-id="2b849-118">Use the [Graph BulkImportAsync method](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph.graphbulkexecutor.bulkimportasync?view=azure-dotnet) to insert the graph objects into the collection.</span><span class="sxs-lookup"><span data-stu-id="2b849-118">Use the [Graph BulkImportAsync method](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph.graphbulkexecutor.bulkimportasync?view=azure-dotnet) to insert the graph objects into the collection.</span></span>

<span data-ttu-id="2b849-119">This mechanism will improve the data migration efficiency as compared to using a Gremlin client.</span><span class="sxs-lookup"><span data-stu-id="2b849-119">This mechanism will improve the data migration efficiency as compared to using a Gremlin client.</span></span> <span data-ttu-id="2b849-120">This improvement is experienced because inserting data with Gremlin will require the application send a query at a time that will need to be validated, evaluated, and then executed to create the data.</span><span class="sxs-lookup"><span data-stu-id="2b849-120">This improvement is experienced because inserting data with Gremlin will require the application send a query at a time that will need to be validated, evaluated, and then executed to create the data.</span></span> <span data-ttu-id="2b849-121">The BulkExecutor library will handle the validation in the application and send multiple graph objects at a time for each network request.</span><span class="sxs-lookup"><span data-stu-id="2b849-121">The BulkExecutor library will handle the validation in the application and send multiple graph objects at a time for each network request.</span></span>

### <a name="creating-vertices-and-edges"></a><span data-ttu-id="2b849-122">Creating Vertices and Edges</span><span class="sxs-lookup"><span data-stu-id="2b849-122">Creating Vertices and Edges</span></span>

<span data-ttu-id="2b849-123">`GraphBulkExecutor` provides the `BulkImportAsync` method that requires a `IEnumerable` list of `GremlinVertex` or `GremlinEdge` objects, both defined in the `Microsoft.Azure.CosmosDB.BulkExecutor.Graph.Element` namespace.</span><span class="sxs-lookup"><span data-stu-id="2b849-123">`GraphBulkExecutor` provides the `BulkImportAsync` method that requires a `IEnumerable` list of `GremlinVertex` or `GremlinEdge` objects, both defined in the `Microsoft.Azure.CosmosDB.BulkExecutor.Graph.Element` namespace.</span></span> <span data-ttu-id="2b849-124">In the sample, we separated the edges and vertices into two BulkExecutor import tasks.</span><span class="sxs-lookup"><span data-stu-id="2b849-124">In the sample, we separated the edges and vertices into two BulkExecutor import tasks.</span></span> <span data-ttu-id="2b849-125">See the example below:</span><span class="sxs-lookup"><span data-stu-id="2b849-125">See the example below:</span></span>

```csharp

IBulkExecutor graphbulkExecutor = new GraphBulkExecutor(documentClient, targetCollection);

BulkImportResponse vResponse = null;
BulkImportResponse eResponse = null;

try
{
    // Import a list of GremlinVertex objects
    vResponse = await graphbulkExecutor.BulkImportAsync(
            Utils.GenerateVertices(numberOfDocumentsToGenerate),
            enableUpsert: true,
            disableAutomaticIdGeneration: true,
            maxConcurrencyPerPartitionKeyRange: null,
            maxInMemorySortingBatchSize: null,
            cancellationToken: token);

    // Import a list of GremlinEdge objects
    eResponse = await graphbulkExecutor.BulkImportAsync(
            Utils.GenerateEdges(numberOfDocumentsToGenerate),
            enableUpsert: true,
            disableAutomaticIdGeneration: true,
            maxConcurrencyPerPartitionKeyRange: null,
            maxInMemorySortingBatchSize: null,
            cancellationToken: token);
}
catch (DocumentClientException de)
{
    Trace.TraceError("Document client exception: {0}", de);
}
catch (Exception e)
{
    Trace.TraceError("Exception: {0}", e);
}
```

<span data-ttu-id="2b849-126">For more information on the parameters of the BulkExecutor library, refer to the [BulkImportData to Azure Cosmos DB topic](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-dot-net#bulk-import-data-to-azure-cosmos-db).</span><span class="sxs-lookup"><span data-stu-id="2b849-126">For more information on the parameters of the BulkExecutor library, refer to the [BulkImportData to Azure Cosmos DB topic](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-dot-net#bulk-import-data-to-azure-cosmos-db).</span></span>

<span data-ttu-id="2b849-127">The payload needs to be instantiated into `GremlinVertex` and `GremlinEdge` objects.</span><span class="sxs-lookup"><span data-stu-id="2b849-127">The payload needs to be instantiated into `GremlinVertex` and `GremlinEdge` objects.</span></span> <span data-ttu-id="2b849-128">Here is how these objects can be created:</span><span class="sxs-lookup"><span data-stu-id="2b849-128">Here is how these objects can be created:</span></span>

<span data-ttu-id="2b849-129">**Vertices**:</span><span class="sxs-lookup"><span data-stu-id="2b849-129">**Vertices**:</span></span>
```csharp
// Creating a vertex
GremlinVertex v = new GremlinVertex(
    "vertexId",
    "vertexLabel");

// Adding custom properties to the vertex
v.AddProperty("customProperty", "value");

// Partitioning keys must be specified for all vertices
v.AddProperty("partitioningKey", "value");
```

<span data-ttu-id="2b849-130">**Edges**:</span><span class="sxs-lookup"><span data-stu-id="2b849-130">**Edges**:</span></span>
```csharp
// Creating an edge
GremlinEdge e = new GremlinEdge(
    "edgeId",
    "edgeLabel",
    "targetVertexId",
    "sourceVertexId",
    "targetVertexLabel",
    "sourceVertexLabel",
    "targetVertexPartitioningKey",
    "sourceVertexPartitioningKey");

// Adding custom properties to the edge
e.AddProperty("customProperty", "value");
```

> [!NOTE]
> <span data-ttu-id="2b849-131">The BulkExecutor utility doesn't automatically check for existing Vertices before adding Edges.</span><span class="sxs-lookup"><span data-stu-id="2b849-131">The BulkExecutor utility doesn't automatically check for existing Vertices before adding Edges.</span></span> <span data-ttu-id="2b849-132">This needs to be validated in the application before running the BulkImport tasks.</span><span class="sxs-lookup"><span data-stu-id="2b849-132">This needs to be validated in the application before running the BulkImport tasks.</span></span>

## <a name="sample-application"></a><span data-ttu-id="2b849-133">Sample application</span><span class="sxs-lookup"><span data-stu-id="2b849-133">Sample application</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2b849-134">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b849-134">Prerequisites</span></span>
* <span data-ttu-id="2b849-135">Visual Studio 2017 with the Azure development workload.</span><span class="sxs-lookup"><span data-stu-id="2b849-135">Visual Studio 2017 with the Azure development workload.</span></span> <span data-ttu-id="2b849-136">You can get started with the [Visual Studio 2017 Community Edition](https://visualstudio.microsoft.com/downloads/) for free.</span><span class="sxs-lookup"><span data-stu-id="2b849-136">You can get started with the [Visual Studio 2017 Community Edition](https://visualstudio.microsoft.com/downloads/) for free.</span></span>
* <span data-ttu-id="2b849-137">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2b849-137">An Azure subscription.</span></span> <span data-ttu-id="2b849-138">You can create [a free Azure account here](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=cosmos-db).</span><span class="sxs-lookup"><span data-stu-id="2b849-138">You can create [a free Azure account here](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=cosmos-db).</span></span> <span data-ttu-id="2b849-139">Alternatively, you can create a Cosmos DB database account with [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2b849-139">Alternatively, you can create a Cosmos DB database account with [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription.</span></span>
* <span data-ttu-id="2b849-140">An Azure Cosmos DB Gremlin API database with an **unlimited collection**.</span><span class="sxs-lookup"><span data-stu-id="2b849-140">An Azure Cosmos DB Gremlin API database with an **unlimited collection**.</span></span> <span data-ttu-id="2b849-141">This guide shows how to get started with [Azure Cosmos DB Gremlin API in .NET](https://docs.microsoft.com/azure/cosmos-db/create-graph-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2b849-141">This guide shows how to get started with [Azure Cosmos DB Gremlin API in .NET](https://docs.microsoft.com/azure/cosmos-db/create-graph-dotnet).</span></span>
* <span data-ttu-id="2b849-142">Git.</span><span class="sxs-lookup"><span data-stu-id="2b849-142">Git.</span></span> <span data-ttu-id="2b849-143">For more information check out the [Git Downloads page](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2b849-143">For more information check out the [Git Downloads page](https://git-scm.com/downloads).</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="2b849-144">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="2b849-144">Clone the sample application</span></span>
<span data-ttu-id="2b849-145">In this tutorial, we'll follow through the steps for getting started by using the [Azure Cosmos DB Graph BulkExecutor sample](https://aka.ms/graph-bulkexecutor-sample) hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b849-145">In this tutorial, we'll follow through the steps for getting started by using the [Azure Cosmos DB Graph BulkExecutor sample](https://aka.ms/graph-bulkexecutor-sample) hosted on GitHub.</span></span> <span data-ttu-id="2b849-146">This application consists of a .NET solution that randomly generates vertex and edge objects and then executes bulk insertions to the specified graph database account.</span><span class="sxs-lookup"><span data-stu-id="2b849-146">This application consists of a .NET solution that randomly generates vertex and edge objects and then executes bulk insertions to the specified graph database account.</span></span> <span data-ttu-id="2b849-147">To get the application, run the `git clone` command below:</span><span class="sxs-lookup"><span data-stu-id="2b849-147">To get the application, run the `git clone` command below:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-cosmosdb-graph-bulkexecutor-dotnet-getting-started.git
```

<span data-ttu-id="2b849-148">This repository contains the GraphBulkExecutor sample with the following files:</span><span class="sxs-lookup"><span data-stu-id="2b849-148">This repository contains the GraphBulkExecutor sample with the following files:</span></span>

<span data-ttu-id="2b849-149">File</span><span class="sxs-lookup"><span data-stu-id="2b849-149">File</span></span>|<span data-ttu-id="2b849-150">Description</span><span class="sxs-lookup"><span data-stu-id="2b849-150">Description</span></span>
---|---
`App.config`|<span data-ttu-id="2b849-151">This is where the application and database-specific parameters are specified.</span><span class="sxs-lookup"><span data-stu-id="2b849-151">This is where the application and database-specific parameters are specified.</span></span> <span data-ttu-id="2b849-152">This file should be modified first to connect to the destination database and collections.</span><span class="sxs-lookup"><span data-stu-id="2b849-152">This file should be modified first to connect to the destination database and collections.</span></span>
`Program.cs`| <span data-ttu-id="2b849-153">This file contains the logic behind creating the `DocumentClient` collection, handling the cleanups and sending the BulkExecutor requests.</span><span class="sxs-lookup"><span data-stu-id="2b849-153">This file contains the logic behind creating the `DocumentClient` collection, handling the cleanups and sending the BulkExecutor requests.</span></span>
`Util.cs`| <span data-ttu-id="2b849-154">This file contains a helper class that contains the logic behind generating test data, and checking if the database and collections exist.</span><span class="sxs-lookup"><span data-stu-id="2b849-154">This file contains a helper class that contains the logic behind generating test data, and checking if the database and collections exist.</span></span>

<span data-ttu-id="2b849-155">In the `App.config` file, the following are the configuration values that can be provided:</span><span class="sxs-lookup"><span data-stu-id="2b849-155">In the `App.config` file, the following are the configuration values that can be provided:</span></span>

<span data-ttu-id="2b849-156">Setting</span><span class="sxs-lookup"><span data-stu-id="2b849-156">Setting</span></span>|<span data-ttu-id="2b849-157">Description</span><span class="sxs-lookup"><span data-stu-id="2b849-157">Description</span></span>
---|---
`EndPointUrl`|<span data-ttu-id="2b849-158">This is **your .NET SDK endpoint** found in the Overview blade of your Azure Cosmos DB Gremlin API database account.</span><span class="sxs-lookup"><span data-stu-id="2b849-158">This is **your .NET SDK endpoint** found in the Overview blade of your Azure Cosmos DB Gremlin API database account.</span></span> <span data-ttu-id="2b849-159">This has the format of `https://your-graph-database-account.documents.azure.com:443/`</span><span class="sxs-lookup"><span data-stu-id="2b849-159">This has the format of `https://your-graph-database-account.documents.azure.com:443/`</span></span>
`AuthorizationKey`|<span data-ttu-id="2b849-160">This is the Primary or Secondary key listed under your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2b849-160">This is the Primary or Secondary key listed under your Azure Cosmos DB account.</span></span> <span data-ttu-id="2b849-161">Learn more about [Securing Access to Azure Cosmos DB data](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#master-keys)</span><span class="sxs-lookup"><span data-stu-id="2b849-161">Learn more about [Securing Access to Azure Cosmos DB data](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#master-keys)</span></span>
<span data-ttu-id="2b849-162">`DatabaseName`, `CollectionName`</span><span class="sxs-lookup"><span data-stu-id="2b849-162">`DatabaseName`, `CollectionName`</span></span>|<span data-ttu-id="2b849-163">These are the **target database and collection names**.</span><span class="sxs-lookup"><span data-stu-id="2b849-163">These are the **target database and collection names**.</span></span> <span data-ttu-id="2b849-164">When `ShouldCleanupOnStart` is set to `true` these values, along with `CollectionThroughput`, will be used to drop them and create a new database and collection.</span><span class="sxs-lookup"><span data-stu-id="2b849-164">When `ShouldCleanupOnStart` is set to `true` these values, along with `CollectionThroughput`, will be used to drop them and create a new database and collection.</span></span> <span data-ttu-id="2b849-165">Similarly, if `ShouldCleanupOnFinish` is set to `true`, they will be used to delete the database as soon as the ingestion is over.</span><span class="sxs-lookup"><span data-stu-id="2b849-165">Similarly, if `ShouldCleanupOnFinish` is set to `true`, they will be used to delete the database as soon as the ingestion is over.</span></span> <span data-ttu-id="2b849-166">Note that the target collection must be **an unlimited collection**.</span><span class="sxs-lookup"><span data-stu-id="2b849-166">Note that the target collection must be **an unlimited collection**.</span></span>
`CollectionThroughput`|<span data-ttu-id="2b849-167">This is used to create a new collection if the `ShouldCleanupOnStart` option is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="2b849-167">This is used to create a new collection if the `ShouldCleanupOnStart` option is set to `true`.</span></span>
`ShouldCleanupOnStart`|<span data-ttu-id="2b849-168">This will drop the database account and collections before the program is run, and then create new ones with the `DatabaseName`, `CollectionName` and `CollectionThroughput` values.</span><span class="sxs-lookup"><span data-stu-id="2b849-168">This will drop the database account and collections before the program is run, and then create new ones with the `DatabaseName`, `CollectionName` and `CollectionThroughput` values.</span></span>
`ShouldCleanupOnFinish`|<span data-ttu-id="2b849-169">This will drop the database account and collections with the specified `DatabaseName` and `CollectionName` after the program is run.</span><span class="sxs-lookup"><span data-stu-id="2b849-169">This will drop the database account and collections with the specified `DatabaseName` and `CollectionName` after the program is run.</span></span>
`NumberOfDocumentsToImport`|<span data-ttu-id="2b849-170">This will determine the number of test vertices and edges that will be generated in the sample.</span><span class="sxs-lookup"><span data-stu-id="2b849-170">This will determine the number of test vertices and edges that will be generated in the sample.</span></span> <span data-ttu-id="2b849-171">This number will apply to both vertices and edges.</span><span class="sxs-lookup"><span data-stu-id="2b849-171">This number will apply to both vertices and edges.</span></span>
`NumberOfBatches`|<span data-ttu-id="2b849-172">This will determine the number of test vertices and edges that will be generated in the sample.</span><span class="sxs-lookup"><span data-stu-id="2b849-172">This will determine the number of test vertices and edges that will be generated in the sample.</span></span> <span data-ttu-id="2b849-173">This number will apply to both vertices and edges.</span><span class="sxs-lookup"><span data-stu-id="2b849-173">This number will apply to both vertices and edges.</span></span>
`CollectionPartitionKey`|<span data-ttu-id="2b849-174">This will be used to create the test vertices and edges, where this property will be auto-assigned.</span><span class="sxs-lookup"><span data-stu-id="2b849-174">This will be used to create the test vertices and edges, where this property will be auto-assigned.</span></span> <span data-ttu-id="2b849-175">This will also be used when re-creating the database and collections if the `ShouldCleanupOnStart` option is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="2b849-175">This will also be used when re-creating the database and collections if the `ShouldCleanupOnStart` option is set to `true`.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="2b849-176">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="2b849-176">Run the sample application</span></span>

1. <span data-ttu-id="2b849-177">Add your specific database configuration parameters in `App.config`.</span><span class="sxs-lookup"><span data-stu-id="2b849-177">Add your specific database configuration parameters in `App.config`.</span></span> <span data-ttu-id="2b849-178">This will be used to create a DocumentClient instance.</span><span class="sxs-lookup"><span data-stu-id="2b849-178">This will be used to create a DocumentClient instance.</span></span> <span data-ttu-id="2b849-179">If the database and container have not been created yet, they will be created automatically.</span><span class="sxs-lookup"><span data-stu-id="2b849-179">If the database and container have not been created yet, they will be created automatically.</span></span>
2. <span data-ttu-id="2b849-180">Run the application.</span><span class="sxs-lookup"><span data-stu-id="2b849-180">Run the application.</span></span> <span data-ttu-id="2b849-181">This will call `BulkImportAsync` two times, one to import Vertices and one to import Edges.</span><span class="sxs-lookup"><span data-stu-id="2b849-181">This will call `BulkImportAsync` two times, one to import Vertices and one to import Edges.</span></span> <span data-ttu-id="2b849-182">If any of the objects generates an error when they're inserted, they will be added to either `.\BadVertices.txt` or `.\BadEdges.txt`.</span><span class="sxs-lookup"><span data-stu-id="2b849-182">If any of the objects generates an error when they're inserted, they will be added to either `.\BadVertices.txt` or `.\BadEdges.txt`.</span></span>
3. <span data-ttu-id="2b849-183">Evaluate the results by querying the graph database.</span><span class="sxs-lookup"><span data-stu-id="2b849-183">Evaluate the results by querying the graph database.</span></span> <span data-ttu-id="2b849-184">If the `ShouldCleanupOnFinish` option is set to true, then the database will automatically be deleted.</span><span class="sxs-lookup"><span data-stu-id="2b849-184">If the `ShouldCleanupOnFinish` option is set to true, then the database will automatically be deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b849-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b849-185">Next steps</span></span>
* <span data-ttu-id="2b849-186">To learn about Nuget package details and release notes of bulk executor .Net library, see [bulk executor SDK details](sql-api-sdk-bulk-executor-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="2b849-186">To learn about Nuget package details and release notes of bulk executor .Net library, see [bulk executor SDK details](sql-api-sdk-bulk-executor-dot-net.md).</span></span> 
* <span data-ttu-id="2b849-187">Check out the [Performance Tips](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-dot-net#performance-tips) to further optimize the usage of BulkExecutor.</span><span class="sxs-lookup"><span data-stu-id="2b849-187">Check out the [Performance Tips](https://docs.microsoft.com/azure/cosmos-db/bulk-executor-dot-net#performance-tips) to further optimize the usage of BulkExecutor.</span></span>
* <span data-ttu-id="2b849-188">Review the [BulkExecutor.Graph Reference article](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph?view=azure-dotnet) for more details about the classes and methods defined in this namespace.</span><span class="sxs-lookup"><span data-stu-id="2b849-188">Review the [BulkExecutor.Graph Reference article](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.graph?view=azure-dotnet) for more details about the classes and methods defined in this namespace.</span></span>
