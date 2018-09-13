---
title: Azure Cosmos DB indexing policies | Microsoft Docs
description: Understand how indexing works in Azure Cosmos DB. Learn how to configure and change the indexing policy for automatic indexing and greater performance.
keywords: how indexing works, automatic indexing, indexing database
services: cosmos-db
author: rafats
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 03/26/2018
ms.author: rafats
ms.openlocfilehash: fea3455b31ff2ea7119fa4146aa84f855a3b6e35
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865322"
---
# <a name="how-does-azure-cosmos-db-index-data"></a><span data-ttu-id="7634a-105">How does Azure Cosmos DB index data?</span><span class="sxs-lookup"><span data-stu-id="7634a-105">How does Azure Cosmos DB index data?</span></span>

<span data-ttu-id="7634a-106">By default, all Azure Cosmos DB data is indexed.</span><span class="sxs-lookup"><span data-stu-id="7634a-106">By default, all Azure Cosmos DB data is indexed.</span></span> <span data-ttu-id="7634a-107">Although many customers are happy to let Azure Cosmos DB automatically handle all aspects of indexing, you can specify a custom *indexing policy* for collections during creation in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7634a-107">Although many customers are happy to let Azure Cosmos DB automatically handle all aspects of indexing, you can specify a custom *indexing policy* for collections during creation in Azure Cosmos DB.</span></span> <span data-ttu-id="7634a-108">Indexing policies in Azure Cosmos DB are more flexible and powerful than secondary indexes that are offered in other database platforms.</span><span class="sxs-lookup"><span data-stu-id="7634a-108">Indexing policies in Azure Cosmos DB are more flexible and powerful than secondary indexes that are offered in other database platforms.</span></span> <span data-ttu-id="7634a-109">In Azure Cosmos DB, you can design and customize the shape of the index without sacrificing schema flexibility.</span><span class="sxs-lookup"><span data-stu-id="7634a-109">In Azure Cosmos DB, you can design and customize the shape of the index without sacrificing schema flexibility.</span></span> 

<span data-ttu-id="7634a-110">To learn how indexing works in Azure Cosmos DB, it's important to understand that when you manage indexing policy, you can make fine-grained trade-offs between index storage overhead, write and query throughput, and query consistency.</span><span class="sxs-lookup"><span data-stu-id="7634a-110">To learn how indexing works in Azure Cosmos DB, it's important to understand that when you manage indexing policy, you can make fine-grained trade-offs between index storage overhead, write and query throughput, and query consistency.</span></span>  

<span data-ttu-id="7634a-111">In the following video, Azure Cosmos DB Program Manager Andrew Liu demonstrates the Azure Cosmos DB automatic indexing capabilities, and how to tune and configure the indexing policy on your Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="7634a-111">In the following video, Azure Cosmos DB Program Manager Andrew Liu demonstrates the Azure Cosmos DB automatic indexing capabilities, and how to tune and configure the indexing policy on your Azure Cosmos DB container.</span></span> 

