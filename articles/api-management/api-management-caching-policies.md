---
title: Azure API Management caching policies | Microsoft Docs
description: Learn about the caching policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: apimpm
ms.openlocfilehash: f3734304bdcc4b3f0944ebf568094595eea01a4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775170"
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="3789f-103">API Management caching policies</span><span class="sxs-lookup"><span data-stu-id="3789f-103">API Management caching policies</span></span>
<span data-ttu-id="3789f-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="3789f-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="3789f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="3789f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="CachingPolicies"></a> <span data-ttu-id="3789f-106">Caching policies</span><span class="sxs-lookup"><span data-stu-id="3789f-106">Caching policies</span></span>  
  
-   <span data-ttu-id="3789f-107">Response caching policies</span><span class="sxs-lookup"><span data-stu-id="3789f-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="3789f-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span><span class="sxs-lookup"><span data-stu-id="3789f-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
    -   <span data-ttu-id="3789f-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span><span class="sxs-lookup"><span data-stu-id="3789f-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="3789f-110">Value caching policies</span><span class="sxs-lookup"><span data-stu-id="3789f-110">Value caching policies</span></span>  

    -   <span data-ttu-id="3789f-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span><span class="sxs-lookup"><span data-stu-id="3789f-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span> 
    -   <span data-ttu-id="3789f-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span><span class="sxs-lookup"><span data-stu-id="3789f-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span> 
    -   <span data-ttu-id="3789f-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span><span class="sxs-lookup"><span data-stu-id="3789f-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <a name="GetFromCache"></a> <span data-ttu-id="3789f-114">Get from cache</span><span class="sxs-lookup"><span data-stu-id="3789f-114">Get from cache</span></span>  
 <span data-ttu-id="3789f-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span><span class="sxs-lookup"><span data-stu-id="3789f-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="3789f-116">This policy can be applied in cases where response content remains static over a period of time.</span><span class="sxs-lookup"><span data-stu-id="3789f-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="3789f-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span><span class="sxs-lookup"><span data-stu-id="3789f-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3789f-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span><span class="sxs-lookup"><span data-stu-id="3789f-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3789f-119">Policy statement</span><span class="sxs-lookup"><span data-stu-id="3789f-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-private-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="3789f-120">Examples</span><span class="sxs-lookup"><span data-stu-id="3789f-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="3789f-121">Example</span><span class="sxs-lookup"><span data-stu-id="3789f-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="3789f-122">Example using policy expressions</span><span class="sxs-lookup"><span data-stu-id="3789f-122">Example using policy expressions</span></span>  
 <span data-ttu-id="3789f-123">This example shows how to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="3789f-123">This example shows how to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="3789f-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span><span class="sxs-lookup"><span data-stu-id="3789f-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="3789f-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="3789f-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3789f-126">Elements</span><span class="sxs-lookup"><span data-stu-id="3789f-126">Elements</span></span>  
  
|<span data-ttu-id="3789f-127">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-127">Name</span></span>|<span data-ttu-id="3789f-128">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-128">Description</span></span>|<span data-ttu-id="3789f-129">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3789f-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="3789f-130">cache-lookup</span></span>|<span data-ttu-id="3789f-131">Root element.</span><span class="sxs-lookup"><span data-stu-id="3789f-131">Root element.</span></span>|<span data-ttu-id="3789f-132">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-132">Yes</span></span>|  
|<span data-ttu-id="3789f-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="3789f-133">vary-by-header</span></span>|<span data-ttu-id="3789f-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="3789f-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="3789f-135">No</span><span class="sxs-lookup"><span data-stu-id="3789f-135">No</span></span>|  
|<span data-ttu-id="3789f-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="3789f-136">vary-by-query-parameter</span></span>|<span data-ttu-id="3789f-137">Start caching responses per value of specified query parameters.</span><span class="sxs-lookup"><span data-stu-id="3789f-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="3789f-138">Enter a single or multiple parameters.</span><span class="sxs-lookup"><span data-stu-id="3789f-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="3789f-139">Use semicolon as a separator.</span><span class="sxs-lookup"><span data-stu-id="3789f-139">Use semicolon as a separator.</span></span> <span data-ttu-id="3789f-140">If none are specified, all query parameters are used.</span><span class="sxs-lookup"><span data-stu-id="3789f-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="3789f-141">No</span><span class="sxs-lookup"><span data-stu-id="3789f-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3789f-142">Attributes</span><span class="sxs-lookup"><span data-stu-id="3789f-142">Attributes</span></span>  
  
