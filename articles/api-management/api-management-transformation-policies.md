---
title: Azure API Management transformation policies | Microsoft Docs
description: Learn about the transformation policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c46a85aaf5237a2a7643cc9069255bdad9ab1d69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540690"
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="bee80-103">API Management transformation policies</span><span class="sxs-lookup"><span data-stu-id="bee80-103">API Management transformation policies</span></span>
<span data-ttu-id="bee80-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="bee80-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="bee80-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="bee80-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="TransformationPolicies"></a> <span data-ttu-id="bee80-106">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="bee80-106">Transformation policies</span></span>  
  
-   <span data-ttu-id="bee80-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span><span class="sxs-lookup"><span data-stu-id="bee80-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="bee80-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span><span class="sxs-lookup"><span data-stu-id="bee80-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="bee80-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span><span class="sxs-lookup"><span data-stu-id="bee80-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="bee80-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span><span class="sxs-lookup"><span data-stu-id="bee80-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="bee80-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span><span class="sxs-lookup"><span data-stu-id="bee80-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="bee80-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span><span class="sxs-lookup"><span data-stu-id="bee80-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="bee80-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span><span class="sxs-lookup"><span data-stu-id="bee80-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="bee80-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span><span class="sxs-lookup"><span data-stu-id="bee80-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="bee80-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span><span class="sxs-lookup"><span data-stu-id="bee80-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="bee80-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span><span class="sxs-lookup"><span data-stu-id="bee80-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <a name="ConvertJSONtoXML"></a> <span data-ttu-id="bee80-117">Convert JSON to XML</span><span class="sxs-lookup"><span data-stu-id="bee80-117">Convert JSON to XML</span></span>  
 <span data-ttu-id="bee80-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span><span class="sxs-lookup"><span data-stu-id="bee80-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-119">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-120">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="bee80-121">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-121">Elements</span></span>  
  
|<span data-ttu-id="bee80-122">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-122">Name</span></span>|<span data-ttu-id="bee80-123">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-123">Description</span></span>|<span data-ttu-id="bee80-124">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="bee80-125">json-to-xml</span></span>|<span data-ttu-id="bee80-126">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-126">Root element.</span></span>|<span data-ttu-id="bee80-127">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bee80-128">Attributes</span><span class="sxs-lookup"><span data-stu-id="bee80-128">Attributes</span></span>  
  
|<span data-ttu-id="bee80-129">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-129">Name</span></span>|<span data-ttu-id="bee80-130">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-130">Description</span></span>|<span data-ttu-id="bee80-131">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-131">Required</span></span>|<span data-ttu-id="bee80-132">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-133">apply</span><span class="sxs-lookup"><span data-stu-id="bee80-133">apply</span></span>|<span data-ttu-id="bee80-134">The attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-135">-   always - always apply conversion.</span><span class="sxs-lookup"><span data-stu-id="bee80-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="bee80-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span><span class="sxs-lookup"><span data-stu-id="bee80-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="bee80-137">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-137">Yes</span></span>|<span data-ttu-id="bee80-138">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-138">N/A</span></span>|  
|<span data-ttu-id="bee80-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="bee80-139">consider-accept-header</span></span>|<span data-ttu-id="bee80-140">The attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-141">-   true - apply conversion if JSON is requested in request Accept header.</span><span class="sxs-lookup"><span data-stu-id="bee80-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="bee80-142">-   false -always apply conversion.</span><span class="sxs-lookup"><span data-stu-id="bee80-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="bee80-143">No</span><span class="sxs-lookup"><span data-stu-id="bee80-143">No</span></span>|<span data-ttu-id="bee80-144">true</span><span class="sxs-lookup"><span data-stu-id="bee80-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-145">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-145">Usage</span></span>  
 <span data-ttu-id="bee80-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-147">**Policy sections:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="bee80-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="bee80-148">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="ConvertXMLtoJSON"></a> <span data-ttu-id="bee80-149">Convert XML to JSON</span><span class="sxs-lookup"><span data-stu-id="bee80-149">Convert XML to JSON</span></span>  
 <span data-ttu-id="bee80-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span><span class="sxs-lookup"><span data-stu-id="bee80-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="bee80-151">This policy can be used to modernize APIs based on XML-only backend web services.</span><span class="sxs-lookup"><span data-stu-id="bee80-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-152">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-153">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="bee80-154">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-154">Elements</span></span>  
  
