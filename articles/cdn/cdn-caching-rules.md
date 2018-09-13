---
title: Control Azure CDN caching behavior with caching rules | Microsoft Docs
description: You can use CDN caching rules to set or modify default cache expiration behavior both globally and with conditions, such as a URL path and file extensions.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: v-deasim
ms.openlocfilehash: 4095ed763de378a673908d033d87b2aa6d72f13c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864512"
---
# <a name="control-azure-cdn-caching-behavior-with-caching-rules"></a><span data-ttu-id="ed58b-103">Control Azure CDN caching behavior with caching rules</span><span class="sxs-lookup"><span data-stu-id="ed58b-103">Control Azure CDN caching behavior with caching rules</span></span>

> [!NOTE] 
> <span data-ttu-id="ed58b-104">Caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span><span class="sxs-lookup"><span data-stu-id="ed58b-104">Caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span> <span data-ttu-id="ed58b-105">For **Azure CDN Premium from Verizon** profiles, you must use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.</span><span class="sxs-lookup"><span data-stu-id="ed58b-105">For **Azure CDN Premium from Verizon** profiles, you must use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.</span></span>
 
<span data-ttu-id="ed58b-106">Azure Content Delivery Network (CDN) offers two ways to control how your files are cached:</span><span class="sxs-lookup"><span data-stu-id="ed58b-106">Azure Content Delivery Network (CDN) offers two ways to control how your files are cached:</span></span> 

- <span data-ttu-id="ed58b-107">Caching rules: This article describes how you can use content delivery network (CDN) caching rules to set or modify default cache expiration behavior both globally and with custom conditions, such as a URL path and file extension.</span><span class="sxs-lookup"><span data-stu-id="ed58b-107">Caching rules: This article describes how you can use content delivery network (CDN) caching rules to set or modify default cache expiration behavior both globally and with custom conditions, such as a URL path and file extension.</span></span> <span data-ttu-id="ed58b-108">Azure CDN provides two types of caching rules:</span><span class="sxs-lookup"><span data-stu-id="ed58b-108">Azure CDN provides two types of caching rules:</span></span>

   - <span data-ttu-id="ed58b-109">Global caching rules: You can set one global caching rule for each endpoint in your profile, which affects all requests to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="ed58b-109">Global caching rules: You can set one global caching rule for each endpoint in your profile, which affects all requests to the endpoint.</span></span> <span data-ttu-id="ed58b-110">The global caching rule overrides any HTTP cache-directive headers, if set.</span><span class="sxs-lookup"><span data-stu-id="ed58b-110">The global caching rule overrides any HTTP cache-directive headers, if set.</span></span>

   - <span data-ttu-id="ed58b-111">Custom caching rules: You can set one or more custom caching rules for each endpoint in your profile.</span><span class="sxs-lookup"><span data-stu-id="ed58b-111">Custom caching rules: You can set one or more custom caching rules for each endpoint in your profile.</span></span> <span data-ttu-id="ed58b-112">Custom caching rules match specific paths and file extensions, are processed in order, and override the global caching rule, if set.</span><span class="sxs-lookup"><span data-stu-id="ed58b-112">Custom caching rules match specific paths and file extensions, are processed in order, and override the global caching rule, if set.</span></span> 

