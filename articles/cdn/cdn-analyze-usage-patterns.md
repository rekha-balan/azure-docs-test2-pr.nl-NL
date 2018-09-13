---
title: Analyze Azure CDN usage patterns | Microsoft Docs
description: 'You can view usage patterns for your CDN using the following reports: Bandwidth, Data Transferred, Hits, Cache Statuses, Cache Hit Ratio, IPV4/IPV6 Data Transferred.'
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 60f388877e4aae2051aef4426cffe71bf2e97c95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554199"
---
# <a name="analyze-azure-cdn-usage-patterns"></a><span data-ttu-id="37132-103">Analyze Azure CDN usage patterns</span><span class="sxs-lookup"><span data-stu-id="37132-103">Analyze Azure CDN usage patterns</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="37132-104">You can view usage patterns for your CDN using the following reports:</span><span class="sxs-lookup"><span data-stu-id="37132-104">You can view usage patterns for your CDN using the following reports:</span></span>

* <span data-ttu-id="37132-105">Bandwidth</span><span class="sxs-lookup"><span data-stu-id="37132-105">Bandwidth</span></span>
* <span data-ttu-id="37132-106">Data Transferred</span><span class="sxs-lookup"><span data-stu-id="37132-106">Data Transferred</span></span>
* <span data-ttu-id="37132-107">Hits</span><span class="sxs-lookup"><span data-stu-id="37132-107">Hits</span></span>
* <span data-ttu-id="37132-108">Cache Statuses</span><span class="sxs-lookup"><span data-stu-id="37132-108">Cache Statuses</span></span>
* <span data-ttu-id="37132-109">Cache Hit Ratio</span><span class="sxs-lookup"><span data-stu-id="37132-109">Cache Hit Ratio</span></span>
* <span data-ttu-id="37132-110">IPV4/IPV6 Data Transferred</span><span class="sxs-lookup"><span data-stu-id="37132-110">IPV4/IPV6 Data Transferred</span></span>

## <a name="accessing-advanced-http-reports"></a><span data-ttu-id="37132-111">Accessing advanced HTTP reports</span><span class="sxs-lookup"><span data-stu-id="37132-111">Accessing advanced HTTP reports</span></span>
1. <span data-ttu-id="37132-112">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="37132-112">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-manage-btn.png)
   
    <span data-ttu-id="37132-114">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="37132-114">The CDN management portal opens.</span></span>