|<span data-ttu-id="bee80-155">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-155">Name</span></span>|<span data-ttu-id="bee80-156">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-156">Description</span></span>|<span data-ttu-id="bee80-157">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="bee80-158">xml-to-json</span></span>|<span data-ttu-id="bee80-159">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-159">Root element.</span></span>|<span data-ttu-id="bee80-160">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bee80-161">Attributes</span><span class="sxs-lookup"><span data-stu-id="bee80-161">Attributes</span></span>  
  
|<span data-ttu-id="bee80-162">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-162">Name</span></span>|<span data-ttu-id="bee80-163">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-163">Description</span></span>|<span data-ttu-id="bee80-164">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-164">Required</span></span>|<span data-ttu-id="bee80-165">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-166">kind</span><span class="sxs-lookup"><span data-stu-id="bee80-166">kind</span></span>|<span data-ttu-id="bee80-167">The attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span><span class="sxs-lookup"><span data-stu-id="bee80-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="bee80-169">-   direct - the converted JSON reflects the original XML document's structure.</span><span class="sxs-lookup"><span data-stu-id="bee80-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="bee80-170">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-170">Yes</span></span>|<span data-ttu-id="bee80-171">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-171">N/A</span></span>|  
|<span data-ttu-id="bee80-172">apply</span><span class="sxs-lookup"><span data-stu-id="bee80-172">apply</span></span>|<span data-ttu-id="bee80-173">The attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-174">-   always - convert always.</span><span class="sxs-lookup"><span data-stu-id="bee80-174">-   always - convert always.</span></span><br /><span data-ttu-id="bee80-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span><span class="sxs-lookup"><span data-stu-id="bee80-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="bee80-176">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-176">Yes</span></span>|<span data-ttu-id="bee80-177">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-177">N/A</span></span>|  
|<span data-ttu-id="bee80-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="bee80-178">consider-accept-header</span></span>|<span data-ttu-id="bee80-179">The attribute must be set to one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-180">-   true - apply conversion if XML is requested in request Accept header.</span><span class="sxs-lookup"><span data-stu-id="bee80-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="bee80-181">-   false -always apply conversion.</span><span class="sxs-lookup"><span data-stu-id="bee80-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="bee80-182">No</span><span class="sxs-lookup"><span data-stu-id="bee80-182">No</span></span>|<span data-ttu-id="bee80-183">true</span><span class="sxs-lookup"><span data-stu-id="bee80-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-184">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-184">Usage</span></span>  
 <span data-ttu-id="bee80-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-186">**Policy sections:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="bee80-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="bee80-187">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="Findandreplacestringinbody"></a> <span data-ttu-id="bee80-188">Find and replace string in body</span><span class="sxs-lookup"><span data-stu-id="bee80-188">Find and replace string in body</span></span>  
 <span data-ttu-id="bee80-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span><span class="sxs-lookup"><span data-stu-id="bee80-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-190">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-191">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="bee80-192">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-192">Elements</span></span>  
  
|<span data-ttu-id="bee80-193">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-193">Name</span></span>|<span data-ttu-id="bee80-194">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-194">Description</span></span>|<span data-ttu-id="bee80-195">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="bee80-196">find-and-replace</span></span>|<span data-ttu-id="bee80-197">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-197">Root element.</span></span>|<span data-ttu-id="bee80-198">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bee80-199">Attributes</span><span class="sxs-lookup"><span data-stu-id="bee80-199">Attributes</span></span>  
  
