---
title: Verizon-specific HTTP headers for Azure CDN rules engine | Microsoft Docs
description: This article describes how to use Verizon-specific HTTP headers with Azure CDN rules engine.
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
ms.date: 04/16/2018
ms.author: v-deasim
ms.openlocfilehash: 1a4bb48efe2a91c85b773341bb38b0f3ce4c7d9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869956"
---
# <a name="verizon-specific-http-headers-for-azure-cdn-rules-engine"></a><span data-ttu-id="d1d40-103">Verizon-specific HTTP headers for Azure CDN rules engine</span><span class="sxs-lookup"><span data-stu-id="d1d40-103">Verizon-specific HTTP headers for Azure CDN rules engine</span></span>

<span data-ttu-id="d1d40-104">For **Azure CDN Premium from Verizon** products, when an HTTP request is sent to the origin server, the point-of-presence (POP) server can add one or more reserved headers (or proxy special headers) in the client request to the POP.</span><span class="sxs-lookup"><span data-stu-id="d1d40-104">For **Azure CDN Premium from Verizon** products, when an HTTP request is sent to the origin server, the point-of-presence (POP) server can add one or more reserved headers (or proxy special headers) in the client request to the POP.</span></span> <span data-ttu-id="d1d40-105">These headers are in addition to the standard forwarding headers received.</span><span class="sxs-lookup"><span data-stu-id="d1d40-105">These headers are in addition to the standard forwarding headers received.</span></span> <span data-ttu-id="d1d40-106">For information about standard request headers, see [Request fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields).</span><span class="sxs-lookup"><span data-stu-id="d1d40-106">For information about standard request headers, see [Request fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields).</span></span>

