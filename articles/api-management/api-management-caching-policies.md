---
title: Azure API Management caching policies | Microsoft Docs
description: Learn about the caching policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549806"
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="4b8fd-103">API Management caching policies</span><span class="sxs-lookup"><span data-stu-id="4b8fd-103">API Management caching policies</span></span>
<span data-ttu-id="4b8fd-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="4b8fd-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="CachingPolicies"></a> <span data-ttu-id="4b8fd-106">Caching policies</span><span class="sxs-lookup"><span data-stu-id="4b8fd-106">Caching policies</span></span>  
  
-   <span data-ttu-id="4b8fd-107">Response caching policies</span><span class="sxs-lookup"><span data-stu-id="4b8fd-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="4b8fd-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="4b8fd-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="4b8fd-110">Value caching policies</span><span class="sxs-lookup"><span data-stu-id="4b8fd-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="4b8fd-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="4b8fd-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="4b8fd-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <a name="GetFromCache"></a> <span data-ttu-id="4b8fd-114">Get from cache</span><span class="sxs-lookup"><span data-stu-id="4b8fd-114">Get from cache</span></span>  
 <span data-ttu-id="4b8fd-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="4b8fd-116">This policy can be applied in cases where response content remains static over a period of time.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="4b8fd-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4b8fd-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4b8fd-119">Policy statement</span><span class="sxs-lookup"><span data-stu-id="4b8fd-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="4b8fd-120">Examples</span><span class="sxs-lookup"><span data-stu-id="4b8fd-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="4b8fd-121">Example</span><span class="sxs-lookup"><span data-stu-id="4b8fd-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="4b8fd-122">Example using policy expressions</span><span class="sxs-lookup"><span data-stu-id="4b8fd-122">Example using policy expressions</span></span>  
 <span data-ttu-id="4b8fd-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="4b8fd-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
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
  
 <span data-ttu-id="4b8fd-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="4b8fd-126">Elements</span><span class="sxs-lookup"><span data-stu-id="4b8fd-126">Elements</span></span>  
  
|<span data-ttu-id="4b8fd-127">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-127">Name</span></span>|<span data-ttu-id="4b8fd-128">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-128">Description</span></span>|<span data-ttu-id="4b8fd-129">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4b8fd-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="4b8fd-130">cache-lookup</span></span>|<span data-ttu-id="4b8fd-131">Root element.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-131">Root element.</span></span>|<span data-ttu-id="4b8fd-132">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-132">Yes</span></span>|  
|<span data-ttu-id="4b8fd-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="4b8fd-133">vary-by-header</span></span>|<span data-ttu-id="4b8fd-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="4b8fd-135">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-135">No</span></span>|  
|<span data-ttu-id="4b8fd-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="4b8fd-136">vary-by-query-parameter</span></span>|<span data-ttu-id="4b8fd-137">Start caching responses per value of specified query parameters.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="4b8fd-138">Enter a single or multiple parameters.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="4b8fd-139">Use semicolon as a separator.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-139">Use semicolon as a separator.</span></span> <span data-ttu-id="4b8fd-140">If none are specified, all query parameters are used.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="4b8fd-141">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4b8fd-142">Attributes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-142">Attributes</span></span>  
  