|<span data-ttu-id="bee80-200">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-200">Name</span></span>|<span data-ttu-id="bee80-201">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-201">Description</span></span>|<span data-ttu-id="bee80-202">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-202">Required</span></span>|<span data-ttu-id="bee80-203">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-204">from</span><span class="sxs-lookup"><span data-stu-id="bee80-204">from</span></span>|<span data-ttu-id="bee80-205">The string to search for.</span><span class="sxs-lookup"><span data-stu-id="bee80-205">The string to search for.</span></span>|<span data-ttu-id="bee80-206">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-206">Yes</span></span>|<span data-ttu-id="bee80-207">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-207">N/A</span></span>|  
|<span data-ttu-id="bee80-208">to</span><span class="sxs-lookup"><span data-stu-id="bee80-208">to</span></span>|<span data-ttu-id="bee80-209">The replacement string.</span><span class="sxs-lookup"><span data-stu-id="bee80-209">The replacement string.</span></span> <span data-ttu-id="bee80-210">Specify a zero length replacement string to remove the search string.</span><span class="sxs-lookup"><span data-stu-id="bee80-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="bee80-211">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-211">Yes</span></span>|<span data-ttu-id="bee80-212">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-213">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-213">Usage</span></span>  
 <span data-ttu-id="bee80-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-215">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bee80-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bee80-216">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="MaskURLSContent"></a> <span data-ttu-id="bee80-217">Mask URLs in content</span><span class="sxs-lookup"><span data-stu-id="bee80-217">Mask URLs in content</span></span>  
 <span data-ttu-id="bee80-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span><span class="sxs-lookup"><span data-stu-id="bee80-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="bee80-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span><span class="sxs-lookup"><span data-stu-id="bee80-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="bee80-220">Use in the inbound section for an opposite effect.</span><span class="sxs-lookup"><span data-stu-id="bee80-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bee80-221">This policy does not change any header values such as `Location` headers.</span><span class="sxs-lookup"><span data-stu-id="bee80-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="bee80-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span><span class="sxs-lookup"><span data-stu-id="bee80-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-223">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-224">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="bee80-225">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-225">Elements</span></span>  
  
|<span data-ttu-id="bee80-226">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-226">Name</span></span>|<span data-ttu-id="bee80-227">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-227">Description</span></span>|<span data-ttu-id="bee80-228">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="bee80-229">redirect-content-urls</span></span>|<span data-ttu-id="bee80-230">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-230">Root element.</span></span>|<span data-ttu-id="bee80-231">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-232">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-232">Usage</span></span>  
 <span data-ttu-id="bee80-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-234">**Policy sections:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="bee80-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="bee80-235">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetBackendService"></a> <span data-ttu-id="bee80-236">Set backend service</span><span class="sxs-lookup"><span data-stu-id="bee80-236">Set backend service</span></span>  
 <span data-ttu-id="bee80-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span><span class="sxs-lookup"><span data-stu-id="bee80-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="bee80-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span><span class="sxs-lookup"><span data-stu-id="bee80-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-239">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-240">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
 <span data-ttu-id="bee80-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span><span class="sxs-lookup"><span data-stu-id="bee80-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>  
  
 <span data-ttu-id="bee80-242">Initially the backend service base URL is derived from the API settings.</span><span class="sxs-lookup"><span data-stu-id="bee80-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="bee80-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span><span class="sxs-lookup"><span data-stu-id="bee80-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
 <span data-ttu-id="bee80-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span><span class="sxs-lookup"><span data-stu-id="bee80-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="bee80-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="bee80-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
 <span data-ttu-id="bee80-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span><span class="sxs-lookup"><span data-stu-id="bee80-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="bee80-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span><span class="sxs-lookup"><span data-stu-id="bee80-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="elements"></a><span data-ttu-id="bee80-248">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-248">Elements</span></span>  
  
|<span data-ttu-id="bee80-249">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-249">Name</span></span>|<span data-ttu-id="bee80-250">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-250">Description</span></span>|<span data-ttu-id="bee80-251">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-251">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-252">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="bee80-252">set-backend-service</span></span>|<span data-ttu-id="bee80-253">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-253">Root element.</span></span>|<span data-ttu-id="bee80-254">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-254">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bee80-255">Attributes</span><span class="sxs-lookup"><span data-stu-id="bee80-255">Attributes</span></span>  
  
