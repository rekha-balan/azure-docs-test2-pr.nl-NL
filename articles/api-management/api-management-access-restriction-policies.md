---
title: Azure API Management access restriction policies | Microsoft Docs
description: Learn about the access restriction policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: apimpm
ms.openlocfilehash: 54bb6056c41126aecada265eb0e079bc7c281be8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827489"
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="22ff3-103">API Management access restriction policies</span><span class="sxs-lookup"><span data-stu-id="22ff3-103">API Management access restriction policies</span></span>
<span data-ttu-id="22ff3-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="22ff3-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="22ff3-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="22ff3-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="AccessRestrictionPolicies"></a> <span data-ttu-id="22ff3-106">Access restriction policies</span><span class="sxs-lookup"><span data-stu-id="22ff3-106">Access restriction policies</span></span>  
  
-   <span data-ttu-id="22ff3-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span><span class="sxs-lookup"><span data-stu-id="22ff3-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
-   <span data-ttu-id="22ff3-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
-   <span data-ttu-id="22ff3-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
-   <span data-ttu-id="22ff3-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span><span class="sxs-lookup"><span data-stu-id="22ff3-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
-   <span data-ttu-id="22ff3-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
-   <span data-ttu-id="22ff3-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
-   <span data-ttu-id="22ff3-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span><span class="sxs-lookup"><span data-stu-id="22ff3-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <a name="CheckHTTPHeader"></a> <span data-ttu-id="22ff3-114">Check HTTP header</span><span class="sxs-lookup"><span data-stu-id="22ff3-114">Check HTTP header</span></span>  
 <span data-ttu-id="22ff3-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span><span class="sxs-lookup"><span data-stu-id="22ff3-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="22ff3-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span><span class="sxs-lookup"><span data-stu-id="22ff3-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="22ff3-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-118">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="true">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-119">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="22ff3-120">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-120">Elements</span></span>  
  
|<span data-ttu-id="22ff3-121">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-121">Name</span></span>|<span data-ttu-id="22ff3-122">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-122">Description</span></span>|<span data-ttu-id="22ff3-123">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-124">check-header</span><span class="sxs-lookup"><span data-stu-id="22ff3-124">check-header</span></span>|<span data-ttu-id="22ff3-125">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-125">Root element.</span></span>|<span data-ttu-id="22ff3-126">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-126">Yes</span></span>|  
|<span data-ttu-id="22ff3-127">value</span><span class="sxs-lookup"><span data-stu-id="22ff3-127">value</span></span>|<span data-ttu-id="22ff3-128">Allowed HTTP header value.</span><span class="sxs-lookup"><span data-stu-id="22ff3-128">Allowed HTTP header value.</span></span> <span data-ttu-id="22ff3-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span><span class="sxs-lookup"><span data-stu-id="22ff3-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="22ff3-130">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-131">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-131">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-132">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-132">Name</span></span>|<span data-ttu-id="22ff3-133">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-133">Description</span></span>|<span data-ttu-id="22ff3-134">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-134">Required</span></span>|<span data-ttu-id="22ff3-135">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="22ff3-136">failed-check-error-message</span></span>|<span data-ttu-id="22ff3-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span><span class="sxs-lookup"><span data-stu-id="22ff3-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="22ff3-138">This message must have any special characters properly escaped.</span><span class="sxs-lookup"><span data-stu-id="22ff3-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="22ff3-139">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-139">Yes</span></span>|<span data-ttu-id="22ff3-140">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-140">N/A</span></span>|  
|<span data-ttu-id="22ff3-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="22ff3-141">failed-check-httpcode</span></span>|<span data-ttu-id="22ff3-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span><span class="sxs-lookup"><span data-stu-id="22ff3-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="22ff3-143">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-143">Yes</span></span>|<span data-ttu-id="22ff3-144">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-144">N/A</span></span>|  
|<span data-ttu-id="22ff3-145">header-name</span><span class="sxs-lookup"><span data-stu-id="22ff3-145">header-name</span></span>|<span data-ttu-id="22ff3-146">The name of the HTTP Header to check.</span><span class="sxs-lookup"><span data-stu-id="22ff3-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="22ff3-147">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-147">Yes</span></span>|<span data-ttu-id="22ff3-148">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-148">N/A</span></span>|  
|<span data-ttu-id="22ff3-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="22ff3-149">ignore-case</span></span>|<span data-ttu-id="22ff3-150">Can be set to True or False.</span><span class="sxs-lookup"><span data-stu-id="22ff3-150">Can be set to True or False.</span></span> <span data-ttu-id="22ff3-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span><span class="sxs-lookup"><span data-stu-id="22ff3-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="22ff3-152">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-152">Yes</span></span>|<span data-ttu-id="22ff3-153">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-154">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-154">Usage</span></span>  
 <span data-ttu-id="22ff3-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-156">**Policy sections:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="22ff3-157">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="LimitCallRate"></a> <span data-ttu-id="22ff3-158">Limit call rate by subscription</span><span class="sxs-lookup"><span data-stu-id="22ff3-158">Limit call rate by subscription</span></span>  
 <span data-ttu-id="22ff3-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span><span class="sxs-lookup"><span data-stu-id="22ff3-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="22ff3-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span><span class="sxs-lookup"><span data-stu-id="22ff3-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="22ff3-161">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="22ff3-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="22ff3-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-163">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="API name" id="API id" calls="number" renewal-period="seconds" />  
        <operation name="operation name" id="operation id" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-164">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="22ff3-165">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-165">Elements</span></span>  
  
