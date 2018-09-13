---
title: Azure API Management page controls | Microsoft Docs
description: Learn about the page controls available for use in developer portal templates in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 91c5e2af06ac1f9e240b7d6ee2e06281b234a6b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662281"
---
# <a name="azure-api-management-page-controls"></a>Azure API Management page controls
Azure API Management provides the following controls for use in the developer portal templates.  
  
 To use a control, place it in the desired location in the developer portal template. Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 The values for the parameters are passed in as part of the data model for the template. In most cases, you can simply paste in the provided example for each control for it to work correctly. For more information on the parameter values, you can see the data model section for each template in which a control may be used.  
  
 For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Developer portal template page controls  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [providers](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.  
  
 ![app&#45;actions control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-app-actions-control.png "APIM app-actions control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|appId|The id of the application.|  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `app-actions` control may be used in the following developer portal templates.  
  
-   [Applications](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.  
  
 ![basic&#45;signin control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-basic-signin-control.png "APIM basic-signin control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `basic-signin` control may be used in the following developer portal templates.  
  
-   [Sign in](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 The `paging-control` provides paging functionality on developer portal pages that display a list of items.  
  
 ![paging control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-paging-control.png "APIM paging control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `paging-control` control may be used in the following developer portal templates.  
  
-   [API list](api-management-api-templates.md#APIList)  
  
-   [Issue list](api-management-issue-templates.md#IssueList)  
  
-   [Product list](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.  
  
 ![providers control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-providers-control.png "APIM providers control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `providers` control may be used in the following developer portal templates.  
  
-   [Sign in](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 The `search-control` provides search functionality on developer portal pages that display a list of items.  
  
 ![search control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-search-control.png "APIM search control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `search-control` control may be used in the following developer portal templates.  
  
-   [API list](api-management-api-templates.md#APIList)  
  
-   [Product list](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.  
  
 ![sign&#45;up control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-sign-up-control.png "APIM sign-up control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `sign-up` control may be used in the following developer portal templates.  
  
-   [Sign up](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 The `subscribe-button` provides a control for subscribing a user to a product.  
  
 ![subscribe&#45;button control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscribe-button-control.png "APIM subscribe-button control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Parameters  
 None.  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `subscribe-button` control may be used in the following developer portal templates.  
  
-   [Product](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.  
  
 ![subscription&#45;cancel control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscription-cancel-control.png "APIM subscription-cancel control")  
  
### <a name="usage"></a>Usage  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|subscriptionId|The id of the subscription to cancel.|  
|cancelUrl|The subscription cancel URL.|  
  
### <a name="developer-portal-templates"></a>Developer portal templates  
 The `subscription-cancel` control may be used in the following developer portal templates.  
  
-   [Product](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Next steps
For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).







