---
title: 'Azure Cosmos DB: .NET Change Feed Processor API, SDK & resources | Microsoft Docs'
description: Learn all about the Change Feed Processor API and SDK including release dates, retirement dates, and changes made between each version of the .NET Change Feed Processor SDK.
services: cosmos-db
author: ealsur
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: dotnet
ms.topic: reference
ms.date: 05/21/2018
ms.author: maquaran
ms.openlocfilehash: b55972099715d32b3cb3ae5a3793ad1a0c676c42
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855616"
---
# <a name="net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="d7edc-103">.NET Change Feed Processor SDK: Download and release notes</span><span class="sxs-lookup"><span data-stu-id="d7edc-103">.NET Change Feed Processor SDK: Download and release notes</span></span>
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

|   |   |
|---|---|
|<span data-ttu-id="d7edc-116">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="d7edc-116">**SDK download**</span></span>|[<span data-ttu-id="d7edc-117">NuGet</span><span class="sxs-lookup"><span data-stu-id="d7edc-117">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)|
|<span data-ttu-id="d7edc-118">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="d7edc-118">**API documentation**</span></span>|[<span data-ttu-id="d7edc-119">Change Feed Processor library API reference documentation</span><span class="sxs-lookup"><span data-stu-id="d7edc-119">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)|
|<span data-ttu-id="d7edc-120">**Get started**</span><span class="sxs-lookup"><span data-stu-id="d7edc-120">**Get started**</span></span>|[<span data-ttu-id="d7edc-121">Get started with the Change Feed Processor .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d7edc-121">Get started with the Change Feed Processor .NET SDK</span></span>](change-feed.md)|
|<span data-ttu-id="d7edc-122">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="d7edc-122">**Current supported framework**</span></span>| [<span data-ttu-id="d7edc-123">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="d7edc-123">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</br> [<span data-ttu-id="d7edc-124">Microsoft .NET Core</span><span class="sxs-lookup"><span data-stu-id="d7edc-124">Microsoft .NET Core</span></span>](https://www.microsoft.com/net/download/core) |

## <a name="release-notes"></a><span data-ttu-id="d7edc-125">Release notes</span><span class="sxs-lookup"><span data-stu-id="d7edc-125">Release notes</span></span>

### <a name="v2-builds"></a><span data-ttu-id="d7edc-126">v2 builds</span><span class="sxs-lookup"><span data-stu-id="d7edc-126">v2 builds</span></span>

### <a name="a-name206206"></a><span data-ttu-id="d7edc-127"><a name="2.0.6"/>2.0.6</span><span class="sxs-lookup"><span data-stu-id="d7edc-127"><a name="2.0.6"/>2.0.6</span></span>
* <span data-ttu-id="d7edc-128">Added ChangeFeedEventHost.HostName public property for compativility with v1.</span><span class="sxs-lookup"><span data-stu-id="d7edc-128">Added ChangeFeedEventHost.HostName public property for compativility with v1.</span></span>

### <a name="a-name205205"></a><span data-ttu-id="d7edc-129"><a name="2.0.5"/>2.0.5</span><span class="sxs-lookup"><span data-stu-id="d7edc-129"><a name="2.0.5"/>2.0.5</span></span>
* <span data-ttu-id="d7edc-130">Fixed a race condition that occurs during partition split.</span><span class="sxs-lookup"><span data-stu-id="d7edc-130">Fixed a race condition that occurs during partition split.</span></span> <span data-ttu-id="d7edc-131">The race condition may lead to acquiring lease and immediately losing it during partition split and causing contention.</span><span class="sxs-lookup"><span data-stu-id="d7edc-131">The race condition may lead to acquiring lease and immediately losing it during partition split and causing contention.</span></span> <span data-ttu-id="d7edc-132">The race condition issue is fixed with this release.</span><span class="sxs-lookup"><span data-stu-id="d7edc-132">The race condition issue is fixed with this release.</span></span>

### <a name="a-name204204"></a><span data-ttu-id="d7edc-133"><a name="2.0.4"/>2.0.4</span><span class="sxs-lookup"><span data-stu-id="d7edc-133"><a name="2.0.4"/>2.0.4</span></span>
* <span data-ttu-id="d7edc-134">GA SDK</span><span class="sxs-lookup"><span data-stu-id="d7edc-134">GA SDK</span></span>

### <a name="a-name203-prerelease203-prerelease"></a><span data-ttu-id="d7edc-135"><a name="2.0.3-prerelease"/>2.0.3-prerelease</span><span class="sxs-lookup"><span data-stu-id="d7edc-135"><a name="2.0.3-prerelease"/>2.0.3-prerelease</span></span>
* <span data-ttu-id="d7edc-136">Fixed the following issues:</span><span class="sxs-lookup"><span data-stu-id="d7edc-136">Fixed the following issues:</span></span>
  * <span data-ttu-id="d7edc-137">When partition split happens, there could be duplicate processing of documents modified before the split.</span><span class="sxs-lookup"><span data-stu-id="d7edc-137">When partition split happens, there could be duplicate processing of documents modified before the split.</span></span>
  * <span data-ttu-id="d7edc-138">The GetEstimatedRemainingWork API returned 0 when no leases were present in the lease collection.</span><span class="sxs-lookup"><span data-stu-id="d7edc-138">The GetEstimatedRemainingWork API returned 0 when no leases were present in the lease collection.</span></span>

* <span data-ttu-id="d7edc-139">The following exceptions are made public.</span><span class="sxs-lookup"><span data-stu-id="d7edc-139">The following exceptions are made public.</span></span> <span data-ttu-id="d7edc-140">Extensions that implement IPartitionProcessor can throw these exceptions.</span><span class="sxs-lookup"><span data-stu-id="d7edc-140">Extensions that implement IPartitionProcessor can throw these exceptions.</span></span>
  * <span data-ttu-id="d7edc-141">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.LeaseLostException.</span><span class="sxs-lookup"><span data-stu-id="d7edc-141">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.LeaseLostException.</span></span> 
  * <span data-ttu-id="d7edc-142">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionException.</span><span class="sxs-lookup"><span data-stu-id="d7edc-142">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionException.</span></span> 
  * <span data-ttu-id="d7edc-143">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="d7edc-143">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionNotFoundException.</span></span>
  * <span data-ttu-id="d7edc-144">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionSplitException.</span><span class="sxs-lookup"><span data-stu-id="d7edc-144">Microsoft.Azure.Documents.ChangeFeedProcessor.Exceptions.PartitionSplitException.</span></span> 

### <a name="a-name202-prerelease202-prerelease"></a><span data-ttu-id="d7edc-145"><a name="2.0.2-prerelease"/>2.0.2-prerelease</span><span class="sxs-lookup"><span data-stu-id="d7edc-145"><a name="2.0.2-prerelease"/>2.0.2-prerelease</span></span>
* <span data-ttu-id="d7edc-146">Minor API changes:</span><span class="sxs-lookup"><span data-stu-id="d7edc-146">Minor API changes:</span></span>
  * <span data-ttu-id="d7edc-147">Removed ChangeFeedProcessorOptions.IsAutoCheckpointEnabled that was marked as obsolete.</span><span class="sxs-lookup"><span data-stu-id="d7edc-147">Removed ChangeFeedProcessorOptions.IsAutoCheckpointEnabled that was marked as obsolete.</span></span>

### <a name="a-name201-prerelease201-prerelease"></a><span data-ttu-id="d7edc-148"><a name="2.0.1-prerelease"/>2.0.1-prerelease</span><span class="sxs-lookup"><span data-stu-id="d7edc-148"><a name="2.0.1-prerelease"/>2.0.1-prerelease</span></span>
* <span data-ttu-id="d7edc-149">Stability improvements:</span><span class="sxs-lookup"><span data-stu-id="d7edc-149">Stability improvements:</span></span>
  * <span data-ttu-id="d7edc-150">Better handling of lease store initialization.</span><span class="sxs-lookup"><span data-stu-id="d7edc-150">Better handling of lease store initialization.</span></span> <span data-ttu-id="d7edc-151">When lease store is empty, only one instance of processor can initialize it, the others will wait.</span><span class="sxs-lookup"><span data-stu-id="d7edc-151">When lease store is empty, only one instance of processor can initialize it, the others will wait.</span></span>
  * <span data-ttu-id="d7edc-152">More stable/efficient lease renewal/release.</span><span class="sxs-lookup"><span data-stu-id="d7edc-152">More stable/efficient lease renewal/release.</span></span> <span data-ttu-id="d7edc-153">Renewing and releasing a lease one partition is independent from renewing others.</span><span class="sxs-lookup"><span data-stu-id="d7edc-153">Renewing and releasing a lease one partition is independent from renewing others.</span></span> <span data-ttu-id="d7edc-154">In v1 that was done sequentially for all partitions.</span><span class="sxs-lookup"><span data-stu-id="d7edc-154">In v1 that was done sequentially for all partitions.</span></span>
* <span data-ttu-id="d7edc-155">New v2 API:</span><span class="sxs-lookup"><span data-stu-id="d7edc-155">New v2 API:</span></span>
  * <span data-ttu-id="d7edc-156">Builder pattern for flexible construction of the processor: the ChangeFeedProcessorBuilder class.</span><span class="sxs-lookup"><span data-stu-id="d7edc-156">Builder pattern for flexible construction of the processor: the ChangeFeedProcessorBuilder class.</span></span>
    * <span data-ttu-id="d7edc-157">Can take any combination of parameters.</span><span class="sxs-lookup"><span data-stu-id="d7edc-157">Can take any combination of parameters.</span></span>
    * <span data-ttu-id="d7edc-158">Can take DocumentClient instance for monitoring and/or lease collection (not available in v1).</span><span class="sxs-lookup"><span data-stu-id="d7edc-158">Can take DocumentClient instance for monitoring and/or lease collection (not available in v1).</span></span>
  * <span data-ttu-id="d7edc-159">IChangeFeedObserver.ProcessChangesAsync now takes CancellationToken.</span><span class="sxs-lookup"><span data-stu-id="d7edc-159">IChangeFeedObserver.ProcessChangesAsync now takes CancellationToken.</span></span>
  * <span data-ttu-id="d7edc-160">IRemainingWorkEstimator - the remaining work estimator can be used separately from the processor.</span><span class="sxs-lookup"><span data-stu-id="d7edc-160">IRemainingWorkEstimator - the remaining work estimator can be used separately from the processor.</span></span>
  * <span data-ttu-id="d7edc-161">New extensibility points:</span><span class="sxs-lookup"><span data-stu-id="d7edc-161">New extensibility points:</span></span>
    * <span data-ttu-id="d7edc-162">IParitionLoadBalancingStrategy - for custom load-balancing of partitions between instances of the processor.</span><span class="sxs-lookup"><span data-stu-id="d7edc-162">IParitionLoadBalancingStrategy - for custom load-balancing of partitions between instances of the processor.</span></span>
    * <span data-ttu-id="d7edc-163">ILease, ILeaseManager - for custom lease management.</span><span class="sxs-lookup"><span data-stu-id="d7edc-163">ILease, ILeaseManager - for custom lease management.</span></span>
    * <span data-ttu-id="d7edc-164">IPartitionProcessor - for custom processing changes on a partition.</span><span class="sxs-lookup"><span data-stu-id="d7edc-164">IPartitionProcessor - for custom processing changes on a partition.</span></span>
* <span data-ttu-id="d7edc-165">Logging - uses [LibLog](https://github.com/damianh/LibLog) library.</span><span class="sxs-lookup"><span data-stu-id="d7edc-165">Logging - uses [LibLog](https://github.com/damianh/LibLog) library.</span></span>
* <span data-ttu-id="d7edc-166">100% backward compatible with v1 API.</span><span class="sxs-lookup"><span data-stu-id="d7edc-166">100% backward compatible with v1 API.</span></span>
* <span data-ttu-id="d7edc-167">New code base.</span><span class="sxs-lookup"><span data-stu-id="d7edc-167">New code base.</span></span>
* <span data-ttu-id="d7edc-168">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.21.1 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-168">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.21.1 and above.</span></span>

### <a name="v1-builds"></a><span data-ttu-id="d7edc-169">v1 builds</span><span class="sxs-lookup"><span data-stu-id="d7edc-169">v1 builds</span></span>

### <a name="a-name133133"></a><span data-ttu-id="d7edc-170"><a name="1.3.3"/>1.3.3</span><span class="sxs-lookup"><span data-stu-id="d7edc-170"><a name="1.3.3"/>1.3.3</span></span>
* <span data-ttu-id="d7edc-171">Added more logging.</span><span class="sxs-lookup"><span data-stu-id="d7edc-171">Added more logging.</span></span>
* <span data-ttu-id="d7edc-172">Fixed a DocumentClient leak when calling the pending work estimation multiple times.</span><span class="sxs-lookup"><span data-stu-id="d7edc-172">Fixed a DocumentClient leak when calling the pending work estimation multiple times.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="d7edc-173"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="d7edc-173"><a name="1.3.2"/>1.3.2</span></span>
* <span data-ttu-id="d7edc-174">Fixes in the pending work estimation.</span><span class="sxs-lookup"><span data-stu-id="d7edc-174">Fixes in the pending work estimation.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="d7edc-175"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="d7edc-175"><a name="1.3.1"/>1.3.1</span></span>
* <span data-ttu-id="d7edc-176">Stability improvements.</span><span class="sxs-lookup"><span data-stu-id="d7edc-176">Stability improvements.</span></span>
  * <span data-ttu-id="d7edc-177">Fix for handling cancelled tasks issue that might lead to stopped observers on some partitions.</span><span class="sxs-lookup"><span data-stu-id="d7edc-177">Fix for handling cancelled tasks issue that might lead to stopped observers on some partitions.</span></span>
* <span data-ttu-id="d7edc-178">Support for manual checkpointing.</span><span class="sxs-lookup"><span data-stu-id="d7edc-178">Support for manual checkpointing.</span></span>
* <span data-ttu-id="d7edc-179">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.21 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-179">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.21 and above.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="d7edc-180"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-180"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="d7edc-181">Adds support for .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="d7edc-181">Adds support for .NET Standard 2.0.</span></span> <span data-ttu-id="d7edc-182">The package now supports `netstandard2.0` and `net451` framework monikers.</span><span class="sxs-lookup"><span data-stu-id="d7edc-182">The package now supports `netstandard2.0` and `net451` framework monikers.</span></span>
* <span data-ttu-id="d7edc-183">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.17.0 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-183">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.17.0 and above.</span></span>
* <span data-ttu-id="d7edc-184">Compatible with [SQL .NET Core SDK](sql-api-sdk-dotnet-core.md) versions 1.5.1 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-184">Compatible with [SQL .NET Core SDK](sql-api-sdk-dotnet-core.md) versions 1.5.1 and above.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="d7edc-185"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="d7edc-185"><a name="1.1.1"/>1.1.1</span></span>
* <span data-ttu-id="d7edc-186">Fixes an issue with the calculation of the estimate of remaining work when the Change Feed was empty or no work was pending.</span><span class="sxs-lookup"><span data-stu-id="d7edc-186">Fixes an issue with the calculation of the estimate of remaining work when the Change Feed was empty or no work was pending.</span></span>
* <span data-ttu-id="d7edc-187">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.13.2 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-187">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="d7edc-188"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-188"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="d7edc-189">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span><span class="sxs-lookup"><span data-stu-id="d7edc-189">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="d7edc-190">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.13.2 and above.</span><span class="sxs-lookup"><span data-stu-id="d7edc-190">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="d7edc-191"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-191"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="d7edc-192">GA SDK</span><span class="sxs-lookup"><span data-stu-id="d7edc-192">GA SDK</span></span>
* <span data-ttu-id="d7edc-193">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.14.1 and below.</span><span class="sxs-lookup"><span data-stu-id="d7edc-193">Compatible with [SQL .NET SDK](sql-api-sdk-dotnet.md) versions 1.14.1 and below.</span></span>


## <a name="release--retirement-dates"></a><span data-ttu-id="d7edc-194">Release & Retirement dates</span><span class="sxs-lookup"><span data-stu-id="d7edc-194">Release & Retirement dates</span></span>
<span data-ttu-id="d7edc-195">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="d7edc-195">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="d7edc-196">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="d7edc-196">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="d7edc-197">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="d7edc-197">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="d7edc-198">Version</span><span class="sxs-lookup"><span data-stu-id="d7edc-198">Version</span></span> | <span data-ttu-id="d7edc-199">Release Date</span><span class="sxs-lookup"><span data-stu-id="d7edc-199">Release Date</span></span> | <span data-ttu-id="d7edc-200">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="d7edc-200">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d7edc-201">1.3.3</span><span class="sxs-lookup"><span data-stu-id="d7edc-201">1.3.3</span></span>](#1.3.3) |<span data-ttu-id="d7edc-202">May 08, 2018</span><span class="sxs-lookup"><span data-stu-id="d7edc-202">May 08, 2018</span></span> |--- |
| [<span data-ttu-id="d7edc-203">1.3.2</span><span class="sxs-lookup"><span data-stu-id="d7edc-203">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="d7edc-204">April 18, 2018</span><span class="sxs-lookup"><span data-stu-id="d7edc-204">April 18, 2018</span></span> |--- |
| [<span data-ttu-id="d7edc-205">1.3.1</span><span class="sxs-lookup"><span data-stu-id="d7edc-205">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="d7edc-206">March 13, 2018</span><span class="sxs-lookup"><span data-stu-id="d7edc-206">March 13, 2018</span></span> |--- |
| [<span data-ttu-id="d7edc-207">1.2.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-207">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="d7edc-208">October 31, 2017</span><span class="sxs-lookup"><span data-stu-id="d7edc-208">October 31, 2017</span></span> |--- |
| [<span data-ttu-id="d7edc-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="d7edc-209">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="d7edc-210">August 29, 2017</span><span class="sxs-lookup"><span data-stu-id="d7edc-210">August 29, 2017</span></span> |--- |
| [<span data-ttu-id="d7edc-211">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-211">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="d7edc-212">August 13, 2017</span><span class="sxs-lookup"><span data-stu-id="d7edc-212">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="d7edc-213">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d7edc-213">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="d7edc-214">July 07, 2017</span><span class="sxs-lookup"><span data-stu-id="d7edc-214">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="d7edc-215">FAQ</span><span class="sxs-lookup"><span data-stu-id="d7edc-215">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="d7edc-216">See also</span><span class="sxs-lookup"><span data-stu-id="d7edc-216">See also</span></span>
<span data-ttu-id="d7edc-217">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="d7edc-217">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