|<span data-ttu-id="22ff3-166">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-166">Name</span></span>|<span data-ttu-id="22ff3-167">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-167">Description</span></span>|<span data-ttu-id="22ff3-168">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="22ff3-169">set-limit</span></span>|<span data-ttu-id="22ff3-170">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-170">Root element.</span></span>|<span data-ttu-id="22ff3-171">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-171">Yes</span></span>|  
|<span data-ttu-id="22ff3-172">api</span><span class="sxs-lookup"><span data-stu-id="22ff3-172">api</span></span>|<span data-ttu-id="22ff3-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span><span class="sxs-lookup"><span data-stu-id="22ff3-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="22ff3-174">Product and API call rate limits are applied independently.</span><span class="sxs-lookup"><span data-stu-id="22ff3-174">Product and API call rate limits are applied independently.</span></span> <span data-ttu-id="22ff3-175">API can be referenced either via `name` or `id`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-175">API can be referenced either via `name` or `id`.</span></span> <span data-ttu-id="22ff3-176">If both attributes are provided, `id` will be used and `name` will be ignored.</span><span class="sxs-lookup"><span data-stu-id="22ff3-176">If both attributes are provided, `id` will be used and `name` will be ignored.</span></span>|<span data-ttu-id="22ff3-177">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-177">No</span></span>|  
|<span data-ttu-id="22ff3-178">operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-178">operation</span></span>|<span data-ttu-id="22ff3-179">Add one  or more of these elements to impose a call rate limit on operations within an API.</span><span class="sxs-lookup"><span data-stu-id="22ff3-179">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="22ff3-180">Product, API, and operation call rate limits are applied independently.</span><span class="sxs-lookup"><span data-stu-id="22ff3-180">Product, API, and operation call rate limits are applied independently.</span></span> <span data-ttu-id="22ff3-181">Operation can be referenced either via `name` or `id`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-181">Operation can be referenced either via `name` or `id`.</span></span> <span data-ttu-id="22ff3-182">If both attributes are provided, `id` will be used and `name` will be ignored.</span><span class="sxs-lookup"><span data-stu-id="22ff3-182">If both attributes are provided, `id` will be used and `name` will be ignored.</span></span>|<span data-ttu-id="22ff3-183">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-183">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-184">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-184">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-185">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-185">Name</span></span>|<span data-ttu-id="22ff3-186">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-186">Description</span></span>|<span data-ttu-id="22ff3-187">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-187">Required</span></span>|<span data-ttu-id="22ff3-188">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-188">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-189">name</span><span class="sxs-lookup"><span data-stu-id="22ff3-189">name</span></span>|<span data-ttu-id="22ff3-190">The name of the API for which to apply the rate limit.</span><span class="sxs-lookup"><span data-stu-id="22ff3-190">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="22ff3-191">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-191">Yes</span></span>|<span data-ttu-id="22ff3-192">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-192">N/A</span></span>|  
|<span data-ttu-id="22ff3-193">calls</span><span class="sxs-lookup"><span data-stu-id="22ff3-193">calls</span></span>|<span data-ttu-id="22ff3-194">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-194">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-195">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-195">Yes</span></span>|<span data-ttu-id="22ff3-196">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-196">N/A</span></span>|  
|<span data-ttu-id="22ff3-197">renewal-period</span><span class="sxs-lookup"><span data-stu-id="22ff3-197">renewal-period</span></span>|<span data-ttu-id="22ff3-198">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="22ff3-198">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="22ff3-199">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-199">Yes</span></span>|<span data-ttu-id="22ff3-200">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-200">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-201">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-201">Usage</span></span>  
 <span data-ttu-id="22ff3-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-203">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-203">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="22ff3-204">**Policy scopes:** product</span><span class="sxs-lookup"><span data-stu-id="22ff3-204">**Policy scopes:** product</span></span>  
  