|<span data-ttu-id="3789f-143">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-143">Name</span></span>|<span data-ttu-id="3789f-144">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-144">Description</span></span>|<span data-ttu-id="3789f-145">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-145">Required</span></span>|<span data-ttu-id="3789f-146">Default</span><span class="sxs-lookup"><span data-stu-id="3789f-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3789f-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="3789f-147">allow-private-response-caching</span></span>|<span data-ttu-id="3789f-148">When set to `true`, allows caching of requests that contain an Authorization header.</span><span class="sxs-lookup"><span data-stu-id="3789f-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="3789f-149">No</span><span class="sxs-lookup"><span data-stu-id="3789f-149">No</span></span>|<span data-ttu-id="3789f-150">false</span><span class="sxs-lookup"><span data-stu-id="3789f-150">false</span></span>|  
|<span data-ttu-id="3789f-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="3789f-151">downstream-caching-type</span></span>|<span data-ttu-id="3789f-152">This attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="3789f-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="3789f-153">-   none - downstream caching is not allowed.</span><span class="sxs-lookup"><span data-stu-id="3789f-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="3789f-154">-   private - downstream private caching is allowed.</span><span class="sxs-lookup"><span data-stu-id="3789f-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="3789f-155">-   public - private and shared downstream caching is allowed.</span><span class="sxs-lookup"><span data-stu-id="3789f-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="3789f-156">No</span><span class="sxs-lookup"><span data-stu-id="3789f-156">No</span></span>|<span data-ttu-id="3789f-157">none</span><span class="sxs-lookup"><span data-stu-id="3789f-157">none</span></span>|  
|<span data-ttu-id="3789f-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="3789f-158">must-revalidate</span></span>|<span data-ttu-id="3789f-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span><span class="sxs-lookup"><span data-stu-id="3789f-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="3789f-160">No</span><span class="sxs-lookup"><span data-stu-id="3789f-160">No</span></span>|<span data-ttu-id="3789f-161">true</span><span class="sxs-lookup"><span data-stu-id="3789f-161">true</span></span>|  
|<span data-ttu-id="3789f-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="3789f-162">vary-by-developer</span></span>|<span data-ttu-id="3789f-163">Set to `true` to cache responses per developer key.</span><span class="sxs-lookup"><span data-stu-id="3789f-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="3789f-164">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-164">Yes</span></span>||  
|<span data-ttu-id="3789f-165">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="3789f-165">vary-by-developer-groups</span></span>|<span data-ttu-id="3789f-166">Set to `true` to cache responses per user role.</span><span class="sxs-lookup"><span data-stu-id="3789f-166">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="3789f-167">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-167">Yes</span></span>||  
  
### <a name="usage"></a><span data-ttu-id="3789f-168">Usage</span><span class="sxs-lookup"><span data-stu-id="3789f-168">Usage</span></span>  
 <span data-ttu-id="3789f-169">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3789f-169">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3789f-170">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="3789f-170">**Policy sections:** inbound</span></span>  
-   <span data-ttu-id="3789f-171">**Policy scopes:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="3789f-171">**Policy scopes:** API, operation, product</span></span>  
  
##  <a name="StoreToCache"></a> <span data-ttu-id="3789f-172">Store to cache</span><span class="sxs-lookup"><span data-stu-id="3789f-172">Store to cache</span></span>  
 <span data-ttu-id="3789f-173">The `cache-store` policy caches responses according to the specified cache settings.</span><span class="sxs-lookup"><span data-stu-id="3789f-173">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="3789f-174">This policy can be applied in cases where response content remains static over a period of time.</span><span class="sxs-lookup"><span data-stu-id="3789f-174">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="3789f-175">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span><span class="sxs-lookup"><span data-stu-id="3789f-175">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3789f-176">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span><span class="sxs-lookup"><span data-stu-id="3789f-176">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3789f-177">Policy statement</span><span class="sxs-lookup"><span data-stu-id="3789f-177">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="3789f-178">Examples</span><span class="sxs-lookup"><span data-stu-id="3789f-178">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="3789f-179">Example</span><span class="sxs-lookup"><span data-stu-id="3789f-179">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="3789f-180">Example using policy expressions</span><span class="sxs-lookup"><span data-stu-id="3789f-180">Example using policy expressions</span></span>  
 <span data-ttu-id="3789f-181">This example shows how to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="3789f-181">This example shows how to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="3789f-182">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span><span class="sxs-lookup"><span data-stu-id="3789f-182">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="3789f-183">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="3789f-183">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3789f-184">Elements</span><span class="sxs-lookup"><span data-stu-id="3789f-184">Elements</span></span>  
  
