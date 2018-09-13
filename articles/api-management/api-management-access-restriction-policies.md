---
title: Azure API Management access restriction policies | Microsoft Docs
description: Learn about the access restriction policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7e1f99c6c603420386432e04d0a2f0ecda95d6b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563094"
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="ffb40-103">API Management access restriction policies</span><span class="sxs-lookup"><span data-stu-id="ffb40-103">API Management access restriction policies</span></span>
<span data-ttu-id="ffb40-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="ffb40-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="ffb40-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="ffb40-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="AccessRestrictionPolicies"></a> <span data-ttu-id="ffb40-106">Access restriction policies</span><span class="sxs-lookup"><span data-stu-id="ffb40-106">Access restriction policies</span></span>  
  
-   <span data-ttu-id="ffb40-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span><span class="sxs-lookup"><span data-stu-id="ffb40-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="ffb40-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="ffb40-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="ffb40-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span><span class="sxs-lookup"><span data-stu-id="ffb40-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="ffb40-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="ffb40-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="ffb40-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span><span class="sxs-lookup"><span data-stu-id="ffb40-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <a name="CheckHTTPHeader"></a> <span data-ttu-id="ffb40-114">Check HTTP header</span><span class="sxs-lookup"><span data-stu-id="ffb40-114">Check HTTP header</span></span>  
 <span data-ttu-id="ffb40-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span><span class="sxs-lookup"><span data-stu-id="ffb40-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="ffb40-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span><span class="sxs-lookup"><span data-stu-id="ffb40-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="ffb40-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-118">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-119">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-120">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-120">Elements</span></span>  
  
|<span data-ttu-id="ffb40-121">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-121">Name</span></span>|<span data-ttu-id="ffb40-122">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-122">Description</span></span>|<span data-ttu-id="ffb40-123">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-124">check-header</span><span class="sxs-lookup"><span data-stu-id="ffb40-124">check-header</span></span>|<span data-ttu-id="ffb40-125">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-125">Root element.</span></span>|<span data-ttu-id="ffb40-126">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-126">Yes</span></span>|  
|<span data-ttu-id="ffb40-127">value</span><span class="sxs-lookup"><span data-stu-id="ffb40-127">value</span></span>|<span data-ttu-id="ffb40-128">Allowed HTTP header value.</span><span class="sxs-lookup"><span data-stu-id="ffb40-128">Allowed HTTP header value.</span></span> <span data-ttu-id="ffb40-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span><span class="sxs-lookup"><span data-stu-id="ffb40-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="ffb40-130">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-131">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-131">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-132">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-132">Name</span></span>|<span data-ttu-id="ffb40-133">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-133">Description</span></span>|<span data-ttu-id="ffb40-134">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-134">Required</span></span>|<span data-ttu-id="ffb40-135">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="ffb40-136">failed-check-error-message</span></span>|<span data-ttu-id="ffb40-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span><span class="sxs-lookup"><span data-stu-id="ffb40-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="ffb40-138">This message must have any special characters properly escaped.</span><span class="sxs-lookup"><span data-stu-id="ffb40-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="ffb40-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-139">Yes</span></span>|<span data-ttu-id="ffb40-140">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-140">N/A</span></span>|  
|<span data-ttu-id="ffb40-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="ffb40-141">failed-check-httpcode</span></span>|<span data-ttu-id="ffb40-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span><span class="sxs-lookup"><span data-stu-id="ffb40-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="ffb40-143">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-143">Yes</span></span>|<span data-ttu-id="ffb40-144">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-144">N/A</span></span>|  
|<span data-ttu-id="ffb40-145">header-name</span><span class="sxs-lookup"><span data-stu-id="ffb40-145">header-name</span></span>|<span data-ttu-id="ffb40-146">The name of the HTTP Header to check.</span><span class="sxs-lookup"><span data-stu-id="ffb40-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="ffb40-147">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-147">Yes</span></span>|<span data-ttu-id="ffb40-148">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-148">N/A</span></span>|  
|<span data-ttu-id="ffb40-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="ffb40-149">ignore-case</span></span>|<span data-ttu-id="ffb40-150">Can be set to True or False.</span><span class="sxs-lookup"><span data-stu-id="ffb40-150">Can be set to True or False.</span></span> <span data-ttu-id="ffb40-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span><span class="sxs-lookup"><span data-stu-id="ffb40-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="ffb40-152">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-152">Yes</span></span>|<span data-ttu-id="ffb40-153">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-154">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-154">Usage</span></span>  
 <span data-ttu-id="ffb40-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-156">**Policy sections:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="ffb40-157">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="LimitCallRate"></a> <span data-ttu-id="ffb40-158">Limit call rate by subscription</span><span class="sxs-lookup"><span data-stu-id="ffb40-158">Limit call rate by subscription</span></span>  
 <span data-ttu-id="ffb40-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span><span class="sxs-lookup"><span data-stu-id="ffb40-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="ffb40-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span><span class="sxs-lookup"><span data-stu-id="ffb40-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ffb40-161">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="ffb40-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ffb40-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-163">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-164">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-165">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-165">Elements</span></span>  
  
