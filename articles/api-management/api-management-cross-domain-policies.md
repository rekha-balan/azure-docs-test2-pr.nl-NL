---
title: Azure API Management cross domain policies | Microsoft Docs
description: Learn about the cross domain policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553626"
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="0df94-103">API Management cross domain policies</span><span class="sxs-lookup"><span data-stu-id="0df94-103">API Management cross domain policies</span></span>
<span data-ttu-id="0df94-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="0df94-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="0df94-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="0df94-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="CrossDomainPolicies"></a> <span data-ttu-id="0df94-106">Cross domain policies</span><span class="sxs-lookup"><span data-stu-id="0df94-106">Cross domain policies</span></span>  
  
-   <span data-ttu-id="0df94-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="0df94-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="0df94-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <a name="AllowCrossDomainCalls"></a> <span data-ttu-id="0df94-110">Allow cross-domain calls</span><span class="sxs-lookup"><span data-stu-id="0df94-110">Allow cross-domain calls</span></span>  
 <span data-ttu-id="0df94-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0df94-112">Policy statement</span><span class="sxs-lookup"><span data-stu-id="0df94-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="0df94-113">Example</span><span class="sxs-lookup"><span data-stu-id="0df94-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="0df94-114">Elements</span><span class="sxs-lookup"><span data-stu-id="0df94-114">Elements</span></span>  
  
|<span data-ttu-id="0df94-115">Name</span><span class="sxs-lookup"><span data-stu-id="0df94-115">Name</span></span>|<span data-ttu-id="0df94-116">Description</span><span class="sxs-lookup"><span data-stu-id="0df94-116">Description</span></span>|<span data-ttu-id="0df94-117">Required</span><span class="sxs-lookup"><span data-stu-id="0df94-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0df94-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="0df94-118">cross-domain</span></span>|<span data-ttu-id="0df94-119">Root element.</span><span class="sxs-lookup"><span data-stu-id="0df94-119">Root element.</span></span> <span data-ttu-id="0df94-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="0df94-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="0df94-121">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0df94-122">Usage</span><span class="sxs-lookup"><span data-stu-id="0df94-122">Usage</span></span>  
 <span data-ttu-id="0df94-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0df94-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0df94-124">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="0df94-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0df94-125">**Policy scopes:** global</span><span class="sxs-lookup"><span data-stu-id="0df94-125">**Policy scopes:** global</span></span>  
  
##  <a name="CORS"></a> <span data-ttu-id="0df94-126">CORS</span><span class="sxs-lookup"><span data-stu-id="0df94-126">CORS</span></span>  
 <span data-ttu-id="0df94-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="0df94-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span><span class="sxs-lookup"><span data-stu-id="0df94-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="0df94-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span><span class="sxs-lookup"><span data-stu-id="0df94-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0df94-130">Policy statement</span><span class="sxs-lookup"><span data-stu-id="0df94-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="0df94-131">Example</span><span class="sxs-lookup"><span data-stu-id="0df94-131">Example</span></span>  
 <span data-ttu-id="0df94-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span><span class="sxs-lookup"><span data-stu-id="0df94-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="0df94-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="0df94-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="0df94-134">Elements</span><span class="sxs-lookup"><span data-stu-id="0df94-134">Elements</span></span>  
  