##  <a name="LimitCallRateByKey"></a> <span data-ttu-id="22ff3-205">Limit call rate by key</span><span class="sxs-lookup"><span data-stu-id="22ff3-205">Limit call rate by key</span></span>  
 <span data-ttu-id="22ff3-206">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span><span class="sxs-lookup"><span data-stu-id="22ff3-206">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="22ff3-207">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="22ff3-207">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="22ff3-208">Optional increment condition can be added to specify which requests should be counted towards the limit.</span><span class="sxs-lookup"><span data-stu-id="22ff3-208">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="22ff3-209">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span><span class="sxs-lookup"><span data-stu-id="22ff3-209">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="22ff3-210">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="22ff3-210">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="22ff3-211">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="22ff3-211">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-212">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-212">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-213">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-213">Example</span></span>  
 <span data-ttu-id="22ff3-214">In the following example, the rate limit is keyed by the caller IP address.</span><span class="sxs-lookup"><span data-stu-id="22ff3-214">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="22ff3-215">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-215">Elements</span></span>  
  
|<span data-ttu-id="22ff3-216">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-216">Name</span></span>|<span data-ttu-id="22ff3-217">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-217">Description</span></span>|<span data-ttu-id="22ff3-218">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-218">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-219">set-limit</span><span class="sxs-lookup"><span data-stu-id="22ff3-219">set-limit</span></span>|<span data-ttu-id="22ff3-220">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-220">Root element.</span></span>|<span data-ttu-id="22ff3-221">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-221">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-222">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-222">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-223">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-223">Name</span></span>|<span data-ttu-id="22ff3-224">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-224">Description</span></span>|<span data-ttu-id="22ff3-225">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-225">Required</span></span>|<span data-ttu-id="22ff3-226">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-226">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-227">calls</span><span class="sxs-lookup"><span data-stu-id="22ff3-227">calls</span></span>|<span data-ttu-id="22ff3-228">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-228">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-229">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-229">Yes</span></span>|<span data-ttu-id="22ff3-230">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-230">N/A</span></span>|  
|<span data-ttu-id="22ff3-231">counter-key</span><span class="sxs-lookup"><span data-stu-id="22ff3-231">counter-key</span></span>|<span data-ttu-id="22ff3-232">The key to use for the rate limit policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-232">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="22ff3-233">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-233">Yes</span></span>|<span data-ttu-id="22ff3-234">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-234">N/A</span></span>|  
|<span data-ttu-id="22ff3-235">increment-condition</span><span class="sxs-lookup"><span data-stu-id="22ff3-235">increment-condition</span></span>|<span data-ttu-id="22ff3-236">The boolean expression specifying if the request should be counted towards the quota (`true`).</span><span class="sxs-lookup"><span data-stu-id="22ff3-236">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="22ff3-237">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-237">No</span></span>|<span data-ttu-id="22ff3-238">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-238">N/A</span></span>|  
|<span data-ttu-id="22ff3-239">renewal-period</span><span class="sxs-lookup"><span data-stu-id="22ff3-239">renewal-period</span></span>|<span data-ttu-id="22ff3-240">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="22ff3-240">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="22ff3-241">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-241">Yes</span></span>|<span data-ttu-id="22ff3-242">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-242">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-243">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-243">Usage</span></span>  
 <span data-ttu-id="22ff3-244">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-244">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-245">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-245">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="22ff3-246">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-246">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="RestrictCallerIPs"></a> <span data-ttu-id="22ff3-247">Restrict caller IPs</span><span class="sxs-lookup"><span data-stu-id="22ff3-247">Restrict caller IPs</span></span>  
 <span data-ttu-id="22ff3-248">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span><span class="sxs-lookup"><span data-stu-id="22ff3-248">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-249">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-249">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-250">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-250">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="22ff3-251">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-251">Elements</span></span>  
  
|<span data-ttu-id="22ff3-252">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-252">Name</span></span>|<span data-ttu-id="22ff3-253">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-253">Description</span></span>|<span data-ttu-id="22ff3-254">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-254">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-255">ip-filter</span><span class="sxs-lookup"><span data-stu-id="22ff3-255">ip-filter</span></span>|<span data-ttu-id="22ff3-256">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-256">Root element.</span></span>|<span data-ttu-id="22ff3-257">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-257">Yes</span></span>|  
|<span data-ttu-id="22ff3-258">address</span><span class="sxs-lookup"><span data-stu-id="22ff3-258">address</span></span>|<span data-ttu-id="22ff3-259">Specifies a single IP address on which to filter.</span><span class="sxs-lookup"><span data-stu-id="22ff3-259">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="22ff3-260">At least one `address` or `address-range` element is required.</span><span class="sxs-lookup"><span data-stu-id="22ff3-260">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="22ff3-261">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="22ff3-261">address-range from="address" to="address"</span></span>|<span data-ttu-id="22ff3-262">Specifies a range of IP address on which to filter.</span><span class="sxs-lookup"><span data-stu-id="22ff3-262">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="22ff3-263">At least one `address` or `address-range` element is required.</span><span class="sxs-lookup"><span data-stu-id="22ff3-263">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-264">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-264">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-265">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-265">Name</span></span>|<span data-ttu-id="22ff3-266">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-266">Description</span></span>|<span data-ttu-id="22ff3-267">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-267">Required</span></span>|<span data-ttu-id="22ff3-268">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-268">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-269">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="22ff3-269">address-range from="address" to="address"</span></span>|<span data-ttu-id="22ff3-270">A range of IP addresses to allow or deny access for.</span><span class="sxs-lookup"><span data-stu-id="22ff3-270">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="22ff3-271">Required when the `address-range` element is used.</span><span class="sxs-lookup"><span data-stu-id="22ff3-271">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="22ff3-272">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-272">N/A</span></span>|  
|<span data-ttu-id="22ff3-273">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="22ff3-273">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="22ff3-274">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span><span class="sxs-lookup"><span data-stu-id="22ff3-274">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="22ff3-275">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-275">Yes</span></span>|<span data-ttu-id="22ff3-276">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-276">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-277">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-277">Usage</span></span>  
 <span data-ttu-id="22ff3-278">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-278">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-279">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-279">**Policy sections:** inbound</span></span>  