|<span data-ttu-id="3789f-185">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-185">Name</span></span>|<span data-ttu-id="3789f-186">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-186">Description</span></span>|<span data-ttu-id="3789f-187">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-187">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3789f-188">cache-store</span><span class="sxs-lookup"><span data-stu-id="3789f-188">cache-store</span></span>|<span data-ttu-id="3789f-189">Root element.</span><span class="sxs-lookup"><span data-stu-id="3789f-189">Root element.</span></span>|<span data-ttu-id="3789f-190">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-190">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3789f-191">Attributes</span><span class="sxs-lookup"><span data-stu-id="3789f-191">Attributes</span></span>  
  
|<span data-ttu-id="3789f-192">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-192">Name</span></span>|<span data-ttu-id="3789f-193">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-193">Description</span></span>|<span data-ttu-id="3789f-194">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-194">Required</span></span>|<span data-ttu-id="3789f-195">Default</span><span class="sxs-lookup"><span data-stu-id="3789f-195">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3789f-196">duration</span><span class="sxs-lookup"><span data-stu-id="3789f-196">duration</span></span>|<span data-ttu-id="3789f-197">Time-to-live of the cached entries, specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="3789f-197">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="3789f-198">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-198">Yes</span></span>|<span data-ttu-id="3789f-199">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-199">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3789f-200">Usage</span><span class="sxs-lookup"><span data-stu-id="3789f-200">Usage</span></span>  
 <span data-ttu-id="3789f-201">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3789f-201">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3789f-202">**Policy sections:** outbound</span><span class="sxs-lookup"><span data-stu-id="3789f-202">**Policy sections:** outbound</span></span>    
-   <span data-ttu-id="3789f-203">**Policy scopes:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="3789f-203">**Policy scopes:** API, operation, product</span></span>  
  
##  <a name="GetFromCacheByKey"></a> <span data-ttu-id="3789f-204">Get value from cache</span><span class="sxs-lookup"><span data-stu-id="3789f-204">Get value from cache</span></span>  
 <span data-ttu-id="3789f-205">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span><span class="sxs-lookup"><span data-stu-id="3789f-205">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="3789f-206">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="3789f-206">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3789f-207">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span><span class="sxs-lookup"><span data-stu-id="3789f-207">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3789f-208">Policy statement</span><span class="sxs-lookup"><span data-stu-id="3789f-208">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="3789f-209">Example</span><span class="sxs-lookup"><span data-stu-id="3789f-209">Example</span></span>  
 <span data-ttu-id="3789f-210">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="3789f-210">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3789f-211">Elements</span><span class="sxs-lookup"><span data-stu-id="3789f-211">Elements</span></span>  
  
|<span data-ttu-id="3789f-212">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-212">Name</span></span>|<span data-ttu-id="3789f-213">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-213">Description</span></span>|<span data-ttu-id="3789f-214">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3789f-215">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="3789f-215">cache-lookup-value</span></span>|<span data-ttu-id="3789f-216">Root element.</span><span class="sxs-lookup"><span data-stu-id="3789f-216">Root element.</span></span>|<span data-ttu-id="3789f-217">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3789f-218">Attributes</span><span class="sxs-lookup"><span data-stu-id="3789f-218">Attributes</span></span>  
  