|<span data-ttu-id="ffb40-166">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-166">Name</span></span>|<span data-ttu-id="ffb40-167">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-167">Description</span></span>|<span data-ttu-id="ffb40-168">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="ffb40-169">set-limit</span></span>|<span data-ttu-id="ffb40-170">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-170">Root element.</span></span>|<span data-ttu-id="ffb40-171">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-171">Yes</span></span>|  
|<span data-ttu-id="ffb40-172">api</span><span class="sxs-lookup"><span data-stu-id="ffb40-172">api</span></span>|<span data-ttu-id="ffb40-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span><span class="sxs-lookup"><span data-stu-id="ffb40-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="ffb40-174">Product and API call rate limits are applied independently.</span><span class="sxs-lookup"><span data-stu-id="ffb40-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="ffb40-175">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-175">No</span></span>|  
|<span data-ttu-id="ffb40-176">operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-176">operation</span></span>|<span data-ttu-id="ffb40-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span><span class="sxs-lookup"><span data-stu-id="ffb40-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="ffb40-178">Product, API, and operation call rate limits are applied independently.</span><span class="sxs-lookup"><span data-stu-id="ffb40-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="ffb40-179">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-180">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-180">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-181">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-181">Name</span></span>|<span data-ttu-id="ffb40-182">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-182">Description</span></span>|<span data-ttu-id="ffb40-183">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-183">Required</span></span>|<span data-ttu-id="ffb40-184">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-185">name</span><span class="sxs-lookup"><span data-stu-id="ffb40-185">name</span></span>|<span data-ttu-id="ffb40-186">The name of the API for which to apply the rate limit.</span><span class="sxs-lookup"><span data-stu-id="ffb40-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="ffb40-187">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-187">Yes</span></span>|<span data-ttu-id="ffb40-188">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-188">N/A</span></span>|  
|<span data-ttu-id="ffb40-189">calls</span><span class="sxs-lookup"><span data-stu-id="ffb40-189">calls</span></span>|<span data-ttu-id="ffb40-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-191">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-191">Yes</span></span>|<span data-ttu-id="ffb40-192">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-192">N/A</span></span>|  
|<span data-ttu-id="ffb40-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ffb40-193">renewal-period</span></span>|<span data-ttu-id="ffb40-194">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="ffb40-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="ffb40-195">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-195">Yes</span></span>|<span data-ttu-id="ffb40-196">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-197">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-197">Usage</span></span>  
 <span data-ttu-id="ffb40-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-199">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-200">**Policy scopes:** product</span><span class="sxs-lookup"><span data-stu-id="ffb40-200">**Policy scopes:** product</span></span>  
  