|<span data-ttu-id="bee80-256">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-256">Name</span></span>|<span data-ttu-id="bee80-257">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-257">Description</span></span>|<span data-ttu-id="bee80-258">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-258">Required</span></span>|<span data-ttu-id="bee80-259">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-259">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-260">base-url</span><span class="sxs-lookup"><span data-stu-id="bee80-260">base-url</span></span>|<span data-ttu-id="bee80-261">New backend service base URL.</span><span class="sxs-lookup"><span data-stu-id="bee80-261">New backend service base URL.</span></span>|<span data-ttu-id="bee80-262">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-262">Yes</span></span>|<span data-ttu-id="bee80-263">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-263">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-264">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-264">Usage</span></span>  
 <span data-ttu-id="bee80-265">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-265">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-266">**Policy sections:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="bee80-266">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="bee80-267">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-267">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetBody"></a> <span data-ttu-id="bee80-268">Set body</span><span class="sxs-lookup"><span data-stu-id="bee80-268">Set body</span></span>  
 <span data-ttu-id="bee80-269">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span><span class="sxs-lookup"><span data-stu-id="bee80-269">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="bee80-270">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span><span class="sxs-lookup"><span data-stu-id="bee80-270">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="bee80-271">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span><span class="sxs-lookup"><span data-stu-id="bee80-271">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="bee80-272">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span><span class="sxs-lookup"><span data-stu-id="bee80-272">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="bee80-273">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span><span class="sxs-lookup"><span data-stu-id="bee80-273">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="bee80-274">Please note the following considerations when using the `set-body` policy.</span><span class="sxs-lookup"><span data-stu-id="bee80-274">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="bee80-275">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span><span class="sxs-lookup"><span data-stu-id="bee80-275">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="bee80-276">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span><span class="sxs-lookup"><span data-stu-id="bee80-276">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="bee80-277">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span><span class="sxs-lookup"><span data-stu-id="bee80-277">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="bee80-278">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span><span class="sxs-lookup"><span data-stu-id="bee80-278">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="bee80-279">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span><span class="sxs-lookup"><span data-stu-id="bee80-279">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-280">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-280">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="bee80-281">Examples</span><span class="sxs-lookup"><span data-stu-id="bee80-281">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="bee80-282">Literal text example</span><span class="sxs-lookup"><span data-stu-id="bee80-282">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="bee80-283">Example accessing the body as a string.</span><span class="sxs-lookup"><span data-stu-id="bee80-283">Example accessing the body as a string.</span></span> <span data-ttu-id="bee80-284">Note that we are preserving the original request body so that we can access it later in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bee80-284">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="bee80-285">Example accessing the body as a JObject.</span><span class="sxs-lookup"><span data-stu-id="bee80-285">Example accessing the body as a JObject.</span></span> <span data-ttu-id="bee80-286">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span><span class="sxs-lookup"><span data-stu-id="bee80-286">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="bee80-287">Filter response based on product</span><span class="sxs-lookup"><span data-stu-id="bee80-287">Filter response based on product</span></span>  
 <span data-ttu-id="bee80-288">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="bee80-288">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="bee80-289">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span><span class="sxs-lookup"><span data-stu-id="bee80-289">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="bee80-290">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span><span class="sxs-lookup"><span data-stu-id="bee80-290">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="bee80-291">Using Liquid templates with set body</span><span class="sxs-lookup"><span data-stu-id="bee80-291">Using Liquid templates with set body</span></span> 
<span data-ttu-id="bee80-292">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span><span class="sxs-lookup"><span data-stu-id="bee80-292">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="bee80-293">This can be very effective if you need to completely reshape the format of your message.</span><span class="sxs-lookup"><span data-stu-id="bee80-293">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bee80-294">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span><span class="sxs-lookup"><span data-stu-id="bee80-294">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="bee80-295">This is particularly important when doing things such as filtering.</span><span class="sxs-lookup"><span data-stu-id="bee80-295">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="bee80-296">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span><span class="sxs-lookup"><span data-stu-id="bee80-296">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="bee80-297">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="bee80-297">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bee80-298">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span><span class="sxs-lookup"><span data-stu-id="bee80-298">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="bee80-299">Convert JSON to SOAP using a Liquid template</span><span class="sxs-lookup"><span data-stu-id="bee80-299">Convert JSON to SOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="bee80-300">Tranform JSON using a Liquid template</span><span class="sxs-lookup"><span data-stu-id="bee80-300">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="bee80-301">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-301">Elements</span></span>  
  