|<span data-ttu-id="3789f-219">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-219">Name</span></span>|<span data-ttu-id="3789f-220">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-220">Description</span></span>|<span data-ttu-id="3789f-221">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-221">Required</span></span>|<span data-ttu-id="3789f-222">Default</span><span class="sxs-lookup"><span data-stu-id="3789f-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3789f-223">default-value</span><span class="sxs-lookup"><span data-stu-id="3789f-223">default-value</span></span>|<span data-ttu-id="3789f-224">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span><span class="sxs-lookup"><span data-stu-id="3789f-224">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="3789f-225">If this attribute is not specified, `null` is assigned.</span><span class="sxs-lookup"><span data-stu-id="3789f-225">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="3789f-226">No</span><span class="sxs-lookup"><span data-stu-id="3789f-226">No</span></span>|`null`|  
|<span data-ttu-id="3789f-227">key</span><span class="sxs-lookup"><span data-stu-id="3789f-227">key</span></span>|<span data-ttu-id="3789f-228">Cache key value to use in the lookup.</span><span class="sxs-lookup"><span data-stu-id="3789f-228">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="3789f-229">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-229">Yes</span></span>|<span data-ttu-id="3789f-230">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-230">N/A</span></span>|  
|<span data-ttu-id="3789f-231">variable-name</span><span class="sxs-lookup"><span data-stu-id="3789f-231">variable-name</span></span>|<span data-ttu-id="3789f-232">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span><span class="sxs-lookup"><span data-stu-id="3789f-232">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="3789f-233">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span><span class="sxs-lookup"><span data-stu-id="3789f-233">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="3789f-234">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-234">Yes</span></span>|<span data-ttu-id="3789f-235">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-235">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3789f-236">Usage</span><span class="sxs-lookup"><span data-stu-id="3789f-236">Usage</span></span>  
 <span data-ttu-id="3789f-237">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3789f-237">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3789f-238">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="3789f-238">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
-   <span data-ttu-id="3789f-239">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="3789f-239">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <a name="StoreToCacheByKey"></a> <span data-ttu-id="3789f-240">Store value in cache</span><span class="sxs-lookup"><span data-stu-id="3789f-240">Store value in cache</span></span>  
 <span data-ttu-id="3789f-241">The `cache-store-value` performs cache storage by key.</span><span class="sxs-lookup"><span data-stu-id="3789f-241">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="3789f-242">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="3789f-242">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3789f-243">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span><span class="sxs-lookup"><span data-stu-id="3789f-243">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3789f-244">Policy statement</span><span class="sxs-lookup"><span data-stu-id="3789f-244">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="3789f-245">Example</span><span class="sxs-lookup"><span data-stu-id="3789f-245">Example</span></span>  
 <span data-ttu-id="3789f-246">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="3789f-246">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3789f-247">Elements</span><span class="sxs-lookup"><span data-stu-id="3789f-247">Elements</span></span>  
  
|<span data-ttu-id="3789f-248">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-248">Name</span></span>|<span data-ttu-id="3789f-249">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-249">Description</span></span>|<span data-ttu-id="3789f-250">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3789f-251">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="3789f-251">cache-store-value</span></span>|<span data-ttu-id="3789f-252">Root element.</span><span class="sxs-lookup"><span data-stu-id="3789f-252">Root element.</span></span>|<span data-ttu-id="3789f-253">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-253">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3789f-254">Attributes</span><span class="sxs-lookup"><span data-stu-id="3789f-254">Attributes</span></span>  
  
|<span data-ttu-id="3789f-255">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-255">Name</span></span>|<span data-ttu-id="3789f-256">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-256">Description</span></span>|<span data-ttu-id="3789f-257">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-257">Required</span></span>|<span data-ttu-id="3789f-258">Default</span><span class="sxs-lookup"><span data-stu-id="3789f-258">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3789f-259">duration</span><span class="sxs-lookup"><span data-stu-id="3789f-259">duration</span></span>|<span data-ttu-id="3789f-260">Value will be cached for the provided duration value, specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="3789f-260">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="3789f-261">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-261">Yes</span></span>|<span data-ttu-id="3789f-262">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-262">N/A</span></span>|  
|<span data-ttu-id="3789f-263">key</span><span class="sxs-lookup"><span data-stu-id="3789f-263">key</span></span>|<span data-ttu-id="3789f-264">Cache key the value will be stored under.</span><span class="sxs-lookup"><span data-stu-id="3789f-264">Cache key the value will be stored under.</span></span>|<span data-ttu-id="3789f-265">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-265">Yes</span></span>|<span data-ttu-id="3789f-266">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-266">N/A</span></span>|  
|<span data-ttu-id="3789f-267">value</span><span class="sxs-lookup"><span data-stu-id="3789f-267">value</span></span>|<span data-ttu-id="3789f-268">The value to be cached.</span><span class="sxs-lookup"><span data-stu-id="3789f-268">The value to be cached.</span></span>|<span data-ttu-id="3789f-269">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-269">Yes</span></span>|<span data-ttu-id="3789f-270">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-270">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3789f-271">Usage</span><span class="sxs-lookup"><span data-stu-id="3789f-271">Usage</span></span>  
 <span data-ttu-id="3789f-272">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3789f-272">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3789f-273">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="3789f-273">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