|<span data-ttu-id="4b8fd-143">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-143">Name</span></span>|<span data-ttu-id="4b8fd-144">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-144">Description</span></span>|<span data-ttu-id="4b8fd-145">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-145">Required</span></span>|<span data-ttu-id="4b8fd-146">Default</span><span class="sxs-lookup"><span data-stu-id="4b8fd-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4b8fd-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="4b8fd-147">allow-private-response-caching</span></span>|<span data-ttu-id="4b8fd-148">When set to `true`, allows caching of requests that contain an Authorization header.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="4b8fd-149">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-149">No</span></span>|<span data-ttu-id="4b8fd-150">false</span><span class="sxs-lookup"><span data-stu-id="4b8fd-150">false</span></span>|  
|<span data-ttu-id="4b8fd-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="4b8fd-151">downstream-caching-type</span></span>|<span data-ttu-id="4b8fd-152">This attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="4b8fd-153">-   none - downstream caching is not allowed.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="4b8fd-154">-   private - downstream private caching is allowed.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="4b8fd-155">-   public - private and shared downstream caching is allowed.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="4b8fd-156">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-156">No</span></span>|<span data-ttu-id="4b8fd-157">none</span><span class="sxs-lookup"><span data-stu-id="4b8fd-157">none</span></span>|  
|<span data-ttu-id="4b8fd-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="4b8fd-158">must-revalidate</span></span>|<span data-ttu-id="4b8fd-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="4b8fd-160">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-160">No</span></span>|<span data-ttu-id="4b8fd-161">true</span><span class="sxs-lookup"><span data-stu-id="4b8fd-161">true</span></span>|  
|<span data-ttu-id="4b8fd-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="4b8fd-162">vary-by-developer</span></span>|<span data-ttu-id="4b8fd-163">Set to `true` to cache responses per developer key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="4b8fd-164">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-164">No</span></span>|<span data-ttu-id="4b8fd-165">false</span><span class="sxs-lookup"><span data-stu-id="4b8fd-165">false</span></span>|  
|<span data-ttu-id="4b8fd-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="4b8fd-166">vary-by-developer-groups</span></span>|<span data-ttu-id="4b8fd-167">Set to `true` to cache responses per user role.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="4b8fd-168">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-168">No</span></span>|<span data-ttu-id="4b8fd-169">false</span><span class="sxs-lookup"><span data-stu-id="4b8fd-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4b8fd-170">Usage</span><span class="sxs-lookup"><span data-stu-id="4b8fd-170">Usage</span></span>  
 <span data-ttu-id="4b8fd-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4b8fd-172">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="4b8fd-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="4b8fd-173">**Policy scopes:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="4b8fd-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <a name="StoreToCache"></a> <span data-ttu-id="4b8fd-174">Store to cache</span><span class="sxs-lookup"><span data-stu-id="4b8fd-174">Store to cache</span></span>  
 <span data-ttu-id="4b8fd-175">The `cache-store` policy caches responses according to the specified cache settings.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="4b8fd-176">This policy can be applied in cases where response content remains static over a period of time.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="4b8fd-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4b8fd-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4b8fd-179">Policy statement</span><span class="sxs-lookup"><span data-stu-id="4b8fd-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="4b8fd-180">Examples</span><span class="sxs-lookup"><span data-stu-id="4b8fd-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="4b8fd-181">Example</span><span class="sxs-lookup"><span data-stu-id="4b8fd-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="4b8fd-182">Example using policy expressions</span><span class="sxs-lookup"><span data-stu-id="4b8fd-182">Example using policy expressions</span></span>  
 <span data-ttu-id="4b8fd-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="4b8fd-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
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
  
 <span data-ttu-id="4b8fd-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="4b8fd-186">Elements</span><span class="sxs-lookup"><span data-stu-id="4b8fd-186">Elements</span></span>  
  
|<span data-ttu-id="4b8fd-187">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-187">Name</span></span>|<span data-ttu-id="4b8fd-188">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-188">Description</span></span>|<span data-ttu-id="4b8fd-189">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4b8fd-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="4b8fd-190">cache-store</span></span>|<span data-ttu-id="4b8fd-191">Root element.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-191">Root element.</span></span>|<span data-ttu-id="4b8fd-192">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4b8fd-193">Attributes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-193">Attributes</span></span>  
  
|<span data-ttu-id="4b8fd-194">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-194">Name</span></span>|<span data-ttu-id="4b8fd-195">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-195">Description</span></span>|<span data-ttu-id="4b8fd-196">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-196">Required</span></span>|<span data-ttu-id="4b8fd-197">Default</span><span class="sxs-lookup"><span data-stu-id="4b8fd-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4b8fd-198">duration</span><span class="sxs-lookup"><span data-stu-id="4b8fd-198">duration</span></span>|<span data-ttu-id="4b8fd-199">Time-to-live of the cached entries, specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="4b8fd-200">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-200">Yes</span></span>|<span data-ttu-id="4b8fd-201">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4b8fd-202">Usage</span><span class="sxs-lookup"><span data-stu-id="4b8fd-202">Usage</span></span>  
 <span data-ttu-id="4b8fd-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4b8fd-204">**Policy sections:** outbound</span><span class="sxs-lookup"><span data-stu-id="4b8fd-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="4b8fd-205">**Policy scopes:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="4b8fd-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <a name="GetFromCacheByKey"></a> <span data-ttu-id="4b8fd-206">Get value from cache</span><span class="sxs-lookup"><span data-stu-id="4b8fd-206">Get value from cache</span></span>  
 <span data-ttu-id="4b8fd-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="4b8fd-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4b8fd-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4b8fd-210">Policy statement</span><span class="sxs-lookup"><span data-stu-id="4b8fd-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="4b8fd-211">Example</span><span class="sxs-lookup"><span data-stu-id="4b8fd-211">Example</span></span>  
 <span data-ttu-id="4b8fd-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="4b8fd-213">Elements</span><span class="sxs-lookup"><span data-stu-id="4b8fd-213">Elements</span></span>  
  