##  <a name="LimitCallRateByKey"></a> <span data-ttu-id="ffb40-201">Limit call rate by key</span><span class="sxs-lookup"><span data-stu-id="ffb40-201">Limit call rate by key</span></span>  
 <span data-ttu-id="ffb40-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span><span class="sxs-lookup"><span data-stu-id="ffb40-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="ffb40-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="ffb40-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="ffb40-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span><span class="sxs-lookup"><span data-stu-id="ffb40-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="ffb40-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span><span class="sxs-lookup"><span data-stu-id="ffb40-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="ffb40-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="ffb40-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ffb40-207">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="ffb40-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-208">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-209">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-209">Example</span></span>  
 <span data-ttu-id="ffb40-210">In the following example, the rate limit is keyed by the caller IP address.</span><span class="sxs-lookup"><span data-stu-id="ffb40-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-211">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-211">Elements</span></span>  
  
|<span data-ttu-id="ffb40-212">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-212">Name</span></span>|<span data-ttu-id="ffb40-213">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-213">Description</span></span>|<span data-ttu-id="ffb40-214">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="ffb40-215">set-limit</span></span>|<span data-ttu-id="ffb40-216">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-216">Root element.</span></span>|<span data-ttu-id="ffb40-217">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-218">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-218">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-219">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-219">Name</span></span>|<span data-ttu-id="ffb40-220">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-220">Description</span></span>|<span data-ttu-id="ffb40-221">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-221">Required</span></span>|<span data-ttu-id="ffb40-222">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-223">calls</span><span class="sxs-lookup"><span data-stu-id="ffb40-223">calls</span></span>|<span data-ttu-id="ffb40-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-225">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-225">Yes</span></span>|<span data-ttu-id="ffb40-226">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-226">N/A</span></span>|  
|<span data-ttu-id="ffb40-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="ffb40-227">counter-key</span></span>|<span data-ttu-id="ffb40-228">The key to use for the rate limit policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="ffb40-229">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-229">Yes</span></span>|<span data-ttu-id="ffb40-230">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-230">N/A</span></span>|  
|<span data-ttu-id="ffb40-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="ffb40-231">increment-condition</span></span>|<span data-ttu-id="ffb40-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span><span class="sxs-lookup"><span data-stu-id="ffb40-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="ffb40-233">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-233">No</span></span>|<span data-ttu-id="ffb40-234">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-234">N/A</span></span>|  
|<span data-ttu-id="ffb40-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ffb40-235">renewal-period</span></span>|<span data-ttu-id="ffb40-236">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="ffb40-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="ffb40-237">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-237">Yes</span></span>|<span data-ttu-id="ffb40-238">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-239">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-239">Usage</span></span>  
 <span data-ttu-id="ffb40-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-241">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-242">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="RestrictCallerIPs"></a> <span data-ttu-id="ffb40-243">Restrict caller IPs</span><span class="sxs-lookup"><span data-stu-id="ffb40-243">Restrict caller IPs</span></span>  
 <span data-ttu-id="ffb40-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span><span class="sxs-lookup"><span data-stu-id="ffb40-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-245">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-246">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-247">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-247">Elements</span></span>  
  