2. <span data-ttu-id="37132-115">Hover over the **Analytics** tab, then hover over the **Core Reports** flyout.</span><span class="sxs-lookup"><span data-stu-id="37132-115">Hover over the **Analytics** tab, then hover over the **Core Reports** flyout.</span></span>  <span data-ttu-id="37132-116">Click on the desired report in the menu.</span><span class="sxs-lookup"><span data-stu-id="37132-116">Click on the desired report in the menu.</span></span>
   
    ![CDN management portal - Core Reports menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a><span data-ttu-id="37132-118">Bandwidth</span><span class="sxs-lookup"><span data-stu-id="37132-118">Bandwidth</span></span>
<span data-ttu-id="37132-119">The bandwidth report consists of a graph and data table indicating the bandwidth usage for HTTP and HTTPS over a particular time period.</span><span class="sxs-lookup"><span data-stu-id="37132-119">The bandwidth report consists of a graph and data table indicating the bandwidth usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="37132-120">You can view the bandwidth usage across all CDN POPs or a particular POP.</span><span class="sxs-lookup"><span data-stu-id="37132-120">You can view the bandwidth usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="37132-121">This allows you to view the traffic spikes and distribution across CDN POPs in Mbps.</span><span class="sxs-lookup"><span data-stu-id="37132-121">This allows you to view the traffic spikes and distribution across CDN POPs in Mbps.</span></span>

* <span data-ttu-id="37132-122">Select All Edge Nodes to see traffic from all nodes or choose a specific region/node from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="37132-122">Select All Edge Nodes to see traffic from all nodes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="37132-123">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-123">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="37132-124">You can export and download the data by clicking the excel sheet icon located next to "go".</span><span class="sxs-lookup"><span data-stu-id="37132-124">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

<span data-ttu-id="37132-125">The report is updated every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="37132-125">The report is updated every 5 minutes.</span></span>

![Bandwidth report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a><span data-ttu-id="37132-127">Data transferred</span><span class="sxs-lookup"><span data-stu-id="37132-127">Data transferred</span></span>
<span data-ttu-id="37132-128">This report consists of a graph and data table indicating the traffic usage for HTTP and HTTPS over a particular time period.</span><span class="sxs-lookup"><span data-stu-id="37132-128">This report consists of a graph and data table indicating the traffic usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="37132-129">You can view the traffic usage across all CDN POPs or a particular POP.</span><span class="sxs-lookup"><span data-stu-id="37132-129">You can view the traffic usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="37132-130">This allows you to view the traffic spikes and distribution across CDN POPs in GB.</span><span class="sxs-lookup"><span data-stu-id="37132-130">This allows you to view the traffic spikes and distribution across CDN POPs in GB.</span></span>

* <span data-ttu-id="37132-131">Select All Edge Nodes to see traffic from all notes or choose a specific region/node from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="37132-131">Select All Edge Nodes to see traffic from all notes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="37132-132">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-132">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="37132-133">You can export and download the data by clicking the excel sheet icon located next to "go" .</span><span class="sxs-lookup"><span data-stu-id="37132-133">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

<span data-ttu-id="37132-134">The report is updated every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="37132-134">The report is updated every 5 minutes.</span></span>

![Data transferred report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a><span data-ttu-id="37132-136">Hits (status codes)</span><span class="sxs-lookup"><span data-stu-id="37132-136">Hits (status codes)</span></span>
<span data-ttu-id="37132-137">This report describes the distribution of request status codes for your content.</span><span class="sxs-lookup"><span data-stu-id="37132-137">This report describes the distribution of request status codes for your content.</span></span> <span data-ttu-id="37132-138">Every request for content will generate an HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="37132-138">Every request for content will generate an HTTP status code.</span></span> <span data-ttu-id="37132-139">The status code describes how edge POPs handled the request.</span><span class="sxs-lookup"><span data-stu-id="37132-139">The status code describes how edge POPs handled the request.</span></span> <span data-ttu-id="37132-140">For example, 2xx status codes indicate that the request was successfully served to a client, while a 4xx status code indicates an error occurred.</span><span class="sxs-lookup"><span data-stu-id="37132-140">For example, 2xx status codes indicate that the request was successfully served to a client, while a 4xx status code indicates an error occurred.</span></span> <span data-ttu-id="37132-141">For more details about HTTP status code, see [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).</span><span class="sxs-lookup"><span data-stu-id="37132-141">For more details about HTTP status code, see [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).</span></span>

* <span data-ttu-id="37132-142">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-142">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="37132-143">You can export and download the data by clicking the excel sheet located next to "go".</span><span class="sxs-lookup"><span data-stu-id="37132-143">You can export and download the data by clicking the excel sheet located next to "go".</span></span>

![Hits report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a><span data-ttu-id="37132-145">Cache statuses</span><span class="sxs-lookup"><span data-stu-id="37132-145">Cache statuses</span></span>
<span data-ttu-id="37132-146">This report describes the distribution of cache hits and cache misses for client request.</span><span class="sxs-lookup"><span data-stu-id="37132-146">This report describes the distribution of cache hits and cache misses for client request.</span></span> <span data-ttu-id="37132-147">Since the fastest performance comes from cache hits, you can optimize data delivery speeds by minimizing cache misses and expired cache hits.</span><span class="sxs-lookup"><span data-stu-id="37132-147">Since the fastest performance comes from cache hits, you can optimize data delivery speeds by minimizing cache misses and expired cache hits.</span></span> <span data-ttu-id="37132-148">Cache misses can be reduced by configuring your origin server to avoid assigning "no-cache" response headers, by avoiding query-string caching except where strictly needed, and by avoiding non-cacheable response codes.</span><span class="sxs-lookup"><span data-stu-id="37132-148">Cache misses can be reduced by configuring your origin server to avoid assigning "no-cache" response headers, by avoiding query-string caching except where strictly needed, and by avoiding non-cacheable response codes.</span></span> <span data-ttu-id="37132-149">Expired cache hits can be avoided by making an asset's max-age as long as possible to minimize the number of requests to the origin server.</span><span class="sxs-lookup"><span data-stu-id="37132-149">Expired cache hits can be avoided by making an asset's max-age as long as possible to minimize the number of requests to the origin server.</span></span>

![Cache statuses report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a><span data-ttu-id="37132-151">Main cache statuses include:</span><span class="sxs-lookup"><span data-stu-id="37132-151">Main cache statuses include:</span></span>
* <span data-ttu-id="37132-152">TCP_HIT: Served from Edge.</span><span class="sxs-lookup"><span data-stu-id="37132-152">TCP_HIT: Served from Edge.</span></span> <span data-ttu-id="37132-153">The object was in cache and had not exceeded its max-age.</span><span class="sxs-lookup"><span data-stu-id="37132-153">The object was in cache and had not exceeded its max-age.</span></span>
* <span data-ttu-id="37132-154">TCP_MISS: Served from Origin.</span><span class="sxs-lookup"><span data-stu-id="37132-154">TCP_MISS: Served from Origin.</span></span> <span data-ttu-id="37132-155">The object was not in cache and the response was back to origin.</span><span class="sxs-lookup"><span data-stu-id="37132-155">The object was not in cache and the response was back to origin.</span></span>
* <span data-ttu-id="37132-156">TCP_EXPIRED _MISS: Served from origin after revalidation with origin.</span><span class="sxs-lookup"><span data-stu-id="37132-156">TCP_EXPIRED _MISS: Served from origin after revalidation with origin.</span></span> <span data-ttu-id="37132-157">The object was in cache but had exceeded its max-age.</span><span class="sxs-lookup"><span data-stu-id="37132-157">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="37132-158">A revalidation with origin resulted in the cache object being replaced by a new response from origin.</span><span class="sxs-lookup"><span data-stu-id="37132-158">A revalidation with origin resulted in the cache object being replaced by a new response from origin.</span></span>
* <span data-ttu-id="37132-159">TCP_EXPIRED _HIT: Served from Edge after revalidation with origin.</span><span class="sxs-lookup"><span data-stu-id="37132-159">TCP_EXPIRED _HIT: Served from Edge after revalidation with origin.</span></span> <span data-ttu-id="37132-160">The object was in cache but had exceeded its max-age.</span><span class="sxs-lookup"><span data-stu-id="37132-160">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="37132-161">A revalidation with the origin server resulted in the cache object being unmodified.</span><span class="sxs-lookup"><span data-stu-id="37132-161">A revalidation with the origin server resulted in the cache object being unmodified.</span></span>
* <span data-ttu-id="37132-162">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-162">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="37132-163">You can export and download the data by clicking the excel sheet icon located next to "go".</span><span class="sxs-lookup"><span data-stu-id="37132-163">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

### <a name="full-list-of-cache-statuses"></a><span data-ttu-id="37132-164">Full list of cache statuses</span><span class="sxs-lookup"><span data-stu-id="37132-164">Full list of cache statuses</span></span>
* <span data-ttu-id="37132-165">TCP_HIT - This status is reported when a request is served directly from the POP to the client.</span><span class="sxs-lookup"><span data-stu-id="37132-165">TCP_HIT - This status is reported when a request is served directly from the POP to the client.</span></span> <span data-ttu-id="37132-166">An asset is immediately served from a POP when it is cached on the POP closest to the client and it has a valid time-to-live, or TTL.</span><span class="sxs-lookup"><span data-stu-id="37132-166">An asset is immediately served from a POP when it is cached on the POP closest to the client and it has a valid time-to-live, or TTL.</span></span> <span data-ttu-id="37132-167">TTL is determined by the following response headers:</span><span class="sxs-lookup"><span data-stu-id="37132-167">TTL is determined by the following response headers:</span></span>
  
  * <span data-ttu-id="37132-168">Cache-Control: s-maxage</span><span class="sxs-lookup"><span data-stu-id="37132-168">Cache-Control: s-maxage</span></span>
  * <span data-ttu-id="37132-169">Cache-Control: max-age</span><span class="sxs-lookup"><span data-stu-id="37132-169">Cache-Control: max-age</span></span>
  * <span data-ttu-id="37132-170">Expires</span><span class="sxs-lookup"><span data-stu-id="37132-170">Expires</span></span>
* <span data-ttu-id="37132-171">TCP_MISS - This status indicates that a cached version of the requested asset was not found on the POP closest to the client.</span><span class="sxs-lookup"><span data-stu-id="37132-171">TCP_MISS - This status indicates that a cached version of the requested asset was not found on the POP closest to the client.</span></span> <span data-ttu-id="37132-172">The asset will be requested from either an origin server or an origin shield server.</span><span class="sxs-lookup"><span data-stu-id="37132-172">The asset will be requested from either an origin server or an origin shield server.</span></span> <span data-ttu-id="37132-173">If the origin server or the origin shield server returns an asset, it will be served to the client and cached on both the client and the edge server.</span><span class="sxs-lookup"><span data-stu-id="37132-173">If the origin server or the origin shield server returns an asset, it will be served to the client and cached on both the client and the edge server.</span></span> <span data-ttu-id="37132-174">Otherwise, a non-200 status code (e.g., 403 Forbidden, 404 Not Found, etc.) will be returned.</span><span class="sxs-lookup"><span data-stu-id="37132-174">Otherwise, a non-200 status code (e.g., 403 Forbidden, 404 Not Found, etc.) will be returned.</span></span>
* <span data-ttu-id="37132-175">TCP_EXPIRED _HIT -  This status is reported when a request that targeted an asset with an expired TTL, such as when the asset's max-age has expired, was served directly from the POP to the client.</span><span class="sxs-lookup"><span data-stu-id="37132-175">TCP_EXPIRED _HIT -  This status is reported when a request that targeted an asset with an expired TTL, such as when the asset's max-age has expired, was served directly from the POP to the client.</span></span>
  
    <span data-ttu-id="37132-176">An expired request typically results in a revalidation request to the origin server.</span><span class="sxs-lookup"><span data-stu-id="37132-176">An expired request typically results in a revalidation request to the origin server.</span></span> <span data-ttu-id="37132-177">In order for a TCP_EXPIRED _HIT to occur, the origin server must indicate that a newer version of the asset does not exist.</span><span class="sxs-lookup"><span data-stu-id="37132-177">In order for a TCP_EXPIRED _HIT to occur, the origin server must indicate that a newer version of the asset does not exist.</span></span> <span data-ttu-id="37132-178">This type of situation will typically update that asset's Cache-Control and Expires headers.</span><span class="sxs-lookup"><span data-stu-id="37132-178">This type of situation will typically update that asset's Cache-Control and Expires headers.</span></span>
* <span data-ttu-id="37132-179">TCP_EXPIRED _MISS - This status is reported when a newer version of an expired cached asset is served from the POP to the client.</span><span class="sxs-lookup"><span data-stu-id="37132-179">TCP_EXPIRED _MISS - This status is reported when a newer version of an expired cached asset is served from the POP to the client.</span></span> <span data-ttu-id="37132-180">This occurs when the TTL for a cached asset has expired (e.g., expired max-age) and the origin server returns a newer version of that asset.</span><span class="sxs-lookup"><span data-stu-id="37132-180">This occurs when the TTL for a cached asset has expired (e.g., expired max-age) and the origin server returns a newer version of that asset.</span></span> <span data-ttu-id="37132-181">This new version of the asset will be served to the client instead of the cached version.</span><span class="sxs-lookup"><span data-stu-id="37132-181">This new version of the asset will be served to the client instead of the cached version.</span></span> <span data-ttu-id="37132-182">Additionally, it will be cached on the edge server and the client.</span><span class="sxs-lookup"><span data-stu-id="37132-182">Additionally, it will be cached on the edge server and the client.</span></span>
* <span data-ttu-id="37132-183">CONFIG_NOCACHE - This status indicates that a customer-specific configuration on our edge POP prevented the asset from being cached.</span><span class="sxs-lookup"><span data-stu-id="37132-183">CONFIG_NOCACHE - This status indicates that a customer-specific configuration on our edge POP prevented the asset from being cached.</span></span>
* <span data-ttu-id="37132-184">NONE - This status indicates that a cache content freshness check was not performed.</span><span class="sxs-lookup"><span data-stu-id="37132-184">NONE - This status indicates that a cache content freshness check was not performed.</span></span>
* <span data-ttu-id="37132-185">TCP_ CLIENT_REFRESH _MISS - This status is reported when an HTTP client (e.g., browser) forces an edge POP to retrieve a new version of a stale asset from the origin server.</span><span class="sxs-lookup"><span data-stu-id="37132-185">TCP_ CLIENT_REFRESH _MISS - This status is reported when an HTTP client (e.g., browser) forces an edge POP to retrieve a new version of a stale asset from the origin server.</span></span>
  
    <span data-ttu-id="37132-186">By default, our servers prevent an HTTP client from forcing our edge servers to retrieve a new version of the asset from the origin server.</span><span class="sxs-lookup"><span data-stu-id="37132-186">By default, our servers prevent an HTTP client from forcing our edge servers to retrieve a new version of the asset from the origin server.</span></span>
* <span data-ttu-id="37132-187">TCP_ PARTIAL_HIT - This status is reported when a byte range request results in a hit for a partially cached asset.</span><span class="sxs-lookup"><span data-stu-id="37132-187">TCP_ PARTIAL_HIT - This status is reported when a byte range request results in a hit for a partially cached asset.</span></span> <span data-ttu-id="37132-188">The requested byte range is immediately served from the POP to the client.</span><span class="sxs-lookup"><span data-stu-id="37132-188">The requested byte range is immediately served from the POP to the client.</span></span>
* <span data-ttu-id="37132-189">UNCACHEABLE - This status is reported when an asset's Cache-Control and Expires headers indicate that it should not be cached on a POP or by the HTTP client.</span><span class="sxs-lookup"><span data-stu-id="37132-189">UNCACHEABLE - This status is reported when an asset's Cache-Control and Expires headers indicate that it should not be cached on a POP or by the HTTP client.</span></span> <span data-ttu-id="37132-190">These types of requests are served from the origin server</span><span class="sxs-lookup"><span data-stu-id="37132-190">These types of requests are served from the origin server</span></span>

## <a name="cache-hit-ratio"></a><span data-ttu-id="37132-191">Cache Hit Ratio</span><span class="sxs-lookup"><span data-stu-id="37132-191">Cache Hit Ratio</span></span>
<span data-ttu-id="37132-192">This report indicates the percentage of cached requests that were served directly from cache.</span><span class="sxs-lookup"><span data-stu-id="37132-192">This report indicates the percentage of cached requests that were served directly from cache.</span></span>

<span data-ttu-id="37132-193">The report provides the following details:</span><span class="sxs-lookup"><span data-stu-id="37132-193">The report provides the following details:</span></span>

* <span data-ttu-id="37132-194">The requested content was cached on the POP closest to the requester.</span><span class="sxs-lookup"><span data-stu-id="37132-194">The requested content was cached on the POP closest to the requester.</span></span>
* <span data-ttu-id="37132-195">The request was served directly from the edge of our network.</span><span class="sxs-lookup"><span data-stu-id="37132-195">The request was served directly from the edge of our network.</span></span>
* <span data-ttu-id="37132-196">The request did not require revalidation with the origin server.</span><span class="sxs-lookup"><span data-stu-id="37132-196">The request did not require revalidation with the origin server.</span></span>

<span data-ttu-id="37132-197">The report doesn't include:</span><span class="sxs-lookup"><span data-stu-id="37132-197">The report doesn't include:</span></span>

* <span data-ttu-id="37132-198">Requests that are denied due to country filtering options.</span><span class="sxs-lookup"><span data-stu-id="37132-198">Requests that are denied due to country filtering options.</span></span>
* <span data-ttu-id="37132-199">Requests for assets whose headers indicate that they should not be cached.</span><span class="sxs-lookup"><span data-stu-id="37132-199">Requests for assets whose headers indicate that they should not be cached.</span></span> <span data-ttu-id="37132-200">For example, Cache-Control: private, Cache-Control: no-cache, or Pragma: no-cache headers will prevent an asset from being cached.</span><span class="sxs-lookup"><span data-stu-id="37132-200">For example, Cache-Control: private, Cache-Control: no-cache, or Pragma: no-cache headers will prevent an asset from being cached.</span></span>
* <span data-ttu-id="37132-201">Byte range requests for partially cached content.</span><span class="sxs-lookup"><span data-stu-id="37132-201">Byte range requests for partially cached content.</span></span>

<span data-ttu-id="37132-202">The formula is: (TCP_ HIT/(TCP_ HIT+TCP_MISS))\*100</span><span class="sxs-lookup"><span data-stu-id="37132-202">The formula is: (TCP_ HIT/(TCP_ HIT+TCP_MISS))\*100</span></span>

* <span data-ttu-id="37132-203">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-203">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="37132-204">You can export and download the data by clicking the excel sheet icon located next to "go" .</span><span class="sxs-lookup"><span data-stu-id="37132-204">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

![Cache hit ratio report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a><span data-ttu-id="37132-206">IPV4/IPV6 Data transferred</span><span class="sxs-lookup"><span data-stu-id="37132-206">IPV4/IPV6 Data transferred</span></span>
<span data-ttu-id="37132-207">This report shows the traffic usage distribution in IPV4 vs IPV6.</span><span class="sxs-lookup"><span data-stu-id="37132-207">This report shows the traffic usage distribution in IPV4 vs IPV6.</span></span>

![IPV4/IPV6 Data transferred](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-reports/cdn-ipv4-ipv6.png)

* <span data-ttu-id="37132-209">Select Date range to view data for today/this week/this month, etc. or enter custom dates.</span><span class="sxs-lookup"><span data-stu-id="37132-209">Select Date range to view data for today/this week/this month, etc. or enter custom dates.</span></span>
* <span data-ttu-id="37132-210">Then, click "go" to make sure your selection is updated.</span><span class="sxs-lookup"><span data-stu-id="37132-210">Then, click "go" to make sure your selection is updated.</span></span>

## <a name="considerations"></a><span data-ttu-id="37132-211">Considerations</span><span class="sxs-lookup"><span data-stu-id="37132-211">Considerations</span></span>
<span data-ttu-id="37132-212">Reports can only be generated within the last 18 months.</span><span class="sxs-lookup"><span data-stu-id="37132-212">Reports can only be generated within the last 18 months.</span></span>