>[!VIDEO https://www.youtube.com/embed/uFu2D-GscG0]

<span data-ttu-id="7634a-112">In this article, we take a close look at Azure Cosmos DB indexing policies, at how to customize indexing policy, and associated trade-offs.</span><span class="sxs-lookup"><span data-stu-id="7634a-112">In this article, we take a close look at Azure Cosmos DB indexing policies, at how to customize indexing policy, and associated trade-offs.</span></span> 

<span data-ttu-id="7634a-113">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="7634a-113">After reading this article, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="7634a-114">How can I override the properties to include or exclude from indexing?</span><span class="sxs-lookup"><span data-stu-id="7634a-114">How can I override the properties to include or exclude from indexing?</span></span>
* <span data-ttu-id="7634a-115">How can I configure the index for eventual updates?</span><span class="sxs-lookup"><span data-stu-id="7634a-115">How can I configure the index for eventual updates?</span></span>
* <span data-ttu-id="7634a-116">How can I configure indexing to perform ORDER BY or range queries?</span><span class="sxs-lookup"><span data-stu-id="7634a-116">How can I configure indexing to perform ORDER BY or range queries?</span></span>
* <span data-ttu-id="7634a-117">How do I make changes to a collection’s indexing policy?</span><span class="sxs-lookup"><span data-stu-id="7634a-117">How do I make changes to a collection’s indexing policy?</span></span>
* <span data-ttu-id="7634a-118">How do I compare storage and performance of different indexing policies?</span><span class="sxs-lookup"><span data-stu-id="7634a-118">How do I compare storage and performance of different indexing policies?</span></span>

## <a id="Indexing"></a> <span data-ttu-id="7634a-119">Cosmos DB indexing</span><span class="sxs-lookup"><span data-stu-id="7634a-119">Cosmos DB indexing</span></span>

<span data-ttu-id="7634a-120">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span><span class="sxs-lookup"><span data-stu-id="7634a-120">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="7634a-121">Often, the choice of the right index for querying a database requires much planning and experimentation.</span><span class="sxs-lookup"><span data-stu-id="7634a-121">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="7634a-122">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span><span class="sxs-lookup"><span data-stu-id="7634a-122">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="7634a-123">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span><span class="sxs-lookup"><span data-stu-id="7634a-123">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="7634a-124">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-124">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span>  

* <span data-ttu-id="7634a-125">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span><span class="sxs-lookup"><span data-stu-id="7634a-125">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>  

* <span data-ttu-id="7634a-126">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span><span class="sxs-lookup"><span data-stu-id="7634a-126">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="7634a-127">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span><span class="sxs-lookup"><span data-stu-id="7634a-127">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>  

* <span data-ttu-id="7634a-128">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span><span class="sxs-lookup"><span data-stu-id="7634a-128">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span>  

* <span data-ttu-id="7634a-129">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span><span class="sxs-lookup"><span data-stu-id="7634a-129">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="7634a-130">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span><span class="sxs-lookup"><span data-stu-id="7634a-130">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

## <span data-ttu-id="7634a-131">Customize the indexing policy of a collection <a id="CustomizingIndexingPolicy"></a></span><span class="sxs-lookup"><span data-stu-id="7634a-131">Customize the indexing policy of a collection <a id="CustomizingIndexingPolicy"></a></span></span>  
<span data-ttu-id="7634a-132">You can customize the trade-offs between storage, write and query performance, and query consistency by overriding the default indexing policy on an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-132">You can customize the trade-offs between storage, write and query performance, and query consistency by overriding the default indexing policy on an Azure Cosmos DB collection.</span></span> <span data-ttu-id="7634a-133">You can configure the following aspects:</span><span class="sxs-lookup"><span data-stu-id="7634a-133">You can configure the following aspects:</span></span>

* <span data-ttu-id="7634a-134">**Include or exclude documents and paths to and from the index**.</span><span class="sxs-lookup"><span data-stu-id="7634a-134">**Include or exclude documents and paths to and from the index**.</span></span> <span data-ttu-id="7634a-135">You can exclude or include specific documents in the index when you insert or replace the documents in the collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-135">You can exclude or include specific documents in the index when you insert or replace the documents in the collection.</span></span> <span data-ttu-id="7634a-136">You can also include or exclude specific JSON properties, also called *paths*, to be indexed across documents that are included in an index.</span><span class="sxs-lookup"><span data-stu-id="7634a-136">You can also include or exclude specific JSON properties, also called *paths*, to be indexed across documents that are included in an index.</span></span> <span data-ttu-id="7634a-137">Paths include wildcard patterns.</span><span class="sxs-lookup"><span data-stu-id="7634a-137">Paths include wildcard patterns.</span></span>
* <span data-ttu-id="7634a-138">**Configure various index types**.</span><span class="sxs-lookup"><span data-stu-id="7634a-138">**Configure various index types**.</span></span> <span data-ttu-id="7634a-139">For each included path, you can specify the type of index the path requires for a collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-139">For each included path, you can specify the type of index the path requires for a collection.</span></span> <span data-ttu-id="7634a-140">You can specify the type of index based on the path's data, the expected query workload, and numeric/string "precision."</span><span class="sxs-lookup"><span data-stu-id="7634a-140">You can specify the type of index based on the path's data, the expected query workload, and numeric/string "precision."</span></span>
* <span data-ttu-id="7634a-141">**Configure index update modes**.</span><span class="sxs-lookup"><span data-stu-id="7634a-141">**Configure index update modes**.</span></span> <span data-ttu-id="7634a-142">Azure Cosmos DB supports three indexing modes: Consistent, Lazy, and None.</span><span class="sxs-lookup"><span data-stu-id="7634a-142">Azure Cosmos DB supports three indexing modes: Consistent, Lazy, and None.</span></span> <span data-ttu-id="7634a-143">You can configure the indexing modes via the indexing policy on an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-143">You can configure the indexing modes via the indexing policy on an Azure Cosmos DB collection.</span></span> 

<span data-ttu-id="7634a-144">The following Microsoft .NET code snippet shows how to set a custom indexing policy when you create a collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-144">The following Microsoft .NET code snippet shows how to set a custom indexing policy when you create a collection.</span></span> <span data-ttu-id="7634a-145">In this example, we set the policy with a Range index for strings and numbers at the maximum precision.</span><span class="sxs-lookup"><span data-stu-id="7634a-145">In this example, we set the policy with a Range index for strings and numbers at the maximum precision.</span></span> <span data-ttu-id="7634a-146">You can use this policy to execute ORDER BY queries against strings.</span><span class="sxs-lookup"><span data-stu-id="7634a-146">You can use this policy to execute ORDER BY queries against strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> <span data-ttu-id="7634a-147">The JSON schema for indexing policy changed with the release of REST API version 2015-06-03.</span><span class="sxs-lookup"><span data-stu-id="7634a-147">The JSON schema for indexing policy changed with the release of REST API version 2015-06-03.</span></span> <span data-ttu-id="7634a-148">With that release, the JSON schema for indexing policy supports Range indexes against strings.</span><span class="sxs-lookup"><span data-stu-id="7634a-148">With that release, the JSON schema for indexing policy supports Range indexes against strings.</span></span> <span data-ttu-id="7634a-149">.NET SDK 1.2.0 and Java, Python, and Node.js SDKs 1.1.0 support the new policy schema.</span><span class="sxs-lookup"><span data-stu-id="7634a-149">.NET SDK 1.2.0 and Java, Python, and Node.js SDKs 1.1.0 support the new policy schema.</span></span> <span data-ttu-id="7634a-150">Earlier versions of the SDK use the REST API version 2015-04-08.</span><span class="sxs-lookup"><span data-stu-id="7634a-150">Earlier versions of the SDK use the REST API version 2015-04-08.</span></span> <span data-ttu-id="7634a-151">They support the earlier schema for indexing policy.</span><span class="sxs-lookup"><span data-stu-id="7634a-151">They support the earlier schema for indexing policy.</span></span>
> 
> <span data-ttu-id="7634a-152">By default, Azure Cosmos DB indexes all string properties within documents consistently with a Hash index.</span><span class="sxs-lookup"><span data-stu-id="7634a-152">By default, Azure Cosmos DB indexes all string properties within documents consistently with a Hash index.</span></span> <span data-ttu-id="7634a-153">It indexes all numeric properties within documents consistently with a Range index.</span><span class="sxs-lookup"><span data-stu-id="7634a-153">It indexes all numeric properties within documents consistently with a Range index.</span></span>  
> 
> 

### <a name="customize-the-indexing-policy-in-the-portal"></a><span data-ttu-id="7634a-154">Customize the indexing policy in the portal</span><span class="sxs-lookup"><span data-stu-id="7634a-154">Customize the indexing policy in the portal</span></span>

<span data-ttu-id="7634a-155">You can change the indexing policy of a collection in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="7634a-155">You can change the indexing policy of a collection in the Azure portal:</span></span> 

1. <span data-ttu-id="7634a-156">In the portal, go to your Azure Cosmos DB account, and then select your collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-156">In the portal, go to your Azure Cosmos DB account, and then select your collection.</span></span> 
2. <span data-ttu-id="7634a-157">In the left navigation menu, select **Settings**, and then select **Indexing Policy**.</span><span class="sxs-lookup"><span data-stu-id="7634a-157">In the left navigation menu, select **Settings**, and then select **Indexing Policy**.</span></span> 
3. <span data-ttu-id="7634a-158">Under **Indexing Policy**, change your indexing policy, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="7634a-158">Under **Indexing Policy**, change your indexing policy, and then select **OK**.</span></span> 

### <span data-ttu-id="7634a-159">Database indexing modes <a id="indexing-modes"></a></span><span class="sxs-lookup"><span data-stu-id="7634a-159">Database indexing modes <a id="indexing-modes"></a></span></span>  
<span data-ttu-id="7634a-160">Azure Cosmos DB supports three indexing modes that you can configure via the indexing policy on an Azure Cosmos DB collection: Consistent, Lazy, and None.</span><span class="sxs-lookup"><span data-stu-id="7634a-160">Azure Cosmos DB supports three indexing modes that you can configure via the indexing policy on an Azure Cosmos DB collection: Consistent, Lazy, and None.</span></span>

<span data-ttu-id="7634a-161">**Consistent**: If an Azure Cosmos DB collection’s policy is Consistent, the queries on a specific Azure Cosmos DB collection follow the same consistency level as specified for the point-reads (strong, bounded-staleness, session, or eventual).</span><span class="sxs-lookup"><span data-stu-id="7634a-161">**Consistent**: If an Azure Cosmos DB collection’s policy is Consistent, the queries on a specific Azure Cosmos DB collection follow the same consistency level as specified for the point-reads (strong, bounded-staleness, session, or eventual).</span></span> <span data-ttu-id="7634a-162">The index is updated synchronously as part of the document update (insert, replace, update, and delete a document in an Azure Cosmos DB collection).</span><span class="sxs-lookup"><span data-stu-id="7634a-162">The index is updated synchronously as part of the document update (insert, replace, update, and delete a document in an Azure Cosmos DB collection).</span></span>

<span data-ttu-id="7634a-163">Consistent indexing supports consistent queries at the cost of a possible reduction in write throughput.</span><span class="sxs-lookup"><span data-stu-id="7634a-163">Consistent indexing supports consistent queries at the cost of a possible reduction in write throughput.</span></span> <span data-ttu-id="7634a-164">This reduction is a function of the unique paths that need to be indexed and the "consistency level."</span><span class="sxs-lookup"><span data-stu-id="7634a-164">This reduction is a function of the unique paths that need to be indexed and the "consistency level."</span></span> <span data-ttu-id="7634a-165">Consistent indexing mode is designed for "write quickly, query immediately" workloads.</span><span class="sxs-lookup"><span data-stu-id="7634a-165">Consistent indexing mode is designed for "write quickly, query immediately" workloads.</span></span>

<span data-ttu-id="7634a-166">**Lazy**:  The index is updated asynchronously when an Azure Cosmos DB collection is quiescent, that is, when the collection’s throughput capacity is not fully utilized to serve user requests.</span><span class="sxs-lookup"><span data-stu-id="7634a-166">**Lazy**:  The index is updated asynchronously when an Azure Cosmos DB collection is quiescent, that is, when the collection’s throughput capacity is not fully utilized to serve user requests.</span></span>  <span data-ttu-id="7634a-167">Note that you might get inconsistent results because data is ingested and indexed slowly.</span><span class="sxs-lookup"><span data-stu-id="7634a-167">Note that you might get inconsistent results because data is ingested and indexed slowly.</span></span> <span data-ttu-id="7634a-168">This means that your COUNT queries or specific query results might not be consistent or repeatable at  given time.</span><span class="sxs-lookup"><span data-stu-id="7634a-168">This means that your COUNT queries or specific query results might not be consistent or repeatable at  given time.</span></span> 

<span data-ttu-id="7634a-169">The index is generally in catch-up mode with ingested data.</span><span class="sxs-lookup"><span data-stu-id="7634a-169">The index is generally in catch-up mode with ingested data.</span></span> <span data-ttu-id="7634a-170">With Lazy indexing, time to live (TTL) changes result in the index being dropped and re-created.</span><span class="sxs-lookup"><span data-stu-id="7634a-170">With Lazy indexing, time to live (TTL) changes result in the index being dropped and re-created.</span></span> <span data-ttu-id="7634a-171">This makes the COUNT and query results inconsistent for a period of time.</span><span class="sxs-lookup"><span data-stu-id="7634a-171">This makes the COUNT and query results inconsistent for a period of time.</span></span> <span data-ttu-id="7634a-172">Most Azure Cosmos DB accounts should use the Consistent indexing mode.</span><span class="sxs-lookup"><span data-stu-id="7634a-172">Most Azure Cosmos DB accounts should use the Consistent indexing mode.</span></span>

<span data-ttu-id="7634a-173">**None**: A collection that has a None index mode has no index associated with it.</span><span class="sxs-lookup"><span data-stu-id="7634a-173">**None**: A collection that has a None index mode has no index associated with it.</span></span> <span data-ttu-id="7634a-174">This is commonly used if Azure Cosmos DB is used as a key-value storage, and documents are accessed only by their ID property.</span><span class="sxs-lookup"><span data-stu-id="7634a-174">This is commonly used if Azure Cosmos DB is used as a key-value storage, and documents are accessed only by their ID property.</span></span> 

> [!NOTE]
> <span data-ttu-id="7634a-175">Configuring the indexing policy with as None has the side effect of dropping any existing index.</span><span class="sxs-lookup"><span data-stu-id="7634a-175">Configuring the indexing policy with as None has the side effect of dropping any existing index.</span></span> <span data-ttu-id="7634a-176">Use this if your access patterns require only ID or self-link.</span><span class="sxs-lookup"><span data-stu-id="7634a-176">Use this if your access patterns require only ID or self-link.</span></span>
> 
> 

<span data-ttu-id="7634a-177">The following table shows the consistency for queries based on the indexing mode (Consistent and Lazy) configured for the collection and the consistency level specified for the query request.</span><span class="sxs-lookup"><span data-stu-id="7634a-177">The following table shows the consistency for queries based on the indexing mode (Consistent and Lazy) configured for the collection and the consistency level specified for the query request.</span></span> <span data-ttu-id="7634a-178">This applies to queries made by using any interface: REST API, SDKs, or from within stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="7634a-178">This applies to queries made by using any interface: REST API, SDKs, or from within stored procedures and triggers.</span></span> 

|<span data-ttu-id="7634a-179">Consistency</span><span class="sxs-lookup"><span data-stu-id="7634a-179">Consistency</span></span>|<span data-ttu-id="7634a-180">Indexing mode: Consistent</span><span class="sxs-lookup"><span data-stu-id="7634a-180">Indexing mode: Consistent</span></span>|<span data-ttu-id="7634a-181">Indexing mode: Lazy</span><span class="sxs-lookup"><span data-stu-id="7634a-181">Indexing mode: Lazy</span></span>|
|---|---|---|
|<span data-ttu-id="7634a-182">Strong</span><span class="sxs-lookup"><span data-stu-id="7634a-182">Strong</span></span>|<span data-ttu-id="7634a-183">Strong</span><span class="sxs-lookup"><span data-stu-id="7634a-183">Strong</span></span>|<span data-ttu-id="7634a-184">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-184">Eventual</span></span>|
|<span data-ttu-id="7634a-185">Bounded staleness</span><span class="sxs-lookup"><span data-stu-id="7634a-185">Bounded staleness</span></span>|<span data-ttu-id="7634a-186">Bounded staleness</span><span class="sxs-lookup"><span data-stu-id="7634a-186">Bounded staleness</span></span>|<span data-ttu-id="7634a-187">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-187">Eventual</span></span>|
|<span data-ttu-id="7634a-188">Session</span><span class="sxs-lookup"><span data-stu-id="7634a-188">Session</span></span>|<span data-ttu-id="7634a-189">Session</span><span class="sxs-lookup"><span data-stu-id="7634a-189">Session</span></span>|<span data-ttu-id="7634a-190">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-190">Eventual</span></span>|
|<span data-ttu-id="7634a-191">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-191">Eventual</span></span>|<span data-ttu-id="7634a-192">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-192">Eventual</span></span>|<span data-ttu-id="7634a-193">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-193">Eventual</span></span>|

<span data-ttu-id="7634a-194">Azure Cosmos DB returns an error for queries made on collections that have a None indexing mode.</span><span class="sxs-lookup"><span data-stu-id="7634a-194">Azure Cosmos DB returns an error for queries made on collections that have a None indexing mode.</span></span> <span data-ttu-id="7634a-195">Queries can still be executed as scans via the explicit **x-ms-documentdb-enable-scan** header in the REST API or the **EnableScanInQuery** request option by using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7634a-195">Queries can still be executed as scans via the explicit **x-ms-documentdb-enable-scan** header in the REST API or the **EnableScanInQuery** request option by using the .NET SDK.</span></span> <span data-ttu-id="7634a-196">Some query features, like ORDER BY, are not supported as scans with **EnableScanInQuery**.</span><span class="sxs-lookup"><span data-stu-id="7634a-196">Some query features, like ORDER BY, are not supported as scans with **EnableScanInQuery**.</span></span>

<span data-ttu-id="7634a-197">The following table shows the consistency for queries based on the indexing mode (Consistent, Lazy, and None) when **EnableScanInQuery** is specified.</span><span class="sxs-lookup"><span data-stu-id="7634a-197">The following table shows the consistency for queries based on the indexing mode (Consistent, Lazy, and None) when **EnableScanInQuery** is specified.</span></span>

|<span data-ttu-id="7634a-198">Consistency</span><span class="sxs-lookup"><span data-stu-id="7634a-198">Consistency</span></span>|<span data-ttu-id="7634a-199">Indexing Mode: Consistent</span><span class="sxs-lookup"><span data-stu-id="7634a-199">Indexing Mode: Consistent</span></span>|<span data-ttu-id="7634a-200">Indexing Mode: Lazy</span><span class="sxs-lookup"><span data-stu-id="7634a-200">Indexing Mode: Lazy</span></span>|<span data-ttu-id="7634a-201">Indexing Mode: None</span><span class="sxs-lookup"><span data-stu-id="7634a-201">Indexing Mode: None</span></span>|
|---|---|---|---|
|<span data-ttu-id="7634a-202">Strong</span><span class="sxs-lookup"><span data-stu-id="7634a-202">Strong</span></span>|<span data-ttu-id="7634a-203">Strong</span><span class="sxs-lookup"><span data-stu-id="7634a-203">Strong</span></span>|<span data-ttu-id="7634a-204">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-204">Eventual</span></span>|<span data-ttu-id="7634a-205">Strong</span><span class="sxs-lookup"><span data-stu-id="7634a-205">Strong</span></span>|
|<span data-ttu-id="7634a-206">Bounded staleness</span><span class="sxs-lookup"><span data-stu-id="7634a-206">Bounded staleness</span></span>|<span data-ttu-id="7634a-207">Bounded staleness</span><span class="sxs-lookup"><span data-stu-id="7634a-207">Bounded staleness</span></span>|<span data-ttu-id="7634a-208">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-208">Eventual</span></span>|<span data-ttu-id="7634a-209">Bounded staleness</span><span class="sxs-lookup"><span data-stu-id="7634a-209">Bounded staleness</span></span>|
|<span data-ttu-id="7634a-210">Session</span><span class="sxs-lookup"><span data-stu-id="7634a-210">Session</span></span>|<span data-ttu-id="7634a-211">Session</span><span class="sxs-lookup"><span data-stu-id="7634a-211">Session</span></span>|<span data-ttu-id="7634a-212">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-212">Eventual</span></span>|<span data-ttu-id="7634a-213">Session</span><span class="sxs-lookup"><span data-stu-id="7634a-213">Session</span></span>|
|<span data-ttu-id="7634a-214">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-214">Eventual</span></span>|<span data-ttu-id="7634a-215">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-215">Eventual</span></span>|<span data-ttu-id="7634a-216">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-216">Eventual</span></span>|<span data-ttu-id="7634a-217">Eventual</span><span class="sxs-lookup"><span data-stu-id="7634a-217">Eventual</span></span>|

<span data-ttu-id="7634a-218">The following code sample show how create an Azure Cosmos DB collection by using the .NET SDK with Consistent indexing on all document insertions.</span><span class="sxs-lookup"><span data-stu-id="7634a-218">The following code sample show how create an Azure Cosmos DB collection by using the .NET SDK with Consistent indexing on all document insertions.</span></span>

     // Default collection creates a Hash index for all string fields and a Range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a><span data-ttu-id="7634a-219">Index paths</span><span class="sxs-lookup"><span data-stu-id="7634a-219">Index paths</span></span>
<span data-ttu-id="7634a-220">Azure Cosmos DB models JSON documents and the index as trees.</span><span class="sxs-lookup"><span data-stu-id="7634a-220">Azure Cosmos DB models JSON documents and the index as trees.</span></span> <span data-ttu-id="7634a-221">You can tune to policies for paths within the tree.</span><span class="sxs-lookup"><span data-stu-id="7634a-221">You can tune to policies for paths within the tree.</span></span> <span data-ttu-id="7634a-222">Within documents, you can choose the paths to include or exclude from indexing.</span><span class="sxs-lookup"><span data-stu-id="7634a-222">Within documents, you can choose the paths to include or exclude from indexing.</span></span> <span data-ttu-id="7634a-223">This can offer improved write performance and lower index storage for scenarios in which the query patterns are known beforehand.</span><span class="sxs-lookup"><span data-stu-id="7634a-223">This can offer improved write performance and lower index storage for scenarios in which the query patterns are known beforehand.</span></span>

<span data-ttu-id="7634a-224">Index paths start with the root (/) and typically end with the ?</span><span class="sxs-lookup"><span data-stu-id="7634a-224">Index paths start with the root (/) and typically end with the ?</span></span> <span data-ttu-id="7634a-225">wildcard operator.</span><span class="sxs-lookup"><span data-stu-id="7634a-225">wildcard operator.</span></span> <span data-ttu-id="7634a-226">This denotes that there are multiple possible values for the prefix.</span><span class="sxs-lookup"><span data-stu-id="7634a-226">This denotes that there are multiple possible values for the prefix.</span></span> <span data-ttu-id="7634a-227">For example, to serve SELECT \* FROM Families F WHERE F.familyName = "Andersen", you must include an index path for /familyName/?</span><span class="sxs-lookup"><span data-stu-id="7634a-227">For example, to serve SELECT \* FROM Families F WHERE F.familyName = "Andersen", you must include an index path for /familyName/?</span></span> <span data-ttu-id="7634a-228">in the collection’s index policy.</span><span class="sxs-lookup"><span data-stu-id="7634a-228">in the collection’s index policy.</span></span>

<span data-ttu-id="7634a-229">Index paths can also use the \* wildcard operator to specify the behavior for paths recursively under the prefix.</span><span class="sxs-lookup"><span data-stu-id="7634a-229">Index paths can also use the \* wildcard operator to specify the behavior for paths recursively under the prefix.</span></span> <span data-ttu-id="7634a-230">For example, /payload/\* can be used to exclude everything under the payload property from indexing.</span><span class="sxs-lookup"><span data-stu-id="7634a-230">For example, /payload/\* can be used to exclude everything under the payload property from indexing.</span></span>

<span data-ttu-id="7634a-231">Here are the common patterns for specifying index paths:</span><span class="sxs-lookup"><span data-stu-id="7634a-231">Here are the common patterns for specifying index paths:</span></span>

| <span data-ttu-id="7634a-232">Path</span><span class="sxs-lookup"><span data-stu-id="7634a-232">Path</span></span>                | <span data-ttu-id="7634a-233">Description/use case</span><span class="sxs-lookup"><span data-stu-id="7634a-233">Description/use case</span></span>                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | <span data-ttu-id="7634a-234">Default path for collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-234">Default path for collection.</span></span> <span data-ttu-id="7634a-235">Recursive and applies to the entire document tree.</span><span class="sxs-lookup"><span data-stu-id="7634a-235">Recursive and applies to the entire document tree.</span></span>                                                                                                                                                                                                                                   |
| <span data-ttu-id="7634a-236">/prop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-236">/prop/?</span></span>             | <span data-ttu-id="7634a-237">Index path required to serve queries like the following (with Hash or Range types, respectively):</span><span class="sxs-lookup"><span data-stu-id="7634a-237">Index path required to serve queries like the following (with Hash or Range types, respectively):</span></span><br><br><span data-ttu-id="7634a-238">SELECT FROM collection c WHERE c.prop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-238">SELECT FROM collection c WHERE c.prop = "value"</span></span><br><br><span data-ttu-id="7634a-239">SELECT FROM collection c WHERE c.prop > 5</span><span class="sxs-lookup"><span data-stu-id="7634a-239">SELECT FROM collection c WHERE c.prop > 5</span></span><br><br><span data-ttu-id="7634a-240">SELECT FROM collection c ORDER BY c.prop</span><span class="sxs-lookup"><span data-stu-id="7634a-240">SELECT FROM collection c ORDER BY c.prop</span></span>                                                                       |
| <span data-ttu-id="7634a-241">/prop/\*</span><span class="sxs-lookup"><span data-stu-id="7634a-241">/prop/\*</span></span>             | <span data-ttu-id="7634a-242">Index path for all paths under the specified label.</span><span class="sxs-lookup"><span data-stu-id="7634a-242">Index path for all paths under the specified label.</span></span> <span data-ttu-id="7634a-243">Works with the following queries</span><span class="sxs-lookup"><span data-stu-id="7634a-243">Works with the following queries</span></span><br><br><span data-ttu-id="7634a-244">SELECT FROM collection c WHERE c.prop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-244">SELECT FROM collection c WHERE c.prop = "value"</span></span><br><br><span data-ttu-id="7634a-245">SELECT FROM collection c WHERE c.prop.subprop > 5</span><span class="sxs-lookup"><span data-stu-id="7634a-245">SELECT FROM collection c WHERE c.prop.subprop > 5</span></span><br><br><span data-ttu-id="7634a-246">SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-246">SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"</span></span><br><br><span data-ttu-id="7634a-247">SELECT FROM collection c ORDER BY c.prop</span><span class="sxs-lookup"><span data-stu-id="7634a-247">SELECT FROM collection c ORDER BY c.prop</span></span>         |
| <span data-ttu-id="7634a-248">/props/[]/?</span><span class="sxs-lookup"><span data-stu-id="7634a-248">/props/[]/?</span></span>         | <span data-ttu-id="7634a-249">Index path required to serve iteration and JOIN queries against arrays of scalars like ["a", "b", "c"]:</span><span class="sxs-lookup"><span data-stu-id="7634a-249">Index path required to serve iteration and JOIN queries against arrays of scalars like ["a", "b", "c"]:</span></span><br><br><span data-ttu-id="7634a-250">SELECT tag FROM tag IN collection.props WHERE tag = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-250">SELECT tag FROM tag IN collection.props WHERE tag = "value"</span></span><br><br><span data-ttu-id="7634a-251">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5</span><span class="sxs-lookup"><span data-stu-id="7634a-251">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5</span></span>                                                                         |
| <span data-ttu-id="7634a-252">/props/[]/subprop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-252">/props/[]/subprop/?</span></span> | <span data-ttu-id="7634a-253">Index path required to serve iteration and JOIN queries against arrays of objects like [{subprop: "a"}, {subprop: "b"}]:</span><span class="sxs-lookup"><span data-stu-id="7634a-253">Index path required to serve iteration and JOIN queries against arrays of objects like [{subprop: "a"}, {subprop: "b"}]:</span></span><br><br><span data-ttu-id="7634a-254">SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-254">SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"</span></span><br><br><span data-ttu-id="7634a-255">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-255">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"</span></span>                                  |
| <span data-ttu-id="7634a-256">/prop/subprop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-256">/prop/subprop/?</span></span>     | <span data-ttu-id="7634a-257">Index path required to serve queries (with Hash or Range types, respectively):</span><span class="sxs-lookup"><span data-stu-id="7634a-257">Index path required to serve queries (with Hash or Range types, respectively):</span></span><br><br><span data-ttu-id="7634a-258">SELECT FROM collection c WHERE c.prop.subprop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-258">SELECT FROM collection c WHERE c.prop.subprop = "value"</span></span><br><br><span data-ttu-id="7634a-259">SELECT FROM collection c WHERE c.prop.subprop > 5</span><span class="sxs-lookup"><span data-stu-id="7634a-259">SELECT FROM collection c WHERE c.prop.subprop > 5</span></span>                                                                                                                    |

> [!NOTE]
> <span data-ttu-id="7634a-260">When you set custom index paths, you are required to specify the default indexing rule for the entire document tree, which is denoted by the special path "/\*".</span><span class="sxs-lookup"><span data-stu-id="7634a-260">When you set custom index paths, you are required to specify the default indexing rule for the entire document tree, which is denoted by the special path "/\*".</span></span> 
> 
> 

<span data-ttu-id="7634a-261">The following example configures a specific path with Range index and a custom precision value of 20 bytes:</span><span class="sxs-lookup"><span data-stu-id="7634a-261">The following example configures a specific path with Range index and a custom precision value of 20 bytes:</span></span>

```
    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);
```

<span data-ttu-id="7634a-262">When a path is added for indexing, both numbers and strings within those paths are indexed.</span><span class="sxs-lookup"><span data-stu-id="7634a-262">When a path is added for indexing, both numbers and strings within those paths are indexed.</span></span> <span data-ttu-id="7634a-263">So even though you define indexing for strings only, Azure Cosmos DB adds default definition for numbers as well.</span><span class="sxs-lookup"><span data-stu-id="7634a-263">So even though you define indexing for strings only, Azure Cosmos DB adds default definition for numbers as well.</span></span> <span data-ttu-id="7634a-264">In other words, Azure Cosmos DB has the ability for path exclusion from indexing policy, but not type exclusion from a specific path.</span><span class="sxs-lookup"><span data-stu-id="7634a-264">In other words, Azure Cosmos DB has the ability for path exclusion from indexing policy, but not type exclusion from a specific path.</span></span> <span data-ttu-id="7634a-265">Following is an example, note that only one index is specified for both paths (Path =  "/\*" and Path =  "/\"attr1\"/?") but the Number datatype is also added to the result.</span><span class="sxs-lookup"><span data-stu-id="7634a-265">Following is an example, note that only one index is specified for both paths (Path =  "/\*" and Path =  "/\"attr1\"/?") but the Number datatype is also added to the result.</span></span>

```
var indices = new[]{
                new IncludedPath  {
                    Indexes = new Collection<Index>
                    {
                        new RangeIndex(DataType.String) { Precision = 3 }// <- note: only 1 index specified
                    },
                    Path =  "/*"
                },
                new IncludedPath  {
                    Indexes = new Collection<Index>
                    {
                        new RangeIndex(DataType.String) { Precision = 3 } // <- note: only 1 index specified
                    },
                    Path =  "/\"attr1\"/?"
                }
            };...

            foreach (var index in indices)
            {
                documentCollection.IndexingPolicy.IncludedPaths.Add(index);
            }
```

<span data-ttu-id="7634a-266">Result of index creation:</span><span class="sxs-lookup"><span data-stu-id="7634a-266">Result of index creation:</span></span>

```json
{
    "indexingMode": "consistent",
    "automatic": true,
    "includedPaths": [
        {
            "path": "/*",
            "indexes": [
                {
                    "kind": "Range",
                    "dataType": "String",
                    "precision": 3
                },
                {
                    "kind": "Range",
                    "dataType": "Number",
                    "precision": -1
                }
            ]
        },
        {
            "path": "/\"attr\"/?",
            "indexes": [
                {
                    "kind": "Range",
                    "dataType": "String",
                    "precision": 3
                },
                {
                    "kind": "Range",
                    "dataType": "Number",
                    "precision": -1
                }
            ]
        }
    ],
}
```

### <a name="index-data-types-kinds-and-precisions"></a><span data-ttu-id="7634a-267">Index data types, kinds, and precisions</span><span class="sxs-lookup"><span data-stu-id="7634a-267">Index data types, kinds, and precisions</span></span>
<span data-ttu-id="7634a-268">You have multiple options when you configure the indexing policy for a path.</span><span class="sxs-lookup"><span data-stu-id="7634a-268">You have multiple options when you configure the indexing policy for a path.</span></span> <span data-ttu-id="7634a-269">You can specify one or more indexing definitions for every path:</span><span class="sxs-lookup"><span data-stu-id="7634a-269">You can specify one or more indexing definitions for every path:</span></span>

* <span data-ttu-id="7634a-270">**Data type**: String, Number, Point, Polygon, or LineString (can contain only one entry per data type per path).</span><span class="sxs-lookup"><span data-stu-id="7634a-270">**Data type**: String, Number, Point, Polygon, or LineString (can contain only one entry per data type per path).</span></span>
* <span data-ttu-id="7634a-271">**Index kind**: Hash (equality queries), Range (equality, range or ORDER BY queries), or Spatial (spatial queries) .</span><span class="sxs-lookup"><span data-stu-id="7634a-271">**Index kind**: Hash (equality queries), Range (equality, range or ORDER BY queries), or Spatial (spatial queries) .</span></span>
* <span data-ttu-id="7634a-272">**Precision**: For a Hash index, this varies from 1 to 8 for both strings and numbers.</span><span class="sxs-lookup"><span data-stu-id="7634a-272">**Precision**: For a Hash index, this varies from 1 to 8 for both strings and numbers.</span></span> <span data-ttu-id="7634a-273">The default is 3.</span><span class="sxs-lookup"><span data-stu-id="7634a-273">The default is 3.</span></span> <span data-ttu-id="7634a-274">For a Range index, this value can be -1 (maximum precision).</span><span class="sxs-lookup"><span data-stu-id="7634a-274">For a Range index, this value can be -1 (maximum precision).</span></span> <span data-ttu-id="7634a-275">It can vary from between 1 and 100 (maximum precision) for string or number values.</span><span class="sxs-lookup"><span data-stu-id="7634a-275">It can vary from between 1 and 100 (maximum precision) for string or number values.</span></span>

#### <a name="index-kind"></a><span data-ttu-id="7634a-276">Index kind</span><span class="sxs-lookup"><span data-stu-id="7634a-276">Index kind</span></span>
<span data-ttu-id="7634a-277">Azure Cosmos DB supports Hash index and Range index kinds for every path that can be configured for String or Number data types, or both.</span><span class="sxs-lookup"><span data-stu-id="7634a-277">Azure Cosmos DB supports Hash index and Range index kinds for every path that can be configured for String or Number data types, or both.</span></span>

* <span data-ttu-id="7634a-278">**Hash** supports efficient equality and JOIN queries.</span><span class="sxs-lookup"><span data-stu-id="7634a-278">**Hash** supports efficient equality and JOIN queries.</span></span> <span data-ttu-id="7634a-279">For most use cases, Hash indexes don't need a higher precision than the default value of 3 bytes.</span><span class="sxs-lookup"><span data-stu-id="7634a-279">For most use cases, Hash indexes don't need a higher precision than the default value of 3 bytes.</span></span> <span data-ttu-id="7634a-280">The data type can be String or Number.</span><span class="sxs-lookup"><span data-stu-id="7634a-280">The data type can be String or Number.</span></span>
* <span data-ttu-id="7634a-281">**Range** supports efficient equality queries, range queries (using >, <, >=, <=, !=), and ORDER BY queries.</span><span class="sxs-lookup"><span data-stu-id="7634a-281">**Range** supports efficient equality queries, range queries (using >, <, >=, <=, !=), and ORDER BY queries.</span></span> <span data-ttu-id="7634a-282">ORDER By queries by default also require maximum index precision (-1).</span><span class="sxs-lookup"><span data-stu-id="7634a-282">ORDER By queries by default also require maximum index precision (-1).</span></span> <span data-ttu-id="7634a-283">The data type can be String or Number.</span><span class="sxs-lookup"><span data-stu-id="7634a-283">The data type can be String or Number.</span></span>

<span data-ttu-id="7634a-284">Azure Cosmos DB also supports the Spatial index kind for every path that can be specified for the Point, Polygon, or LineString data types.</span><span class="sxs-lookup"><span data-stu-id="7634a-284">Azure Cosmos DB also supports the Spatial index kind for every path that can be specified for the Point, Polygon, or LineString data types.</span></span> <span data-ttu-id="7634a-285">The value at the specified path must be a valid GeoJSON fragment like `{"type": "Point", "coordinates": [0.0, 10.0]}`.</span><span class="sxs-lookup"><span data-stu-id="7634a-285">The value at the specified path must be a valid GeoJSON fragment like `{"type": "Point", "coordinates": [0.0, 10.0]}`.</span></span>

* <span data-ttu-id="7634a-286">**Spatial** supports efficient spatial (within and distance) queries.</span><span class="sxs-lookup"><span data-stu-id="7634a-286">**Spatial** supports efficient spatial (within and distance) queries.</span></span> <span data-ttu-id="7634a-287">The data type can be Point, Polygon, or LineString.</span><span class="sxs-lookup"><span data-stu-id="7634a-287">The data type can be Point, Polygon, or LineString.</span></span>

> [!NOTE]
> <span data-ttu-id="7634a-288">Azure Cosmos DB supports automatic indexing of Point, Polygon, and LineString data types.</span><span class="sxs-lookup"><span data-stu-id="7634a-288">Azure Cosmos DB supports automatic indexing of Point, Polygon, and LineString data types.</span></span>
> 
> 

<span data-ttu-id="7634a-289">Here are the supported index kinds and examples of queries that they can be used to serve:</span><span class="sxs-lookup"><span data-stu-id="7634a-289">Here are the supported index kinds and examples of queries that they can be used to serve:</span></span>

| <span data-ttu-id="7634a-290">Index kind</span><span class="sxs-lookup"><span data-stu-id="7634a-290">Index kind</span></span> | <span data-ttu-id="7634a-291">Description/use case</span><span class="sxs-lookup"><span data-stu-id="7634a-291">Description/use case</span></span>                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="7634a-292">Hash</span><span class="sxs-lookup"><span data-stu-id="7634a-292">Hash</span></span>       | <span data-ttu-id="7634a-293">Hash over /prop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-293">Hash over /prop/?</span></span> <span data-ttu-id="7634a-294">(or /) can be used to serve the following queries efficiently:</span><span class="sxs-lookup"><span data-stu-id="7634a-294">(or /) can be used to serve the following queries efficiently:</span></span><br><br><span data-ttu-id="7634a-295">SELECT FROM collection c WHERE c.prop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-295">SELECT FROM collection c WHERE c.prop = "value"</span></span><br><br><span data-ttu-id="7634a-296">Hash over /props/[]/?</span><span class="sxs-lookup"><span data-stu-id="7634a-296">Hash over /props/[]/?</span></span> <span data-ttu-id="7634a-297">(or / or /props/) can be used to serve the following queries efficiently:</span><span class="sxs-lookup"><span data-stu-id="7634a-297">(or / or /props/) can be used to serve the following queries efficiently:</span></span><br><br><span data-ttu-id="7634a-298">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5</span><span class="sxs-lookup"><span data-stu-id="7634a-298">SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5</span></span>                                                                                                                       |
| <span data-ttu-id="7634a-299">Range</span><span class="sxs-lookup"><span data-stu-id="7634a-299">Range</span></span>      | <span data-ttu-id="7634a-300">Range over /prop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-300">Range over /prop/?</span></span> <span data-ttu-id="7634a-301">(or /) can be used to serve the following queries efficiently:</span><span class="sxs-lookup"><span data-stu-id="7634a-301">(or /) can be used to serve the following queries efficiently:</span></span><br><br><span data-ttu-id="7634a-302">SELECT FROM collection c WHERE c.prop = "value"</span><span class="sxs-lookup"><span data-stu-id="7634a-302">SELECT FROM collection c WHERE c.prop = "value"</span></span><br><br><span data-ttu-id="7634a-303">SELECT FROM collection c WHERE c.prop > 5</span><span class="sxs-lookup"><span data-stu-id="7634a-303">SELECT FROM collection c WHERE c.prop > 5</span></span><br><br><span data-ttu-id="7634a-304">SELECT FROM collection c ORDER BY c.prop</span><span class="sxs-lookup"><span data-stu-id="7634a-304">SELECT FROM collection c ORDER BY c.prop</span></span>                                                                                                                                                                                                              |
| <span data-ttu-id="7634a-305">Spatial</span><span class="sxs-lookup"><span data-stu-id="7634a-305">Spatial</span></span>     | <span data-ttu-id="7634a-306">Range over /prop/?</span><span class="sxs-lookup"><span data-stu-id="7634a-306">Range over /prop/?</span></span> <span data-ttu-id="7634a-307">(or /) can be used to serve the following queries efficiently:</span><span class="sxs-lookup"><span data-stu-id="7634a-307">(or /) can be used to serve the following queries efficiently:</span></span><br><br><span data-ttu-id="7634a-308">SELECT FROM collection c</span><span class="sxs-lookup"><span data-stu-id="7634a-308">SELECT FROM collection c</span></span><br><br><span data-ttu-id="7634a-309">WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40</span><span class="sxs-lookup"><span data-stu-id="7634a-309">WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40</span></span><br><br><span data-ttu-id="7634a-310">SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled</span><span class="sxs-lookup"><span data-stu-id="7634a-310">SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled</span></span><br><br><span data-ttu-id="7634a-311">SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled</span><span class="sxs-lookup"><span data-stu-id="7634a-311">SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled</span></span>              |

<span data-ttu-id="7634a-312">By default, an error is returned for queries with range operators such as >= if there is no Range index (of any precision) to signal that a scan might be necessary to serve the query.</span><span class="sxs-lookup"><span data-stu-id="7634a-312">By default, an error is returned for queries with range operators such as >= if there is no Range index (of any precision) to signal that a scan might be necessary to serve the query.</span></span> <span data-ttu-id="7634a-313">Range queries can be performed without a Range index by using the **x-ms-documentdb-enable-scan** header in the REST API or the **EnableScanInQuery** request option by using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7634a-313">Range queries can be performed without a Range index by using the **x-ms-documentdb-enable-scan** header in the REST API or the **EnableScanInQuery** request option by using the .NET SDK.</span></span> <span data-ttu-id="7634a-314">If there are any other filters in the query that Azure Cosmos DB can use the index to filter against, no error is returned.</span><span class="sxs-lookup"><span data-stu-id="7634a-314">If there are any other filters in the query that Azure Cosmos DB can use the index to filter against, no error is returned.</span></span>

<span data-ttu-id="7634a-315">The same rules apply for spatial queries.</span><span class="sxs-lookup"><span data-stu-id="7634a-315">The same rules apply for spatial queries.</span></span> <span data-ttu-id="7634a-316">By default, an error is returned for spatial queries if there is no spatial index, and there are no other filters that can be served from the index.</span><span class="sxs-lookup"><span data-stu-id="7634a-316">By default, an error is returned for spatial queries if there is no spatial index, and there are no other filters that can be served from the index.</span></span> <span data-ttu-id="7634a-317">They can be performed as a scan by using **x-ms-documentdb-enable-scan** or **EnableScanInQuery**.</span><span class="sxs-lookup"><span data-stu-id="7634a-317">They can be performed as a scan by using **x-ms-documentdb-enable-scan** or **EnableScanInQuery**.</span></span>

#### <a name="index-precision"></a><span data-ttu-id="7634a-318">Index precision</span><span class="sxs-lookup"><span data-stu-id="7634a-318">Index precision</span></span>
<span data-ttu-id="7634a-319">You can use index precision to make trade-offs between index storage overhead and query performance.</span><span class="sxs-lookup"><span data-stu-id="7634a-319">You can use index precision to make trade-offs between index storage overhead and query performance.</span></span> <span data-ttu-id="7634a-320">For numbers, we recommend using the default precision configuration of -1 (maximum).</span><span class="sxs-lookup"><span data-stu-id="7634a-320">For numbers, we recommend using the default precision configuration of -1 (maximum).</span></span> <span data-ttu-id="7634a-321">Because numbers are 8 bytes in JSON, this is equivalent to a configuration of 8 bytes.</span><span class="sxs-lookup"><span data-stu-id="7634a-321">Because numbers are 8 bytes in JSON, this is equivalent to a configuration of 8 bytes.</span></span> <span data-ttu-id="7634a-322">Choosing a lower value for precision, such as 1 through 7, means that values within some ranges map to the same index entry.</span><span class="sxs-lookup"><span data-stu-id="7634a-322">Choosing a lower value for precision, such as 1 through 7, means that values within some ranges map to the same index entry.</span></span> <span data-ttu-id="7634a-323">Therefore, you reduce index storage space, but query execution might have to process more documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-323">Therefore, you reduce index storage space, but query execution might have to process more documents.</span></span> <span data-ttu-id="7634a-324">Consequently, it consumes more throughput in request units.</span><span class="sxs-lookup"><span data-stu-id="7634a-324">Consequently, it consumes more throughput in request units.</span></span>

<span data-ttu-id="7634a-325">Index precision configuration has more practical application with string ranges.</span><span class="sxs-lookup"><span data-stu-id="7634a-325">Index precision configuration has more practical application with string ranges.</span></span> <span data-ttu-id="7634a-326">Because strings can be any arbitrary length, the choice of the index precision might affect the performance of string range queries.</span><span class="sxs-lookup"><span data-stu-id="7634a-326">Because strings can be any arbitrary length, the choice of the index precision might affect the performance of string range queries.</span></span> <span data-ttu-id="7634a-327">It also might affect the amount of index storage space that's required.</span><span class="sxs-lookup"><span data-stu-id="7634a-327">It also might affect the amount of index storage space that's required.</span></span> <span data-ttu-id="7634a-328">String Range indexes can be configured with 1 through 100 or -1 (maximum).</span><span class="sxs-lookup"><span data-stu-id="7634a-328">String Range indexes can be configured with 1 through 100 or -1 (maximum).</span></span> <span data-ttu-id="7634a-329">If you want to perform ORDER BY queries against string properties, you must specify a precision of -1 for the corresponding paths.</span><span class="sxs-lookup"><span data-stu-id="7634a-329">If you want to perform ORDER BY queries against string properties, you must specify a precision of -1 for the corresponding paths.</span></span>

<span data-ttu-id="7634a-330">Spatial indexes always use the default index precision for all types (Point, LineString, and Polygon).</span><span class="sxs-lookup"><span data-stu-id="7634a-330">Spatial indexes always use the default index precision for all types (Point, LineString, and Polygon).</span></span> <span data-ttu-id="7634a-331">The default index precision for spatial indexes can't be overridden.</span><span class="sxs-lookup"><span data-stu-id="7634a-331">The default index precision for spatial indexes can't be overridden.</span></span> 

<span data-ttu-id="7634a-332">The following example shows how to increase the precision for Range indexes in a collection by using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7634a-332">The following example shows how to increase the precision for Range indexes in a collection by using the .NET SDK.</span></span> 

<span data-ttu-id="7634a-333">**Create a collection with a custom index precision**</span><span class="sxs-lookup"><span data-stu-id="7634a-333">**Create a collection with a custom index precision**</span></span>

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override the default policy for strings to Range indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> <span data-ttu-id="7634a-334">Azure Cosmos DB returns an error when a query uses ORDER BY but doesn't have a Range index against the queried path with the maximum precision.</span><span class="sxs-lookup"><span data-stu-id="7634a-334">Azure Cosmos DB returns an error when a query uses ORDER BY but doesn't have a Range index against the queried path with the maximum precision.</span></span> 
> 
> 

<span data-ttu-id="7634a-335">Similarly, you can completely exclude paths from indexing.</span><span class="sxs-lookup"><span data-stu-id="7634a-335">Similarly, you can completely exclude paths from indexing.</span></span> <span data-ttu-id="7634a-336">The next example shows how to exclude an entire section of the documents (a *subtree*) from indexing by using the \* wildcard operator.</span><span class="sxs-lookup"><span data-stu-id="7634a-336">The next example shows how to exclude an entire section of the documents (a *subtree*) from indexing by using the \* wildcard operator.</span></span>

    var excluded = new DocumentCollection { Id = "excludedPathCollection" };
    excluded.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    excluded.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opt-in-and-opt-out-of-indexing"></a><span data-ttu-id="7634a-337">Opt in and opt out of indexing</span><span class="sxs-lookup"><span data-stu-id="7634a-337">Opt in and opt out of indexing</span></span>
<span data-ttu-id="7634a-338">You can choose whether you want the collection to automatically index all documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-338">You can choose whether you want the collection to automatically index all documents.</span></span> <span data-ttu-id="7634a-339">By default, all documents are automatically indexed, but you can turn off automatic indexing.</span><span class="sxs-lookup"><span data-stu-id="7634a-339">By default, all documents are automatically indexed, but you can turn off automatic indexing.</span></span> <span data-ttu-id="7634a-340">When indexing is turned off, documents can be accessed only through their self-links or by queries by using the document ID.</span><span class="sxs-lookup"><span data-stu-id="7634a-340">When indexing is turned off, documents can be accessed only through their self-links or by queries by using the document ID.</span></span>

<span data-ttu-id="7634a-341">With automatic indexing turned off, you can still selectively add only specific documents to the index.</span><span class="sxs-lookup"><span data-stu-id="7634a-341">With automatic indexing turned off, you can still selectively add only specific documents to the index.</span></span> <span data-ttu-id="7634a-342">Conversely, you can leave automatic indexing on and selectively choose to exclude specific documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-342">Conversely, you can leave automatic indexing on and selectively choose to exclude specific documents.</span></span> <span data-ttu-id="7634a-343">Indexing on/off configurations are useful when you have only a subset of documents that needs to be queried.</span><span class="sxs-lookup"><span data-stu-id="7634a-343">Indexing on/off configurations are useful when you have only a subset of documents that needs to be queried.</span></span>

<span data-ttu-id="7634a-344">The following sample shows how to include a document explicitly by using the [SQL API .NET SDK](https://docs.microsoft.com/azure/cosmos-db/sql-api-sdk-dotnet) and the [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) property.</span><span class="sxs-lookup"><span data-stu-id="7634a-344">The following sample shows how to include a document explicitly by using the [SQL API .NET SDK](https://docs.microsoft.com/azure/cosmos-db/sql-api-sdk-dotnet) and the [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) property.</span></span>

    // If you want to override the default collection behavior to either
    // exclude (or include) a document in indexing,
    // use the RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modify-the-indexing-policy-of-a-collection"></a><span data-ttu-id="7634a-345">Modify the indexing policy of a collection</span><span class="sxs-lookup"><span data-stu-id="7634a-345">Modify the indexing policy of a collection</span></span>
<span data-ttu-id="7634a-346">In Azure Cosmos DB, you can make changes to the indexing policy of a collection on the fly.</span><span class="sxs-lookup"><span data-stu-id="7634a-346">In Azure Cosmos DB, you can make changes to the indexing policy of a collection on the fly.</span></span> <span data-ttu-id="7634a-347">A change in indexing policy on an Azure Cosmos DB collection can lead to a change in the shape of the index.</span><span class="sxs-lookup"><span data-stu-id="7634a-347">A change in indexing policy on an Azure Cosmos DB collection can lead to a change in the shape of the index.</span></span> <span data-ttu-id="7634a-348">The change affects the paths that can be indexed, their precision, and the consistency model of the index itself.</span><span class="sxs-lookup"><span data-stu-id="7634a-348">The change affects the paths that can be indexed, their precision, and the consistency model of the index itself.</span></span> <span data-ttu-id="7634a-349">A change in indexing policy effectively requires a transformation of the old index into a new index.</span><span class="sxs-lookup"><span data-stu-id="7634a-349">A change in indexing policy effectively requires a transformation of the old index into a new index.</span></span> 

<span data-ttu-id="7634a-350">**Online index transformations**</span><span class="sxs-lookup"><span data-stu-id="7634a-350">**Online index transformations**</span></span>

![How indexing works – Azure Cosmos DB online index transformations](./media/indexing-policies/index-transformations.png)

<span data-ttu-id="7634a-352">Index transformations are made online.</span><span class="sxs-lookup"><span data-stu-id="7634a-352">Index transformations are made online.</span></span> <span data-ttu-id="7634a-353">This means that the documents indexed per the old policy are efficiently transformed per the new policy *without affecting the write availability or the provisioned throughput* of the collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-353">This means that the documents indexed per the old policy are efficiently transformed per the new policy *without affecting the write availability or the provisioned throughput* of the collection.</span></span> <span data-ttu-id="7634a-354">The consistency of read and write operations made by using the REST API, SDKs, or from within stored procedures and triggers is not affected during index transformation.</span><span class="sxs-lookup"><span data-stu-id="7634a-354">The consistency of read and write operations made by using the REST API, SDKs, or from within stored procedures and triggers is not affected during index transformation.</span></span> 

<span data-ttu-id="7634a-355">Changing indexing policy is an asynchronous process and the time to complete the operation depends on the number of documents, provisioned RUs, and size of documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-355">Changing indexing policy is an asynchronous process and the time to complete the operation depends on the number of documents, provisioned RUs, and size of documents.</span></span> <span data-ttu-id="7634a-356">While re-indexing is in progress, your query may not return all matching results if the query uses the index that is being modified and queries will not return any errors/failures.</span><span class="sxs-lookup"><span data-stu-id="7634a-356">While re-indexing is in progress, your query may not return all matching results if the query uses the index that is being modified and queries will not return any errors/failures.</span></span> <span data-ttu-id="7634a-357">While re-indexing is in progress, queries are eventually consistent regardless of the indexing mode configuration(Consistent or Lazy).</span><span class="sxs-lookup"><span data-stu-id="7634a-357">While re-indexing is in progress, queries are eventually consistent regardless of the indexing mode configuration(Consistent or Lazy).</span></span> <span data-ttu-id="7634a-358">After the index transformation is complete, you will continue to see consistent results.</span><span class="sxs-lookup"><span data-stu-id="7634a-358">After the index transformation is complete, you will continue to see consistent results.</span></span> <span data-ttu-id="7634a-359">This also applies to queries from all interfaces: REST API, SDKs, and from within stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="7634a-359">This also applies to queries from all interfaces: REST API, SDKs, and from within stored procedures and triggers.</span></span> <span data-ttu-id="7634a-360">Just like with Lazy indexing, index transformation is performed asynchronously in the background on the replicas by using the spare resources that are available for a specific replica.</span><span class="sxs-lookup"><span data-stu-id="7634a-360">Just like with Lazy indexing, index transformation is performed asynchronously in the background on the replicas by using the spare resources that are available for a specific replica.</span></span> 

<span data-ttu-id="7634a-361">Index transformations are also made in place.</span><span class="sxs-lookup"><span data-stu-id="7634a-361">Index transformations are also made in place.</span></span> <span data-ttu-id="7634a-362">Azure Cosmos DB doesn't maintain two copies of the index and swap out the old index with the new one.</span><span class="sxs-lookup"><span data-stu-id="7634a-362">Azure Cosmos DB doesn't maintain two copies of the index and swap out the old index with the new one.</span></span> <span data-ttu-id="7634a-363">This means that no additional disk space is required or consumed in your collections while index transformations occur.</span><span class="sxs-lookup"><span data-stu-id="7634a-363">This means that no additional disk space is required or consumed in your collections while index transformations occur.</span></span>

<span data-ttu-id="7634a-364">When you change indexing policy, changes are applied to move from the old index to the new primarily based on the indexing mode configurations.</span><span class="sxs-lookup"><span data-stu-id="7634a-364">When you change indexing policy, changes are applied to move from the old index to the new primarily based on the indexing mode configurations.</span></span> <span data-ttu-id="7634a-365">Indexing mode configurations play a larger role than other values like included/excluded paths, index kinds, and precisions.</span><span class="sxs-lookup"><span data-stu-id="7634a-365">Indexing mode configurations play a larger role than other values like included/excluded paths, index kinds, and precisions.</span></span> 

<span data-ttu-id="7634a-366">If your old and new policies both use Consistent indexing, Azure Cosmos DB performs an online index transformation.</span><span class="sxs-lookup"><span data-stu-id="7634a-366">If your old and new policies both use Consistent indexing, Azure Cosmos DB performs an online index transformation.</span></span> <span data-ttu-id="7634a-367">You can't apply another indexing policy change that has Consistent indexing mode while the transformation is in progress.</span><span class="sxs-lookup"><span data-stu-id="7634a-367">You can't apply another indexing policy change that has Consistent indexing mode while the transformation is in progress.</span></span> <span data-ttu-id="7634a-368">However, you can move to Lazy or None indexing mode while a transformation is in progress:</span><span class="sxs-lookup"><span data-stu-id="7634a-368">However, you can move to Lazy or None indexing mode while a transformation is in progress:</span></span> 

* <span data-ttu-id="7634a-369">When you move to Lazy, the index policy change is effective immediately.</span><span class="sxs-lookup"><span data-stu-id="7634a-369">When you move to Lazy, the index policy change is effective immediately.</span></span> <span data-ttu-id="7634a-370">Azure Cosmos DB starts re-creating the index asynchronously.</span><span class="sxs-lookup"><span data-stu-id="7634a-370">Azure Cosmos DB starts re-creating the index asynchronously.</span></span> 
* <span data-ttu-id="7634a-371">When you move to None, the index is dropped immediately.</span><span class="sxs-lookup"><span data-stu-id="7634a-371">When you move to None, the index is dropped immediately.</span></span> <span data-ttu-id="7634a-372">Moving to None is useful when you want to cancel an in-progress transformation, and start fresh with a different indexing policy.</span><span class="sxs-lookup"><span data-stu-id="7634a-372">Moving to None is useful when you want to cancel an in-progress transformation, and start fresh with a different indexing policy.</span></span> 

<span data-ttu-id="7634a-373">The following code snippet shows how to modify a collection's indexing policy from Consistent indexing mode to Lazy indexing mode.</span><span class="sxs-lookup"><span data-stu-id="7634a-373">The following code snippet shows how to modify a collection's indexing policy from Consistent indexing mode to Lazy indexing mode.</span></span> <span data-ttu-id="7634a-374">If you’re using the .NET SDK, you can kick off an indexing policy change by using the new **ReplaceDocumentCollectionAsync** method.</span><span class="sxs-lookup"><span data-stu-id="7634a-374">If you’re using the .NET SDK, you can kick off an indexing policy change by using the new **ReplaceDocumentCollectionAsync** method.</span></span>

<span data-ttu-id="7634a-375">**Modify indexing policy from Consistent to Lazy**</span><span class="sxs-lookup"><span data-stu-id="7634a-375">**Modify indexing policy from Consistent to Lazy**</span></span>

    // Switch to Lazy indexing mode.
    Console.WriteLine("Changing from Default to Lazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);

<span data-ttu-id="7634a-376">**Track progress of index transformation**</span><span class="sxs-lookup"><span data-stu-id="7634a-376">**Track progress of index transformation**</span></span>

<span data-ttu-id="7634a-377">You can track the percentage progress of the index transformation to a Consistent index by using the **IndexTransformationProgress** response property from a **ReadDocumentCollectionAsync** call.</span><span class="sxs-lookup"><span data-stu-id="7634a-377">You can track the percentage progress of the index transformation to a Consistent index by using the **IndexTransformationProgress** response property from a **ReadDocumentCollectionAsync** call.</span></span> <span data-ttu-id="7634a-378">Other SDKs, and the REST API, support equivalent properties and methods for making indexing policy changes.</span><span class="sxs-lookup"><span data-stu-id="7634a-378">Other SDKs, and the REST API, support equivalent properties and methods for making indexing policy changes.</span></span> <span data-ttu-id="7634a-379">You can check the progress of an index transformation to a Consistent index by calling  **ReadDocumentCollectionAsync**:</span><span class="sxs-lookup"><span data-stu-id="7634a-379">You can check the progress of an index transformation to a Consistent index by calling  **ReadDocumentCollectionAsync**:</span></span> 

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

> [!NOTE]
> * <span data-ttu-id="7634a-380">The **IndexTransformationProgress** property is applicable only when transforming to a Consistent index.</span><span class="sxs-lookup"><span data-stu-id="7634a-380">The **IndexTransformationProgress** property is applicable only when transforming to a Consistent index.</span></span> <span data-ttu-id="7634a-381">Use the **ResourceResponse.LazyIndexingProgress** property for tracking transformations to a Lazy index.</span><span class="sxs-lookup"><span data-stu-id="7634a-381">Use the **ResourceResponse.LazyIndexingProgress** property for tracking transformations to a Lazy index.</span></span>
> * <span data-ttu-id="7634a-382">The **IndexTransformationProgress** and the **LazyIndexingProgress** properties are populated only for a non-partitioned collection, that is, a collection that is created without a partition key.</span><span class="sxs-lookup"><span data-stu-id="7634a-382">The **IndexTransformationProgress** and the **LazyIndexingProgress** properties are populated only for a non-partitioned collection, that is, a collection that is created without a partition key.</span></span>
>

<span data-ttu-id="7634a-383">You can drop the index for a collection by moving to the None indexing mode.</span><span class="sxs-lookup"><span data-stu-id="7634a-383">You can drop the index for a collection by moving to the None indexing mode.</span></span> <span data-ttu-id="7634a-384">This might be a useful operational tool if you want to cancel an in-progress transformation, and then immediately start a new one.</span><span class="sxs-lookup"><span data-stu-id="7634a-384">This might be a useful operational tool if you want to cancel an in-progress transformation, and then immediately start a new one.</span></span>

<span data-ttu-id="7634a-385">**Drop the index for a collection**</span><span class="sxs-lookup"><span data-stu-id="7634a-385">**Drop the index for a collection**</span></span>

    // Switch to Lazy indexing mode.
    Console.WriteLine("Dropping index by changing to the None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

<span data-ttu-id="7634a-386">When would you make indexing policy changes to your Azure Cosmos DB collections?</span><span class="sxs-lookup"><span data-stu-id="7634a-386">When would you make indexing policy changes to your Azure Cosmos DB collections?</span></span> <span data-ttu-id="7634a-387">The following are the most common use cases:</span><span class="sxs-lookup"><span data-stu-id="7634a-387">The following are the most common use cases:</span></span>

* <span data-ttu-id="7634a-388">Serve consistent results during normal operation, but fall back to Lazy indexing mode during bulk data imports.</span><span class="sxs-lookup"><span data-stu-id="7634a-388">Serve consistent results during normal operation, but fall back to Lazy indexing mode during bulk data imports.</span></span>
* <span data-ttu-id="7634a-389">Start using new indexing features on your current Azure Cosmos DB collections.</span><span class="sxs-lookup"><span data-stu-id="7634a-389">Start using new indexing features on your current Azure Cosmos DB collections.</span></span> <span data-ttu-id="7634a-390">For example, you can use geospatial querying, which requires the Spatial index kind, or ORDER BY/string range queries, which require the string Range index kind.</span><span class="sxs-lookup"><span data-stu-id="7634a-390">For example, you can use geospatial querying, which requires the Spatial index kind, or ORDER BY/string range queries, which require the string Range index kind.</span></span>
* <span data-ttu-id="7634a-391">Hand-select the properties to be indexed, and change them over time.</span><span class="sxs-lookup"><span data-stu-id="7634a-391">Hand-select the properties to be indexed, and change them over time.</span></span>
* <span data-ttu-id="7634a-392">Tune indexing precision to improve query performance or to reduce storage consumed.</span><span class="sxs-lookup"><span data-stu-id="7634a-392">Tune indexing precision to improve query performance or to reduce storage consumed.</span></span>

> [!NOTE]
> <span data-ttu-id="7634a-393">To modify indexing policy by using **ReplaceDocumentCollectionAsync**, you must use version 1.3.0 or a later version of the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7634a-393">To modify indexing policy by using **ReplaceDocumentCollectionAsync**, you must use version 1.3.0 or a later version of the .NET SDK.</span></span>
> 
> <span data-ttu-id="7634a-394">For index transformation to successfully finish, ensure that there is sufficient free storage space available on the collection.</span><span class="sxs-lookup"><span data-stu-id="7634a-394">For index transformation to successfully finish, ensure that there is sufficient free storage space available on the collection.</span></span> <span data-ttu-id="7634a-395">If the collection reaches its storage quota, the index transformation is paused.</span><span class="sxs-lookup"><span data-stu-id="7634a-395">If the collection reaches its storage quota, the index transformation is paused.</span></span> <span data-ttu-id="7634a-396">Index transformation automatically resumes when storage space is available, for example, if you delete some documents.</span><span class="sxs-lookup"><span data-stu-id="7634a-396">Index transformation automatically resumes when storage space is available, for example, if you delete some documents.</span></span>
> 
> 

## <a name="performance-tuning"></a><span data-ttu-id="7634a-397">Performance tuning</span><span class="sxs-lookup"><span data-stu-id="7634a-397">Performance tuning</span></span>
<span data-ttu-id="7634a-398">The SQL APIs provide information about performance metrics, such as the index storage used and the throughput cost (request units) for every operation.</span><span class="sxs-lookup"><span data-stu-id="7634a-398">The SQL APIs provide information about performance metrics, such as the index storage used and the throughput cost (request units) for every operation.</span></span> <span data-ttu-id="7634a-399">You can use this information to compare various indexing policies, and for performance tuning.</span><span class="sxs-lookup"><span data-stu-id="7634a-399">You can use this information to compare various indexing policies, and for performance tuning.</span></span>

<span data-ttu-id="7634a-400">To check the storage quota and usage of a collection, run a **HEAD** or **GET** request against the collection resource.</span><span class="sxs-lookup"><span data-stu-id="7634a-400">To check the storage quota and usage of a collection, run a **HEAD** or **GET** request against the collection resource.</span></span> <span data-ttu-id="7634a-401">Then, inspect the **x-ms-request-quota** and the **x-ms-request-usage** headers.</span><span class="sxs-lookup"><span data-stu-id="7634a-401">Then, inspect the **x-ms-request-quota** and the **x-ms-request-usage** headers.</span></span> <span data-ttu-id="7634a-402">In the .NET SDK, the [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) and [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) properties in [ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) contain these corresponding values.</span><span class="sxs-lookup"><span data-stu-id="7634a-402">In the .NET SDK, the [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) and [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) properties in [ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) contain these corresponding values.</span></span>

     // Measure the document size usage (which includes the index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


<span data-ttu-id="7634a-403">To measure the overhead of indexing on each write operation (create, update, or delete), inspect the **x-ms-request-charge** header (or the equivalent [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) property in [ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) in the .NET SDK) to measure the number of request units that are consumed by these operations.</span><span class="sxs-lookup"><span data-stu-id="7634a-403">To measure the overhead of indexing on each write operation (create, update, or delete), inspect the **x-ms-request-charge** header (or the equivalent [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) property in [ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) in the .NET SDK) to measure the number of request units that are consumed by these operations.</span></span>

     // Measure the performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure the performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-to-the-indexing-policy-specification"></a><span data-ttu-id="7634a-404">Changes to the indexing policy specification</span><span class="sxs-lookup"><span data-stu-id="7634a-404">Changes to the indexing policy specification</span></span>
<span data-ttu-id="7634a-405">A change in the schema for indexing policy was introduced July 7, 2015, with REST API version 2015-06-03.</span><span class="sxs-lookup"><span data-stu-id="7634a-405">A change in the schema for indexing policy was introduced July 7, 2015, with REST API version 2015-06-03.</span></span> <span data-ttu-id="7634a-406">The corresponding classes in the SDK versions have new implementations to match the schema.</span><span class="sxs-lookup"><span data-stu-id="7634a-406">The corresponding classes in the SDK versions have new implementations to match the schema.</span></span> 

<span data-ttu-id="7634a-407">The following changes were implemented in the JSON specification:</span><span class="sxs-lookup"><span data-stu-id="7634a-407">The following changes were implemented in the JSON specification:</span></span>

* <span data-ttu-id="7634a-408">Indexing policy supports Range indexes for strings.</span><span class="sxs-lookup"><span data-stu-id="7634a-408">Indexing policy supports Range indexes for strings.</span></span>
* <span data-ttu-id="7634a-409">Each path can have multiple index definitions.</span><span class="sxs-lookup"><span data-stu-id="7634a-409">Each path can have multiple index definitions.</span></span> <span data-ttu-id="7634a-410">It can have one for each data type.</span><span class="sxs-lookup"><span data-stu-id="7634a-410">It can have one for each data type.</span></span>
* <span data-ttu-id="7634a-411">Indexing precision supports 1 through 8 for numbers, 1 through 100 for strings, and -1 (maximum precision).</span><span class="sxs-lookup"><span data-stu-id="7634a-411">Indexing precision supports 1 through 8 for numbers, 1 through 100 for strings, and -1 (maximum precision).</span></span>
* <span data-ttu-id="7634a-412">Path segments don't require a double quotation to escape each path.</span><span class="sxs-lookup"><span data-stu-id="7634a-412">Path segments don't require a double quotation to escape each path.</span></span> <span data-ttu-id="7634a-413">For example, you can add a path for **/title/?**</span><span class="sxs-lookup"><span data-stu-id="7634a-413">For example, you can add a path for **/title/?**</span></span> <span data-ttu-id="7634a-414">instead of **/"title"/?**.</span><span class="sxs-lookup"><span data-stu-id="7634a-414">instead of **/"title"/?**.</span></span>
* <span data-ttu-id="7634a-415">The root path that represents "all paths" can be represented as **/\*** (in addition to **/**).</span><span class="sxs-lookup"><span data-stu-id="7634a-415">The root path that represents "all paths" can be represented as **/\*** (in addition to **/**).</span></span>

<span data-ttu-id="7634a-416">If you have code that provisions collections with a custom indexing policy written with version 1.1.0 of the .NET SDK or an earlier version, to move to SDK version 1.2.0, you must change your application code to handle these changes.</span><span class="sxs-lookup"><span data-stu-id="7634a-416">If you have code that provisions collections with a custom indexing policy written with version 1.1.0 of the .NET SDK or an earlier version, to move to SDK version 1.2.0, you must change your application code to handle these changes.</span></span> <span data-ttu-id="7634a-417">If you don't have code that configures indexing policy, or if you plan to continue using an earlier version of the SDK, no changes are required.</span><span class="sxs-lookup"><span data-stu-id="7634a-417">If you don't have code that configures indexing policy, or if you plan to continue using an earlier version of the SDK, no changes are required.</span></span>

<span data-ttu-id="7634a-418">For a practical comparison, here's an example of a custom indexing policy written by using REST API version 2015-06-03, followed by the same indexing policy written by using the earlier REST API version 2015-04-08.</span><span class="sxs-lookup"><span data-stu-id="7634a-418">For a practical comparison, here's an example of a custom indexing policy written by using REST API version 2015-06-03, followed by the same indexing policy written by using the earlier REST API version 2015-04-08.</span></span>

<span data-ttu-id="7634a-419">**Current indexing policy JSON (REST API version 2015-06-03)**</span><span class="sxs-lookup"><span data-stu-id="7634a-419">**Current indexing policy JSON (REST API version 2015-06-03)**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }


<span data-ttu-id="7634a-420">**Earlier indexing policy JSON (REST API version 2015-04-08)**</span><span class="sxs-lookup"><span data-stu-id="7634a-420">**Earlier indexing policy JSON (REST API version 2015-04-08)**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }


## <a name="next-steps"></a><span data-ttu-id="7634a-421">Next steps</span><span class="sxs-lookup"><span data-stu-id="7634a-421">Next steps</span></span>
<span data-ttu-id="7634a-422">For index policy management samples and to learn more about the Azure Cosmos DB query language, see the following links:</span><span class="sxs-lookup"><span data-stu-id="7634a-422">For index policy management samples and to learn more about the Azure Cosmos DB query language, see the following links:</span></span>

* [<span data-ttu-id="7634a-423">SQL API .NET index management code samples</span><span class="sxs-lookup"><span data-stu-id="7634a-423">SQL API .NET index management code samples</span></span>](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
* [<span data-ttu-id="7634a-424">SQL API REST collection operations</span><span class="sxs-lookup"><span data-stu-id="7634a-424">SQL API REST collection operations</span></span>](https://msdn.microsoft.com/library/azure/dn782195.aspx)
* [<span data-ttu-id="7634a-425">Query with SQL</span><span class="sxs-lookup"><span data-stu-id="7634a-425">Query with SQL</span></span>](sql-api-sql-query.md)