|<span data-ttu-id="bee80-302">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-302">Name</span></span>|<span data-ttu-id="bee80-303">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-303">Description</span></span>|<span data-ttu-id="bee80-304">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-304">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-305">set-body</span><span class="sxs-lookup"><span data-stu-id="bee80-305">set-body</span></span>|<span data-ttu-id="bee80-306">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-306">Root element.</span></span> <span data-ttu-id="bee80-307">Contains the body text or an expressions that returns a body.</span><span class="sxs-lookup"><span data-stu-id="bee80-307">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="bee80-308">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-308">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="bee80-309">Properties</span><span class="sxs-lookup"><span data-stu-id="bee80-309">Properties</span></span>  
  
|<span data-ttu-id="bee80-310">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-310">Name</span></span>|<span data-ttu-id="bee80-311">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-311">Description</span></span>|<span data-ttu-id="bee80-312">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-312">Required</span></span>|<span data-ttu-id="bee80-313">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-313">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-314">template</span><span class="sxs-lookup"><span data-stu-id="bee80-314">template</span></span>|<span data-ttu-id="bee80-315">Used to change the templating mode that the set body policy will run in.</span><span class="sxs-lookup"><span data-stu-id="bee80-315">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="bee80-316">Currently the only supported value is:</span><span class="sxs-lookup"><span data-stu-id="bee80-316">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="bee80-317">- liquid - the set body policy will use the liquid templating engine</span><span class="sxs-lookup"><span data-stu-id="bee80-317">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="bee80-318">No</span><span class="sxs-lookup"><span data-stu-id="bee80-318">No</span></span>|<span data-ttu-id="bee80-319">liquid</span><span class="sxs-lookup"><span data-stu-id="bee80-319">liquid</span></span>|  

<span data-ttu-id="bee80-320">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="bee80-320">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="bee80-321">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-321">Usage</span></span>  
 <span data-ttu-id="bee80-322">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-322">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-323">**Policy sections:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="bee80-323">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="bee80-324">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-324">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetHTTPheader"></a> <span data-ttu-id="bee80-325">Set HTTP header</span><span class="sxs-lookup"><span data-stu-id="bee80-325">Set HTTP header</span></span>  
 <span data-ttu-id="bee80-326">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span><span class="sxs-lookup"><span data-stu-id="bee80-326">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="bee80-327">Inserts a list of HTTP headers into an HTTP message.</span><span class="sxs-lookup"><span data-stu-id="bee80-327">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="bee80-328">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span><span class="sxs-lookup"><span data-stu-id="bee80-328">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="bee80-329">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span><span class="sxs-lookup"><span data-stu-id="bee80-329">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-330">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-330">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="bee80-331">Examples</span><span class="sxs-lookup"><span data-stu-id="bee80-331">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bee80-332">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-332">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="bee80-333">Forward context information to the backend service</span><span class="sxs-lookup"><span data-stu-id="bee80-333">Forward context information to the backend service</span></span>  
 <span data-ttu-id="bee80-334">This example shows how to apply policy at the API level to supply context information to the backend service.</span><span class="sxs-lookup"><span data-stu-id="bee80-334">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="bee80-335">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span><span class="sxs-lookup"><span data-stu-id="bee80-335">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="bee80-336">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span><span class="sxs-lookup"><span data-stu-id="bee80-336">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="bee80-337">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="bee80-337">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="bee80-338">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-338">Elements</span></span>  
  
|<span data-ttu-id="bee80-339">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-339">Name</span></span>|<span data-ttu-id="bee80-340">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-340">Description</span></span>|<span data-ttu-id="bee80-341">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-341">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-342">set-header</span><span class="sxs-lookup"><span data-stu-id="bee80-342">set-header</span></span>|<span data-ttu-id="bee80-343">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-343">Root element.</span></span>|<span data-ttu-id="bee80-344">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-344">Yes</span></span>|  
|<span data-ttu-id="bee80-345">value</span><span class="sxs-lookup"><span data-stu-id="bee80-345">value</span></span>|<span data-ttu-id="bee80-346">Specifies the value of the header to be set.</span><span class="sxs-lookup"><span data-stu-id="bee80-346">Specifies the value of the header to be set.</span></span> <span data-ttu-id="bee80-347">For multiple headers with the same name add additional `value` elements.</span><span class="sxs-lookup"><span data-stu-id="bee80-347">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="bee80-348">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-348">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="bee80-349">Properties</span><span class="sxs-lookup"><span data-stu-id="bee80-349">Properties</span></span>  
  
