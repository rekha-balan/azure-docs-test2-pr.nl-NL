---
title: 'Azure Cosmos DB: SQL Node.js API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL Node.js API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB Node.js SDK.
services: cosmos-db
author: rnagpal
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: nodejs
ms.topic: reference
ms.date: 5/3/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e19c1cb7b297d2537e969e0dd632dae3e1c3d211
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864728"
---
# <a name="azure-cosmos-db-nodejs-sdk-for-sql-api-release-notes-and-resources"></a><span data-ttu-id="7a5ec-103">Azure Cosmos DB Node.js SDK for SQL API: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="7a5ec-103">Azure Cosmos DB Node.js SDK for SQL API: Release notes and resources</span></span>
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

|<span data-ttu-id="7a5ec-116">Resource</span><span class="sxs-lookup"><span data-stu-id="7a5ec-116">Resource</span></span>  |<span data-ttu-id="7a5ec-117">Link</span><span class="sxs-lookup"><span data-stu-id="7a5ec-117">Link</span></span>  |
|---------|---------|
|<span data-ttu-id="7a5ec-118">Download SDK</span><span class="sxs-lookup"><span data-stu-id="7a5ec-118">Download SDK</span></span>  |   [<span data-ttu-id="7a5ec-119">NPM</span><span class="sxs-lookup"><span data-stu-id="7a5ec-119">NPM</span></span>](https://www.npmjs.com/package/@azure/cosmos) 
|<span data-ttu-id="7a5ec-120">API Documentation</span><span class="sxs-lookup"><span data-stu-id="7a5ec-120">API Documentation</span></span>  |  [<span data-ttu-id="7a5ec-121">JavaScript SDK reference documentation</span><span class="sxs-lookup"><span data-stu-id="7a5ec-121">JavaScript SDK reference documentation</span></span>](https://docs.microsoft.com/javascript/api/%40azure/cosmos/?view=azure-node-latest)
|<span data-ttu-id="7a5ec-122">SDK installation instructions</span><span class="sxs-lookup"><span data-stu-id="7a5ec-122">SDK installation instructions</span></span>  |  [<span data-ttu-id="7a5ec-123">Installation instructions</span><span class="sxs-lookup"><span data-stu-id="7a5ec-123">Installation instructions</span></span>](https://github.com/Azure/azure-cosmos-js#installation)
|<span data-ttu-id="7a5ec-124">Contribute to SDK</span><span class="sxs-lookup"><span data-stu-id="7a5ec-124">Contribute to SDK</span></span> | [<span data-ttu-id="7a5ec-125">GitHub</span><span class="sxs-lookup"><span data-stu-id="7a5ec-125">GitHub</span></span>](https://github.com/Azure/azure-cosmos-js/tree/master)
| <span data-ttu-id="7a5ec-126">Samples</span><span class="sxs-lookup"><span data-stu-id="7a5ec-126">Samples</span></span> | [<span data-ttu-id="7a5ec-127">Node.js code samples</span><span class="sxs-lookup"><span data-stu-id="7a5ec-127">Node.js code samples</span></span>](sql-api-nodejs-samples-preview.md)
| <span data-ttu-id="7a5ec-128">Getting started tutorial</span><span class="sxs-lookup"><span data-stu-id="7a5ec-128">Getting started tutorial</span></span> | [<span data-ttu-id="7a5ec-129">Get started with the JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="7a5ec-129">Get started with the JavaScript SDK</span></span>](sql-api-nodejs-get-started-preview.md)
| <span data-ttu-id="7a5ec-130">Web app tutorial</span><span class="sxs-lookup"><span data-stu-id="7a5ec-130">Web app tutorial</span></span> | [<span data-ttu-id="7a5ec-131">Build a Node.js web application using Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a5ec-131">Build a Node.js web application using Azure Cosmos DB</span></span>](sql-api-nodejs-application-preview.md)
| <span data-ttu-id="7a5ec-132">Current supported platform</span><span class="sxs-lookup"><span data-stu-id="7a5ec-132">Current supported platform</span></span> | <span data-ttu-id="7a5ec-133">[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/) - required for SDK Version 2.0.0 and above.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-133">[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/) - required for SDK Version 2.0.0 and above.</span></span><br/>[<span data-ttu-id="7a5ec-134">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-134">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> [<span data-ttu-id="7a5ec-135">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="7a5ec-135">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> [<span data-ttu-id="7a5ec-136">Node.js v0.10</span><span class="sxs-lookup"><span data-stu-id="7a5ec-136">Node.js v0.10</span></span>](https://nodejs.org/en/blog/release/v0.10.0/) 

## <a name="release-notes"></a><span data-ttu-id="7a5ec-137">Release notes</span><span class="sxs-lookup"><span data-stu-id="7a5ec-137">Release notes</span></span>

### <span data-ttu-id="7a5ec-138"><a name="2.0.0-3"/>2.0.0-3</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-138"><a name="2.0.0-3"/>2.0.0-3</a></span></span>
* <span data-ttu-id="7a5ec-139">RC1 of Version 2.0.0 of the JavaScript SDK for public preview.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-139">RC1 of Version 2.0.0 of the JavaScript SDK for public preview.</span></span>
* <span data-ttu-id="7a5ec-140">New object model, with top-level CosmosClient and methods split across relevant Database, Container, and Item classes.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-140">New object model, with top-level CosmosClient and methods split across relevant Database, Container, and Item classes.</span></span> 
* <span data-ttu-id="7a5ec-141">Support for [promises](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-141">Support for [promises](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> 
* <span data-ttu-id="7a5ec-142">SDK converted to TypeScript.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-142">SDK converted to TypeScript.</span></span>

### <span data-ttu-id="7a5ec-143"><a name="1.14.4"/>1.14.4</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-143"><a name="1.14.4"/>1.14.4</a></span></span>
* <span data-ttu-id="7a5ec-144">npm documentation fixed.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-144">npm documentation fixed.</span></span>

### <span data-ttu-id="7a5ec-145"><a name="1.14.3"/>1.14.3</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-145"><a name="1.14.3"/>1.14.3</a></span></span>
* <span data-ttu-id="7a5ec-146">Added support for default retries on connection issues.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-146">Added support for default retries on connection issues.</span></span>
* <span data-ttu-id="7a5ec-147">Added support to read collection change feed.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-147">Added support to read collection change feed.</span></span>
* <span data-ttu-id="7a5ec-148">Fixed session consistency bug that intermittently caused "read session not available".</span><span class="sxs-lookup"><span data-stu-id="7a5ec-148">Fixed session consistency bug that intermittently caused "read session not available".</span></span>
* <span data-ttu-id="7a5ec-149">Added support for query metrics.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-149">Added support for query metrics.</span></span>
* <span data-ttu-id="7a5ec-150">Modified http Agent's maximum number of connections.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-150">Modified http Agent's maximum number of connections.</span></span>

### <span data-ttu-id="7a5ec-151"><a name="1.14.2"/>1.14.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-151"><a name="1.14.2"/>1.14.2</a></span></span>
* <span data-ttu-id="7a5ec-152">Updated documentation to reference Azure Cosmos DB instead of Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-152">Updated documentation to reference Azure Cosmos DB instead of Azure DocumentDB.</span></span>
* <span data-ttu-id="7a5ec-153">Added Support for proxyUrl setting in ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-153">Added Support for proxyUrl setting in ConnectionPolicy.</span></span>

### <span data-ttu-id="7a5ec-154"><a name="1.14.1"/>1.14.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-154"><a name="1.14.1"/>1.14.1</a></span></span>
* <span data-ttu-id="7a5ec-155">Minor fix for case sensitive file systems.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-155">Minor fix for case sensitive file systems.</span></span>

### <span data-ttu-id="7a5ec-156"><a name="1.14.0"/>1.14.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-156"><a name="1.14.0"/>1.14.0</a></span></span>
* <span data-ttu-id="7a5ec-157">Adds support for Session Consistency.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-157">Adds support for Session Consistency.</span></span>
* <span data-ttu-id="7a5ec-158">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-158">This SDK version requires the latest version of Azure Cosmos DB Emulator available for download from https://aka.ms/cosmosdb-emulator.</span></span>

### <span data-ttu-id="7a5ec-159"><a name="1.13.0"/>1.13.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-159"><a name="1.13.0"/>1.13.0</a></span></span>
* <span data-ttu-id="7a5ec-160">Split proofed cross partition queries.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-160">Split proofed cross partition queries.</span></span>
* <span data-ttu-id="7a5ec-161">Adds supports for resource link with leading and trailing slashes (and corresponding tests).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-161">Adds supports for resource link with leading and trailing slashes (and corresponding tests).</span></span>

### <span data-ttu-id="7a5ec-162"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-162"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="7a5ec-163">npm documentation fixed.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-163">npm documentation fixed.</span></span>

### <span data-ttu-id="7a5ec-164"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-164"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="7a5ec-165">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-165">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="7a5ec-166">Fixed a bug in handling documents with Unicode characters in the partition key.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-166">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="7a5ec-167">Fixed support for creating collections with the name media.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-167">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="7a5ec-168">Github issue #114.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-168">Github issue #114.</span></span>
* <span data-ttu-id="7a5ec-169">Fixed support for permission authorization token.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-169">Fixed support for permission authorization token.</span></span> <span data-ttu-id="7a5ec-170">Github issue #178.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-170">Github issue #178.</span></span>

### <span data-ttu-id="7a5ec-171"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-171"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="7a5ec-172">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-172">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="7a5ec-173">Added support for UriFactory.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-173">Added support for UriFactory.</span></span>
* <span data-ttu-id="7a5ec-174">Fixed a Unicode support bug.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-174">Fixed a Unicode support bug.</span></span> <span data-ttu-id="7a5ec-175">GitHub issue #171.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-175">GitHub issue #171.</span></span>

### <span data-ttu-id="7a5ec-176"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-176"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="7a5ec-177">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-177">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="7a5ec-178">Added the option for controlling degree of parallelism for cross partition queries.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-178">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="7a5ec-179">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-179">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="7a5ec-180">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-180">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="7a5ec-181">Fixed the continuation token bug for single partition collection.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-181">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="7a5ec-182">Github issue #107.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-182">Github issue #107.</span></span>
* <span data-ttu-id="7a5ec-183">Fixed the executeStoredProcedure bug in handling 0 as single param.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-183">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="7a5ec-184">Github issue #155.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-184">Github issue #155.</span></span>

### <span data-ttu-id="7a5ec-185"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-185"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="7a5ec-186">Fixed user-agent header to include the SDK version.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-186">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="7a5ec-187">Minor code cleanup.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-187">Minor code cleanup.</span></span>

### <span data-ttu-id="7a5ec-188"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-188"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="7a5ec-189">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-189">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="7a5ec-190">Added support for enabling script logging during stored procedure execution.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-190">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="7a5ec-191"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-191"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="7a5ec-192">Added support for cross partition parallel queries.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-192">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="7a5ec-193">Added support for TOP/ORDER BY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-193">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="7a5ec-194"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-194"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="7a5ec-195">Added retry policy support for throttled requests.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-195">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="7a5ec-196">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-196">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="7a5ec-197">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-197">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="7a5ec-198">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-198">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="7a5ec-199">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-199">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="7a5ec-200">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-200">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="7a5ec-201">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-201">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="7a5ec-202"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-202"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="7a5ec-203">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-203">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="7a5ec-204"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-204"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="7a5ec-205">Added the support for Time To Live(TTL) feature for documents.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-205">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="7a5ec-206"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-206"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="7a5ec-207">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="7a5ec-207">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="7a5ec-208"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-208"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="7a5ec-209">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-209">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="7a5ec-210"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-210"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="7a5ec-211">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-211">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="7a5ec-212"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-212"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="7a5ec-213">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-213">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="7a5ec-214">Use a dedicated agent for all of the lib’s requests.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-214">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="7a5ec-215"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-215"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="7a5ec-216">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-216">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="7a5ec-217"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-217"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="7a5ec-218">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-218">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="7a5ec-219"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-219"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="7a5ec-220">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-220">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="7a5ec-221"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-221"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="7a5ec-222">Implement sharding support by adding hash & range partition resolvers.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-222">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="7a5ec-223"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-223"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="7a5ec-224">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-224">Implement Upsert.</span></span> <span data-ttu-id="7a5ec-225">New upsertXXX methods on documentClient.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-225">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="7a5ec-226"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-226"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="7a5ec-227">Skipped to bring version numbers in alignment with other SDKs.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-227">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="7a5ec-228"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-228"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="7a5ec-229">Split Q promises wrapper to new repository.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-229">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="7a5ec-230">Update to package file for npm registry.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-230">Update to package file for npm registry.</span></span>

### <span data-ttu-id="7a5ec-231"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-231"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="7a5ec-232">Implements ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-232">Implements ID Based Routing.</span></span>
* <span data-ttu-id="7a5ec-233">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span><span class="sxs-lookup"><span data-stu-id="7a5ec-233">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="7a5ec-234"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-234"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="7a5ec-235">Added support for GeoSpatial index.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-235">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="7a5ec-236">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-236">Validates id property for all resources.</span></span> <span data-ttu-id="7a5ec-237">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-237">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="7a5ec-238">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-238">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="7a5ec-239"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-239"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="7a5ec-240">Implements V2 indexing policy.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-240">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="7a5ec-241"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-241"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="7a5ec-242">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-242">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="7a5ec-243"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-243"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="7a5ec-244">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-244">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="7a5ec-245"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-245"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="7a5ec-246">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-246">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="7a5ec-247">Updated API documentation.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-247">Updated API documentation.</span></span>
* <span data-ttu-id="7a5ec-248">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-248">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="7a5ec-249"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="7a5ec-249"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="7a5ec-250">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-250">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="7a5ec-251">Release & Retirement Dates</span><span class="sxs-lookup"><span data-stu-id="7a5ec-251">Release & Retirement Dates</span></span>
<span data-ttu-id="7a5ec-252">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-252">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="7a5ec-253">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-253">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="7a5ec-254">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-254">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="7a5ec-255">Version</span><span class="sxs-lookup"><span data-stu-id="7a5ec-255">Version</span></span> | <span data-ttu-id="7a5ec-256">Release Date</span><span class="sxs-lookup"><span data-stu-id="7a5ec-256">Release Date</span></span> | <span data-ttu-id="7a5ec-257">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="7a5ec-257">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="7a5ec-258">2.0.0-3 (RC)</span><span class="sxs-lookup"><span data-stu-id="7a5ec-258">2.0.0-3 (RC)</span></span>](#2.0.0-3) |<span data-ttu-id="7a5ec-259">August 2, 2018</span><span class="sxs-lookup"><span data-stu-id="7a5ec-259">August 2, 2018</span></span> |--- |
| [<span data-ttu-id="7a5ec-260">1.14.4</span><span class="sxs-lookup"><span data-stu-id="7a5ec-260">1.14.4</span></span>](#1.14.4) |<span data-ttu-id="7a5ec-261">May 03, 2018</span><span class="sxs-lookup"><span data-stu-id="7a5ec-261">May 03, 2018</span></span> |--- |
| [<span data-ttu-id="7a5ec-262">1.14.3</span><span class="sxs-lookup"><span data-stu-id="7a5ec-262">1.14.3</span></span>](#1.14.3) |<span data-ttu-id="7a5ec-263">May 03, 2018</span><span class="sxs-lookup"><span data-stu-id="7a5ec-263">May 03, 2018</span></span> |--- |
| [<span data-ttu-id="7a5ec-264">1.14.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-264">1.14.2</span></span>](#1.14.2) |<span data-ttu-id="7a5ec-265">December 21, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-265">December 21, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-266">1.14.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-266">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="7a5ec-267">November 10, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-267">November 10, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-268">1.14.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-268">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="7a5ec-269">November 9, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-269">November 9, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-270">1.13.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-270">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="7a5ec-271">October 11, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-271">October 11, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-272">1.12.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-272">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="7a5ec-273">August 10, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-273">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-274">1.12.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-274">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="7a5ec-275">August 10, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-275">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-276">1.12.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-276">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="7a5ec-277">May 10, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-277">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-278">1.11.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-278">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="7a5ec-279">March 16, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-279">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-280">1.10.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-280">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="7a5ec-281">January 27, 2017</span><span class="sxs-lookup"><span data-stu-id="7a5ec-281">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="7a5ec-282">1.10.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-282">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="7a5ec-283">December 22, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-283">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-284">1.10.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-284">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="7a5ec-285">October 03, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-285">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-286">1.9.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-286">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="7a5ec-287">July 07, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-287">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-288">1.8.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-288">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="7a5ec-289">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-289">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-290">1.7.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-290">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="7a5ec-291">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-291">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-292">1.6.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-292">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="7a5ec-293">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-293">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-294">1.5.6</span><span class="sxs-lookup"><span data-stu-id="7a5ec-294">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="7a5ec-295">March 08, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-295">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-296">1.5.5</span><span class="sxs-lookup"><span data-stu-id="7a5ec-296">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="7a5ec-297">February 02, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-297">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-298">1.5.4</span><span class="sxs-lookup"><span data-stu-id="7a5ec-298">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="7a5ec-299">February 01, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-299">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-300">1.5.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-300">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="7a5ec-301">January 26, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-301">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-302">1.5.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-302">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="7a5ec-303">January 22, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-303">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-304">1.5.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-304">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="7a5ec-305">January 4, 2016</span><span class="sxs-lookup"><span data-stu-id="7a5ec-305">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="7a5ec-306">1.5.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-306">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="7a5ec-307">December 31, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-307">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-308">1.4.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-308">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="7a5ec-309">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-309">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-310">1.3.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-310">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="7a5ec-311">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-311">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-312">1.2.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-312">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="7a5ec-313">September 10, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-313">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-314">1.2.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-314">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="7a5ec-315">August 15, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-315">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-316">1.2.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-316">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="7a5ec-317">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-317">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-318">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-318">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="7a5ec-319">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-319">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-320">1.0.3</span><span class="sxs-lookup"><span data-stu-id="7a5ec-320">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="7a5ec-321">June 04, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-321">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-322">1.0.2</span><span class="sxs-lookup"><span data-stu-id="7a5ec-322">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="7a5ec-323">May 23, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-323">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-324">1.0.1</span><span class="sxs-lookup"><span data-stu-id="7a5ec-324">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="7a5ec-325">May 15, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-325">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="7a5ec-326">1.0.0</span><span class="sxs-lookup"><span data-stu-id="7a5ec-326">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="7a5ec-327">April 08, 2015</span><span class="sxs-lookup"><span data-stu-id="7a5ec-327">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="7a5ec-328">FAQ</span><span class="sxs-lookup"><span data-stu-id="7a5ec-328">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="7a5ec-329">See also</span><span class="sxs-lookup"><span data-stu-id="7a5ec-329">See also</span></span>
<span data-ttu-id="7a5ec-330">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="7a5ec-330">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

