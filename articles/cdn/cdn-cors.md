---
title: Using Azure CDN with CORS | Microsoft Docs
description: Learn how to use the Azure Content Delivery Network (CDN) to with Cross-Origin Resource Sharing (CORS).
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 96d992bcb9018782e146e05d225cb46c54f4fb9c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672451"
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="c264b-103">Using Azure CDN with CORS</span><span class="sxs-lookup"><span data-stu-id="c264b-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="c264b-104">What is CORS?</span><span class="sxs-lookup"><span data-stu-id="c264b-104">What is CORS?</span></span>
<span data-ttu-id="c264b-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span><span class="sxs-lookup"><span data-stu-id="c264b-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="c264b-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="c264b-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="c264b-107">This prevents a web page from calling APIs in a different domain.</span><span class="sxs-lookup"><span data-stu-id="c264b-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="c264b-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span><span class="sxs-lookup"><span data-stu-id="c264b-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c264b-109">How it works</span><span class="sxs-lookup"><span data-stu-id="c264b-109">How it works</span></span>
<span data-ttu-id="c264b-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span><span class="sxs-lookup"><span data-stu-id="c264b-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="c264b-111">For simple requests:</span><span class="sxs-lookup"><span data-stu-id="c264b-111">For simple requests:</span></span>

1. <span data-ttu-id="c264b-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span><span class="sxs-lookup"><span data-stu-id="c264b-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="c264b-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span><span class="sxs-lookup"><span data-stu-id="c264b-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="c264b-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="c264b-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="c264b-115">The server may respond with any of the following:</span><span class="sxs-lookup"><span data-stu-id="c264b-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="c264b-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span><span class="sxs-lookup"><span data-stu-id="c264b-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="c264b-117">For example:</span><span class="sxs-lookup"><span data-stu-id="c264b-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="c264b-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span><span class="sxs-lookup"><span data-stu-id="c264b-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="c264b-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span><span class="sxs-lookup"><span data-stu-id="c264b-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="c264b-120">For complex requests:</span><span class="sxs-lookup"><span data-stu-id="c264b-120">For complex requests:</span></span>

<span data-ttu-id="c264b-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span><span class="sxs-lookup"><span data-stu-id="c264b-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="c264b-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span><span class="sxs-lookup"><span data-stu-id="c264b-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="c264b-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="c264b-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="c264b-124">Wildcard or single origin scenarios</span><span class="sxs-lookup"><span data-stu-id="c264b-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="c264b-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (\*) or a single origin.</span><span class="sxs-lookup"><span data-stu-id="c264b-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (\*) or a single origin.</span></span>  <span data-ttu-id="c264b-126">The CDN will cache the first response and subsequent requests will use the same header.</span><span class="sxs-lookup"><span data-stu-id="c264b-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="c264b-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span><span class="sxs-lookup"><span data-stu-id="c264b-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="c264b-128">Multiple origin scenarios</span><span class="sxs-lookup"><span data-stu-id="c264b-128">Multiple origin scenarios</span></span>
<span data-ttu-id="c264b-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span><span class="sxs-lookup"><span data-stu-id="c264b-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="c264b-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span><span class="sxs-lookup"><span data-stu-id="c264b-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="c264b-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span><span class="sxs-lookup"><span data-stu-id="c264b-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="c264b-132">There are several ways to correct this.</span><span class="sxs-lookup"><span data-stu-id="c264b-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="c264b-133">Azure CDN Premium from Verizon</span><span class="sxs-lookup"><span data-stu-id="c264b-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="c264b-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span><span class="sxs-lookup"><span data-stu-id="c264b-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="c264b-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span><span class="sxs-lookup"><span data-stu-id="c264b-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="c264b-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span><span class="sxs-lookup"><span data-stu-id="c264b-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="c264b-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span><span class="sxs-lookup"><span data-stu-id="c264b-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="c264b-138">There are two ways to do this with the rules engine.</span><span class="sxs-lookup"><span data-stu-id="c264b-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="c264b-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span><span class="sxs-lookup"><span data-stu-id="c264b-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="c264b-140">One regular expression with all valid origins</span><span class="sxs-lookup"><span data-stu-id="c264b-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="c264b-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span><span class="sxs-lookup"><span data-stu-id="c264b-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="c264b-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span><span class="sxs-lookup"><span data-stu-id="c264b-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="c264b-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span><span class="sxs-lookup"><span data-stu-id="c264b-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="c264b-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span><span class="sxs-lookup"><span data-stu-id="c264b-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="c264b-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span><span class="sxs-lookup"><span data-stu-id="c264b-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="c264b-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="c264b-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Rules example with regular expression](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="c264b-148">Request header rule for each origin.</span><span class="sxs-lookup"><span data-stu-id="c264b-148">Request header rule for each origin.</span></span>
<span data-ttu-id="c264b-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="c264b-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="c264b-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span><span class="sxs-lookup"><span data-stu-id="c264b-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Rules example without regular expression](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="c264b-152">In the example above, the use of the wildcard character \* tells the rules engine to match both HTTP and HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c264b-152">In the example above, the use of the wildcard character \* tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="c264b-153">Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="c264b-153">Azure CDN Standard</span></span>
<span data-ttu-id="c264b-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="c264b-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="c264b-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span><span class="sxs-lookup"><span data-stu-id="c264b-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="c264b-156">Doing this will result in the CDN caching a separate object for each unique query string.</span><span class="sxs-lookup"><span data-stu-id="c264b-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="c264b-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span><span class="sxs-lookup"><span data-stu-id="c264b-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  


