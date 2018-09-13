---
title: 'Azure Cosmos DB: SQL Java API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL Java API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB SQL Java SDK.
services: cosmos-db
author: rnagpal
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 06/29/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7d00d6236b601d145be03e6086bec2d72faafcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869189"
---
# <a name="azure-cosmos-db-java-sdk-for-sql-api-release-notes-and-resources"></a><span data-ttu-id="c849c-103">Azure Cosmos DB Java SDK for SQL API: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="c849c-103">Azure Cosmos DB Java SDK for SQL API: Release notes and resources</span></span>
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

<span data-ttu-id="c849c-116">The SQL API Java SDK supports synchronous operations.</span><span class="sxs-lookup"><span data-stu-id="c849c-116">The SQL API Java SDK supports synchronous operations.</span></span> <span data-ttu-id="c849c-117">For asynchronous support, use the [SQL API Async Java SDK](sql-api-sdk-async-java.md).</span><span class="sxs-lookup"><span data-stu-id="c849c-117">For asynchronous support, use the [SQL API Async Java SDK](sql-api-sdk-async-java.md).</span></span> 

<table>

<tr><td><span data-ttu-id="c849c-118">**SDK Download**</span><span class="sxs-lookup"><span data-stu-id="c849c-118">**SDK Download**</span></span></td><td>[<span data-ttu-id="c849c-119">Maven</span><span class="sxs-lookup"><span data-stu-id="c849c-119">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="c849c-120">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="c849c-120">**API documentation**</span></span></td><td>[<span data-ttu-id="c849c-121">Java API reference documentation</span><span class="sxs-lookup"><span data-stu-id="c849c-121">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="c849c-122">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="c849c-122">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="c849c-123">GitHub</span><span class="sxs-lookup"><span data-stu-id="c849c-123">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="c849c-124">**Get started**</span><span class="sxs-lookup"><span data-stu-id="c849c-124">**Get started**</span></span></td><td>[<span data-ttu-id="c849c-125">Get started with the Java SDK</span><span class="sxs-lookup"><span data-stu-id="c849c-125">Get started with the Java SDK</span></span>](sql-api-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="c849c-126">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="c849c-126">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="c849c-127">Web application development with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c849c-127">Web application development with Azure Cosmos DB</span></span>](sql-api-java-application.md)</td></tr>

<tr><td><span data-ttu-id="c849c-128">**Minimum supported runtime**</span><span class="sxs-lookup"><span data-stu-id="c849c-128">**Minimum supported runtime**</span></span></td><td>[<span data-ttu-id="c849c-129">JDK 7</span><span class="sxs-lookup"><span data-stu-id="c849c-129">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="c849c-130">Release notes</span><span class="sxs-lookup"><span data-stu-id="c849c-130">Release notes</span></span>

### <a name="a-name11621162"></a><span data-ttu-id="c849c-131"><a name="1.16.2"/>1.16.2</span><span class="sxs-lookup"><span data-stu-id="c849c-131"><a name="1.16.2"/>1.16.2</span></span>
* <span data-ttu-id="c849c-132">Added streaming fail over support.</span><span class="sxs-lookup"><span data-stu-id="c849c-132">Added streaming fail over support.</span></span>
* <span data-ttu-id="c849c-133">Added support for custom metadata.</span><span class="sxs-lookup"><span data-stu-id="c849c-133">Added support for custom metadata.</span></span>
* <span data-ttu-id="c849c-134">Improved session handling logic.</span><span class="sxs-lookup"><span data-stu-id="c849c-134">Improved session handling logic.</span></span>
* <span data-ttu-id="c849c-135">Fixed a bug in partition key range cache.</span><span class="sxs-lookup"><span data-stu-id="c849c-135">Fixed a bug in partition key range cache.</span></span>
* <span data-ttu-id="c849c-136">Fixed a NPE bug in direct mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-136">Fixed a NPE bug in direct mode.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="c849c-137"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="c849c-137"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="c849c-138">Added support for Unique Index.</span><span class="sxs-lookup"><span data-stu-id="c849c-138">Added support for Unique Index.</span></span>
* <span data-ttu-id="c849c-139">Added support for limiting continuation token size in feed-options.</span><span class="sxs-lookup"><span data-stu-id="c849c-139">Added support for limiting continuation token size in feed-options.</span></span>
* <span data-ttu-id="c849c-140">Fixed a bug in Json Serialization (timestamp).</span><span class="sxs-lookup"><span data-stu-id="c849c-140">Fixed a bug in Json Serialization (timestamp).</span></span>
* <span data-ttu-id="c849c-141">Fixed a bug in Json Serialization (enum).</span><span class="sxs-lookup"><span data-stu-id="c849c-141">Fixed a bug in Json Serialization (enum).</span></span>
* <span data-ttu-id="c849c-142">Dependency on com.fasterxml.jackson.core:jackson-databind upgraded to 2.9.5.</span><span class="sxs-lookup"><span data-stu-id="c849c-142">Dependency on com.fasterxml.jackson.core:jackson-databind upgraded to 2.9.5.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="c849c-143"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="c849c-143"><a name="1.16.0"/>1.16.0</span></span>
* <span data-ttu-id="c849c-144">Improved Connection Pooling for Direct Mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-144">Improved Connection Pooling for Direct Mode.</span></span>
* <span data-ttu-id="c849c-145">Improved Prefetch improvement for non-orderby cross partition query.</span><span class="sxs-lookup"><span data-stu-id="c849c-145">Improved Prefetch improvement for non-orderby cross partition query.</span></span>
* <span data-ttu-id="c849c-146">Improved UUID generation.</span><span class="sxs-lookup"><span data-stu-id="c849c-146">Improved UUID generation.</span></span>
* <span data-ttu-id="c849c-147">Improved Session consistency logic.</span><span class="sxs-lookup"><span data-stu-id="c849c-147">Improved Session consistency logic.</span></span>
* <span data-ttu-id="c849c-148">Added support for multipolygon.</span><span class="sxs-lookup"><span data-stu-id="c849c-148">Added support for multipolygon.</span></span>
* <span data-ttu-id="c849c-149">Added support for Partition Key Range Statistics for Collection.</span><span class="sxs-lookup"><span data-stu-id="c849c-149">Added support for Partition Key Range Statistics for Collection.</span></span>
* <span data-ttu-id="c849c-150">Fixed a bug in Multi-region support.</span><span class="sxs-lookup"><span data-stu-id="c849c-150">Fixed a bug in Multi-region support.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="c849c-151"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="c849c-151"><a name="1.15.0"/>1.15.0</span></span>
* <span data-ttu-id="c849c-152">Improved Json Serialization performance.</span><span class="sxs-lookup"><span data-stu-id="c849c-152">Improved Json Serialization performance.</span></span>
* <span data-ttu-id="c849c-153">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span><span class="sxs-lookup"><span data-stu-id="c849c-153">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="c849c-154"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="c849c-154"><a name="1.14.0"/>1.14.0</span></span>
* <span data-ttu-id="c849c-155">Internal changes for Microsoft friends libraries.</span><span class="sxs-lookup"><span data-stu-id="c849c-155">Internal changes for Microsoft friends libraries.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="c849c-156"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="c849c-156"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="c849c-157">Fixed an issue in reading single partition key ranges.</span><span class="sxs-lookup"><span data-stu-id="c849c-157">Fixed an issue in reading single partition key ranges.</span></span>
* <span data-ttu-id="c849c-158">Fixed an issue in ResourceID parsing that affects database with short names.</span><span class="sxs-lookup"><span data-stu-id="c849c-158">Fixed an issue in ResourceID parsing that affects database with short names.</span></span>
* <span data-ttu-id="c849c-159">Fixed an issue cause by partition key encoding.</span><span class="sxs-lookup"><span data-stu-id="c849c-159">Fixed an issue cause by partition key encoding.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="c849c-160"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="c849c-160"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="c849c-161">Critical bug fixes to request processing during partition splits.</span><span class="sxs-lookup"><span data-stu-id="c849c-161">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="c849c-162">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span><span class="sxs-lookup"><span data-stu-id="c849c-162">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="c849c-163"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="c849c-163"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="c849c-164">Added support for a new consistency level called ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="c849c-164">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="c849c-165">Fixed a bug in reading collection in session mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-165">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="c849c-166"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="c849c-166"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="c849c-167">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span><span class="sxs-lookup"><span data-stu-id="c849c-167">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="c849c-168">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span><span class="sxs-lookup"><span data-stu-id="c849c-168">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="c849c-169"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="c849c-169"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="c849c-170">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-170">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="c849c-171">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span><span class="sxs-lookup"><span data-stu-id="c849c-171">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="c849c-172"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="c849c-172"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="c849c-173">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="c849c-173">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="c849c-174">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="c849c-174">See [Aggregation support](sql-api-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="c849c-175">Added support for change feed.</span><span class="sxs-lookup"><span data-stu-id="c849c-175">Added support for change feed.</span></span>
* <span data-ttu-id="c849c-176">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="c849c-176">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="c849c-177">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="c849c-177">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="c849c-178">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span><span class="sxs-lookup"><span data-stu-id="c849c-178">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="c849c-179">Fixed a bug in session consistency mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-179">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="c849c-180">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span><span class="sxs-lookup"><span data-stu-id="c849c-180">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="c849c-181">Improved performance of DirectHttps mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-181">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="c849c-182"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="c849c-182"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="c849c-183">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span><span class="sxs-lookup"><span data-stu-id="c849c-183">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="c849c-184">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span><span class="sxs-lookup"><span data-stu-id="c849c-184">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="c849c-185">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span><span class="sxs-lookup"><span data-stu-id="c849c-185">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="c849c-186">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span><span class="sxs-lookup"><span data-stu-id="c849c-186">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="c849c-187">Refactored logging to use SLF4J.</span><span class="sxs-lookup"><span data-stu-id="c849c-187">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="c849c-188">Fixed a few other bugs in consistency reader.</span><span class="sxs-lookup"><span data-stu-id="c849c-188">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="c849c-189"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="c849c-189"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="c849c-190">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span><span class="sxs-lookup"><span data-stu-id="c849c-190">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="c849c-191">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span><span class="sxs-lookup"><span data-stu-id="c849c-191">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="c849c-192">Improved performance by reducing the number of network call for the internal caches.</span><span class="sxs-lookup"><span data-stu-id="c849c-192">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="c849c-193">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="c849c-193">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="c849c-194"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="c849c-194"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="c849c-195">Fixed an issue in the connection management for stability.</span><span class="sxs-lookup"><span data-stu-id="c849c-195">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="c849c-196"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="c849c-196"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="c849c-197">Added support for BoundedStaleness consistency level.</span><span class="sxs-lookup"><span data-stu-id="c849c-197">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="c849c-198">Added support for direct connectivity for CRUD operations for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="c849c-198">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="c849c-199">Fixed a bug in querying a database with SQL.</span><span class="sxs-lookup"><span data-stu-id="c849c-199">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="c849c-200">Fixed a bug in the session cache where session token may be set incorrectly.</span><span class="sxs-lookup"><span data-stu-id="c849c-200">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="c849c-201"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="c849c-201"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="c849c-202">Added support for cross partition parallel queries.</span><span class="sxs-lookup"><span data-stu-id="c849c-202">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="c849c-203">Added support for TOP/ORDER BY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="c849c-203">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="c849c-204">Added support for strong consistency.</span><span class="sxs-lookup"><span data-stu-id="c849c-204">Added support for strong consistency.</span></span>
* <span data-ttu-id="c849c-205">Added support for name based requests when using direct connectivity.</span><span class="sxs-lookup"><span data-stu-id="c849c-205">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="c849c-206">Fixed to make ActivityId stay consistent across all request retries.</span><span class="sxs-lookup"><span data-stu-id="c849c-206">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="c849c-207">Fixed a bug related to the session cache when recreating a collection with the same name.</span><span class="sxs-lookup"><span data-stu-id="c849c-207">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="c849c-208">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span><span class="sxs-lookup"><span data-stu-id="c849c-208">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="c849c-209">Fixed issues with Java Doc for Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="c849c-209">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="c849c-210"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="c849c-210"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="c849c-211">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span><span class="sxs-lookup"><span data-stu-id="c849c-211">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="c849c-212">Fixed a bug to not retry when an incorrect partition key value is provided.</span><span class="sxs-lookup"><span data-stu-id="c849c-212">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="c849c-213"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="c849c-213"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="c849c-214">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="c849c-214">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="c849c-215">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span><span class="sxs-lookup"><span data-stu-id="c849c-215">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="c849c-216">See RetryOptions and ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="c849c-216">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="c849c-217">Deprecated IPartitionResolver based custom partitioning code.</span><span class="sxs-lookup"><span data-stu-id="c849c-217">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="c849c-218">Please use partitioned collections for higher storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="c849c-218">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="c849c-219"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="c849c-219"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="c849c-220">Added retry policy support for rate limiting.</span><span class="sxs-lookup"><span data-stu-id="c849c-220">Added retry policy support for rate limiting.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="c849c-221"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="c849c-221"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="c849c-222">Added time to live (TTL) support for documents.</span><span class="sxs-lookup"><span data-stu-id="c849c-222">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="c849c-223"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="c849c-223"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="c849c-224">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c849c-224">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="c849c-225"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="c849c-225"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="c849c-226">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span><span class="sxs-lookup"><span data-stu-id="c849c-226">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="c849c-227"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="c849c-227"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="c849c-228">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="c849c-228">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="c849c-229"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="c849c-229"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="c849c-230">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="c849c-230">Implement Upsert.</span></span> <span data-ttu-id="c849c-231">New upsertXXX methods added to support Upsert feature.</span><span class="sxs-lookup"><span data-stu-id="c849c-231">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="c849c-232">Implement ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="c849c-232">Implement ID Based Routing.</span></span> <span data-ttu-id="c849c-233">No public API changes, all changes internal.</span><span class="sxs-lookup"><span data-stu-id="c849c-233">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="c849c-234"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="c849c-234"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="c849c-235">Release skipped to bring version number in alignment with other SDKs</span><span class="sxs-lookup"><span data-stu-id="c849c-235">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="c849c-236"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="c849c-236"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="c849c-237">Supports GeoSpatial Index</span><span class="sxs-lookup"><span data-stu-id="c849c-237">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="c849c-238">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="c849c-238">Validates id property for all resources.</span></span> <span data-ttu-id="c849c-239">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="c849c-239">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="c849c-240">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="c849c-240">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="c849c-241"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="c849c-241"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="c849c-242">Implements V2 indexing policy</span><span class="sxs-lookup"><span data-stu-id="c849c-242">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="c849c-243"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="c849c-243"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="c849c-244">GA SDK</span><span class="sxs-lookup"><span data-stu-id="c849c-244">GA SDK</span></span>

## <a name="release-and-retirement-dates"></a><span data-ttu-id="c849c-245">Release and retirement dates</span><span class="sxs-lookup"><span data-stu-id="c849c-245">Release and retirement dates</span></span>
<span data-ttu-id="c849c-246">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="c849c-246">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="c849c-247">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="c849c-247">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="c849c-248">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="c849c-248">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> All versions of the SQL SDK for Java prior to version **1.0.0** were retired on **February 29, 2016**.
> 
> 

<br/>

| <span data-ttu-id="c849c-250">Version</span><span class="sxs-lookup"><span data-stu-id="c849c-250">Version</span></span> | <span data-ttu-id="c849c-251">Release Date</span><span class="sxs-lookup"><span data-stu-id="c849c-251">Release Date</span></span> | <span data-ttu-id="c849c-252">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="c849c-252">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c849c-253">1.16.2</span><span class="sxs-lookup"><span data-stu-id="c849c-253">1.16.2</span></span>](#1.16.2) |<span data-ttu-id="c849c-254">June 29, 2018</span><span class="sxs-lookup"><span data-stu-id="c849c-254">June 29, 2018</span></span> |--- |
| [<span data-ttu-id="c849c-255">1.16.1</span><span class="sxs-lookup"><span data-stu-id="c849c-255">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="c849c-256">May 16, 2018</span><span class="sxs-lookup"><span data-stu-id="c849c-256">May 16, 2018</span></span> |--- |
| [<span data-ttu-id="c849c-257">1.16.0</span><span class="sxs-lookup"><span data-stu-id="c849c-257">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="c849c-258">March 15, 2018</span><span class="sxs-lookup"><span data-stu-id="c849c-258">March 15, 2018</span></span> |--- |
| [<span data-ttu-id="c849c-259">1.15.0</span><span class="sxs-lookup"><span data-stu-id="c849c-259">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="c849c-260">Nov 14, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-260">Nov 14, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-261">1.14.0</span><span class="sxs-lookup"><span data-stu-id="c849c-261">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="c849c-262">Oct 28, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-262">Oct 28, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-263">1.13.0</span><span class="sxs-lookup"><span data-stu-id="c849c-263">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="c849c-264">August 25, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-264">August 25, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-265">1.12.0</span><span class="sxs-lookup"><span data-stu-id="c849c-265">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="c849c-266">July 11, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-266">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-267">1.11.0</span><span class="sxs-lookup"><span data-stu-id="c849c-267">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="c849c-268">May 10, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-268">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-269">1.10.0</span><span class="sxs-lookup"><span data-stu-id="c849c-269">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="c849c-270">March 11, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-270">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-271">1.9.6</span><span class="sxs-lookup"><span data-stu-id="c849c-271">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="c849c-272">February 21, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-272">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-273">1.9.5</span><span class="sxs-lookup"><span data-stu-id="c849c-273">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="c849c-274">January 31, 2017</span><span class="sxs-lookup"><span data-stu-id="c849c-274">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="c849c-275">1.9.4</span><span class="sxs-lookup"><span data-stu-id="c849c-275">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="c849c-276">November 24, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-276">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-277">1.9.3</span><span class="sxs-lookup"><span data-stu-id="c849c-277">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="c849c-278">October 30, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-278">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-279">1.9.2</span><span class="sxs-lookup"><span data-stu-id="c849c-279">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="c849c-280">October 28, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-280">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-281">1.9.1</span><span class="sxs-lookup"><span data-stu-id="c849c-281">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="c849c-282">October 26, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-282">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-283">1.9.0</span><span class="sxs-lookup"><span data-stu-id="c849c-283">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="c849c-284">October 03, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-284">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-285">1.8.1</span><span class="sxs-lookup"><span data-stu-id="c849c-285">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="c849c-286">June 30, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-286">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-287">1.8.0</span><span class="sxs-lookup"><span data-stu-id="c849c-287">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="c849c-288">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-288">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-289">1.7.1</span><span class="sxs-lookup"><span data-stu-id="c849c-289">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="c849c-290">April 30, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-290">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-291">1.7.0</span><span class="sxs-lookup"><span data-stu-id="c849c-291">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="c849c-292">April 27, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-292">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-293">1.6.0</span><span class="sxs-lookup"><span data-stu-id="c849c-293">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="c849c-294">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-294">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="c849c-295">1.5.1</span><span class="sxs-lookup"><span data-stu-id="c849c-295">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="c849c-296">December 31, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-296">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-297">1.5.0</span><span class="sxs-lookup"><span data-stu-id="c849c-297">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="c849c-298">December 04, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-298">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-299">1.4.0</span><span class="sxs-lookup"><span data-stu-id="c849c-299">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="c849c-300">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-300">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-301">1.3.0</span><span class="sxs-lookup"><span data-stu-id="c849c-301">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="c849c-302">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-302">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-303">1.2.0</span><span class="sxs-lookup"><span data-stu-id="c849c-303">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="c849c-304">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-304">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-305">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c849c-305">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c849c-306">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-306">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-307">1.0.1</span><span class="sxs-lookup"><span data-stu-id="c849c-307">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="c849c-308">May 12, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-308">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="c849c-309">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c849c-309">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c849c-310">April 07, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-310">April 07, 2015</span></span> |--- |
| <span data-ttu-id="c849c-311">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-311">0.9.5-prelease</span></span> |<span data-ttu-id="c849c-312">Mar 09, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-312">Mar 09, 2015</span></span> |<span data-ttu-id="c849c-313">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-313">February 29, 2016</span></span> |
| <span data-ttu-id="c849c-314">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-314">0.9.4-prelease</span></span> |<span data-ttu-id="c849c-315">February 17, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-315">February 17, 2015</span></span> |<span data-ttu-id="c849c-316">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-316">February 29, 2016</span></span> |
| <span data-ttu-id="c849c-317">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-317">0.9.3-prelease</span></span> |<span data-ttu-id="c849c-318">January 13, 2015</span><span class="sxs-lookup"><span data-stu-id="c849c-318">January 13, 2015</span></span> |<span data-ttu-id="c849c-319">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-319">February 29, 2016</span></span> |
| <span data-ttu-id="c849c-320">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-320">0.9.2-prelease</span></span> |<span data-ttu-id="c849c-321">December 19, 2014</span><span class="sxs-lookup"><span data-stu-id="c849c-321">December 19, 2014</span></span> |<span data-ttu-id="c849c-322">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-322">February 29, 2016</span></span> |
| <span data-ttu-id="c849c-323">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-323">0.9.1-prelease</span></span> |<span data-ttu-id="c849c-324">December 19, 2014</span><span class="sxs-lookup"><span data-stu-id="c849c-324">December 19, 2014</span></span> |<span data-ttu-id="c849c-325">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-325">February 29, 2016</span></span> |
| <span data-ttu-id="c849c-326">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="c849c-326">0.9.0-prelease</span></span> |<span data-ttu-id="c849c-327">December 10, 2014</span><span class="sxs-lookup"><span data-stu-id="c849c-327">December 10, 2014</span></span> |<span data-ttu-id="c849c-328">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="c849c-328">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="c849c-329">FAQ</span><span class="sxs-lookup"><span data-stu-id="c849c-329">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c849c-330">See also</span><span class="sxs-lookup"><span data-stu-id="c849c-330">See also</span></span>
<span data-ttu-id="c849c-331">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="c849c-331">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