|<span data-ttu-id="4b8fd-214">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-214">Name</span></span>|<span data-ttu-id="4b8fd-215">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-215">Description</span></span>|<span data-ttu-id="4b8fd-216">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4b8fd-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="4b8fd-217">cache-lookup-value</span></span>|<span data-ttu-id="4b8fd-218">Root element.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-218">Root element.</span></span>|<span data-ttu-id="4b8fd-219">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4b8fd-220">Attributes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-220">Attributes</span></span>  
  
|<span data-ttu-id="4b8fd-221">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-221">Name</span></span>|<span data-ttu-id="4b8fd-222">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-222">Description</span></span>|<span data-ttu-id="4b8fd-223">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-223">Required</span></span>|<span data-ttu-id="4b8fd-224">Default</span><span class="sxs-lookup"><span data-stu-id="4b8fd-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4b8fd-225">default-value</span><span class="sxs-lookup"><span data-stu-id="4b8fd-225">default-value</span></span>|<span data-ttu-id="4b8fd-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="4b8fd-227">If this attribute is not specified, `null` is assigned.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="4b8fd-228">No</span><span class="sxs-lookup"><span data-stu-id="4b8fd-228">No</span></span>|`null`|  
|<span data-ttu-id="4b8fd-229">key</span><span class="sxs-lookup"><span data-stu-id="4b8fd-229">key</span></span>|<span data-ttu-id="4b8fd-230">Cache key value to use in the lookup.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="4b8fd-231">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-231">Yes</span></span>|<span data-ttu-id="4b8fd-232">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-232">N/A</span></span>|  
|<span data-ttu-id="4b8fd-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-233">variable-name</span></span>|<span data-ttu-id="4b8fd-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="4b8fd-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="4b8fd-236">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-236">Yes</span></span>|<span data-ttu-id="4b8fd-237">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4b8fd-238">Usage</span><span class="sxs-lookup"><span data-stu-id="4b8fd-238">Usage</span></span>  
 <span data-ttu-id="4b8fd-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4b8fd-240">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="4b8fd-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="4b8fd-241">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="4b8fd-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <a name="StoreToCacheByKey"></a> <span data-ttu-id="4b8fd-242">Store value in cache</span><span class="sxs-lookup"><span data-stu-id="4b8fd-242">Store value in cache</span></span>  
 <span data-ttu-id="4b8fd-243">The `cache-store-value` performs cache storage by key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="4b8fd-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4b8fd-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4b8fd-246">Policy statement</span><span class="sxs-lookup"><span data-stu-id="4b8fd-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="4b8fd-247">Example</span><span class="sxs-lookup"><span data-stu-id="4b8fd-247">Example</span></span>  
 <span data-ttu-id="4b8fd-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="4b8fd-249">Elements</span><span class="sxs-lookup"><span data-stu-id="4b8fd-249">Elements</span></span>  
  
|<span data-ttu-id="4b8fd-250">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-250">Name</span></span>|<span data-ttu-id="4b8fd-251">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-251">Description</span></span>|<span data-ttu-id="4b8fd-252">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4b8fd-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="4b8fd-253">cache-store-value</span></span>|<span data-ttu-id="4b8fd-254">Root element.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-254">Root element.</span></span>|<span data-ttu-id="4b8fd-255">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4b8fd-256">Attributes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-256">Attributes</span></span>  
  