-   <span data-ttu-id="22ff3-280">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-280">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetUsageQuota"></a> <span data-ttu-id="22ff3-281">Set usage quota by subscription</span><span class="sxs-lookup"><span data-stu-id="22ff3-281">Set usage quota by subscription</span></span>  
 <span data-ttu-id="22ff3-282">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-282">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="22ff3-283">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="22ff3-283">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="22ff3-284">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-284">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-285">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-285">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="API name" id="API id" calls="number" renewal-period="seconds" />  
        <operation name="operation name" id="operation id" calls="number" renewal-period="seconds" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-286">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-286">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="22ff3-287">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-287">Elements</span></span>  
  
|<span data-ttu-id="22ff3-288">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-288">Name</span></span>|<span data-ttu-id="22ff3-289">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-289">Description</span></span>|<span data-ttu-id="22ff3-290">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-290">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-291">quota</span><span class="sxs-lookup"><span data-stu-id="22ff3-291">quota</span></span>|<span data-ttu-id="22ff3-292">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-292">Root element.</span></span>|<span data-ttu-id="22ff3-293">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-293">Yes</span></span>|  
|<span data-ttu-id="22ff3-294">api</span><span class="sxs-lookup"><span data-stu-id="22ff3-294">api</span></span>|<span data-ttu-id="22ff3-295">Add one  or more of these elements to impose call quota on APIs within the product.</span><span class="sxs-lookup"><span data-stu-id="22ff3-295">Add one  or more of these elements to impose call quota on APIs within the product.</span></span> <span data-ttu-id="22ff3-296">Product and API call quotas are applied independently.</span><span class="sxs-lookup"><span data-stu-id="22ff3-296">Product and API call quotas are applied independently.</span></span> <span data-ttu-id="22ff3-297">API can be referenced either via `name` or `id`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-297">API can be referenced either via `name` or `id`.</span></span> <span data-ttu-id="22ff3-298">If both attributes are provided, `id` will be used and `name` will be ignored.</span><span class="sxs-lookup"><span data-stu-id="22ff3-298">If both attributes are provided, `id` will be used and `name` will be ignored.</span></span>|<span data-ttu-id="22ff3-299">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-299">No</span></span>|  
|<span data-ttu-id="22ff3-300">operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-300">operation</span></span>|<span data-ttu-id="22ff3-301">Add one  or more of these elements to impose call quota on operations within an API.</span><span class="sxs-lookup"><span data-stu-id="22ff3-301">Add one  or more of these elements to impose call quota on operations within an API.</span></span> <span data-ttu-id="22ff3-302">Product, API, and operation call quotas are applied independently.</span><span class="sxs-lookup"><span data-stu-id="22ff3-302">Product, API, and operation call quotas are applied independently.</span></span> <span data-ttu-id="22ff3-303">Operation can be referenced either via `name` or `id`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-303">Operation can be referenced either via `name` or `id`.</span></span> <span data-ttu-id="22ff3-304">If both attributes are provided, `id` will be used and `name` will be ignored.</span><span class="sxs-lookup"><span data-stu-id="22ff3-304">If both attributes are provided, `id` will be used and `name` will be ignored.</span></span>|<span data-ttu-id="22ff3-305">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-305">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-306">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-306">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-307">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-307">Name</span></span>|<span data-ttu-id="22ff3-308">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-308">Description</span></span>|<span data-ttu-id="22ff3-309">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-309">Required</span></span>|<span data-ttu-id="22ff3-310">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-310">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-311">name</span><span class="sxs-lookup"><span data-stu-id="22ff3-311">name</span></span>|<span data-ttu-id="22ff3-312">The name of the API or operation for which the quota applies.</span><span class="sxs-lookup"><span data-stu-id="22ff3-312">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="22ff3-313">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-313">Yes</span></span>|<span data-ttu-id="22ff3-314">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-314">N/A</span></span>|  
|<span data-ttu-id="22ff3-315">bandwidth</span><span class="sxs-lookup"><span data-stu-id="22ff3-315">bandwidth</span></span>|<span data-ttu-id="22ff3-316">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-316">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-317">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="22ff3-317">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="22ff3-318">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-318">N/A</span></span>|  
|<span data-ttu-id="22ff3-319">calls</span><span class="sxs-lookup"><span data-stu-id="22ff3-319">calls</span></span>|<span data-ttu-id="22ff3-320">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-320">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-321">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="22ff3-321">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="22ff3-322">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-322">N/A</span></span>|  
|<span data-ttu-id="22ff3-323">renewal-period</span><span class="sxs-lookup"><span data-stu-id="22ff3-323">renewal-period</span></span>|<span data-ttu-id="22ff3-324">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="22ff3-324">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="22ff3-325">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-325">Yes</span></span>|<span data-ttu-id="22ff3-326">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-326">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-327">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-327">Usage</span></span>  
 <span data-ttu-id="22ff3-328">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-328">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-329">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-329">**Policy sections:** inbound</span></span>  
