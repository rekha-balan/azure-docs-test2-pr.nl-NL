---
title: 'Azure Cosmos DB: SQL .NET Core API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL .NET Core API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB .NET Core SDK.
services: cosmos-db
author: rnagpal
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: dotnet
ms.topic: reference
ms.date: 03/22/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b1ab1381271391da9f4775488908af4eb1e47f5d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857889"
---
# <a name="azure-cosmos-db-net-core-sdk-for-sql-api-release-notes-and-resources"></a><span data-ttu-id="b6cdd-103">Azure Cosmos DB .NET Core SDK for SQL API: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="b6cdd-103">Azure Cosmos DB .NET Core SDK for SQL API: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [.NET](sql-api-sdk-dotnet.md)
> * [.NET Change Feed](sql-api-sdk-dotnet-changefeed.md)
> * [.NET Core](sql-api-sdk-dotnet-core.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Async Java](sql-api-sdk-async-java.md)
> * [Java](sql-api-sdk-java.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/cosmos-db/)
> * [REST Resource Provider](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> * [BulkExecutor - .NET](sql-api-sdk-bulk-executor-dot-net.md)
> * [BulkExecutor - Java](sql-api-sdk-bulk-executor-java.md)

<table>

<tr><td><span data-ttu-id="b6cdd-116">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-116">**SDK download**</span></span></td><td>[<span data-ttu-id="b6cdd-117">NuGet</span><span class="sxs-lookup"><span data-stu-id="b6cdd-117">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="b6cdd-118">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-118">**API documentation**</span></span></td><td>[<span data-ttu-id="b6cdd-119">.NET API reference documentation</span><span class="sxs-lookup"><span data-stu-id="b6cdd-119">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="b6cdd-120">**Samples**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-120">**Samples**</span></span></td><td>[<span data-ttu-id="b6cdd-121">.NET code samples</span><span class="sxs-lookup"><span data-stu-id="b6cdd-121">.NET code samples</span></span>](sql-api-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="b6cdd-122">**Get started**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-122">**Get started**</span></span></td><td>[<span data-ttu-id="b6cdd-123">Get started with the Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="b6cdd-123">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](sql-api-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="b6cdd-124">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-124">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="b6cdd-125">Web application development with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b6cdd-125">Web application development with Azure Cosmos DB</span></span>](sql-api-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="b6cdd-126">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="b6cdd-126">**Current supported framework**</span></span></td><td>[<span data-ttu-id="b6cdd-127">.NET Standard 1.6 and .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="b6cdd-127">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b6cdd-128">Release Notes</span><span class="sxs-lookup"><span data-stu-id="b6cdd-128">Release Notes</span></span>

<span data-ttu-id="b6cdd-129">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](sql-api-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-129">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](sql-api-sdk-dotnet.md).</span></span>

### <a name="a-name200200"></a><span data-ttu-id="b6cdd-130"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-130"><a name="2.0.0"/>2.0.0</span></span>

* <span data-ttu-id="b6cdd-131">Added request cancellation support.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-131">Added request cancellation support.</span></span>
* <span data-ttu-id="b6cdd-132">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-132">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span></span>
* <span data-ttu-id="b6cdd-133">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-133">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span></span>
* <span data-ttu-id="b6cdd-134">DocumentClient methods now have parity with IDocumentClient.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-134">DocumentClient methods now have parity with IDocumentClient.</span></span>
* <span data-ttu-id="b6cdd-135">Updated direct TCP transport stack to reduce the number of connections established.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-135">Updated direct TCP transport stack to reduce the number of connections established.</span></span>
* <span data-ttu-id="b6cdd-136">Added support for Direct Mode TCP for non-Windows clients.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-136">Added support for Direct Mode TCP for non-Windows clients.</span></span>

### <a name="a-name200-preview2200-preview2"></a><span data-ttu-id="b6cdd-137"><a name="2.0.0-preview2"/>2.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-137"><a name="2.0.0-preview2"/>2.0.0-preview2</span></span>

* <span data-ttu-id="b6cdd-138">Added request cancellation support.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-138">Added request cancellation support.</span></span>
* <span data-ttu-id="b6cdd-139">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-139">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span></span>
* <span data-ttu-id="b6cdd-140">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-140">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span></span>

### <a name="a-name200-preview200-preview"></a><span data-ttu-id="b6cdd-141"><a name="2.0.0-preview"/>2.0.0-preview</span><span class="sxs-lookup"><span data-stu-id="b6cdd-141"><a name="2.0.0-preview"/>2.0.0-preview</span></span>

* <span data-ttu-id="b6cdd-142">DocumentClient methods now have parity with IDocumentClient.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-142">DocumentClient methods now have parity with IDocumentClient.</span></span>
* <span data-ttu-id="b6cdd-143">Updated direct TCP transport stack to reduce the number of connections established.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-143">Updated direct TCP transport stack to reduce the number of connections established.</span></span>
* <span data-ttu-id="b6cdd-144">Added support for Direct Mode TCP for non-Windows clients.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-144">Added support for Direct Mode TCP for non-Windows clients.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="b6cdd-145"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-145"><a name="1.10.0"/>1.10.0</span></span>

* <span data-ttu-id="b6cdd-146">Added ConsistencyLevel Property to FeedOptions.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-146">Added ConsistencyLevel Property to FeedOptions.</span></span>
* <span data-ttu-id="b6cdd-147">Added JsonSerializerSettings to RequestOptions and FeedOptions.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-147">Added JsonSerializerSettings to RequestOptions and FeedOptions.</span></span>
* <span data-ttu-id="b6cdd-148">Added EnableReadRequestsFallback to ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-148">Added EnableReadRequestsFallback to ConnectionPolicy.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="b6cdd-149"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-149"><a name="1.9.1"/>1.9.1</span></span>

* <span data-ttu-id="b6cdd-150">Fixed KeyNotFoundException for cross partition order by queries in corner cases.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-150">Fixed KeyNotFoundException for cross partition order by queries in corner cases.</span></span>
* <span data-ttu-id="b6cdd-151">Fixed bug where JsonPropery attribute in select clause for LINQ queries was not being honored.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-151">Fixed bug where JsonPropery attribute in select clause for LINQ queries was not being honored.</span></span>

### <a name="a-name182182"></a><span data-ttu-id="b6cdd-152"><a name="1.8.2"/>1.8.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-152"><a name="1.8.2"/>1.8.2</span></span>

* <span data-ttu-id="b6cdd-153">Fixed bug that is hit under certain race conditions, that results in intermittent "Microsoft.Azure.Documents.NotFoundException: The read session is not available for the input session token" errors when using Session consistency level.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-153">Fixed bug that is hit under certain race conditions, that results in intermittent "Microsoft.Azure.Documents.NotFoundException: The read session is not available for the input session token" errors when using Session consistency level.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="b6cdd-154"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-154"><a name="1.8.1"/>1.8.1</span></span>

* <span data-ttu-id="b6cdd-155">Fixed regression where FeedOptions.MaxItemCount = -1 threw an System.ArithmeticException: page size is negative.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-155">Fixed regression where FeedOptions.MaxItemCount = -1 threw an System.ArithmeticException: page size is negative.</span></span>
* <span data-ttu-id="b6cdd-156">Added a new ToString() function to QueryMetrics.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-156">Added a new ToString() function to QueryMetrics.</span></span>
* <span data-ttu-id="b6cdd-157">Exposed partition statistics on reading collections.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-157">Exposed partition statistics on reading collections.</span></span>
* <span data-ttu-id="b6cdd-158">Added PartitionKey property to ChangeFeedOptions.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-158">Added PartitionKey property to ChangeFeedOptions.</span></span>
* <span data-ttu-id="b6cdd-159">Minor bug fixes.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-159">Minor bug fixes.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="b6cdd-160"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-160"><a name="1.7.1"/>1.7.1</span></span>
 
 * <span data-ttu-id="b6cdd-161">Adds the ability to specify unique indexes for the documents by using UniqueKeyPolicy property on the DocumentCollection.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-161">Adds the ability to specify unique indexes for the documents by using UniqueKeyPolicy property on the DocumentCollection.</span></span>
 * <span data-ttu-id="b6cdd-162">Fixed a bug in which the custom JsonSerializer settings were not being honored for some queries and stored procedure execution.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-162">Fixed a bug in which the custom JsonSerializer settings were not being honored for some queries and stored procedure execution.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="b6cdd-163"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-163"><a name="1.7.0"/>1.7.0</span></span>
 
 * <span data-ttu-id="b6cdd-164">Branding change from Azure DocumentDB to Azure Cosmos DB in the API Reference documentation, metadata information in assemblies, and the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-164">Branding change from Azure DocumentDB to Azure Cosmos DB in the API Reference documentation, metadata information in assemblies, and the NuGet package.</span></span> 
 * <span data-ttu-id="b6cdd-165">Expose diagnostic information and latency from the response of requests sent with direct connectivity mode.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-165">Expose diagnostic information and latency from the response of requests sent with direct connectivity mode.</span></span> <span data-ttu-id="b6cdd-166">The property names are RequestDiagnosticsString and RequestLatency on ResourceResponse class.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-166">The property names are RequestDiagnosticsString and RequestLatency on ResourceResponse class.</span></span>
 * <span data-ttu-id="b6cdd-167">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-167">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span></span>
 
### <a name="a-name160160"></a><span data-ttu-id="b6cdd-168"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-168"><a name="1.6.0"/>1.6.0</span></span>

* <span data-ttu-id="b6cdd-169">Added several reliability fixes and improvements.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-169">Added several reliability fixes and improvements.</span></span>

### <a name="a-name151151"></a><span data-ttu-id="b6cdd-170"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-170"><a name="1.5.1"/>1.5.1</span></span> 

* <span data-ttu-id="b6cdd-171">Internal changes related to supporting [Microsoft.Azure.Graphs](https://docs.microsoft.com/azure/cosmos-db/graph-sdk-dotnet)</span><span class="sxs-lookup"><span data-stu-id="b6cdd-171">Internal changes related to supporting [Microsoft.Azure.Graphs](https://docs.microsoft.com/azure/cosmos-db/graph-sdk-dotnet)</span></span>

### <a name="a-name150150"></a><span data-ttu-id="b6cdd-172"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-172"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="b6cdd-173">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-173">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="b6cdd-174">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-174">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="b6cdd-175"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-175"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="b6cdd-176">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-176">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="b6cdd-177"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-177"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="b6cdd-178">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-178">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="b6cdd-179"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-179"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="b6cdd-180">Supporting .NET Standard 1.5 as one of the target frameworks.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-180">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="b6cdd-181"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-181"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="b6cdd-182">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-182">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="b6cdd-183"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-183"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="b6cdd-184">Added support for a new consistency level called ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-184">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="b6cdd-185">Added support for query metrics for individual partitions.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-185">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="b6cdd-186">Added support for limiting the size of the continuation token for queries.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-186">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="b6cdd-187">Added support for more detailed tracing for failed requests.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-187">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="b6cdd-188">Made some performance improvements in the SDK.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-188">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="b6cdd-189"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-189"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="b6cdd-190">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-190">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="b6cdd-191">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-191">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="b6cdd-192"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-192"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="b6cdd-193">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-193">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="b6cdd-194"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-194"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="b6cdd-195">Fixes to make SDK more resilient to automatic failover under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-195">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="b6cdd-196"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-196"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="b6cdd-197">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-197">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="b6cdd-198">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-198">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="b6cdd-199"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-199"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="b6cdd-200">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-200">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="b6cdd-201">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-201">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="b6cdd-202">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-202">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="b6cdd-203">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-203">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="b6cdd-204"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-204"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="b6cdd-205">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-205">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="b6cdd-206">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-206">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="b6cdd-207">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-207">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b6cdd-208"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-208"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="b6cdd-209">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-209">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="b6cdd-210">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-210">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="b6cdd-211"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="b6cdd-211"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="b6cdd-212">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-212">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="b6cdd-213">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](sql-api-sdk-dotnet.md) and supports the following:</span><span class="sxs-lookup"><span data-stu-id="b6cdd-213">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](sql-api-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="b6cdd-214">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-214">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="b6cdd-215">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-215">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="b6cdd-216">[Partitioned collections](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-216">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="b6cdd-217">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-217">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="b6cdd-218">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="b6cdd-218">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="b6cdd-219">Release & Retirement Dates</span><span class="sxs-lookup"><span data-stu-id="b6cdd-219">Release & Retirement Dates</span></span>

| <span data-ttu-id="b6cdd-220">Version</span><span class="sxs-lookup"><span data-stu-id="b6cdd-220">Version</span></span> | <span data-ttu-id="b6cdd-221">Release Date</span><span class="sxs-lookup"><span data-stu-id="b6cdd-221">Release Date</span></span> | <span data-ttu-id="b6cdd-222">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="b6cdd-222">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b6cdd-223">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-223">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="b6cdd-224">September 07, 2018</span><span class="sxs-lookup"><span data-stu-id="b6cdd-224">September 07, 2018</span></span> |--- |
| [<span data-ttu-id="b6cdd-225">1.9.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-225">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="b6cdd-226">March 09, 2018</span><span class="sxs-lookup"><span data-stu-id="b6cdd-226">March 09, 2018</span></span> |--- |
| [<span data-ttu-id="b6cdd-227">1.8.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-227">1.8.2</span></span>](#1.8.2) |<span data-ttu-id="b6cdd-228">February 21, 2018</span><span class="sxs-lookup"><span data-stu-id="b6cdd-228">February 21, 2018</span></span> |--- |
| [<span data-ttu-id="b6cdd-229">1.8.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-229">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="b6cdd-230">February 05, 2018</span><span class="sxs-lookup"><span data-stu-id="b6cdd-230">February 05, 2018</span></span> |--- |
| [<span data-ttu-id="b6cdd-231">1.7.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-231">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="b6cdd-232">November 16, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-232">November 16, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-233">1.7.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-233">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="b6cdd-234">November 10, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-234">November 10, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-235">1.6.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-235">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="b6cdd-236">October 17, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-236">October 17, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-237">1.5.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-237">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="b6cdd-238">October 02, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-238">October 02, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-239">1.5.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-239">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="b6cdd-240">August 10, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-240">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="b6cdd-241">1.4.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-241">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="b6cdd-242">August 07, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-242">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-243">1.4.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-243">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="b6cdd-244">August 02, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-244">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-245">1.3.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-245">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="b6cdd-246">June 12, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-246">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-247">1.3.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-247">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="b6cdd-248">May 23, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-248">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-249">1.3.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-249">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="b6cdd-250">May 10, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-250">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-251">1.2.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-251">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="b6cdd-252">April 19, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-252">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-253">1.2.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-253">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="b6cdd-254">March 29, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-254">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-255">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-255">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="b6cdd-256">March 25, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-256">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-257">1.1.2</span><span class="sxs-lookup"><span data-stu-id="b6cdd-257">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="b6cdd-258">March 20, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-258">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-259">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b6cdd-259">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="b6cdd-260">March 14, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-260">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-261">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-261">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="b6cdd-262">February 16, 2017</span><span class="sxs-lookup"><span data-stu-id="b6cdd-262">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="b6cdd-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b6cdd-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b6cdd-264">December 21, 2016</span><span class="sxs-lookup"><span data-stu-id="b6cdd-264">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="b6cdd-265">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="b6cdd-265">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="b6cdd-266">November 15, 2016</span><span class="sxs-lookup"><span data-stu-id="b6cdd-266">November 15, 2016</span></span> |<span data-ttu-id="b6cdd-267">December 31, 2016</span><span class="sxs-lookup"><span data-stu-id="b6cdd-267">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="b6cdd-268">See Also</span><span class="sxs-lookup"><span data-stu-id="b6cdd-268">See Also</span></span>
<span data-ttu-id="b6cdd-269">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="b6cdd-269">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

