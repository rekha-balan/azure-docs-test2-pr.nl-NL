---
title: Azure DocumentDB Node.js API, SDK & Resources | Microsoft Docs
description: Learn all about the Node.js API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB Node.js SDK.
services: documentdb
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/16/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dd6e6184dd755ea356cae1c4d50a2b7ba39da9fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564496"
---
# <a name="documentdb-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="a2087-103">DocumentDB Node.js SDK: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="a2087-103">DocumentDB Node.js SDK: Release notes and resources</span></span>
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

<tr><td><span data-ttu-id="a2087-112">**Download SDK**</span><span class="sxs-lookup"><span data-stu-id="a2087-112">**Download SDK**</span></span></td><td>[<span data-ttu-id="a2087-113">NPM</span><span class="sxs-lookup"><span data-stu-id="a2087-113">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="a2087-114">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="a2087-114">**API documentation**</span></span></td><td>[<span data-ttu-id="a2087-115">Node.js API reference documentation</span><span class="sxs-lookup"><span data-stu-id="a2087-115">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="a2087-116">**SDK installation instructions**</span><span class="sxs-lookup"><span data-stu-id="a2087-116">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="a2087-117">Installation instructions</span><span class="sxs-lookup"><span data-stu-id="a2087-117">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="a2087-118">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="a2087-118">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="a2087-119">GitHub</span><span class="sxs-lookup"><span data-stu-id="a2087-119">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="a2087-120">**Samples**</span><span class="sxs-lookup"><span data-stu-id="a2087-120">**Samples**</span></span></td><td>[<span data-ttu-id="a2087-121">Node.js code samples</span><span class="sxs-lookup"><span data-stu-id="a2087-121">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="a2087-122">**Get started tutorial**</span><span class="sxs-lookup"><span data-stu-id="a2087-122">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="a2087-123">Get started with the Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="a2087-123">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="a2087-124">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="a2087-124">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="a2087-125">Build a Node.js web application using DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a2087-125">Build a Node.js web application using DocumentDB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="a2087-126">**Current supported platform**</span><span class="sxs-lookup"><span data-stu-id="a2087-126">**Current supported platform**</span></span></td><td>[<span data-ttu-id="a2087-127">Node.js v0.10</span><span class="sxs-lookup"><span data-stu-id="a2087-127">Node.js v0.10</span></span>](https://nodejs.org/en/blog/release/v0.10.0/)<br/>[<span data-ttu-id="a2087-128">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="a2087-128">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/>[<span data-ttu-id="a2087-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="a2087-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="a2087-130">Release notes</span><span class="sxs-lookup"><span data-stu-id="a2087-130">Release notes</span></span>

### <span data-ttu-id="a2087-131"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-131"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="a2087-132">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="a2087-132">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="a2087-133">Added the option for controlling degree of parallelism for cross partition queries.</span><span class="sxs-lookup"><span data-stu-id="a2087-133">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="a2087-134">Added the option for disabling SSL verification when running against DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="a2087-134">Added the option for disabling SSL verification when running against DocumentDB Emulator.</span></span>
* <span data-ttu-id="a2087-135">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="a2087-135">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="a2087-136">Fixed the continuation token bug for single partition collection (github #107).</span><span class="sxs-lookup"><span data-stu-id="a2087-136">Fixed the continuation token bug for single partition collection (github #107).</span></span>
* <span data-ttu-id="a2087-137">Fixed the executeStoredProcedure bug in handling 0 as single param (github #155).</span><span class="sxs-lookup"><span data-stu-id="a2087-137">Fixed the executeStoredProcedure bug in handling 0 as single param (github #155).</span></span>

### <span data-ttu-id="a2087-138"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="a2087-138"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="a2087-139">Fixed user-agent header to include the SDK version.</span><span class="sxs-lookup"><span data-stu-id="a2087-139">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="a2087-140">Minor code cleanup.</span><span class="sxs-lookup"><span data-stu-id="a2087-140">Minor code cleanup.</span></span>

### <span data-ttu-id="a2087-141"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="a2087-141"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="a2087-142">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="a2087-142">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="a2087-143">Added support for enabling script logging during stored procedure execution.</span><span class="sxs-lookup"><span data-stu-id="a2087-143">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="a2087-144"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-144"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="a2087-145">Added support for cross partition parallel queries.</span><span class="sxs-lookup"><span data-stu-id="a2087-145">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="a2087-146">Added support for TOP/ORDER BY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="a2087-146">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="a2087-147"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-147"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="a2087-148">Added retry policy support for throttled requests.</span><span class="sxs-lookup"><span data-stu-id="a2087-148">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="a2087-149">(Throttled requests receive a request rate too large exception, error code 429.) By default, DocumentDB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span><span class="sxs-lookup"><span data-stu-id="a2087-149">(Throttled requests receive a request rate too large exception, error code 429.) By default, DocumentDB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="a2087-150">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span><span class="sxs-lookup"><span data-stu-id="a2087-150">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="a2087-151">DocumentDB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span><span class="sxs-lookup"><span data-stu-id="a2087-151">DocumentDB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="a2087-152">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span><span class="sxs-lookup"><span data-stu-id="a2087-152">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="a2087-153">DocumentDB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span><span class="sxs-lookup"><span data-stu-id="a2087-153">DocumentDB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="a2087-154">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span><span class="sxs-lookup"><span data-stu-id="a2087-154">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="a2087-155"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-155"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="a2087-156">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="a2087-156">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="a2087-157"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-157"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="a2087-158">Added the support for Time To Live(TTL) feature for documents.</span><span class="sxs-lookup"><span data-stu-id="a2087-158">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="a2087-159"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-159"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="a2087-160">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="a2087-160">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span></span>

### <span data-ttu-id="a2087-161"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="a2087-161"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="a2087-162">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span><span class="sxs-lookup"><span data-stu-id="a2087-162">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="a2087-163"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="a2087-163"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="a2087-164">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span><span class="sxs-lookup"><span data-stu-id="a2087-164">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="a2087-165"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="a2087-165"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="a2087-166">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for DocumentDB purposes.</span><span class="sxs-lookup"><span data-stu-id="a2087-166">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for DocumentDB purposes.</span></span> <span data-ttu-id="a2087-167">Use a dedicated agent for all of the lib’s requests.</span><span class="sxs-lookup"><span data-stu-id="a2087-167">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="a2087-168"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="a2087-168"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="a2087-169">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span><span class="sxs-lookup"><span data-stu-id="a2087-169">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="a2087-170"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="a2087-170"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="a2087-171">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span><span class="sxs-lookup"><span data-stu-id="a2087-171">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="a2087-172"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="a2087-172"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="a2087-173">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case sensitive systems.</span><span class="sxs-lookup"><span data-stu-id="a2087-173">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case sensitive systems.</span></span>

### <span data-ttu-id="a2087-174"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-174"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="a2087-175">Implement sharding support by adding hash & range partition resolvers.</span><span class="sxs-lookup"><span data-stu-id="a2087-175">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="a2087-176"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-176"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="a2087-177">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="a2087-177">Implement Upsert.</span></span> <span data-ttu-id="a2087-178">New upsertXXX methods on documentClient.</span><span class="sxs-lookup"><span data-stu-id="a2087-178">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="a2087-179"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-179"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="a2087-180">Skipped to bring version numbers in alignment with other SDKs.</span><span class="sxs-lookup"><span data-stu-id="a2087-180">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="a2087-181"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="a2087-181"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="a2087-182">Split Q promises wrapper to new repository.</span><span class="sxs-lookup"><span data-stu-id="a2087-182">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="a2087-183">Update to package file for npm registry.</span><span class="sxs-lookup"><span data-stu-id="a2087-183">Update to package file for npm registry.</span></span>

### <span data-ttu-id="a2087-184"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="a2087-184"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="a2087-185">Implements ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="a2087-185">Implements ID Based Routing.</span></span>
* <span data-ttu-id="a2087-186">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span><span class="sxs-lookup"><span data-stu-id="a2087-186">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="a2087-187"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-187"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="a2087-188">Added support for GeoSpatial index.</span><span class="sxs-lookup"><span data-stu-id="a2087-188">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="a2087-189">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="a2087-189">Validates id property for all resources.</span></span> <span data-ttu-id="a2087-190">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="a2087-190">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="a2087-191">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="a2087-191">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="a2087-192"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-192"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="a2087-193">Implements V2 indexing policy.</span><span class="sxs-lookup"><span data-stu-id="a2087-193">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="a2087-194"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="a2087-194"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="a2087-195">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span><span class="sxs-lookup"><span data-stu-id="a2087-195">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="a2087-196"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="a2087-196"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="a2087-197">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span><span class="sxs-lookup"><span data-stu-id="a2087-197">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="a2087-198"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="a2087-198"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="a2087-199">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="a2087-199">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="a2087-200">Updated API documentation.</span><span class="sxs-lookup"><span data-stu-id="a2087-200">Updated API documentation.</span></span>
* <span data-ttu-id="a2087-201">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span><span class="sxs-lookup"><span data-stu-id="a2087-201">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="a2087-202"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="a2087-202"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="a2087-203">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="a2087-203">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="a2087-204">Release & Retirement Dates</span><span class="sxs-lookup"><span data-stu-id="a2087-204">Release & Retirement Dates</span></span>
<span data-ttu-id="a2087-205">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="a2087-205">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="a2087-206">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="a2087-206">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="a2087-207">Any request to DocumentDB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="a2087-207">Any request to DocumentDB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="a2087-208">Version</span><span class="sxs-lookup"><span data-stu-id="a2087-208">Version</span></span> | <span data-ttu-id="a2087-209">Release Date</span><span class="sxs-lookup"><span data-stu-id="a2087-209">Release Date</span></span> | <span data-ttu-id="a2087-210">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="a2087-210">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a2087-211">1.11.0</span><span class="sxs-lookup"><span data-stu-id="a2087-211">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="a2087-212">March 16, 2017</span><span class="sxs-lookup"><span data-stu-id="a2087-212">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="a2087-213">1.10.2</span><span class="sxs-lookup"><span data-stu-id="a2087-213">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="a2087-214">January 27, 2017</span><span class="sxs-lookup"><span data-stu-id="a2087-214">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="a2087-215">1.10.1</span><span class="sxs-lookup"><span data-stu-id="a2087-215">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="a2087-216">December 22, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-216">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-217">1.10.0</span><span class="sxs-lookup"><span data-stu-id="a2087-217">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="a2087-218">October 03, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-218">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-219">1.9.0</span><span class="sxs-lookup"><span data-stu-id="a2087-219">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="a2087-220">July 07, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-220">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-221">1.8.0</span><span class="sxs-lookup"><span data-stu-id="a2087-221">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="a2087-222">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-222">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-223">1.7.0</span><span class="sxs-lookup"><span data-stu-id="a2087-223">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="a2087-224">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-224">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-225">1.6.0</span><span class="sxs-lookup"><span data-stu-id="a2087-225">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="a2087-226">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-226">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-227">1.5.6</span><span class="sxs-lookup"><span data-stu-id="a2087-227">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="a2087-228">March 08, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-228">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-229">1.5.5</span><span class="sxs-lookup"><span data-stu-id="a2087-229">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="a2087-230">February 02, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-230">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-231">1.5.4</span><span class="sxs-lookup"><span data-stu-id="a2087-231">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="a2087-232">February 01, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-232">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-233">1.5.2</span><span class="sxs-lookup"><span data-stu-id="a2087-233">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="a2087-234">January 26, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-234">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-235">1.5.2</span><span class="sxs-lookup"><span data-stu-id="a2087-235">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="a2087-236">January 22, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-236">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-237">1.5.1</span><span class="sxs-lookup"><span data-stu-id="a2087-237">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="a2087-238">January 4, 2016</span><span class="sxs-lookup"><span data-stu-id="a2087-238">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="a2087-239">1.5.0</span><span class="sxs-lookup"><span data-stu-id="a2087-239">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="a2087-240">December 31, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-240">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-241">1.4.0</span><span class="sxs-lookup"><span data-stu-id="a2087-241">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="a2087-242">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-242">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-243">1.3.0</span><span class="sxs-lookup"><span data-stu-id="a2087-243">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="a2087-244">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-244">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-245">1.2.2</span><span class="sxs-lookup"><span data-stu-id="a2087-245">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="a2087-246">September 10, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-246">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-247">1.2.1</span><span class="sxs-lookup"><span data-stu-id="a2087-247">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="a2087-248">August 15, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-248">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-249">1.2.0</span><span class="sxs-lookup"><span data-stu-id="a2087-249">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="a2087-250">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-250">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-251">1.1.0</span><span class="sxs-lookup"><span data-stu-id="a2087-251">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="a2087-252">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-252">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-253">1.0.3</span><span class="sxs-lookup"><span data-stu-id="a2087-253">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="a2087-254">June 04, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-254">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-255">1.0.2</span><span class="sxs-lookup"><span data-stu-id="a2087-255">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="a2087-256">May 23, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-256">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-257">1.0.1</span><span class="sxs-lookup"><span data-stu-id="a2087-257">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="a2087-258">May 15, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-258">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="a2087-259">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a2087-259">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="a2087-260">April 08, 2015</span><span class="sxs-lookup"><span data-stu-id="a2087-260">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="a2087-261">FAQ</span><span class="sxs-lookup"><span data-stu-id="a2087-261">FAQ</span></span>
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="a2087-262">See also</span><span class="sxs-lookup"><span data-stu-id="a2087-262">See also</span></span>
<span data-ttu-id="a2087-263">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span><span class="sxs-lookup"><span data-stu-id="a2087-263">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span></span>