|<span data-ttu-id="ffb40-248">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-248">Name</span></span>|<span data-ttu-id="ffb40-249">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-249">Description</span></span>|<span data-ttu-id="ffb40-250">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="ffb40-251">ip-filter</span></span>|<span data-ttu-id="ffb40-252">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-252">Root element.</span></span>|<span data-ttu-id="ffb40-253">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-253">Yes</span></span>|  
|<span data-ttu-id="ffb40-254">address</span><span class="sxs-lookup"><span data-stu-id="ffb40-254">address</span></span>|<span data-ttu-id="ffb40-255">Specifies a single IP address on which to filter.</span><span class="sxs-lookup"><span data-stu-id="ffb40-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="ffb40-256">At least one `address` or `address-range` element is required.</span><span class="sxs-lookup"><span data-stu-id="ffb40-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="ffb40-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="ffb40-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="ffb40-258">Specifies a range of IP address on which to filter.</span><span class="sxs-lookup"><span data-stu-id="ffb40-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="ffb40-259">At least one `address` or `address-range` element is required.</span><span class="sxs-lookup"><span data-stu-id="ffb40-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-260">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-260">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-261">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-261">Name</span></span>|<span data-ttu-id="ffb40-262">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-262">Description</span></span>|<span data-ttu-id="ffb40-263">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-263">Required</span></span>|<span data-ttu-id="ffb40-264">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="ffb40-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="ffb40-266">A range of IP addresses to allow or deny access for.</span><span class="sxs-lookup"><span data-stu-id="ffb40-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="ffb40-267">Required when the `address-range` element is used.</span><span class="sxs-lookup"><span data-stu-id="ffb40-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="ffb40-268">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-268">N/A</span></span>|  
|<span data-ttu-id="ffb40-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="ffb40-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="ffb40-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span><span class="sxs-lookup"><span data-stu-id="ffb40-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="ffb40-271">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-271">Yes</span></span>|<span data-ttu-id="ffb40-272">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-273">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-273">Usage</span></span>  
 <span data-ttu-id="ffb40-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-275">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-276">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetUsageQuota"></a> <span data-ttu-id="ffb40-277">Set usage quota by subscription</span><span class="sxs-lookup"><span data-stu-id="ffb40-277">Set usage quota by subscription</span></span>  
 <span data-ttu-id="ffb40-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ffb40-279">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="ffb40-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ffb40-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-281">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-282">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-283">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-283">Elements</span></span>  
  
|<span data-ttu-id="ffb40-284">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-284">Name</span></span>|<span data-ttu-id="ffb40-285">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-285">Description</span></span>|<span data-ttu-id="ffb40-286">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-287">quota</span><span class="sxs-lookup"><span data-stu-id="ffb40-287">quota</span></span>|<span data-ttu-id="ffb40-288">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-288">Root element.</span></span>|<span data-ttu-id="ffb40-289">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-289">Yes</span></span>|  
|<span data-ttu-id="ffb40-290">api</span><span class="sxs-lookup"><span data-stu-id="ffb40-290">api</span></span>|<span data-ttu-id="ffb40-291">Add one  or more of these elements to impose a quota on APIs within the product.</span><span class="sxs-lookup"><span data-stu-id="ffb40-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="ffb40-292">Product and API quotas are applied independently.</span><span class="sxs-lookup"><span data-stu-id="ffb40-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="ffb40-293">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-293">No</span></span>|  
|<span data-ttu-id="ffb40-294">operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-294">operation</span></span>|<span data-ttu-id="ffb40-295">Add one  or more of these elements to impose a quota on operations within an API.</span><span class="sxs-lookup"><span data-stu-id="ffb40-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="ffb40-296">Product, API, and operation quotas are applied independently.</span><span class="sxs-lookup"><span data-stu-id="ffb40-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="ffb40-297">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-298">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-298">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-299">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-299">Name</span></span>|<span data-ttu-id="ffb40-300">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-300">Description</span></span>|<span data-ttu-id="ffb40-301">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-301">Required</span></span>|<span data-ttu-id="ffb40-302">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-303">name</span><span class="sxs-lookup"><span data-stu-id="ffb40-303">name</span></span>|<span data-ttu-id="ffb40-304">The name of the API or operation for which the quota applies.</span><span class="sxs-lookup"><span data-stu-id="ffb40-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="ffb40-305">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-305">Yes</span></span>|<span data-ttu-id="ffb40-306">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-306">N/A</span></span>|  
|<span data-ttu-id="ffb40-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="ffb40-307">bandwidth</span></span>|<span data-ttu-id="ffb40-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-309">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="ffb40-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ffb40-310">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-310">N/A</span></span>|  
|<span data-ttu-id="ffb40-311">calls</span><span class="sxs-lookup"><span data-stu-id="ffb40-311">calls</span></span>|<span data-ttu-id="ffb40-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-313">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="ffb40-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ffb40-314">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-314">N/A</span></span>|  
|<span data-ttu-id="ffb40-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ffb40-315">renewal-period</span></span>|<span data-ttu-id="ffb40-316">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="ffb40-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="ffb40-317">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-317">Yes</span></span>|<span data-ttu-id="ffb40-318">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-319">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-319">Usage</span></span>  
 <span data-ttu-id="ffb40-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-321">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-322">**Policy scopes:** product</span><span class="sxs-lookup"><span data-stu-id="ffb40-322">**Policy scopes:** product</span></span>  
  
