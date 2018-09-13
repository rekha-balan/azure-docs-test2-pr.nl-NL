---
title: Azure CDN rules engine match conditions | Microsoft Docs
description: Reference documentation for Azure Content Delivery Network rules engine match conditions.
services: cdn
documentationcenter: ''
author: Lichard
manager: akucer
editor: ''
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2017
ms.author: rli
ms.openlocfilehash: f8dac5469e7160fae93e8251ab7f4195a383f8b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818667"
---
# <a name="azure-cdn-rules-engine-match-conditions"></a><span data-ttu-id="09430-103">Azure CDN rules engine match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-103">Azure CDN rules engine match conditions</span></span> 
<span data-ttu-id="09430-104">This article lists detailed descriptions of the available match conditions for the Azure Content Delivery Network (CDN) [rules engine](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="09430-104">This article lists detailed descriptions of the available match conditions for the Azure Content Delivery Network (CDN) [rules engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="09430-105">The second part of a rule is the match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-105">The second part of a rule is the match condition.</span></span> <span data-ttu-id="09430-106">A match condition identifies specific types of requests for which a set of features will be performed.</span><span class="sxs-lookup"><span data-stu-id="09430-106">A match condition identifies specific types of requests for which a set of features will be performed.</span></span>

<span data-ttu-id="09430-107">For example, you can use a match condition to:</span><span class="sxs-lookup"><span data-stu-id="09430-107">For example, you can use a match condition to:</span></span>
- <span data-ttu-id="09430-108">Filter requests for content at a particular location.</span><span class="sxs-lookup"><span data-stu-id="09430-108">Filter requests for content at a particular location.</span></span>
- <span data-ttu-id="09430-109">Filter requests generated from a particular IP address or country.</span><span class="sxs-lookup"><span data-stu-id="09430-109">Filter requests generated from a particular IP address or country.</span></span>
- <span data-ttu-id="09430-110">Filter requests by header information.</span><span class="sxs-lookup"><span data-stu-id="09430-110">Filter requests by header information.</span></span>

## <a name="always-match-condition"></a><span data-ttu-id="09430-111">Always match condition</span><span class="sxs-lookup"><span data-stu-id="09430-111">Always match condition</span></span>

<span data-ttu-id="09430-112">The Always match condition applies a default set of features to all requests.</span><span class="sxs-lookup"><span data-stu-id="09430-112">The Always match condition applies a default set of features to all requests.</span></span>

<span data-ttu-id="09430-113">Name</span><span class="sxs-lookup"><span data-stu-id="09430-113">Name</span></span> | <span data-ttu-id="09430-114">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-114">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-115">Always</span><span class="sxs-lookup"><span data-stu-id="09430-115">Always</span></span>](#always) | <span data-ttu-id="09430-116">Applies a default set of features to all requests.</span><span class="sxs-lookup"><span data-stu-id="09430-116">Applies a default set of features to all requests.</span></span>

## <a name="device-match-condition"></a><span data-ttu-id="09430-117">Device match condition</span><span class="sxs-lookup"><span data-stu-id="09430-117">Device match condition</span></span>

<span data-ttu-id="09430-118">The Device match condition identifies requests made from a mobile device based on its properties.</span><span class="sxs-lookup"><span data-stu-id="09430-118">The Device match condition identifies requests made from a mobile device based on its properties.</span></span>  

<span data-ttu-id="09430-119">Name</span><span class="sxs-lookup"><span data-stu-id="09430-119">Name</span></span> | <span data-ttu-id="09430-120">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-120">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-121">Device</span><span class="sxs-lookup"><span data-stu-id="09430-121">Device</span></span>](#device) | <span data-ttu-id="09430-122">Identifies requests made from a mobile device based on its properties.</span><span class="sxs-lookup"><span data-stu-id="09430-122">Identifies requests made from a mobile device based on its properties.</span></span>

## <a name="location-match-conditions"></a><span data-ttu-id="09430-123">Location match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-123">Location match conditions</span></span>

<span data-ttu-id="09430-124">The Location match conditions identify requests based on the requester's location.</span><span class="sxs-lookup"><span data-stu-id="09430-124">The Location match conditions identify requests based on the requester's location.</span></span>

<span data-ttu-id="09430-125">Name</span><span class="sxs-lookup"><span data-stu-id="09430-125">Name</span></span> | <span data-ttu-id="09430-126">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-126">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-127">AS Number</span><span class="sxs-lookup"><span data-stu-id="09430-127">AS Number</span></span>](#as-number) | <span data-ttu-id="09430-128">Identifies requests that originate from a particular network.</span><span class="sxs-lookup"><span data-stu-id="09430-128">Identifies requests that originate from a particular network.</span></span>
[<span data-ttu-id="09430-129">Country</span><span class="sxs-lookup"><span data-stu-id="09430-129">Country</span></span>](#country) | <span data-ttu-id="09430-130">Identifies requests that originate from the specified countries.</span><span class="sxs-lookup"><span data-stu-id="09430-130">Identifies requests that originate from the specified countries.</span></span>

## <a name="origin-match-conditions"></a><span data-ttu-id="09430-131">Origin match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-131">Origin match conditions</span></span>

<span data-ttu-id="09430-132">The Origin match conditions identify requests that point to Content Delivery Network storage or a customer origin server.</span><span class="sxs-lookup"><span data-stu-id="09430-132">The Origin match conditions identify requests that point to Content Delivery Network storage or a customer origin server.</span></span>

<span data-ttu-id="09430-133">Name</span><span class="sxs-lookup"><span data-stu-id="09430-133">Name</span></span> | <span data-ttu-id="09430-134">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-134">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-135">CDN Origin</span><span class="sxs-lookup"><span data-stu-id="09430-135">CDN Origin</span></span>](#cdn-origin) | <span data-ttu-id="09430-136">Identifies requests for content stored in Content Delivery Network storage.</span><span class="sxs-lookup"><span data-stu-id="09430-136">Identifies requests for content stored in Content Delivery Network storage.</span></span>
[<span data-ttu-id="09430-137">Customer Origin</span><span class="sxs-lookup"><span data-stu-id="09430-137">Customer Origin</span></span>](#customer-origin) | <span data-ttu-id="09430-138">Identifies requests for content stored on a specific customer origin server.</span><span class="sxs-lookup"><span data-stu-id="09430-138">Identifies requests for content stored on a specific customer origin server.</span></span>

## <a name="request-match-conditions"></a><span data-ttu-id="09430-139">Request match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-139">Request match conditions</span></span>

<span data-ttu-id="09430-140">The Request match conditions identify requests based on their properties.</span><span class="sxs-lookup"><span data-stu-id="09430-140">The Request match conditions identify requests based on their properties.</span></span>

<span data-ttu-id="09430-141">Name</span><span class="sxs-lookup"><span data-stu-id="09430-141">Name</span></span> | <span data-ttu-id="09430-142">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-142">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-143">Client IP Address</span><span class="sxs-lookup"><span data-stu-id="09430-143">Client IP Address</span></span>](#client-ip-address) | <span data-ttu-id="09430-144">Identifies requests that originate from a particular IP address.</span><span class="sxs-lookup"><span data-stu-id="09430-144">Identifies requests that originate from a particular IP address.</span></span>
[<span data-ttu-id="09430-145">Cookie Parameter</span><span class="sxs-lookup"><span data-stu-id="09430-145">Cookie Parameter</span></span>](#cookie-parameter) | <span data-ttu-id="09430-146">Checks the cookies associated with each request for the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-146">Checks the cookies associated with each request for the specified value.</span></span>
[<span data-ttu-id="09430-147">Cookie Parameter Regex</span><span class="sxs-lookup"><span data-stu-id="09430-147">Cookie Parameter Regex</span></span>](#cookie-parameter-regex) | <span data-ttu-id="09430-148">Checks the cookies associated with each request for the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-148">Checks the cookies associated with each request for the specified regular expression.</span></span>
[<span data-ttu-id="09430-149">Edge Cname</span><span class="sxs-lookup"><span data-stu-id="09430-149">Edge Cname</span></span>](#edge-cname) | <span data-ttu-id="09430-150">Identifies requests that point to a specific edge CNAME.</span><span class="sxs-lookup"><span data-stu-id="09430-150">Identifies requests that point to a specific edge CNAME.</span></span>
[<span data-ttu-id="09430-151">Referring Domain</span><span class="sxs-lookup"><span data-stu-id="09430-151">Referring Domain</span></span>](#referring-domain) | <span data-ttu-id="09430-152">Identifies requests that were referred from the specified host names.</span><span class="sxs-lookup"><span data-stu-id="09430-152">Identifies requests that were referred from the specified host names.</span></span>
[<span data-ttu-id="09430-153">Request Header Literal</span><span class="sxs-lookup"><span data-stu-id="09430-153">Request Header Literal</span></span>](#request-header-literal) | <span data-ttu-id="09430-154">Identifies requests that contain the specified header set to a specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-154">Identifies requests that contain the specified header set to a specified value.</span></span>
[<span data-ttu-id="09430-155">Request Header Regex</span><span class="sxs-lookup"><span data-stu-id="09430-155">Request Header Regex</span></span>](#request-header-regex) | <span data-ttu-id="09430-156">Identifies requests that contain the specified header set to a value that matches the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-156">Identifies requests that contain the specified header set to a value that matches the specified regular expression.</span></span>
[<span data-ttu-id="09430-157">Request Header Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-157">Request Header Wildcard</span></span>](#request-header-wildcard) | <span data-ttu-id="09430-158">Identifies requests that contain the specified header set to a value that matches the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-158">Identifies requests that contain the specified header set to a value that matches the specified pattern.</span></span>
[<span data-ttu-id="09430-159">Request Method</span><span class="sxs-lookup"><span data-stu-id="09430-159">Request Method</span></span>](#request-method) | <span data-ttu-id="09430-160">Identifies requests by their HTTP method.</span><span class="sxs-lookup"><span data-stu-id="09430-160">Identifies requests by their HTTP method.</span></span>
[<span data-ttu-id="09430-161">Request Scheme</span><span class="sxs-lookup"><span data-stu-id="09430-161">Request Scheme</span></span>](#request-scheme) | <span data-ttu-id="09430-162">Identifies requests by their HTTP protocol.</span><span class="sxs-lookup"><span data-stu-id="09430-162">Identifies requests by their HTTP protocol.</span></span>

## <a name="url-match-conditions"></a><span data-ttu-id="09430-163">URL match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-163">URL match conditions</span></span>

<span data-ttu-id="09430-164">The URL match conditions identify requests based on their URLs.</span><span class="sxs-lookup"><span data-stu-id="09430-164">The URL match conditions identify requests based on their URLs.</span></span>

<span data-ttu-id="09430-165">Name</span><span class="sxs-lookup"><span data-stu-id="09430-165">Name</span></span> | <span data-ttu-id="09430-166">Purpose</span><span class="sxs-lookup"><span data-stu-id="09430-166">Purpose</span></span>
-----|--------
[<span data-ttu-id="09430-167">URL Path Directory</span><span class="sxs-lookup"><span data-stu-id="09430-167">URL Path Directory</span></span>](#url-path-directory) | <span data-ttu-id="09430-168">Identifies requests by their relative path.</span><span class="sxs-lookup"><span data-stu-id="09430-168">Identifies requests by their relative path.</span></span>
[<span data-ttu-id="09430-169">URL Path Extension</span><span class="sxs-lookup"><span data-stu-id="09430-169">URL Path Extension</span></span>](#url-path-extension) | <span data-ttu-id="09430-170">Identifies requests by their file name extension.</span><span class="sxs-lookup"><span data-stu-id="09430-170">Identifies requests by their file name extension.</span></span>
[<span data-ttu-id="09430-171">URL Path Filename</span><span class="sxs-lookup"><span data-stu-id="09430-171">URL Path Filename</span></span>](#url-path-filename) | <span data-ttu-id="09430-172">Identifies requests by their file name.</span><span class="sxs-lookup"><span data-stu-id="09430-172">Identifies requests by their file name.</span></span>
[<span data-ttu-id="09430-173">URL Path Literal</span><span class="sxs-lookup"><span data-stu-id="09430-173">URL Path Literal</span></span>](#url-path-literal) | <span data-ttu-id="09430-174">Compares a request's relative path to the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-174">Compares a request's relative path to the specified value.</span></span>
[<span data-ttu-id="09430-175">URL Path Regex</span><span class="sxs-lookup"><span data-stu-id="09430-175">URL Path Regex</span></span>](#url-path-regex) | <span data-ttu-id="09430-176">Compares a request's relative path to the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-176">Compares a request's relative path to the specified regular expression.</span></span>
[<span data-ttu-id="09430-177">URL Path Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-177">URL Path Wildcard</span></span>](#url-path-wildcard) | <span data-ttu-id="09430-178">Compares a request's relative path to the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-178">Compares a request's relative path to the specified pattern.</span></span>
[<span data-ttu-id="09430-179">URL Query Literal</span><span class="sxs-lookup"><span data-stu-id="09430-179">URL Query Literal</span></span>](#url-query-literal) | <span data-ttu-id="09430-180">Compares a request's query string to the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-180">Compares a request's query string to the specified value.</span></span>
[<span data-ttu-id="09430-181">URL Query Parameter</span><span class="sxs-lookup"><span data-stu-id="09430-181">URL Query Parameter</span></span>](#url-query-parameter) | <span data-ttu-id="09430-182">Identifies requests that contain the specified query string parameter set to a value that matches a specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-182">Identifies requests that contain the specified query string parameter set to a value that matches a specified pattern.</span></span>
[<span data-ttu-id="09430-183">URL Query Regex</span><span class="sxs-lookup"><span data-stu-id="09430-183">URL Query Regex</span></span>](#url-query-regex) | <span data-ttu-id="09430-184">Identifies requests that contain the specified query string parameter set to a value that matches a specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-184">Identifies requests that contain the specified query string parameter set to a value that matches a specified regular expression.</span></span>
[<span data-ttu-id="09430-185">URL Query Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-185">URL Query Wildcard</span></span>](#url-query-wildcard) | <span data-ttu-id="09430-186">Compares the specified value against the request's query string.</span><span class="sxs-lookup"><span data-stu-id="09430-186">Compares the specified value against the request's query string.</span></span>


## <a name="reference-for-rules-engine-match-conditions"></a><span data-ttu-id="09430-187">Reference for rules engine match conditions</span><span class="sxs-lookup"><span data-stu-id="09430-187">Reference for rules engine match conditions</span></span>

---
### <a name="always"></a><span data-ttu-id="09430-188">Always</span><span class="sxs-lookup"><span data-stu-id="09430-188">Always</span></span>

<span data-ttu-id="09430-189">The Always match condition applies a default set of features to all requests.</span><span class="sxs-lookup"><span data-stu-id="09430-189">The Always match condition applies a default set of features to all requests.</span></span>

[<span data-ttu-id="09430-190">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-190">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="as-number"></a><span data-ttu-id="09430-191">AS Number</span><span class="sxs-lookup"><span data-stu-id="09430-191">AS Number</span></span> 
<span data-ttu-id="09430-192">The AS Number network is defined by its autonomous system number (ASN).</span><span class="sxs-lookup"><span data-stu-id="09430-192">The AS Number network is defined by its autonomous system number (ASN).</span></span> 

<span data-ttu-id="09430-193">The **Matches**/**Does Not Match** option determines the conditions under which the AS Number match condition is met:</span><span class="sxs-lookup"><span data-stu-id="09430-193">The **Matches**/**Does Not Match** option determines the conditions under which the AS Number match condition is met:</span></span>
- <span data-ttu-id="09430-194">**Matches**: Requires that the ASN of the client network matches one of the specified ASNs.</span><span class="sxs-lookup"><span data-stu-id="09430-194">**Matches**: Requires that the ASN of the client network matches one of the specified ASNs.</span></span> 
- <span data-ttu-id="09430-195">**Does Not Match**: Requires that the ASN of the client network does not match any of the specified ASNs.</span><span class="sxs-lookup"><span data-stu-id="09430-195">**Does Not Match**: Requires that the ASN of the client network does not match any of the specified ASNs.</span></span>

<span data-ttu-id="09430-196">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-196">Key information:</span></span>
- <span data-ttu-id="09430-197">Specify multiple ASNs by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-197">Specify multiple ASNs by delimiting each one with a single space.</span></span> <span data-ttu-id="09430-198">For example, 64514 64515 matches requests that arrive from either 64514 or 64515.</span><span class="sxs-lookup"><span data-stu-id="09430-198">For example, 64514 64515 matches requests that arrive from either 64514 or 64515.</span></span>
- <span data-ttu-id="09430-199">Certain requests might not return a valid ASN.</span><span class="sxs-lookup"><span data-stu-id="09430-199">Certain requests might not return a valid ASN.</span></span> <span data-ttu-id="09430-200">A question mark (?) will match requests for which a valid ASN could not be determined.</span><span class="sxs-lookup"><span data-stu-id="09430-200">A question mark (?) will match requests for which a valid ASN could not be determined.</span></span>
- <span data-ttu-id="09430-201">Specify the entire ASN for the desired network.</span><span class="sxs-lookup"><span data-stu-id="09430-201">Specify the entire ASN for the desired network.</span></span> <span data-ttu-id="09430-202">Partial values will not be matched.</span><span class="sxs-lookup"><span data-stu-id="09430-202">Partial values will not be matched.</span></span>
- <span data-ttu-id="09430-203">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-203">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-204">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-204">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-205">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-205">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-206">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-206">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-207">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-207">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-208">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-208">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-209">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-209">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="cdn-origin"></a><span data-ttu-id="09430-210">CDN Origin</span><span class="sxs-lookup"><span data-stu-id="09430-210">CDN Origin</span></span>
<span data-ttu-id="09430-211">The CDN Origin match condition is met when both of the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="09430-211">The CDN Origin match condition is met when both of the following conditions are met:</span></span>
- <span data-ttu-id="09430-212">Content from CDN storage was requested.</span><span class="sxs-lookup"><span data-stu-id="09430-212">Content from CDN storage was requested.</span></span>
- <span data-ttu-id="09430-213">The request URI uses the type of content access point (for example, /000001) that's defined in this match condition:</span><span class="sxs-lookup"><span data-stu-id="09430-213">The request URI uses the type of content access point (for example, /000001) that's defined in this match condition:</span></span>
  - <span data-ttu-id="09430-214">CDN URL: The request URI must contain the selected content access point.</span><span class="sxs-lookup"><span data-stu-id="09430-214">CDN URL: The request URI must contain the selected content access point.</span></span>
  - <span data-ttu-id="09430-215">Edge CNAME URL: The corresponding edge CNAME configuration must point to the selected content access point.</span><span class="sxs-lookup"><span data-stu-id="09430-215">Edge CNAME URL: The corresponding edge CNAME configuration must point to the selected content access point.</span></span>
  
<span data-ttu-id="09430-216">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-216">Key information:</span></span>
 - <span data-ttu-id="09430-217">The content access point identifies the service that should serve the requested content.</span><span class="sxs-lookup"><span data-stu-id="09430-217">The content access point identifies the service that should serve the requested content.</span></span>
 - <span data-ttu-id="09430-218">Don't use an AND IF statement to combine certain match conditions.</span><span class="sxs-lookup"><span data-stu-id="09430-218">Don't use an AND IF statement to combine certain match conditions.</span></span> <span data-ttu-id="09430-219">For example, combining a CDN Origin match condition with a Customer Origin match condition would create a match pattern that could never be matched.</span><span class="sxs-lookup"><span data-stu-id="09430-219">For example, combining a CDN Origin match condition with a Customer Origin match condition would create a match pattern that could never be matched.</span></span> <span data-ttu-id="09430-220">For this reason, two CDN Origin match conditions cannot be combined through an AND IF statement.</span><span class="sxs-lookup"><span data-stu-id="09430-220">For this reason, two CDN Origin match conditions cannot be combined through an AND IF statement.</span></span>

[<span data-ttu-id="09430-221">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-221">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="client-ip-address"></a><span data-ttu-id="09430-222">Client IP Address</span><span class="sxs-lookup"><span data-stu-id="09430-222">Client IP Address</span></span>
<span data-ttu-id="09430-223">The **Matches**/**Does Not Match** option determines the conditions under which the Client IP Address match condition is met:</span><span class="sxs-lookup"><span data-stu-id="09430-223">The **Matches**/**Does Not Match** option determines the conditions under which the Client IP Address match condition is met:</span></span>
- <span data-ttu-id="09430-224">**Matches**: Requires that the client's IP address matches one of the specified IP addresses.</span><span class="sxs-lookup"><span data-stu-id="09430-224">**Matches**: Requires that the client's IP address matches one of the specified IP addresses.</span></span> 
- <span data-ttu-id="09430-225">**Does Not Match**: Requires that the client's IP address does not match any of the specified IP addresses.</span><span class="sxs-lookup"><span data-stu-id="09430-225">**Does Not Match**: Requires that the client's IP address does not match any of the specified IP addresses.</span></span> 

<span data-ttu-id="09430-226">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-226">Key information:</span></span>
- <span data-ttu-id="09430-227">Use CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="09430-227">Use CIDR notation.</span></span>
- <span data-ttu-id="09430-228">Specify multiple IP addresses and/or IP address blocks by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-228">Specify multiple IP addresses and/or IP address blocks by delimiting each one with a single space.</span></span> <span data-ttu-id="09430-229">For example:</span><span class="sxs-lookup"><span data-stu-id="09430-229">For example:</span></span>
  - <span data-ttu-id="09430-230">**IPv4 example**: 1.2.3.4 10.20.30.40 matches any requests that arrive from either address 1.2.3.4 or 10.20.30.40.</span><span class="sxs-lookup"><span data-stu-id="09430-230">**IPv4 example**: 1.2.3.4 10.20.30.40 matches any requests that arrive from either address 1.2.3.4 or 10.20.30.40.</span></span>
  - <span data-ttu-id="09430-231">**IPv6 example**: 1:2:3:4:5:6:7:8 10:20:30:40:50:60:70:80 matches any requests that arrive from either address 1:2:3:4:5:6:7:8 or 10:20:30:40:50:60:70:80.</span><span class="sxs-lookup"><span data-stu-id="09430-231">**IPv6 example**: 1:2:3:4:5:6:7:8 10:20:30:40:50:60:70:80 matches any requests that arrive from either address 1:2:3:4:5:6:7:8 or 10:20:30:40:50:60:70:80.</span></span>
- <span data-ttu-id="09430-232">The syntax for an IP address block is the base IP address followed by a forward slash and the prefix size.</span><span class="sxs-lookup"><span data-stu-id="09430-232">The syntax for an IP address block is the base IP address followed by a forward slash and the prefix size.</span></span> <span data-ttu-id="09430-233">For example:</span><span class="sxs-lookup"><span data-stu-id="09430-233">For example:</span></span>
  - <span data-ttu-id="09430-234">**IPv4 example**: 5.5.5.64/26 matches any requests that arrive from addresses 5.5.5.64 through 5.5.5.127.</span><span class="sxs-lookup"><span data-stu-id="09430-234">**IPv4 example**: 5.5.5.64/26 matches any requests that arrive from addresses 5.5.5.64 through 5.5.5.127.</span></span>
  - <span data-ttu-id="09430-235">**IPv6 example**: 1:2:3:/48 matches any requests that arrive from addresses 1:2:3:0:0:0:0:0 through 1:2:3:ffff:ffff:ffff:ffff:ffff.</span><span class="sxs-lookup"><span data-stu-id="09430-235">**IPv6 example**: 1:2:3:/48 matches any requests that arrive from addresses 1:2:3:0:0:0:0:0 through 1:2:3:ffff:ffff:ffff:ffff:ffff.</span></span>
- <span data-ttu-id="09430-236">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-236">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-237">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-237">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-238">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-238">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-239">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-239">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-240">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-240">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-241">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-241">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-242">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-242">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="cookie-parameter"></a><span data-ttu-id="09430-243">Cookie Parameter</span><span class="sxs-lookup"><span data-stu-id="09430-243">Cookie Parameter</span></span>
<span data-ttu-id="09430-244">The **Matches**/**Does Not Match** option determines the conditions under which the Cookie Parameter match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-244">The **Matches**/**Does Not Match** option determines the conditions under which the Cookie Parameter match condition is met.</span></span>
- <span data-ttu-id="09430-245">**Matches**: Requires a request to contain the specified cookie with a value that matches at least one of the values that are defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-245">**Matches**: Requires a request to contain the specified cookie with a value that matches at least one of the values that are defined in this match condition.</span></span>
- <span data-ttu-id="09430-246">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-246">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-247">It does not contain the specified cookie.</span><span class="sxs-lookup"><span data-stu-id="09430-247">It does not contain the specified cookie.</span></span>
  - <span data-ttu-id="09430-248">It contains the specified cookie, but its value does not match any of the values that are defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-248">It contains the specified cookie, but its value does not match any of the values that are defined in this match condition.</span></span>
  
<span data-ttu-id="09430-249">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-249">Key information:</span></span>
- <span data-ttu-id="09430-250">Cookie name:</span><span class="sxs-lookup"><span data-stu-id="09430-250">Cookie name:</span></span> 
  - <span data-ttu-id="09430-251">Because wildcard values, including asterisks (\*), are not supported when you're specifying a cookie name, only exact cookie name matches are eligible for comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-251">Because wildcard values, including asterisks (\*), are not supported when you're specifying a cookie name, only exact cookie name matches are eligible for comparison.</span></span>
  - <span data-ttu-id="09430-252">Only a single cookie name can be specified per instance of this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-252">Only a single cookie name can be specified per instance of this match condition.</span></span>
  - <span data-ttu-id="09430-253">Cookie name comparisons are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-253">Cookie name comparisons are case-insensitive.</span></span>
- <span data-ttu-id="09430-254">Cookie value:</span><span class="sxs-lookup"><span data-stu-id="09430-254">Cookie value:</span></span> 
  - <span data-ttu-id="09430-255">Specify multiple cookie values by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-255">Specify multiple cookie values by delimiting each one with a single space.</span></span>
  - <span data-ttu-id="09430-256">A cookie value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-256">A cookie value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span> 
  - <span data-ttu-id="09430-257">If a wildcard value has not been specified, then only an exact match will satisfy this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-257">If a wildcard value has not been specified, then only an exact match will satisfy this match condition.</span></span> <span data-ttu-id="09430-258">For example, specifying "Value" will match "Value," but not "Value1" or "Value2."</span><span class="sxs-lookup"><span data-stu-id="09430-258">For example, specifying "Value" will match "Value," but not "Value1" or "Value2."</span></span>
  - <span data-ttu-id="09430-259">Use the **Ignore Case** option to control whether a case-sensitive comparison is made against the request's cookie value.</span><span class="sxs-lookup"><span data-stu-id="09430-259">Use the **Ignore Case** option to control whether a case-sensitive comparison is made against the request's cookie value.</span></span>
- <span data-ttu-id="09430-260">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-260">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-261">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-261">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-262">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-262">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-263">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-263">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-264">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-264">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-265">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-265">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-266">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-266">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="cookie-parameter-regex"></a><span data-ttu-id="09430-267">Cookie Parameter Regex</span><span class="sxs-lookup"><span data-stu-id="09430-267">Cookie Parameter Regex</span></span>
<span data-ttu-id="09430-268">The Cookie Parameter Regex match condition defines a cookie name and value.</span><span class="sxs-lookup"><span data-stu-id="09430-268">The Cookie Parameter Regex match condition defines a cookie name and value.</span></span> <span data-ttu-id="09430-269">You can use [regular expressions](cdn-rules-engine-reference.md#regular-expressions) to define the desired cookie value.</span><span class="sxs-lookup"><span data-stu-id="09430-269">You can use [regular expressions](cdn-rules-engine-reference.md#regular-expressions) to define the desired cookie value.</span></span> 

<span data-ttu-id="09430-270">The **Matches**/**Does Not Match** option determines the conditions under which the Cookie Parameter Regex match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-270">The **Matches**/**Does Not Match** option determines the conditions under which the Cookie Parameter Regex match condition is met.</span></span>
- <span data-ttu-id="09430-271">**Matches**: Requires a request to contain the specified cookie with a value that matches the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-271">**Matches**: Requires a request to contain the specified cookie with a value that matches the specified regular expression.</span></span>
- <span data-ttu-id="09430-272">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-272">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-273">It does not contain the specified cookie.</span><span class="sxs-lookup"><span data-stu-id="09430-273">It does not contain the specified cookie.</span></span>
  - <span data-ttu-id="09430-274">It contains the specified cookie, but its value does not match the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-274">It contains the specified cookie, but its value does not match the specified regular expression.</span></span>
  
<span data-ttu-id="09430-275">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-275">Key information:</span></span>
- <span data-ttu-id="09430-276">Cookie name:</span><span class="sxs-lookup"><span data-stu-id="09430-276">Cookie name:</span></span> 
  - <span data-ttu-id="09430-277">Because regular expressions and wildcard values, including asterisks (\*), are not supported when you're specifying a cookie name, only exact cookie name matches are eligible for comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-277">Because regular expressions and wildcard values, including asterisks (\*), are not supported when you're specifying a cookie name, only exact cookie name matches are eligible for comparison.</span></span>
  - <span data-ttu-id="09430-278">Only a single cookie name can be specified per instance of this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-278">Only a single cookie name can be specified per instance of this match condition.</span></span>
  - <span data-ttu-id="09430-279">Cookie name comparisons are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-279">Cookie name comparisons are case-insensitive.</span></span>
- <span data-ttu-id="09430-280">Cookie value:</span><span class="sxs-lookup"><span data-stu-id="09430-280">Cookie value:</span></span> 
  - <span data-ttu-id="09430-281">A cookie value can take advantage of regular expressions.</span><span class="sxs-lookup"><span data-stu-id="09430-281">A cookie value can take advantage of regular expressions.</span></span>
  - <span data-ttu-id="09430-282">Use the **Ignore Case** option to control whether a case-sensitive comparison is made against the request's cookie value.</span><span class="sxs-lookup"><span data-stu-id="09430-282">Use the **Ignore Case** option to control whether a case-sensitive comparison is made against the request's cookie value.</span></span>
- <span data-ttu-id="09430-283">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-283">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-284">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-284">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-285">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-285">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-286">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-286">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-287">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-287">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-288">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-288">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-289">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-289">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

--- 
### <a name="country"></a><span data-ttu-id="09430-290">Country</span><span class="sxs-lookup"><span data-stu-id="09430-290">Country</span></span>
<span data-ttu-id="09430-291">You can specify a country through its country code.</span><span class="sxs-lookup"><span data-stu-id="09430-291">You can specify a country through its country code.</span></span> 

<span data-ttu-id="09430-292">The **Matches**/**Does Not Match** option determines the conditions under which the Country match condition is met:</span><span class="sxs-lookup"><span data-stu-id="09430-292">The **Matches**/**Does Not Match** option determines the conditions under which the Country match condition is met:</span></span>
- <span data-ttu-id="09430-293">**Matches**: Requires the request to contain the specified country code values.</span><span class="sxs-lookup"><span data-stu-id="09430-293">**Matches**: Requires the request to contain the specified country code values.</span></span> 
- <span data-ttu-id="09430-294">**Does Not Match**: Requires that the request does not contain the specified country code values.</span><span class="sxs-lookup"><span data-stu-id="09430-294">**Does Not Match**: Requires that the request does not contain the specified country code values.</span></span>

<span data-ttu-id="09430-295">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-295">Key information:</span></span>
- <span data-ttu-id="09430-296">Specify multiple country codes by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-296">Specify multiple country codes by delimiting each one with a single space.</span></span>
- <span data-ttu-id="09430-297">Wildcards are not supported when you're specifying a country code.</span><span class="sxs-lookup"><span data-stu-id="09430-297">Wildcards are not supported when you're specifying a country code.</span></span>
- <span data-ttu-id="09430-298">The "EU" and "AP" country codes do not encompass all IP addresses in those regions.</span><span class="sxs-lookup"><span data-stu-id="09430-298">The "EU" and "AP" country codes do not encompass all IP addresses in those regions.</span></span>
- <span data-ttu-id="09430-299">Certain requests might not return a valid country code.</span><span class="sxs-lookup"><span data-stu-id="09430-299">Certain requests might not return a valid country code.</span></span> <span data-ttu-id="09430-300">A question mark (?) will match requests for which a valid country code could not be determined.</span><span class="sxs-lookup"><span data-stu-id="09430-300">A question mark (?) will match requests for which a valid country code could not be determined.</span></span>
- <span data-ttu-id="09430-301">Country codes are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-301">Country codes are case-sensitive.</span></span>
- <span data-ttu-id="09430-302">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-302">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-303">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-303">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-304">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-304">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-305">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-305">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-306">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-306">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-307">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-307">Internal Max-Stale</span></span>

#### <a name="implementing-country-filtering-by-using-the-rules-engine"></a><span data-ttu-id="09430-308">Implementing Country Filtering by using the rules engine</span><span class="sxs-lookup"><span data-stu-id="09430-308">Implementing Country Filtering by using the rules engine</span></span>
<span data-ttu-id="09430-309">This match condition allows you to perform a multitude of customizations based on the location from which a request originated.</span><span class="sxs-lookup"><span data-stu-id="09430-309">This match condition allows you to perform a multitude of customizations based on the location from which a request originated.</span></span> <span data-ttu-id="09430-310">For example, the behavior of the Country Filtering feature can be replicated through the following configuration:</span><span class="sxs-lookup"><span data-stu-id="09430-310">For example, the behavior of the Country Filtering feature can be replicated through the following configuration:</span></span>

- <span data-ttu-id="09430-311">URL Path Wildcard match: Set the [URL Path Wildcard match condition](#url-path-wildcard) to the directory that will be secured.</span><span class="sxs-lookup"><span data-stu-id="09430-311">URL Path Wildcard match: Set the [URL Path Wildcard match condition](#url-path-wildcard) to the directory that will be secured.</span></span> 
    <span data-ttu-id="09430-312">Append an asterisk to the end of the relative path to ensure that access to all of its children will be restricted by this rule.</span><span class="sxs-lookup"><span data-stu-id="09430-312">Append an asterisk to the end of the relative path to ensure that access to all of its children will be restricted by this rule.</span></span>

- <span data-ttu-id="09430-313">Country match: Set the Country match condition to the desired set of countries.</span><span class="sxs-lookup"><span data-stu-id="09430-313">Country match: Set the Country match condition to the desired set of countries.</span></span>
   - <span data-ttu-id="09430-314">Allow: Set the Country match condition to **Does Not Match** to allow only the specified countries access to content stored in the location defined by the URL Path Wildcard match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-314">Allow: Set the Country match condition to **Does Not Match** to allow only the specified countries access to content stored in the location defined by the URL Path Wildcard match condition.</span></span>
   - <span data-ttu-id="09430-315">Block: Set the Country match condition to **Matches** to block the specified countries from accessing content stored in the location defined by the URL Path Wildcard match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-315">Block: Set the Country match condition to **Matches** to block the specified countries from accessing content stored in the location defined by the URL Path Wildcard match condition.</span></span>

- <span data-ttu-id="09430-316">Deny Access (403) Feature: Enable the [Deny Access (403) feature](cdn-rules-engine-reference-features.md#deny-access-403) to replicate the allow or block portion of the Country Filtering feature.</span><span class="sxs-lookup"><span data-stu-id="09430-316">Deny Access (403) Feature: Enable the [Deny Access (403) feature](cdn-rules-engine-reference-features.md#deny-access-403) to replicate the allow or block portion of the Country Filtering feature.</span></span>

[<span data-ttu-id="09430-317">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-317">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="customer-origin"></a><span data-ttu-id="09430-318">Customer Origin</span><span class="sxs-lookup"><span data-stu-id="09430-318">Customer Origin</span></span>

<span data-ttu-id="09430-319">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-319">Key information:</span></span> 
- <span data-ttu-id="09430-320">The Customer Origin match condition is met regardless of whether content is requested through a CDN URL or an edge CNAME URL that points to the selected customer origin.</span><span class="sxs-lookup"><span data-stu-id="09430-320">The Customer Origin match condition is met regardless of whether content is requested through a CDN URL or an edge CNAME URL that points to the selected customer origin.</span></span>
- <span data-ttu-id="09430-321">A customer origin configuration that's referenced by a rule cannot be deleted from the Customer Origin page.</span><span class="sxs-lookup"><span data-stu-id="09430-321">A customer origin configuration that's referenced by a rule cannot be deleted from the Customer Origin page.</span></span> <span data-ttu-id="09430-322">Before you attempt to delete a customer origin configuration, make sure that the following configurations do not reference it:</span><span class="sxs-lookup"><span data-stu-id="09430-322">Before you attempt to delete a customer origin configuration, make sure that the following configurations do not reference it:</span></span>
  - <span data-ttu-id="09430-323">A Customer Origin match condition</span><span class="sxs-lookup"><span data-stu-id="09430-323">A Customer Origin match condition</span></span>
  - <span data-ttu-id="09430-324">An edge CNAME configuration</span><span class="sxs-lookup"><span data-stu-id="09430-324">An edge CNAME configuration</span></span>
- <span data-ttu-id="09430-325">Don't use an AND IF statement to combine certain match conditions.</span><span class="sxs-lookup"><span data-stu-id="09430-325">Don't use an AND IF statement to combine certain match conditions.</span></span> <span data-ttu-id="09430-326">For example, combining a Customer Origin match condition with a CDN Origin match condition would create a match pattern that could never be matched.</span><span class="sxs-lookup"><span data-stu-id="09430-326">For example, combining a Customer Origin match condition with a CDN Origin match condition would create a match pattern that could never be matched.</span></span> <span data-ttu-id="09430-327">For this reason, two Customer Origin match conditions cannot be combined through an AND IF statement.</span><span class="sxs-lookup"><span data-stu-id="09430-327">For this reason, two Customer Origin match conditions cannot be combined through an AND IF statement.</span></span>

[<span data-ttu-id="09430-328">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-328">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="device"></a><span data-ttu-id="09430-329">Device</span><span class="sxs-lookup"><span data-stu-id="09430-329">Device</span></span>

<span data-ttu-id="09430-330">The Device match condition identifies requests made from a mobile device based on its properties.</span><span class="sxs-lookup"><span data-stu-id="09430-330">The Device match condition identifies requests made from a mobile device based on its properties.</span></span> <span data-ttu-id="09430-331">Mobile device detection is achieved through [WURFL](http://wurfl.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="09430-331">Mobile device detection is achieved through [WURFL](http://wurfl.sourceforge.net/).</span></span> 

<span data-ttu-id="09430-332">The **Matches**/**Does Not Match** option determines the conditions under which the Device match condition is met:</span><span class="sxs-lookup"><span data-stu-id="09430-332">The **Matches**/**Does Not Match** option determines the conditions under which the Device match condition is met:</span></span>
- <span data-ttu-id="09430-333">**Matches**: Requires the requester's device to match the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-333">**Matches**: Requires the requester's device to match the specified value.</span></span> 
- <span data-ttu-id="09430-334">**Does Not Match**: Requires that the requester's device does not match the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-334">**Does Not Match**: Requires that the requester's device does not match the specified value.</span></span>

<span data-ttu-id="09430-335">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-335">Key information:</span></span>

- <span data-ttu-id="09430-336">Use the **Ignore Case** option to specify whether the specified value is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-336">Use the **Ignore Case** option to specify whether the specified value is case-sensitive.</span></span>
- <span data-ttu-id="09430-337">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-337">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-338">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-338">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-339">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-339">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-340">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-340">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-341">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-341">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-342">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-342">Internal Max-Stale</span></span>

#### <a name="string-type"></a><span data-ttu-id="09430-343">String Type</span><span class="sxs-lookup"><span data-stu-id="09430-343">String Type</span></span>
<span data-ttu-id="09430-344">A WURFL capability typically accepts any combination of numbers, letters, and symbols.</span><span class="sxs-lookup"><span data-stu-id="09430-344">A WURFL capability typically accepts any combination of numbers, letters, and symbols.</span></span> <span data-ttu-id="09430-345">Due to the flexible nature of this capability, you must choose how the value associated with this match condition is interpreted.</span><span class="sxs-lookup"><span data-stu-id="09430-345">Due to the flexible nature of this capability, you must choose how the value associated with this match condition is interpreted.</span></span> <span data-ttu-id="09430-346">The following table describes the available set of options:</span><span class="sxs-lookup"><span data-stu-id="09430-346">The following table describes the available set of options:</span></span>

<span data-ttu-id="09430-347">Type</span><span class="sxs-lookup"><span data-stu-id="09430-347">Type</span></span>     | <span data-ttu-id="09430-348">Description</span><span class="sxs-lookup"><span data-stu-id="09430-348">Description</span></span>
---------|------------
<span data-ttu-id="09430-349">Literal</span><span class="sxs-lookup"><span data-stu-id="09430-349">Literal</span></span>  | <span data-ttu-id="09430-350">Select this option to prevent most characters from taking on special meaning by using their [literal value](cdn-rules-engine-reference.md#literal-values).</span><span class="sxs-lookup"><span data-stu-id="09430-350">Select this option to prevent most characters from taking on special meaning by using their [literal value](cdn-rules-engine-reference.md#literal-values).</span></span>
<span data-ttu-id="09430-351">Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-351">Wildcard</span></span> | <span data-ttu-id="09430-352">Select this option to take advantage of all [wildcard characters]([wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-352">Select this option to take advantage of all [wildcard characters]([wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span>
<span data-ttu-id="09430-353">Regex</span><span class="sxs-lookup"><span data-stu-id="09430-353">Regex</span></span>    | <span data-ttu-id="09430-354">Select this option to use [regular expressions](cdn-rules-engine-reference.md#regular-expressions).</span><span class="sxs-lookup"><span data-stu-id="09430-354">Select this option to use [regular expressions](cdn-rules-engine-reference.md#regular-expressions).</span></span> <span data-ttu-id="09430-355">Regular expressions are useful for defining a pattern of characters.</span><span class="sxs-lookup"><span data-stu-id="09430-355">Regular expressions are useful for defining a pattern of characters.</span></span>

#### <a name="wurfl-capabilities"></a><span data-ttu-id="09430-356">WURFL capabilities</span><span class="sxs-lookup"><span data-stu-id="09430-356">WURFL capabilities</span></span>
<span data-ttu-id="09430-357">A WURFL capability refers to a category that describes mobile devices.</span><span class="sxs-lookup"><span data-stu-id="09430-357">A WURFL capability refers to a category that describes mobile devices.</span></span> <span data-ttu-id="09430-358">The selected capability determines the type of mobile device description that is used to identify requests.</span><span class="sxs-lookup"><span data-stu-id="09430-358">The selected capability determines the type of mobile device description that is used to identify requests.</span></span>

<span data-ttu-id="09430-359">The following table lists WURFL capabilities and their variables for the rules engine.</span><span class="sxs-lookup"><span data-stu-id="09430-359">The following table lists WURFL capabilities and their variables for the rules engine.</span></span>
<br>
> [!NOTE] 
> <span data-ttu-id="09430-360">The following variables are supported in the **Modify Client Request Header** and **Modify Client Response Header** features.</span><span class="sxs-lookup"><span data-stu-id="09430-360">The following variables are supported in the **Modify Client Request Header** and **Modify Client Response Header** features.</span></span>

<span data-ttu-id="09430-361">Capability</span><span class="sxs-lookup"><span data-stu-id="09430-361">Capability</span></span> | <span data-ttu-id="09430-362">Variable</span><span class="sxs-lookup"><span data-stu-id="09430-362">Variable</span></span> | <span data-ttu-id="09430-363">Description</span><span class="sxs-lookup"><span data-stu-id="09430-363">Description</span></span> | <span data-ttu-id="09430-364">Sample values</span><span class="sxs-lookup"><span data-stu-id="09430-364">Sample values</span></span>
-----------|----------|-------------|----------------
<span data-ttu-id="09430-365">Brand Name</span><span class="sxs-lookup"><span data-stu-id="09430-365">Brand Name</span></span> | <span data-ttu-id="09430-366">%{wurfl_cap_brand_name}</span><span class="sxs-lookup"><span data-stu-id="09430-366">%{wurfl_cap_brand_name}</span></span> | <span data-ttu-id="09430-367">A string that indicates the brand name of the device.</span><span class="sxs-lookup"><span data-stu-id="09430-367">A string that indicates the brand name of the device.</span></span> | <span data-ttu-id="09430-368">Samsung</span><span class="sxs-lookup"><span data-stu-id="09430-368">Samsung</span></span>
<span data-ttu-id="09430-369">Device OS</span><span class="sxs-lookup"><span data-stu-id="09430-369">Device OS</span></span> | <span data-ttu-id="09430-370">%{wurfl_cap_device_os}</span><span class="sxs-lookup"><span data-stu-id="09430-370">%{wurfl_cap_device_os}</span></span> | <span data-ttu-id="09430-371">A string that indicates the operating system installed on the device.</span><span class="sxs-lookup"><span data-stu-id="09430-371">A string that indicates the operating system installed on the device.</span></span> | <span data-ttu-id="09430-372">IOS</span><span class="sxs-lookup"><span data-stu-id="09430-372">IOS</span></span>
<span data-ttu-id="09430-373">Device OS Version</span><span class="sxs-lookup"><span data-stu-id="09430-373">Device OS Version</span></span> | <span data-ttu-id="09430-374">%{wurfl_cap_device_os_version}</span><span class="sxs-lookup"><span data-stu-id="09430-374">%{wurfl_cap_device_os_version}</span></span> | <span data-ttu-id="09430-375">A string that indicates the version number of the operating system installed on the device.</span><span class="sxs-lookup"><span data-stu-id="09430-375">A string that indicates the version number of the operating system installed on the device.</span></span> | <span data-ttu-id="09430-376">1.0.1</span><span class="sxs-lookup"><span data-stu-id="09430-376">1.0.1</span></span>
<span data-ttu-id="09430-377">Dual Orientation</span><span class="sxs-lookup"><span data-stu-id="09430-377">Dual Orientation</span></span> | <span data-ttu-id="09430-378">%{wurfl_cap_dual_orientation}</span><span class="sxs-lookup"><span data-stu-id="09430-378">%{wurfl_cap_dual_orientation}</span></span> | <span data-ttu-id="09430-379">A Boolean that indicates whether the device supports dual orientation.</span><span class="sxs-lookup"><span data-stu-id="09430-379">A Boolean that indicates whether the device supports dual orientation.</span></span> | <span data-ttu-id="09430-380">true</span><span class="sxs-lookup"><span data-stu-id="09430-380">true</span></span>
<span data-ttu-id="09430-381">HTML Preferred DTD</span><span class="sxs-lookup"><span data-stu-id="09430-381">HTML Preferred DTD</span></span> | <span data-ttu-id="09430-382">%{wurfl_cap_html_preferred_dtd}</span><span class="sxs-lookup"><span data-stu-id="09430-382">%{wurfl_cap_html_preferred_dtd}</span></span> | <span data-ttu-id="09430-383">A string that indicates the mobile device's preferred document type definition (DTD) for HTML content.</span><span class="sxs-lookup"><span data-stu-id="09430-383">A string that indicates the mobile device's preferred document type definition (DTD) for HTML content.</span></span> | <span data-ttu-id="09430-384">none</span><span class="sxs-lookup"><span data-stu-id="09430-384">none</span></span><br/><span data-ttu-id="09430-385">xhtml_basic</span><span class="sxs-lookup"><span data-stu-id="09430-385">xhtml_basic</span></span><br/><span data-ttu-id="09430-386">html5</span><span class="sxs-lookup"><span data-stu-id="09430-386">html5</span></span>
<span data-ttu-id="09430-387">Image Inlining</span><span class="sxs-lookup"><span data-stu-id="09430-387">Image Inlining</span></span> | <span data-ttu-id="09430-388">%{wurfl_cap_image_inlining}</span><span class="sxs-lookup"><span data-stu-id="09430-388">%{wurfl_cap_image_inlining}</span></span> | <span data-ttu-id="09430-389">A Boolean that indicates whether the device supports Base64 encoded images.</span><span class="sxs-lookup"><span data-stu-id="09430-389">A Boolean that indicates whether the device supports Base64 encoded images.</span></span> | <span data-ttu-id="09430-390">false</span><span class="sxs-lookup"><span data-stu-id="09430-390">false</span></span>
<span data-ttu-id="09430-391">Is Android</span><span class="sxs-lookup"><span data-stu-id="09430-391">Is Android</span></span> | <span data-ttu-id="09430-392">%{wurfl_vcap_is_android}</span><span class="sxs-lookup"><span data-stu-id="09430-392">%{wurfl_vcap_is_android}</span></span> | <span data-ttu-id="09430-393">A Boolean that indicates whether the device uses the Android OS.</span><span class="sxs-lookup"><span data-stu-id="09430-393">A Boolean that indicates whether the device uses the Android OS.</span></span> | <span data-ttu-id="09430-394">true</span><span class="sxs-lookup"><span data-stu-id="09430-394">true</span></span>
<span data-ttu-id="09430-395">Is IOS</span><span class="sxs-lookup"><span data-stu-id="09430-395">Is IOS</span></span> | <span data-ttu-id="09430-396">%{wurfl_vcap_is_ios}</span><span class="sxs-lookup"><span data-stu-id="09430-396">%{wurfl_vcap_is_ios}</span></span> | <span data-ttu-id="09430-397">A Boolean that indicates whether the device uses iOS.</span><span class="sxs-lookup"><span data-stu-id="09430-397">A Boolean that indicates whether the device uses iOS.</span></span> | <span data-ttu-id="09430-398">false</span><span class="sxs-lookup"><span data-stu-id="09430-398">false</span></span>
<span data-ttu-id="09430-399">Is Smart TV</span><span class="sxs-lookup"><span data-stu-id="09430-399">Is Smart TV</span></span> | <span data-ttu-id="09430-400">%{wurfl_cap_is_smarttv}</span><span class="sxs-lookup"><span data-stu-id="09430-400">%{wurfl_cap_is_smarttv}</span></span> | <span data-ttu-id="09430-401">A Boolean that indicates whether the device is a smart TV.</span><span class="sxs-lookup"><span data-stu-id="09430-401">A Boolean that indicates whether the device is a smart TV.</span></span> | <span data-ttu-id="09430-402">false</span><span class="sxs-lookup"><span data-stu-id="09430-402">false</span></span>
<span data-ttu-id="09430-403">Is Smartphone</span><span class="sxs-lookup"><span data-stu-id="09430-403">Is Smartphone</span></span> | <span data-ttu-id="09430-404">%{wurfl_vcap_is_smartphone}</span><span class="sxs-lookup"><span data-stu-id="09430-404">%{wurfl_vcap_is_smartphone}</span></span> | <span data-ttu-id="09430-405">A Boolean that indicates whether the device is a smartphone.</span><span class="sxs-lookup"><span data-stu-id="09430-405">A Boolean that indicates whether the device is a smartphone.</span></span> | <span data-ttu-id="09430-406">true</span><span class="sxs-lookup"><span data-stu-id="09430-406">true</span></span>
<span data-ttu-id="09430-407">Is Tablet</span><span class="sxs-lookup"><span data-stu-id="09430-407">Is Tablet</span></span> | <span data-ttu-id="09430-408">%{wurfl_cap_is_tablet}</span><span class="sxs-lookup"><span data-stu-id="09430-408">%{wurfl_cap_is_tablet}</span></span> | <span data-ttu-id="09430-409">A Boolean that indicates whether the device is a tablet.</span><span class="sxs-lookup"><span data-stu-id="09430-409">A Boolean that indicates whether the device is a tablet.</span></span> <span data-ttu-id="09430-410">This description is  OS-independent.</span><span class="sxs-lookup"><span data-stu-id="09430-410">This description is  OS-independent.</span></span> | <span data-ttu-id="09430-411">true</span><span class="sxs-lookup"><span data-stu-id="09430-411">true</span></span>
<span data-ttu-id="09430-412">Is Wireless Device</span><span class="sxs-lookup"><span data-stu-id="09430-412">Is Wireless Device</span></span> | <span data-ttu-id="09430-413">%{wurfl_cap_is_wireless_device}</span><span class="sxs-lookup"><span data-stu-id="09430-413">%{wurfl_cap_is_wireless_device}</span></span> | <span data-ttu-id="09430-414">A Boolean that indicates whether the device is considered a wireless device.</span><span class="sxs-lookup"><span data-stu-id="09430-414">A Boolean that indicates whether the device is considered a wireless device.</span></span> | <span data-ttu-id="09430-415">true</span><span class="sxs-lookup"><span data-stu-id="09430-415">true</span></span>
<span data-ttu-id="09430-416">Marketing Name</span><span class="sxs-lookup"><span data-stu-id="09430-416">Marketing Name</span></span> | <span data-ttu-id="09430-417">%{wurfl_cap_marketing_name}</span><span class="sxs-lookup"><span data-stu-id="09430-417">%{wurfl_cap_marketing_name}</span></span> | <span data-ttu-id="09430-418">A string that indicates the device's marketing name.</span><span class="sxs-lookup"><span data-stu-id="09430-418">A string that indicates the device's marketing name.</span></span> | <span data-ttu-id="09430-419">BlackBerry 8100 Pearl</span><span class="sxs-lookup"><span data-stu-id="09430-419">BlackBerry 8100 Pearl</span></span>
<span data-ttu-id="09430-420">Mobile Browser</span><span class="sxs-lookup"><span data-stu-id="09430-420">Mobile Browser</span></span> | <span data-ttu-id="09430-421">%{wurfl_cap_mobile_browser}</span><span class="sxs-lookup"><span data-stu-id="09430-421">%{wurfl_cap_mobile_browser}</span></span> | <span data-ttu-id="09430-422">A string that indicates the browser that's used to request content from the device.</span><span class="sxs-lookup"><span data-stu-id="09430-422">A string that indicates the browser that's used to request content from the device.</span></span> | <span data-ttu-id="09430-423">Chrome</span><span class="sxs-lookup"><span data-stu-id="09430-423">Chrome</span></span>
<span data-ttu-id="09430-424">Mobile Browser Version</span><span class="sxs-lookup"><span data-stu-id="09430-424">Mobile Browser Version</span></span> | <span data-ttu-id="09430-425">%{wurfl_cap_mobile_browser_version}</span><span class="sxs-lookup"><span data-stu-id="09430-425">%{wurfl_cap_mobile_browser_version}</span></span> | <span data-ttu-id="09430-426">A string that indicates the version of the browser that's used to request content from the device.</span><span class="sxs-lookup"><span data-stu-id="09430-426">A string that indicates the version of the browser that's used to request content from the device.</span></span> | <span data-ttu-id="09430-427">31</span><span class="sxs-lookup"><span data-stu-id="09430-427">31</span></span>
<span data-ttu-id="09430-428">Model Name</span><span class="sxs-lookup"><span data-stu-id="09430-428">Model Name</span></span> | <span data-ttu-id="09430-429">%{wurfl_cap_model_name}</span><span class="sxs-lookup"><span data-stu-id="09430-429">%{wurfl_cap_model_name}</span></span> | <span data-ttu-id="09430-430">A string that indicates the device's model name.</span><span class="sxs-lookup"><span data-stu-id="09430-430">A string that indicates the device's model name.</span></span> | <span data-ttu-id="09430-431">s3</span><span class="sxs-lookup"><span data-stu-id="09430-431">s3</span></span>
<span data-ttu-id="09430-432">Progressive Download</span><span class="sxs-lookup"><span data-stu-id="09430-432">Progressive Download</span></span> | <span data-ttu-id="09430-433">%{wurfl_cap_progressive_download}</span><span class="sxs-lookup"><span data-stu-id="09430-433">%{wurfl_cap_progressive_download}</span></span> | <span data-ttu-id="09430-434">A Boolean that indicates whether the device supports the playback of audio and video while it is still being downloaded.</span><span class="sxs-lookup"><span data-stu-id="09430-434">A Boolean that indicates whether the device supports the playback of audio and video while it is still being downloaded.</span></span> | <span data-ttu-id="09430-435">true</span><span class="sxs-lookup"><span data-stu-id="09430-435">true</span></span>
<span data-ttu-id="09430-436">Release Date</span><span class="sxs-lookup"><span data-stu-id="09430-436">Release Date</span></span> | <span data-ttu-id="09430-437">%{wurfl_cap_release_date}</span><span class="sxs-lookup"><span data-stu-id="09430-437">%{wurfl_cap_release_date}</span></span> | <span data-ttu-id="09430-438">A string that indicates the year and month on which the device was added to the WURFL database.</span><span class="sxs-lookup"><span data-stu-id="09430-438">A string that indicates the year and month on which the device was added to the WURFL database.</span></span><br/><br/><span data-ttu-id="09430-439">Format: `yyyy_mm`</span><span class="sxs-lookup"><span data-stu-id="09430-439">Format: `yyyy_mm`</span></span> | <span data-ttu-id="09430-440">2013_december</span><span class="sxs-lookup"><span data-stu-id="09430-440">2013_december</span></span>
<span data-ttu-id="09430-441">Resolution Height</span><span class="sxs-lookup"><span data-stu-id="09430-441">Resolution Height</span></span> | <span data-ttu-id="09430-442">%{wurfl_cap_resolution_height}</span><span class="sxs-lookup"><span data-stu-id="09430-442">%{wurfl_cap_resolution_height}</span></span> | <span data-ttu-id="09430-443">An integer that indicates the device's height in pixels.</span><span class="sxs-lookup"><span data-stu-id="09430-443">An integer that indicates the device's height in pixels.</span></span> | <span data-ttu-id="09430-444">768</span><span class="sxs-lookup"><span data-stu-id="09430-444">768</span></span>
<span data-ttu-id="09430-445">Resolution Width</span><span class="sxs-lookup"><span data-stu-id="09430-445">Resolution Width</span></span> | <span data-ttu-id="09430-446">%{wurfl_cap_resolution_width}</span><span class="sxs-lookup"><span data-stu-id="09430-446">%{wurfl_cap_resolution_width}</span></span> | <span data-ttu-id="09430-447">An integer that indicates the device's width in pixels.</span><span class="sxs-lookup"><span data-stu-id="09430-447">An integer that indicates the device's width in pixels.</span></span> | <span data-ttu-id="09430-448">1024</span><span class="sxs-lookup"><span data-stu-id="09430-448">1024</span></span>

[<span data-ttu-id="09430-449">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-449">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="edge-cname"></a><span data-ttu-id="09430-450">Edge Cname</span><span class="sxs-lookup"><span data-stu-id="09430-450">Edge Cname</span></span>
<span data-ttu-id="09430-451">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-451">Key information:</span></span> 
- <span data-ttu-id="09430-452">The list of available edge CNAMEs is limited to those edge CNAMEs that have been configured on the Edge CNAMEs page for the platform on which the rules engine is being configured.</span><span class="sxs-lookup"><span data-stu-id="09430-452">The list of available edge CNAMEs is limited to those edge CNAMEs that have been configured on the Edge CNAMEs page for the platform on which the rules engine is being configured.</span></span>
- <span data-ttu-id="09430-453">Before you attempt to delete an edge CNAME configuration, make sure that an Edge Cname match condition does not reference it.</span><span class="sxs-lookup"><span data-stu-id="09430-453">Before you attempt to delete an edge CNAME configuration, make sure that an Edge Cname match condition does not reference it.</span></span> <span data-ttu-id="09430-454">Edge CNAME configurations that have been defined in a rule cannot be deleted from the Edge CNAMEs page.</span><span class="sxs-lookup"><span data-stu-id="09430-454">Edge CNAME configurations that have been defined in a rule cannot be deleted from the Edge CNAMEs page.</span></span> 
- <span data-ttu-id="09430-455">Don't use an AND IF statement to combine certain match conditions.</span><span class="sxs-lookup"><span data-stu-id="09430-455">Don't use an AND IF statement to combine certain match conditions.</span></span> <span data-ttu-id="09430-456">For example, combining an Edge Cname match condition with a Customer Origin match condition would create a match pattern that could never be matched.</span><span class="sxs-lookup"><span data-stu-id="09430-456">For example, combining an Edge Cname match condition with a Customer Origin match condition would create a match pattern that could never be matched.</span></span> <span data-ttu-id="09430-457">For this reason, two Edge Cname match conditions cannot be combined through an AND IF statement.</span><span class="sxs-lookup"><span data-stu-id="09430-457">For this reason, two Edge Cname match conditions cannot be combined through an AND IF statement.</span></span>
- <span data-ttu-id="09430-458">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-458">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-459">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-459">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-460">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-460">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-461">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-461">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-462">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-462">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-463">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-463">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-464">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-464">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="referring-domain"></a><span data-ttu-id="09430-465">Referring Domain</span><span class="sxs-lookup"><span data-stu-id="09430-465">Referring Domain</span></span>
<span data-ttu-id="09430-466">The host name associated with the referrer through which content was requested determines whether the Referring Domain condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-466">The host name associated with the referrer through which content was requested determines whether the Referring Domain condition is met.</span></span> 

<span data-ttu-id="09430-467">The **Matches**/**Does Not Match** option determines the conditions under which the Referring Domain match condition is met:</span><span class="sxs-lookup"><span data-stu-id="09430-467">The **Matches**/**Does Not Match** option determines the conditions under which the Referring Domain match condition is met:</span></span>
- <span data-ttu-id="09430-468">**Matches**: Requires the referring host name to match the specified values.</span><span class="sxs-lookup"><span data-stu-id="09430-468">**Matches**: Requires the referring host name to match the specified values.</span></span> 
- <span data-ttu-id="09430-469">**Does Not Match**: Requires that the referring host name does not match the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-469">**Does Not Match**: Requires that the referring host name does not match the specified value.</span></span>

<span data-ttu-id="09430-470">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-470">Key information:</span></span>
- <span data-ttu-id="09430-471">Specify multiple host names by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-471">Specify multiple host names by delimiting each one with a single space.</span></span>
- <span data-ttu-id="09430-472">This match condition supports [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-472">This match condition supports [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span>
- <span data-ttu-id="09430-473">If the specified value does not contain an asterisk, it must be an exact match for the referrer's host name.</span><span class="sxs-lookup"><span data-stu-id="09430-473">If the specified value does not contain an asterisk, it must be an exact match for the referrer's host name.</span></span> <span data-ttu-id="09430-474">For example, specifying "mydomain.com" would not match "www.mydomain.com."</span><span class="sxs-lookup"><span data-stu-id="09430-474">For example, specifying "mydomain.com" would not match "www.mydomain.com."</span></span>
- <span data-ttu-id="09430-475">Use the **Ignore Case** option to control whether a case-sensitive comparison is made.</span><span class="sxs-lookup"><span data-stu-id="09430-475">Use the **Ignore Case** option to control whether a case-sensitive comparison is made.</span></span>
- <span data-ttu-id="09430-476">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-476">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-477">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-477">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-478">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-478">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-479">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-479">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-480">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-480">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-481">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-481">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-482">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-482">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---  
### <a name="request-header-literal"></a><span data-ttu-id="09430-483">Request Header Literal</span><span class="sxs-lookup"><span data-stu-id="09430-483">Request Header Literal</span></span>
<span data-ttu-id="09430-484">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Literal match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-484">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Literal match condition is met.</span></span>
- <span data-ttu-id="09430-485">**Matches**: Requires the request to contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-485">**Matches**: Requires the request to contain the specified header.</span></span> <span data-ttu-id="09430-486">Its value must match the one that's defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-486">Its value must match the one that's defined in this match condition.</span></span>
- <span data-ttu-id="09430-487">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-487">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-488">It does not contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-488">It does not contain the specified header.</span></span>
  - <span data-ttu-id="09430-489">It contains the specified header, but its value does not match the one that's defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-489">It contains the specified header, but its value does not match the one that's defined in this match condition.</span></span>
  
<span data-ttu-id="09430-490">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-490">Key information:</span></span>
- <span data-ttu-id="09430-491">Header name comparisons are always case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-491">Header name comparisons are always case-insensitive.</span></span> <span data-ttu-id="09430-492">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-492">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span></span>
- <span data-ttu-id="09430-493">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-493">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-494">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-494">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-495">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-495">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-496">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-496">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-497">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-497">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-498">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-498">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-499">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-499">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---  
### <a name="request-header-regex"></a><span data-ttu-id="09430-500">Request Header Regex</span><span class="sxs-lookup"><span data-stu-id="09430-500">Request Header Regex</span></span>
<span data-ttu-id="09430-501">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Regex match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-501">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Regex match condition is met.</span></span>
- <span data-ttu-id="09430-502">**Matches**: Requires the request to contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-502">**Matches**: Requires the request to contain the specified header.</span></span> <span data-ttu-id="09430-503">Its value must match the pattern that's defined in the specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span><span class="sxs-lookup"><span data-stu-id="09430-503">Its value must match the pattern that's defined in the specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span></span>
- <span data-ttu-id="09430-504">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-504">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-505">It does not contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-505">It does not contain the specified header.</span></span>
  - <span data-ttu-id="09430-506">It contains the specified header, but its value does not match the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-506">It contains the specified header, but its value does not match the specified regular expression.</span></span>

<span data-ttu-id="09430-507">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-507">Key information:</span></span>
- <span data-ttu-id="09430-508">Header name:</span><span class="sxs-lookup"><span data-stu-id="09430-508">Header name:</span></span> 
  - <span data-ttu-id="09430-509">Header name comparisons are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-509">Header name comparisons are case-insensitive.</span></span>
  - <span data-ttu-id="09430-510">Replace spaces in the header name with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-510">Replace spaces in the header name with "%20."</span></span> 
- <span data-ttu-id="09430-511">Header value:</span><span class="sxs-lookup"><span data-stu-id="09430-511">Header value:</span></span> 
  - <span data-ttu-id="09430-512">A header value can take advantage of regular expressions.</span><span class="sxs-lookup"><span data-stu-id="09430-512">A header value can take advantage of regular expressions.</span></span>
  - <span data-ttu-id="09430-513">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-513">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span></span>
  - <span data-ttu-id="09430-514">The match condition is met only when a header value exactly matches at least one of the specified patterns.</span><span class="sxs-lookup"><span data-stu-id="09430-514">The match condition is met only when a header value exactly matches at least one of the specified patterns.</span></span>
- <span data-ttu-id="09430-515">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-515">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-516">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-516">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-517">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-517">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-518">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-518">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-519">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-519">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-520">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-520">Internal Max-Stale</span></span> 

[<span data-ttu-id="09430-521">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-521">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="request-header-wildcard"></a><span data-ttu-id="09430-522">Request Header Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-522">Request Header Wildcard</span></span>
<span data-ttu-id="09430-523">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Wildcard match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-523">The **Matches**/**Does Not Match** option determines the conditions under which the Request Header Wildcard match condition is met.</span></span>
- <span data-ttu-id="09430-524">**Matches**: Requires the request to contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-524">**Matches**: Requires the request to contain the specified header.</span></span> <span data-ttu-id="09430-525">Its value must match at least one of the values that are defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-525">Its value must match at least one of the values that are defined in this match condition.</span></span>
- <span data-ttu-id="09430-526">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-526">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-527">It does not contain the specified header.</span><span class="sxs-lookup"><span data-stu-id="09430-527">It does not contain the specified header.</span></span>
  - <span data-ttu-id="09430-528">It contains the specified header, but its value does not match any of the specified values.</span><span class="sxs-lookup"><span data-stu-id="09430-528">It contains the specified header, but its value does not match any of the specified values.</span></span>
  
<span data-ttu-id="09430-529">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-529">Key information:</span></span>
- <span data-ttu-id="09430-530">Header name:</span><span class="sxs-lookup"><span data-stu-id="09430-530">Header name:</span></span> 
  - <span data-ttu-id="09430-531">Header name comparisons are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="09430-531">Header name comparisons are case-insensitive.</span></span>
  - <span data-ttu-id="09430-532">Spaces in the header name should be replaced with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-532">Spaces in the header name should be replaced with "%20."</span></span> <span data-ttu-id="09430-533">You can also use this value to specify spaces in a header value.</span><span class="sxs-lookup"><span data-stu-id="09430-533">You can also use this value to specify spaces in a header value.</span></span>
- <span data-ttu-id="09430-534">Header value:</span><span class="sxs-lookup"><span data-stu-id="09430-534">Header value:</span></span> 
  - <span data-ttu-id="09430-535">A header value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-535">A header value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span>
  - <span data-ttu-id="09430-536">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-536">Use the **Ignore Case** option to control the case-sensitivity of header value comparisons.</span></span>
  - <span data-ttu-id="09430-537">This match condition is met when a header value exactly matches to at least one of the specified patterns.</span><span class="sxs-lookup"><span data-stu-id="09430-537">This match condition is met when a header value exactly matches to at least one of the specified patterns.</span></span>
  - <span data-ttu-id="09430-538">Specify multiple values by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-538">Specify multiple values by delimiting each one with a single space.</span></span>
- <span data-ttu-id="09430-539">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-539">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-540">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-540">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-541">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-541">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-542">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-542">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-543">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-543">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-544">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-544">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-545">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-545">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="request-method"></a><span data-ttu-id="09430-546">Request Method</span><span class="sxs-lookup"><span data-stu-id="09430-546">Request Method</span></span>
<span data-ttu-id="09430-547">The Request Method match condition is met only when assets are requested through the selected request method.</span><span class="sxs-lookup"><span data-stu-id="09430-547">The Request Method match condition is met only when assets are requested through the selected request method.</span></span> <span data-ttu-id="09430-548">The available request methods are:</span><span class="sxs-lookup"><span data-stu-id="09430-548">The available request methods are:</span></span>
- <span data-ttu-id="09430-549">GET</span><span class="sxs-lookup"><span data-stu-id="09430-549">GET</span></span>
- <span data-ttu-id="09430-550">HEAD</span><span class="sxs-lookup"><span data-stu-id="09430-550">HEAD</span></span> 
- <span data-ttu-id="09430-551">POST</span><span class="sxs-lookup"><span data-stu-id="09430-551">POST</span></span> 
- <span data-ttu-id="09430-552">OPTIONS</span><span class="sxs-lookup"><span data-stu-id="09430-552">OPTIONS</span></span> 
- <span data-ttu-id="09430-553">PUT</span><span class="sxs-lookup"><span data-stu-id="09430-553">PUT</span></span> 
- <span data-ttu-id="09430-554">DELETE</span><span class="sxs-lookup"><span data-stu-id="09430-554">DELETE</span></span> 
- <span data-ttu-id="09430-555">TRACE</span><span class="sxs-lookup"><span data-stu-id="09430-555">TRACE</span></span> 
- <span data-ttu-id="09430-556">CONNECT</span><span class="sxs-lookup"><span data-stu-id="09430-556">CONNECT</span></span> 

<span data-ttu-id="09430-557">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-557">Key information:</span></span>
- <span data-ttu-id="09430-558">By default, only the GET request method can generate cached content on the network.</span><span class="sxs-lookup"><span data-stu-id="09430-558">By default, only the GET request method can generate cached content on the network.</span></span> <span data-ttu-id="09430-559">All other request methods are proxied through the network.</span><span class="sxs-lookup"><span data-stu-id="09430-559">All other request methods are proxied through the network.</span></span>
- <span data-ttu-id="09430-560">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-560">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-561">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-561">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-562">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-562">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-563">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-563">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-564">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-564">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-565">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-565">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-566">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-566">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="request-scheme"></a><span data-ttu-id="09430-567">Request Scheme</span><span class="sxs-lookup"><span data-stu-id="09430-567">Request Scheme</span></span>
<span data-ttu-id="09430-568">The Request Scheme match condition is met only when assets are requested through the selected protocol.</span><span class="sxs-lookup"><span data-stu-id="09430-568">The Request Scheme match condition is met only when assets are requested through the selected protocol.</span></span> <span data-ttu-id="09430-569">The available protocols are:</span><span class="sxs-lookup"><span data-stu-id="09430-569">The available protocols are:</span></span> 
- <span data-ttu-id="09430-570">HTTP</span><span class="sxs-lookup"><span data-stu-id="09430-570">HTTP</span></span>
- <span data-ttu-id="09430-571">HTTPS</span><span class="sxs-lookup"><span data-stu-id="09430-571">HTTPS</span></span>

<span data-ttu-id="09430-572">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-572">Key information:</span></span>
- <span data-ttu-id="09430-573">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-573">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
  - <span data-ttu-id="09430-574">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-574">Complete Cache Fill</span></span>
  - <span data-ttu-id="09430-575">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-575">Default Internal Max-Age</span></span>
  - <span data-ttu-id="09430-576">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-576">Force Internal Max-Age</span></span>
  - <span data-ttu-id="09430-577">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-577">Ignore Origin No-Cache</span></span>
  - <span data-ttu-id="09430-578">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-578">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-579">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-579">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-directory"></a><span data-ttu-id="09430-580">URL Path Directory</span><span class="sxs-lookup"><span data-stu-id="09430-580">URL Path Directory</span></span>
<span data-ttu-id="09430-581">Identifies a request by its relative path, which excludes the file name of the requested asset.</span><span class="sxs-lookup"><span data-stu-id="09430-581">Identifies a request by its relative path, which excludes the file name of the requested asset.</span></span>

<span data-ttu-id="09430-582">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Directory match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-582">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Directory match condition is met.</span></span>
- <span data-ttu-id="09430-583">**Matches**: Requires the request to contain a relative URL path, excluding the file name, that matches the specified URL pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-583">**Matches**: Requires the request to contain a relative URL path, excluding the file name, that matches the specified URL pattern.</span></span>
- <span data-ttu-id="09430-584">**Does Not Match**: Requires the request to contain a relative URL path, excluding file name, that does not match the specified URL pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-584">**Does Not Match**: Requires the request to contain a relative URL path, excluding file name, that does not match the specified URL pattern.</span></span>

<span data-ttu-id="09430-585">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-585">Key information:</span></span>
- <span data-ttu-id="09430-586">Use the **Relative to** option to specify whether the URL comparison starts before or after the content access point.</span><span class="sxs-lookup"><span data-stu-id="09430-586">Use the **Relative to** option to specify whether the URL comparison starts before or after the content access point.</span></span> <span data-ttu-id="09430-587">The content access point is the portion of the path that appears between the Verizon CDN hostname and the relative path to the requested asset (for example, /800001/CustomerOrigin).</span><span class="sxs-lookup"><span data-stu-id="09430-587">The content access point is the portion of the path that appears between the Verizon CDN hostname and the relative path to the requested asset (for example, /800001/CustomerOrigin).</span></span> <span data-ttu-id="09430-588">It identifies a location by server type (for example, CDN or customer origin) and your customer account number.</span><span class="sxs-lookup"><span data-stu-id="09430-588">It identifies a location by server type (for example, CDN or customer origin) and your customer account number.</span></span>

   <span data-ttu-id="09430-589">The following values are available for the **Relative to** option:</span><span class="sxs-lookup"><span data-stu-id="09430-589">The following values are available for the **Relative to** option:</span></span>
   - <span data-ttu-id="09430-590">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span><span class="sxs-lookup"><span data-stu-id="09430-590">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span></span> 

     <span data-ttu-id="09430-591">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder**/index.htm</span><span class="sxs-lookup"><span data-stu-id="09430-591">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder**/index.htm</span></span>

   - <span data-ttu-id="09430-592">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span><span class="sxs-lookup"><span data-stu-id="09430-592">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span></span> <span data-ttu-id="09430-593">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span><span class="sxs-lookup"><span data-stu-id="09430-593">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span></span> 

     <span data-ttu-id="09430-594">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder**/index.htm</span><span class="sxs-lookup"><span data-stu-id="09430-594">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder**/index.htm</span></span> 

     <span data-ttu-id="09430-595">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder**/index.htm</span><span class="sxs-lookup"><span data-stu-id="09430-595">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder**/index.htm</span></span>

- <span data-ttu-id="09430-596">An edge CNAME URL is rewritten to a CDN URL prior to the URL comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-596">An edge CNAME URL is rewritten to a CDN URL prior to the URL comparison.</span></span>

    <span data-ttu-id="09430-597">For example, both of the following URLs point to the same asset and therefore have the same URL path.</span><span class="sxs-lookup"><span data-stu-id="09430-597">For example, both of the following URLs point to the same asset and therefore have the same URL path.</span></span>
    - <span data-ttu-id="09430-598">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-598">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span></span>
    
    - <span data-ttu-id="09430-599">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-599">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span></span>
    
    <span data-ttu-id="09430-600">Additional information:</span><span class="sxs-lookup"><span data-stu-id="09430-600">Additional information:</span></span>
    - <span data-ttu-id="09430-601">Custom domain: https:\//my.domain.com/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-601">Custom domain: https:\//my.domain.com/path/asset.htm</span></span>
    
    - <span data-ttu-id="09430-602">URL path (relative to root): /800001/CustomerOrigin/path/</span><span class="sxs-lookup"><span data-stu-id="09430-602">URL path (relative to root): /800001/CustomerOrigin/path/</span></span>
    
    - <span data-ttu-id="09430-603">URL path (relative to origin): /path/</span><span class="sxs-lookup"><span data-stu-id="09430-603">URL path (relative to origin): /path/</span></span>

- <span data-ttu-id="09430-604">The portion of the URL that is used for the URL comparison ends just before the file name of the requested asset.</span><span class="sxs-lookup"><span data-stu-id="09430-604">The portion of the URL that is used for the URL comparison ends just before the file name of the requested asset.</span></span> <span data-ttu-id="09430-605">A trailing forward slash is the last character in this type of path.</span><span class="sxs-lookup"><span data-stu-id="09430-605">A trailing forward slash is the last character in this type of path.</span></span>
    
- <span data-ttu-id="09430-606">Replace any spaces in the URL path pattern with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-606">Replace any spaces in the URL path pattern with "%20."</span></span>
    
- <span data-ttu-id="09430-607">Each URL path pattern can contain one or more asterisks (\*), where each asterisk matches a sequence of one or more characters.</span><span class="sxs-lookup"><span data-stu-id="09430-607">Each URL path pattern can contain one or more asterisks (\*), where each asterisk matches a sequence of one or more characters.</span></span>
    
- <span data-ttu-id="09430-608">Specify multiple URL paths in the pattern by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-608">Specify multiple URL paths in the pattern by delimiting each one with a single space.</span></span>

    <span data-ttu-id="09430-609">For example: \*/sales/ \*/marketing/</span><span class="sxs-lookup"><span data-stu-id="09430-609">For example: \*/sales/ \*/marketing/</span></span>

- <span data-ttu-id="09430-610">A URL path specification can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-610">A URL path specification can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span>

- <span data-ttu-id="09430-611">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-611">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>

[<span data-ttu-id="09430-612">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-612">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-extension"></a><span data-ttu-id="09430-613">URL Path Extension</span><span class="sxs-lookup"><span data-stu-id="09430-613">URL Path Extension</span></span>
<span data-ttu-id="09430-614">Identifies requests by the file extension of the requested asset.</span><span class="sxs-lookup"><span data-stu-id="09430-614">Identifies requests by the file extension of the requested asset.</span></span>

<span data-ttu-id="09430-615">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Extension match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-615">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Extension match condition is met.</span></span>
- <span data-ttu-id="09430-616">**Matches**: Requires the URL of the request to contain a file extension that exactly matches the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-616">**Matches**: Requires the URL of the request to contain a file extension that exactly matches the specified pattern.</span></span>

   <span data-ttu-id="09430-617">For example, if you specify "htm", "htm" assets are matched, but not "html" assets.</span><span class="sxs-lookup"><span data-stu-id="09430-617">For example, if you specify "htm", "htm" assets are matched, but not "html" assets.</span></span>  

- <span data-ttu-id="09430-618">**Does Not Match**: Requires the URL request to contain a file extension that does not match the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-618">**Does Not Match**: Requires the URL request to contain a file extension that does not match the specified pattern.</span></span>

<span data-ttu-id="09430-619">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-619">Key information:</span></span>
- <span data-ttu-id="09430-620">Specify the file extensions to match in the **Value** box.</span><span class="sxs-lookup"><span data-stu-id="09430-620">Specify the file extensions to match in the **Value** box.</span></span> <span data-ttu-id="09430-621">Do not include a leading period; for example, use htm instead of .htm.</span><span class="sxs-lookup"><span data-stu-id="09430-621">Do not include a leading period; for example, use htm instead of .htm.</span></span>

- <span data-ttu-id="09430-622">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-622">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>

- <span data-ttu-id="09430-623">Specify multiple file extensions by delimiting each extension with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-623">Specify multiple file extensions by delimiting each extension with a single space.</span></span> 

    <span data-ttu-id="09430-624">For example: htm html</span><span class="sxs-lookup"><span data-stu-id="09430-624">For example: htm html</span></span>

- <span data-ttu-id="09430-625">For example, specifying "htm" matches "htm" assets, but not "html" assets.</span><span class="sxs-lookup"><span data-stu-id="09430-625">For example, specifying "htm" matches "htm" assets, but not "html" assets.</span></span>


#### <a name="sample-scenario"></a><span data-ttu-id="09430-626">Sample Scenario</span><span class="sxs-lookup"><span data-stu-id="09430-626">Sample Scenario</span></span>

<span data-ttu-id="09430-627">The following sample configuration assumes that this match condition is met when a request matches one of the specified extensions.</span><span class="sxs-lookup"><span data-stu-id="09430-627">The following sample configuration assumes that this match condition is met when a request matches one of the specified extensions.</span></span>

<span data-ttu-id="09430-628">Value   specification: asp aspx php html</span><span class="sxs-lookup"><span data-stu-id="09430-628">Value   specification: asp aspx php html</span></span>

<span data-ttu-id="09430-629">This match condition is met when it finds URLs that end with the following extensions:</span><span class="sxs-lookup"><span data-stu-id="09430-629">This match condition is met when it finds URLs that end with the following extensions:</span></span>
- <span data-ttu-id="09430-630">.asp</span><span class="sxs-lookup"><span data-stu-id="09430-630">.asp</span></span>
- <span data-ttu-id="09430-631">.aspx</span><span class="sxs-lookup"><span data-stu-id="09430-631">.aspx</span></span>
- <span data-ttu-id="09430-632">.php</span><span class="sxs-lookup"><span data-stu-id="09430-632">.php</span></span>
- <span data-ttu-id="09430-633">.html</span><span class="sxs-lookup"><span data-stu-id="09430-633">.html</span></span>

[<span data-ttu-id="09430-634">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-634">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-filename"></a><span data-ttu-id="09430-635">URL Path Filename</span><span class="sxs-lookup"><span data-stu-id="09430-635">URL Path Filename</span></span>
<span data-ttu-id="09430-636">Identifies requests by the file name of the requested asset.</span><span class="sxs-lookup"><span data-stu-id="09430-636">Identifies requests by the file name of the requested asset.</span></span> <span data-ttu-id="09430-637">For the purposes of this match condition, a file name consists of the name of the requested asset, a period, and the file extension (for example, index.html).</span><span class="sxs-lookup"><span data-stu-id="09430-637">For the purposes of this match condition, a file name consists of the name of the requested asset, a period, and the file extension (for example, index.html).</span></span>

<span data-ttu-id="09430-638">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Filename match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-638">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Filename match condition is met.</span></span>
- <span data-ttu-id="09430-639">**Matches**: Requires the request to contain a file name in its URL path that matches the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-639">**Matches**: Requires the request to contain a file name in its URL path that matches the specified pattern.</span></span>
- <span data-ttu-id="09430-640">**Does Not Match**: Requires the request to contain a file name in its URL path that does not match the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-640">**Does Not Match**: Requires the request to contain a file name in its URL path that does not match the specified pattern.</span></span>

<span data-ttu-id="09430-641">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-641">Key information:</span></span>
- <span data-ttu-id="09430-642">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-642">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>

- <span data-ttu-id="09430-643">To specify multiple file extensions, separate each extension with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-643">To specify multiple file extensions, separate each extension with a single space.</span></span>

    <span data-ttu-id="09430-644">For example: index.htm index.html</span><span class="sxs-lookup"><span data-stu-id="09430-644">For example: index.htm index.html</span></span>

- <span data-ttu-id="09430-645">Replace spaces in a file name value with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-645">Replace spaces in a file name value with "%20."</span></span>
    
- <span data-ttu-id="09430-646">A file name value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-646">A file name value can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span> <span data-ttu-id="09430-647">For example, each file name pattern can consist of one or more asterisks (\*), where each asterisk matches a sequence of one or more characters.</span><span class="sxs-lookup"><span data-stu-id="09430-647">For example, each file name pattern can consist of one or more asterisks (\*), where each asterisk matches a sequence of one or more characters.</span></span>
    
- <span data-ttu-id="09430-648">If wildcard characters are not specified, then only an exact match will satisfy this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-648">If wildcard characters are not specified, then only an exact match will satisfy this match condition.</span></span>

    <span data-ttu-id="09430-649">For example, specifying "presentation.ppt" matches an asset named "presentation.ppt," but not one named "presentation.pptx."</span><span class="sxs-lookup"><span data-stu-id="09430-649">For example, specifying "presentation.ppt" matches an asset named "presentation.ppt," but not one named "presentation.pptx."</span></span>

[<span data-ttu-id="09430-650">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-650">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-literal"></a><span data-ttu-id="09430-651">URL Path Literal</span><span class="sxs-lookup"><span data-stu-id="09430-651">URL Path Literal</span></span>
<span data-ttu-id="09430-652">Compares a request's URL path, including file name, to the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-652">Compares a request's URL path, including file name, to the specified value.</span></span>

<span data-ttu-id="09430-653">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Literal match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-653">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Literal match condition is met.</span></span>
- <span data-ttu-id="09430-654">**Matches**: Requires the request to contain a URL path that matches the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-654">**Matches**: Requires the request to contain a URL path that matches the specified pattern.</span></span>
- <span data-ttu-id="09430-655">**Does Not Match**: Requires the request to contain a URL path that does not match the specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-655">**Does Not Match**: Requires the request to contain a URL path that does not match the specified pattern.</span></span>

<span data-ttu-id="09430-656">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-656">Key information:</span></span>
- <span data-ttu-id="09430-657">Use the **Relative to** option to specify whether the URL comparison point begins before or after the content access point.</span><span class="sxs-lookup"><span data-stu-id="09430-657">Use the **Relative to** option to specify whether the URL comparison point begins before or after the content access point.</span></span> 

    <span data-ttu-id="09430-658">The following values are available for the **Relative to** option:</span><span class="sxs-lookup"><span data-stu-id="09430-658">The following values are available for the **Relative to** option:</span></span>
     - <span data-ttu-id="09430-659">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span><span class="sxs-lookup"><span data-stu-id="09430-659">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span></span>

       <span data-ttu-id="09430-660">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-660">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder/index.htm**</span></span>

     - <span data-ttu-id="09430-661">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span><span class="sxs-lookup"><span data-stu-id="09430-661">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span></span> <span data-ttu-id="09430-662">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span><span class="sxs-lookup"><span data-stu-id="09430-662">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span></span> 

       <span data-ttu-id="09430-663">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-663">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder/index.htm**</span></span>

     <span data-ttu-id="09430-664">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-664">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder/index.htm**</span></span>

- <span data-ttu-id="09430-665">An edge CNAME URL is rewritten to a CDN URL prior to a URL comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-665">An edge CNAME URL is rewritten to a CDN URL prior to a URL comparison.</span></span>

    <span data-ttu-id="09430-666">For example, both of the following URLs point to the same asset and therefore have the same URL path:</span><span class="sxs-lookup"><span data-stu-id="09430-666">For example, both of the following URLs point to the same asset and therefore have the same URL path:</span></span>
    - <span data-ttu-id="09430-667">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-667">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span></span>
    - <span data-ttu-id="09430-668">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-668">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span></span>
    
    <span data-ttu-id="09430-669">Additional information:</span><span class="sxs-lookup"><span data-stu-id="09430-669">Additional information:</span></span>
    
    - <span data-ttu-id="09430-670">URL path (relative to root): /800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-670">URL path (relative to root): /800001/CustomerOrigin/path/asset.htm</span></span>
   
    - <span data-ttu-id="09430-671">URL path (relative to origin): /path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-671">URL path (relative to origin): /path/asset.htm</span></span>

- <span data-ttu-id="09430-672">Query strings in the URL are ignored.</span><span class="sxs-lookup"><span data-stu-id="09430-672">Query strings in the URL are ignored.</span></span>
- <span data-ttu-id="09430-673">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-673">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>
- <span data-ttu-id="09430-674">The value specified for this match condition is compared against the relative path of the exact request made by the client.</span><span class="sxs-lookup"><span data-stu-id="09430-674">The value specified for this match condition is compared against the relative path of the exact request made by the client.</span></span>

- <span data-ttu-id="09430-675">To match all requests made to a particular directory, use the [URL Path Directory](#url-path-directory) or the [URL Path Wildcard](#url-path-wildcard) match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-675">To match all requests made to a particular directory, use the [URL Path Directory](#url-path-directory) or the [URL Path Wildcard](#url-path-wildcard) match condition.</span></span>

[<span data-ttu-id="09430-676">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-676">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-regex"></a><span data-ttu-id="09430-677">URL Path Regex</span><span class="sxs-lookup"><span data-stu-id="09430-677">URL Path Regex</span></span>
<span data-ttu-id="09430-678">Compares a request's URL path to the specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span><span class="sxs-lookup"><span data-stu-id="09430-678">Compares a request's URL path to the specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span></span>

<span data-ttu-id="09430-679">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Regex match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-679">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Regex match condition is met.</span></span>
- <span data-ttu-id="09430-680">**Matches**: Requires the request to contain a URL path that matches the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-680">**Matches**: Requires the request to contain a URL path that matches the specified regular expression.</span></span>
- <span data-ttu-id="09430-681">**Does Not Match**: Requires the request to contain a URL path that does not match the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-681">**Does Not Match**: Requires the request to contain a URL path that does not match the specified regular expression.</span></span>

<span data-ttu-id="09430-682">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-682">Key information:</span></span>
- <span data-ttu-id="09430-683">An edge CNAME URL is rewritten to a CDN URL prior to URL comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-683">An edge CNAME URL is rewritten to a CDN URL prior to URL comparison.</span></span> 
 
    <span data-ttu-id="09430-684">For example, both URLs point to the same asset and therefore have the same URL path.</span><span class="sxs-lookup"><span data-stu-id="09430-684">For example, both URLs point to the same asset and therefore have the same URL path.</span></span>

     - <span data-ttu-id="09430-685">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-685">CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span></span>

     - <span data-ttu-id="09430-686">Edge CNAME URL: http:\//my.domain.com/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-686">Edge CNAME URL: http:\//my.domain.com/path/asset.htm</span></span>
    
    <span data-ttu-id="09430-687">Additional information:</span><span class="sxs-lookup"><span data-stu-id="09430-687">Additional information:</span></span>
    
     - <span data-ttu-id="09430-688">URL path: /800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-688">URL path: /800001/CustomerOrigin/path/asset.htm</span></span>

- <span data-ttu-id="09430-689">Query strings in the URL are ignored.</span><span class="sxs-lookup"><span data-stu-id="09430-689">Query strings in the URL are ignored.</span></span>
    
- <span data-ttu-id="09430-690">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-690">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>
    
- <span data-ttu-id="09430-691">Spaces in the URL path should be replaced with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-691">Spaces in the URL path should be replaced with "%20."</span></span>

[<span data-ttu-id="09430-692">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-692">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-path-wildcard"></a><span data-ttu-id="09430-693">URL Path Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-693">URL Path Wildcard</span></span>
<span data-ttu-id="09430-694">Compares a request's relative URL path to the specified wildcard pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-694">Compares a request's relative URL path to the specified wildcard pattern.</span></span>

<span data-ttu-id="09430-695">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Wildcard match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-695">The **Matches**/**Does Not Match** option determines the conditions under which the URL Path Wildcard match condition is met.</span></span>
- <span data-ttu-id="09430-696">**Matches**: Requires the request to contain a URL path that matches the specified wildcard pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-696">**Matches**: Requires the request to contain a URL path that matches the specified wildcard pattern.</span></span>
- <span data-ttu-id="09430-697">**Does Not Match**: Requires the request to contain a URL path that does not match the specified wildcard pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-697">**Does Not Match**: Requires the request to contain a URL path that does not match the specified wildcard pattern.</span></span>

<span data-ttu-id="09430-698">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-698">Key information:</span></span>
- <span data-ttu-id="09430-699">**Relative to** option: This option determines whether the URL comparison point begins before or after the content access point.</span><span class="sxs-lookup"><span data-stu-id="09430-699">**Relative to** option: This option determines whether the URL comparison point begins before or after the content access point.</span></span>

   <span data-ttu-id="09430-700">This option can have the following values:</span><span class="sxs-lookup"><span data-stu-id="09430-700">This option can have the following values:</span></span>
     - <span data-ttu-id="09430-701">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span><span class="sxs-lookup"><span data-stu-id="09430-701">**Root**: Indicates that the URL comparison point begins directly after the CDN hostname.</span></span>

       <span data-ttu-id="09430-702">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-702">For example: http:\//wpc.0001.&lt;domain&gt;/**800001/myorigin/myfolder/index.htm**</span></span>

     - <span data-ttu-id="09430-703">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span><span class="sxs-lookup"><span data-stu-id="09430-703">**Origin**: Indicates that the URL comparison point begins after the content access point (for example, /000001 or /800001/myorigin).</span></span> <span data-ttu-id="09430-704">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span><span class="sxs-lookup"><span data-stu-id="09430-704">Because the \*.azureedge.net CNAME is created relative to the origin directory on the Verizon CDN hostname by default, Azure CDN users should use the **Origin** value.</span></span> 

       <span data-ttu-id="09430-705">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-705">For example: https:\//&lt;endpoint&gt;.azureedge.net/**myfolder/index.htm**</span></span>

     <span data-ttu-id="09430-706">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder/index.htm**</span><span class="sxs-lookup"><span data-stu-id="09430-706">This URL points to the following Verizon CDN hostname: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/**myfolder/index.htm**</span></span>

- <span data-ttu-id="09430-707">An edge CNAME URL is rewritten to a CDN URL prior to URL comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-707">An edge CNAME URL is rewritten to a CDN URL prior to URL comparison.</span></span>

    <span data-ttu-id="09430-708">For example, both of the following URLs point to the same asset and therefore have the same URL path:</span><span class="sxs-lookup"><span data-stu-id="09430-708">For example, both of the following URLs point to the same asset and therefore have the same URL path:</span></span>
     - <span data-ttu-id="09430-709">CDN URL: http://wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-709">CDN URL: http://wpc.0001.&lt;domain&gt;/800001/CustomerOrigin/path/asset.htm</span></span>
     - <span data-ttu-id="09430-710">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-710">Edge CNAME URL: http:\//&lt;endpoint&gt;.azureedge.net/path/asset.htm</span></span>
    
    <span data-ttu-id="09430-711">Additional information:</span><span class="sxs-lookup"><span data-stu-id="09430-711">Additional information:</span></span>
    
     - <span data-ttu-id="09430-712">URL path (relative to root): /800001/CustomerOrigin/path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-712">URL path (relative to root): /800001/CustomerOrigin/path/asset.htm</span></span>
    
     - <span data-ttu-id="09430-713">URL path (relative to origin): /path/asset.htm</span><span class="sxs-lookup"><span data-stu-id="09430-713">URL path (relative to origin): /path/asset.htm</span></span>
    
- <span data-ttu-id="09430-714">Specify multiple URL paths by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-714">Specify multiple URL paths by delimiting each one with a single space.</span></span>

   <span data-ttu-id="09430-715">For example: /marketing/asset.\* /sales/\*.htm</span><span class="sxs-lookup"><span data-stu-id="09430-715">For example: /marketing/asset.\* /sales/\*.htm</span></span>

- <span data-ttu-id="09430-716">Query strings in the URL are ignored.</span><span class="sxs-lookup"><span data-stu-id="09430-716">Query strings in the URL are ignored.</span></span>
    
- <span data-ttu-id="09430-717">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span><span class="sxs-lookup"><span data-stu-id="09430-717">Use the **Ignore Case** option to control whether a case-sensitive comparison is performed.</span></span>
    
- <span data-ttu-id="09430-718">Replace spaces in the URL path with "%20."</span><span class="sxs-lookup"><span data-stu-id="09430-718">Replace spaces in the URL path with "%20."</span></span>
    
- <span data-ttu-id="09430-719">The value specified for a URL path can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-719">The value specified for a URL path can take advantage of [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span> <span data-ttu-id="09430-720">Each URL path pattern can contain one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span><span class="sxs-lookup"><span data-stu-id="09430-720">Each URL path pattern can contain one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="09430-721">Sample Scenarios</span><span class="sxs-lookup"><span data-stu-id="09430-721">Sample Scenarios</span></span>

<span data-ttu-id="09430-722">The sample configurations in the following table assume that this match condition is met when a request matches the specified URL pattern:</span><span class="sxs-lookup"><span data-stu-id="09430-722">The sample configurations in the following table assume that this match condition is met when a request matches the specified URL pattern:</span></span>

<span data-ttu-id="09430-723">Value</span><span class="sxs-lookup"><span data-stu-id="09430-723">Value</span></span>                   | <span data-ttu-id="09430-724">Relative to</span><span class="sxs-lookup"><span data-stu-id="09430-724">Relative to</span></span>    | <span data-ttu-id="09430-725">Result</span><span class="sxs-lookup"><span data-stu-id="09430-725">Result</span></span> 
------------------------|----------------|-------
<span data-ttu-id="09430-726">\*/test.html \*/test.php</span><span class="sxs-lookup"><span data-stu-id="09430-726">\*/test.html \*/test.php</span></span>  | <span data-ttu-id="09430-727">Root or Origin</span><span class="sxs-lookup"><span data-stu-id="09430-727">Root or Origin</span></span> | <span data-ttu-id="09430-728">This pattern is matched by requests for assets named "test.html" or "test.php" in any folder.</span><span class="sxs-lookup"><span data-stu-id="09430-728">This pattern is matched by requests for assets named "test.html" or "test.php" in any folder.</span></span>
<span data-ttu-id="09430-729">/80ABCD/origin/text/\*</span><span class="sxs-lookup"><span data-stu-id="09430-729">/80ABCD/origin/text/\*</span></span>   | <span data-ttu-id="09430-730">Root</span><span class="sxs-lookup"><span data-stu-id="09430-730">Root</span></span>           | <span data-ttu-id="09430-731">This pattern is matched when the requested asset meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-731">This pattern is matched when the requested asset meets the following criteria:</span></span> <br /><span data-ttu-id="09430-732">- It must reside on a customer origin called "origin."</span><span class="sxs-lookup"><span data-stu-id="09430-732">- It must reside on a customer origin called "origin."</span></span> <br /><span data-ttu-id="09430-733">- The relative path must start with a folder called "text."</span><span class="sxs-lookup"><span data-stu-id="09430-733">- The relative path must start with a folder called "text."</span></span> <span data-ttu-id="09430-734">That is, the requested asset can either reside in the "text" folder or one of its recursive subfolders.</span><span class="sxs-lookup"><span data-stu-id="09430-734">That is, the requested asset can either reside in the "text" folder or one of its recursive subfolders.</span></span>
<span data-ttu-id="09430-735">*/css/* */js/*</span><span class="sxs-lookup"><span data-stu-id="09430-735">*/css/* */js/*</span></span>          | <span data-ttu-id="09430-736">Root or Origin</span><span class="sxs-lookup"><span data-stu-id="09430-736">Root or Origin</span></span> | <span data-ttu-id="09430-737">This pattern is matched by all CDN or edge CNAME URLs that contain a css or js folder.</span><span class="sxs-lookup"><span data-stu-id="09430-737">This pattern is matched by all CDN or edge CNAME URLs that contain a css or js folder.</span></span>
<span data-ttu-id="09430-738">\*.jpg \*.gif \*.png</span><span class="sxs-lookup"><span data-stu-id="09430-738">\*.jpg \*.gif \*.png</span></span>       | <span data-ttu-id="09430-739">Root or Origin</span><span class="sxs-lookup"><span data-stu-id="09430-739">Root or Origin</span></span> | <span data-ttu-id="09430-740">This pattern is matched by all CDN or edge CNAME URLs ending with .jpg, .gif, or .png.</span><span class="sxs-lookup"><span data-stu-id="09430-740">This pattern is matched by all CDN or edge CNAME URLs ending with .jpg, .gif, or .png.</span></span> <span data-ttu-id="09430-741">An alternative way to specify this pattern is with the [URL Path Extension match condition](#url-path-extension).</span><span class="sxs-lookup"><span data-stu-id="09430-741">An alternative way to specify this pattern is with the [URL Path Extension match condition](#url-path-extension).</span></span>
<span data-ttu-id="09430-742">/images/\* /media/\*</span><span class="sxs-lookup"><span data-stu-id="09430-742">/images/\* /media/\*</span></span>      | <span data-ttu-id="09430-743">Origin</span><span class="sxs-lookup"><span data-stu-id="09430-743">Origin</span></span>         | <span data-ttu-id="09430-744">This pattern is matched by CDN or edge CNAME URLs whose relative path starts with an "images" or "media" folder.</span><span class="sxs-lookup"><span data-stu-id="09430-744">This pattern is matched by CDN or edge CNAME URLs whose relative path starts with an "images" or "media" folder.</span></span> <br /><span data-ttu-id="09430-745">- CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/images/sales/event1.png</span><span class="sxs-lookup"><span data-stu-id="09430-745">- CDN URL: http:\//wpc.0001.&lt;domain&gt;/800001/myorigin/images/sales/event1.png</span></span><br /><span data-ttu-id="09430-746">- Sample edge CNAME URL: http:\//cdn.mydomain.com/images/sales/event1.png</span><span class="sxs-lookup"><span data-stu-id="09430-746">- Sample edge CNAME URL: http:\//cdn.mydomain.com/images/sales/event1.png</span></span>

[<span data-ttu-id="09430-747">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-747">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-query-literal"></a><span data-ttu-id="09430-748">URL Query Literal</span><span class="sxs-lookup"><span data-stu-id="09430-748">URL Query Literal</span></span>
<span data-ttu-id="09430-749">Compares a request's query string to the specified value.</span><span class="sxs-lookup"><span data-stu-id="09430-749">Compares a request's query string to the specified value.</span></span>

<span data-ttu-id="09430-750">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Literal match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-750">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Literal match condition is met.</span></span>
- <span data-ttu-id="09430-751">**Matches**: Requires the request to contain a URL query string that matches the specified query string.</span><span class="sxs-lookup"><span data-stu-id="09430-751">**Matches**: Requires the request to contain a URL query string that matches the specified query string.</span></span>
- <span data-ttu-id="09430-752">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified query string.</span><span class="sxs-lookup"><span data-stu-id="09430-752">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified query string.</span></span>

<span data-ttu-id="09430-753">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-753">Key information:</span></span>

- <span data-ttu-id="09430-754">Only exact query string matches satisfy this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-754">Only exact query string matches satisfy this match condition.</span></span>
    
- <span data-ttu-id="09430-755">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-755">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span></span>
    
- <span data-ttu-id="09430-756">Do not include a leading question mark (?) in the query string value text.</span><span class="sxs-lookup"><span data-stu-id="09430-756">Do not include a leading question mark (?) in the query string value text.</span></span>
    
- <span data-ttu-id="09430-757">Certain characters require URL encoding.</span><span class="sxs-lookup"><span data-stu-id="09430-757">Certain characters require URL encoding.</span></span> <span data-ttu-id="09430-758">Use the percentage symbol to URL encode the following characters:</span><span class="sxs-lookup"><span data-stu-id="09430-758">Use the percentage symbol to URL encode the following characters:</span></span>

   <span data-ttu-id="09430-759">Character</span><span class="sxs-lookup"><span data-stu-id="09430-759">Character</span></span> | <span data-ttu-id="09430-760">URL Encoding</span><span class="sxs-lookup"><span data-stu-id="09430-760">URL Encoding</span></span>
   ----------|---------
   <span data-ttu-id="09430-761">Space</span><span class="sxs-lookup"><span data-stu-id="09430-761">Space</span></span>     | <span data-ttu-id="09430-762">%20</span><span class="sxs-lookup"><span data-stu-id="09430-762">%20</span></span>
   &         | <span data-ttu-id="09430-763">%25</span><span class="sxs-lookup"><span data-stu-id="09430-763">%25</span></span>

- <span data-ttu-id="09430-764">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-764">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
   - <span data-ttu-id="09430-765">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-765">Complete Cache Fill</span></span>
   - <span data-ttu-id="09430-766">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-766">Default Internal Max-Age</span></span>
   - <span data-ttu-id="09430-767">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-767">Force Internal Max-Age</span></span>
   - <span data-ttu-id="09430-768">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-768">Ignore Origin No-Cache</span></span>
   - <span data-ttu-id="09430-769">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-769">Internal Max-Stale</span></span>

[<span data-ttu-id="09430-770">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-770">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-query-parameter"></a><span data-ttu-id="09430-771">URL Query Parameter</span><span class="sxs-lookup"><span data-stu-id="09430-771">URL Query Parameter</span></span>
<span data-ttu-id="09430-772">Identifies requests that contain the specified query string parameter.</span><span class="sxs-lookup"><span data-stu-id="09430-772">Identifies requests that contain the specified query string parameter.</span></span> <span data-ttu-id="09430-773">This parameter is set to a value that matches a specified pattern.</span><span class="sxs-lookup"><span data-stu-id="09430-773">This parameter is set to a value that matches a specified pattern.</span></span> <span data-ttu-id="09430-774">Query string parameters (for example, parameter=value) in the request URL determine whether this condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-774">Query string parameters (for example, parameter=value) in the request URL determine whether this condition is met.</span></span> <span data-ttu-id="09430-775">This match condition identifies a query string parameter by its name and accepts one or more values for the parameter value.</span><span class="sxs-lookup"><span data-stu-id="09430-775">This match condition identifies a query string parameter by its name and accepts one or more values for the parameter value.</span></span> 

<span data-ttu-id="09430-776">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Parameter match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-776">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Parameter match condition is met.</span></span>
- <span data-ttu-id="09430-777">**Matches**: Requires a request to contain the specified parameter with a value that matches at least one of the values that are defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-777">**Matches**: Requires a request to contain the specified parameter with a value that matches at least one of the values that are defined in this match condition.</span></span>
- <span data-ttu-id="09430-778">**Does Not Match**: Requires that the request meets either of the following criteria:</span><span class="sxs-lookup"><span data-stu-id="09430-778">**Does Not Match**: Requires that the request meets either of the following criteria:</span></span>
  - <span data-ttu-id="09430-779">It does not contain the specified parameter.</span><span class="sxs-lookup"><span data-stu-id="09430-779">It does not contain the specified parameter.</span></span>
  - <span data-ttu-id="09430-780">It contains the specified parameter, but its value does not match any of the values that are defined in this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-780">It contains the specified parameter, but its value does not match any of the values that are defined in this match condition.</span></span>

<span data-ttu-id="09430-781">This match condition provides an easy way to specify parameter name/value combinations.</span><span class="sxs-lookup"><span data-stu-id="09430-781">This match condition provides an easy way to specify parameter name/value combinations.</span></span> <span data-ttu-id="09430-782">For more flexibility if you are matching a query string parameter, consider using the [URL Query Wildcard](#url-query-wildcard) match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-782">For more flexibility if you are matching a query string parameter, consider using the [URL Query Wildcard](#url-query-wildcard) match condition.</span></span>

<span data-ttu-id="09430-783">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-783">Key information:</span></span>
- <span data-ttu-id="09430-784">Only a single URL query parameter name can be specified per instance of this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-784">Only a single URL query parameter name can be specified per instance of this match condition.</span></span>
    
- <span data-ttu-id="09430-785">Because wildcard values are not supported when a parameter name is specified, only exact parameter name matches are eligible for comparison.</span><span class="sxs-lookup"><span data-stu-id="09430-785">Because wildcard values are not supported when a parameter name is specified, only exact parameter name matches are eligible for comparison.</span></span>
- <span data-ttu-id="09430-786">Parameter value(s) can include [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span><span class="sxs-lookup"><span data-stu-id="09430-786">Parameter value(s) can include [wildcard values](cdn-rules-engine-reference.md#wildcard-values).</span></span>
   - <span data-ttu-id="09430-787">Each parameter value pattern can consist of one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span><span class="sxs-lookup"><span data-stu-id="09430-787">Each parameter value pattern can consist of one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span></span>
   - <span data-ttu-id="09430-788">Certain characters require URL encoding.</span><span class="sxs-lookup"><span data-stu-id="09430-788">Certain characters require URL encoding.</span></span> <span data-ttu-id="09430-789">Use the percentage symbol to URL encode the following characters:</span><span class="sxs-lookup"><span data-stu-id="09430-789">Use the percentage symbol to URL encode the following characters:</span></span>

       <span data-ttu-id="09430-790">Character</span><span class="sxs-lookup"><span data-stu-id="09430-790">Character</span></span> | <span data-ttu-id="09430-791">URL Encoding</span><span class="sxs-lookup"><span data-stu-id="09430-791">URL Encoding</span></span>
       ----------|---------
       <span data-ttu-id="09430-792">Space</span><span class="sxs-lookup"><span data-stu-id="09430-792">Space</span></span>     | <span data-ttu-id="09430-793">%20</span><span class="sxs-lookup"><span data-stu-id="09430-793">%20</span></span>
       &         | <span data-ttu-id="09430-794">%25</span><span class="sxs-lookup"><span data-stu-id="09430-794">%25</span></span>

- <span data-ttu-id="09430-795">Specify multiple query string parameter values by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-795">Specify multiple query string parameter values by delimiting each one with a single space.</span></span> <span data-ttu-id="09430-796">This match condition is met when a request contains one of the specified name/value combinations.</span><span class="sxs-lookup"><span data-stu-id="09430-796">This match condition is met when a request contains one of the specified name/value combinations.</span></span>

   - <span data-ttu-id="09430-797">Example 1:</span><span class="sxs-lookup"><span data-stu-id="09430-797">Example 1:</span></span>

     - <span data-ttu-id="09430-798">Configuration:</span><span class="sxs-lookup"><span data-stu-id="09430-798">Configuration:</span></span>

       <span data-ttu-id="09430-799">ValueA ValueB</span><span class="sxs-lookup"><span data-stu-id="09430-799">ValueA ValueB</span></span>

     - <span data-ttu-id="09430-800">This configuration matches the following query string parameters:</span><span class="sxs-lookup"><span data-stu-id="09430-800">This configuration matches the following query string parameters:</span></span>

       <span data-ttu-id="09430-801">Parameter1=ValueA</span><span class="sxs-lookup"><span data-stu-id="09430-801">Parameter1=ValueA</span></span>
    
       <span data-ttu-id="09430-802">Parameter1=ValueB</span><span class="sxs-lookup"><span data-stu-id="09430-802">Parameter1=ValueB</span></span>

   - <span data-ttu-id="09430-803">Example 2:</span><span class="sxs-lookup"><span data-stu-id="09430-803">Example 2:</span></span>

     - <span data-ttu-id="09430-804">Configuration:</span><span class="sxs-lookup"><span data-stu-id="09430-804">Configuration:</span></span> 

        <span data-ttu-id="09430-805">Value%20A Value%20B</span><span class="sxs-lookup"><span data-stu-id="09430-805">Value%20A Value%20B</span></span>

     - <span data-ttu-id="09430-806">This configuration matches the following query string parameters:</span><span class="sxs-lookup"><span data-stu-id="09430-806">This configuration matches the following query string parameters:</span></span>

       <span data-ttu-id="09430-807">Parameter1=Value%20A</span><span class="sxs-lookup"><span data-stu-id="09430-807">Parameter1=Value%20A</span></span>

       <span data-ttu-id="09430-808">Parameter1=Value%20B</span><span class="sxs-lookup"><span data-stu-id="09430-808">Parameter1=Value%20B</span></span>

- <span data-ttu-id="09430-809">This match condition is met only when there is an exact match to at least one of the specified query string name/value combinations.</span><span class="sxs-lookup"><span data-stu-id="09430-809">This match condition is met only when there is an exact match to at least one of the specified query string name/value combinations.</span></span>

   <span data-ttu-id="09430-810">For example, if you use the configuration in the previous example, the parameter name/value combination "Parameter1=ValueAdd" would not be considered a match.</span><span class="sxs-lookup"><span data-stu-id="09430-810">For example, if you use the configuration in the previous example, the parameter name/value combination "Parameter1=ValueAdd" would not be considered a match.</span></span> <span data-ttu-id="09430-811">However, if you specify either of the following values, it will match that name/value combination:</span><span class="sxs-lookup"><span data-stu-id="09430-811">However, if you specify either of the following values, it will match that name/value combination:</span></span>

   - <span data-ttu-id="09430-812">ValueA ValueB ValueAdd</span><span class="sxs-lookup"><span data-stu-id="09430-812">ValueA ValueB ValueAdd</span></span>
   - <span data-ttu-id="09430-813">ValueA\* ValueB</span><span class="sxs-lookup"><span data-stu-id="09430-813">ValueA\* ValueB</span></span>

- <span data-ttu-id="09430-814">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-814">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span></span>
    
- <span data-ttu-id="09430-815">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-815">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
   - <span data-ttu-id="09430-816">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-816">Complete Cache Fill</span></span>
   - <span data-ttu-id="09430-817">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-817">Default Internal Max-Age</span></span>
   - <span data-ttu-id="09430-818">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-818">Force Internal Max-Age</span></span>
   - <span data-ttu-id="09430-819">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-819">Ignore Origin No-Cache</span></span>
   - <span data-ttu-id="09430-820">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-820">Internal Max-Stale</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="09430-821">Sample scenarios</span><span class="sxs-lookup"><span data-stu-id="09430-821">Sample scenarios</span></span>
<span data-ttu-id="09430-822">The following example demonstrates how this option works in specific situations:</span><span class="sxs-lookup"><span data-stu-id="09430-822">The following example demonstrates how this option works in specific situations:</span></span>

<span data-ttu-id="09430-823">Name</span><span class="sxs-lookup"><span data-stu-id="09430-823">Name</span></span>  | <span data-ttu-id="09430-824">Value</span><span class="sxs-lookup"><span data-stu-id="09430-824">Value</span></span> |  <span data-ttu-id="09430-825">Result</span><span class="sxs-lookup"><span data-stu-id="09430-825">Result</span></span>
------|-------|--------
<span data-ttu-id="09430-826">User</span><span class="sxs-lookup"><span data-stu-id="09430-826">User</span></span>  | <span data-ttu-id="09430-827">Joe</span><span class="sxs-lookup"><span data-stu-id="09430-827">Joe</span></span>   | <span data-ttu-id="09430-828">This pattern is matched when the query string for a requested URL is "?user=joe."</span><span class="sxs-lookup"><span data-stu-id="09430-828">This pattern is matched when the query string for a requested URL is "?user=joe."</span></span>
<span data-ttu-id="09430-829">User</span><span class="sxs-lookup"><span data-stu-id="09430-829">User</span></span>  | *     | <span data-ttu-id="09430-830">This pattern is matched when the query string for a requested URL contains a User parameter.</span><span class="sxs-lookup"><span data-stu-id="09430-830">This pattern is matched when the query string for a requested URL contains a User parameter.</span></span>
<span data-ttu-id="09430-831">Email</span><span class="sxs-lookup"><span data-stu-id="09430-831">Email</span></span> | <span data-ttu-id="09430-832">Joe\*</span><span class="sxs-lookup"><span data-stu-id="09430-832">Joe\*</span></span> | <span data-ttu-id="09430-833">This pattern is matched when the query string for a requested URL contains an Email parameter that starts with "Joe."</span><span class="sxs-lookup"><span data-stu-id="09430-833">This pattern is matched when the query string for a requested URL contains an Email parameter that starts with "Joe."</span></span>

[<span data-ttu-id="09430-834">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-834">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-query-regex"></a><span data-ttu-id="09430-835">URL Query Regex</span><span class="sxs-lookup"><span data-stu-id="09430-835">URL Query Regex</span></span>
<span data-ttu-id="09430-836">Identifies requests that contain the specified query string parameter.</span><span class="sxs-lookup"><span data-stu-id="09430-836">Identifies requests that contain the specified query string parameter.</span></span> <span data-ttu-id="09430-837">This parameter is set to a value that matches a specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span><span class="sxs-lookup"><span data-stu-id="09430-837">This parameter is set to a value that matches a specified [regular expression](cdn-rules-engine-reference.md#regular-expressions).</span></span>

<span data-ttu-id="09430-838">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Regex match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-838">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Regex match condition is met.</span></span>
- <span data-ttu-id="09430-839">**Matches**: Requires the request to contain a URL query string that matches the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-839">**Matches**: Requires the request to contain a URL query string that matches the specified regular expression.</span></span>
- <span data-ttu-id="09430-840">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-840">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified regular expression.</span></span>

<span data-ttu-id="09430-841">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-841">Key information:</span></span>
- <span data-ttu-id="09430-842">Only exact matches to the specified regular expression satisfy this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-842">Only exact matches to the specified regular expression satisfy this match condition.</span></span>
    
- <span data-ttu-id="09430-843">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-843">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span></span>
    
- <span data-ttu-id="09430-844">For the purposes of this option, a query string starts with the first character after the question mark (?) delimiter for the query string.</span><span class="sxs-lookup"><span data-stu-id="09430-844">For the purposes of this option, a query string starts with the first character after the question mark (?) delimiter for the query string.</span></span>
    
- <span data-ttu-id="09430-845">Certain characters require URL encoding.</span><span class="sxs-lookup"><span data-stu-id="09430-845">Certain characters require URL encoding.</span></span> <span data-ttu-id="09430-846">Use the percentage symbol to URL encode the following characters:</span><span class="sxs-lookup"><span data-stu-id="09430-846">Use the percentage symbol to URL encode the following characters:</span></span>

   <span data-ttu-id="09430-847">Character</span><span class="sxs-lookup"><span data-stu-id="09430-847">Character</span></span> | <span data-ttu-id="09430-848">URL Encoding</span><span class="sxs-lookup"><span data-stu-id="09430-848">URL Encoding</span></span> | <span data-ttu-id="09430-849">Value</span><span class="sxs-lookup"><span data-stu-id="09430-849">Value</span></span>
   ----------|--------------|------
   <span data-ttu-id="09430-850">Space</span><span class="sxs-lookup"><span data-stu-id="09430-850">Space</span></span>     | <span data-ttu-id="09430-851">%20</span><span class="sxs-lookup"><span data-stu-id="09430-851">%20</span></span>          | <span data-ttu-id="09430-852">\%20</span><span class="sxs-lookup"><span data-stu-id="09430-852">\%20</span></span>
   &         | <span data-ttu-id="09430-853">%25</span><span class="sxs-lookup"><span data-stu-id="09430-853">%25</span></span>          | <span data-ttu-id="09430-854">\%25</span><span class="sxs-lookup"><span data-stu-id="09430-854">\%25</span></span>

   <span data-ttu-id="09430-855">Note that percentage symbols must be escaped.</span><span class="sxs-lookup"><span data-stu-id="09430-855">Note that percentage symbols must be escaped.</span></span>

- <span data-ttu-id="09430-856">Double-escape special regular expression characters (for example, \^$.+) to include a backslash in the regular expression.</span><span class="sxs-lookup"><span data-stu-id="09430-856">Double-escape special regular expression characters (for example, \^$.+) to include a backslash in the regular expression.</span></span>

   <span data-ttu-id="09430-857">For example:</span><span class="sxs-lookup"><span data-stu-id="09430-857">For example:</span></span>

   <span data-ttu-id="09430-858">Value</span><span class="sxs-lookup"><span data-stu-id="09430-858">Value</span></span> | <span data-ttu-id="09430-859">Interpreted As</span><span class="sxs-lookup"><span data-stu-id="09430-859">Interpreted As</span></span> 
   ------|---------------
   \\+    | +
   \\\\+   | \\+

- <span data-ttu-id="09430-860">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-860">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
   - <span data-ttu-id="09430-861">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-861">Complete Cache Fill</span></span>
   - <span data-ttu-id="09430-862">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-862">Default Internal Max-Age</span></span>
   - <span data-ttu-id="09430-863">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-863">Force Internal Max-Age</span></span>
   - <span data-ttu-id="09430-864">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-864">Ignore Origin No-Cache</span></span>
   - <span data-ttu-id="09430-865">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-865">Internal Max-Stale</span></span>


[<span data-ttu-id="09430-866">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-866">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

---
### <a name="url-query-wildcard"></a><span data-ttu-id="09430-867">URL Query Wildcard</span><span class="sxs-lookup"><span data-stu-id="09430-867">URL Query Wildcard</span></span>
<span data-ttu-id="09430-868">Compares the specified value(s) against the request's query string.</span><span class="sxs-lookup"><span data-stu-id="09430-868">Compares the specified value(s) against the request's query string.</span></span>

<span data-ttu-id="09430-869">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Wildcard match condition is met.</span><span class="sxs-lookup"><span data-stu-id="09430-869">The **Matches**/**Does Not Match** option determines the conditions under which the URL Query Wildcard match condition is met.</span></span>
- <span data-ttu-id="09430-870">**Matches**: Requires the request to contain a URL query string that matches the specified wildcard value.</span><span class="sxs-lookup"><span data-stu-id="09430-870">**Matches**: Requires the request to contain a URL query string that matches the specified wildcard value.</span></span>
- <span data-ttu-id="09430-871">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified wildcard value.</span><span class="sxs-lookup"><span data-stu-id="09430-871">**Does Not Match**: Requires the request to contain a URL query string that does not match the specified wildcard value.</span></span>

<span data-ttu-id="09430-872">Key information:</span><span class="sxs-lookup"><span data-stu-id="09430-872">Key information:</span></span>
- <span data-ttu-id="09430-873">For the purposes of this option, a query string starts with the first character after the question mark (?) delimiter for the query string.</span><span class="sxs-lookup"><span data-stu-id="09430-873">For the purposes of this option, a query string starts with the first character after the question mark (?) delimiter for the query string.</span></span>
- <span data-ttu-id="09430-874">Parameter values can include [wildcard values](cdn-rules-engine-reference.md#wildcard-values):</span><span class="sxs-lookup"><span data-stu-id="09430-874">Parameter values can include [wildcard values](cdn-rules-engine-reference.md#wildcard-values):</span></span>
   - <span data-ttu-id="09430-875">Each parameter value pattern can consist of one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span><span class="sxs-lookup"><span data-stu-id="09430-875">Each parameter value pattern can consist of one or more asterisks (\*), where each asterisk can match a sequence of one or more characters.</span></span>
   - <span data-ttu-id="09430-876">Certain characters require URL encoding.</span><span class="sxs-lookup"><span data-stu-id="09430-876">Certain characters require URL encoding.</span></span> <span data-ttu-id="09430-877">Use the percentage symbol to URL encode the following characters:</span><span class="sxs-lookup"><span data-stu-id="09430-877">Use the percentage symbol to URL encode the following characters:</span></span>

     <span data-ttu-id="09430-878">Character</span><span class="sxs-lookup"><span data-stu-id="09430-878">Character</span></span> | <span data-ttu-id="09430-879">URL Encoding</span><span class="sxs-lookup"><span data-stu-id="09430-879">URL Encoding</span></span>
     ----------|---------
     <span data-ttu-id="09430-880">Space</span><span class="sxs-lookup"><span data-stu-id="09430-880">Space</span></span>     | <span data-ttu-id="09430-881">%20</span><span class="sxs-lookup"><span data-stu-id="09430-881">%20</span></span>
     &         | <span data-ttu-id="09430-882">%25</span><span class="sxs-lookup"><span data-stu-id="09430-882">%25</span></span>

- <span data-ttu-id="09430-883">Specify multiple values by delimiting each one with a single space.</span><span class="sxs-lookup"><span data-stu-id="09430-883">Specify multiple values by delimiting each one with a single space.</span></span>

   <span data-ttu-id="09430-884">For example: *Parameter1=ValueA* *ValueB* *Parameter1=ValueC&Parameter2=ValueD*</span><span class="sxs-lookup"><span data-stu-id="09430-884">For example: *Parameter1=ValueA* *ValueB* *Parameter1=ValueC&Parameter2=ValueD*</span></span>

- <span data-ttu-id="09430-885">Only exact matches to at least one of the specified query string patterns satisfy this match condition.</span><span class="sxs-lookup"><span data-stu-id="09430-885">Only exact matches to at least one of the specified query string patterns satisfy this match condition.</span></span>
    
- <span data-ttu-id="09430-886">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span><span class="sxs-lookup"><span data-stu-id="09430-886">Use the **Ignore Case** option to control the case-sensitivity of query string comparisons.</span></span>
    
- <span data-ttu-id="09430-887">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span><span class="sxs-lookup"><span data-stu-id="09430-887">Due to the manner in which cache settings are tracked, this match condition is incompatible with the following features:</span></span>
   - <span data-ttu-id="09430-888">Complete Cache Fill</span><span class="sxs-lookup"><span data-stu-id="09430-888">Complete Cache Fill</span></span>
   - <span data-ttu-id="09430-889">Default Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-889">Default Internal Max-Age</span></span>
   - <span data-ttu-id="09430-890">Force Internal Max-Age</span><span class="sxs-lookup"><span data-stu-id="09430-890">Force Internal Max-Age</span></span>
   - <span data-ttu-id="09430-891">Ignore Origin No-Cache</span><span class="sxs-lookup"><span data-stu-id="09430-891">Ignore Origin No-Cache</span></span>
   - <span data-ttu-id="09430-892">Internal Max-Stale</span><span class="sxs-lookup"><span data-stu-id="09430-892">Internal Max-Stale</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="09430-893">Sample scenarios</span><span class="sxs-lookup"><span data-stu-id="09430-893">Sample scenarios</span></span>
<span data-ttu-id="09430-894">The following example demonstrates how this option works in specific situations:</span><span class="sxs-lookup"><span data-stu-id="09430-894">The following example demonstrates how this option works in specific situations:</span></span>

 <span data-ttu-id="09430-895">Name</span><span class="sxs-lookup"><span data-stu-id="09430-895">Name</span></span>                 | <span data-ttu-id="09430-896">Description</span><span class="sxs-lookup"><span data-stu-id="09430-896">Description</span></span>
 ---------------------|------------
<span data-ttu-id="09430-897">user=joe</span><span class="sxs-lookup"><span data-stu-id="09430-897">user=joe</span></span>              | <span data-ttu-id="09430-898">This pattern is matched when the query string for a requested URL is "?user=joe."</span><span class="sxs-lookup"><span data-stu-id="09430-898">This pattern is matched when the query string for a requested URL is "?user=joe."</span></span>
<span data-ttu-id="09430-899">\*user=\* \*optout=\*</span><span class="sxs-lookup"><span data-stu-id="09430-899">\*user=\* \*optout=\*</span></span> | <span data-ttu-id="09430-900">This pattern is matched when the CDN URL query contains either the user or optout parameter.</span><span class="sxs-lookup"><span data-stu-id="09430-900">This pattern is matched when the CDN URL query contains either the user or optout parameter.</span></span>

[<span data-ttu-id="09430-901">Back to top</span><span class="sxs-lookup"><span data-stu-id="09430-901">Back to top</span></span>](#match-conditions-for-the-azure-cdn-rules-engine)

</br>

## <a name="next-steps"></a><span data-ttu-id="09430-902">Next steps</span><span class="sxs-lookup"><span data-stu-id="09430-902">Next steps</span></span>
* [<span data-ttu-id="09430-903">Azure Content Delivery Network overview</span><span class="sxs-lookup"><span data-stu-id="09430-903">Azure Content Delivery Network overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="09430-904">Rules engine reference</span><span class="sxs-lookup"><span data-stu-id="09430-904">Rules engine reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="09430-905">Rules engine conditional expressions</span><span class="sxs-lookup"><span data-stu-id="09430-905">Rules engine conditional expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="09430-906">Rules engine features</span><span class="sxs-lookup"><span data-stu-id="09430-906">Rules engine features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="09430-907">Overriding default HTTP behavior using the rules engine</span><span class="sxs-lookup"><span data-stu-id="09430-907">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)