|<span data-ttu-id="0df94-135">Name</span><span class="sxs-lookup"><span data-stu-id="0df94-135">Name</span></span>|<span data-ttu-id="0df94-136">Description</span><span class="sxs-lookup"><span data-stu-id="0df94-136">Description</span></span>|<span data-ttu-id="0df94-137">Required</span><span class="sxs-lookup"><span data-stu-id="0df94-137">Required</span></span>|<span data-ttu-id="0df94-138">Default</span><span class="sxs-lookup"><span data-stu-id="0df94-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0df94-139">cors</span><span class="sxs-lookup"><span data-stu-id="0df94-139">cors</span></span>|<span data-ttu-id="0df94-140">Root element.</span><span class="sxs-lookup"><span data-stu-id="0df94-140">Root element.</span></span>|<span data-ttu-id="0df94-141">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-141">Yes</span></span>|<span data-ttu-id="0df94-142">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-142">N/A</span></span>|  
|<span data-ttu-id="0df94-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="0df94-143">allowed-origins</span></span>|<span data-ttu-id="0df94-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span><span class="sxs-lookup"><span data-stu-id="0df94-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="0df94-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span><span class="sxs-lookup"><span data-stu-id="0df94-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="0df94-146">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-146">Yes</span></span>|<span data-ttu-id="0df94-147">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-147">N/A</span></span>|  
|<span data-ttu-id="0df94-148">origin</span><span class="sxs-lookup"><span data-stu-id="0df94-148">origin</span></span>|<span data-ttu-id="0df94-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span><span class="sxs-lookup"><span data-stu-id="0df94-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="0df94-150">The URI must include a scheme, host, and port.</span><span class="sxs-lookup"><span data-stu-id="0df94-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="0df94-151">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-151">Yes</span></span>|<span data-ttu-id="0df94-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0df94-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="0df94-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="0df94-153">allowed-methods</span></span>|<span data-ttu-id="0df94-154">This element is required if methods other than GET or POST are allowed.</span><span class="sxs-lookup"><span data-stu-id="0df94-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="0df94-155">Contains `method` elements that specify the supported HTTP verbs.</span><span class="sxs-lookup"><span data-stu-id="0df94-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="0df94-156">No</span><span class="sxs-lookup"><span data-stu-id="0df94-156">No</span></span>|<span data-ttu-id="0df94-157">If this section is not present, GET and POST are supported.</span><span class="sxs-lookup"><span data-stu-id="0df94-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="0df94-158">method</span><span class="sxs-lookup"><span data-stu-id="0df94-158">method</span></span>|<span data-ttu-id="0df94-159">Specifies an HTTP verb.</span><span class="sxs-lookup"><span data-stu-id="0df94-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="0df94-160">At least one `method` element is required if the `allowed-methods` section is present.</span><span class="sxs-lookup"><span data-stu-id="0df94-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="0df94-161">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-161">N/A</span></span>|  
|<span data-ttu-id="0df94-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="0df94-162">allowed-headers</span></span>|<span data-ttu-id="0df94-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span><span class="sxs-lookup"><span data-stu-id="0df94-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="0df94-164">No</span><span class="sxs-lookup"><span data-stu-id="0df94-164">No</span></span>|<span data-ttu-id="0df94-165">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-165">N/A</span></span>|  
|<span data-ttu-id="0df94-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="0df94-166">expose-headers</span></span>|<span data-ttu-id="0df94-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span><span class="sxs-lookup"><span data-stu-id="0df94-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="0df94-168">No</span><span class="sxs-lookup"><span data-stu-id="0df94-168">No</span></span>|<span data-ttu-id="0df94-169">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-169">N/A</span></span>|  
|<span data-ttu-id="0df94-170">header</span><span class="sxs-lookup"><span data-stu-id="0df94-170">header</span></span>|<span data-ttu-id="0df94-171">Specifies a header name.</span><span class="sxs-lookup"><span data-stu-id="0df94-171">Specifies a header name.</span></span>|<span data-ttu-id="0df94-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span><span class="sxs-lookup"><span data-stu-id="0df94-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="0df94-173">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0df94-174">Attributes</span><span class="sxs-lookup"><span data-stu-id="0df94-174">Attributes</span></span>  
  