##  <a name="SetUsageQuotaByKey"></a> <span data-ttu-id="ffb40-323">Set usage quota by key</span><span class="sxs-lookup"><span data-stu-id="ffb40-323">Set usage quota by key</span></span>  
 <span data-ttu-id="ffb40-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="ffb40-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="ffb40-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="ffb40-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="ffb40-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span><span class="sxs-lookup"><span data-stu-id="ffb40-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="ffb40-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="ffb40-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ffb40-328">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="ffb40-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ffb40-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-330">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ffb40-331">Example</span><span class="sxs-lookup"><span data-stu-id="ffb40-331">Example</span></span>  
 <span data-ttu-id="ffb40-332">In the following example, the quota is keyed by the caller IP address.</span><span class="sxs-lookup"><span data-stu-id="ffb40-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-333">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-333">Elements</span></span>  
  
|<span data-ttu-id="ffb40-334">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-334">Name</span></span>|<span data-ttu-id="ffb40-335">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-335">Description</span></span>|<span data-ttu-id="ffb40-336">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ffb40-337">quota</span><span class="sxs-lookup"><span data-stu-id="ffb40-337">quota</span></span>|<span data-ttu-id="ffb40-338">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-338">Root element.</span></span>|<span data-ttu-id="ffb40-339">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-340">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-340">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-341">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-341">Name</span></span>|<span data-ttu-id="ffb40-342">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-342">Description</span></span>|<span data-ttu-id="ffb40-343">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-343">Required</span></span>|<span data-ttu-id="ffb40-344">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="ffb40-345">bandwidth</span></span>|<span data-ttu-id="ffb40-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-347">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="ffb40-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ffb40-348">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-348">N/A</span></span>|  
|<span data-ttu-id="ffb40-349">calls</span><span class="sxs-lookup"><span data-stu-id="ffb40-349">calls</span></span>|<span data-ttu-id="ffb40-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="ffb40-351">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="ffb40-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ffb40-352">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-352">N/A</span></span>|  
|<span data-ttu-id="ffb40-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="ffb40-353">counter-key</span></span>|<span data-ttu-id="ffb40-354">The key to use for the quota policy.</span><span class="sxs-lookup"><span data-stu-id="ffb40-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="ffb40-355">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-355">Yes</span></span>|<span data-ttu-id="ffb40-356">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-356">N/A</span></span>|  
|<span data-ttu-id="ffb40-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="ffb40-357">increment-condition</span></span>|<span data-ttu-id="ffb40-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span><span class="sxs-lookup"><span data-stu-id="ffb40-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="ffb40-359">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-359">No</span></span>|<span data-ttu-id="ffb40-360">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-360">N/A</span></span>|  
|<span data-ttu-id="ffb40-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ffb40-361">renewal-period</span></span>|<span data-ttu-id="ffb40-362">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="ffb40-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="ffb40-363">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-363">Yes</span></span>|<span data-ttu-id="ffb40-364">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-365">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-365">Usage</span></span>  
 <span data-ttu-id="ffb40-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-367">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-368">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="ValidateJWT"></a> <span data-ttu-id="ffb40-369">Validate JWT</span><span class="sxs-lookup"><span data-stu-id="ffb40-369">Validate JWT</span></span>  
 <span data-ttu-id="ffb40-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span><span class="sxs-lookup"><span data-stu-id="ffb40-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ffb40-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="ffb40-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span><span class="sxs-lookup"><span data-stu-id="ffb40-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="ffb40-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span><span class="sxs-lookup"><span data-stu-id="ffb40-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="ffb40-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span><span class="sxs-lookup"><span data-stu-id="ffb40-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ffb40-375">Policy statement</span><span class="sxs-lookup"><span data-stu-id="ffb40-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="ffb40-376">Examples</span><span class="sxs-lookup"><span data-stu-id="ffb40-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="ffb40-377">Azure Mobile Services token validation</span><span class="sxs-lookup"><span data-stu-id="ffb40-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="ffb40-378">Azure Active Directory token validation</span><span class="sxs-lookup"><span data-stu-id="ffb40-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.windows.net/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="ffb40-379">Authorize access to operations based on token claims</span><span class="sxs-lookup"><span data-stu-id="ffb40-379">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="ffb40-380">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span><span class="sxs-lookup"><span data-stu-id="ffb40-380">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="ffb40-381">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span><span class="sxs-lookup"><span data-stu-id="ffb40-381">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="ffb40-382">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-382">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="ffb40-383">Elements</span><span class="sxs-lookup"><span data-stu-id="ffb40-383">Elements</span></span>  
  