|<span data-ttu-id="4b8fd-257">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-257">Name</span></span>|<span data-ttu-id="4b8fd-258">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-258">Description</span></span>|<span data-ttu-id="4b8fd-259">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-259">Required</span></span>|<span data-ttu-id="4b8fd-260">Default</span><span class="sxs-lookup"><span data-stu-id="4b8fd-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4b8fd-261">duration</span><span class="sxs-lookup"><span data-stu-id="4b8fd-261">duration</span></span>|<span data-ttu-id="4b8fd-262">Value will be cached for the provided duration value, specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="4b8fd-263">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-263">Yes</span></span>|<span data-ttu-id="4b8fd-264">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-264">N/A</span></span>|  
|<span data-ttu-id="4b8fd-265">key</span><span class="sxs-lookup"><span data-stu-id="4b8fd-265">key</span></span>|<span data-ttu-id="4b8fd-266">Cache key the value will be stored under.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="4b8fd-267">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-267">Yes</span></span>|<span data-ttu-id="4b8fd-268">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-268">N/A</span></span>|  
|<span data-ttu-id="4b8fd-269">value</span><span class="sxs-lookup"><span data-stu-id="4b8fd-269">value</span></span>|<span data-ttu-id="4b8fd-270">The value to be cached.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-270">The value to be cached.</span></span>|<span data-ttu-id="4b8fd-271">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-271">Yes</span></span>|<span data-ttu-id="4b8fd-272">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4b8fd-273">Usage</span><span class="sxs-lookup"><span data-stu-id="4b8fd-273">Usage</span></span>  
 <span data-ttu-id="4b8fd-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4b8fd-275">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="4b8fd-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="4b8fd-276">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="4b8fd-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <a name="RemoveCacheByKey"></a> <span data-ttu-id="4b8fd-277">Remove value from cache</span><span class="sxs-lookup"><span data-stu-id="4b8fd-277">Remove value from cache</span></span>  
 <span data-ttu-id="4b8fd-278">The             `cache-remove-value` deletes a cached item identified by its key.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="4b8fd-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="4b8fd-280">Policy statement</span><span class="sxs-lookup"><span data-stu-id="4b8fd-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="4b8fd-281">Example</span><span class="sxs-lookup"><span data-stu-id="4b8fd-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="4b8fd-282">Elements</span><span class="sxs-lookup"><span data-stu-id="4b8fd-282">Elements</span></span>  
  
|<span data-ttu-id="4b8fd-283">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-283">Name</span></span>|<span data-ttu-id="4b8fd-284">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-284">Description</span></span>|<span data-ttu-id="4b8fd-285">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4b8fd-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="4b8fd-286">cache-remove-value</span></span>|<span data-ttu-id="4b8fd-287">Root element.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-287">Root element.</span></span>|<span data-ttu-id="4b8fd-288">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="4b8fd-289">Attributes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-289">Attributes</span></span>  
  
|<span data-ttu-id="4b8fd-290">Name</span><span class="sxs-lookup"><span data-stu-id="4b8fd-290">Name</span></span>|<span data-ttu-id="4b8fd-291">Description</span><span class="sxs-lookup"><span data-stu-id="4b8fd-291">Description</span></span>|<span data-ttu-id="4b8fd-292">Required</span><span class="sxs-lookup"><span data-stu-id="4b8fd-292">Required</span></span>|<span data-ttu-id="4b8fd-293">Default</span><span class="sxs-lookup"><span data-stu-id="4b8fd-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4b8fd-294">key</span><span class="sxs-lookup"><span data-stu-id="4b8fd-294">key</span></span>|<span data-ttu-id="4b8fd-295">The key of the previously cached value to be removed from the cache.</span><span class="sxs-lookup"><span data-stu-id="4b8fd-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="4b8fd-296">Yes</span><span class="sxs-lookup"><span data-stu-id="4b8fd-296">Yes</span></span>|<span data-ttu-id="4b8fd-297">N/A</span><span class="sxs-lookup"><span data-stu-id="4b8fd-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="4b8fd-298">Usage</span><span class="sxs-lookup"><span data-stu-id="4b8fd-298">Usage</span></span>  
 <span data-ttu-id="4b8fd-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="4b8fd-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="4b8fd-300">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="4b8fd-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="4b8fd-301">**Policy scopes:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="4b8fd-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="4b8fd-302">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b8fd-302">Next steps</span></span>
<span data-ttu-id="4b8fd-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4b8fd-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  