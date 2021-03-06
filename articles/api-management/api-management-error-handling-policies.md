---
title: Error handling in Azure API Management policies | Microsoft Docs
description: Learn how to respond to error conditions that may occur during the processing of requests in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2fb403cc7454227083dc34d41a6f5f3a5876b1e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554804"
---
# <a name="error-handling-in-api-management-policies"></a>Error handling in API Management policies
Azure API Management allows publishers to respond to error conditions that may occur during the processing of requests to the proxy by providing a `ProxyError` object. The `ProxyError` object is accessed through the [context.LastError](api-management-policy-expressions.md#ContextVariables) property and can be used by policies in the `on-error` policy section. This topic provides a reference for the error handling capabilities in Azure API Management.  
  
## <a name="error-handling-in-api-management"></a>Error handling in API Management  
 Policies in Azure API Management are divided into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following example.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements to be applied to the request go here -->  
  </inbound>  
  <backend>  
    <!-- statements to be applied before the request is   
         forwarded to the backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements to be applied to the response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements to be applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 During the processing of a request, built-in steps are executed along with any policies that are in scope for the request. If an error occurs, processing immediately jumps to the `on-error` policy section. The `on-error` policy section can be used at any scope, and API publishers can configure custom behavior such as logging the error to event hubs or creating a new response to return to the caller.  
  
> [!NOTE]
>  The `on-error` section is not present in policies by default. To add the `on-error` section to a policy, browse to the desired policy in the policy editor and add it. For more information about configuring policies, see [Policies in API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  If there is no `on-error` section, callers will receive 400 or 500 HTTP response messages if an error condition occurs.  
  
### <a name="policies-allowed-in-on-error"></a>Policies allowed in on-error  
 The following policies can be used in the `on-error` policy section.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 When an error occurs and control jumps to the `on-error` policy section, the error is stored in  [context.LastError](api-management-policy-expressions.md#ContextVariables) property which can be accessed by policies in the `on-error` section and has the following properties.  
  
|Name|Type|Description|Required|  
|----------|----------|-----------------|--------------|  
|Source|string|Names the element where the error occurred. Could be either policy or a  built-in pipeline step name.|Yes|  
|Reason|string|Machine-friendly error code, which could be used in error handling.|No|  
|Message|string|Human-readable error description.|Yes|  
|Scope|string|Name of the scope where the error occurred and could be one of "global", "product", "api", or "operation"|No|  
|Section|string|Section name where error occurred and could one of "inbound", "backend", "outbound", or "on-error".|No|  
|Path|string|Specifies nested policy, e.g. "choose[3]/when[2]".|No|  
|PolicyId|string|Value of the `id` attribute, if specified by the customer, on the policy where error occurred|No|  
  
> [!NOTE]
>  All policies have an optional `id` attribute that can be added to the root element of the policy. If this attribute is present in a policy when an error condition occurs, the value of the attribute can be retrieved using the `context.LastError.PolicyId` property.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Predefined errors for built-in steps  
 The following errors are predefined for error conditions that can occur during the evaluation of built-in processing steps.  
  
|Source|Condition|Reason|Message|  
|------------|---------------|------------|-------------|  
|configuration|Uri doesn't match to any Api or Operation|OperationNotFound|Unable to match incoming request to an operation.|  
|authorization|Subscription key not supplied|SubscriptionKeyNotFound|Access denied due to missing subscription key. Make sure to include subscription key when making requests to this API.|  
|authorization|Subscription key value is invalid|SubscriptionKeyInvalid|Access denied due to invalid subscription key. Make sure to provide a valid key for an active subscription.|  
  
## <a name="predefined-errors-for-policies"></a>Predefined errors for policies  
 The following errors are predefined for error conditions that can occur during policy evaluation.  
  
|Source|Condition|Reason|Message|  
|------------|---------------|------------|-------------|  
|rate-limit|Rate limit exceeded|RateLimitExceeded|Rate limit is exceeded|  
|quota|Quota exceeded|QuotaExceeded|Out of call volume quota. Quota will be replenished in xx:xx:xx. -or- Out of bandwidth quota. Quota will be replenished in xx:xx:xx.|  
|jsonp|Callback parameter value is invalid (contains wrong characters)|CallbackParameterInvalid|Value of callback parameter {callback-parameter-name} is not a valid JavaScript identifier.|  
|ip-filter|Failed to parse caller IP from request|FailedToParseCallerIP|Failed to establish IP address for the caller. Access denied.|  
|ip-filter|Caller IP is not in allowed list|CallerIpNotAllowed|Caller IP address {ip-address} is not allowed. Access denied.|  
|ip-filter|Caller IP is in blocked list|CallerIpBlocked|Caller IP address is blocked. Access denied.|  
|check-header|Required header not presented or value is missing|HeaderNotFound|Header {header-name} was not found in the request. Access denied.|  
|check-header|Required header not presented or value is missing|HeaderValueNotAllowed|Header {header-name} value of {header-value} is not allowed. Access denied.|  
|validate-jwt|Jwt token is missing in request|TokenNotFound|JWT not found in the request. Access denied.|  
|validate-jwt|Signature validation failed|TokenSignatureInvalid|<message from jwt library\>. Access denied.|  
|validate-jwt|Invalid audience|TokenAudienceNotAllowed|<message from jwt library\>. Access denied.|  
|validate-jwt|Invalid issuer|TokenIssuerNotAllowed|<message from jwt library\>. Access denied.|  
|validate-jwt|Token expired|TokenExpired|<message from jwt library\>. Access denied.|  
|validate-jwt|Signature key was not resolved by id|TokenSignatureKeyNotFound|<message from jwt library\>. Access denied.|  
|validate-jwt|Required claims are missing from token|TokenClaimNotFound|JWT token is missing the following claims: <c1\>, <c2\>, … Access denied.|  
|validate-jwt|Claim values mismatch|TokenClaimValueNotAllowed|Claim {claim-name} value of {claim-value} is not allowed. Access denied.|  
|validate-jwt|Other validation failures|JwtInvalid|<message from jwt library\>|

## <a name="next-steps"></a>Next steps
For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).  