|<span data-ttu-id="ffb40-384">Element</span><span class="sxs-lookup"><span data-stu-id="ffb40-384">Element</span></span>|<span data-ttu-id="ffb40-385">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-385">Description</span></span>|<span data-ttu-id="ffb40-386">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-386">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ffb40-387">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="ffb40-387">validate-jwt</span></span>|<span data-ttu-id="ffb40-388">Root element.</span><span class="sxs-lookup"><span data-stu-id="ffb40-388">Root element.</span></span>|<span data-ttu-id="ffb40-389">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-389">Yes</span></span>|  
|<span data-ttu-id="ffb40-390">audiences</span><span class="sxs-lookup"><span data-stu-id="ffb40-390">audiences</span></span>|<span data-ttu-id="ffb40-391">Contains a list of acceptable audience claims that can be present on the token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-391">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="ffb40-392">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span><span class="sxs-lookup"><span data-stu-id="ffb40-392">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="ffb40-393">At least one audience must be specified.</span><span class="sxs-lookup"><span data-stu-id="ffb40-393">At least one audience must be specified.</span></span>|<span data-ttu-id="ffb40-394">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-394">No</span></span>|  
|<span data-ttu-id="ffb40-395">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="ffb40-395">issuer-signing-keys</span></span>|<span data-ttu-id="ffb40-396">A list of Base64-encoded security keys used to validate signed tokens.</span><span class="sxs-lookup"><span data-stu-id="ffb40-396">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="ffb40-397">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span><span class="sxs-lookup"><span data-stu-id="ffb40-397">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="ffb40-398">Key elements have an optional `id` attribute used to match against `kid` claim.</span><span class="sxs-lookup"><span data-stu-id="ffb40-398">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="ffb40-399">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-399">No</span></span>|  
|<span data-ttu-id="ffb40-400">issuers</span><span class="sxs-lookup"><span data-stu-id="ffb40-400">issuers</span></span>|<span data-ttu-id="ffb40-401">A list of acceptable principals that issued the token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-401">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="ffb40-402">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span><span class="sxs-lookup"><span data-stu-id="ffb40-402">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="ffb40-403">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-403">No</span></span>|  
|<span data-ttu-id="ffb40-404">openid-config</span><span class="sxs-lookup"><span data-stu-id="ffb40-404">openid-config</span></span>|<span data-ttu-id="ffb40-405">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span><span class="sxs-lookup"><span data-stu-id="ffb40-405">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="ffb40-406">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-406">No</span></span>|  
|<span data-ttu-id="ffb40-407">required-claims</span><span class="sxs-lookup"><span data-stu-id="ffb40-407">required-claims</span></span>|<span data-ttu-id="ffb40-408">Contains a list of claims expected to be present on the token for it to be considered valid.</span><span class="sxs-lookup"><span data-stu-id="ffb40-408">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="ffb40-409">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-409">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="ffb40-410">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-410">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="ffb40-411">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-411">No</span></span>|  
|<span data-ttu-id="ffb40-412">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="ffb40-412">zumo-master-key</span></span>|<span data-ttu-id="ffb40-413">Master key for tokens issued by Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="ffb40-413">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="ffb40-414">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-414">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ffb40-415">Attributes</span><span class="sxs-lookup"><span data-stu-id="ffb40-415">Attributes</span></span>  
  