|<span data-ttu-id="bee80-350">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-350">Name</span></span>|<span data-ttu-id="bee80-351">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-351">Description</span></span>|<span data-ttu-id="bee80-352">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-352">Required</span></span>|<span data-ttu-id="bee80-353">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-353">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-354">exists-action</span><span class="sxs-lookup"><span data-stu-id="bee80-354">exists-action</span></span>|<span data-ttu-id="bee80-355">Specifies what action to take when the header is already specified.</span><span class="sxs-lookup"><span data-stu-id="bee80-355">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="bee80-356">This attribute must have one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-356">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-357">-   override - replaces the value of the existing header.</span><span class="sxs-lookup"><span data-stu-id="bee80-357">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="bee80-358">-   skip - does not replace the existing header value.</span><span class="sxs-lookup"><span data-stu-id="bee80-358">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="bee80-359">-   append - appends the value to the existing header value.</span><span class="sxs-lookup"><span data-stu-id="bee80-359">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="bee80-360">-   delete - removes the header from the request.</span><span class="sxs-lookup"><span data-stu-id="bee80-360">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="bee80-361">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span><span class="sxs-lookup"><span data-stu-id="bee80-361">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bee80-362">No</span><span class="sxs-lookup"><span data-stu-id="bee80-362">No</span></span>|<span data-ttu-id="bee80-363">override</span><span class="sxs-lookup"><span data-stu-id="bee80-363">override</span></span>|  
|<span data-ttu-id="bee80-364">name</span><span class="sxs-lookup"><span data-stu-id="bee80-364">name</span></span>|<span data-ttu-id="bee80-365">Specifies name of the header to be set.</span><span class="sxs-lookup"><span data-stu-id="bee80-365">Specifies name of the header to be set.</span></span>|<span data-ttu-id="bee80-366">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-366">Yes</span></span>|<span data-ttu-id="bee80-367">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-367">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-368">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-368">Usage</span></span>  
 <span data-ttu-id="bee80-369">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-369">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-370">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bee80-370">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bee80-371">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-371">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="SetQueryStringParameter"></a> <span data-ttu-id="bee80-372">Set query string parameter</span><span class="sxs-lookup"><span data-stu-id="bee80-372">Set query string parameter</span></span>  
 <span data-ttu-id="bee80-373">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span><span class="sxs-lookup"><span data-stu-id="bee80-373">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="bee80-374">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span><span class="sxs-lookup"><span data-stu-id="bee80-374">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-375">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-375">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="bee80-376">Examples</span><span class="sxs-lookup"><span data-stu-id="bee80-376">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bee80-377">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-377">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="bee80-378">Forward context information to the backend service</span><span class="sxs-lookup"><span data-stu-id="bee80-378">Forward context information to the backend service</span></span>  
 <span data-ttu-id="bee80-379">This example shows how to apply policy at the API level to supply context information to the backend service.</span><span class="sxs-lookup"><span data-stu-id="bee80-379">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="bee80-380">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span><span class="sxs-lookup"><span data-stu-id="bee80-380">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="bee80-381">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span><span class="sxs-lookup"><span data-stu-id="bee80-381">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="bee80-382">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="bee80-382">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="bee80-383">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-383">Elements</span></span>  
  
|<span data-ttu-id="bee80-384">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-384">Name</span></span>|<span data-ttu-id="bee80-385">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-385">Description</span></span>|<span data-ttu-id="bee80-386">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-386">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-387">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="bee80-387">set-query-parameter</span></span>|<span data-ttu-id="bee80-388">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-388">Root element.</span></span>|<span data-ttu-id="bee80-389">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-389">Yes</span></span>|  
|<span data-ttu-id="bee80-390">value</span><span class="sxs-lookup"><span data-stu-id="bee80-390">value</span></span>|<span data-ttu-id="bee80-391">Specifies the value of the query parameter to be set.</span><span class="sxs-lookup"><span data-stu-id="bee80-391">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="bee80-392">For multiple query parameters with the same name add additional `value` elements.</span><span class="sxs-lookup"><span data-stu-id="bee80-392">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="bee80-393">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-393">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="bee80-394">Properties</span><span class="sxs-lookup"><span data-stu-id="bee80-394">Properties</span></span>  
  
