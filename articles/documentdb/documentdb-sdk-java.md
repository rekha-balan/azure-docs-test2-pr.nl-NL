---
title: Azure DocumentDB Java API, SDK & Resources | Microsoft Docs
description: Learn all about the Java API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB Java SDK.
services: documentdb
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 03/16/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40ea65f692d1e2cbc39a6c65b2f8b255282e34cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563759"
---
# <a name="documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="ff084-103">DocumentDB Java SDK: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="ff084-103">DocumentDB Java SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/en-us/rest/api/documentdb/)
> * [REST Resource Provider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="ff084-112">**SDK Download**</span><span class="sxs-lookup"><span data-stu-id="ff084-112">**SDK Download**</span></span></td><td>[<span data-ttu-id="ff084-113">Maven</span><span class="sxs-lookup"><span data-stu-id="ff084-113">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="ff084-114">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="ff084-114">**API documentation**</span></span></td><td>[<span data-ttu-id="ff084-115">Java API reference documentation</span><span class="sxs-lookup"><span data-stu-id="ff084-115">Java API reference documentation</span></span>](http://azure.github.io/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="ff084-116">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="ff084-116">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="ff084-117">GitHub</span><span class="sxs-lookup"><span data-stu-id="ff084-117">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="ff084-118">**Get started**</span><span class="sxs-lookup"><span data-stu-id="ff084-118">**Get started**</span></span></td><td>[<span data-ttu-id="ff084-119">Get started with the Java SDK</span><span class="sxs-lookup"><span data-stu-id="ff084-119">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="ff084-120">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="ff084-120">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="ff084-121">Web application development with DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ff084-121">Web application development with DocumentDB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="ff084-122">**Current supported runtime**</span><span class="sxs-lookup"><span data-stu-id="ff084-122">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="ff084-123">JDK 7</span><span class="sxs-lookup"><span data-stu-id="ff084-123">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="ff084-124">Release Notes</span><span class="sxs-lookup"><span data-stu-id="ff084-124">Release Notes</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="ff084-125"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="ff084-125"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="ff084-126">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span><span class="sxs-lookup"><span data-stu-id="ff084-126">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="ff084-127">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span><span class="sxs-lookup"><span data-stu-id="ff084-127">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="ff084-128"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="ff084-128"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="ff084-129">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span><span class="sxs-lookup"><span data-stu-id="ff084-129">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="ff084-130">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span><span class="sxs-lookup"><span data-stu-id="ff084-130">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="ff084-131"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="ff084-131"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="ff084-132">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="ff084-132">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="ff084-133">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="ff084-133">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="ff084-134">Added support for change feed.</span><span class="sxs-lookup"><span data-stu-id="ff084-134">Added support for change feed.</span></span>
* <span data-ttu-id="ff084-135">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="ff084-135">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="ff084-136">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="ff084-136">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="ff084-137">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span><span class="sxs-lookup"><span data-stu-id="ff084-137">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="ff084-138">Fixed a bug in session consistency mode.</span><span class="sxs-lookup"><span data-stu-id="ff084-138">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="ff084-139">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span><span class="sxs-lookup"><span data-stu-id="ff084-139">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="ff084-140">Improved performance of DirectHttps mode.</span><span class="sxs-lookup"><span data-stu-id="ff084-140">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="ff084-141"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="ff084-141"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="ff084-142">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span><span class="sxs-lookup"><span data-stu-id="ff084-142">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="ff084-143">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span><span class="sxs-lookup"><span data-stu-id="ff084-143">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="ff084-144">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span><span class="sxs-lookup"><span data-stu-id="ff084-144">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="ff084-145">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span><span class="sxs-lookup"><span data-stu-id="ff084-145">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="ff084-146">Refactored logging to use SLF4J.</span><span class="sxs-lookup"><span data-stu-id="ff084-146">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="ff084-147">Fixed a few other bugs in consistency reader.</span><span class="sxs-lookup"><span data-stu-id="ff084-147">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="ff084-148"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="ff084-148"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="ff084-149">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span><span class="sxs-lookup"><span data-stu-id="ff084-149">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="ff084-150">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span><span class="sxs-lookup"><span data-stu-id="ff084-150">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="ff084-151">Improved performance by reducing the number of network call for the internal caches.</span><span class="sxs-lookup"><span data-stu-id="ff084-151">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="ff084-152">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="ff084-152">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="ff084-153"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="ff084-153"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="ff084-154">Fixed an issue in the connection management for stability.</span><span class="sxs-lookup"><span data-stu-id="ff084-154">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="ff084-155"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="ff084-155"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="ff084-156">Added support for BoundedStaleness consistency level.</span><span class="sxs-lookup"><span data-stu-id="ff084-156">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="ff084-157">Added support for direct connectivity for CRUD operations for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="ff084-157">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="ff084-158">Fixed a bug in querying a database with SQL.</span><span class="sxs-lookup"><span data-stu-id="ff084-158">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="ff084-159">Fixed a bug in the session cache where session token may be set incorrectly.</span><span class="sxs-lookup"><span data-stu-id="ff084-159">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="ff084-160"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="ff084-160"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="ff084-161">Added support for cross partition parallel queries.</span><span class="sxs-lookup"><span data-stu-id="ff084-161">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="ff084-162">Added support for TOP/ORDER BY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="ff084-162">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="ff084-163">Added support for strong consistency.</span><span class="sxs-lookup"><span data-stu-id="ff084-163">Added support for strong consistency.</span></span>
* <span data-ttu-id="ff084-164">Added support for name based requests when using direct connectivity.</span><span class="sxs-lookup"><span data-stu-id="ff084-164">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="ff084-165">Fixed to make ActivityId stay consistent across all request retries.</span><span class="sxs-lookup"><span data-stu-id="ff084-165">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="ff084-166">Fixed a bug related to the session cache when recreating a collection with the same name.</span><span class="sxs-lookup"><span data-stu-id="ff084-166">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="ff084-167">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span><span class="sxs-lookup"><span data-stu-id="ff084-167">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="ff084-168">Fixed issues with Java Doc for Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="ff084-168">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="ff084-169"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="ff084-169"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="ff084-170">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span><span class="sxs-lookup"><span data-stu-id="ff084-170">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="ff084-171">Fixed a bug to not retry when an incorrect partition key value is provided.</span><span class="sxs-lookup"><span data-stu-id="ff084-171">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="ff084-172"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="ff084-172"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="ff084-173">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="ff084-173">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="ff084-174">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span><span class="sxs-lookup"><span data-stu-id="ff084-174">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="ff084-175">See RetryOptions and ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="ff084-175">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="ff084-176">Deprecated IPartitionResolver based custom partitioning code.</span><span class="sxs-lookup"><span data-stu-id="ff084-176">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="ff084-177">Please use partitioned collections for higher storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="ff084-177">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="ff084-178"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="ff084-178"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="ff084-179">Added retry policy support for throttling.</span><span class="sxs-lookup"><span data-stu-id="ff084-179">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="ff084-180"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="ff084-180"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="ff084-181">Added time to live (TTL) support for documents.</span><span class="sxs-lookup"><span data-stu-id="ff084-181">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="ff084-182"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="ff084-182"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="ff084-183">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ff084-183">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="ff084-184"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="ff084-184"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="ff084-185">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span><span class="sxs-lookup"><span data-stu-id="ff084-185">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="ff084-186"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="ff084-186"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="ff084-187">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="ff084-187">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="ff084-188"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="ff084-188"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="ff084-189">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="ff084-189">Implement Upsert.</span></span> <span data-ttu-id="ff084-190">New upsertXXX methods added to support Upsert feature.</span><span class="sxs-lookup"><span data-stu-id="ff084-190">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="ff084-191">Implement ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="ff084-191">Implement ID Based Routing.</span></span> <span data-ttu-id="ff084-192">No public API changes, all changes internal.</span><span class="sxs-lookup"><span data-stu-id="ff084-192">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="ff084-193"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="ff084-193"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="ff084-194">Release skipped to bring version number in alignment with other SDKs</span><span class="sxs-lookup"><span data-stu-id="ff084-194">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="ff084-195"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="ff084-195"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="ff084-196">Supports GeoSpatial Index</span><span class="sxs-lookup"><span data-stu-id="ff084-196">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="ff084-197">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="ff084-197">Validates id property for all resources.</span></span> <span data-ttu-id="ff084-198">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="ff084-198">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="ff084-199">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="ff084-199">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="ff084-200"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="ff084-200"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="ff084-201">Implements V2 indexing policy</span><span class="sxs-lookup"><span data-stu-id="ff084-201">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="ff084-202"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="ff084-202"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="ff084-203">GA SDK</span><span class="sxs-lookup"><span data-stu-id="ff084-203">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="ff084-204">Release & Retirement Dates</span><span class="sxs-lookup"><span data-stu-id="ff084-204">Release & Retirement Dates</span></span>
<span data-ttu-id="ff084-205">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="ff084-205">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="ff084-206">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="ff084-206">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="ff084-207">Any request to DocumentDB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="ff084-207">Any request to DocumentDB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> All versions of the Azure DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.
> 
> 

<br/>

| <span data-ttu-id="ff084-209">Version</span><span class="sxs-lookup"><span data-stu-id="ff084-209">Version</span></span> | <span data-ttu-id="ff084-210">Release Date</span><span class="sxs-lookup"><span data-stu-id="ff084-210">Release Date</span></span> | <span data-ttu-id="ff084-211">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="ff084-211">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="ff084-212">1.10.0</span><span class="sxs-lookup"><span data-stu-id="ff084-212">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="ff084-213">March 11, 2017</span><span class="sxs-lookup"><span data-stu-id="ff084-213">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="ff084-214">1.9.6</span><span class="sxs-lookup"><span data-stu-id="ff084-214">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="ff084-215">February 21, 2017</span><span class="sxs-lookup"><span data-stu-id="ff084-215">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="ff084-216">1.9.5</span><span class="sxs-lookup"><span data-stu-id="ff084-216">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="ff084-217">January 31, 2017</span><span class="sxs-lookup"><span data-stu-id="ff084-217">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="ff084-218">1.9.4</span><span class="sxs-lookup"><span data-stu-id="ff084-218">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="ff084-219">November 24, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-219">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-220">1.9.3</span><span class="sxs-lookup"><span data-stu-id="ff084-220">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="ff084-221">October 30, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-221">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-222">1.9.2</span><span class="sxs-lookup"><span data-stu-id="ff084-222">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="ff084-223">October 28, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-223">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-224">1.9.1</span><span class="sxs-lookup"><span data-stu-id="ff084-224">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="ff084-225">October 26, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-225">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-226">1.9.0</span><span class="sxs-lookup"><span data-stu-id="ff084-226">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="ff084-227">October 03, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-227">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-228">1.8.1</span><span class="sxs-lookup"><span data-stu-id="ff084-228">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="ff084-229">June 30, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-229">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-230">1.8.0</span><span class="sxs-lookup"><span data-stu-id="ff084-230">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="ff084-231">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-231">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-232">1.7.1</span><span class="sxs-lookup"><span data-stu-id="ff084-232">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="ff084-233">April 30, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-233">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-234">1.7.0</span><span class="sxs-lookup"><span data-stu-id="ff084-234">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="ff084-235">April 27, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-235">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-236">1.6.0</span><span class="sxs-lookup"><span data-stu-id="ff084-236">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="ff084-237">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-237">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="ff084-238">1.5.1</span><span class="sxs-lookup"><span data-stu-id="ff084-238">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="ff084-239">December 31, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-239">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-240">1.5.0</span><span class="sxs-lookup"><span data-stu-id="ff084-240">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="ff084-241">December 04, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-241">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-242">1.4.0</span><span class="sxs-lookup"><span data-stu-id="ff084-242">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="ff084-243">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-243">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-244">1.3.0</span><span class="sxs-lookup"><span data-stu-id="ff084-244">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="ff084-245">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-245">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-246">1.2.0</span><span class="sxs-lookup"><span data-stu-id="ff084-246">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="ff084-247">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-247">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-248">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ff084-248">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="ff084-249">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-249">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-250">1.0.1</span><span class="sxs-lookup"><span data-stu-id="ff084-250">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="ff084-251">May 12, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-251">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="ff084-252">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ff084-252">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="ff084-253">April 07, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-253">April 07, 2015</span></span> |--- |
| <span data-ttu-id="ff084-254">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-254">0.9.5-prelease</span></span> |<span data-ttu-id="ff084-255">Mar 09, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-255">Mar 09, 2015</span></span> |<span data-ttu-id="ff084-256">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-256">February 29, 2016</span></span> |
| <span data-ttu-id="ff084-257">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-257">0.9.4-prelease</span></span> |<span data-ttu-id="ff084-258">February 17, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-258">February 17, 2015</span></span> |<span data-ttu-id="ff084-259">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-259">February 29, 2016</span></span> |
| <span data-ttu-id="ff084-260">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-260">0.9.3-prelease</span></span> |<span data-ttu-id="ff084-261">January 13, 2015</span><span class="sxs-lookup"><span data-stu-id="ff084-261">January 13, 2015</span></span> |<span data-ttu-id="ff084-262">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-262">February 29, 2016</span></span> |
| <span data-ttu-id="ff084-263">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-263">0.9.2-prelease</span></span> |<span data-ttu-id="ff084-264">December 19, 2014</span><span class="sxs-lookup"><span data-stu-id="ff084-264">December 19, 2014</span></span> |<span data-ttu-id="ff084-265">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-265">February 29, 2016</span></span> |
| <span data-ttu-id="ff084-266">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-266">0.9.1-prelease</span></span> |<span data-ttu-id="ff084-267">December 19, 2014</span><span class="sxs-lookup"><span data-stu-id="ff084-267">December 19, 2014</span></span> |<span data-ttu-id="ff084-268">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-268">February 29, 2016</span></span> |
| <span data-ttu-id="ff084-269">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="ff084-269">0.9.0-prelease</span></span> |<span data-ttu-id="ff084-270">December 10, 2014</span><span class="sxs-lookup"><span data-stu-id="ff084-270">December 10, 2014</span></span> |<span data-ttu-id="ff084-271">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="ff084-271">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="ff084-272">FAQ</span><span class="sxs-lookup"><span data-stu-id="ff084-272">FAQ</span></span>
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="ff084-273">See Also</span><span class="sxs-lookup"><span data-stu-id="ff084-273">See Also</span></span>
<span data-ttu-id="ff084-274">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span><span class="sxs-lookup"><span data-stu-id="ff084-274">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span></span>