|<span data-ttu-id="ffb40-416">Name</span><span class="sxs-lookup"><span data-stu-id="ffb40-416">Name</span></span>|<span data-ttu-id="ffb40-417">Description</span><span class="sxs-lookup"><span data-stu-id="ffb40-417">Description</span></span>|<span data-ttu-id="ffb40-418">Required</span><span class="sxs-lookup"><span data-stu-id="ffb40-418">Required</span></span>|<span data-ttu-id="ffb40-419">Default</span><span class="sxs-lookup"><span data-stu-id="ffb40-419">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ffb40-420">clock-skew</span><span class="sxs-lookup"><span data-stu-id="ffb40-420">clock-skew</span></span>|<span data-ttu-id="ffb40-421">Timespan.</span><span class="sxs-lookup"><span data-stu-id="ffb40-421">Timespan.</span></span> <span data-ttu-id="ffb40-422">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span><span class="sxs-lookup"><span data-stu-id="ffb40-422">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="ffb40-423">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-423">No</span></span>|<span data-ttu-id="ffb40-424">0 seconds</span><span class="sxs-lookup"><span data-stu-id="ffb40-424">0 seconds</span></span>|  
|<span data-ttu-id="ffb40-425">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="ffb40-425">failed-validation-error-message</span></span>|<span data-ttu-id="ffb40-426">Error message to return in the HTTP response body if the JWT does not pass validation.</span><span class="sxs-lookup"><span data-stu-id="ffb40-426">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="ffb40-427">This message must have any special characters properly escaped.</span><span class="sxs-lookup"><span data-stu-id="ffb40-427">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="ffb40-428">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-428">No</span></span>|<span data-ttu-id="ffb40-429">Default error message depends on validation issue, for example "JWT not present."</span><span class="sxs-lookup"><span data-stu-id="ffb40-429">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="ffb40-430">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="ffb40-430">failed-validation-httpcode</span></span>|<span data-ttu-id="ffb40-431">HTTP Status code to return if the JWT doesn't pass validation.</span><span class="sxs-lookup"><span data-stu-id="ffb40-431">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="ffb40-432">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-432">No</span></span>|<span data-ttu-id="ffb40-433">401</span><span class="sxs-lookup"><span data-stu-id="ffb40-433">401</span></span>|  
|<span data-ttu-id="ffb40-434">header-name</span><span class="sxs-lookup"><span data-stu-id="ffb40-434">header-name</span></span>|<span data-ttu-id="ffb40-435">The name of the HTTP header holding the token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-435">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="ffb40-436">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span><span class="sxs-lookup"><span data-stu-id="ffb40-436">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="ffb40-437">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-437">N/A</span></span>|  
|<span data-ttu-id="ffb40-438">id</span><span class="sxs-lookup"><span data-stu-id="ffb40-438">id</span></span>|<span data-ttu-id="ffb40-439">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span><span class="sxs-lookup"><span data-stu-id="ffb40-439">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="ffb40-440">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-440">No</span></span>|<span data-ttu-id="ffb40-441">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-441">N/A</span></span>|  
|<span data-ttu-id="ffb40-442">match</span><span class="sxs-lookup"><span data-stu-id="ffb40-442">match</span></span>|<span data-ttu-id="ffb40-443">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-443">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="ffb40-444">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="ffb40-444">Possible values are:</span></span><br /><br /> <span data-ttu-id="ffb40-445">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-445">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="ffb40-446">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-446">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="ffb40-447">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-447">No</span></span>|<span data-ttu-id="ffb40-448">all</span><span class="sxs-lookup"><span data-stu-id="ffb40-448">all</span></span>|  
|<span data-ttu-id="ffb40-449">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="ffb40-449">query-paremeter-name</span></span>|<span data-ttu-id="ffb40-450">The name of the the query parameter holding the token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-450">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="ffb40-451">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span><span class="sxs-lookup"><span data-stu-id="ffb40-451">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="ffb40-452">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-452">N/A</span></span>|  
|<span data-ttu-id="ffb40-453">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="ffb40-453">require-expiration-time</span></span>|<span data-ttu-id="ffb40-454">Boolean.</span><span class="sxs-lookup"><span data-stu-id="ffb40-454">Boolean.</span></span> <span data-ttu-id="ffb40-455">Specifies whether an expiration claim is required in the token.</span><span class="sxs-lookup"><span data-stu-id="ffb40-455">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="ffb40-456">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-456">No</span></span>|<span data-ttu-id="ffb40-457">true</span><span class="sxs-lookup"><span data-stu-id="ffb40-457">true</span></span>|
|<span data-ttu-id="ffb40-458">require-scheme</span><span class="sxs-lookup"><span data-stu-id="ffb40-458">require-scheme</span></span>|<span data-ttu-id="ffb40-459">The name of the token scheme, e.g. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="ffb40-459">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="ffb40-460">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span><span class="sxs-lookup"><span data-stu-id="ffb40-460">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="ffb40-461">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-461">No</span></span>|<span data-ttu-id="ffb40-462">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-462">N/A</span></span>|
|<span data-ttu-id="ffb40-463">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="ffb40-463">require-signed-tokens</span></span>|<span data-ttu-id="ffb40-464">Boolean.</span><span class="sxs-lookup"><span data-stu-id="ffb40-464">Boolean.</span></span> <span data-ttu-id="ffb40-465">Specifies whether a token is required to be signed.</span><span class="sxs-lookup"><span data-stu-id="ffb40-465">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="ffb40-466">No</span><span class="sxs-lookup"><span data-stu-id="ffb40-466">No</span></span>|<span data-ttu-id="ffb40-467">true</span><span class="sxs-lookup"><span data-stu-id="ffb40-467">true</span></span>|  
|<span data-ttu-id="ffb40-468">url</span><span class="sxs-lookup"><span data-stu-id="ffb40-468">url</span></span>|<span data-ttu-id="ffb40-469">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span><span class="sxs-lookup"><span data-stu-id="ffb40-469">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="ffb40-470">For Azure Active Directory use the following URL: `https://login.windows.net/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="ffb40-470">For Azure Active Directory use the following URL: `https://login.windows.net/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="ffb40-471">Yes</span><span class="sxs-lookup"><span data-stu-id="ffb40-471">Yes</span></span>|<span data-ttu-id="ffb40-472">N/A</span><span class="sxs-lookup"><span data-stu-id="ffb40-472">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ffb40-473">Usage</span><span class="sxs-lookup"><span data-stu-id="ffb40-473">Usage</span></span>  
 <span data-ttu-id="ffb40-474">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ffb40-474">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ffb40-475">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="ffb40-475">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ffb40-476">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ffb40-476">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ffb40-477">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffb40-477">Next steps</span></span>
<span data-ttu-id="ffb40-478">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ffb40-478">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