-   <span data-ttu-id="22ff3-330">**Policy scopes:** product</span><span class="sxs-lookup"><span data-stu-id="22ff3-330">**Policy scopes:** product</span></span>  
  
##  <a name="SetUsageQuotaByKey"></a> <span data-ttu-id="22ff3-331">Set usage quota by key</span><span class="sxs-lookup"><span data-stu-id="22ff3-331">Set usage quota by key</span></span>  
 <span data-ttu-id="22ff3-332">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span><span class="sxs-lookup"><span data-stu-id="22ff3-332">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="22ff3-333">The key can have an arbitrary string value and is typically provided using a policy expression.</span><span class="sxs-lookup"><span data-stu-id="22ff3-333">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="22ff3-334">Optional increment condition can be added to specify which requests should be counted towards the quota.</span><span class="sxs-lookup"><span data-stu-id="22ff3-334">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="22ff3-335">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="22ff3-335">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="22ff3-336">This policy can be used only once per policy document.</span><span class="sxs-lookup"><span data-stu-id="22ff3-336">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="22ff3-337">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-337">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-338">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-338">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="22ff3-339">Example</span><span class="sxs-lookup"><span data-stu-id="22ff3-339">Example</span></span>  
 <span data-ttu-id="22ff3-340">In the following example, the quota is keyed by the caller IP address.</span><span class="sxs-lookup"><span data-stu-id="22ff3-340">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="22ff3-341">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-341">Elements</span></span>  
  
|<span data-ttu-id="22ff3-342">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-342">Name</span></span>|<span data-ttu-id="22ff3-343">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-343">Description</span></span>|<span data-ttu-id="22ff3-344">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-344">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="22ff3-345">quota</span><span class="sxs-lookup"><span data-stu-id="22ff3-345">quota</span></span>|<span data-ttu-id="22ff3-346">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-346">Root element.</span></span>|<span data-ttu-id="22ff3-347">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-347">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-348">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-348">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-349">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-349">Name</span></span>|<span data-ttu-id="22ff3-350">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-350">Description</span></span>|<span data-ttu-id="22ff3-351">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-351">Required</span></span>|<span data-ttu-id="22ff3-352">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-352">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-353">bandwidth</span><span class="sxs-lookup"><span data-stu-id="22ff3-353">bandwidth</span></span>|<span data-ttu-id="22ff3-354">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-354">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-355">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="22ff3-355">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="22ff3-356">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-356">N/A</span></span>|  
|<span data-ttu-id="22ff3-357">calls</span><span class="sxs-lookup"><span data-stu-id="22ff3-357">calls</span></span>|<span data-ttu-id="22ff3-358">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-358">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="22ff3-359">Either `calls`, `bandwidth`, or both together must be specified.</span><span class="sxs-lookup"><span data-stu-id="22ff3-359">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="22ff3-360">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-360">N/A</span></span>|  
|<span data-ttu-id="22ff3-361">counter-key</span><span class="sxs-lookup"><span data-stu-id="22ff3-361">counter-key</span></span>|<span data-ttu-id="22ff3-362">The key to use for the quota policy.</span><span class="sxs-lookup"><span data-stu-id="22ff3-362">The key to use for the quota policy.</span></span>|<span data-ttu-id="22ff3-363">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-363">Yes</span></span>|<span data-ttu-id="22ff3-364">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-364">N/A</span></span>|  
|<span data-ttu-id="22ff3-365">increment-condition</span><span class="sxs-lookup"><span data-stu-id="22ff3-365">increment-condition</span></span>|<span data-ttu-id="22ff3-366">The boolean expression specifying if the request should be counted towards the quota (`true`)</span><span class="sxs-lookup"><span data-stu-id="22ff3-366">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="22ff3-367">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-367">No</span></span>|<span data-ttu-id="22ff3-368">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-368">N/A</span></span>|  
|<span data-ttu-id="22ff3-369">renewal-period</span><span class="sxs-lookup"><span data-stu-id="22ff3-369">renewal-period</span></span>|<span data-ttu-id="22ff3-370">The time period in seconds after which the quota resets.</span><span class="sxs-lookup"><span data-stu-id="22ff3-370">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="22ff3-371">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-371">Yes</span></span>|<span data-ttu-id="22ff3-372">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-372">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-373">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-373">Usage</span></span>  
 <span data-ttu-id="22ff3-374">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-374">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-375">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-375">**Policy sections:** inbound</span></span>  
