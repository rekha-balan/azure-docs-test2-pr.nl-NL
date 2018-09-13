---
title: X-EC-Debug HTTP headers for Azure CDN rules engine | Microsoft Docs
description: The X-EC-Debug debug cache request header provides additional information about the cache policy that is applied to the requested asset. These headers are specific to Verizon.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2018
ms.author: v-deasim
ms.openlocfilehash: 3a99e322d81748c54585e7dd0eb06959bfeb9569
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866937"
---
# <a name="x-ec-debug-http-headers-for-azure-cdn-rules-engine"></a><span data-ttu-id="17323-104">X-EC-Debug HTTP headers for Azure CDN rules engine</span><span class="sxs-lookup"><span data-stu-id="17323-104">X-EC-Debug HTTP headers for Azure CDN rules engine</span></span>
<span data-ttu-id="17323-105">The debug cache request header, `X-EC-Debug`, provides additional information about the cache policy that is applied to the requested asset.</span><span class="sxs-lookup"><span data-stu-id="17323-105">The debug cache request header, `X-EC-Debug`, provides additional information about the cache policy that is applied to the requested asset.</span></span> <span data-ttu-id="17323-106">These headers are specific to **Azure CDN Premium from Verizon** products.</span><span class="sxs-lookup"><span data-stu-id="17323-106">These headers are specific to **Azure CDN Premium from Verizon** products.</span></span>

## <a name="usage"></a><span data-ttu-id="17323-107">Usage</span><span class="sxs-lookup"><span data-stu-id="17323-107">Usage</span></span>
<span data-ttu-id="17323-108">The response sent from the POP servers to a user includes the `X-EC-Debug` header only when the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="17323-108">The response sent from the POP servers to a user includes the `X-EC-Debug` header only when the following conditions are met:</span></span>

