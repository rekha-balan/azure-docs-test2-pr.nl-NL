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
# <a name="api-management-caching-policies"></a>API Management caching policies
This topic provides a reference for the following API Management policies. For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Caching policies  
  
-   Response caching policies  
  
    -   [Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.  
  
    -   [Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.  
  
-   Value caching policies  
  
    -   [Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.  
  
    -   [Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.  
  
    -   [Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.  
  
##  <a name="GetFromCache"></a> Get from cache  
 Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available. This policy can be applied in cases where response content remains static over a period of time. Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.  
  
> [!NOTE]
>  This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.  
  
### <a name="policy-statement"></a>Policy statement  
  
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
  
### <a name="examples"></a>Examples  
  
#### <a name="example"></a>Example  
  
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
  
#### <a name="example-using-policy-expressions"></a>Example using policy expressions  
 This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive. For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.  
  
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
  
 For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|cache-lookup|Root element.|Yes|  
|vary-by-header|Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.|No|  
|vary-by-query-parameter|Start caching responses per value of specified query parameters. Enter a single or multiple parameters. Use semicolon as a separator. If none are specified, all query parameters are used.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|When set to `true`, allows caching of requests that contain an Authorization header.|No|false|  
|downstream-caching-type|This attribute must be set to one of the following values.<br /><br /> -   none - downstream caching is not allowed.<br />-   private - downstream private caching is allowed.<br />-   public - private and shared downstream caching is allowed.|No|none|  
|must-revalidate|When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.|No|true|  
|vary-by-developer|Set to `true` to cache responses per developer key.|No|false|  
|vary-by-developer-groups|Set to `true` to cache responses per user role.|No|false|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** API, operation, product  
  
##  <a name="StoreToCache"></a> Store to cache  
 The `cache-store` policy caches responses according to the specified cache settings. This policy can be applied in cases where response content remains static over a period of time. Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.  
  
> [!NOTE]
>  This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.  
  
### <a name="policy-statement"></a>Policy statement  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Examples  
  
#### <a name="example"></a>Example  
  
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
  
#### <a name="example-using-policy-expressions"></a>Example using policy expressions  
 This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive. For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.  
  
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
  
 For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|cache-store|Root element.|Yes|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Time-to-live of the cached entries, specified in seconds.|Yes|N/A|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** outbound  
  
-   **Policy scopes:** API, operation, product  
  
##  <a name="GetFromCacheByKey"></a> Get value from cache  
 Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value. The key can have an arbitrary string value and is typically provided using a policy expression.  
  
> [!NOTE]
>  This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.  
  
### <a name="policy-statement"></a>Policy statement  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Example  
 For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|cache-lookup-value|Root element.|Yes|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|default-value|A value that will be assigned to the variable if the cache key lookup resulted in a miss. If this attribute is not specified, `null` is assigned.|No|`null`|  
|key|Cache key value to use in the lookup.|Yes|N/A|  
|variable-name|Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful. If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.|Yes|N/A|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, backend, on-error  
  
-   **Policy scopes:** global, API, operation, product  
  
##  <a name="StoreToCacheByKey"></a> Store value in cache  
 The `cache-store-value` performs cache storage by key. The key can have an arbitrary string value and is typically provided using a policy expression.  
  
> [!NOTE]
>  This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.  
  
### <a name="policy-statement"></a>Policy statement  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a>Example  
 For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|cache-store-value|Root element.|Yes|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Value will be cached for the provided duration value, specified in seconds.|Yes|N/A|  
|key|Cache key the value will be stored under.|Yes|N/A|  
|value|The value to be cached.|Yes|N/A|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound, backend, on-error  
  
-   **Policy scopes:** global, API, operation, product  
  
###  <a name="RemoveCacheByKey"></a> Remove value from cache  
 The             `cache-remove-value` deletes a cached item identified by its key. The key can have an arbitrary string value and is typically provided using a policy expression.  
  
#### <a name="policy-statement"></a>Policy statement  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Example  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|cache-remove-value|Root element.|Yes|  
  
#### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|key|The key of the previously cached value to be removed from the cache.|Yes|N/A|  
  
#### <a name="usage"></a>Usage  
 This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Policy sections:** inbound, outbound, backend, on-error  
  
-   **Policy scopes:** global, API, operation, product  
  

## <a name="next-steps"></a>Next steps
For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).  