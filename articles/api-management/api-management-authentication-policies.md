---
title: Azure API Management authentication policies | Microsoft Docs
description: Learn about the authentication policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: apimpm
ms.openlocfilehash: 4d13d9dbea9da9db5bfe9a9af85fdbf9eab1ae84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804926"
---
# <a name="api-management-authentication-policies"></a>API Management authentication policies
This topic provides a reference for the following API Management policies. For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  

##  <a name="AuthenticationPolicies"></a> Authentication policies  
  
-   [Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.  
  
-   [Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.  
  
##  <a name="Basic"></a> Authenticate with Basic  
 Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication. This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.  
  
### <a name="policy-statement"></a>Policy statement  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Example  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|authentication-basic|Root element.|Yes|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|username|Specifies the username of the Basic credential.|Yes|N/A|  
|password|Specifies the password of the Basic credential.|Yes|N/A|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** API  
  
##  <a name="ClientCertificate"></a> Authenticate with client certificate  
 Use the `authentication-certificate` policy to authenticate with a backend service using client certificate. The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.  
  
### <a name="policy-statement"></a>Policy statement  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Example  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|authentication-certificate|Root element.|Yes|  
  
### <a name="attributes"></a>Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|thumbprint|The thumbprint for the client certificate.|Yes|N/A|  
  
### <a name="usage"></a>Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** API  
  

## <a name="next-steps"></a>Next steps
For more information working with policies, see:

+ [Policies in API Management](api-management-howto-policies.md)
+ [Transform APIs](transform-api.md)
+ [Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings
+ [Policy samples](policy-samples.md)   