- <span data-ttu-id="17323-109">The [Debug Cache Response Headers feature](cdn-rules-engine-reference-features.md#debug-cache-response-headers) has been enabled on the rules engine for the specified request.</span><span class="sxs-lookup"><span data-stu-id="17323-109">The [Debug Cache Response Headers feature](cdn-rules-engine-reference-features.md#debug-cache-response-headers) has been enabled on the rules engine for the specified request.</span></span>
- <span data-ttu-id="17323-110">The specified request defines the set of debug cache response headers that will be included in the response.</span><span class="sxs-lookup"><span data-stu-id="17323-110">The specified request defines the set of debug cache response headers that will be included in the response.</span></span>

## <a name="requesting-debug-cache-information"></a><span data-ttu-id="17323-111">Requesting debug cache information</span><span class="sxs-lookup"><span data-stu-id="17323-111">Requesting debug cache information</span></span>
<span data-ttu-id="17323-112">Use the following directives in the specified request to define the debug cache information that will be included in the response:</span><span class="sxs-lookup"><span data-stu-id="17323-112">Use the following directives in the specified request to define the debug cache information that will be included in the response:</span></span>

<span data-ttu-id="17323-113">Request header</span><span class="sxs-lookup"><span data-stu-id="17323-113">Request header</span></span> | <span data-ttu-id="17323-114">Description</span><span class="sxs-lookup"><span data-stu-id="17323-114">Description</span></span> |
---------------|-------------|
<span data-ttu-id="17323-115">X-EC-Debug: x-ec-cache</span><span class="sxs-lookup"><span data-stu-id="17323-115">X-EC-Debug: x-ec-cache</span></span> | [<span data-ttu-id="17323-116">Cache status code</span><span class="sxs-lookup"><span data-stu-id="17323-116">Cache status code</span></span>](#cache-status-code-information)
<span data-ttu-id="17323-117">X-EC-Debug: x-ec-cache-remote</span><span class="sxs-lookup"><span data-stu-id="17323-117">X-EC-Debug: x-ec-cache-remote</span></span> | [<span data-ttu-id="17323-118">Cache status code</span><span class="sxs-lookup"><span data-stu-id="17323-118">Cache status code</span></span>](#cache-status-code-information)
<span data-ttu-id="17323-119">X-EC-Debug: x-ec-check-cacheable</span><span class="sxs-lookup"><span data-stu-id="17323-119">X-EC-Debug: x-ec-check-cacheable</span></span> | [<span data-ttu-id="17323-120">Cacheable</span><span class="sxs-lookup"><span data-stu-id="17323-120">Cacheable</span></span>](#cacheable-response-header)
<span data-ttu-id="17323-121">X-EC-Debug: x-ec-cache-key</span><span class="sxs-lookup"><span data-stu-id="17323-121">X-EC-Debug: x-ec-cache-key</span></span> | [<span data-ttu-id="17323-122">Cache-key</span><span class="sxs-lookup"><span data-stu-id="17323-122">Cache-key</span></span>](#cache-key-response-header)
<span data-ttu-id="17323-123">X-EC-Debug: x-ec-cache-state</span><span class="sxs-lookup"><span data-stu-id="17323-123">X-EC-Debug: x-ec-cache-state</span></span> | [<span data-ttu-id="17323-124">Cache state</span><span class="sxs-lookup"><span data-stu-id="17323-124">Cache state</span></span>](#cache-state-response-header)

### <a name="syntax"></a><span data-ttu-id="17323-125">Syntax</span><span class="sxs-lookup"><span data-stu-id="17323-125">Syntax</span></span>

<span data-ttu-id="17323-126">Debug cache response headers may be requested by including the following header and the specified directives in the request:</span><span class="sxs-lookup"><span data-stu-id="17323-126">Debug cache response headers may be requested by including the following header and the specified directives in the request:</span></span>

`X-EC-Debug: Directive1,Directive2,DirectiveN`

### <a name="sample-x-ec-debug-header"></a><span data-ttu-id="17323-127">Sample X-EC-Debug header</span><span class="sxs-lookup"><span data-stu-id="17323-127">Sample X-EC-Debug header</span></span>

`X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state`

## <a name="cache-status-code-information"></a><span data-ttu-id="17323-128">Cache status code information</span><span class="sxs-lookup"><span data-stu-id="17323-128">Cache status code information</span></span>
<span data-ttu-id="17323-129">The X-EC-Debug response header can identify a server and how it handled the response through the following directives:</span><span class="sxs-lookup"><span data-stu-id="17323-129">The X-EC-Debug response header can identify a server and how it handled the response through the following directives:</span></span>

<span data-ttu-id="17323-130">Header</span><span class="sxs-lookup"><span data-stu-id="17323-130">Header</span></span> | <span data-ttu-id="17323-131">Description</span><span class="sxs-lookup"><span data-stu-id="17323-131">Description</span></span>
-------|------------
<span data-ttu-id="17323-132">X-EC-Debug: x-ec-cache</span><span class="sxs-lookup"><span data-stu-id="17323-132">X-EC-Debug: x-ec-cache</span></span> | <span data-ttu-id="17323-133">This header is reported whenever content is routed through the CDN.</span><span class="sxs-lookup"><span data-stu-id="17323-133">This header is reported whenever content is routed through the CDN.</span></span> <span data-ttu-id="17323-134">It identifies the POP server that fulfilled the request.</span><span class="sxs-lookup"><span data-stu-id="17323-134">It identifies the POP server that fulfilled the request.</span></span>
<span data-ttu-id="17323-135">X-EC-Debug: x-ec-cache-remote</span><span class="sxs-lookup"><span data-stu-id="17323-135">X-EC-Debug: x-ec-cache-remote</span></span> | <span data-ttu-id="17323-136">This header is reported only when the requested content was cached on an origin shield server or an ADN gateway server.</span><span class="sxs-lookup"><span data-stu-id="17323-136">This header is reported only when the requested content was cached on an origin shield server or an ADN gateway server.</span></span>

### <a name="response-header-format"></a><span data-ttu-id="17323-137">Response header format</span><span class="sxs-lookup"><span data-stu-id="17323-137">Response header format</span></span>

<span data-ttu-id="17323-138">The X-EC-Debug header reports cache status code information in the following format:</span><span class="sxs-lookup"><span data-stu-id="17323-138">The X-EC-Debug header reports cache status code information in the following format:</span></span>

- `X-EC-Debug: x-ec-cache: <StatusCode from Platform (POP/ID)>`

- `X-EC-Debug: x-ec-cache-remote: <StatusCode from Platform (POP/ID)>`

<span data-ttu-id="17323-139">The terms used in the above response header syntax are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="17323-139">The terms used in the above response header syntax are defined as follows:</span></span>
- <span data-ttu-id="17323-140">StatusCode: Indicates how the requested content was handled by the CDN, which is represented through a cache status code.</span><span class="sxs-lookup"><span data-stu-id="17323-140">StatusCode: Indicates how the requested content was handled by the CDN, which is represented through a cache status code.</span></span>
    
    <span data-ttu-id="17323-141">The TCP_DENIED status code may be reported instead of NONE when an unauthorized request is denied due to Token-Based Authentication.</span><span class="sxs-lookup"><span data-stu-id="17323-141">The TCP_DENIED status code may be reported instead of NONE when an unauthorized request is denied due to Token-Based Authentication.</span></span> <span data-ttu-id="17323-142">However, the NONE status code will continue to be used when viewing Cache Status reports or raw log data.</span><span class="sxs-lookup"><span data-stu-id="17323-142">However, the NONE status code will continue to be used when viewing Cache Status reports or raw log data.</span></span>

- <span data-ttu-id="17323-143">Platform: Indicates the platform on which the content was requested.</span><span class="sxs-lookup"><span data-stu-id="17323-143">Platform: Indicates the platform on which the content was requested.</span></span> <span data-ttu-id="17323-144">The following codes are valid for this field:</span><span class="sxs-lookup"><span data-stu-id="17323-144">The following codes are valid for this field:</span></span>

    <span data-ttu-id="17323-145">Code</span><span class="sxs-lookup"><span data-stu-id="17323-145">Code</span></span>  | <span data-ttu-id="17323-146">Platform</span><span class="sxs-lookup"><span data-stu-id="17323-146">Platform</span></span>
    ------| --------
    <span data-ttu-id="17323-147">ECAcc</span><span class="sxs-lookup"><span data-stu-id="17323-147">ECAcc</span></span> | <span data-ttu-id="17323-148">HTTP Large</span><span class="sxs-lookup"><span data-stu-id="17323-148">HTTP Large</span></span>
    <span data-ttu-id="17323-149">ECS</span><span class="sxs-lookup"><span data-stu-id="17323-149">ECS</span></span>   | <span data-ttu-id="17323-150">HTTP Small</span><span class="sxs-lookup"><span data-stu-id="17323-150">HTTP Small</span></span>
    <span data-ttu-id="17323-151">ECD</span><span class="sxs-lookup"><span data-stu-id="17323-151">ECD</span></span>   | <span data-ttu-id="17323-152">Application Delivery Network (ADN)</span><span class="sxs-lookup"><span data-stu-id="17323-152">Application Delivery Network (ADN)</span></span>

- <span data-ttu-id="17323-153">POP: Indicates the [POP](cdn-pop-abbreviations.md) that handled the request.</span><span class="sxs-lookup"><span data-stu-id="17323-153">POP: Indicates the [POP](cdn-pop-abbreviations.md) that handled the request.</span></span> 

### <a name="sample-response-headers"></a><span data-ttu-id="17323-154">Sample response headers</span><span class="sxs-lookup"><span data-stu-id="17323-154">Sample response headers</span></span>

<span data-ttu-id="17323-155">The following sample headers provide cache status code information for a request:</span><span class="sxs-lookup"><span data-stu-id="17323-155">The following sample headers provide cache status code information for a request:</span></span>

- `X-EC-Debug: x-ec-cache: TCP_HIT from ECD (lga/0FE8)`

- `X-EC-Debug: x-ec-cache-remote: TCP_HIT from ECD (dca/EF00)`

## <a name="cacheable-response-header"></a><span data-ttu-id="17323-156">Cacheable response header</span><span class="sxs-lookup"><span data-stu-id="17323-156">Cacheable response header</span></span>
<span data-ttu-id="17323-157">The `X-EC-Debug: x-ec-check-cacheable` response header indicates whether the requested content could have been cached.</span><span class="sxs-lookup"><span data-stu-id="17323-157">The `X-EC-Debug: x-ec-check-cacheable` response header indicates whether the requested content could have been cached.</span></span>

<span data-ttu-id="17323-158">This response header does not indicate whether caching took place.</span><span class="sxs-lookup"><span data-stu-id="17323-158">This response header does not indicate whether caching took place.</span></span> <span data-ttu-id="17323-159">Rather, it indicates whether the request was eligible for caching.</span><span class="sxs-lookup"><span data-stu-id="17323-159">Rather, it indicates whether the request was eligible for caching.</span></span>

### <a name="response-header-format"></a><span data-ttu-id="17323-160">Response header format</span><span class="sxs-lookup"><span data-stu-id="17323-160">Response header format</span></span>

<span data-ttu-id="17323-161">The `X-EC-Debug` response header reporting whether a request could have been cached is in the following format:</span><span class="sxs-lookup"><span data-stu-id="17323-161">The `X-EC-Debug` response header reporting whether a request could have been cached is in the following format:</span></span>

`X-EC-Debug: x-ec-check-cacheable: <cacheable status>`

<span data-ttu-id="17323-162">The term used in the above response header syntax is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="17323-162">The term used in the above response header syntax is defined as follows:</span></span>

<span data-ttu-id="17323-163">Value</span><span class="sxs-lookup"><span data-stu-id="17323-163">Value</span></span>  | <span data-ttu-id="17323-164">Description</span><span class="sxs-lookup"><span data-stu-id="17323-164">Description</span></span>
-------| --------
<span data-ttu-id="17323-165">YES</span><span class="sxs-lookup"><span data-stu-id="17323-165">YES</span></span>    | <span data-ttu-id="17323-166">Indicates that the requested content was eligible for caching.</span><span class="sxs-lookup"><span data-stu-id="17323-166">Indicates that the requested content was eligible for caching.</span></span>
<span data-ttu-id="17323-167">NO</span><span class="sxs-lookup"><span data-stu-id="17323-167">NO</span></span>     | <span data-ttu-id="17323-168">Indicates that the requested content was ineligible for caching.</span><span class="sxs-lookup"><span data-stu-id="17323-168">Indicates that the requested content was ineligible for caching.</span></span> <span data-ttu-id="17323-169">This status may be due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="17323-169">This status may be due to one of the following reasons:</span></span> <br /> <span data-ttu-id="17323-170">- Customer-Specific Configuration: A configuration specific to your account can prevent the pop servers from caching an asset.</span><span class="sxs-lookup"><span data-stu-id="17323-170">- Customer-Specific Configuration: A configuration specific to your account can prevent the pop servers from caching an asset.</span></span> <span data-ttu-id="17323-171">For example, Rules Engine can prevent an asset from being cached by enabling the Bypass Cache feature for qualifying requests.</span><span class="sxs-lookup"><span data-stu-id="17323-171">For example, Rules Engine can prevent an asset from being cached by enabling the Bypass Cache feature for qualifying requests.</span></span><br /> <span data-ttu-id="17323-172">- Cache Response Headers: The requested asset's Cache-Control and Expires headers can prevent the POP servers from caching it.</span><span class="sxs-lookup"><span data-stu-id="17323-172">- Cache Response Headers: The requested asset's Cache-Control and Expires headers can prevent the POP servers from caching it.</span></span>
<span data-ttu-id="17323-173">UNKNOWN</span><span class="sxs-lookup"><span data-stu-id="17323-173">UNKNOWN</span></span> | <span data-ttu-id="17323-174">Indicates that the servers were unable to assess whether the requested asset was cacheable.</span><span class="sxs-lookup"><span data-stu-id="17323-174">Indicates that the servers were unable to assess whether the requested asset was cacheable.</span></span> <span data-ttu-id="17323-175">This status typically occurs when the request is denied due to token-based authentication.</span><span class="sxs-lookup"><span data-stu-id="17323-175">This status typically occurs when the request is denied due to token-based authentication.</span></span>

### <a name="sample-response-header"></a><span data-ttu-id="17323-176">Sample response header</span><span class="sxs-lookup"><span data-stu-id="17323-176">Sample response header</span></span>

<span data-ttu-id="17323-177">The following sample response header indicates whether the requested content could have been cached:</span><span class="sxs-lookup"><span data-stu-id="17323-177">The following sample response header indicates whether the requested content could have been cached:</span></span>

`X-EC-Debug: x-ec-check-cacheable: YES`

## <a name="cache-key-response-header"></a><span data-ttu-id="17323-178">Cache-Key response header</span><span class="sxs-lookup"><span data-stu-id="17323-178">Cache-Key response header</span></span>
<span data-ttu-id="17323-179">The `X-EC-Debug: x-ec-cache-key` response header indicates the physical cache-key associated with the requested content.</span><span class="sxs-lookup"><span data-stu-id="17323-179">The `X-EC-Debug: x-ec-cache-key` response header indicates the physical cache-key associated with the requested content.</span></span> <span data-ttu-id="17323-180">A physical cache-key consists of a path that identifies an asset for the purposes of caching.</span><span class="sxs-lookup"><span data-stu-id="17323-180">A physical cache-key consists of a path that identifies an asset for the purposes of caching.</span></span> <span data-ttu-id="17323-181">In other words, the servers will check for a cached version of an asset according to its path as defined by its cache-key.</span><span class="sxs-lookup"><span data-stu-id="17323-181">In other words, the servers will check for a cached version of an asset according to its path as defined by its cache-key.</span></span>

<span data-ttu-id="17323-182">This physical cache-key starts with a double forward slash (//) followed by the protocol used to request the content (HTTP or HTTPS).</span><span class="sxs-lookup"><span data-stu-id="17323-182">This physical cache-key starts with a double forward slash (//) followed by the protocol used to request the content (HTTP or HTTPS).</span></span> <span data-ttu-id="17323-183">This protocol is followed by the relative path to the requested asset, which starts with the content access point (for example, _/000001/_).</span><span class="sxs-lookup"><span data-stu-id="17323-183">This protocol is followed by the relative path to the requested asset, which starts with the content access point (for example, _/000001/_).</span></span>

<span data-ttu-id="17323-184">By default, HTTP platforms are configured to use *standard-cache*, which means that query strings are ignored by the caching mechanism.</span><span class="sxs-lookup"><span data-stu-id="17323-184">By default, HTTP platforms are configured to use *standard-cache*, which means that query strings are ignored by the caching mechanism.</span></span> <span data-ttu-id="17323-185">This type of configuration prevents the cache-key from including query string data.</span><span class="sxs-lookup"><span data-stu-id="17323-185">This type of configuration prevents the cache-key from including query string data.</span></span>

<span data-ttu-id="17323-186">If a query string is recorded in the cache-key, it's converted to its hash equivalent and then inserted between the name of the requested asset and its file extension (for example, asset&lt;hash value&gt;.html).</span><span class="sxs-lookup"><span data-stu-id="17323-186">If a query string is recorded in the cache-key, it's converted to its hash equivalent and then inserted between the name of the requested asset and its file extension (for example, asset&lt;hash value&gt;.html).</span></span>

### <a name="response-header-format"></a><span data-ttu-id="17323-187">Response header format</span><span class="sxs-lookup"><span data-stu-id="17323-187">Response header format</span></span>

<span data-ttu-id="17323-188">The `X-EC-Debug` response header reports physical cache-key information in the following format:</span><span class="sxs-lookup"><span data-stu-id="17323-188">The `X-EC-Debug` response header reports physical cache-key information in the following format:</span></span>

`X-EC-Debug: x-ec-cache-key: CacheKey`

### <a name="sample-response-header"></a><span data-ttu-id="17323-189">Sample response header</span><span class="sxs-lookup"><span data-stu-id="17323-189">Sample response header</span></span>

<span data-ttu-id="17323-190">The following sample response header indicates the physical cache-key for the requested content:</span><span class="sxs-lookup"><span data-stu-id="17323-190">The following sample response header indicates the physical cache-key for the requested content:</span></span>

`X-EC-Debug: x-ec-cache-key: //http/800001/origin/images/foo.jpg`

## <a name="cache-state-response-header"></a><span data-ttu-id="17323-191">Cache state response header</span><span class="sxs-lookup"><span data-stu-id="17323-191">Cache state response header</span></span>
<span data-ttu-id="17323-192">The `X-EC-Debug: x-ec-cache-state` response header indicates the cache state of the requested content at the time it was requested.</span><span class="sxs-lookup"><span data-stu-id="17323-192">The `X-EC-Debug: x-ec-cache-state` response header indicates the cache state of the requested content at the time it was requested.</span></span>

### <a name="response-header-format"></a><span data-ttu-id="17323-193">Response header format</span><span class="sxs-lookup"><span data-stu-id="17323-193">Response header format</span></span>

<span data-ttu-id="17323-194">The `X-EC-Debug` response header reports cache state information in the following format:</span><span class="sxs-lookup"><span data-stu-id="17323-194">The `X-EC-Debug` response header reports cache state information in the following format:</span></span>

`X-EC-Debug: x-ec-cache-state: max-age=MASeconds (MATimePeriod); cache-ts=UnixTime (ddd, dd MMM yyyy HH:mm:ss GMT); cache-age=CASeconds (CATimePeriod); remaining-ttl=RTSeconds (RTTimePeriod); expires-delta=ExpiresSeconds`

<span data-ttu-id="17323-195">The terms used in the above response header syntax are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="17323-195">The terms used in the above response header syntax are defined as follows:</span></span>

- <span data-ttu-id="17323-196">MASeconds: Indicates the max-age (in seconds) as defined by the requested content's Cache-Control headers.</span><span class="sxs-lookup"><span data-stu-id="17323-196">MASeconds: Indicates the max-age (in seconds) as defined by the requested content's Cache-Control headers.</span></span>

- <span data-ttu-id="17323-197">MATimePeriod: Converts the max-age value (that is, MASeconds) to the approximate equivalent of a larger unit (for example, days).</span><span class="sxs-lookup"><span data-stu-id="17323-197">MATimePeriod: Converts the max-age value (that is, MASeconds) to the approximate equivalent of a larger unit (for example, days).</span></span> 

- <span data-ttu-id="17323-198">UnixTime: Indicates the cache timestamp of the requested content in Unix time (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="17323-198">UnixTime: Indicates the cache timestamp of the requested content in Unix time (a.k.a.</span></span> <span data-ttu-id="17323-199">POSIX time or Unix epoch).</span><span class="sxs-lookup"><span data-stu-id="17323-199">POSIX time or Unix epoch).</span></span> <span data-ttu-id="17323-200">The cache timestamp indicates the starting date/time from which an asset's TTL will be calculated.</span><span class="sxs-lookup"><span data-stu-id="17323-200">The cache timestamp indicates the starting date/time from which an asset's TTL will be calculated.</span></span> 

    <span data-ttu-id="17323-201">If the origin server does not utilize a third-party HTTP caching server or if that server does not return the Age response header, then the cache timestamp will always be the date/time when the asset was retrieved or revalidated.</span><span class="sxs-lookup"><span data-stu-id="17323-201">If the origin server does not utilize a third-party HTTP caching server or if that server does not return the Age response header, then the cache timestamp will always be the date/time when the asset was retrieved or revalidated.</span></span> <span data-ttu-id="17323-202">Otherwise, the POP servers will use the Age field to calculate the asset's TTL as follows: Retrieval/RevalidateDateTime - Age.</span><span class="sxs-lookup"><span data-stu-id="17323-202">Otherwise, the POP servers will use the Age field to calculate the asset's TTL as follows: Retrieval/RevalidateDateTime - Age.</span></span>

- <span data-ttu-id="17323-203">ddd, dd MMM yyyy HH:mm:ss GMT: Indicates the cache timestamp of the requested content.</span><span class="sxs-lookup"><span data-stu-id="17323-203">ddd, dd MMM yyyy HH:mm:ss GMT: Indicates the cache timestamp of the requested content.</span></span> <span data-ttu-id="17323-204">For more information, please see the UnixTime term above.</span><span class="sxs-lookup"><span data-stu-id="17323-204">For more information, please see the UnixTime term above.</span></span>

- <span data-ttu-id="17323-205">CASeconds: Indicates the number of seconds that have elapsed since the cache timestamp.</span><span class="sxs-lookup"><span data-stu-id="17323-205">CASeconds: Indicates the number of seconds that have elapsed since the cache timestamp.</span></span>

- <span data-ttu-id="17323-206">RTSeconds: Indicates the number of seconds remaining for which the cached content will be considered fresh.</span><span class="sxs-lookup"><span data-stu-id="17323-206">RTSeconds: Indicates the number of seconds remaining for which the cached content will be considered fresh.</span></span> <span data-ttu-id="17323-207">This value is calculated as follows: RTSeconds = max-age - cache age.</span><span class="sxs-lookup"><span data-stu-id="17323-207">This value is calculated as follows: RTSeconds = max-age - cache age.</span></span>

- <span data-ttu-id="17323-208">RTTimePeriod: Converts the remaining TTL value (that is, RTSeconds) to the approximate equivalent of a larger unit (for example, days).</span><span class="sxs-lookup"><span data-stu-id="17323-208">RTTimePeriod: Converts the remaining TTL value (that is, RTSeconds) to the approximate equivalent of a larger unit (for example, days).</span></span>

- <span data-ttu-id="17323-209">ExpiresSeconds: Indicates the number of seconds remaining before the date/time specified in the `Expires` response header.</span><span class="sxs-lookup"><span data-stu-id="17323-209">ExpiresSeconds: Indicates the number of seconds remaining before the date/time specified in the `Expires` response header.</span></span> <span data-ttu-id="17323-210">If the `Expires` response header was not included in the response, then the value of this term is *none*.</span><span class="sxs-lookup"><span data-stu-id="17323-210">If the `Expires` response header was not included in the response, then the value of this term is *none*.</span></span>

### <a name="sample-response-header"></a><span data-ttu-id="17323-211">Sample response header</span><span class="sxs-lookup"><span data-stu-id="17323-211">Sample response header</span></span>

<span data-ttu-id="17323-212">The following sample response header indicates the cache state of the requested content at the time that it was requested:</span><span class="sxs-lookup"><span data-stu-id="17323-212">The following sample response header indicates the cache state of the requested content at the time that it was requested:</span></span>

```X-EC-Debug: x-ec-cache-state: max-age=604800 (7d); cache-ts=1341802519 (Mon, 09 Jul 2012 02:55:19 GMT); cache-age=0 (0s); remaining-ttl=604800 (7d); expires-delta=none```