|<span data-ttu-id="bee80-395">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-395">Name</span></span>|<span data-ttu-id="bee80-396">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-396">Description</span></span>|<span data-ttu-id="bee80-397">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-397">Required</span></span>|<span data-ttu-id="bee80-398">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-398">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-399">exists-action</span><span class="sxs-lookup"><span data-stu-id="bee80-399">exists-action</span></span>|<span data-ttu-id="bee80-400">Specifies what action to take when the query parameter is already specified.</span><span class="sxs-lookup"><span data-stu-id="bee80-400">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="bee80-401">This attribute must have one of the following values.</span><span class="sxs-lookup"><span data-stu-id="bee80-401">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bee80-402">-   override - replaces the value of the existing parameter.</span><span class="sxs-lookup"><span data-stu-id="bee80-402">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="bee80-403">-   skip - does not replace the existing query parameter value.</span><span class="sxs-lookup"><span data-stu-id="bee80-403">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="bee80-404">-   append - appends the value to the existing query parameter value.</span><span class="sxs-lookup"><span data-stu-id="bee80-404">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="bee80-405">-   delete - removes the query parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="bee80-405">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="bee80-406">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span><span class="sxs-lookup"><span data-stu-id="bee80-406">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bee80-407">No</span><span class="sxs-lookup"><span data-stu-id="bee80-407">No</span></span>|<span data-ttu-id="bee80-408">override</span><span class="sxs-lookup"><span data-stu-id="bee80-408">override</span></span>|  
|<span data-ttu-id="bee80-409">name</span><span class="sxs-lookup"><span data-stu-id="bee80-409">name</span></span>|<span data-ttu-id="bee80-410">Specifies name of the query parameter to be set.</span><span class="sxs-lookup"><span data-stu-id="bee80-410">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="bee80-411">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-411">Yes</span></span>|<span data-ttu-id="bee80-412">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-412">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-413">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-413">Usage</span></span>  
 <span data-ttu-id="bee80-414">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-414">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-415">**Policy sections:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="bee80-415">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="bee80-416">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-416">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <a name="RewriteURL"></a> <span data-ttu-id="bee80-417">Rewrite URL</span><span class="sxs-lookup"><span data-stu-id="bee80-417">Rewrite URL</span></span>  
 <span data-ttu-id="bee80-418">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="bee80-418">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="bee80-419">Public URL - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="bee80-419">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="bee80-420">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="bee80-420">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="bee80-421">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span><span class="sxs-lookup"><span data-stu-id="bee80-421">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="bee80-422">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span><span class="sxs-lookup"><span data-stu-id="bee80-422">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="bee80-423">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span><span class="sxs-lookup"><span data-stu-id="bee80-423">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bee80-424">You can only add query string parameters using the policy.</span><span class="sxs-lookup"><span data-stu-id="bee80-424">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="bee80-425">You cannot add extra template path parameters in the rewrite URL.</span><span class="sxs-lookup"><span data-stu-id="bee80-425">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="bee80-426">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-426">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-427">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-427">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="bee80-428">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-428">Elements</span></span>  
  
|<span data-ttu-id="bee80-429">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-429">Name</span></span>|<span data-ttu-id="bee80-430">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-430">Description</span></span>|<span data-ttu-id="bee80-431">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-431">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-432">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="bee80-432">rewrite-uri</span></span>|<span data-ttu-id="bee80-433">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-433">Root element.</span></span>|<span data-ttu-id="bee80-434">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-434">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bee80-435">Attributes</span><span class="sxs-lookup"><span data-stu-id="bee80-435">Attributes</span></span>  
  