|<span data-ttu-id="0df94-175">Name</span><span class="sxs-lookup"><span data-stu-id="0df94-175">Name</span></span>|<span data-ttu-id="0df94-176">Description</span><span class="sxs-lookup"><span data-stu-id="0df94-176">Description</span></span>|<span data-ttu-id="0df94-177">Required</span><span class="sxs-lookup"><span data-stu-id="0df94-177">Required</span></span>|<span data-ttu-id="0df94-178">Default</span><span class="sxs-lookup"><span data-stu-id="0df94-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0df94-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="0df94-179">allow-credentials</span></span>|<span data-ttu-id="0df94-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span><span class="sxs-lookup"><span data-stu-id="0df94-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="0df94-181">No</span><span class="sxs-lookup"><span data-stu-id="0df94-181">No</span></span>|<span data-ttu-id="0df94-182">false</span><span class="sxs-lookup"><span data-stu-id="0df94-182">false</span></span>|  
|<span data-ttu-id="0df94-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="0df94-183">preflight-result-max-age</span></span>|<span data-ttu-id="0df94-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span><span class="sxs-lookup"><span data-stu-id="0df94-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="0df94-185">No</span><span class="sxs-lookup"><span data-stu-id="0df94-185">No</span></span>|<span data-ttu-id="0df94-186">0</span><span class="sxs-lookup"><span data-stu-id="0df94-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0df94-187">Usage</span><span class="sxs-lookup"><span data-stu-id="0df94-187">Usage</span></span>  
 <span data-ttu-id="0df94-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0df94-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0df94-189">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="0df94-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0df94-190">**Policy scopes:** API, operation</span><span class="sxs-lookup"><span data-stu-id="0df94-190">**Policy scopes:** API, operation</span></span>  
  
##  <a name="JSONP"></a> <span data-ttu-id="0df94-191">JSONP</span><span class="sxs-lookup"><span data-stu-id="0df94-191">JSONP</span></span>  
 <span data-ttu-id="0df94-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span><span class="sxs-lookup"><span data-stu-id="0df94-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="0df94-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span><span class="sxs-lookup"><span data-stu-id="0df94-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="0df94-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span><span class="sxs-lookup"><span data-stu-id="0df94-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0df94-195">Policy statement</span><span class="sxs-lookup"><span data-stu-id="0df94-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="0df94-196">Example</span><span class="sxs-lookup"><span data-stu-id="0df94-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="0df94-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span><span class="sxs-lookup"><span data-stu-id="0df94-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="0df94-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="0df94-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0df94-199">Elements</span><span class="sxs-lookup"><span data-stu-id="0df94-199">Elements</span></span>  
  
|<span data-ttu-id="0df94-200">Name</span><span class="sxs-lookup"><span data-stu-id="0df94-200">Name</span></span>|<span data-ttu-id="0df94-201">Description</span><span class="sxs-lookup"><span data-stu-id="0df94-201">Description</span></span>|<span data-ttu-id="0df94-202">Required</span><span class="sxs-lookup"><span data-stu-id="0df94-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0df94-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="0df94-203">jsonp</span></span>|<span data-ttu-id="0df94-204">Root element.</span><span class="sxs-lookup"><span data-stu-id="0df94-204">Root element.</span></span>|<span data-ttu-id="0df94-205">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0df94-206">Attributes</span><span class="sxs-lookup"><span data-stu-id="0df94-206">Attributes</span></span>  
  
|<span data-ttu-id="0df94-207">Name</span><span class="sxs-lookup"><span data-stu-id="0df94-207">Name</span></span>|<span data-ttu-id="0df94-208">Description</span><span class="sxs-lookup"><span data-stu-id="0df94-208">Description</span></span>|<span data-ttu-id="0df94-209">Required</span><span class="sxs-lookup"><span data-stu-id="0df94-209">Required</span></span>|<span data-ttu-id="0df94-210">Default</span><span class="sxs-lookup"><span data-stu-id="0df94-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0df94-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="0df94-211">callback-parameter-name</span></span>|<span data-ttu-id="0df94-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span><span class="sxs-lookup"><span data-stu-id="0df94-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="0df94-213">Yes</span><span class="sxs-lookup"><span data-stu-id="0df94-213">Yes</span></span>|<span data-ttu-id="0df94-214">N/A</span><span class="sxs-lookup"><span data-stu-id="0df94-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0df94-215">Usage</span><span class="sxs-lookup"><span data-stu-id="0df94-215">Usage</span></span>  
 <span data-ttu-id="0df94-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0df94-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0df94-217">**Policy sections:** outbound</span><span class="sxs-lookup"><span data-stu-id="0df94-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="0df94-218">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="0df94-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0df94-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="0df94-219">Next steps</span></span>
<span data-ttu-id="0df94-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0df94-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  