-   <span data-ttu-id="22ff3-376">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-376">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="ValidateJWT"></a> <span data-ttu-id="22ff3-377">Validate JWT</span><span class="sxs-lookup"><span data-stu-id="22ff3-377">Validate JWT</span></span>  
 <span data-ttu-id="22ff3-378">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span><span class="sxs-lookup"><span data-stu-id="22ff3-378">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="22ff3-379">The `validate-jwt` policy requires that the `exp` registered claim is included in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-379">The `validate-jwt` policy requires that the `exp` registered claim is included in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="22ff3-380">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span><span class="sxs-lookup"><span data-stu-id="22ff3-380">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="22ff3-381">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span><span class="sxs-lookup"><span data-stu-id="22ff3-381">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="22ff3-382">For RS256 the key has to be provide via an Open ID configuration endpoint.</span><span class="sxs-lookup"><span data-stu-id="22ff3-382">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="22ff3-383">Policy statement</span><span class="sxs-lookup"><span data-stu-id="22ff3-383">Policy statement</span></span>  
  
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
    <claim name="name of the claim as it appears in the token" match="all|any" separator="separator character in a multi-valued claim">
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="22ff3-384">Examples</span><span class="sxs-lookup"><span data-stu-id="22ff3-384">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="22ff3-385">Azure Mobile Services token validation</span><span class="sxs-lookup"><span data-stu-id="22ff3-385">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="22ff3-386">Azure Active Directory token validation</span><span class="sxs-lookup"><span data-stu-id="22ff3-386">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="22ff3-387">Azure Active Directory B2C token validation</span><span class="sxs-lookup"><span data-stu-id="22ff3-387">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="22ff3-388">Authorize access to operations based on token claims</span><span class="sxs-lookup"><span data-stu-id="22ff3-388">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="22ff3-389">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span><span class="sxs-lookup"><span data-stu-id="22ff3-389">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="22ff3-390">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span><span class="sxs-lookup"><span data-stu-id="22ff3-390">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="22ff3-391">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-391">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="22ff3-392">Elements</span><span class="sxs-lookup"><span data-stu-id="22ff3-392">Elements</span></span>  
  
|<span data-ttu-id="22ff3-393">Element</span><span class="sxs-lookup"><span data-stu-id="22ff3-393">Element</span></span>|<span data-ttu-id="22ff3-394">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-394">Description</span></span>|<span data-ttu-id="22ff3-395">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-395">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="22ff3-396">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="22ff3-396">validate-jwt</span></span>|<span data-ttu-id="22ff3-397">Root element.</span><span class="sxs-lookup"><span data-stu-id="22ff3-397">Root element.</span></span>|<span data-ttu-id="22ff3-398">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-398">Yes</span></span>|  
|<span data-ttu-id="22ff3-399">audiences</span><span class="sxs-lookup"><span data-stu-id="22ff3-399">audiences</span></span>|<span data-ttu-id="22ff3-400">Contains a list of acceptable audience claims that can be present on the token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-400">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="22ff3-401">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span><span class="sxs-lookup"><span data-stu-id="22ff3-401">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="22ff3-402">At least one audience must be specified.</span><span class="sxs-lookup"><span data-stu-id="22ff3-402">At least one audience must be specified.</span></span>|<span data-ttu-id="22ff3-403">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-403">No</span></span>|  
|<span data-ttu-id="22ff3-404">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="22ff3-404">issuer-signing-keys</span></span>|<span data-ttu-id="22ff3-405">A list of Base64-encoded security keys used to validate signed tokens.</span><span class="sxs-lookup"><span data-stu-id="22ff3-405">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="22ff3-406">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span><span class="sxs-lookup"><span data-stu-id="22ff3-406">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="22ff3-407">Key elements have an optional `id` attribute used to match against `kid` claim.</span><span class="sxs-lookup"><span data-stu-id="22ff3-407">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="22ff3-408">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-408">No</span></span>|  
|<span data-ttu-id="22ff3-409">issuers</span><span class="sxs-lookup"><span data-stu-id="22ff3-409">issuers</span></span>|<span data-ttu-id="22ff3-410">A list of acceptable principals that issued the token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-410">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="22ff3-411">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span><span class="sxs-lookup"><span data-stu-id="22ff3-411">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="22ff3-412">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-412">No</span></span>|  
|<span data-ttu-id="22ff3-413">openid-config</span><span class="sxs-lookup"><span data-stu-id="22ff3-413">openid-config</span></span>|<span data-ttu-id="22ff3-414">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span><span class="sxs-lookup"><span data-stu-id="22ff3-414">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="22ff3-415">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-415">No</span></span>|  
|<span data-ttu-id="22ff3-416">required-claims</span><span class="sxs-lookup"><span data-stu-id="22ff3-416">required-claims</span></span>|<span data-ttu-id="22ff3-417">Contains a list of claims expected to be present on the token for it to be considered valid.</span><span class="sxs-lookup"><span data-stu-id="22ff3-417">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="22ff3-418">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-418">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="22ff3-419">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-419">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="22ff3-420">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-420">No</span></span>|  
|<span data-ttu-id="22ff3-421">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="22ff3-421">zumo-master-key</span></span>|<span data-ttu-id="22ff3-422">Master key for tokens issued by Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="22ff3-422">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="22ff3-423">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-423">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="22ff3-424">Attributes</span><span class="sxs-lookup"><span data-stu-id="22ff3-424">Attributes</span></span>  
  
