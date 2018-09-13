---
title: Azure Active Directory developer's guide | Microsoft Docs
description: This article provides a comprehensive guide to developer-oriented resources for Azure Active Directory.
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: ''
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/09/2016
ms.author: mbaldwin
ms.openlocfilehash: a8f67d94549fa89da9746ad156dd6c68d99330aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554032"
---
# <a name="azure-active-directory-developers-guide"></a>Azure Active Directory developer's guide
## <a name="overview"></a>Overview
As an identity management as a service (IDMaaS) platform, Azure Active Directory (AD) provides developers an effective way to integrate identity management into their applications. The following articles provide overviews on implementation and key features of Azure AD. We suggest that you read them in order, or jump to [Getting started](#getting-started) if you're ready to dig in.

1. [The benefits of Azure AD integration](active-directory-how-to-integrate.md): Discover why integration with Azure AD offers the best solution for secure sign-in and authorization.
2. [Azure AD authentication scenarios](active-directory-authentication-scenarios.md): Take advantage of simplified authentication in Azure AD to provide sign-on to your application.
3. [Integrating applications with Azure AD](active-directory-integrating-applications.md): Learn how to add, update, and remove applications from Azure AD, and about the branding guidelines for integrated apps.
4. [Microsoft Graph](https://graph.microsoft.io/) and [Azure AD Graph API](active-directory-graph-api.md): Programmatically access Azure AD through REST API endpoints. **We strongly recommend that you use Microsoft Graph instead of Azure AD Graph API to access Azure Active Directory resources.** Our development efforts are now concentrated on Microsoft Graph and no further enhancements are planned for Azure AD Graph API. There are a very limited number of scenarios for which Azure AD Graph API might still be appropriate; for more information, see the [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blog post in the Office Dev Center.
5. [Azure AD authentication libraries](active-directory-authentication-libraries.md): Easily authenticate users to obtain access tokens by using Azure AD authentication libraries for .NET, JavaScript, Objective-C, Android, and more.

## <a name="getting-started"></a>Getting started
These tutorials are tailored for multiple platforms and can help you quickly start developing with Azure Active Directory. As a prerequisite, you must [get an Azure Active Directory tenant](active-directory-howto-tenant.md).

### <a name="mobile-and-pc-application-quick-start-guides"></a>Mobile and PC application quick-start guides
| [![iOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/ios.png)](active-directory-devquickstarts-ios.md) | [![Android](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/android.png)](active-directory-devquickstarts-android.md) | [![.NET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/net.png)](active-directory-devquickstarts-dotnet.md) | [![Windows Universal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/windows.png)](active-directory-devquickstarts-windowsstore.md) | 
|:---:|:---:|:---:|:---:|:---:|
| [iOS](active-directory-devquickstarts-ios.md) |[Android](active-directory-devquickstarts-android.md) |[.NET](active-directory-devquickstarts-dotnet.md) |[Windows</br>Universal](active-directory-devquickstarts-windowsstore.md) |

|[![Xamarin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/xamarin.png)](active-directory-devquickstarts-xamarin.md) | [![Cordova](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/cordova.png)](active-directory-devquickstarts-cordova.md) | [![OAuth 2.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/oauth-2.png)](active-directory-protocols-oauth-code.md) |
|:---:|:---:|:---:|
|[Xamarin](active-directory-devquickstarts-xamarin.md) |[Cordova](active-directory-devquickstarts-cordova.md) |[Integrate directly</br>with OAuth 2.0](active-directory-protocols-oauth-code.md) |

### <a name="web-application-quick-start-guides"></a>Web application quick-start guides
| [![.NET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/net.png)](active-directory-devquickstarts-webapp-dotnet.md) | [![Java](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/java.png)](active-directory-devquickstarts-webapp-java.md) | [![AngularJS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/angularjs.png)](active-directory-devquickstarts-angular.md) |
|:---:|:---:|:---:|
| [.NET](active-directory-devquickstarts-webapp-dotnet.md) |[Java](active-directory-devquickstarts-webapp-java.md) |[AngularJS](active-directory-devquickstarts-angular.md) |[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |[Node.js](active-directory-devquickstarts-openidconnect-nodejs.md) |[Integrate directly</br> with OpenID Connect](active-directory-protocols-openid-connect-code.md) |

| [![Javascript](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/javascript.png)](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | [![Node.js](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/nodejs.png)](active-directory-devquickstarts-openidconnect-nodejs.md) | [![OpenID Connect](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/openid-connect.png)](active-directory-protocols-openid-connect-code.md) |
|:---:|:---:|:---:|
|[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |[Node.js](active-directory-devquickstarts-openidconnect-nodejs.md) |[Integrate directly</br> with OpenID Connect](active-directory-protocols-openid-connect-code.md) |

### <a name="web-api-quick-start-guides"></a>Web API quick-start guides
| [![.NET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/net.png)](active-directory-devquickstarts-webapi-dotnet.md) | [![Node.js](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/nodejs.png)](active-directory-devquickstarts-webapi-nodejs.md) |
|:---:|:---:|
| [.NET](active-directory-devquickstarts-webapi-dotnet.md) |[Node.js](active-directory-devquickstarts-webapi-nodejs.md) |

### <a name="microsoft-graph-and-azure-ad-graph-api-quick-start-guides"></a>Microsoft Graph and Azure AD Graph API quick-start guides
| [![Microsoft Graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/msgraph.png)](https://developer.microsoft.com/graph/quick-start) | [![Azure AD Graph API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-developers-guide/graph.png)](active-directory-graph-api-quickstart.md) |
|:---:|:---:|
| [Microsoft Graph](https://developer.microsoft.com/graph/quick-start) | [Azure AD Graph API](active-directory-graph-api-quickstart.md) |

## <a name="how-tos"></a>How-tos
These articles describe how to perform specific tasks by using Azure Active Directory:

* [Get an Azure AD tenant](active-directory-howto-tenant.md)
* [Sign in any Azure AD user using the multi-tenant application pattern](active-directory-devhowto-multi-tenant-overview.md)
* [Use a certificate instead of a secret to authenticate an application identity](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/)
* Enable cross-app SSO using ADAL, on [Android](active-directory-sso-android.md) and on [iOS](active-directory-sso-ios.md) devices
* [Make your application AppSource Certified for Azure AD](active-directory-devhowto-appsource-certified.md)
* [List your application in the Azure AD application gallery](active-directory-app-gallery-listing.md)
* [Submit web apps for Office 365 to the Seller Dashboard](https://msdn.microsoft.com/office/office365/howto/submit-web-apps-seller-dashboard)
* [Register an application with Azure Active Directory using the Azure portal](../active-directory-app-registration.md)
* [Understand the Azure Active Directory application manifest](active-directory-application-manifest.md)
* [Understand the branding guidelines for the sign-in and app acquisition buttons in your client application](active-directory-branding-guidelines.md)
* [Preview: How to build apps that sign users in with both personal & work or school accounts](active-directory-appmodel-v2-overview.md)
* [Preview: How to build apps that sign up & sign in consumers](../../active-directory-b2c/active-directory-b2c-overview.md)
* [Preview: Configuring token lifetimes in Azure AD](../active-directory-configurable-token-lifetimes.md) using PowerShell. See [Policy operations](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) and the [Policy entity](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity) for details on configuring via the Azure AD Graph API.

## <a name="reference"></a>Reference
These articles provide a foundation reference for REST and authentication library APIs, protocols, errors, code samples, and endpoints.  

### <a name="support"></a>Support
* [Tagged questions](http://stackoverflow.com/questions/tagged/azure-active-directory): Find Azure Active Directory solutions on Stack Overflow by searching for the tags [azure-active-directory](http://stackoverflow.com/questions/tagged/azure-active-directory) and [adal](http://stackoverflow.com/questions/tagged/adal).
* See the [Azure AD developer glossary](active-directory-dev-glossary.md) for definitions of some of the commonly used terms related to application development and integration.

### <a name="code"></a>Code
* [Azure Active Directory open-source libraries](http://github.com/AzureAD): The easiest way to find a library’s source is by using our [library list](active-directory-authentication-libraries.md).
* [Azure Active Directory samples](https://github.com/azure-samples?query=active-directory): The easiest way to navigate the list of samples is by using the [index of code samples](active-directory-code-samples.md).
* [Active Directory Authentication Library (ADAL) for .NET](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) - Reference documentation is available for both [the latest major version](https://docs.microsoft.com/active-directory/adal/microsoft.identitymodel.clients.activedirectory) and [the previous major version](https://docs.microsoft.com/active-directory/adal/v2/microsoft.identitymodel.clients.activedirectory).

### <a name="microsoft-graph-and-azure-ad-graph-api"></a>Microsoft Graph and Azure AD Graph API
> [!IMPORTANT]
> We strongly recommend that you use [Microsoft Graph](https://graph.microsoft.io/) instead of Azure AD Graph API to access Azure Active Directory resources. Our development efforts are now concentrated on Microsoft Graph and no further enhancements are planned for Azure AD Graph API. There are a very limited number of scenarios for which Azure AD Graph API might still be appropriate; for more information, see the [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blog post in the Office Dev Center.
> 

* [Microsoft Graph](https://graph.microsoft.io/): Documentation, reference, samples, and SDKs for Microsoft Graph. 
* [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog): REST reference for the Azure Active Directory Graph API. 
* [Azure AD Graph API permission scopes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes): OAuth 2.0 permission scopes that are used to control the access that an app has to directory data in a tenant.

### <a name="authentication-and-authorization-protocols"></a>Authentication and authorization protocols
* [Signing Key Rollover in Azure AD](active-directory-signing-key-rollover.md): Learn about Azure AD’s signing key rollover cadence and how to update the key for the most common application scenarios.
* [OAuth 2.0 protocol: Using the authorization code grant](active-directory-protocols-oauth-code.md): You can use the OAuth 2.0 protocol's authorization code grant, to authorize access to Web applications and Web APIs in your Azure Active Directory tenant.
* [OAuth 2.0 protocol: Understanding the implicit grant](active-directory-dev-understanding-oauth2-implicit-grant.md): Learn more about the implicit authorization grant, and whether it's right for your application.
* [OAuth 2.0 protocol: Service to Service Calls Using Client Credentials](active-directory-protocols-oauth-service-to-service.md): The OAuth 2.0 Client Credentials grant permits a web service (a confidential client) to use its own credentials to authenticate when calling another web service, instead of impersonating a user. In this scenario, the client is typically a middle-tier web service, a daemon service, or website.
* [OpenID Connect 1.0 protocol: Sign-in and authentication](active-directory-protocols-openid-connect-code.md): The OpenID Connect 1.0 protocol extends OAuth 2.0 for use as an authentication protocol. A client application can receive an id_token to manage the sign-in process, or augment the authorization code flow to receive both an id_token and authorization code.
* [SAML 2.0 protocol reference](active-directory-saml-protocol-reference.md): The SAML 2.0 protocol enables applications to provide a single sign-on experience to their users.
* [WS-Federation 1.2 protocol](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html): Azure Active Directory supports WS-Federation 1.2 as per the Web Services Federation Version 1.2 Specification. For more information about the federation metadata document, please see [Federation Metadata](active-directory-federation-metadata.md).
* [Supported token and claim types](active-directory-token-and-claims.md): You can use this guide to understand and evaluate the claims in the SAML 2.0 and JSON Web Tokens (JWT) tokens.

## <a name="videos"></a>Videos
### <a name="build"></a>Build
These overview presentations on developing apps by using Azure Active Directory feature speakers who work directly in the engineering team. The presentations cover fundamental topics, including IDMaaS, authentication, identity federation, and single sign-on.

* [Microsoft Identity: State of the Union and Future Direction](https://azure.microsoft.com/documentation/videos/build-2016-microsoft-identity-state-of-the-union-and-future-direction/)
* [Azure Active Directory: Identity management as a service for modern applications](https://azure.microsoft.com/documentation/videos/build-2015-azure-active-directory-identity-management-as-a-service-for-modern-applications/)
* [Develop modern web applications with Azure Active Directory](https://azure.microsoft.com/documentation/videos/build-2015-develop-modern-web-applications-with-azure-active-directory/)
* [Develop modern native applications with Azure Active Directory](https://azure.microsoft.com/documentation/videos/build-2015-develop-modern-native-applications-with-azure-active-directory/)

### <a name="azure-friday"></a>Azure Friday
[Azure Friday](https://azure.microsoft.com/documentation/videos/azure-friday/) is a recurring Friday 1:1 video series that's dedicated to bringing you short (10–15 minutes) interviews with experts on a variety of Azure topics.  Use the Services Filter feature on the page to see all Azure Active Directory videos.

* [Azure Identity 101](https://azure.microsoft.com/documentation/videos/azure-identity-basics/)
* [Azure Identity 102](https://azure.microsoft.com/documentation/videos/azure-identity-creating-active-directory/)
* [Azure Identity 103](https://azure.microsoft.com/documentation/videos/azure-identity-application-to-authenticate/)

## <a name="social"></a>Social
* [Active Directory Team blog](http://blogs.technet.com/b/ad/): The latest developments in the world of Azure Active Directory.
* [Azure Active Directory Graph Team blog](https://blogs.msdn.microsoft.com/aadgraphteam): Azure Active Directory information that's specific to the Graph API.
* [Cloud Identity](http://www.cloudidentity.net): Thoughts on identity management as a service, from a principal Azure Active Directory PM.  
* [Azure Active Directory on Twitter](https://twitter.com/azuread): Azure Active Directory announcements in 140 characters or fewer.

## <a name="windows-server-on-premises-development"></a>Windows Server on-premises development
For guidance on using Windows Server and Active Directory Federation Services (ADFS) development, see:

* [AD FS Scenarios for Developers](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/ad-fs-scenarios-for-developers): Provides an overview of AD FS components and how it works, with details on the supported authentication/authorization scenarios.
* [AD FS walkthroughs](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/ad-fs-development): a list of walk-through articles, which provide step-by-step instructions on implementing the related authentication/authorization flows.

