|<span data-ttu-id="bee80-436">Attribute</span><span class="sxs-lookup"><span data-stu-id="bee80-436">Attribute</span></span>|<span data-ttu-id="bee80-437">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-437">Description</span></span>|<span data-ttu-id="bee80-438">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-438">Required</span></span>|<span data-ttu-id="bee80-439">Default</span><span class="sxs-lookup"><span data-stu-id="bee80-439">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bee80-440">template</span><span class="sxs-lookup"><span data-stu-id="bee80-440">template</span></span>|<span data-ttu-id="bee80-441">The actual web service URL with any query string parameters.</span><span class="sxs-lookup"><span data-stu-id="bee80-441">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="bee80-442">When using expressions, the whole value must be an expression.</span><span class="sxs-lookup"><span data-stu-id="bee80-442">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="bee80-443">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-443">Yes</span></span>|<span data-ttu-id="bee80-444">N/A</span><span class="sxs-lookup"><span data-stu-id="bee80-444">N/A</span></span>|  
|<span data-ttu-id="bee80-445">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="bee80-445">copy-unmatched-params</span></span>|<span data-ttu-id="bee80-446">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span><span class="sxs-lookup"><span data-stu-id="bee80-446">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="bee80-447">No</span><span class="sxs-lookup"><span data-stu-id="bee80-447">No</span></span>|<span data-ttu-id="bee80-448">true</span><span class="sxs-lookup"><span data-stu-id="bee80-448">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-449">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-449">Usage</span></span>  
 <span data-ttu-id="bee80-450">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-450">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-451">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="bee80-451">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="bee80-452">**Policy scopes:** product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-452">**Policy scopes:** product, API, operation</span></span>  
  
##  <a name="XSLTransform"></a> <span data-ttu-id="bee80-453">Transform XML using an XSLT</span><span class="sxs-lookup"><span data-stu-id="bee80-453">Transform XML using an XSLT</span></span>  
 <span data-ttu-id="bee80-454">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span><span class="sxs-lookup"><span data-stu-id="bee80-454">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bee80-455">Policy statement</span><span class="sxs-lookup"><span data-stu-id="bee80-455">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="bee80-456">Example</span><span class="sxs-lookup"><span data-stu-id="bee80-456">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="bee80-457">Elements</span><span class="sxs-lookup"><span data-stu-id="bee80-457">Elements</span></span>  
  
|<span data-ttu-id="bee80-458">Name</span><span class="sxs-lookup"><span data-stu-id="bee80-458">Name</span></span>|<span data-ttu-id="bee80-459">Description</span><span class="sxs-lookup"><span data-stu-id="bee80-459">Description</span></span>|<span data-ttu-id="bee80-460">Required</span><span class="sxs-lookup"><span data-stu-id="bee80-460">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="bee80-461">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="bee80-461">xsl-transform</span></span>|<span data-ttu-id="bee80-462">Root element.</span><span class="sxs-lookup"><span data-stu-id="bee80-462">Root element.</span></span>|<span data-ttu-id="bee80-463">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-463">Yes</span></span>|  
|<span data-ttu-id="bee80-464">parameter</span><span class="sxs-lookup"><span data-stu-id="bee80-464">parameter</span></span>|<span data-ttu-id="bee80-465">Used to define variables used in the transform</span><span class="sxs-lookup"><span data-stu-id="bee80-465">Used to define variables used in the transform</span></span>|<span data-ttu-id="bee80-466">No</span><span class="sxs-lookup"><span data-stu-id="bee80-466">No</span></span>|  
|<span data-ttu-id="bee80-467">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="bee80-467">xsl:stylesheet</span></span>|<span data-ttu-id="bee80-468">Root stylesheet element.</span><span class="sxs-lookup"><span data-stu-id="bee80-468">Root stylesheet element.</span></span> <span data-ttu-id="bee80-469">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="bee80-469">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="bee80-470">Yes</span><span class="sxs-lookup"><span data-stu-id="bee80-470">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bee80-471">Usage</span><span class="sxs-lookup"><span data-stu-id="bee80-471">Usage</span></span>  
 <span data-ttu-id="bee80-472">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bee80-472">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bee80-473">**Policy sections:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="bee80-473">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="bee80-474">**Policy scopes:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="bee80-474">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bee80-475">Next steps</span><span class="sxs-lookup"><span data-stu-id="bee80-475">Next steps</span></span>
<span data-ttu-id="bee80-476">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bee80-476">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
