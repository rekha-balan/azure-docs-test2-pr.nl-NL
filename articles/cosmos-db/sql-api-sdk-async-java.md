---
title: 'Azure Cosmos DB: SQL Async Java API, SDK & resources | Microsoft Docs'
description: Learn all about the SQL Async Java API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB SQL Async Java SDK.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 09/05/2018
ms.author: sngun
ms.openlocfilehash: e90c5640e571aaf28e184e9439f6228e3a5bbc6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865276"
---
# <a name="azure-cosmos-db-async-java-sdk-for-sql-api-release-notes-and-resources"></a><span data-ttu-id="b2f29-103">Azure Cosmos DB Async Java SDK for SQL API: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="b2f29-103">Azure Cosmos DB Async Java SDK for SQL API: Release notes and resources</span></span>
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

<span data-ttu-id="b2f29-116">The SQL API Async Java SDK differs from the SQL API Java SDK by providing asynchronous operations with support of the [Netty library](http://netty.io/).</span><span class="sxs-lookup"><span data-stu-id="b2f29-116">The SQL API Async Java SDK differs from the SQL API Java SDK by providing asynchronous operations with support of the [Netty library](http://netty.io/).</span></span> <span data-ttu-id="b2f29-117">The pre-existing [SQL API Java SDK](sql-api-sdk-java.md) does not support asynchronous operations.</span><span class="sxs-lookup"><span data-stu-id="b2f29-117">The pre-existing [SQL API Java SDK](sql-api-sdk-java.md) does not support asynchronous operations.</span></span> 

<table>

<tr><td><span data-ttu-id="b2f29-118">**SDK Download**</span><span class="sxs-lookup"><span data-stu-id="b2f29-118">**SDK Download**</span></span></td><td>[<span data-ttu-id="b2f29-119">Maven</span><span class="sxs-lookup"><span data-stu-id="b2f29-119">Maven</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb)</td></tr>

<tr><td><span data-ttu-id="b2f29-120">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="b2f29-120">**API documentation**</span></span></td><td>[<span data-ttu-id="b2f29-121">Java API reference documentation</span><span class="sxs-lookup"><span data-stu-id="b2f29-121">Java API reference documentation</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.cosmosdb.rx._async_document_client?view=azure-java-stable)</td></tr>

<tr><td><span data-ttu-id="b2f29-122">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="b2f29-122">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="b2f29-123">GitHub</span><span class="sxs-lookup"><span data-stu-id="b2f29-123">GitHub</span></span>](https://github.com/Azure/azure-cosmosdb-java)</td></tr>

<tr><td><span data-ttu-id="b2f29-124">**Get started**</span><span class="sxs-lookup"><span data-stu-id="b2f29-124">**Get started**</span></span></td><td>[<span data-ttu-id="b2f29-125">Get started with the Async Java SDK</span><span class="sxs-lookup"><span data-stu-id="b2f29-125">Get started with the Async Java SDK</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started)</td></tr>

<tr><td><span data-ttu-id="b2f29-126">**Code sample**</span><span class="sxs-lookup"><span data-stu-id="b2f29-126">**Code sample**</span></span></td><td>[<span data-ttu-id="b2f29-127">Github</span><span class="sxs-lookup"><span data-stu-id="b2f29-127">Github</span></span>](https://github.com/Azure/azure-cosmosdb-java#usage-code-sample)</td></tr>

<tr><td><span data-ttu-id="b2f29-128">**Performance tips**</span><span class="sxs-lookup"><span data-stu-id="b2f29-128">**Performance tips**</span></span></td><td>[<span data-ttu-id="b2f29-129">Github readme</span><span class="sxs-lookup"><span data-stu-id="b2f29-129">Github readme</span></span>](https://github.com/Azure/azure-cosmosdb-java#guide-for-prod)</td></tr>

<tr><td><span data-ttu-id="b2f29-130">**Minimum supported runtime**</span><span class="sxs-lookup"><span data-stu-id="b2f29-130">**Minimum supported runtime**</span></span></td><td>[<span data-ttu-id="b2f29-131">JDK 8</span><span class="sxs-lookup"><span data-stu-id="b2f29-131">JDK 8</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b2f29-132">Release notes</span><span class="sxs-lookup"><span data-stu-id="b2f29-132">Release notes</span></span>

### <a name="a-name210210"></a><span data-ttu-id="b2f29-133"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-133"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="b2f29-134">Added support for Proxy.</span><span class="sxs-lookup"><span data-stu-id="b2f29-134">Added support for Proxy.</span></span>
* <span data-ttu-id="b2f29-135">Added support for resource token authorization.</span><span class="sxs-lookup"><span data-stu-id="b2f29-135">Added support for resource token authorization.</span></span>
* <span data-ttu-id="b2f29-136">Fixed a bug in handling large partition keys ([github #63](https://github.com/Azure/azure-cosmosdb-java/issues/63)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-136">Fixed a bug in handling large partition keys ([github #63](https://github.com/Azure/azure-cosmosdb-java/issues/63)).</span></span>
* <span data-ttu-id="b2f29-137">Documentation improved.</span><span class="sxs-lookup"><span data-stu-id="b2f29-137">Documentation improved.</span></span>
* <span data-ttu-id="b2f29-138">SDK restructured into more granular modules.</span><span class="sxs-lookup"><span data-stu-id="b2f29-138">SDK restructured into more granular modules.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="b2f29-139"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="b2f29-139"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="b2f29-140">Fixed a bug for non-english locales ([github #51](https://github.com/Azure/azure-cosmosdb-java/issues/51)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-140">Fixed a bug for non-english locales ([github #51](https://github.com/Azure/azure-cosmosdb-java/issues/51)).</span></span>
* <span data-ttu-id="b2f29-141">Added helper methods in Conflict Resource.</span><span class="sxs-lookup"><span data-stu-id="b2f29-141">Added helper methods in Conflict Resource.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="b2f29-142"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-142"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="b2f29-143">Replaced org.json dependency by jackson due to performance reasons and licensing ([github #29](https://github.com/Azure/azure-cosmosdb-java/issues/29)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-143">Replaced org.json dependency by jackson due to performance reasons and licensing ([github #29](https://github.com/Azure/azure-cosmosdb-java/issues/29)).</span></span>
* <span data-ttu-id="b2f29-144">Removed deprecated OfferV2 class.</span><span class="sxs-lookup"><span data-stu-id="b2f29-144">Removed deprecated OfferV2 class.</span></span>
* <span data-ttu-id="b2f29-145">Added accessor method to Offer class for throughput content.</span><span class="sxs-lookup"><span data-stu-id="b2f29-145">Added accessor method to Offer class for throughput content.</span></span>
* <span data-ttu-id="b2f29-146">Any method in Document/Resource returning org.json types changed to return a jackson object type.</span><span class="sxs-lookup"><span data-stu-id="b2f29-146">Any method in Document/Resource returning org.json types changed to return a jackson object type.</span></span>
* <span data-ttu-id="b2f29-147">getObject(.) method of classes extending JsonSerializable changed to return a jackson ObjectNode type.</span><span class="sxs-lookup"><span data-stu-id="b2f29-147">getObject(.) method of classes extending JsonSerializable changed to return a jackson ObjectNode type.</span></span>
* <span data-ttu-id="b2f29-148">getCollection(.) method changed to return Collection of ObjectNode.</span><span class="sxs-lookup"><span data-stu-id="b2f29-148">getCollection(.) method changed to return Collection of ObjectNode.</span></span>
* <span data-ttu-id="b2f29-149">Removed JsonSerializable subclasses' constructors with org.json.JSONObject arg.</span><span class="sxs-lookup"><span data-stu-id="b2f29-149">Removed JsonSerializable subclasses' constructors with org.json.JSONObject arg.</span></span>
* <span data-ttu-id="b2f29-150">JsonSerializable.toJson (SerializationFormattingPolicy.Indented) now uses two spaces for indentation.</span><span class="sxs-lookup"><span data-stu-id="b2f29-150">JsonSerializable.toJson (SerializationFormattingPolicy.Indented) now uses two spaces for indentation.</span></span>
  
### <a name="a-name102102"></a><span data-ttu-id="b2f29-151"><a name="1.0.2"/>1.0.2</span><span class="sxs-lookup"><span data-stu-id="b2f29-151"><a name="1.0.2"/>1.0.2</span></span>
* <span data-ttu-id="b2f29-152">Added support for Unique Index Policy.</span><span class="sxs-lookup"><span data-stu-id="b2f29-152">Added support for Unique Index Policy.</span></span>
* <span data-ttu-id="b2f29-153">Added support for limiting response continuation token size in feed options.</span><span class="sxs-lookup"><span data-stu-id="b2f29-153">Added support for limiting response continuation token size in feed options.</span></span>
* <span data-ttu-id="b2f29-154">Added support for Partition Split in Cross Partition Query.</span><span class="sxs-lookup"><span data-stu-id="b2f29-154">Added support for Partition Split in Cross Partition Query.</span></span>
* <span data-ttu-id="b2f29-155">Fixed a bug in Json timestamp serialization ([github #32](https://github.com/Azure/azure-cosmosdb-java/issues/32)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-155">Fixed a bug in Json timestamp serialization ([github #32](https://github.com/Azure/azure-cosmosdb-java/issues/32)).</span></span>
* <span data-ttu-id="b2f29-156">Fixed a bug in Json enum serialization.</span><span class="sxs-lookup"><span data-stu-id="b2f29-156">Fixed a bug in Json enum serialization.</span></span>
* <span data-ttu-id="b2f29-157">Fixed a bug in managing documents of 2MB size ([github #33](https://github.com/Azure/azure-cosmosdb-java/issues/33)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-157">Fixed a bug in managing documents of 2MB size ([github #33](https://github.com/Azure/azure-cosmosdb-java/issues/33)).</span></span>
* <span data-ttu-id="b2f29-158">Dependency com.fasterxml.jackson.core:jackson-databind upgraded to 2.9.5 due to a bug ([jackson-databind: github #1599](https://github.com/FasterXML/jackson-databind/issues/1599))</span><span class="sxs-lookup"><span data-stu-id="b2f29-158">Dependency com.fasterxml.jackson.core:jackson-databind upgraded to 2.9.5 due to a bug ([jackson-databind: github #1599](https://github.com/FasterXML/jackson-databind/issues/1599))</span></span>
* <span data-ttu-id="b2f29-159">Dependency on rxjava-extras upgraded to 0.8.0.17 due to a bug ([rxjava-extras: github #30](https://github.com/davidmoten/rxjava-extras/issues/30)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-159">Dependency on rxjava-extras upgraded to 0.8.0.17 due to a bug ([rxjava-extras: github #30](https://github.com/davidmoten/rxjava-extras/issues/30)).</span></span>
* <span data-ttu-id="b2f29-160">The metadata description in pom file updated to be inline with the rest of documentation.</span><span class="sxs-lookup"><span data-stu-id="b2f29-160">The metadata description in pom file updated to be inline with the rest of documentation.</span></span>
* <span data-ttu-id="b2f29-161">Syntax improvement ([github #41](https://github.com/Azure/azure-cosmosdb-java/issues/41)), ([github #40](https://github.com/Azure/azure-cosmosdb-java/issues/40)).</span><span class="sxs-lookup"><span data-stu-id="b2f29-161">Syntax improvement ([github #41](https://github.com/Azure/azure-cosmosdb-java/issues/41)), ([github #40](https://github.com/Azure/azure-cosmosdb-java/issues/40)).</span></span>

### <a name="a-name101101"></a><span data-ttu-id="b2f29-162"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="b2f29-162"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="b2f29-163">Added back-pressure support in query.</span><span class="sxs-lookup"><span data-stu-id="b2f29-163">Added back-pressure support in query.</span></span>
* <span data-ttu-id="b2f29-164">Added support for partition key range id in query.</span><span class="sxs-lookup"><span data-stu-id="b2f29-164">Added support for partition key range id in query.</span></span>
* <span data-ttu-id="b2f29-165">Fix to allow larger continuation token in request header (bugfix github #24).</span><span class="sxs-lookup"><span data-stu-id="b2f29-165">Fix to allow larger continuation token in request header (bugfix github #24).</span></span>
* <span data-ttu-id="b2f29-166">Netty dependency upgraded to 4.1.22.Final to ensure JVM shuts down after main thread finishes.</span><span class="sxs-lookup"><span data-stu-id="b2f29-166">Netty dependency upgraded to 4.1.22.Final to ensure JVM shuts down after main thread finishes.</span></span>
* <span data-ttu-id="b2f29-167">Fix to avoid passing session token when reading master resources.</span><span class="sxs-lookup"><span data-stu-id="b2f29-167">Fix to avoid passing session token when reading master resources.</span></span>
* <span data-ttu-id="b2f29-168">Added more examples.</span><span class="sxs-lookup"><span data-stu-id="b2f29-168">Added more examples.</span></span>
* <span data-ttu-id="b2f29-169">Added more benchmarking scenarios.</span><span class="sxs-lookup"><span data-stu-id="b2f29-169">Added more benchmarking scenarios.</span></span>
* <span data-ttu-id="b2f29-170">Fixed Java header files for proper java doc generation.</span><span class="sxs-lookup"><span data-stu-id="b2f29-170">Fixed Java header files for proper java doc generation.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b2f29-171"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-171"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="b2f29-172">GA SDK with end-to-end support for non-blocking IO using the [Netty library](http://netty.io/) in gateway mode.</span><span class="sxs-lookup"><span data-stu-id="b2f29-172">GA SDK with end-to-end support for non-blocking IO using the [Netty library](http://netty.io/) in gateway mode.</span></span> 

## <a name="release-and-retirement-dates"></a><span data-ttu-id="b2f29-173">Release and retirement dates</span><span class="sxs-lookup"><span data-stu-id="b2f29-173">Release and retirement dates</span></span>
<span data-ttu-id="b2f29-174">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="b2f29-174">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="b2f29-175">New features and functionality and optimizations are only added to the current SDK.</span><span class="sxs-lookup"><span data-stu-id="b2f29-175">New features and functionality and optimizations are only added to the current SDK.</span></span> <span data-ttu-id="b2f29-176">So it's recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="b2f29-176">So it's recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="b2f29-177">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="b2f29-177">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="b2f29-178">Version</span><span class="sxs-lookup"><span data-stu-id="b2f29-178">Version</span></span> | <span data-ttu-id="b2f29-179">Release Date</span><span class="sxs-lookup"><span data-stu-id="b2f29-179">Release Date</span></span> | <span data-ttu-id="b2f29-180">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="b2f29-180">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b2f29-181">2.1.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-181">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="b2f29-182">September 5, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-182">September 5, 2018</span></span>|--- |
| [<span data-ttu-id="b2f29-183">2.0.1</span><span class="sxs-lookup"><span data-stu-id="b2f29-183">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="b2f29-184">August 16, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-184">August 16, 2018</span></span>|--- |
| [<span data-ttu-id="b2f29-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-185">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="b2f29-186">June 20, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-186">June 20, 2018</span></span>|--- |
| [<span data-ttu-id="b2f29-187">1.0.2</span><span class="sxs-lookup"><span data-stu-id="b2f29-187">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="b2f29-188">May 18, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-188">May 18, 2018</span></span>|--- |
| [<span data-ttu-id="b2f29-189">1.0.1</span><span class="sxs-lookup"><span data-stu-id="b2f29-189">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="b2f29-190">April 20, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-190">April 20, 2018</span></span>|--- |
| [<span data-ttu-id="b2f29-191">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b2f29-191">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b2f29-192">February 27, 2018</span><span class="sxs-lookup"><span data-stu-id="b2f29-192">February 27, 2018</span></span>|--- |

## <a name="faq"></a><span data-ttu-id="b2f29-193">FAQ</span><span class="sxs-lookup"><span data-stu-id="b2f29-193">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="b2f29-194">See also</span><span class="sxs-lookup"><span data-stu-id="b2f29-194">See also</span></span>
<span data-ttu-id="b2f29-195">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="b2f29-195">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

