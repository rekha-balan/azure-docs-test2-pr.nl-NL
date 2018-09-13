---
title: Azure Active Directory Application and Service Principal Objects | Microsoft Docs
description: A discussion of the relationship between application and service principal objects in Azure Active Directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
services: active-directory
editor: ''
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/29/2016
ms.author: bryanla;mbaldwin
ms.openlocfilehash: 23c353f510c3eab7b6395aae9108e4b6bc6713ee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554816"
---
# <a name="application-and-service-principal-objects-in-azure-active-directory"></a>Application and service principal objects in Azure Active Directory
Sometimes the meaning of the Azure Active Directory (Azure AD) term "application" can be easily misunderstood, especially if supporting context is missing. The goal of this article is to make it clearer, by clarifying conceptual and concrete aspects of Azure AD application integration, with an illustration of registration and consent for a [multi-tenant application](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Overview
An Azure AD application is broader than just a piece of software. It's a conceptual term, referring not only to application software, but also its registration (aka: identity configuration) with Azure AD, which allows it to participate in authentication and authorization "conversations" at runtime. By definition, an application can function in a [client](active-directory-dev-glossary.md#client-application) role (consuming a resource), a [resource server](active-directory-dev-glossary.md#resource-server) role (exposing APIs to clients), or even both. The conversation protocol is defined by an [OAuth 2.0 Authorization Grant flow](active-directory-dev-glossary.md#authorization-grant), with a goal of allowing the client/resource to access/protect a resource's data respectively. Now let's go a level deeper, and see how the Azure AD application model represents an application internally. 

## <a name="application-registration"></a>Application registration
When you register an application in the [Azure portal][AZURE-Portal], two objects are created in your Azure AD tenant: an application object, and a service principal object.

#### <a name="application-object"></a>Application object
An Azure AD application is *defined* by its one and only application object, which resides in the Azure AD tenant where the application was registered, known as the application's "home" tenant. The application object provides identity-related information for an application, and is the template from which its corresponding service principal object(s) are *derived* for use at run-time. 

Consider the application object as the *global* representation of your application (for use across all tenants), and the service principal as the *local* representation (for use in a specific tenant). The Azure AD Graph [Application entity][AAD-Graph-App-Entity] defines the schema for an application object. An application object therefore has a 1:1 relationship with the software application, and a 1:*n* relationship with its corresponding *n* service principal object(s).

#### <a name="service-principal-object"></a>Service principal object
The service principal object defines the policy and permissions for an application, providing the basis for a security principal to represent the application when accessing resources at run-time. The Azure AD Graph [ServicePrincipal entity][AAD-Graph-Sp-Entity] defines the schema for a service principal object. 

Before an Azure AD tenant will allow an application to access the resources it is securing, a service principal must be created in the given tenant. The service principal provides the basis for Azure AD to secure the application's access to resources owned by users from that tenant. A single-tenant application will have only one service principal (in its home tenant). A multi-tenant [Web application](active-directory-dev-glossary.md#web-client) will also have a service principal in each tenant where an administrator or user(s) from that tenant have given consent, allowing it to access their resources. Following consent, the service principal object will be consulted for future authorization requests. 

> [!NOTE]
> Any changes you make to your application object, are also reflected in its service principal object in the application's home tenant only (the tenant where it was registered). For multi-tenant applications, changes to the application object are not reflected in any consumer tenants' service principal objects, until the consumer tenant removes access and grants access again.
> 
> 

## <a name="example"></a>Example
The following diagram illustrates the relationship between an application's application object and corresponding service principal objects, in the context of a sample multi-tenant application called **HR app**. There are three Azure AD tenants in this scenario: 

* **Adatum** - the tenant used by the company that developed the **HR app**
* **Contoso** - the tenant used by the Contoso organization, which is a consumer of the **HR app**
* **Fabrikam** - the tenant used by the Fabrikam organization, which also consumes the **HR app**

![Relationship between an application object and a service principal object](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-application-objects/application-objects-relationship.png)

In the previous diagram, Step 1 is the process of creating the application and service principal objects in the application's home tenant.

In Step 2, when Contoso and Fabrikam administrators complete consent, a service principal object is created in their company's Azure AD tenant and assigned the permissions that the administrator granted. Also note that the HR app could be configured/designed to allow consent by users for individual use.

In Step 3, the consumer tenants of the HR application (Contoso and Fabrikam) each have their own service principal object. Each represents their use of an instance of the application at runtime, governed by the permissions consented by the respective administrator.

## <a name="next-steps"></a>Next steps
An application's application object can be accessed via the Azure AD Graph API, as represented by its OData [Application entity][AAD-Graph-App-Entity]

An application's service principal object can be accessed via the Azure AD Graph API, as represented by its OData [ServicePrincipal entity][AAD-Graph-Sp-Entity]

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com