<span data-ttu-id="d1d40-107">If you want to prevent one of these reserved headers from being added in the Azure CDN (Content Delivery Network) POP request to the origin server, you must create a rule with the [Proxy Special Headers feature](cdn-rules-engine-reference-features.md#proxy-special-headers) in the rules engine.</span><span class="sxs-lookup"><span data-stu-id="d1d40-107">If you want to prevent one of these reserved headers from being added in the Azure CDN (Content Delivery Network) POP request to the origin server, you must create a rule with the [Proxy Special Headers feature](cdn-rules-engine-reference-features.md#proxy-special-headers) in the rules engine.</span></span> <span data-ttu-id="d1d40-108">In this rule, exclude the header you want to remove from the default list of headers in the headers field.</span><span class="sxs-lookup"><span data-stu-id="d1d40-108">In this rule, exclude the header you want to remove from the default list of headers in the headers field.</span></span> <span data-ttu-id="d1d40-109">If you've enabled the [Debug Cache Response Headers feature](cdn-rules-engine-reference-features.md#debug-cache-response-headers), be sure to add the necessary `X-EC-Debug` headers.</span><span class="sxs-lookup"><span data-stu-id="d1d40-109">If you've enabled the [Debug Cache Response Headers feature](cdn-rules-engine-reference-features.md#debug-cache-response-headers), be sure to add the necessary `X-EC-Debug` headers.</span></span> 

<span data-ttu-id="d1d40-110">For example, to remove the `Via` header, the headers field of the rule should include the following list of headers: *X-Forwarded-For, X-Forwarded-Proto, X-Host, X-Midgress, X-Gateway-List, X-EC-Name, Host*.</span><span class="sxs-lookup"><span data-stu-id="d1d40-110">For example, to remove the `Via` header, the headers field of the rule should include the following list of headers: *X-Forwarded-For, X-Forwarded-Proto, X-Host, X-Midgress, X-Gateway-List, X-EC-Name, Host*.</span></span> 

![Proxy Special Headers rule](./media/cdn-http-headers/cdn-proxy-special-header-rule.png)

<span data-ttu-id="d1d40-112">The following table describes the headers that can be added by the Verizon CDN POP in the request:</span><span class="sxs-lookup"><span data-stu-id="d1d40-112">The following table describes the headers that can be added by the Verizon CDN POP in the request:</span></span>

<span data-ttu-id="d1d40-113">Request header</span><span class="sxs-lookup"><span data-stu-id="d1d40-113">Request header</span></span> | <span data-ttu-id="d1d40-114">Description</span><span class="sxs-lookup"><span data-stu-id="d1d40-114">Description</span></span> | <span data-ttu-id="d1d40-115">Example</span><span class="sxs-lookup"><span data-stu-id="d1d40-115">Example</span></span>
---------------|-------------|--------
[<span data-ttu-id="d1d40-116">Via</span><span class="sxs-lookup"><span data-stu-id="d1d40-116">Via</span></span>](#via-request-header) | <span data-ttu-id="d1d40-117">Identifies the POP server that proxied the request to an origin server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-117">Identifies the POP server that proxied the request to an origin server.</span></span> | <span data-ttu-id="d1d40-118">HTTP/1.1 ECS (dca/1A2B)</span><span class="sxs-lookup"><span data-stu-id="d1d40-118">HTTP/1.1 ECS (dca/1A2B)</span></span>
<span data-ttu-id="d1d40-119">X-Forwarded-For</span><span class="sxs-lookup"><span data-stu-id="d1d40-119">X-Forwarded-For</span></span> | <span data-ttu-id="d1d40-120">Indicates the requester's IP address.</span><span class="sxs-lookup"><span data-stu-id="d1d40-120">Indicates the requester's IP address.</span></span>| <span data-ttu-id="d1d40-121">10.10.10.10</span><span class="sxs-lookup"><span data-stu-id="d1d40-121">10.10.10.10</span></span>
<span data-ttu-id="d1d40-122">X-Forwarded-Proto</span><span class="sxs-lookup"><span data-stu-id="d1d40-122">X-Forwarded-Proto</span></span> | <span data-ttu-id="d1d40-123">Indicates the request's protocol.</span><span class="sxs-lookup"><span data-stu-id="d1d40-123">Indicates the request's protocol.</span></span> | <span data-ttu-id="d1d40-124">http</span><span class="sxs-lookup"><span data-stu-id="d1d40-124">http</span></span>
<span data-ttu-id="d1d40-125">X-Host</span><span class="sxs-lookup"><span data-stu-id="d1d40-125">X-Host</span></span> | <span data-ttu-id="d1d40-126">Indicates the request's hostname.</span><span class="sxs-lookup"><span data-stu-id="d1d40-126">Indicates the request's hostname.</span></span> | <span data-ttu-id="d1d40-127">cdn.mydomain.com</span><span class="sxs-lookup"><span data-stu-id="d1d40-127">cdn.mydomain.com</span></span>
<span data-ttu-id="d1d40-128">X-Midgress</span><span class="sxs-lookup"><span data-stu-id="d1d40-128">X-Midgress</span></span> | <span data-ttu-id="d1d40-129">Indicates whether the request was proxied through an additional CDN server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-129">Indicates whether the request was proxied through an additional CDN server.</span></span> <span data-ttu-id="d1d40-130">For example, a POP server-to-origin shield server or a POP server-to-ADN gateway server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-130">For example, a POP server-to-origin shield server or a POP server-to-ADN gateway server.</span></span> <br /><span data-ttu-id="d1d40-131">This header is added to the request only when midgress traffic takes place.</span><span class="sxs-lookup"><span data-stu-id="d1d40-131">This header is added to the request only when midgress traffic takes place.</span></span> <span data-ttu-id="d1d40-132">In this case, the header is set to 1 to indicate that the request was proxied through an additional CDN server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-132">In this case, the header is set to 1 to indicate that the request was proxied through an additional CDN server.</span></span>| <span data-ttu-id="d1d40-133">1</span><span class="sxs-lookup"><span data-stu-id="d1d40-133">1</span></span>
[<span data-ttu-id="d1d40-134">Host</span><span class="sxs-lookup"><span data-stu-id="d1d40-134">Host</span></span>](#host-request-header) | <span data-ttu-id="d1d40-135">Identifies the host and the port where the requested content may be found.</span><span class="sxs-lookup"><span data-stu-id="d1d40-135">Identifies the host and the port where the requested content may be found.</span></span> | <span data-ttu-id="d1d40-136">marketing.mydomain.com:80</span><span class="sxs-lookup"><span data-stu-id="d1d40-136">marketing.mydomain.com:80</span></span>
[<span data-ttu-id="d1d40-137">X-Gateway-List</span><span class="sxs-lookup"><span data-stu-id="d1d40-137">X-Gateway-List</span></span>](#x-gateway-list-request-header) | <span data-ttu-id="d1d40-138">ADN: Identifies the failover list of ADN Gateway servers assigned to a customer origin.</span><span class="sxs-lookup"><span data-stu-id="d1d40-138">ADN: Identifies the failover list of ADN Gateway servers assigned to a customer origin.</span></span> <br /><span data-ttu-id="d1d40-139">Origin shield: Indicates the set of origin shield servers assigned to a customer origin.</span><span class="sxs-lookup"><span data-stu-id="d1d40-139">Origin shield: Indicates the set of origin shield servers assigned to a customer origin.</span></span> | `icn1,hhp1,hnd1`
<span data-ttu-id="d1d40-140">X-EC-_&lt;name&gt;_</span><span class="sxs-lookup"><span data-stu-id="d1d40-140">X-EC-_&lt;name&gt;_</span></span> | <span data-ttu-id="d1d40-141">Request headers that begin with *X-EC* (for example, X-EC-Tag, [X-EC-Debug](cdn-http-debug-headers.md)) are reserved for use by the CDN.</span><span class="sxs-lookup"><span data-stu-id="d1d40-141">Request headers that begin with *X-EC* (for example, X-EC-Tag, [X-EC-Debug](cdn-http-debug-headers.md)) are reserved for use by the CDN.</span></span>| <span data-ttu-id="d1d40-142">waf-production</span><span class="sxs-lookup"><span data-stu-id="d1d40-142">waf-production</span></span>

## <a name="via-request-header"></a><span data-ttu-id="d1d40-143">Via request header</span><span class="sxs-lookup"><span data-stu-id="d1d40-143">Via request header</span></span>
<span data-ttu-id="d1d40-144">The format through which the `Via` request header identifies a POP server is specified by the following syntax:</span><span class="sxs-lookup"><span data-stu-id="d1d40-144">The format through which the `Via` request header identifies a POP server is specified by the following syntax:</span></span>

`Via: Protocol from Platform (POP/ID)` 

<span data-ttu-id="d1d40-145">The terms used in the syntax are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="d1d40-145">The terms used in the syntax are defined as follows:</span></span>
- <span data-ttu-id="d1d40-146">Protocol: Indicates the version of the protocol (for example, HTTP/1.1) used to proxy the request.</span><span class="sxs-lookup"><span data-stu-id="d1d40-146">Protocol: Indicates the version of the protocol (for example, HTTP/1.1) used to proxy the request.</span></span> 

- <span data-ttu-id="d1d40-147">Platform: Indicates the platform on which the content was requested.</span><span class="sxs-lookup"><span data-stu-id="d1d40-147">Platform: Indicates the platform on which the content was requested.</span></span> <span data-ttu-id="d1d40-148">The following codes are valid for this field:</span><span class="sxs-lookup"><span data-stu-id="d1d40-148">The following codes are valid for this field:</span></span> 
    <span data-ttu-id="d1d40-149">Code</span><span class="sxs-lookup"><span data-stu-id="d1d40-149">Code</span></span> | <span data-ttu-id="d1d40-150">Platform</span><span class="sxs-lookup"><span data-stu-id="d1d40-150">Platform</span></span>
    -----|---------
    <span data-ttu-id="d1d40-151">ECAcc</span><span class="sxs-lookup"><span data-stu-id="d1d40-151">ECAcc</span></span> | <span data-ttu-id="d1d40-152">HTTP Large</span><span class="sxs-lookup"><span data-stu-id="d1d40-152">HTTP Large</span></span>
    <span data-ttu-id="d1d40-153">ECS</span><span class="sxs-lookup"><span data-stu-id="d1d40-153">ECS</span></span>   | <span data-ttu-id="d1d40-154">HTTP Small</span><span class="sxs-lookup"><span data-stu-id="d1d40-154">HTTP Small</span></span>
    <span data-ttu-id="d1d40-155">ECD</span><span class="sxs-lookup"><span data-stu-id="d1d40-155">ECD</span></span>   | <span data-ttu-id="d1d40-156">Application delivery network (ADN)</span><span class="sxs-lookup"><span data-stu-id="d1d40-156">Application delivery network (ADN)</span></span>

- <span data-ttu-id="d1d40-157">POP: Indicates the [POP](cdn-pop-abbreviations.md) that handled the request.</span><span class="sxs-lookup"><span data-stu-id="d1d40-157">POP: Indicates the [POP](cdn-pop-abbreviations.md) that handled the request.</span></span> 

- <span data-ttu-id="d1d40-158">ID: For internal use only.</span><span class="sxs-lookup"><span data-stu-id="d1d40-158">ID: For internal use only.</span></span>

### <a name="example-via-request-header"></a><span data-ttu-id="d1d40-159">Example Via request header</span><span class="sxs-lookup"><span data-stu-id="d1d40-159">Example Via request header</span></span>

`Via: HTTP/1.1 ECD (dca/1A2B)`

## <a name="host-request-header"></a><span data-ttu-id="d1d40-160">Host request header</span><span class="sxs-lookup"><span data-stu-id="d1d40-160">Host request header</span></span>
<span data-ttu-id="d1d40-161">The POP servers will overwrite the `Host` header when both of the following conditions are true:</span><span class="sxs-lookup"><span data-stu-id="d1d40-161">The POP servers will overwrite the `Host` header when both of the following conditions are true:</span></span>
- <span data-ttu-id="d1d40-162">The source for the requested content is a customer origin server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-162">The source for the requested content is a customer origin server.</span></span>
- <span data-ttu-id="d1d40-163">The corresponding customer origin's HTTP Host Header option is not blank.</span><span class="sxs-lookup"><span data-stu-id="d1d40-163">The corresponding customer origin's HTTP Host Header option is not blank.</span></span>

<span data-ttu-id="d1d40-164">The `Host` request header will be overwritten to reflect the value defined in the HTTP Host Header option.</span><span class="sxs-lookup"><span data-stu-id="d1d40-164">The `Host` request header will be overwritten to reflect the value defined in the HTTP Host Header option.</span></span>
<span data-ttu-id="d1d40-165">If the customer origin's HTTP Host Header option is set to blank, then the `Host` request header that is submitted by the requester will be forwarded to the customer's origin server.</span><span class="sxs-lookup"><span data-stu-id="d1d40-165">If the customer origin's HTTP Host Header option is set to blank, then the `Host` request header that is submitted by the requester will be forwarded to the customer's origin server.</span></span>

## <a name="x-gateway-list-request-header"></a><span data-ttu-id="d1d40-166">X-Gateway-List request header</span><span class="sxs-lookup"><span data-stu-id="d1d40-166">X-Gateway-List request header</span></span>
<span data-ttu-id="d1d40-167">A POP server will add/overwrite the \`X-Gateway-List request header when either of the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="d1d40-167">A POP server will add/overwrite the \`X-Gateway-List request header when either of the following conditions are met:</span></span>
- <span data-ttu-id="d1d40-168">The request points to the ADN platform.</span><span class="sxs-lookup"><span data-stu-id="d1d40-168">The request points to the ADN platform.</span></span>
- <span data-ttu-id="d1d40-169">The request is forwarded to a customer origin server that is protected by the Origin Shield feature.</span><span class="sxs-lookup"><span data-stu-id="d1d40-169">The request is forwarded to a customer origin server that is protected by the Origin Shield feature.</span></span>