-   <span data-ttu-id="3789f-274">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="3789f-274">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <a name="RemoveCacheByKey"></a> <span data-ttu-id="3789f-275">Remove value from cache</span><span class="sxs-lookup"><span data-stu-id="3789f-275">Remove value from cache</span></span>  
<span data-ttu-id="3789f-276">The             `cache-remove-value` deletes a cached item identified by its key.</span><span class="sxs-lookup"><span data-stu-id="3789f-276">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="3789f-277">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="3789f-277">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="3789f-278">Policy statement</span><span class="sxs-lookup"><span data-stu-id="3789f-278">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="3789f-279">Example</span><span class="sxs-lookup"><span data-stu-id="3789f-279">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="3789f-280">Elements</span><span class="sxs-lookup"><span data-stu-id="3789f-280">Elements</span></span>  
  
|<span data-ttu-id="3789f-281">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-281">Name</span></span>|<span data-ttu-id="3789f-282">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-282">Description</span></span>|<span data-ttu-id="3789f-283">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-283">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3789f-284">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="3789f-284">cache-remove-value</span></span>|<span data-ttu-id="3789f-285">Root element.</span><span class="sxs-lookup"><span data-stu-id="3789f-285">Root element.</span></span>|<span data-ttu-id="3789f-286">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-286">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="3789f-287">Attributes</span><span class="sxs-lookup"><span data-stu-id="3789f-287">Attributes</span></span>  
  
|<span data-ttu-id="3789f-288">Name</span><span class="sxs-lookup"><span data-stu-id="3789f-288">Name</span></span>|<span data-ttu-id="3789f-289">Description</span><span class="sxs-lookup"><span data-stu-id="3789f-289">Description</span></span>|<span data-ttu-id="3789f-290">Required</span><span class="sxs-lookup"><span data-stu-id="3789f-290">Required</span></span>|<span data-ttu-id="3789f-291">Default</span><span class="sxs-lookup"><span data-stu-id="3789f-291">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3789f-292">key</span><span class="sxs-lookup"><span data-stu-id="3789f-292">key</span></span>|<span data-ttu-id="3789f-293">The key of the previously cached value to be removed from the cache.</span><span class="sxs-lookup"><span data-stu-id="3789f-293">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="3789f-294">Yes</span><span class="sxs-lookup"><span data-stu-id="3789f-294">Yes</span></span>|<span data-ttu-id="3789f-295">N/A</span><span class="sxs-lookup"><span data-stu-id="3789f-295">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="3789f-296">Usage</span><span class="sxs-lookup"><span data-stu-id="3789f-296">Usage</span></span>  
 <span data-ttu-id="3789f-297">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="3789f-297">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="3789f-298">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="3789f-298">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
-   <span data-ttu-id="3789f-299">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="3789f-299">**Policy scopes:** global, API, operation, product</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3789f-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="3789f-300">Next steps</span></span>

<span data-ttu-id="3789f-301">For more information working with policies, see:</span><span class="sxs-lookup"><span data-stu-id="3789f-301">For more information working with policies, see:</span></span>

+ [<span data-ttu-id="3789f-302">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="3789f-302">Policies in API Management</span></span>](api-management-howto-policies.md)
+ [<span data-ttu-id="3789f-303">Transform APIs</span><span class="sxs-lookup"><span data-stu-id="3789f-303">Transform APIs</span></span>](transform-api.md)
+ <span data-ttu-id="3789f-304">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span><span class="sxs-lookup"><span data-stu-id="3789f-304">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span></span>
+ [<span data-ttu-id="3789f-305">Policy samples</span><span class="sxs-lookup"><span data-stu-id="3789f-305">Policy samples</span></span>](policy-samples.md)   