- <span data-ttu-id="ed58b-113">Query string caching: You can adjust how the Azure CDN treats caching for requests with query strings.</span><span class="sxs-lookup"><span data-stu-id="ed58b-113">Query string caching: You can adjust how the Azure CDN treats caching for requests with query strings.</span></span> <span data-ttu-id="ed58b-114">For information, see [Control Azure CDN caching behavior with query strings](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="ed58b-114">For information, see [Control Azure CDN caching behavior with query strings](cdn-query-string.md).</span></span> <span data-ttu-id="ed58b-115">If the file is not cacheable, the query string caching setting has no effect, based on caching rules and CDN default behaviors.</span><span class="sxs-lookup"><span data-stu-id="ed58b-115">If the file is not cacheable, the query string caching setting has no effect, based on caching rules and CDN default behaviors.</span></span>

<span data-ttu-id="ed58b-116">For information about default caching behavior and caching directive headers, see [How caching works](cdn-how-caching-works.md).</span><span class="sxs-lookup"><span data-stu-id="ed58b-116">For information about default caching behavior and caching directive headers, see [How caching works](cdn-how-caching-works.md).</span></span> 


## <a name="accessing-azure-cdn-caching-rules"></a><span data-ttu-id="ed58b-117">Accessing Azure CDN caching rules</span><span class="sxs-lookup"><span data-stu-id="ed58b-117">Accessing Azure CDN caching rules</span></span>

1. <span data-ttu-id="ed58b-118">Open the Azure portal, select a CDN profile, then select an endpoint.</span><span class="sxs-lookup"><span data-stu-id="ed58b-118">Open the Azure portal, select a CDN profile, then select an endpoint.</span></span>

2. <span data-ttu-id="ed58b-119">In the left pane under Settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="ed58b-119">In the left pane under Settings, select **Caching rules**.</span></span>

   ![CDN Caching rules button](./media/cdn-caching-rules/cdn-caching-rules-btn.png)

   <span data-ttu-id="ed58b-121">The **Caching rules** page appears.</span><span class="sxs-lookup"><span data-stu-id="ed58b-121">The **Caching rules** page appears.</span></span>

   ![CDN Caching rules page](./media/cdn-caching-rules/cdn-caching-rules-page.png)


## <a name="caching-behavior-settings"></a><span data-ttu-id="ed58b-123">Caching behavior settings</span><span class="sxs-lookup"><span data-stu-id="ed58b-123">Caching behavior settings</span></span>
<span data-ttu-id="ed58b-124">For global and custom caching rules, you can specify the following **Caching behavior** settings:</span><span class="sxs-lookup"><span data-stu-id="ed58b-124">For global and custom caching rules, you can specify the following **Caching behavior** settings:</span></span>

- <span data-ttu-id="ed58b-125">**Bypass cache**: Do not cache and ignore origin-provided cache-directive headers.</span><span class="sxs-lookup"><span data-stu-id="ed58b-125">**Bypass cache**: Do not cache and ignore origin-provided cache-directive headers.</span></span>

- <span data-ttu-id="ed58b-126">**Override**: Ignore origin-provided cache-directive headers; use the provided cache duration instead.</span><span class="sxs-lookup"><span data-stu-id="ed58b-126">**Override**: Ignore origin-provided cache-directive headers; use the provided cache duration instead.</span></span>

- <span data-ttu-id="ed58b-127">**Set if missing**: Honor origin-provided cache-directive headers, if they exist; otherwise, use the provided cache duration.</span><span class="sxs-lookup"><span data-stu-id="ed58b-127">**Set if missing**: Honor origin-provided cache-directive headers, if they exist; otherwise, use the provided cache duration.</span></span>

![Global caching rules](./media/cdn-caching-rules/cdn-global-caching-rules.png)

![Custom caching rules](./media/cdn-caching-rules/cdn-custom-caching-rules.png)

## <a name="cache-expiration-duration"></a><span data-ttu-id="ed58b-130">Cache expiration duration</span><span class="sxs-lookup"><span data-stu-id="ed58b-130">Cache expiration duration</span></span>
<span data-ttu-id="ed58b-131">For global and custom caching rules, you can specify the cache expiration duration in days, hours, minutes, and seconds:</span><span class="sxs-lookup"><span data-stu-id="ed58b-131">For global and custom caching rules, you can specify the cache expiration duration in days, hours, minutes, and seconds:</span></span>

- <span data-ttu-id="ed58b-132">For the **Override** and **Set if missing** **Caching behavior** settings, valid cache durations range between 0 seconds and 366 days.</span><span class="sxs-lookup"><span data-stu-id="ed58b-132">For the **Override** and **Set if missing** **Caching behavior** settings, valid cache durations range between 0 seconds and 366 days.</span></span> <span data-ttu-id="ed58b-133">For a value of 0 seconds, the CDN caches the content, but must revalidate each request with the origin server.</span><span class="sxs-lookup"><span data-stu-id="ed58b-133">For a value of 0 seconds, the CDN caches the content, but must revalidate each request with the origin server.</span></span>

- <span data-ttu-id="ed58b-134">For the **Bypass cache** setting, the cache duration is automatically set to 0 seconds and cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="ed58b-134">For the **Bypass cache** setting, the cache duration is automatically set to 0 seconds and cannot be changed.</span></span>

## <a name="custom-caching-rules-match-conditions"></a><span data-ttu-id="ed58b-135">Custom caching rules match conditions</span><span class="sxs-lookup"><span data-stu-id="ed58b-135">Custom caching rules match conditions</span></span>

<span data-ttu-id="ed58b-136">For custom cache rules, two match conditions are available:</span><span class="sxs-lookup"><span data-stu-id="ed58b-136">For custom cache rules, two match conditions are available:</span></span>
 
- <span data-ttu-id="ed58b-137">**Path**: This condition matches the path of the URL, excluding the domain name, and supports the wildcard symbol (\*).</span><span class="sxs-lookup"><span data-stu-id="ed58b-137">**Path**: This condition matches the path of the URL, excluding the domain name, and supports the wildcard symbol (\*).</span></span> <span data-ttu-id="ed58b-138">For example, _/myfile.html_, _/my/folder/\*_, and _/my/images/\*.jpg_.</span><span class="sxs-lookup"><span data-stu-id="ed58b-138">For example, _/myfile.html_, _/my/folder/\*_, and _/my/images/\*.jpg_.</span></span> <span data-ttu-id="ed58b-139">The maximum length is 260 characters.</span><span class="sxs-lookup"><span data-stu-id="ed58b-139">The maximum length is 260 characters.</span></span>

- <span data-ttu-id="ed58b-140">**Extension**: This condition matches the file extension of the requested file.</span><span class="sxs-lookup"><span data-stu-id="ed58b-140">**Extension**: This condition matches the file extension of the requested file.</span></span> <span data-ttu-id="ed58b-141">You can provide a list of comma-separated file extensions to match.</span><span class="sxs-lookup"><span data-stu-id="ed58b-141">You can provide a list of comma-separated file extensions to match.</span></span> <span data-ttu-id="ed58b-142">For example, _.jpg_, _.mp3_, or _.png_.</span><span class="sxs-lookup"><span data-stu-id="ed58b-142">For example, _.jpg_, _.mp3_, or _.png_.</span></span> <span data-ttu-id="ed58b-143">The maximum number of extensions is 50 and the maximum number of characters per extension is 16.</span><span class="sxs-lookup"><span data-stu-id="ed58b-143">The maximum number of extensions is 50 and the maximum number of characters per extension is 16.</span></span> 

## <a name="global-and-custom-rule-processing-order"></a><span data-ttu-id="ed58b-144">Global and custom rule processing order</span><span class="sxs-lookup"><span data-stu-id="ed58b-144">Global and custom rule processing order</span></span>
<span data-ttu-id="ed58b-145">Global and custom caching rules are processed in the following order:</span><span class="sxs-lookup"><span data-stu-id="ed58b-145">Global and custom caching rules are processed in the following order:</span></span>

- <span data-ttu-id="ed58b-146">Global caching rules take precedence over the default CDN caching behavior (HTTP cache-directive header settings).</span><span class="sxs-lookup"><span data-stu-id="ed58b-146">Global caching rules take precedence over the default CDN caching behavior (HTTP cache-directive header settings).</span></span> 

- <span data-ttu-id="ed58b-147">Custom caching rules take precedence over global caching rules, where they apply.</span><span class="sxs-lookup"><span data-stu-id="ed58b-147">Custom caching rules take precedence over global caching rules, where they apply.</span></span> <span data-ttu-id="ed58b-148">Custom caching rules are processed in order from top to bottom.</span><span class="sxs-lookup"><span data-stu-id="ed58b-148">Custom caching rules are processed in order from top to bottom.</span></span> <span data-ttu-id="ed58b-149">That is, if a request matches both conditions, rules at the bottom of the list take precedence over rules at the top of the list.</span><span class="sxs-lookup"><span data-stu-id="ed58b-149">That is, if a request matches both conditions, rules at the bottom of the list take precedence over rules at the top of the list.</span></span> <span data-ttu-id="ed58b-150">Therefore, you should place more specific rules lower in the list.</span><span class="sxs-lookup"><span data-stu-id="ed58b-150">Therefore, you should place more specific rules lower in the list.</span></span>

<span data-ttu-id="ed58b-151">**Example**:</span><span class="sxs-lookup"><span data-stu-id="ed58b-151">**Example**:</span></span>
- <span data-ttu-id="ed58b-152">Global caching rule:</span><span class="sxs-lookup"><span data-stu-id="ed58b-152">Global caching rule:</span></span> 
   - <span data-ttu-id="ed58b-153">Caching behavior: **Override**</span><span class="sxs-lookup"><span data-stu-id="ed58b-153">Caching behavior: **Override**</span></span>
   - <span data-ttu-id="ed58b-154">Cache expiration duration: 1 day</span><span class="sxs-lookup"><span data-stu-id="ed58b-154">Cache expiration duration: 1 day</span></span>

- <span data-ttu-id="ed58b-155">Custom caching rule #1:</span><span class="sxs-lookup"><span data-stu-id="ed58b-155">Custom caching rule #1:</span></span>
   - <span data-ttu-id="ed58b-156">Match condition: **Path**</span><span class="sxs-lookup"><span data-stu-id="ed58b-156">Match condition: **Path**</span></span>
   - <span data-ttu-id="ed58b-157">Match value: _/home/\*_</span><span class="sxs-lookup"><span data-stu-id="ed58b-157">Match value: _/home/\*_</span></span>
   - <span data-ttu-id="ed58b-158">Caching behavior: **Override**</span><span class="sxs-lookup"><span data-stu-id="ed58b-158">Caching behavior: **Override**</span></span>
   - <span data-ttu-id="ed58b-159">Cache expiration duration: 2 days</span><span class="sxs-lookup"><span data-stu-id="ed58b-159">Cache expiration duration: 2 days</span></span>

- <span data-ttu-id="ed58b-160">Custom caching rule #2:</span><span class="sxs-lookup"><span data-stu-id="ed58b-160">Custom caching rule #2:</span></span>
   - <span data-ttu-id="ed58b-161">Match condition: **Extension**</span><span class="sxs-lookup"><span data-stu-id="ed58b-161">Match condition: **Extension**</span></span>
   - <span data-ttu-id="ed58b-162">Match value: _.html_</span><span class="sxs-lookup"><span data-stu-id="ed58b-162">Match value: _.html_</span></span>
   - <span data-ttu-id="ed58b-163">Caching behavior: **Set if missing**</span><span class="sxs-lookup"><span data-stu-id="ed58b-163">Caching behavior: **Set if missing**</span></span>
   - <span data-ttu-id="ed58b-164">Cache expiration duration: 3 days</span><span class="sxs-lookup"><span data-stu-id="ed58b-164">Cache expiration duration: 3 days</span></span>

<span data-ttu-id="ed58b-165">When these rules are set, a request for _&lt;endpoint hostname&gt;_.azureedge.net/home/index.html triggers custom caching rule #2, which is set to: **Set if missing** and 3 days.</span><span class="sxs-lookup"><span data-stu-id="ed58b-165">When these rules are set, a request for _&lt;endpoint hostname&gt;_.azureedge.net/home/index.html triggers custom caching rule #2, which is set to: **Set if missing** and 3 days.</span></span> <span data-ttu-id="ed58b-166">Therefore, if the *index.html* file has `Cache-Control` or `Expires` HTTP headers, they are honored; otherwise, if these headers are not set, the file is cached for 3 days.</span><span class="sxs-lookup"><span data-stu-id="ed58b-166">Therefore, if the *index.html* file has `Cache-Control` or `Expires` HTTP headers, they are honored; otherwise, if these headers are not set, the file is cached for 3 days.</span></span>

> [!NOTE] 
> <span data-ttu-id="ed58b-167">Files that are cached before a rule change maintain their origin cache duration setting.</span><span class="sxs-lookup"><span data-stu-id="ed58b-167">Files that are cached before a rule change maintain their origin cache duration setting.</span></span> <span data-ttu-id="ed58b-168">To reset their cache durations, you must [purge the file](cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ed58b-168">To reset their cache durations, you must [purge the file](cdn-purge-endpoint.md).</span></span> 
>
> <span data-ttu-id="ed58b-169">Azure CDN configuration changes can take some time to propagate through the network:</span><span class="sxs-lookup"><span data-stu-id="ed58b-169">Azure CDN configuration changes can take some time to propagate through the network:</span></span> 
> - <span data-ttu-id="ed58b-170">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span><span class="sxs-lookup"><span data-stu-id="ed58b-170">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span></span> 
> - <span data-ttu-id="ed58b-171">For **Azure CDN Standard from Verizon** profiles, propagation usually completes in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ed58b-171">For **Azure CDN Standard from Verizon** profiles, propagation usually completes in 10 minutes.</span></span>  
>

## <a name="see-also"></a><span data-ttu-id="ed58b-172">See also</span><span class="sxs-lookup"><span data-stu-id="ed58b-172">See also</span></span>

- [<span data-ttu-id="ed58b-173">How caching works</span><span class="sxs-lookup"><span data-stu-id="ed58b-173">How caching works</span></span>](cdn-how-caching-works.md)
- [<span data-ttu-id="ed58b-174">Tutorial: Set Azure CDN caching rules</span><span class="sxs-lookup"><span data-stu-id="ed58b-174">Tutorial: Set Azure CDN caching rules</span></span>](cdn-caching-rules-tutorial.md)
