---
title: Azure DocumentDB Python API, SDK & Resources | Microsoft Docs
description: Learn all about the Python API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB Python SDK.
services: documentdb
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 10/30/2016
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 84a04f71ffde07e9caa439c03b55920d0bb0ef16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554077"
---
# <a name="documentdb-python-sdk-release-notes-and-resources"></a><span data-ttu-id="fbaeb-103">DocumentDB Python SDK: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="fbaeb-103">DocumentDB Python SDK: Release notes and resources</span></span>
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

<tr><td><span data-ttu-id="fbaeb-112">**Download SDK**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-112">**Download SDK**</span></span></td><td>[<span data-ttu-id="fbaeb-113">PyPI</span><span class="sxs-lookup"><span data-stu-id="fbaeb-113">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="fbaeb-114">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-114">**API documentation**</span></span></td><td>[<span data-ttu-id="fbaeb-115">Python API reference documentation</span><span class="sxs-lookup"><span data-stu-id="fbaeb-115">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="fbaeb-116">**SDK installation instructions**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-116">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="fbaeb-117">Python SDK installation instructions</span><span class="sxs-lookup"><span data-stu-id="fbaeb-117">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="fbaeb-118">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-118">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="fbaeb-119">GitHub</span><span class="sxs-lookup"><span data-stu-id="fbaeb-119">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="fbaeb-120">**Get started**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-120">**Get started**</span></span></td><td>[<span data-ttu-id="fbaeb-121">Get started with the Python SDK</span><span class="sxs-lookup"><span data-stu-id="fbaeb-121">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="fbaeb-122">**Current supported platform**</span><span class="sxs-lookup"><span data-stu-id="fbaeb-122">**Current supported platform**</span></span></td><td><span data-ttu-id="fbaeb-123">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="fbaeb-123">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="fbaeb-124">Release notes</span><span class="sxs-lookup"><span data-stu-id="fbaeb-124">Release notes</span></span>
### <a name="a-name201201"></a><span data-ttu-id="fbaeb-125"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-125"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="fbaeb-126">Made editorial changes to documentation comments.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-126">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="fbaeb-127"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-127"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="fbaeb-128">Added support for Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-128">Added support for Python 3.5.</span></span>
* <span data-ttu-id="fbaeb-129">Added support for connection pooling using a requests module.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-129">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="fbaeb-130">Added support for session consistency.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-130">Added support for session consistency.</span></span>
* <span data-ttu-id="fbaeb-131">Added support for TOP/ORDERBY queries for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-131">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="fbaeb-132"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-132"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="fbaeb-133">Added retry policy support for throttled requests.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-133">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="fbaeb-134">(Throttled requests receive a request rate too large exception, error code 429.) By default, DocumentDB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-134">(Throttled requests receive a request rate too large exception, error code 429.) By default, DocumentDB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="fbaeb-135">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-135">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="fbaeb-136">DocumentDB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-136">DocumentDB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="fbaeb-137">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-137">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="fbaeb-138">DocumentDB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-138">DocumentDB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="fbaeb-139">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-139">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="fbaeb-140"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-140"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="fbaeb-141">Added the support for multi-region database accounts.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-141">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="fbaeb-142"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-142"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="fbaeb-143">Added the support for Time To Live(TTL) feature for documents.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-143">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="fbaeb-144"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-144"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="fbaeb-145">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-145">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="fbaeb-146"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-146"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="fbaeb-147">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fbaeb-147">Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="fbaeb-148"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-148"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="fbaeb-149">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-149">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="fbaeb-150"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="fbaeb-150"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="fbaeb-151">Implement Upsert.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-151">Implement Upsert.</span></span> <span data-ttu-id="fbaeb-152">New UpsertXXX methods added to support Upsert feature.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-152">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="fbaeb-153">Implement ID Based Routing.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-153">Implement ID Based Routing.</span></span> <span data-ttu-id="fbaeb-154">No public API changes, all changes internal.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-154">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="fbaeb-155"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-155"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="fbaeb-156">Supports GeoSpatial index.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-156">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="fbaeb-157">Validates id property for all resources.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-157">Validates id property for all resources.</span></span> <span data-ttu-id="fbaeb-158">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-158">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="fbaeb-159">Adds new header "index transformation progress" to ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-159">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="fbaeb-160"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-160"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="fbaeb-161">Implements V2 indexing policy.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-161">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="fbaeb-162"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-162"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="fbaeb-163">Supports proxy connection.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-163">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="fbaeb-164"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-164"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="fbaeb-165">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-165">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="fbaeb-166">Release & retirement dates</span><span class="sxs-lookup"><span data-stu-id="fbaeb-166">Release & retirement dates</span></span>
<span data-ttu-id="fbaeb-167">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-167">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="fbaeb-168">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-168">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="fbaeb-169">Any request to DocumentDB using a retired SDK will be rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-169">Any request to DocumentDB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**. 
> 
> 

<br/>

| <span data-ttu-id="fbaeb-171">Version</span><span class="sxs-lookup"><span data-stu-id="fbaeb-171">Version</span></span> | <span data-ttu-id="fbaeb-172">Release Date</span><span class="sxs-lookup"><span data-stu-id="fbaeb-172">Release Date</span></span> | <span data-ttu-id="fbaeb-173">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="fbaeb-173">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="fbaeb-174">2.0.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-174">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="fbaeb-175">October 30, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-175">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-176">2.0.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-176">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="fbaeb-177">September 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-177">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-178">1.9.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-178">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="fbaeb-179">July 07, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-179">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-180">1.8.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-180">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="fbaeb-181">June 14, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-181">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-182">1.7.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-182">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="fbaeb-183">April 26, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-183">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-184">1.6.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-184">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="fbaeb-185">April 08, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-185">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-186">1.6.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-186">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="fbaeb-187">March 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-187">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-188">1.5.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-188">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="fbaeb-189">January 03, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-189">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="fbaeb-190">1.4.2</span><span class="sxs-lookup"><span data-stu-id="fbaeb-190">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="fbaeb-191">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-191">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="fbaeb-192">1.4.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-192">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="fbaeb-193">October 06, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-193">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="fbaeb-194">1.2.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-194">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="fbaeb-195">August 06, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-195">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="fbaeb-196">1.1.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-196">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="fbaeb-197">July 09, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-197">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="fbaeb-198">1.0.1</span><span class="sxs-lookup"><span data-stu-id="fbaeb-198">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="fbaeb-199">May 25, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-199">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="fbaeb-200">1.0.0</span><span class="sxs-lookup"><span data-stu-id="fbaeb-200">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="fbaeb-201">April 07, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-201">April 07, 2015</span></span> |--- |
| <span data-ttu-id="fbaeb-202">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="fbaeb-202">0.9.4-prelease</span></span> |<span data-ttu-id="fbaeb-203">January 14, 2015</span><span class="sxs-lookup"><span data-stu-id="fbaeb-203">January 14, 2015</span></span> |<span data-ttu-id="fbaeb-204">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-204">February 29, 2016</span></span> |
| <span data-ttu-id="fbaeb-205">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="fbaeb-205">0.9.3-prelease</span></span> |<span data-ttu-id="fbaeb-206">December 09, 2014</span><span class="sxs-lookup"><span data-stu-id="fbaeb-206">December 09, 2014</span></span> |<span data-ttu-id="fbaeb-207">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-207">February 29, 2016</span></span> |
| <span data-ttu-id="fbaeb-208">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="fbaeb-208">0.9.2-prelease</span></span> |<span data-ttu-id="fbaeb-209">November 25, 2014</span><span class="sxs-lookup"><span data-stu-id="fbaeb-209">November 25, 2014</span></span> |<span data-ttu-id="fbaeb-210">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-210">February 29, 2016</span></span> |
| <span data-ttu-id="fbaeb-211">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="fbaeb-211">0.9.1-prelease</span></span> |<span data-ttu-id="fbaeb-212">September 23, 2014</span><span class="sxs-lookup"><span data-stu-id="fbaeb-212">September 23, 2014</span></span> |<span data-ttu-id="fbaeb-213">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-213">February 29, 2016</span></span> |
| <span data-ttu-id="fbaeb-214">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="fbaeb-214">0.9.0-prelease</span></span> |<span data-ttu-id="fbaeb-215">August 21, 2014</span><span class="sxs-lookup"><span data-stu-id="fbaeb-215">August 21, 2014</span></span> |<span data-ttu-id="fbaeb-216">February 29, 2016</span><span class="sxs-lookup"><span data-stu-id="fbaeb-216">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="fbaeb-217">FAQ</span><span class="sxs-lookup"><span data-stu-id="fbaeb-217">FAQ</span></span>
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="fbaeb-218">See also</span><span class="sxs-lookup"><span data-stu-id="fbaeb-218">See also</span></span>
<span data-ttu-id="fbaeb-219">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span><span class="sxs-lookup"><span data-stu-id="fbaeb-219">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span></span> 

