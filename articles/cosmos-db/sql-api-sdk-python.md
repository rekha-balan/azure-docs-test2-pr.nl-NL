---
title: 'Azure Cosmos DB: SQL Python API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL Python API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB Python SDK.
services: cosmos-db
author: rnagpal
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: python
ms.topic: reference
ms.date: 5/8/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a79c1951fb8cfbfc208942835ee87b91b763c44
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855698"
---
# <a name="azure-cosmos-db-python-sdk-for-sql-api-release-notes-and-resources"></a><span data-ttu-id="1283f-103">Azure Cosmos DB Python SDK for SQL API: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="1283f-103">Azure Cosmos DB Python SDK for SQL API: Release notes and resources</span></span>
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

<tr><td><span data-ttu-id="1283f-116">**Download SDK**</span><span class="sxs-lookup"><span data-stu-id="1283f-116">**Download SDK**</span></span></td><td>[<span data-ttu-id="1283f-117">PyPI</span><span class="sxs-lookup"><span data-stu-id="1283f-117">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="1283f-118">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="1283f-118">**API documentation**</span></span></td><td>[<span data-ttu-id="1283f-119">Python API reference documentation</span><span class="sxs-lookup"><span data-stu-id="1283f-119">Python API reference documentation</span></span>](https://docs.microsoft.com/python/api/pydocumentdb?view=azure-python)</td></tr>

<tr><td><span data-ttu-id="1283f-120">**SDK installation instructions**</span><span class="sxs-lookup"><span data-stu-id="1283f-120">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="1283f-121">Python SDK installation instructions</span><span class="sxs-lookup"><span data-stu-id="1283f-121">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="1283f-122">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="1283f-122">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="1283f-123">GitHub</span><span class="sxs-lookup"><span data-stu-id="1283f-123">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="1283f-124">**Get started**</span><span class="sxs-lookup"><span data-stu-id="1283f-124">**Get started**</span></span></td><td>[<span data-ttu-id="1283f-125">Get started with the Python SDK</span><span class="sxs-lookup"><span data-stu-id="1283f-125">Get started with the Python SDK</span></span>](sql-api-python-application.md)</td></tr>

<tr><td><span data-ttu-id="1283f-126">**Current supported platform**</span><span class="sxs-lookup"><span data-stu-id="1283f-126">**Current supported platform**</span></span></td><td><span data-ttu-id="1283f-127">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1283f-127">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="1283f-128">Release notes</span><span class="sxs-lookup"><span data-stu-id="1283f-128">Release notes</span></span>
### <a name="a-name232232"></a><span data-ttu-id="1283f-129"><a name="2.3.2"/>2.3.2</span><span class="sxs-lookup"><span data-stu-id="1283f-129"><a name="2.3.2"/>2.3.2</span></span>
* <span data-ttu-id="1283f-130">Added support for default retries on connection issues.</span><span class="sxs-lookup"><span data-stu-id="1283f-130">Added support for default retries on connection issues.</span></span>

### <a name="a-name231231"></a><span data-ttu-id="1283f-131"><a name="2.3.1"/>2.3.1</span><span class="sxs-lookup"><span data-stu-id="1283f-131"><a name="2.3.1"/>2.3.1</span></span>
* <span data-ttu-id="1283f-132">Updated documentation to reference Azure Cosmos DB instead of Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="1283f-132">Updated documentation to reference Azure Cosmos DB instead of Azure DocumentDB.</span></span>

### <a name="a-name230230"></a><span data-ttu-id="1283f-133"><a name="2.3.0"/>2.3.0</span><span class="sxs-lookup"><span data-stu-id="1283f-133"><a name="2.3.0"/>2.3.0</span></span>
* <span data-ttu-id="1283f-134">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span><span class="sxs-lookup"><span data-stu-id="1283f-134">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span></span>

### <a name="a-name221221"></a><span data-ttu-id="1283f-135"><a name="2.2.1"/>2.2.1</span><span class="sxs-lookup"><span data-stu-id="1283f-135"><a name="2.2.1"/>2.2.1</span></span>
* <span data-ttu-id="1283f-136">Bug fix for aggregate dictionary.</span><span class="sxs-lookup"><span data-stu-id="1283f-136">Bug fix for aggregate dictionary.</span></span>
* <span data-ttu-id="1283f-137">Bug fix for trimming slashes in the resource link.</span><span class="sxs-lookup"><span data-stu-id="1283f-137">Bug fix for trimming slashes in the resource link.</span></span>
* <span data-ttu-id="1283f-138">Added tests for Unicode encoding.</span><span class="sxs-lookup"><span data-stu-id="1283f-138">Added tests for Unicode encoding.</span></span>

### <a name="a-name220220"></a><span data-ttu-id="1283f-139"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="1283f-139"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="1283f-140">Added support for a new consistency level called ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="1283f-140">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="1283f-141"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="1283f-141"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="1283f-142">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="1283f-142">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="1283f-143">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="1283f-143">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="1283f-144">Removed the restriction of dependent requests module to be exactly 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="1283f-144">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="1283f-145">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1283f-145">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="1283f-146">Added support for enabling script logging during stored procedure execution.</span><span class="sxs-lookup"><span data-stu-id="1283f-146">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="1283f-147">REST API version bumped to '2017-01-19' with this release.</span><span class="sxs-lookup"><span data-stu-id="1283f-147">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="1283f-148"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="1283f-148"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="1283f-149">Made editorial changes to documentation comments.</span><span class="sxs-lookup"><span data-stu-id="1283f-149">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="1283f-150"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="1283f-150"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="1283f-151">Added support for Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="1283f-151">Added support for Python 3.5.</span></span>
* <span data-ttu-id="1283f-152">Added support for connection pooling using a requests module.</span><span class="sxs-lookup"><span data-stu-id="1283f-152">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="1283f-153">Added support for session consistency.</span><span class="sxs-lookup"><span data-stu-id="1283f-153">Added support for session consistency.</span></span>
* <span data-ttu-id="1283f-154">Added support for TOP/ORDERBY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="1283f-154">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="1283f-155"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="1283f-155"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="1283f-156">Added retry policy support for throttled requests.</span><span class="sxs-lookup"><span data-stu-id="1283f-156">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="1283f-157">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span><span class="sxs-lookup"><span data-stu-id="1283f-157">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="1283f-158">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span><span class="sxs-lookup"><span data-stu-id="1283f-158">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="1283f-159">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span><span class="sxs-lookup"><span data-stu-id="1283f-159">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="1283f-160">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span><span class="sxs-lookup"><span data-stu-id="1283f-160">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="1283f-161">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span><span class="sxs-lookup"><span data-stu-id="1283f-161">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="1283f-162">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span><span class="sxs-lookup"><span data-stu-id="1283f-162">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="1283f-163"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="1283f-163"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="1283f-164">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="1283f-164">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="1283f-165"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="1283f-165"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="1283f-166">Added the support for Time To Live(TTL) feature for documents.</span><span class="sxs-lookup"><span data-stu-id="1283f-166">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="1283f-167"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="1283f-167"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="1283f-168">Bug fixes related to server-side partitioning to allow special characters in partition key path.</span><span class="sxs-lookup"><span data-stu-id="1283f-168">Bug fixes related to server-side partitioning to allow special characters in partition key path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="1283f-169"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="1283f-169"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="1283f-170">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="1283f-170">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="1283f-171"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="1283f-171"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="1283f-172">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="1283f-172">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="1283f-173"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="1283f-173"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="1283f-174">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="1283f-174">Implement Upsert.</span></span> <span data-ttu-id="1283f-175">New UpsertXXX methods added to support Upsert feature.</span><span class="sxs-lookup"><span data-stu-id="1283f-175">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="1283f-176">Implement ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="1283f-176">Implement ID Based Routing.</span></span> <span data-ttu-id="1283f-177">No public API changes, all changes internal.</span><span class="sxs-lookup"><span data-stu-id="1283f-177">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="1283f-178"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="1283f-178"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="1283f-179">Supports GeoSpatial index.</span><span class="sxs-lookup"><span data-stu-id="1283f-179">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="1283f-180">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="1283f-180">Validates id property for all resources.</span></span> <span data-ttu-id="1283f-181">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="1283f-181">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="1283f-182">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="1283f-182">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="1283f-183"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="1283f-183"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="1283f-184">Implements V2 indexing policy.</span><span class="sxs-lookup"><span data-stu-id="1283f-184">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="1283f-185"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="1283f-185"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="1283f-186">Supports proxy connection.</span><span class="sxs-lookup"><span data-stu-id="1283f-186">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="1283f-187"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="1283f-187"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="1283f-188">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="1283f-188">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="1283f-189">Release & retirement dates</span><span class="sxs-lookup"><span data-stu-id="1283f-189">Release & retirement dates</span></span>
<span data-ttu-id="1283f-190">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="1283f-190">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="1283f-191">New features and functionality and optimizations are only added to the current SDK, as such it is recommend that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="1283f-191">New features and functionality and optimizations are only added to the current SDK, as such it is recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="1283f-192">Any request to Cosmos DB using a retired SDK are rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="1283f-192">Any request to Cosmos DB using a retired SDK are rejected by the service.</span></span>

> [!WARNING]
> All versions of the Azure SQL SDK for Python prior to version **1.0.0** were retired on **February 29, 2016**. 
> 
> 

<br/>

| <span data-ttu-id="1283f-194">Version</span><span class="sxs-lookup"><span data-stu-id="1283f-194">Version</span></span> | <span data-ttu-id="1283f-195">Release Date</span><span class="sxs-lookup"><span data-stu-id="1283f-195">Release Date</span></span> | <span data-ttu-id="1283f-196">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="1283f-196">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="1283f-197">2.3.2</span><span class="sxs-lookup"><span data-stu-id="1283f-197">2.3.2</span></span>](#2.3.2) |<span data-ttu-id="1283f-198">May 08, 2018</span><span class="sxs-lookup"><span data-stu-id="1283f-198">May 08, 2018</span></span> |--- |
| [<span data-ttu-id="1283f-199">2.3.1</span><span class="sxs-lookup"><span data-stu-id="1283f-199">2.3.1</span></span>](#2.3.1) |<span data-ttu-id="1283f-200">December 21, 2017</span><span class="sxs-lookup"><span data-stu-id="1283f-200">December 21, 2017</span></span> |--- |
| [<span data-ttu-id="1283f-201">2.3.0</span><span class="sxs-lookup"><span data-stu-id="1283f-201">2.3.0</span></span>](#2.3.0) |<span data-ttu-id="1283f-202">November 10, 2017</span><span class="sxs-lookup"><span data-stu-id="1283f-202">November 10, 2017</span></span> |--- |
| [<span data-ttu-id="1283f-203">2.2.1</span><span class="sxs-lookup"><span data-stu-id="1283f-203">2.2.1</span></span>](#2.2.1) |<span data-ttu-id="1283f-204">Sep 29, 2017</span><span class="sxs-lookup"><span data-stu-id="1283f-204">Sep 29, 2017</span></span> |--- |
| [<span data-ttu-id="1283f-205">2.2.0</span><span class="sxs-lookup"><span data-stu-id="1283f-205">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="1283f-206">May 10, 2017</span><span class="sxs-lookup"><span data-stu-id="1283f-206">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="1283f-207">2.1.0</span><span class="sxs-lookup"><span data-stu-id="1283f-207">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="1283f-208">May 01, 2017</span><span class="sxs-lookup"><span data-stu-id="1283f-208">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="1283f-209">2.0.1</span><span class="sxs-lookup"><span data-stu-id="1283f-209">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="1283f-210">October 30, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-210">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-211">2.0.0</span><span class="sxs-lookup"><span data-stu-id="1283f-211">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="1283f-212">September 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-212">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-213">1.9.0</span><span class="sxs-lookup"><span data-stu-id="1283f-213">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="1283f-214">July 07, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-214">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-215">1.8.0</span><span class="sxs-lookup"><span data-stu-id="1283f-215">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="1283f-216">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-216">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-217">1.7.0</span><span class="sxs-lookup"><span data-stu-id="1283f-217">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="1283f-218">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-218">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-219">1.6.1</span><span class="sxs-lookup"><span data-stu-id="1283f-219">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="1283f-220">April 08, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-220">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-221">1.6.0</span><span class="sxs-lookup"><span data-stu-id="1283f-221">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="1283f-222">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-222">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-223">1.5.0</span><span class="sxs-lookup"><span data-stu-id="1283f-223">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="1283f-224">January 03, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-224">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="1283f-225">1.4.2</span><span class="sxs-lookup"><span data-stu-id="1283f-225">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="1283f-226">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-226">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="1283f-227">1.4.1</span><span class="sxs-lookup"><span data-stu-id="1283f-227">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="1283f-228">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-228">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="1283f-229">1.2.0</span><span class="sxs-lookup"><span data-stu-id="1283f-229">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="1283f-230">August 06, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-230">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="1283f-231">1.1.0</span><span class="sxs-lookup"><span data-stu-id="1283f-231">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="1283f-232">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-232">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="1283f-233">1.0.1</span><span class="sxs-lookup"><span data-stu-id="1283f-233">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="1283f-234">May 25, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-234">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="1283f-235">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1283f-235">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="1283f-236">April 07, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-236">April 07, 2015</span></span> |--- |
| <span data-ttu-id="1283f-237">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="1283f-237">0.9.4-prelease</span></span> |<span data-ttu-id="1283f-238">January 14, 2015</span><span class="sxs-lookup"><span data-stu-id="1283f-238">January 14, 2015</span></span> |<span data-ttu-id="1283f-239">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-239">February 29, 2016</span></span> |
| <span data-ttu-id="1283f-240">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="1283f-240">0.9.3-prelease</span></span> |<span data-ttu-id="1283f-241">December 09, 2014</span><span class="sxs-lookup"><span data-stu-id="1283f-241">December 09, 2014</span></span> |<span data-ttu-id="1283f-242">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-242">February 29, 2016</span></span> |
| <span data-ttu-id="1283f-243">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="1283f-243">0.9.2-prelease</span></span> |<span data-ttu-id="1283f-244">November 25, 2014</span><span class="sxs-lookup"><span data-stu-id="1283f-244">November 25, 2014</span></span> |<span data-ttu-id="1283f-245">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-245">February 29, 2016</span></span> |
| <span data-ttu-id="1283f-246">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="1283f-246">0.9.1-prelease</span></span> |<span data-ttu-id="1283f-247">September 23, 2014</span><span class="sxs-lookup"><span data-stu-id="1283f-247">September 23, 2014</span></span> |<span data-ttu-id="1283f-248">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-248">February 29, 2016</span></span> |
| <span data-ttu-id="1283f-249">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="1283f-249">0.9.0-prelease</span></span> |<span data-ttu-id="1283f-250">August 21, 2014</span><span class="sxs-lookup"><span data-stu-id="1283f-250">August 21, 2014</span></span> |<span data-ttu-id="1283f-251">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="1283f-251">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="1283f-252">FAQ</span><span class="sxs-lookup"><span data-stu-id="1283f-252">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="1283f-253">See also</span><span class="sxs-lookup"><span data-stu-id="1283f-253">See also</span></span>
<span data-ttu-id="1283f-254">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="1283f-254">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