|<span data-ttu-id="22ff3-425">Name</span><span class="sxs-lookup"><span data-stu-id="22ff3-425">Name</span></span>|<span data-ttu-id="22ff3-426">Description</span><span class="sxs-lookup"><span data-stu-id="22ff3-426">Description</span></span>|<span data-ttu-id="22ff3-427">Required</span><span class="sxs-lookup"><span data-stu-id="22ff3-427">Required</span></span>|<span data-ttu-id="22ff3-428">Default</span><span class="sxs-lookup"><span data-stu-id="22ff3-428">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="22ff3-429">clock-skew</span><span class="sxs-lookup"><span data-stu-id="22ff3-429">clock-skew</span></span>|<span data-ttu-id="22ff3-430">Timespan.</span><span class="sxs-lookup"><span data-stu-id="22ff3-430">Timespan.</span></span> <span data-ttu-id="22ff3-431">Use to specify maximum expected time difference between the system clocks of the token issuer and the API Management instance.</span><span class="sxs-lookup"><span data-stu-id="22ff3-431">Use to specify maximum expected time difference between the system clocks of the token issuer and the API Management instance.</span></span>|<span data-ttu-id="22ff3-432">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-432">No</span></span>|<span data-ttu-id="22ff3-433">0 seconds</span><span class="sxs-lookup"><span data-stu-id="22ff3-433">0 seconds</span></span>|  
|<span data-ttu-id="22ff3-434">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="22ff3-434">failed-validation-error-message</span></span>|<span data-ttu-id="22ff3-435">Error message to return in the HTTP response body if the JWT does not pass validation.</span><span class="sxs-lookup"><span data-stu-id="22ff3-435">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="22ff3-436">This message must have any special characters properly escaped.</span><span class="sxs-lookup"><span data-stu-id="22ff3-436">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="22ff3-437">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-437">No</span></span>|<span data-ttu-id="22ff3-438">Default error message depends on validation issue, for example "JWT not present."</span><span class="sxs-lookup"><span data-stu-id="22ff3-438">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="22ff3-439">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="22ff3-439">failed-validation-httpcode</span></span>|<span data-ttu-id="22ff3-440">HTTP Status code to return if the JWT doesn't pass validation.</span><span class="sxs-lookup"><span data-stu-id="22ff3-440">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="22ff3-441">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-441">No</span></span>|<span data-ttu-id="22ff3-442">401</span><span class="sxs-lookup"><span data-stu-id="22ff3-442">401</span></span>|  
|<span data-ttu-id="22ff3-443">header-name</span><span class="sxs-lookup"><span data-stu-id="22ff3-443">header-name</span></span>|<span data-ttu-id="22ff3-444">The name of the HTTP header holding the token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-444">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="22ff3-445">Either `header-name` or `query-parameter-name` must be specified; but not both.</span><span class="sxs-lookup"><span data-stu-id="22ff3-445">Either `header-name` or `query-parameter-name` must be specified; but not both.</span></span>|<span data-ttu-id="22ff3-446">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-446">N/A</span></span>|  
|<span data-ttu-id="22ff3-447">id</span><span class="sxs-lookup"><span data-stu-id="22ff3-447">id</span></span>|<span data-ttu-id="22ff3-448">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span><span class="sxs-lookup"><span data-stu-id="22ff3-448">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="22ff3-449">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-449">No</span></span>|<span data-ttu-id="22ff3-450">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-450">N/A</span></span>|  
|<span data-ttu-id="22ff3-451">match</span><span class="sxs-lookup"><span data-stu-id="22ff3-451">match</span></span>|<span data-ttu-id="22ff3-452">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-452">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="22ff3-453">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="22ff3-453">Possible values are:</span></span><br /><br /> <span data-ttu-id="22ff3-454">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-454">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="22ff3-455">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-455">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="22ff3-456">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-456">No</span></span>|<span data-ttu-id="22ff3-457">all</span><span class="sxs-lookup"><span data-stu-id="22ff3-457">all</span></span>|  
|<span data-ttu-id="22ff3-458">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="22ff3-458">query-paremeter-name</span></span>|<span data-ttu-id="22ff3-459">The name of the query parameter holding the token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-459">The name of the query parameter holding the token.</span></span>|<span data-ttu-id="22ff3-460">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span><span class="sxs-lookup"><span data-stu-id="22ff3-460">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="22ff3-461">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-461">N/A</span></span>|  
|<span data-ttu-id="22ff3-462">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="22ff3-462">require-expiration-time</span></span>|<span data-ttu-id="22ff3-463">Boolean.</span><span class="sxs-lookup"><span data-stu-id="22ff3-463">Boolean.</span></span> <span data-ttu-id="22ff3-464">Specifies whether an expiration claim is required in the token.</span><span class="sxs-lookup"><span data-stu-id="22ff3-464">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="22ff3-465">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-465">No</span></span>|<span data-ttu-id="22ff3-466">true</span><span class="sxs-lookup"><span data-stu-id="22ff3-466">true</span></span>|
|<span data-ttu-id="22ff3-467">require-scheme</span><span class="sxs-lookup"><span data-stu-id="22ff3-467">require-scheme</span></span>|<span data-ttu-id="22ff3-468">The name of the token scheme, e.g. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="22ff3-468">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="22ff3-469">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span><span class="sxs-lookup"><span data-stu-id="22ff3-469">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="22ff3-470">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-470">No</span></span>|<span data-ttu-id="22ff3-471">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-471">N/A</span></span>|
|<span data-ttu-id="22ff3-472">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="22ff3-472">require-signed-tokens</span></span>|<span data-ttu-id="22ff3-473">Boolean.</span><span class="sxs-lookup"><span data-stu-id="22ff3-473">Boolean.</span></span> <span data-ttu-id="22ff3-474">Specifies whether a token is required to be signed.</span><span class="sxs-lookup"><span data-stu-id="22ff3-474">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="22ff3-475">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-475">No</span></span>|<span data-ttu-id="22ff3-476">true</span><span class="sxs-lookup"><span data-stu-id="22ff3-476">true</span></span>|  
|<span data-ttu-id="22ff3-477">separator</span><span class="sxs-lookup"><span data-stu-id="22ff3-477">separator</span></span>|<span data-ttu-id="22ff3-478">String.</span><span class="sxs-lookup"><span data-stu-id="22ff3-478">String.</span></span> <span data-ttu-id="22ff3-479">Specifies a separator (e.g. ",") to be used for extracting a set of values from a multi-valued claim.</span><span class="sxs-lookup"><span data-stu-id="22ff3-479">Specifies a separator (e.g. ",") to be used for extracting a set of values from a multi-valued claim.</span></span>|<span data-ttu-id="22ff3-480">No</span><span class="sxs-lookup"><span data-stu-id="22ff3-480">No</span></span>|<span data-ttu-id="22ff3-481">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-481">N/A</span></span>| 
|<span data-ttu-id="22ff3-482">url</span><span class="sxs-lookup"><span data-stu-id="22ff3-482">url</span></span>|<span data-ttu-id="22ff3-483">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span><span class="sxs-lookup"><span data-stu-id="22ff3-483">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="22ff3-484">The response should be according to specs as defined at URL:`https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-484">The response should be according to specs as defined at URL:`https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata`.</span></span>  <span data-ttu-id="22ff3-485">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="22ff3-485">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="22ff3-486">Yes</span><span class="sxs-lookup"><span data-stu-id="22ff3-486">Yes</span></span>|<span data-ttu-id="22ff3-487">N/A</span><span class="sxs-lookup"><span data-stu-id="22ff3-487">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="22ff3-488">Usage</span><span class="sxs-lookup"><span data-stu-id="22ff3-488">Usage</span></span>  
 <span data-ttu-id="22ff3-489">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="22ff3-489">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="22ff3-490">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="22ff3-490">**Policy sections:** inbound</span></span>  
-   <span data-ttu-id="22ff3-491">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="22ff3-491">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="22ff3-492">Next steps</span><span class="sxs-lookup"><span data-stu-id="22ff3-492">Next steps</span></span>

<span data-ttu-id="22ff3-493">For more information working with policies, see:</span><span class="sxs-lookup"><span data-stu-id="22ff3-493">For more information working with policies, see:</span></span>

+ [<span data-ttu-id="22ff3-494">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="22ff3-494">Policies in API Management</span></span>](api-management-howto-policies.md)
+ [<span data-ttu-id="22ff3-495">Transform APIs</span><span class="sxs-lookup"><span data-stu-id="22ff3-495">Transform APIs</span></span>](transform-api.md)
+ <span data-ttu-id="22ff3-496">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span><span class="sxs-lookup"><span data-stu-id="22ff3-496">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span></span>
+ [<span data-ttu-id="22ff3-497">Policy samples</span><span class="sxs-lookup"><span data-stu-id="22ff3-497">Policy samples</span></span>](policy-samples.md)   
