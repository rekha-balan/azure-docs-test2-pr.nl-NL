---
title: Azure DocumentDB .NET SDK & Resources | Microsoft Docs
description: Learn all about the .NET API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB .NET SDK.
services: documentdb
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/29/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 410a5d04286ebc9984142303c3edd67ca60500e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672259"
---
# <a name="documentdb-net-sdk-download-and-release-notes"></a><span data-ttu-id="d2638-103">DocumentDB .NET SDK: Download and release notes</span><span class="sxs-lookup"><span data-stu-id="d2638-103">DocumentDB .NET SDK: Download and release notes</span></span>
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

<tr><td><span data-ttu-id="d2638-112">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="d2638-112">**SDK download**</span></span></td><td>[<span data-ttu-id="d2638-113">NuGet</span><span class="sxs-lookup"><span data-stu-id="d2638-113">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="d2638-114">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="d2638-114">**API documentation**</span></span></td><td>[<span data-ttu-id="d2638-115">.NET API reference documentation</span><span class="sxs-lookup"><span data-stu-id="d2638-115">.NET API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn948556.aspx)</td></tr>

<tr><td><span data-ttu-id="d2638-116">**Samples**</span><span class="sxs-lookup"><span data-stu-id="d2638-116">**Samples**</span></span></td><td>[<span data-ttu-id="d2638-117">.NET code samples</span><span class="sxs-lookup"><span data-stu-id="d2638-117">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="d2638-118">**Get started**</span><span class="sxs-lookup"><span data-stu-id="d2638-118">**Get started**</span></span></td><td>[<span data-ttu-id="d2638-119">Get started with the DocumentDB .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d2638-119">Get started with the DocumentDB .NET SDK</span></span>](documentdb-get-started.md)</td></tr>

<tr><td><span data-ttu-id="d2638-120">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="d2638-120">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="d2638-121">Web application development with DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d2638-121">Web application development with DocumentDB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="d2638-122">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="d2638-122">**Current supported framework**</span></span></td><td>[<span data-ttu-id="d2638-123">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="d2638-123">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="d2638-124">Release notes</span><span class="sxs-lookup"><span data-stu-id="d2638-124">Release notes</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="d2638-125"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="d2638-125"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="d2638-126">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span><span class="sxs-lookup"><span data-stu-id="d2638-126">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="d2638-127"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="d2638-127"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="d2638-128">Fixes to make SDK more resilient to automatic failover under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="d2638-128">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="d2638-129"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="d2638-129"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="d2638-130">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span><span class="sxs-lookup"><span data-stu-id="d2638-130">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="d2638-131">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span><span class="sxs-lookup"><span data-stu-id="d2638-131">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="d2638-132"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="d2638-132"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="d2638-133">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="d2638-133">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="d2638-134">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span><span class="sxs-lookup"><span data-stu-id="d2638-134">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="d2638-135">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span><span class="sxs-lookup"><span data-stu-id="d2638-135">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="d2638-136">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span><span class="sxs-lookup"><span data-stu-id="d2638-136">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="d2638-137"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="d2638-137"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="d2638-138">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="d2638-138">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="d2638-139">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="d2638-139">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="d2638-140">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="d2638-140">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="d2638-141"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="d2638-141"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="d2638-142">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span><span class="sxs-lookup"><span data-stu-id="d2638-142">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span></span>
* <span data-ttu-id="d2638-143">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span><span class="sxs-lookup"><span data-stu-id="d2638-143">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="d2638-144">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span><span class="sxs-lookup"><span data-stu-id="d2638-144">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="d2638-145">Client side performance fixes for increasing the read and write throughput of the requests.</span><span class="sxs-lookup"><span data-stu-id="d2638-145">Client side performance fixes for increasing the read and write throughput of the requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="d2638-146"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="d2638-146"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="d2638-147">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span><span class="sxs-lookup"><span data-stu-id="d2638-147">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span></span>
* <span data-ttu-id="d2638-148">Added support for the SDK to work in a 32-bit host process.</span><span class="sxs-lookup"><span data-stu-id="d2638-148">Added support for the SDK to work in a 32-bit host process.</span></span> <span data-ttu-id="d2638-149">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span><span class="sxs-lookup"><span data-stu-id="d2638-149">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="d2638-150">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span><span class="sxs-lookup"><span data-stu-id="d2638-150">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="d2638-151">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span><span class="sxs-lookup"><span data-stu-id="d2638-151">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="d2638-152"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="d2638-152"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="d2638-153">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span><span class="sxs-lookup"><span data-stu-id="d2638-153">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="d2638-154">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="d2638-154">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="d2638-155"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="d2638-155"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="d2638-156">Support for new classes and methods to process the [change feed](documentdb-change-feed.md) of documents within a collection.</span><span class="sxs-lookup"><span data-stu-id="d2638-156">Support for new classes and methods to process the [change feed](documentdb-change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="d2638-157">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span><span class="sxs-lookup"><span data-stu-id="d2638-157">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="d2638-158">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span><span class="sxs-lookup"><span data-stu-id="d2638-158">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="d2638-159">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span><span class="sxs-lookup"><span data-stu-id="d2638-159">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="d2638-160">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span><span class="sxs-lookup"><span data-stu-id="d2638-160">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="d2638-161">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span><span class="sxs-lookup"><span data-stu-id="d2638-161">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="d2638-162"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="d2638-162"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="d2638-163">Added direct connectivity support for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="d2638-163">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="d2638-164">Improved performance for the Bounded Staleness consistency level.</span><span class="sxs-lookup"><span data-stu-id="d2638-164">Improved performance for the Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="d2638-165">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span><span class="sxs-lookup"><span data-stu-id="d2638-165">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="d2638-166">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span><span class="sxs-lookup"><span data-stu-id="d2638-166">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="d2638-167">Various SDK bug fixes.</span><span class="sxs-lookup"><span data-stu-id="d2638-167">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="d2638-168"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="d2638-168"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="d2638-169">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span><span class="sxs-lookup"><span data-stu-id="d2638-169">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span></span> <span data-ttu-id="d2638-170">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span><span class="sxs-lookup"><span data-stu-id="d2638-170">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="d2638-171">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span><span class="sxs-lookup"><span data-stu-id="d2638-171">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="d2638-172"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="d2638-172"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="d2638-173">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span><span class="sxs-lookup"><span data-stu-id="d2638-173">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="d2638-174">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span><span class="sxs-lookup"><span data-stu-id="d2638-174">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="d2638-175"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="d2638-175"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="d2638-176">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span><span class="sxs-lookup"><span data-stu-id="d2638-176">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span></span>
* <span data-ttu-id="d2638-177">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span><span class="sxs-lookup"><span data-stu-id="d2638-177">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="d2638-178"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="d2638-178"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="d2638-179">Added support for parallel queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="d2638-179">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="d2638-180">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="d2638-180">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="d2638-181">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing a DocumentDB project with a reference to the DocumentDB Nuget package.</span><span class="sxs-lookup"><span data-stu-id="d2638-181">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing a DocumentDB project with a reference to the DocumentDB Nuget package.</span></span>
* <span data-ttu-id="d2638-182">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span><span class="sxs-lookup"><span data-stu-id="d2638-182">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="d2638-183">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span><span class="sxs-lookup"><span data-stu-id="d2638-183">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span></span>
* <span data-ttu-id="d2638-184">Added methods to the IDocumentClient interface that were missing:</span><span class="sxs-lookup"><span data-stu-id="d2638-184">Added methods to the IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="d2638-185">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span><span class="sxs-lookup"><span data-stu-id="d2638-185">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="d2638-186">CreateAttachmentAsync method that takes options as a parameter</span><span class="sxs-lookup"><span data-stu-id="d2638-186">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="d2638-187">CreateOfferQuery method that takes querySpec as a parameter.</span><span class="sxs-lookup"><span data-stu-id="d2638-187">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="d2638-188">Unsealed public classes that are exposed in the IDocumentClient interface.</span><span class="sxs-lookup"><span data-stu-id="d2638-188">Unsealed public classes that are exposed in the IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="d2638-189"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="d2638-189"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="d2638-190">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="d2638-190">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="d2638-191">Added support for retry on throttled requests.</span><span class="sxs-lookup"><span data-stu-id="d2638-191">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="d2638-192">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span><span class="sxs-lookup"><span data-stu-id="d2638-192">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="d2638-193">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span><span class="sxs-lookup"><span data-stu-id="d2638-193">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="d2638-194">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span><span class="sxs-lookup"><span data-stu-id="d2638-194">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span></span>
* <span data-ttu-id="d2638-195">Added configuration option to set the ServicePoint.ConnectionLimit for a given DocumentDB endpoint Uri.</span><span class="sxs-lookup"><span data-stu-id="d2638-195">Added configuration option to set the ServicePoint.ConnectionLimit for a given DocumentDB endpoint Uri.</span></span>  <span data-ttu-id="d2638-196">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span><span class="sxs-lookup"><span data-stu-id="d2638-196">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span></span>
* <span data-ttu-id="d2638-197">Deprecated IPartitionResolver and its implementation.</span><span class="sxs-lookup"><span data-stu-id="d2638-197">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="d2638-198">Support for IPartitionResolver is now obsolete.</span><span class="sxs-lookup"><span data-stu-id="d2638-198">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="d2638-199">It's recommended that you use Partitioned Collections for higher storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="d2638-199">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="d2638-200"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="d2638-200"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="d2638-201">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span><span class="sxs-lookup"><span data-stu-id="d2638-201">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="d2638-202"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="d2638-202"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="d2638-203">Added time to live (TTL) support for documents.</span><span class="sxs-lookup"><span data-stu-id="d2638-203">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="d2638-204"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="d2638-204"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="d2638-205">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span><span class="sxs-lookup"><span data-stu-id="d2638-205">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="d2638-206"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="d2638-206"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="d2638-207">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d2638-207">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="d2638-208"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="d2638-208"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="d2638-209">**[Fixed]** Querying DocumentDB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span><span class="sxs-lookup"><span data-stu-id="d2638-209">**[Fixed]** Querying DocumentDB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="d2638-210"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="d2638-210"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="d2638-211">Expanded LINQ support including new operators for paging, conditional expressions and range comparison.</span><span class="sxs-lookup"><span data-stu-id="d2638-211">Expanded LINQ support including new operators for paging, conditional expressions and range comparison.</span></span>
  * <span data-ttu-id="d2638-212">Take operator to enable SELECT TOP behavior in LINQ</span><span class="sxs-lookup"><span data-stu-id="d2638-212">Take operator to enable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="d2638-213">CompareTo operator to enable string range comparisons</span><span class="sxs-lookup"><span data-stu-id="d2638-213">CompareTo operator to enable string range comparisons</span></span>
  * <span data-ttu-id="d2638-214">Conditional (?) and coalesce operators (??)</span><span class="sxs-lookup"><span data-stu-id="d2638-214">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="d2638-215">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in linq query.</span><span class="sxs-lookup"><span data-stu-id="d2638-215">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in linq query.</span></span>  [<span data-ttu-id="d2638-216">#81</span><span class="sxs-lookup"><span data-stu-id="d2638-216">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="d2638-217"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="d2638-217"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="d2638-218">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT \* incorrectly.</span><span class="sxs-lookup"><span data-stu-id="d2638-218">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT \* incorrectly.</span></span>  [<span data-ttu-id="d2638-219">#58</span><span class="sxs-lookup"><span data-stu-id="d2638-219">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="d2638-220"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="d2638-220"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="d2638-221">Implemented Upsert, Added UpsertXXXAsync methods</span><span class="sxs-lookup"><span data-stu-id="d2638-221">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="d2638-222">Performance improvements for all requests</span><span class="sxs-lookup"><span data-stu-id="d2638-222">Performance improvements for all requests</span></span>
* <span data-ttu-id="d2638-223">LINQ Provider support for conditional, coalesce and CompareTo methods for strings</span><span class="sxs-lookup"><span data-stu-id="d2638-223">LINQ Provider support for conditional, coalesce and CompareTo methods for strings</span></span>
* <span data-ttu-id="d2638-224">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span><span class="sxs-lookup"><span data-stu-id="d2638-224">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="d2638-225">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span><span class="sxs-lookup"><span data-stu-id="d2638-225">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="d2638-226">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span><span class="sxs-lookup"><span data-stu-id="d2638-226">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="d2638-227"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="d2638-227"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="d2638-228">**[Fixed]** Localization issues when using non en culture info such as nl-NL etc.</span><span class="sxs-lookup"><span data-stu-id="d2638-228">**[Fixed]** Localization issues when using non en culture info such as nl-NL etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="d2638-229"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="d2638-229"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="d2638-230">ID Based Routing</span><span class="sxs-lookup"><span data-stu-id="d2638-230">ID Based Routing</span></span>
  * <span data-ttu-id="d2638-231">New UriFactory helper to assist with constructing ID based resource links</span><span class="sxs-lookup"><span data-stu-id="d2638-231">New UriFactory helper to assist with constructing ID based resource links</span></span>
  * <span data-ttu-id="d2638-232">New overloads on DocumentClient to take in URI</span><span class="sxs-lookup"><span data-stu-id="d2638-232">New overloads on DocumentClient to take in URI</span></span>
* <span data-ttu-id="d2638-233">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span><span class="sxs-lookup"><span data-stu-id="d2638-233">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="d2638-234">LINQ Provider support enhanced</span><span class="sxs-lookup"><span data-stu-id="d2638-234">LINQ Provider support enhanced</span></span>
  * <span data-ttu-id="d2638-235">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span><span class="sxs-lookup"><span data-stu-id="d2638-235">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="d2638-236">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span><span class="sxs-lookup"><span data-stu-id="d2638-236">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="d2638-237">**Array** - Concat, Contains, Count</span><span class="sxs-lookup"><span data-stu-id="d2638-237">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="d2638-238">**IN** operator</span><span class="sxs-lookup"><span data-stu-id="d2638-238">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="d2638-239"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="d2638-239"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="d2638-240">Added support for modifying indexing policies</span><span class="sxs-lookup"><span data-stu-id="d2638-240">Added support for modifying indexing policies</span></span>
  * <span data-ttu-id="d2638-241">New ReplaceDocumentCollectionAsync method in DocumentClient</span><span class="sxs-lookup"><span data-stu-id="d2638-241">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="d2638-242">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span><span class="sxs-lookup"><span data-stu-id="d2638-242">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="d2638-243">DocumentCollection.IndexingPolicy is now mutable</span><span class="sxs-lookup"><span data-stu-id="d2638-243">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="d2638-244">Added support for spatial indexing and query</span><span class="sxs-lookup"><span data-stu-id="d2638-244">Added support for spatial indexing and query</span></span>
  * <span data-ttu-id="d2638-245">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span><span class="sxs-lookup"><span data-stu-id="d2638-245">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="d2638-246">New SpatialIndex class for indexing GeoJSON data stored in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d2638-246">New SpatialIndex class for indexing GeoJSON data stored in DocumentDB</span></span>
* <span data-ttu-id="d2638-247">**[Fixed]** : Incorrect SQL query generated from linq expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38)</span><span class="sxs-lookup"><span data-stu-id="d2638-247">**[Fixed]** : Incorrect SQL query generated from linq expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38)</span></span>

### <a name="a-name120120"></a><span data-ttu-id="d2638-248"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="d2638-248"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="d2638-249">Dependency on Newtonsoft.Json v5.0.7</span><span class="sxs-lookup"><span data-stu-id="d2638-249">Dependency on Newtonsoft.Json v5.0.7</span></span> 
* <span data-ttu-id="d2638-250">Changes to support Order By</span><span class="sxs-lookup"><span data-stu-id="d2638-250">Changes to support Order By</span></span>
  
  * <span data-ttu-id="d2638-251">LINQ provider support for OrderBy() or OrderByDescending()</span><span class="sxs-lookup"><span data-stu-id="d2638-251">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="d2638-252">IndexingPolicy to support Order By</span><span class="sxs-lookup"><span data-stu-id="d2638-252">IndexingPolicy to support Order By</span></span> 
    
    <span data-ttu-id="d2638-253">**NB: Possible breaking change**</span><span class="sxs-lookup"><span data-stu-id="d2638-253">**NB: Possible breaking change**</span></span> 
    
    <span data-ttu-id="d2638-254">If you have existing code that provisions collections with a custom indexing policy, then your existing code will need to be updated to support the new IndexingPolicy class.</span><span class="sxs-lookup"><span data-stu-id="d2638-254">If you have existing code that provisions collections with a custom indexing policy, then your existing code will need to be updated to support the new IndexingPolicy class.</span></span> <span data-ttu-id="d2638-255">If you have no custom indexing policy, then this change does not affect you.</span><span class="sxs-lookup"><span data-stu-id="d2638-255">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="d2638-256"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="d2638-256"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="d2638-257">Support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver</span><span class="sxs-lookup"><span data-stu-id="d2638-257">Support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver</span></span>
* <span data-ttu-id="d2638-258">DataContract serialization</span><span class="sxs-lookup"><span data-stu-id="d2638-258">DataContract serialization</span></span>
* <span data-ttu-id="d2638-259">Guid support in LINQ provider</span><span class="sxs-lookup"><span data-stu-id="d2638-259">Guid support in LINQ provider</span></span>
* <span data-ttu-id="d2638-260">UDF support in LINQ</span><span class="sxs-lookup"><span data-stu-id="d2638-260">UDF support in LINQ</span></span>

### <a name="a-name100100"></a><span data-ttu-id="d2638-261"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="d2638-261"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="d2638-262">GA SDK</span><span class="sxs-lookup"><span data-stu-id="d2638-262">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="d2638-263">Release & Retirement dates</span><span class="sxs-lookup"><span data-stu-id="d2638-263">Release & Retirement dates</span></span>
<span data-ttu-id="d2638-264">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="d2638-264">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="d2638-265">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="d2638-265">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="d2638-266">Any request to DocumentDB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="d2638-266">Any request to DocumentDB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="d2638-267">Version</span><span class="sxs-lookup"><span data-stu-id="d2638-267">Version</span></span> | <span data-ttu-id="d2638-268">Release Date</span><span class="sxs-lookup"><span data-stu-id="d2638-268">Release Date</span></span> | <span data-ttu-id="d2638-269">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="d2638-269">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d2638-270">1.13.1</span><span class="sxs-lookup"><span data-stu-id="d2638-270">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="d2638-271">March 29, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-271">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-272">1.13.0</span><span class="sxs-lookup"><span data-stu-id="d2638-272">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="d2638-273">March 24, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-273">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-274">1.12.2</span><span class="sxs-lookup"><span data-stu-id="d2638-274">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="d2638-275">March 20, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-275">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-276">1.12.1</span><span class="sxs-lookup"><span data-stu-id="d2638-276">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="d2638-277">March 14, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-277">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-278">1.12.0</span><span class="sxs-lookup"><span data-stu-id="d2638-278">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="d2638-279">February 15, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-279">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-280">1.11.4</span><span class="sxs-lookup"><span data-stu-id="d2638-280">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="d2638-281">February 06, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-281">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-282">1.11.3</span><span class="sxs-lookup"><span data-stu-id="d2638-282">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="d2638-283">January 26, 2017</span><span class="sxs-lookup"><span data-stu-id="d2638-283">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="d2638-284">1.11.1</span><span class="sxs-lookup"><span data-stu-id="d2638-284">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="d2638-285">December 21, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-285">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-286">1.11.0</span><span class="sxs-lookup"><span data-stu-id="d2638-286">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="d2638-287">December 08, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-287">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-288">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d2638-288">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="d2638-289">September 27, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-289">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-290">1.9.5</span><span class="sxs-lookup"><span data-stu-id="d2638-290">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="d2638-291">September 01, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-291">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-292">1.9.4</span><span class="sxs-lookup"><span data-stu-id="d2638-292">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="d2638-293">August 24, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-293">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-294">1.9.3</span><span class="sxs-lookup"><span data-stu-id="d2638-294">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="d2638-295">August 15, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-295">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-296">1.9.2</span><span class="sxs-lookup"><span data-stu-id="d2638-296">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="d2638-297">July 23, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-297">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-298">1.8.0</span><span class="sxs-lookup"><span data-stu-id="d2638-298">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="d2638-299">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-299">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-300">1.7.1</span><span class="sxs-lookup"><span data-stu-id="d2638-300">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="d2638-301">May 06, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-301">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-302">1.7.0</span><span class="sxs-lookup"><span data-stu-id="d2638-302">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="d2638-303">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-303">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-304">1.6.3</span><span class="sxs-lookup"><span data-stu-id="d2638-304">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="d2638-305">April 08, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-305">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-306">1.6.2</span><span class="sxs-lookup"><span data-stu-id="d2638-306">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="d2638-307">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-307">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-308">1.5.3</span><span class="sxs-lookup"><span data-stu-id="d2638-308">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="d2638-309">February 19, 2016</span><span class="sxs-lookup"><span data-stu-id="d2638-309">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="d2638-310">1.5.2</span><span class="sxs-lookup"><span data-stu-id="d2638-310">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="d2638-311">December 14, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-311">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-312">1.5.1</span><span class="sxs-lookup"><span data-stu-id="d2638-312">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="d2638-313">November 23, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-313">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-314">1.5.0</span><span class="sxs-lookup"><span data-stu-id="d2638-314">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="d2638-315">October 05, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-315">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-316">1.4.1</span><span class="sxs-lookup"><span data-stu-id="d2638-316">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="d2638-317">August 25, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-317">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-318">1.4.0</span><span class="sxs-lookup"><span data-stu-id="d2638-318">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="d2638-319">August 13, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-319">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-320">1.3.0</span><span class="sxs-lookup"><span data-stu-id="d2638-320">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="d2638-321">August 05, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-321">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-322">1.2.0</span><span class="sxs-lookup"><span data-stu-id="d2638-322">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="d2638-323">July 06, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-323">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-324">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d2638-324">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="d2638-325">April 30, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-325">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="d2638-326">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d2638-326">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="d2638-327">April 08, 2015</span><span class="sxs-lookup"><span data-stu-id="d2638-327">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="d2638-328">FAQ</span><span class="sxs-lookup"><span data-stu-id="d2638-328">FAQ</span></span>
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="d2638-329">See also</span><span class="sxs-lookup"><span data-stu-id="d2638-329">See also</span></span>
<span data-ttu-id="d2638-330">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span><span class="sxs-lookup"><span data-stu-id="d2638-330">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span></span> 

