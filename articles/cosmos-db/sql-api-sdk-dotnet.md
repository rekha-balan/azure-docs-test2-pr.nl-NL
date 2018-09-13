---
title: 'Azure Cosmos DB: SQL .NET API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL .NET API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB .NET SDK.
services: cosmos-db
author: rnagpal
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: dotnet
ms.topic: reference
ms.date: 03/09/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 26de3545c5d79c711703fa97cb796cd6c504f663
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869666"
---
# <a name="azure-cosmos-db-net-sdk-for-sql-api-download-and-release-notes"></a><span data-ttu-id="9d886-103">Azure Cosmos DB .NET SDK for SQL API: Download and release notes</span><span class="sxs-lookup"><span data-stu-id="9d886-103">Azure Cosmos DB .NET SDK for SQL API: Download and release notes</span></span>
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

<tr><td><span data-ttu-id="9d886-116">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="9d886-116">**SDK download**</span></span></td><td>[<span data-ttu-id="9d886-117">NuGet</span><span class="sxs-lookup"><span data-stu-id="9d886-117">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="9d886-118">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="9d886-118">**API documentation**</span></span></td><td>[<span data-ttu-id="9d886-119">.NET API reference documentation</span><span class="sxs-lookup"><span data-stu-id="9d886-119">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="9d886-120">**Samples**</span><span class="sxs-lookup"><span data-stu-id="9d886-120">**Samples**</span></span></td><td>[<span data-ttu-id="9d886-121">.NET code samples</span><span class="sxs-lookup"><span data-stu-id="9d886-121">.NET code samples</span></span>](sql-api-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="9d886-122">**Get started**</span><span class="sxs-lookup"><span data-stu-id="9d886-122">**Get started**</span></span></td><td>[<span data-ttu-id="9d886-123">Get started with the Azure Cosmos DB .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9d886-123">Get started with the Azure Cosmos DB .NET SDK</span></span>](sql-api-get-started.md)</td></tr>

<tr><td><span data-ttu-id="9d886-124">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="9d886-124">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="9d886-125">Web application development with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9d886-125">Web application development with Azure Cosmos DB</span></span>](sql-api-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="9d886-126">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="9d886-126">**Current supported framework**</span></span></td><td>[<span data-ttu-id="9d886-127">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="9d886-127">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="9d886-128">Release notes</span><span class="sxs-lookup"><span data-stu-id="9d886-128">Release notes</span></span>
### <a name="a-name200200"></a><span data-ttu-id="9d886-129"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="9d886-129"><a name="2.0.0"/>2.0.0</span></span>

* <span data-ttu-id="9d886-130">Added request cancellation support.</span><span class="sxs-lookup"><span data-stu-id="9d886-130">Added request cancellation support.</span></span>
* <span data-ttu-id="9d886-131">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span><span class="sxs-lookup"><span data-stu-id="9d886-131">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span></span>
* <span data-ttu-id="9d886-132">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span><span class="sxs-lookup"><span data-stu-id="9d886-132">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span></span>
* <span data-ttu-id="9d886-133">DocumentClient methods now have parity with IDocumentClient.</span><span class="sxs-lookup"><span data-stu-id="9d886-133">DocumentClient methods now have parity with IDocumentClient.</span></span>
* <span data-ttu-id="9d886-134">Updated direct TCP transport stack to reduce the number of connections established.</span><span class="sxs-lookup"><span data-stu-id="9d886-134">Updated direct TCP transport stack to reduce the number of connections established.</span></span>
* <span data-ttu-id="9d886-135">Added support for Direct Mode TCP for non-Windows clients.</span><span class="sxs-lookup"><span data-stu-id="9d886-135">Added support for Direct Mode TCP for non-Windows clients.</span></span>

### <a name="a-name200-preview2200-preview2"></a><span data-ttu-id="9d886-136"><a name="2.0.0-preview2"/>2.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="9d886-136"><a name="2.0.0-preview2"/>2.0.0-preview2</span></span>

* <span data-ttu-id="9d886-137">Added request cancellation support.</span><span class="sxs-lookup"><span data-stu-id="9d886-137">Added request cancellation support.</span></span>
* <span data-ttu-id="9d886-138">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span><span class="sxs-lookup"><span data-stu-id="9d886-138">Added SetCurrentLocation to ConnectionPolicy, which automatically populates the preferred locations based on the region.</span></span>
* <span data-ttu-id="9d886-139">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span><span class="sxs-lookup"><span data-stu-id="9d886-139">Fixed Bug in Cross Partition Queries with Min/Max and a filter that matches no documents on an individual partition.</span></span>

### <a name="a-name200-preview200-preview"></a><span data-ttu-id="9d886-140"><a name="2.0.0-preview"/>2.0.0-preview</span><span class="sxs-lookup"><span data-stu-id="9d886-140"><a name="2.0.0-preview"/>2.0.0-preview</span></span>

* <span data-ttu-id="9d886-141">DocumentClient methods now have parity with IDocumentClient.</span><span class="sxs-lookup"><span data-stu-id="9d886-141">DocumentClient methods now have parity with IDocumentClient.</span></span>
* <span data-ttu-id="9d886-142">Updated direct TCP transport stack to reduce the number of connections established.</span><span class="sxs-lookup"><span data-stu-id="9d886-142">Updated direct TCP transport stack to reduce the number of connections established.</span></span>
* <span data-ttu-id="9d886-143">Added support for Direct Mode TCP for non-Windows clients.</span><span class="sxs-lookup"><span data-stu-id="9d886-143">Added support for Direct Mode TCP for non-Windows clients.</span></span>

### <a name="a-name12201220"></a><span data-ttu-id="9d886-144"><a name="1.22.0"/>1.22.0</span><span class="sxs-lookup"><span data-stu-id="9d886-144"><a name="1.22.0"/>1.22.0</span></span>

* <span data-ttu-id="9d886-145">Added ConsistencyLevel Property to FeedOptions.</span><span class="sxs-lookup"><span data-stu-id="9d886-145">Added ConsistencyLevel Property to FeedOptions.</span></span>
* <span data-ttu-id="9d886-146">Added JsonSerializerSettings to RequestOptions and FeedOptions.</span><span class="sxs-lookup"><span data-stu-id="9d886-146">Added JsonSerializerSettings to RequestOptions and FeedOptions.</span></span>
* <span data-ttu-id="9d886-147">Added EnableReadRequestsFallback to ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="9d886-147">Added EnableReadRequestsFallback to ConnectionPolicy.</span></span>

### <a name="a-name12111211"></a><span data-ttu-id="9d886-148"><a name="1.21.1"/>1.21.1</span><span class="sxs-lookup"><span data-stu-id="9d886-148"><a name="1.21.1"/>1.21.1</span></span>

* <span data-ttu-id="9d886-149">Fixed KeyNotFoundException for cross partition order by queries in corner cases.</span><span class="sxs-lookup"><span data-stu-id="9d886-149">Fixed KeyNotFoundException for cross partition order by queries in corner cases.</span></span>
* <span data-ttu-id="9d886-150">Fixed bug where JsonProperty attribute in select clause for LINQ queries was not being honored.</span><span class="sxs-lookup"><span data-stu-id="9d886-150">Fixed bug where JsonProperty attribute in select clause for LINQ queries was not being honored.</span></span>

### <a name="a-name12021202"></a><span data-ttu-id="9d886-151"><a name="1.20.2"/>1.20.2</span><span class="sxs-lookup"><span data-stu-id="9d886-151"><a name="1.20.2"/>1.20.2</span></span>

* <span data-ttu-id="9d886-152">Fixed bug that is hit under certain race conditions, that results in intermittent "Microsoft.Azure.Documents.NotFoundException: The read session is not available for the input session token" errors when using Session consistency level.</span><span class="sxs-lookup"><span data-stu-id="9d886-152">Fixed bug that is hit under certain race conditions, that results in intermittent "Microsoft.Azure.Documents.NotFoundException: The read session is not available for the input session token" errors when using Session consistency level.</span></span>

### <a name="a-name12011201"></a><span data-ttu-id="9d886-153"><a name="1.20.1"/>1.20.1</span><span class="sxs-lookup"><span data-stu-id="9d886-153"><a name="1.20.1"/>1.20.1</span></span>

* <span data-ttu-id="9d886-154">Fixed regression where FeedOptions.MaxItemCount = -1 threw an System.ArithmeticException: page size is negative.</span><span class="sxs-lookup"><span data-stu-id="9d886-154">Fixed regression where FeedOptions.MaxItemCount = -1 threw an System.ArithmeticException: page size is negative.</span></span>
* <span data-ttu-id="9d886-155">Added a new ToString() function to QueryMetrics.</span><span class="sxs-lookup"><span data-stu-id="9d886-155">Added a new ToString() function to QueryMetrics.</span></span>
* <span data-ttu-id="9d886-156">Exposed partition statistics on reading collections.</span><span class="sxs-lookup"><span data-stu-id="9d886-156">Exposed partition statistics on reading collections.</span></span>
* <span data-ttu-id="9d886-157">Added PartitionKey property to ChangeFeedOptions.</span><span class="sxs-lookup"><span data-stu-id="9d886-157">Added PartitionKey property to ChangeFeedOptions.</span></span>
* <span data-ttu-id="9d886-158">Minor bug fixes.</span><span class="sxs-lookup"><span data-stu-id="9d886-158">Minor bug fixes.</span></span>

### <a name="a-name11911191"></a><span data-ttu-id="9d886-159"><a name="1.19.1"/>1.19.1</span><span class="sxs-lookup"><span data-stu-id="9d886-159"><a name="1.19.1"/>1.19.1</span></span>

* <span data-ttu-id="9d886-160">Adds the ability to specify unique indexes for the documents by using UniqueKeyPolicy property on the DocumentCollection.</span><span class="sxs-lookup"><span data-stu-id="9d886-160">Adds the ability to specify unique indexes for the documents by using UniqueKeyPolicy property on the DocumentCollection.</span></span>
* <span data-ttu-id="9d886-161">Fixed a bug in which the custom JsonSerializer settings were not being honored for some queries and stored procedure execution.</span><span class="sxs-lookup"><span data-stu-id="9d886-161">Fixed a bug in which the custom JsonSerializer settings were not being honored for some queries and stored procedure execution.</span></span>

### <a name="a-name11901190"></a><span data-ttu-id="9d886-162"><a name="1.19.0"/>1.19.0</span><span class="sxs-lookup"><span data-stu-id="9d886-162"><a name="1.19.0"/>1.19.0</span></span>

* <span data-ttu-id="9d886-163">Branding change from Azure DocumentDB to Azure Cosmos DB in the API Reference documentation, metadata information in assemblies, and the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="9d886-163">Branding change from Azure DocumentDB to Azure Cosmos DB in the API Reference documentation, metadata information in assemblies, and the NuGet package.</span></span> 
* <span data-ttu-id="9d886-164">Expose diagnostic information and latency from the response of requests sent with direct connectivity mode.</span><span class="sxs-lookup"><span data-stu-id="9d886-164">Expose diagnostic information and latency from the response of requests sent with direct connectivity mode.</span></span> <span data-ttu-id="9d886-165">The property names are RequestDiagnosticsString and RequestLatency on ResourceResponse class.</span><span class="sxs-lookup"><span data-stu-id="9d886-165">The property names are RequestDiagnosticsString and RequestLatency on ResourceResponse class.</span></span>
* <span data-ttu-id="9d886-166">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span><span class="sxs-lookup"><span data-stu-id="9d886-166">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span></span> 

### <a name="a-name11811181"></a><span data-ttu-id="9d886-167"><a name="1.18.1"/>1.18.1</span><span class="sxs-lookup"><span data-stu-id="9d886-167"><a name="1.18.1"/>1.18.1</span></span> 

* <span data-ttu-id="9d886-168">Internal changes for Microsoft friends assemblies.</span><span class="sxs-lookup"><span data-stu-id="9d886-168">Internal changes for Microsoft friends assemblies.</span></span>

### <a name="a-name11801180"></a><span data-ttu-id="9d886-169"><a name="1.18.0"/>1.18.0</span><span class="sxs-lookup"><span data-stu-id="9d886-169"><a name="1.18.0"/>1.18.0</span></span> 

* <span data-ttu-id="9d886-170">Added several reliability fixes and improvements.</span><span class="sxs-lookup"><span data-stu-id="9d886-170">Added several reliability fixes and improvements.</span></span>

### <a name="a-name11701170"></a><span data-ttu-id="9d886-171"><a name="1.17.0"/>1.17.0</span><span class="sxs-lookup"><span data-stu-id="9d886-171"><a name="1.17.0"/>1.17.0</span></span> 

* <span data-ttu-id="9d886-172">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span><span class="sxs-lookup"><span data-stu-id="9d886-172">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="9d886-173">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span><span class="sxs-lookup"><span data-stu-id="9d886-173">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="9d886-174"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="9d886-174"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="9d886-175">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span><span class="sxs-lookup"><span data-stu-id="9d886-175">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="9d886-176"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="9d886-176"><a name="1.16.0"/>1.16.0</span></span>
*   <span data-ttu-id="9d886-177">Fixed an issue that required recompiling of the application due to the introduction of JsonSerializerSettings as an optional parameter in the DocumentClient constructor.</span><span class="sxs-lookup"><span data-stu-id="9d886-177">Fixed an issue that required recompiling of the application due to the introduction of JsonSerializerSettings as an optional parameter in the DocumentClient constructor.</span></span>
* <span data-ttu-id="9d886-178">Marked the DocumentClient constructor obsolete that required JsonSerializerSettings as the last parameter to allow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span><span class="sxs-lookup"><span data-stu-id="9d886-178">Marked the DocumentClient constructor obsolete that required JsonSerializerSettings as the last parameter to allow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="9d886-179"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="9d886-179"><a name="1.15.0"/>1.15.0</span></span>
*   <span data-ttu-id="9d886-180">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="9d886-180">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span></span>

### <a name="a-name11411141"></a><span data-ttu-id="9d886-181"><a name="1.14.1"/>1.14.1</span><span class="sxs-lookup"><span data-stu-id="9d886-181"><a name="1.14.1"/>1.14.1</span></span>
*   <span data-ttu-id="9d886-182">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB SQL queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-182">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB SQL queries.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="9d886-183"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="9d886-183"><a name="1.14.0"/>1.14.0</span></span>
*   <span data-ttu-id="9d886-184">Added support for a new consistency level called ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="9d886-184">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="9d886-185">Added support for query metrics for individual partitions.</span><span class="sxs-lookup"><span data-stu-id="9d886-185">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="9d886-186">Added support for limiting the size of the continuation token for queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-186">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="9d886-187">Added support for more detailed tracing for failed requests.</span><span class="sxs-lookup"><span data-stu-id="9d886-187">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="9d886-188">Made some performance improvements in the SDK.</span><span class="sxs-lookup"><span data-stu-id="9d886-188">Made some performance improvements in the SDK.</span></span>

### <a name="a-name11341134"></a><span data-ttu-id="9d886-189"><a name="1.13.4"/>1.13.4</span><span class="sxs-lookup"><span data-stu-id="9d886-189"><a name="1.13.4"/>1.13.4</span></span>
* <span data-ttu-id="9d886-190">Functionally same as 1.13.3.</span><span class="sxs-lookup"><span data-stu-id="9d886-190">Functionally same as 1.13.3.</span></span> <span data-ttu-id="9d886-191">Made some internal changes.</span><span class="sxs-lookup"><span data-stu-id="9d886-191">Made some internal changes.</span></span>

### <a name="a-name11331133"></a><span data-ttu-id="9d886-192"><a name="1.13.3"/>1.13.3</span><span class="sxs-lookup"><span data-stu-id="9d886-192"><a name="1.13.3"/>1.13.3</span></span>
* <span data-ttu-id="9d886-193">Functionally same as 1.13.2.</span><span class="sxs-lookup"><span data-stu-id="9d886-193">Functionally same as 1.13.2.</span></span> <span data-ttu-id="9d886-194">Made some internal changes.</span><span class="sxs-lookup"><span data-stu-id="9d886-194">Made some internal changes.</span></span>

### <a name="a-name11321132"></a><span data-ttu-id="9d886-195"><a name="1.13.2"/>1.13.2</span><span class="sxs-lookup"><span data-stu-id="9d886-195"><a name="1.13.2"/>1.13.2</span></span>
* <span data-ttu-id="9d886-196">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-196">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="9d886-197">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span><span class="sxs-lookup"><span data-stu-id="9d886-197">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="9d886-198"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="9d886-198"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="9d886-199">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span><span class="sxs-lookup"><span data-stu-id="9d886-199">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="9d886-200"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="9d886-200"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="9d886-201">Fixes to make SDK more resilient to automatic failover under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="9d886-201">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="9d886-202"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="9d886-202"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="9d886-203">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span><span class="sxs-lookup"><span data-stu-id="9d886-203">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="9d886-204">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span><span class="sxs-lookup"><span data-stu-id="9d886-204">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="9d886-205"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="9d886-205"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="9d886-206">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="9d886-206">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="9d886-207">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span><span class="sxs-lookup"><span data-stu-id="9d886-207">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="9d886-208">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span><span class="sxs-lookup"><span data-stu-id="9d886-208">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="9d886-209">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span><span class="sxs-lookup"><span data-stu-id="9d886-209">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="9d886-210"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="9d886-210"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="9d886-211">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="9d886-211">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="9d886-212">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="9d886-212">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="9d886-213">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="9d886-213">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="9d886-214"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="9d886-214"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="9d886-215">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span><span class="sxs-lookup"><span data-stu-id="9d886-215">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span></span>
* <span data-ttu-id="9d886-216">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span><span class="sxs-lookup"><span data-stu-id="9d886-216">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="9d886-217">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span><span class="sxs-lookup"><span data-stu-id="9d886-217">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="9d886-218">Client side performance fixes for increasing the read and write throughput of the requests.</span><span class="sxs-lookup"><span data-stu-id="9d886-218">Client side performance fixes for increasing the read and write throughput of the requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="9d886-219"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="9d886-219"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="9d886-220">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span><span class="sxs-lookup"><span data-stu-id="9d886-220">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span></span>
* <span data-ttu-id="9d886-221">Added support for the SDK to work in a 32-bit host process.</span><span class="sxs-lookup"><span data-stu-id="9d886-221">Added support for the SDK to work in a 32-bit host process.</span></span> <span data-ttu-id="9d886-222">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span><span class="sxs-lookup"><span data-stu-id="9d886-222">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="9d886-223">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span><span class="sxs-lookup"><span data-stu-id="9d886-223">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="9d886-224">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span><span class="sxs-lookup"><span data-stu-id="9d886-224">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="9d886-225"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="9d886-225"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="9d886-226">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span><span class="sxs-lookup"><span data-stu-id="9d886-226">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="9d886-227">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="9d886-227">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="9d886-228"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="9d886-228"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="9d886-229">Support for new classes and methods to process the [change feed](change-feed.md) of documents within a collection.</span><span class="sxs-lookup"><span data-stu-id="9d886-229">Support for new classes and methods to process the [change feed](change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="9d886-230">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-230">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="9d886-231">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span><span class="sxs-lookup"><span data-stu-id="9d886-231">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="9d886-232">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span><span class="sxs-lookup"><span data-stu-id="9d886-232">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="9d886-233">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span><span class="sxs-lookup"><span data-stu-id="9d886-233">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="9d886-234">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span><span class="sxs-lookup"><span data-stu-id="9d886-234">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="9d886-235"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="9d886-235"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="9d886-236">Added direct connectivity support for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="9d886-236">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="9d886-237">Improved performance for the Bounded Staleness consistency level.</span><span class="sxs-lookup"><span data-stu-id="9d886-237">Improved performance for the Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="9d886-238">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-238">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="9d886-239">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span><span class="sxs-lookup"><span data-stu-id="9d886-239">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="9d886-240">Various SDK bug fixes.</span><span class="sxs-lookup"><span data-stu-id="9d886-240">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="9d886-241"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="9d886-241"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="9d886-242">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span><span class="sxs-lookup"><span data-stu-id="9d886-242">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span></span> <span data-ttu-id="9d886-243">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span><span class="sxs-lookup"><span data-stu-id="9d886-243">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="9d886-244">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span><span class="sxs-lookup"><span data-stu-id="9d886-244">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="9d886-245"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="9d886-245"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="9d886-246">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span><span class="sxs-lookup"><span data-stu-id="9d886-246">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="9d886-247">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span><span class="sxs-lookup"><span data-stu-id="9d886-247">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="9d886-248"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="9d886-248"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="9d886-249">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span><span class="sxs-lookup"><span data-stu-id="9d886-249">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span></span>
* <span data-ttu-id="9d886-250">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span><span class="sxs-lookup"><span data-stu-id="9d886-250">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="9d886-251"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="9d886-251"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="9d886-252">Added support for parallel queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="9d886-252">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="9d886-253">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="9d886-253">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="9d886-254">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference to the Azure Cosmos DB Nuget package.</span><span class="sxs-lookup"><span data-stu-id="9d886-254">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference to the Azure Cosmos DB Nuget package.</span></span>
* <span data-ttu-id="9d886-255">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span><span class="sxs-lookup"><span data-stu-id="9d886-255">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="9d886-256">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span><span class="sxs-lookup"><span data-stu-id="9d886-256">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span></span>
* <span data-ttu-id="9d886-257">Added methods to the IDocumentClient interface that were missing:</span><span class="sxs-lookup"><span data-stu-id="9d886-257">Added methods to the IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="9d886-258">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span><span class="sxs-lookup"><span data-stu-id="9d886-258">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="9d886-259">CreateAttachmentAsync method that takes options as a parameter</span><span class="sxs-lookup"><span data-stu-id="9d886-259">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="9d886-260">CreateOfferQuery method that takes querySpec as a parameter.</span><span class="sxs-lookup"><span data-stu-id="9d886-260">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="9d886-261">Unsealed public classes that are exposed in the IDocumentClient interface.</span><span class="sxs-lookup"><span data-stu-id="9d886-261">Unsealed public classes that are exposed in the IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="9d886-262"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="9d886-262"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="9d886-263">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="9d886-263">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="9d886-264">Added support for retry on throttled requests.</span><span class="sxs-lookup"><span data-stu-id="9d886-264">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="9d886-265">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span><span class="sxs-lookup"><span data-stu-id="9d886-265">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="9d886-266">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span><span class="sxs-lookup"><span data-stu-id="9d886-266">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="9d886-267">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span><span class="sxs-lookup"><span data-stu-id="9d886-267">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span></span>
* <span data-ttu-id="9d886-268">Added configuration option to set the ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span><span class="sxs-lookup"><span data-stu-id="9d886-268">Added configuration option to set the ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span></span>  <span data-ttu-id="9d886-269">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span><span class="sxs-lookup"><span data-stu-id="9d886-269">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span></span>
* <span data-ttu-id="9d886-270">Deprecated IPartitionResolver and its implementation.</span><span class="sxs-lookup"><span data-stu-id="9d886-270">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="9d886-271">Support for IPartitionResolver is now obsolete.</span><span class="sxs-lookup"><span data-stu-id="9d886-271">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="9d886-272">It's recommended that you use Partitioned Collections for higher storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="9d886-272">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="9d886-273"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="9d886-273"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="9d886-274">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span><span class="sxs-lookup"><span data-stu-id="9d886-274">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="9d886-275"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="9d886-275"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="9d886-276">Added time to live (TTL) support for documents.</span><span class="sxs-lookup"><span data-stu-id="9d886-276">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="9d886-277"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="9d886-277"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="9d886-278">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span><span class="sxs-lookup"><span data-stu-id="9d886-278">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="9d886-279"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="9d886-279"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="9d886-280">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9d886-280">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="9d886-281"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="9d886-281"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="9d886-282">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span><span class="sxs-lookup"><span data-stu-id="9d886-282">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="9d886-283"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="9d886-283"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="9d886-284">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span><span class="sxs-lookup"><span data-stu-id="9d886-284">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span></span>
  * <span data-ttu-id="9d886-285">Take operator to enable SELECT TOP behavior in LINQ</span><span class="sxs-lookup"><span data-stu-id="9d886-285">Take operator to enable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="9d886-286">CompareTo operator to enable string range comparisons</span><span class="sxs-lookup"><span data-stu-id="9d886-286">CompareTo operator to enable string range comparisons</span></span>
  * <span data-ttu-id="9d886-287">Conditional (?) and coalesce operators (??)</span><span class="sxs-lookup"><span data-stu-id="9d886-287">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="9d886-288">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span><span class="sxs-lookup"><span data-stu-id="9d886-288">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span></span> [<span data-ttu-id="9d886-289">#81</span><span class="sxs-lookup"><span data-stu-id="9d886-289">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="9d886-290"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="9d886-290"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="9d886-291">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT \* incorrectly.</span><span class="sxs-lookup"><span data-stu-id="9d886-291">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT \* incorrectly.</span></span>  [<span data-ttu-id="9d886-292">#58</span><span class="sxs-lookup"><span data-stu-id="9d886-292">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="9d886-293"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="9d886-293"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="9d886-294">Implemented Upsert, Added UpsertXXXAsync methods</span><span class="sxs-lookup"><span data-stu-id="9d886-294">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="9d886-295">Performance improvements for all requests</span><span class="sxs-lookup"><span data-stu-id="9d886-295">Performance improvements for all requests</span></span>
* <span data-ttu-id="9d886-296">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span><span class="sxs-lookup"><span data-stu-id="9d886-296">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span></span>
* <span data-ttu-id="9d886-297">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span><span class="sxs-lookup"><span data-stu-id="9d886-297">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="9d886-298">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span><span class="sxs-lookup"><span data-stu-id="9d886-298">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="9d886-299">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span><span class="sxs-lookup"><span data-stu-id="9d886-299">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="9d886-300"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="9d886-300"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="9d886-301">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span><span class="sxs-lookup"><span data-stu-id="9d886-301">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="9d886-302"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="9d886-302"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="9d886-303">Added ID-based routing</span><span class="sxs-lookup"><span data-stu-id="9d886-303">Added ID-based routing</span></span>
  * <span data-ttu-id="9d886-304">New UriFactory helper to assist with constructing ID-based resource links</span><span class="sxs-lookup"><span data-stu-id="9d886-304">New UriFactory helper to assist with constructing ID-based resource links</span></span>
  * <span data-ttu-id="9d886-305">New overloads on DocumentClient to take in URI</span><span class="sxs-lookup"><span data-stu-id="9d886-305">New overloads on DocumentClient to take in URI</span></span>
* <span data-ttu-id="9d886-306">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span><span class="sxs-lookup"><span data-stu-id="9d886-306">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="9d886-307">LINQ Provider support enhanced:</span><span class="sxs-lookup"><span data-stu-id="9d886-307">LINQ Provider support enhanced:</span></span>
  * <span data-ttu-id="9d886-308">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span><span class="sxs-lookup"><span data-stu-id="9d886-308">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="9d886-309">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span><span class="sxs-lookup"><span data-stu-id="9d886-309">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="9d886-310">**Array** - Concat, Contains, Count</span><span class="sxs-lookup"><span data-stu-id="9d886-310">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="9d886-311">**IN** operator</span><span class="sxs-lookup"><span data-stu-id="9d886-311">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="9d886-312"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="9d886-312"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="9d886-313">Added support for modifying indexing policies.</span><span class="sxs-lookup"><span data-stu-id="9d886-313">Added support for modifying indexing policies.</span></span>
  * <span data-ttu-id="9d886-314">New ReplaceDocumentCollectionAsync method in DocumentClient</span><span class="sxs-lookup"><span data-stu-id="9d886-314">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="9d886-315">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span><span class="sxs-lookup"><span data-stu-id="9d886-315">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="9d886-316">DocumentCollection.IndexingPolicy is now mutable</span><span class="sxs-lookup"><span data-stu-id="9d886-316">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="9d886-317">Added support for spatial indexing and query.</span><span class="sxs-lookup"><span data-stu-id="9d886-317">Added support for spatial indexing and query.</span></span>
  * <span data-ttu-id="9d886-318">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span><span class="sxs-lookup"><span data-stu-id="9d886-318">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="9d886-319">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9d886-319">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span></span>
* <span data-ttu-id="9d886-320">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span><span class="sxs-lookup"><span data-stu-id="9d886-320">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span></span>

### <a name="a-name120120"></a><span data-ttu-id="9d886-321"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="9d886-321"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="9d886-322">Added a dependency on Newtonsoft.Json v5.0.7.</span><span class="sxs-lookup"><span data-stu-id="9d886-322">Added a dependency on Newtonsoft.Json v5.0.7.</span></span>
* <span data-ttu-id="9d886-323">Made changes to support Order By:</span><span class="sxs-lookup"><span data-stu-id="9d886-323">Made changes to support Order By:</span></span>
  
  * <span data-ttu-id="9d886-324">LINQ provider support for OrderBy() or OrderByDescending()</span><span class="sxs-lookup"><span data-stu-id="9d886-324">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="9d886-325">IndexingPolicy to support Order By</span><span class="sxs-lookup"><span data-stu-id="9d886-325">IndexingPolicy to support Order By</span></span> 
    
    <span data-ttu-id="9d886-326">**Possible breaking change**</span><span class="sxs-lookup"><span data-stu-id="9d886-326">**Possible breaking change**</span></span> 
    
    <span data-ttu-id="9d886-327">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs to be updated to support the new IndexingPolicy class.</span><span class="sxs-lookup"><span data-stu-id="9d886-327">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs to be updated to support the new IndexingPolicy class.</span></span> <span data-ttu-id="9d886-328">If you have no custom indexing policy, then this change does not affect you.</span><span class="sxs-lookup"><span data-stu-id="9d886-328">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="9d886-329"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="9d886-329"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="9d886-330">Added support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="9d886-330">Added support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver.</span></span>
* <span data-ttu-id="9d886-331">Added DataContract serialization.</span><span class="sxs-lookup"><span data-stu-id="9d886-331">Added DataContract serialization.</span></span>
* <span data-ttu-id="9d886-332">Added GUID support in LINQ provider.</span><span class="sxs-lookup"><span data-stu-id="9d886-332">Added GUID support in LINQ provider.</span></span>
* <span data-ttu-id="9d886-333">Added UDF support in LINQ.</span><span class="sxs-lookup"><span data-stu-id="9d886-333">Added UDF support in LINQ.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="9d886-334"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="9d886-334"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="9d886-335">GA SDK</span><span class="sxs-lookup"><span data-stu-id="9d886-335">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="9d886-336">Release & Retirement dates</span><span class="sxs-lookup"><span data-stu-id="9d886-336">Release & Retirement dates</span></span>
<span data-ttu-id="9d886-337">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="9d886-337">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="9d886-338">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="9d886-338">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="9d886-339">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="9d886-339">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span></span>

<br/>

| <span data-ttu-id="9d886-340">Version</span><span class="sxs-lookup"><span data-stu-id="9d886-340">Version</span></span> | <span data-ttu-id="9d886-341">Release Date</span><span class="sxs-lookup"><span data-stu-id="9d886-341">Release Date</span></span> | <span data-ttu-id="9d886-342">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="9d886-342">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9d886-343">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9d886-343">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="9d886-344">September 07, 2018</span><span class="sxs-lookup"><span data-stu-id="9d886-344">September 07, 2018</span></span> |--- |
| [<span data-ttu-id="9d886-345">1.22.0</span><span class="sxs-lookup"><span data-stu-id="9d886-345">1.22.0</span></span>](#1.22.0) |<span data-ttu-id="9d886-346">April 19, 2018</span><span class="sxs-lookup"><span data-stu-id="9d886-346">April 19, 2018</span></span> |--- |
| [<span data-ttu-id="9d886-347">1.21.1</span><span class="sxs-lookup"><span data-stu-id="9d886-347">1.21.1</span></span>](#1.20.1) |<span data-ttu-id="9d886-348">March 09, 2018</span><span class="sxs-lookup"><span data-stu-id="9d886-348">March 09, 2018</span></span> |--- |
| [<span data-ttu-id="9d886-349">1.20.2</span><span class="sxs-lookup"><span data-stu-id="9d886-349">1.20.2</span></span>](#1.20.1) |<span data-ttu-id="9d886-350">February 21, 2018</span><span class="sxs-lookup"><span data-stu-id="9d886-350">February 21, 2018</span></span> |--- |
| [<span data-ttu-id="9d886-351">1.20.1</span><span class="sxs-lookup"><span data-stu-id="9d886-351">1.20.1</span></span>](#1.20.1) |<span data-ttu-id="9d886-352">February 05, 2018</span><span class="sxs-lookup"><span data-stu-id="9d886-352">February 05, 2018</span></span> |--- |
| [<span data-ttu-id="9d886-353">1.19.1</span><span class="sxs-lookup"><span data-stu-id="9d886-353">1.19.1</span></span>](#1.19.1) |<span data-ttu-id="9d886-354">November 16, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-354">November 16, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-355">1.19.0</span><span class="sxs-lookup"><span data-stu-id="9d886-355">1.19.0</span></span>](#1.19.0) |<span data-ttu-id="9d886-356">November 10, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-356">November 10, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-357">1.18.1</span><span class="sxs-lookup"><span data-stu-id="9d886-357">1.18.1</span></span>](#1.18.1) |<span data-ttu-id="9d886-358">November 07, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-358">November 07, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-359">1.18.0</span><span class="sxs-lookup"><span data-stu-id="9d886-359">1.18.0</span></span>](#1.18.0) |<span data-ttu-id="9d886-360">October 17, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-360">October 17, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-361">1.17.0</span><span class="sxs-lookup"><span data-stu-id="9d886-361">1.17.0</span></span>](#1.17.0) |<span data-ttu-id="9d886-362">August 10, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-362">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-363">1.16.1</span><span class="sxs-lookup"><span data-stu-id="9d886-363">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="9d886-364">August 07, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-364">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-365">1.16.0</span><span class="sxs-lookup"><span data-stu-id="9d886-365">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="9d886-366">August 02, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-366">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-367">1.15.0</span><span class="sxs-lookup"><span data-stu-id="9d886-367">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="9d886-368">June 30, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-368">June 30, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-369">1.14.1</span><span class="sxs-lookup"><span data-stu-id="9d886-369">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="9d886-370">May 23, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-370">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-371">1.14.0</span><span class="sxs-lookup"><span data-stu-id="9d886-371">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="9d886-372">May 10, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-372">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-373">1.13.4</span><span class="sxs-lookup"><span data-stu-id="9d886-373">1.13.4</span></span>](#1.13.4) |<span data-ttu-id="9d886-374">May 09, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-374">May 09, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-375">1.13.3</span><span class="sxs-lookup"><span data-stu-id="9d886-375">1.13.3</span></span>](#1.13.3) |<span data-ttu-id="9d886-376">May 06, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-376">May 06, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-377">1.13.2</span><span class="sxs-lookup"><span data-stu-id="9d886-377">1.13.2</span></span>](#1.13.2) |<span data-ttu-id="9d886-378">April 19, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-378">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-379">1.13.1</span><span class="sxs-lookup"><span data-stu-id="9d886-379">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="9d886-380">March 29, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-380">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-381">1.13.0</span><span class="sxs-lookup"><span data-stu-id="9d886-381">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="9d886-382">March 24, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-382">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-383">1.12.2</span><span class="sxs-lookup"><span data-stu-id="9d886-383">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="9d886-384">March 20, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-384">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-385">1.12.1</span><span class="sxs-lookup"><span data-stu-id="9d886-385">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="9d886-386">March 14, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-386">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-387">1.12.0</span><span class="sxs-lookup"><span data-stu-id="9d886-387">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="9d886-388">February 15, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-388">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-389">1.11.4</span><span class="sxs-lookup"><span data-stu-id="9d886-389">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="9d886-390">February 06, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-390">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-391">1.11.3</span><span class="sxs-lookup"><span data-stu-id="9d886-391">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="9d886-392">January 26, 2017</span><span class="sxs-lookup"><span data-stu-id="9d886-392">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="9d886-393">1.11.1</span><span class="sxs-lookup"><span data-stu-id="9d886-393">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="9d886-394">December 21, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-394">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-395">1.11.0</span><span class="sxs-lookup"><span data-stu-id="9d886-395">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="9d886-396">December 08, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-396">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-397">1.10.0</span><span class="sxs-lookup"><span data-stu-id="9d886-397">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="9d886-398">September 27, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-398">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-399">1.9.5</span><span class="sxs-lookup"><span data-stu-id="9d886-399">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="9d886-400">September 01, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-400">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-401">1.9.4</span><span class="sxs-lookup"><span data-stu-id="9d886-401">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="9d886-402">August 24, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-402">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-403">1.9.3</span><span class="sxs-lookup"><span data-stu-id="9d886-403">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="9d886-404">August 15, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-404">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-405">1.9.2</span><span class="sxs-lookup"><span data-stu-id="9d886-405">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="9d886-406">July 23, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-406">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-407">1.8.0</span><span class="sxs-lookup"><span data-stu-id="9d886-407">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="9d886-408">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-408">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-409">1.7.1</span><span class="sxs-lookup"><span data-stu-id="9d886-409">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="9d886-410">May 06, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-410">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-411">1.7.0</span><span class="sxs-lookup"><span data-stu-id="9d886-411">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="9d886-412">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-412">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-413">1.6.3</span><span class="sxs-lookup"><span data-stu-id="9d886-413">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="9d886-414">April 08, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-414">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-415">1.6.2</span><span class="sxs-lookup"><span data-stu-id="9d886-415">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="9d886-416">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-416">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-417">1.5.3</span><span class="sxs-lookup"><span data-stu-id="9d886-417">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="9d886-418">February 19, 2016</span><span class="sxs-lookup"><span data-stu-id="9d886-418">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="9d886-419">1.5.2</span><span class="sxs-lookup"><span data-stu-id="9d886-419">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="9d886-420">December 14, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-420">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-421">1.5.1</span><span class="sxs-lookup"><span data-stu-id="9d886-421">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="9d886-422">November 23, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-422">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-423">1.5.0</span><span class="sxs-lookup"><span data-stu-id="9d886-423">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="9d886-424">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-424">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-425">1.4.1</span><span class="sxs-lookup"><span data-stu-id="9d886-425">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="9d886-426">August 25, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-426">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-427">1.4.0</span><span class="sxs-lookup"><span data-stu-id="9d886-427">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="9d886-428">August 13, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-428">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-429">1.3.0</span><span class="sxs-lookup"><span data-stu-id="9d886-429">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="9d886-430">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-430">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-431">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9d886-431">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="9d886-432">July 06, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-432">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-433">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9d886-433">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="9d886-434">April 30, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-434">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="9d886-435">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9d886-435">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="9d886-436">April 08, 2015</span><span class="sxs-lookup"><span data-stu-id="9d886-436">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="9d886-437">FAQ</span><span class="sxs-lookup"><span data-stu-id="9d886-437">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="9d886-438">See also</span><span class="sxs-lookup"><span data-stu-id="9d886-438">See also</span></span>
<span data-ttu-id="9d886-439">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="9d886-439">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

