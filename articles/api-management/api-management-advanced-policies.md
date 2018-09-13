---
title: Azure API Management advanced policies | Microsoft Docs
description: Learn about the advanced policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 15fc4443e9d8a1140b580c1537c048f2d4dfca93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660763"
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="51d52-103">API Management advanced policies</span><span class="sxs-lookup"><span data-stu-id="51d52-103">API Management advanced policies</span></span>
<span data-ttu-id="51d52-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="51d52-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="51d52-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="51d52-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="AdvancedPolicies"></a> <span data-ttu-id="51d52-106">Advanced policies</span><span class="sxs-lookup"><span data-stu-id="51d52-106">Advanced policies</span></span>  
  
-   <span data-ttu-id="51d52-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="51d52-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="51d52-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span><span class="sxs-lookup"><span data-stu-id="51d52-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
-   <span data-ttu-id="51d52-109">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span><span class="sxs-lookup"><span data-stu-id="51d52-109">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="51d52-110">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-110">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="51d52-111">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span><span class="sxs-lookup"><span data-stu-id="51d52-111">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="51d52-112">Execution will repeat at the specified time intervals and up to the specified retry count.</span><span class="sxs-lookup"><span data-stu-id="51d52-112">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="51d52-113">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-113">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
-   <span data-ttu-id="51d52-114">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span><span class="sxs-lookup"><span data-stu-id="51d52-114">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="51d52-115">[Send request](#SendRequest) - Sends a request to the specified URL.</span><span class="sxs-lookup"><span data-stu-id="51d52-115">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  
  
-   <span data-ttu-id="51d52-116">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span><span class="sxs-lookup"><span data-stu-id="51d52-116">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  
  
-   <span data-ttu-id="51d52-117">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span><span class="sxs-lookup"><span data-stu-id="51d52-117">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="51d52-118">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span><span class="sxs-lookup"><span data-stu-id="51d52-118">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="51d52-119">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span><span class="sxs-lookup"><span data-stu-id="51d52-119">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="51d52-120">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span><span class="sxs-lookup"><span data-stu-id="51d52-120">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <a name="choose"></a> <span data-ttu-id="51d52-121">Control flow</span><span class="sxs-lookup"><span data-stu-id="51d52-121">Control flow</span></span>  
 <span data-ttu-id="51d52-122">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span><span class="sxs-lookup"><span data-stu-id="51d52-122">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <a name="ChoosePolicyStatement"></a> <span data-ttu-id="51d52-123">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-123">Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="51d52-124">The control flow policy must contain at least one `<when/>` element.</span><span class="sxs-lookup"><span data-stu-id="51d52-124">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="51d52-125">The `<otherwise/>` element is optional.</span><span class="sxs-lookup"><span data-stu-id="51d52-125">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="51d52-126">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-126">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="51d52-127">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span><span class="sxs-lookup"><span data-stu-id="51d52-127">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="51d52-128">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span><span class="sxs-lookup"><span data-stu-id="51d52-128">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="51d52-129">Examples</span><span class="sxs-lookup"><span data-stu-id="51d52-129">Examples</span></span>  
  
####  <a name="ChooseExample"></a> <span data-ttu-id="51d52-130">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-130">Example</span></span>  
 <span data-ttu-id="51d52-131">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span><span class="sxs-lookup"><span data-stu-id="51d52-131">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="51d52-132">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="51d52-132">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="51d52-133">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span><span class="sxs-lookup"><span data-stu-id="51d52-133">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="51d52-134">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="51d52-134">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="51d52-135">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-135">Example</span></span>  
 <span data-ttu-id="51d52-136">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="51d52-136">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="51d52-137">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span><span class="sxs-lookup"><span data-stu-id="51d52-137">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="51d52-138">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span><span class="sxs-lookup"><span data-stu-id="51d52-138">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="51d52-139">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-139">Elements</span></span>  
  
|<span data-ttu-id="51d52-140">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-140">Element</span></span>|<span data-ttu-id="51d52-141">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-141">Description</span></span>|<span data-ttu-id="51d52-142">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-142">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-143">choose</span><span class="sxs-lookup"><span data-stu-id="51d52-143">choose</span></span>|<span data-ttu-id="51d52-144">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-144">Root element.</span></span>|<span data-ttu-id="51d52-145">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-145">Yes</span></span>|  
|<span data-ttu-id="51d52-146">when</span><span class="sxs-lookup"><span data-stu-id="51d52-146">when</span></span>|<span data-ttu-id="51d52-147">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-147">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="51d52-148">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span><span class="sxs-lookup"><span data-stu-id="51d52-148">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="51d52-149">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span><span class="sxs-lookup"><span data-stu-id="51d52-149">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="51d52-150">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-150">Yes</span></span>|  
|<span data-ttu-id="51d52-151">otherwise</span><span class="sxs-lookup"><span data-stu-id="51d52-151">otherwise</span></span>|<span data-ttu-id="51d52-152">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span><span class="sxs-lookup"><span data-stu-id="51d52-152">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="51d52-153">No</span><span class="sxs-lookup"><span data-stu-id="51d52-153">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-154">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-154">Attributes</span></span>  
  
|<span data-ttu-id="51d52-155">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-155">Attribute</span></span>|<span data-ttu-id="51d52-156">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-156">Description</span></span>|<span data-ttu-id="51d52-157">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-157">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="51d52-158">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="51d52-158">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="51d52-159">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span><span class="sxs-lookup"><span data-stu-id="51d52-159">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="51d52-160">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-160">Yes</span></span>|  
  
###  <a name="ChooseUsage"></a> <span data-ttu-id="51d52-161">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-161">Usage</span></span>  
 <span data-ttu-id="51d52-162">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-162">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-163">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-163">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-164">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-164">**Policy scopes:** all scopes</span></span>  
  
##  <a name="ForwardRequest"></a> <span data-ttu-id="51d52-165">Forward request</span><span class="sxs-lookup"><span data-stu-id="51d52-165">Forward request</span></span>  
 <span data-ttu-id="51d52-166">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="51d52-166">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="51d52-167">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-167">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="51d52-168">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span><span class="sxs-lookup"><span data-stu-id="51d52-168">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-169">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-169">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="51d52-170">Examples</span><span class="sxs-lookup"><span data-stu-id="51d52-170">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="51d52-171">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-171">Example</span></span>  
 <span data-ttu-id="51d52-172">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="51d52-172">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="51d52-173">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-173">Example</span></span>  
 <span data-ttu-id="51d52-174">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span><span class="sxs-lookup"><span data-stu-id="51d52-174">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="51d52-175">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-175">Example</span></span>  
 <span data-ttu-id="51d52-176">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-176">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="51d52-177">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-177">Example</span></span>  
 <span data-ttu-id="51d52-178">This operation level policy does not forward requests to the backend service.</span><span class="sxs-lookup"><span data-stu-id="51d52-178">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-179">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-179">Elements</span></span>  
  
|<span data-ttu-id="51d52-180">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-180">Element</span></span>|<span data-ttu-id="51d52-181">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-181">Description</span></span>|<span data-ttu-id="51d52-182">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-182">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-183">forward-request</span><span class="sxs-lookup"><span data-stu-id="51d52-183">forward-request</span></span>|<span data-ttu-id="51d52-184">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-184">Root element.</span></span>|<span data-ttu-id="51d52-185">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-185">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-186">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-186">Attributes</span></span>  
  
|<span data-ttu-id="51d52-187">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-187">Attribute</span></span>|<span data-ttu-id="51d52-188">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-188">Description</span></span>|<span data-ttu-id="51d52-189">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-189">Required</span></span>|<span data-ttu-id="51d52-190">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-190">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-191">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="51d52-191">timeout="integer"</span></span>|<span data-ttu-id="51d52-192">The timeout interval in seconds before the call to the backend service fails.</span><span class="sxs-lookup"><span data-stu-id="51d52-192">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="51d52-193">No</span><span class="sxs-lookup"><span data-stu-id="51d52-193">No</span></span>|<span data-ttu-id="51d52-194">No timeout</span><span class="sxs-lookup"><span data-stu-id="51d52-194">No timeout</span></span>|  
|<span data-ttu-id="51d52-195">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="51d52-195">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="51d52-196">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-196">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="51d52-197">No</span><span class="sxs-lookup"><span data-stu-id="51d52-197">No</span></span>|<span data-ttu-id="51d52-198">false</span><span class="sxs-lookup"><span data-stu-id="51d52-198">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-199">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-199">Usage</span></span>  
 <span data-ttu-id="51d52-200">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-200">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-201">**Policy sections:** backend</span><span class="sxs-lookup"><span data-stu-id="51d52-201">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="51d52-202">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-202">**Policy scopes:** all scopes</span></span>  
  
##  <a name="log-to-eventhub"></a> <span data-ttu-id="51d52-203">Log to Event Hub</span><span class="sxs-lookup"><span data-stu-id="51d52-203">Log to Event Hub</span></span>  
 <span data-ttu-id="51d52-204">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span><span class="sxs-lookup"><span data-stu-id="51d52-204">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="51d52-205">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span><span class="sxs-lookup"><span data-stu-id="51d52-205">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="51d52-206">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="51d52-206">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-207">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-207">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-208">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-208">Example</span></span>  
 <span data-ttu-id="51d52-209">Any string can be used as the value to be logged in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="51d52-209">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="51d52-210">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="51d52-210">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-211">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-211">Elements</span></span>  
  
|<span data-ttu-id="51d52-212">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-212">Element</span></span>|<span data-ttu-id="51d52-213">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-213">Description</span></span>|<span data-ttu-id="51d52-214">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-214">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-215">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="51d52-215">log-to-eventhub</span></span>|<span data-ttu-id="51d52-216">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-216">Root element.</span></span> <span data-ttu-id="51d52-217">The value of this element is the string to log to your event hub.</span><span class="sxs-lookup"><span data-stu-id="51d52-217">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="51d52-218">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-218">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-219">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-219">Attributes</span></span>  
  
|<span data-ttu-id="51d52-220">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-220">Attribute</span></span>|<span data-ttu-id="51d52-221">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-221">Description</span></span>|<span data-ttu-id="51d52-222">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-222">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="51d52-223">logger-id</span><span class="sxs-lookup"><span data-stu-id="51d52-223">logger-id</span></span>|<span data-ttu-id="51d52-224">The id of the Logger registered with your API Management service.</span><span class="sxs-lookup"><span data-stu-id="51d52-224">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="51d52-225">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-225">Yes</span></span>|  
|<span data-ttu-id="51d52-226">partition-id</span><span class="sxs-lookup"><span data-stu-id="51d52-226">partition-id</span></span>|<span data-ttu-id="51d52-227">Specifies the index of the partition where messages are sent.</span><span class="sxs-lookup"><span data-stu-id="51d52-227">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="51d52-228">Optional.</span><span class="sxs-lookup"><span data-stu-id="51d52-228">Optional.</span></span> <span data-ttu-id="51d52-229">This attribute may not be used if `partition-key` is used.</span><span class="sxs-lookup"><span data-stu-id="51d52-229">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="51d52-230">partition-key</span><span class="sxs-lookup"><span data-stu-id="51d52-230">partition-key</span></span>|<span data-ttu-id="51d52-231">Specifies the value used for partition assignment when messages are sent.</span><span class="sxs-lookup"><span data-stu-id="51d52-231">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="51d52-232">Optional.</span><span class="sxs-lookup"><span data-stu-id="51d52-232">Optional.</span></span> <span data-ttu-id="51d52-233">This attribute may not be used if `partition-id` is used.</span><span class="sxs-lookup"><span data-stu-id="51d52-233">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-234">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-234">Usage</span></span>  
 <span data-ttu-id="51d52-235">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-235">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-236">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-236">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-237">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-237">**Policy scopes:** all scopes</span></span>  

##  <a name="mock-response"></a> <span data-ttu-id="51d52-238">Mock response</span><span class="sxs-lookup"><span data-stu-id="51d52-238">Mock response</span></span>  
<span data-ttu-id="51d52-239">The `mock-response`, as the name implies, is used to mock APIs and operations.</span><span class="sxs-lookup"><span data-stu-id="51d52-239">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="51d52-240">It aborts normal pipeline execution and returns a mocked response to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-240">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="51d52-241">The policy always tries to return responses of highest fidelity.</span><span class="sxs-lookup"><span data-stu-id="51d52-241">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="51d52-242">It prefers response content examples, whenever available.</span><span class="sxs-lookup"><span data-stu-id="51d52-242">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="51d52-243">It generates sample responses from schemas, when schemas are provided and examples are not.</span><span class="sxs-lookup"><span data-stu-id="51d52-243">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="51d52-244">If neither examples or schemas are found, responses with no content are returned.</span><span class="sxs-lookup"><span data-stu-id="51d52-244">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-245">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-245">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="51d52-246">Examples</span><span class="sxs-lookup"><span data-stu-id="51d52-246">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-247">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-247">Elements</span></span>  
  
|<span data-ttu-id="51d52-248">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-248">Element</span></span>|<span data-ttu-id="51d52-249">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-249">Description</span></span>|<span data-ttu-id="51d52-250">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-250">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-251">mock-response</span><span class="sxs-lookup"><span data-stu-id="51d52-251">mock-response</span></span>|<span data-ttu-id="51d52-252">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-252">Root element.</span></span>|<span data-ttu-id="51d52-253">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-253">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-254">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-254">Attributes</span></span>  
  
|<span data-ttu-id="51d52-255">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-255">Attribute</span></span>|<span data-ttu-id="51d52-256">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-256">Description</span></span>|<span data-ttu-id="51d52-257">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-257">Required</span></span>|<span data-ttu-id="51d52-258">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-258">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="51d52-259">status-code</span><span class="sxs-lookup"><span data-stu-id="51d52-259">status-code</span></span>|<span data-ttu-id="51d52-260">Specifies response status code and is used to select corresponding example or schema.</span><span class="sxs-lookup"><span data-stu-id="51d52-260">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="51d52-261">No</span><span class="sxs-lookup"><span data-stu-id="51d52-261">No</span></span>|<span data-ttu-id="51d52-262">200</span><span class="sxs-lookup"><span data-stu-id="51d52-262">200</span></span>|  
|<span data-ttu-id="51d52-263">content-type</span><span class="sxs-lookup"><span data-stu-id="51d52-263">content-type</span></span>|<span data-ttu-id="51d52-264">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span><span class="sxs-lookup"><span data-stu-id="51d52-264">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="51d52-265">No</span><span class="sxs-lookup"><span data-stu-id="51d52-265">No</span></span>|<span data-ttu-id="51d52-266">None</span><span class="sxs-lookup"><span data-stu-id="51d52-266">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-267">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-267">Usage</span></span>  
 <span data-ttu-id="51d52-268">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-268">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-269">**Policy sections:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-269">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="51d52-270">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-270">**Policy scopes:** all scopes</span></span>

##  <a name="Retry"></a> <span data-ttu-id="51d52-271">Retry</span><span class="sxs-lookup"><span data-stu-id="51d52-271">Retry</span></span>  
 <span data-ttu-id="51d52-272">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span><span class="sxs-lookup"><span data-stu-id="51d52-272">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-273">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-273">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-274">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-274">Example</span></span>  
 <span data-ttu-id="51d52-275">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span><span class="sxs-lookup"><span data-stu-id="51d52-275">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="51d52-276">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span><span class="sxs-lookup"><span data-stu-id="51d52-276">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-277">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-277">Elements</span></span>  
  
|<span data-ttu-id="51d52-278">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-278">Element</span></span>|<span data-ttu-id="51d52-279">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-279">Description</span></span>|<span data-ttu-id="51d52-280">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-280">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-281">retry</span><span class="sxs-lookup"><span data-stu-id="51d52-281">retry</span></span>|<span data-ttu-id="51d52-282">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-282">Root element.</span></span> <span data-ttu-id="51d52-283">May contain any other policies as its child elements.</span><span class="sxs-lookup"><span data-stu-id="51d52-283">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="51d52-284">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-284">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-285">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-285">Attributes</span></span>  
  
|<span data-ttu-id="51d52-286">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-286">Attribute</span></span>|<span data-ttu-id="51d52-287">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-287">Description</span></span>|<span data-ttu-id="51d52-288">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-288">Required</span></span>|<span data-ttu-id="51d52-289">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-289">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-290">condition</span><span class="sxs-lookup"><span data-stu-id="51d52-290">condition</span></span>|<span data-ttu-id="51d52-291">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span><span class="sxs-lookup"><span data-stu-id="51d52-291">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="51d52-292">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-292">Yes</span></span>|<span data-ttu-id="51d52-293">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-293">N/A</span></span>|  
|<span data-ttu-id="51d52-294">count</span><span class="sxs-lookup"><span data-stu-id="51d52-294">count</span></span>|<span data-ttu-id="51d52-295">A positive number specifying the maximum number of retries to attempt.</span><span class="sxs-lookup"><span data-stu-id="51d52-295">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="51d52-296">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-296">Yes</span></span>|<span data-ttu-id="51d52-297">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-297">N/A</span></span>|  
|<span data-ttu-id="51d52-298">interval</span><span class="sxs-lookup"><span data-stu-id="51d52-298">interval</span></span>|<span data-ttu-id="51d52-299">A positive number in seconds specifying the wait interval between the retry attempts.</span><span class="sxs-lookup"><span data-stu-id="51d52-299">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="51d52-300">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-300">Yes</span></span>|<span data-ttu-id="51d52-301">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-301">N/A</span></span>|  
|<span data-ttu-id="51d52-302">max-interval</span><span class="sxs-lookup"><span data-stu-id="51d52-302">max-interval</span></span>|<span data-ttu-id="51d52-303">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span><span class="sxs-lookup"><span data-stu-id="51d52-303">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="51d52-304">It is used to implement an exponential retry algorithm.</span><span class="sxs-lookup"><span data-stu-id="51d52-304">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="51d52-305">No</span><span class="sxs-lookup"><span data-stu-id="51d52-305">No</span></span>|<span data-ttu-id="51d52-306">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-306">N/A</span></span>|  
|<span data-ttu-id="51d52-307">delta</span><span class="sxs-lookup"><span data-stu-id="51d52-307">delta</span></span>|<span data-ttu-id="51d52-308">A positive number in seconds specifying the wait interval increment.</span><span class="sxs-lookup"><span data-stu-id="51d52-308">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="51d52-309">It is used to implement the linear and exponential retry algorithms.</span><span class="sxs-lookup"><span data-stu-id="51d52-309">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="51d52-310">No</span><span class="sxs-lookup"><span data-stu-id="51d52-310">No</span></span>|<span data-ttu-id="51d52-311">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-311">N/A</span></span>|  
|<span data-ttu-id="51d52-312">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="51d52-312">first-fast-retry</span></span>|<span data-ttu-id="51d52-313">If set to                                    `true` , the first retry attempt is performed immediately.</span><span class="sxs-lookup"><span data-stu-id="51d52-313">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="51d52-314">No</span><span class="sxs-lookup"><span data-stu-id="51d52-314">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="51d52-315">When only the `interval` is specified, **fixed** interval retries are performed.</span><span class="sxs-lookup"><span data-stu-id="51d52-315">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="51d52-316">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="51d52-316">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="51d52-317">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="51d52-317">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="51d52-318">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-318">Usage</span></span>  
 <span data-ttu-id="51d52-319">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="51d52-319">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="51d52-320">Note that child policy usage restrictions will be inherited by this policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-320">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="51d52-321">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-321">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-322">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-322">**Policy scopes:** all scopes</span></span>  
  
##  <a name="ReturnResponse"></a> <span data-ttu-id="51d52-323">Return response</span><span class="sxs-lookup"><span data-stu-id="51d52-323">Return response</span></span>  
 <span data-ttu-id="51d52-324">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-324">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="51d52-325">Default response is `200 OK` with no body.</span><span class="sxs-lookup"><span data-stu-id="51d52-325">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="51d52-326">Custom response can be specified via a context variable or policy statements.</span><span class="sxs-lookup"><span data-stu-id="51d52-326">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="51d52-327">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span><span class="sxs-lookup"><span data-stu-id="51d52-327">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-328">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-328">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-329">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-329">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-330">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-330">Elements</span></span>  
  
|<span data-ttu-id="51d52-331">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-331">Element</span></span>|<span data-ttu-id="51d52-332">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-332">Description</span></span>|<span data-ttu-id="51d52-333">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-333">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-334">return-response</span><span class="sxs-lookup"><span data-stu-id="51d52-334">return-response</span></span>|<span data-ttu-id="51d52-335">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-335">Root element.</span></span>|<span data-ttu-id="51d52-336">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-336">Yes</span></span>|  
|<span data-ttu-id="51d52-337">set-header</span><span class="sxs-lookup"><span data-stu-id="51d52-337">set-header</span></span>|<span data-ttu-id="51d52-338">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span><span class="sxs-lookup"><span data-stu-id="51d52-338">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="51d52-339">No</span><span class="sxs-lookup"><span data-stu-id="51d52-339">No</span></span>|  
|<span data-ttu-id="51d52-340">set-body</span><span class="sxs-lookup"><span data-stu-id="51d52-340">set-body</span></span>|<span data-ttu-id="51d52-341">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span><span class="sxs-lookup"><span data-stu-id="51d52-341">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="51d52-342">No</span><span class="sxs-lookup"><span data-stu-id="51d52-342">No</span></span>|  
|<span data-ttu-id="51d52-343">set-status</span><span class="sxs-lookup"><span data-stu-id="51d52-343">set-status</span></span>|<span data-ttu-id="51d52-344">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span><span class="sxs-lookup"><span data-stu-id="51d52-344">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="51d52-345">No</span><span class="sxs-lookup"><span data-stu-id="51d52-345">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-346">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-346">Attributes</span></span>  
  
|<span data-ttu-id="51d52-347">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-347">Attribute</span></span>|<span data-ttu-id="51d52-348">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-348">Description</span></span>|<span data-ttu-id="51d52-349">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-349">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="51d52-350">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="51d52-350">response-variable-name</span></span>|<span data-ttu-id="51d52-351">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span><span class="sxs-lookup"><span data-stu-id="51d52-351">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="51d52-352">Optional.</span><span class="sxs-lookup"><span data-stu-id="51d52-352">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-353">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-353">Usage</span></span>  
 <span data-ttu-id="51d52-354">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-354">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-355">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-355">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-356">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-356">**Policy scopes:** all scopes</span></span>  
  
##  <a name="SendOneWayRequest"></a> <span data-ttu-id="51d52-357">Send one way request</span><span class="sxs-lookup"><span data-stu-id="51d52-357">Send one way request</span></span>  
 <span data-ttu-id="51d52-358">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span><span class="sxs-lookup"><span data-stu-id="51d52-358">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-359">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-359">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-360">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-360">Example</span></span>  
 <span data-ttu-id="51d52-361">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span><span class="sxs-lookup"><span data-stu-id="51d52-361">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="51d52-362">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="51d52-362">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-363">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-363">Elements</span></span>  
  
|<span data-ttu-id="51d52-364">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-364">Element</span></span>|<span data-ttu-id="51d52-365">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-365">Description</span></span>|<span data-ttu-id="51d52-366">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-366">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-367">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="51d52-367">send-one-way-request</span></span>|<span data-ttu-id="51d52-368">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-368">Root element.</span></span>|<span data-ttu-id="51d52-369">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-369">Yes</span></span>|  
|<span data-ttu-id="51d52-370">url</span><span class="sxs-lookup"><span data-stu-id="51d52-370">url</span></span>|<span data-ttu-id="51d52-371">The URL of the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-371">The URL of the request.</span></span>|<span data-ttu-id="51d52-372">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="51d52-372">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="51d52-373">method</span><span class="sxs-lookup"><span data-stu-id="51d52-373">method</span></span>|<span data-ttu-id="51d52-374">The HTTP method for the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-374">The HTTP method for the request.</span></span>|<span data-ttu-id="51d52-375">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="51d52-375">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="51d52-376">header</span><span class="sxs-lookup"><span data-stu-id="51d52-376">header</span></span>|<span data-ttu-id="51d52-377">Request header.</span><span class="sxs-lookup"><span data-stu-id="51d52-377">Request header.</span></span> <span data-ttu-id="51d52-378">Use multiple header elements for multiple request headers.</span><span class="sxs-lookup"><span data-stu-id="51d52-378">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="51d52-379">No</span><span class="sxs-lookup"><span data-stu-id="51d52-379">No</span></span>|  
|<span data-ttu-id="51d52-380">body</span><span class="sxs-lookup"><span data-stu-id="51d52-380">body</span></span>|<span data-ttu-id="51d52-381">The request body.</span><span class="sxs-lookup"><span data-stu-id="51d52-381">The request body.</span></span>|<span data-ttu-id="51d52-382">No</span><span class="sxs-lookup"><span data-stu-id="51d52-382">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-383">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-383">Attributes</span></span>  
  
|<span data-ttu-id="51d52-384">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-384">Attribute</span></span>|<span data-ttu-id="51d52-385">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-385">Description</span></span>|<span data-ttu-id="51d52-386">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-386">Required</span></span>|<span data-ttu-id="51d52-387">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-387">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-388">mode="string"</span><span class="sxs-lookup"><span data-stu-id="51d52-388">mode="string"</span></span>|<span data-ttu-id="51d52-389">Determines whether this is a new request or a copy of the current request.</span><span class="sxs-lookup"><span data-stu-id="51d52-389">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="51d52-390">In outbound mode, mode=copy does not initialize the request body.</span><span class="sxs-lookup"><span data-stu-id="51d52-390">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="51d52-391">No</span><span class="sxs-lookup"><span data-stu-id="51d52-391">No</span></span>|<span data-ttu-id="51d52-392">New</span><span class="sxs-lookup"><span data-stu-id="51d52-392">New</span></span>|  
|<span data-ttu-id="51d52-393">name</span><span class="sxs-lookup"><span data-stu-id="51d52-393">name</span></span>|<span data-ttu-id="51d52-394">Specifies the name of the header to be set.</span><span class="sxs-lookup"><span data-stu-id="51d52-394">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="51d52-395">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-395">Yes</span></span>|<span data-ttu-id="51d52-396">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-396">N/A</span></span>|  
|<span data-ttu-id="51d52-397">exists-action</span><span class="sxs-lookup"><span data-stu-id="51d52-397">exists-action</span></span>|<span data-ttu-id="51d52-398">Specifies what action to take when the header is already specified.</span><span class="sxs-lookup"><span data-stu-id="51d52-398">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="51d52-399">This attribute must have one of the following values.</span><span class="sxs-lookup"><span data-stu-id="51d52-399">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="51d52-400">-   override - replaces the value of the existing header.</span><span class="sxs-lookup"><span data-stu-id="51d52-400">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="51d52-401">-   skip - does not replace the existing header value.</span><span class="sxs-lookup"><span data-stu-id="51d52-401">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="51d52-402">-   append - appends the value to the existing header value.</span><span class="sxs-lookup"><span data-stu-id="51d52-402">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="51d52-403">-   delete - removes the header from the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-403">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="51d52-404">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span><span class="sxs-lookup"><span data-stu-id="51d52-404">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="51d52-405">No</span><span class="sxs-lookup"><span data-stu-id="51d52-405">No</span></span>|<span data-ttu-id="51d52-406">override</span><span class="sxs-lookup"><span data-stu-id="51d52-406">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-407">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-407">Usage</span></span>  
 <span data-ttu-id="51d52-408">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-408">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-409">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-409">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-410">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-410">**Policy scopes:** all scopes</span></span>  
  
##  <a name="SendRequest"></a> <span data-ttu-id="51d52-411">Send request</span><span class="sxs-lookup"><span data-stu-id="51d52-411">Send request</span></span>  
 <span data-ttu-id="51d52-412">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span><span class="sxs-lookup"><span data-stu-id="51d52-412">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-413">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-413">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-414">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-414">Example</span></span>  
 <span data-ttu-id="51d52-415">This example shows one way to verify a reference token with an authorization server.</span><span class="sxs-lookup"><span data-stu-id="51d52-415">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="51d52-416">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="51d52-416">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-417">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-417">Elements</span></span>  
  
|<span data-ttu-id="51d52-418">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-418">Element</span></span>|<span data-ttu-id="51d52-419">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-419">Description</span></span>|<span data-ttu-id="51d52-420">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-420">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-421">send-request</span><span class="sxs-lookup"><span data-stu-id="51d52-421">send-request</span></span>|<span data-ttu-id="51d52-422">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-422">Root element.</span></span>|<span data-ttu-id="51d52-423">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-423">Yes</span></span>|  
|<span data-ttu-id="51d52-424">url</span><span class="sxs-lookup"><span data-stu-id="51d52-424">url</span></span>|<span data-ttu-id="51d52-425">The URL of the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-425">The URL of the request.</span></span>|<span data-ttu-id="51d52-426">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="51d52-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="51d52-427">method</span><span class="sxs-lookup"><span data-stu-id="51d52-427">method</span></span>|<span data-ttu-id="51d52-428">The HTTP method for the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-428">The HTTP method for the request.</span></span>|<span data-ttu-id="51d52-429">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="51d52-429">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="51d52-430">header</span><span class="sxs-lookup"><span data-stu-id="51d52-430">header</span></span>|<span data-ttu-id="51d52-431">Request header.</span><span class="sxs-lookup"><span data-stu-id="51d52-431">Request header.</span></span> <span data-ttu-id="51d52-432">Use multiple header elements for multiple request headers.</span><span class="sxs-lookup"><span data-stu-id="51d52-432">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="51d52-433">No</span><span class="sxs-lookup"><span data-stu-id="51d52-433">No</span></span>|  
|<span data-ttu-id="51d52-434">body</span><span class="sxs-lookup"><span data-stu-id="51d52-434">body</span></span>|<span data-ttu-id="51d52-435">The request body.</span><span class="sxs-lookup"><span data-stu-id="51d52-435">The request body.</span></span>|<span data-ttu-id="51d52-436">No</span><span class="sxs-lookup"><span data-stu-id="51d52-436">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-437">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-437">Attributes</span></span>  
  
|<span data-ttu-id="51d52-438">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-438">Attribute</span></span>|<span data-ttu-id="51d52-439">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-439">Description</span></span>|<span data-ttu-id="51d52-440">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-440">Required</span></span>|<span data-ttu-id="51d52-441">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-441">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-442">mode="string"</span><span class="sxs-lookup"><span data-stu-id="51d52-442">mode="string"</span></span>|<span data-ttu-id="51d52-443">Determines whether this is a new request or a copy of the current request.</span><span class="sxs-lookup"><span data-stu-id="51d52-443">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="51d52-444">In outbound mode, mode=copy does not initialize the request body.</span><span class="sxs-lookup"><span data-stu-id="51d52-444">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="51d52-445">No</span><span class="sxs-lookup"><span data-stu-id="51d52-445">No</span></span>|<span data-ttu-id="51d52-446">New</span><span class="sxs-lookup"><span data-stu-id="51d52-446">New</span></span>|  
|<span data-ttu-id="51d52-447">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="51d52-447">response-variable-name="string"</span></span>|<span data-ttu-id="51d52-448">If not present, `context.Response` is used.</span><span class="sxs-lookup"><span data-stu-id="51d52-448">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="51d52-449">No</span><span class="sxs-lookup"><span data-stu-id="51d52-449">No</span></span>|<span data-ttu-id="51d52-450">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-450">N/A</span></span>|  
|<span data-ttu-id="51d52-451">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="51d52-451">timeout="integer"</span></span>|<span data-ttu-id="51d52-452">The timeout interval in seconds before the call to the URL fails.</span><span class="sxs-lookup"><span data-stu-id="51d52-452">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="51d52-453">No</span><span class="sxs-lookup"><span data-stu-id="51d52-453">No</span></span>|<span data-ttu-id="51d52-454">60</span><span class="sxs-lookup"><span data-stu-id="51d52-454">60</span></span>|  
|<span data-ttu-id="51d52-455">ignore-error</span><span class="sxs-lookup"><span data-stu-id="51d52-455">ignore-error</span></span>|<span data-ttu-id="51d52-456">If true and the request results in an error:</span><span class="sxs-lookup"><span data-stu-id="51d52-456">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="51d52-457">-   If response-variable-name was specified it will contain a null value.</span><span class="sxs-lookup"><span data-stu-id="51d52-457">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="51d52-458">-   If response-variable-name was not specified, context.Request will not be updated.</span><span class="sxs-lookup"><span data-stu-id="51d52-458">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="51d52-459">No</span><span class="sxs-lookup"><span data-stu-id="51d52-459">No</span></span>|<span data-ttu-id="51d52-460">false</span><span class="sxs-lookup"><span data-stu-id="51d52-460">false</span></span>|  
|<span data-ttu-id="51d52-461">name</span><span class="sxs-lookup"><span data-stu-id="51d52-461">name</span></span>|<span data-ttu-id="51d52-462">Specifies the name of the header to be set.</span><span class="sxs-lookup"><span data-stu-id="51d52-462">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="51d52-463">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-463">Yes</span></span>|<span data-ttu-id="51d52-464">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-464">N/A</span></span>|  
|<span data-ttu-id="51d52-465">exists-action</span><span class="sxs-lookup"><span data-stu-id="51d52-465">exists-action</span></span>|<span data-ttu-id="51d52-466">Specifies what action to take when the header is already specified.</span><span class="sxs-lookup"><span data-stu-id="51d52-466">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="51d52-467">This attribute must have one of the following values.</span><span class="sxs-lookup"><span data-stu-id="51d52-467">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="51d52-468">-   override - replaces the value of the existing header.</span><span class="sxs-lookup"><span data-stu-id="51d52-468">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="51d52-469">-   skip - does not replace the existing header value.</span><span class="sxs-lookup"><span data-stu-id="51d52-469">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="51d52-470">-   append - appends the value to the existing header value.</span><span class="sxs-lookup"><span data-stu-id="51d52-470">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="51d52-471">-   delete - removes the header from the request.</span><span class="sxs-lookup"><span data-stu-id="51d52-471">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="51d52-472">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span><span class="sxs-lookup"><span data-stu-id="51d52-472">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="51d52-473">No</span><span class="sxs-lookup"><span data-stu-id="51d52-473">No</span></span>|<span data-ttu-id="51d52-474">override</span><span class="sxs-lookup"><span data-stu-id="51d52-474">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-475">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-475">Usage</span></span>  
 <span data-ttu-id="51d52-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-477">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-477">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-478">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-478">**Policy scopes:** all scopes</span></span>  
  
##  <a name="set-variable"></a> <span data-ttu-id="51d52-479">Set variable</span><span class="sxs-lookup"><span data-stu-id="51d52-479">Set variable</span></span>  
 <span data-ttu-id="51d52-480">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span><span class="sxs-lookup"><span data-stu-id="51d52-480">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="51d52-481">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span><span class="sxs-lookup"><span data-stu-id="51d52-481">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <a name="set-variablePolicyStatement"></a> <span data-ttu-id="51d52-482">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-482">Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> <span data-ttu-id="51d52-483">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-483">Example</span></span>  
 <span data-ttu-id="51d52-484">The following example demonstrates a set variable policy in the inbound section.</span><span class="sxs-lookup"><span data-stu-id="51d52-484">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="51d52-485">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="51d52-485">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-486">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-486">Elements</span></span>  
  
|<span data-ttu-id="51d52-487">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-487">Element</span></span>|<span data-ttu-id="51d52-488">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-488">Description</span></span>|<span data-ttu-id="51d52-489">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-489">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-490">set-variable</span><span class="sxs-lookup"><span data-stu-id="51d52-490">set-variable</span></span>|<span data-ttu-id="51d52-491">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-491">Root element.</span></span>|<span data-ttu-id="51d52-492">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-492">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-493">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-493">Attributes</span></span>  
  
|<span data-ttu-id="51d52-494">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-494">Attribute</span></span>|<span data-ttu-id="51d52-495">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-495">Description</span></span>|<span data-ttu-id="51d52-496">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-496">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="51d52-497">name</span><span class="sxs-lookup"><span data-stu-id="51d52-497">name</span></span>|<span data-ttu-id="51d52-498">The name of the variable.</span><span class="sxs-lookup"><span data-stu-id="51d52-498">The name of the variable.</span></span>|<span data-ttu-id="51d52-499">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-499">Yes</span></span>|  
|<span data-ttu-id="51d52-500">value</span><span class="sxs-lookup"><span data-stu-id="51d52-500">value</span></span>|<span data-ttu-id="51d52-501">The value of the variable.</span><span class="sxs-lookup"><span data-stu-id="51d52-501">The value of the variable.</span></span> <span data-ttu-id="51d52-502">This can be an expression or a literal value.</span><span class="sxs-lookup"><span data-stu-id="51d52-502">This can be an expression or a literal value.</span></span>|<span data-ttu-id="51d52-503">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-503">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-504">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-504">Usage</span></span>  
 <span data-ttu-id="51d52-505">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-505">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-506">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-506">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-507">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-507">**Policy scopes:** all scopes</span></span>  
  
###  <a name="set-variableAllowedTypes"></a> <span data-ttu-id="51d52-508">Allowed types</span><span class="sxs-lookup"><span data-stu-id="51d52-508">Allowed types</span></span>  
 <span data-ttu-id="51d52-509">Expressions used in the `set-variable` policy must return one of the following basic types.</span><span class="sxs-lookup"><span data-stu-id="51d52-509">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="51d52-510">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="51d52-510">System.Boolean</span></span>  
  
-   <span data-ttu-id="51d52-511">System.SByte</span><span class="sxs-lookup"><span data-stu-id="51d52-511">System.SByte</span></span>  
  
-   <span data-ttu-id="51d52-512">System.Byte</span><span class="sxs-lookup"><span data-stu-id="51d52-512">System.Byte</span></span>  
  
-   <span data-ttu-id="51d52-513">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="51d52-513">System.UInt16</span></span>  
  
-   <span data-ttu-id="51d52-514">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="51d52-514">System.UInt32</span></span>  
  
-   <span data-ttu-id="51d52-515">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="51d52-515">System.UInt64</span></span>  
  
-   <span data-ttu-id="51d52-516">System.Int16</span><span class="sxs-lookup"><span data-stu-id="51d52-516">System.Int16</span></span>  
  
-   <span data-ttu-id="51d52-517">System.Int32</span><span class="sxs-lookup"><span data-stu-id="51d52-517">System.Int32</span></span>  
  
-   <span data-ttu-id="51d52-518">System.Int64</span><span class="sxs-lookup"><span data-stu-id="51d52-518">System.Int64</span></span>  
  
-   <span data-ttu-id="51d52-519">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="51d52-519">System.Decimal</span></span>  
  
-   <span data-ttu-id="51d52-520">System.Single</span><span class="sxs-lookup"><span data-stu-id="51d52-520">System.Single</span></span>  
  
-   <span data-ttu-id="51d52-521">System.Double</span><span class="sxs-lookup"><span data-stu-id="51d52-521">System.Double</span></span>  
  
-   <span data-ttu-id="51d52-522">System.Guid</span><span class="sxs-lookup"><span data-stu-id="51d52-522">System.Guid</span></span>  
  
-   <span data-ttu-id="51d52-523">System.String</span><span class="sxs-lookup"><span data-stu-id="51d52-523">System.String</span></span>  
  
-   <span data-ttu-id="51d52-524">System.Char</span><span class="sxs-lookup"><span data-stu-id="51d52-524">System.Char</span></span>  
  
-   <span data-ttu-id="51d52-525">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="51d52-525">System.DateTime</span></span>  
  
-   <span data-ttu-id="51d52-526">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="51d52-526">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="51d52-527">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="51d52-527">System.Byte?</span></span>  
  
-   <span data-ttu-id="51d52-528">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="51d52-528">System.UInt16?</span></span>  
  
-   <span data-ttu-id="51d52-529">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="51d52-529">System.UInt32?</span></span>  
  
-   <span data-ttu-id="51d52-530">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="51d52-530">System.UInt64?</span></span>  
  
-   <span data-ttu-id="51d52-531">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="51d52-531">System.Int16?</span></span>  
  
-   <span data-ttu-id="51d52-532">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="51d52-532">System.Int32?</span></span>  
  
-   <span data-ttu-id="51d52-533">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="51d52-533">System.Int64?</span></span>  
  
-   <span data-ttu-id="51d52-534">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="51d52-534">System.Decimal?</span></span>  
  
-   <span data-ttu-id="51d52-535">System.Single?</span><span class="sxs-lookup"><span data-stu-id="51d52-535">System.Single?</span></span>  
  
-   <span data-ttu-id="51d52-536">System.Double?</span><span class="sxs-lookup"><span data-stu-id="51d52-536">System.Double?</span></span>  
  
-   <span data-ttu-id="51d52-537">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="51d52-537">System.Guid?</span></span>  
  
-   <span data-ttu-id="51d52-538">System.String?</span><span class="sxs-lookup"><span data-stu-id="51d52-538">System.String?</span></span>  
  
-   <span data-ttu-id="51d52-539">System.Char?</span><span class="sxs-lookup"><span data-stu-id="51d52-539">System.Char?</span></span>  
  
-   <span data-ttu-id="51d52-540">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="51d52-540">System.DateTime?</span></span>  
  
##  <a name="SetRequestMethod"></a> <span data-ttu-id="51d52-541">Set request method</span><span class="sxs-lookup"><span data-stu-id="51d52-541">Set request method</span></span>  
 <span data-ttu-id="51d52-542">The `set-method` policy allows you to change the HTTP request method for a request.</span><span class="sxs-lookup"><span data-stu-id="51d52-542">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-543">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-543">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-544">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-544">Example</span></span>  
 <span data-ttu-id="51d52-545">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span><span class="sxs-lookup"><span data-stu-id="51d52-545">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="51d52-546">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="51d52-546">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-547">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-547">Elements</span></span>  
  
|<span data-ttu-id="51d52-548">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-548">Element</span></span>|<span data-ttu-id="51d52-549">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-549">Description</span></span>|<span data-ttu-id="51d52-550">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-550">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-551">set-method</span><span class="sxs-lookup"><span data-stu-id="51d52-551">set-method</span></span>|<span data-ttu-id="51d52-552">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-552">Root element.</span></span> <span data-ttu-id="51d52-553">The value of the element specifies the HTTP method.</span><span class="sxs-lookup"><span data-stu-id="51d52-553">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="51d52-554">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-554">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-555">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-555">Usage</span></span>  
 <span data-ttu-id="51d52-556">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-556">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-557">**Policy sections:** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-557">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="51d52-558">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-558">**Policy scopes:** all scopes</span></span>  
  
##  <a name="SetStatus"></a> <span data-ttu-id="51d52-559">Set status code</span><span class="sxs-lookup"><span data-stu-id="51d52-559">Set status code</span></span>  
 <span data-ttu-id="51d52-560">The `set-status` policy sets the HTTP status code to the specified value.</span><span class="sxs-lookup"><span data-stu-id="51d52-560">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-561">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-561">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-562">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-562">Example</span></span>  
 <span data-ttu-id="51d52-563">This example shows how to return a 401 response if the authorization token is invalid.</span><span class="sxs-lookup"><span data-stu-id="51d52-563">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="51d52-564">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="51d52-564">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-565">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-565">Elements</span></span>  
  
|<span data-ttu-id="51d52-566">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-566">Element</span></span>|<span data-ttu-id="51d52-567">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-567">Description</span></span>|<span data-ttu-id="51d52-568">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-568">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-569">set-status</span><span class="sxs-lookup"><span data-stu-id="51d52-569">set-status</span></span>|<span data-ttu-id="51d52-570">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-570">Root element.</span></span>|<span data-ttu-id="51d52-571">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-571">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-572">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-572">Attributes</span></span>  
  
|<span data-ttu-id="51d52-573">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-573">Attribute</span></span>|<span data-ttu-id="51d52-574">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-574">Description</span></span>|<span data-ttu-id="51d52-575">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-575">Required</span></span>|<span data-ttu-id="51d52-576">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-576">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-577">code="integer"</span><span class="sxs-lookup"><span data-stu-id="51d52-577">code="integer"</span></span>|<span data-ttu-id="51d52-578">The HTTP status code to return.</span><span class="sxs-lookup"><span data-stu-id="51d52-578">The HTTP status code to return.</span></span>|<span data-ttu-id="51d52-579">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-579">Yes</span></span>|<span data-ttu-id="51d52-580">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-580">N/A</span></span>|  
|<span data-ttu-id="51d52-581">reason="string"</span><span class="sxs-lookup"><span data-stu-id="51d52-581">reason="string"</span></span>|<span data-ttu-id="51d52-582">A description of the reason for returning the status code.</span><span class="sxs-lookup"><span data-stu-id="51d52-582">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="51d52-583">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-583">Yes</span></span>|<span data-ttu-id="51d52-584">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-584">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-585">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-585">Usage</span></span>  
 <span data-ttu-id="51d52-586">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-586">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-587">**Policy sections:** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-587">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-588">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-588">**Policy scopes:** all scopes</span></span>  
  
##  <a name="Trace"></a> <span data-ttu-id="51d52-589">Trace</span><span class="sxs-lookup"><span data-stu-id="51d52-589">Trace</span></span>  
 <span data-ttu-id="51d52-590">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span><span class="sxs-lookup"><span data-stu-id="51d52-590">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="51d52-591">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span><span class="sxs-lookup"><span data-stu-id="51d52-591">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-592">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-592">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-593">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-593">Elements</span></span>  
  
|<span data-ttu-id="51d52-594">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-594">Element</span></span>|<span data-ttu-id="51d52-595">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-595">Description</span></span>|<span data-ttu-id="51d52-596">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-596">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-597">trace</span><span class="sxs-lookup"><span data-stu-id="51d52-597">trace</span></span>|<span data-ttu-id="51d52-598">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-598">Root element.</span></span>|<span data-ttu-id="51d52-599">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-599">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-600">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-600">Attributes</span></span>  
  
|<span data-ttu-id="51d52-601">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-601">Attribute</span></span>|<span data-ttu-id="51d52-602">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-602">Description</span></span>|<span data-ttu-id="51d52-603">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-603">Required</span></span>|<span data-ttu-id="51d52-604">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-604">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-605">source</span><span class="sxs-lookup"><span data-stu-id="51d52-605">source</span></span>|<span data-ttu-id="51d52-606">String literal meaningful to the trace viewer and specifying the source of the message.</span><span class="sxs-lookup"><span data-stu-id="51d52-606">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="51d52-607">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-607">Yes</span></span>|<span data-ttu-id="51d52-608">N/A</span><span class="sxs-lookup"><span data-stu-id="51d52-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-609">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-609">Usage</span></span>  
 <span data-ttu-id="51d52-610">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="51d52-610">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="51d52-611">**Policy sections:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="51d52-611">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="51d52-612">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-612">**Policy scopes:** all scopes</span></span>  
  
##  <a name="Wait"></a> <span data-ttu-id="51d52-613">Wait</span><span class="sxs-lookup"><span data-stu-id="51d52-613">Wait</span></span>  
 <span data-ttu-id="51d52-614">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span><span class="sxs-lookup"><span data-stu-id="51d52-614">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="51d52-615">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span><span class="sxs-lookup"><span data-stu-id="51d52-615">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="51d52-616">Policy statement</span><span class="sxs-lookup"><span data-stu-id="51d52-616">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="51d52-617">Example</span><span class="sxs-lookup"><span data-stu-id="51d52-617">Example</span></span>  
 <span data-ttu-id="51d52-618">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-618">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="51d52-619">Each of these `choose` policies executes in parallel.</span><span class="sxs-lookup"><span data-stu-id="51d52-619">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="51d52-620">Each `choose` policy attempts to retrieve a cached value.</span><span class="sxs-lookup"><span data-stu-id="51d52-620">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="51d52-621">If there is a cache miss, a backend service is called to provide the value.</span><span class="sxs-lookup"><span data-stu-id="51d52-621">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="51d52-622">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span><span class="sxs-lookup"><span data-stu-id="51d52-622">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="51d52-623">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span><span class="sxs-lookup"><span data-stu-id="51d52-623">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="51d52-624">Elements</span><span class="sxs-lookup"><span data-stu-id="51d52-624">Elements</span></span>  
  
|<span data-ttu-id="51d52-625">Element</span><span class="sxs-lookup"><span data-stu-id="51d52-625">Element</span></span>|<span data-ttu-id="51d52-626">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-626">Description</span></span>|<span data-ttu-id="51d52-627">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-627">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="51d52-628">wait</span><span class="sxs-lookup"><span data-stu-id="51d52-628">wait</span></span>|<span data-ttu-id="51d52-629">Root element.</span><span class="sxs-lookup"><span data-stu-id="51d52-629">Root element.</span></span> <span data-ttu-id="51d52-630">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span><span class="sxs-lookup"><span data-stu-id="51d52-630">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="51d52-631">Yes</span><span class="sxs-lookup"><span data-stu-id="51d52-631">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="51d52-632">Attributes</span><span class="sxs-lookup"><span data-stu-id="51d52-632">Attributes</span></span>  
  
|<span data-ttu-id="51d52-633">Attribute</span><span class="sxs-lookup"><span data-stu-id="51d52-633">Attribute</span></span>|<span data-ttu-id="51d52-634">Description</span><span class="sxs-lookup"><span data-stu-id="51d52-634">Description</span></span>|<span data-ttu-id="51d52-635">Required</span><span class="sxs-lookup"><span data-stu-id="51d52-635">Required</span></span>|<span data-ttu-id="51d52-636">Default</span><span class="sxs-lookup"><span data-stu-id="51d52-636">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="51d52-637">for</span><span class="sxs-lookup"><span data-stu-id="51d52-637">for</span></span>|<span data-ttu-id="51d52-638">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span><span class="sxs-lookup"><span data-stu-id="51d52-638">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="51d52-639">Allowed values are:</span><span class="sxs-lookup"><span data-stu-id="51d52-639">Allowed values are:</span></span><br /><br /> <span data-ttu-id="51d52-640">-   `all` - wait for all immediate child policies to complete</span><span class="sxs-lookup"><span data-stu-id="51d52-640">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="51d52-641">-   any - wait for any immediate child policy to complete.</span><span class="sxs-lookup"><span data-stu-id="51d52-641">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="51d52-642">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span><span class="sxs-lookup"><span data-stu-id="51d52-642">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="51d52-643">No</span><span class="sxs-lookup"><span data-stu-id="51d52-643">No</span></span>|<span data-ttu-id="51d52-644">all</span><span class="sxs-lookup"><span data-stu-id="51d52-644">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="51d52-645">Usage</span><span class="sxs-lookup"><span data-stu-id="51d52-645">Usage</span></span>  
 <span data-ttu-id="51d52-646">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="51d52-646">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="51d52-647">**Policy sections:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="51d52-647">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="51d52-648">**Policy scopes:** all scopes</span><span class="sxs-lookup"><span data-stu-id="51d52-648">**Policy scopes:** all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="51d52-649">Next steps</span><span class="sxs-lookup"><span data-stu-id="51d52-649">Next steps</span></span>
<span data-ttu-id="51d52-650">For more information working with policies, see:</span><span class="sxs-lookup"><span data-stu-id="51d52-650">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="51d52-651">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="51d52-651">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="51d52-652">Policy expressions</span><span class="sxs-lookup"><span data-stu-id="51d52-652">Policy expressions</span></span>](api-management-policy-expressions.md)
