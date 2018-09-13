---
title: 'Azure Active Directory B2C: Limitations and restrictions | Microsoft Docs'
description: A list of limitations and restrictions with Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: bryanla
ms.assetid: 04ec3310-98bb-4bb1-856d-ddc66913b390
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: parakhj
ms.openlocfilehash: 0fb7648a41ca534cec00a93b165f809d17d75c3e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548873"
---
# <a name="azure-active-directory-b2c-limitations-and-restrictions"></a>Azure Active Directory B2C: Limitations and restrictions

There are several features and functionalities of Azure Active Directory (Azure AD) B2C that are not yet supported. Many of these known issues & limitations will be addressed going forward, but you should be aware of them if you are building consumer-facing applications using Azure AD B2C.

## <a name="issues-during-the-creation-of-azure-ad-b2c-tenants"></a>Issues during the creation of Azure AD B2C tenants

If you encounter issues during the [creation of an Azure AD B2C tenant](active-directory-b2c-get-started.md), see [Create an Azure AD tenant or an Azure AD B2C tenant--issues and resolutions](active-directory-b2c-support-create-directory.md) for guidance.

Note that there are known issues when you delete an existing B2C tenant and re-create it with the same domain name. You have to create a B2C tenant with a different domain name.

## <a name="branding-issues-on-verification-email"></a>Branding issues on verification email

The default verification email contains Microsoft branding. We will remove it in the future. For now, you can remove it by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).

## <a name="branding-issues-on-local-account-sign-in-page-in-a-sign-in-policy"></a>Branding issues on local account sign-in page in a Sign-in policy

The local account sign-in page in a Sign-in policy can be customized only using the [company branding feature](../active-directory/active-directory-add-company-branding.md), and not by the page UI customization feature described [here](active-directory-b2c-reference-ui-customization.md). In addition, there are no labels or placeholders available on the username and password fields. As a workaround, we recommend that you use the fully-customizable "Sign-up or Sign-in policy" instead. If you are interested in fully customizing the local account sign-in page in a Sign-in policy, do vote for the feature on [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/13062033-b2c-fully-customizable-sign-in-page).

## <a name="restrictions-on-applications"></a>Restrictions on applications

The following types of applications are not currently supported in Azure AD B2C. For a description of the supported types of applications, refer to [Azure AD B2C: Types of applications](active-directory-b2c-apps.md).

### <a name="daemons--server-side-applications"></a>Daemons / server-side applications

Applications that contain long-running processes or that operate without the presence of a user also need a way to access secured resources, such as Web APIs. These applications can authenticate and get tokens by using the application's identity (rather than a consumer's delegated identity) in the [OAuth 2.0 client credentials flow](active-directory-b2c-reference-protocols.md). This flow is not yet available in Azure AD B2C, so for now, applications can get tokens only after an interactive consumer sign-in flow has occurred.


### <a name="web-api-chains-on-behalf-of"></a>Web API chains (On-Behalf-Of)

Many architectures include a Web API that needs to call another downstream Web API, both secured by Azure AD B2C. This scenario is common in native clients that have a Web API back end, which in turn calls a Microsoft online service such as the Azure AD Graph API.

This chained Web API scenario can be supported by using the OAuth 2.0 Jwt Bearer Credential grant, otherwise known as the On-Behalf-Of flow. However, the On-Behalf-Of flow is not currently implemented in the Azure AD B2C.

## <a name="restrictions-on-reply-urls"></a>Restrictions on reply URLs

Currently, apps registered in Azure AD B2C are restricted to a limited set of reply URL values. The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain. For example, you cannot register a web app that has one of these direct URLs:

`https://login-east.contoso.com`
`https://login-west.contoso.com`

The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding. The request to add the DNS name will fail if either of the following conditions is true:

* The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.
* The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.

For example, if the app has this reply URL:

`https://login.contoso.com`

You can add to it, like this:

`https://login.contoso.com/new`

In this case, the DNS name matches exactly. Or, you can do this:

`https://new.login.contoso.com`

In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:

`https://contoso.com`
`https://login-east.contoso.com`
`https://login-west.contoso.com`

You can add the latter two because they are subdomains of the first reply URL, contoso.com. This limitation will be removed in an upcoming release.

To learn how to register an app in Azure AD B2C, see [How to register your application with Azure Active Directory B2C](active-directory-b2c-app-registration.md).

## <a name="restriction-on-libraries-and-sdks"></a>Restriction on libraries and SDKs

The set of Microsoft supported libraries that work Azure AD B2C is very limited at this time. We have support for .NET based web apps and services, as well as NodeJS web apps and services.  We also have a preview .NET client library known as MSAL that can be used with Azure AD B2C in Windows & other .NET apps.

We do not currently have library support any other languages or platforms, including iOS & Android.  If you wish to build on a different platform than those mentioned above, we recommend using an open-source SDK, referring to our [OAuth 2.0 and OpenID Connect Protocol Reference](active-directory-b2c-reference-protocols.md) as necessary.  Azure AD B2C implements OAuth & OpenID Connect, which makes it possible to use a generic OAuth or OpenID Connect library for integration.

Our iOS & Android quick start tutorials use open-source libraries that we have tested for compatibility with Azure AD B2C.  All of our quick-start tutorials are available in our [Getting started](active-directory-b2c-overview.md#get-started) section.

## <a name="restriction-on-protocols"></a>Restriction on protocols

Azure AD B2C supports OpenID Connect and OAuth 2.0. However, not all features and capabilities of each protocol have been implemented. To better understand the scope of supported protocol functionality in Azure AD B2C, read through our [OpenID Connect and OAuth 2.0 protocol reference](active-directory-b2c-reference-protocols.md). SAML and WS-Fed protocol support is not available.

## <a name="restriction-on-tokens"></a>Restriction on tokens

Many of the tokens issued by Azure AD B2C are implemented as JSON Web Tokens, or JWTs. However, not all information contained in JWTs (known as "claims") is quite as it should be or is missing. An example is the "preferred_username" claim.  As the values, format, or meaning of claims change over time, tokens for your existing policies will remain unaffected - you can rely on their values in production apps.  As values change, we will give you the opportunity to configure those changes for each of your policies.  To better understand the tokens emitted currently by the Azure AD B2C service, read through our [token reference](active-directory-b2c-reference-tokens.md).

## <a name="restriction-on-nested-groups"></a>Restriction on nested groups

Nested group memberships aren't supported in Azure AD B2C tenants. We don't plan to add this capability.

## <a name="restriction-on-differential-query-feature-on-azure-ad-graph-api"></a>Restriction on differential query feature on Azure AD Graph API

The [differential query feature on Azure AD Graph API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-differential-query) isn't supported in Azure AD B2C tenants. This is on our long-term roadmap.

## <a name="issues-with-user-management-on-the-azure-classic-portal"></a>Issues with user management on the Azure classic portal

B2C features are accessible on the Azure portal. However, you can use the Azure classic portal to access other tenant features, including user management. Currently there are a couple of known issues with user management (the **Users** tab) on the Azure classic portal:

* For a local account user (i.e., a consumer who signs up with an email address and password, or a username and password), the **User Name** field doesn't correspond to the sign-in identifier (email address or username) that was used during sign-up. This is because the field displayed on the Azure classic portal is actually the User Principal Name (UPN), which is not used in B2C scenarios. To view the sign-in identifier of the local account, find the user object in [Graph Explorer](https://graphexplorer.cloudapp.net/). You will find the same issue with a social account user (i.e., a consumer who signs up with Facebook, Google+, etc.), but in that case, there is no sign-in identifier to speak of.

    ![Local account - UPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-limitations/limitations-user-mgmt.png)
* For a local account user, you will not able to edit any of the fields and save changes on the **Profile** tab.

## <a name="issues-with-admin-initiated-password-reset-on-the-azure-classic-portal"></a>Issues with admin-initiated password reset on the Azure classic portal

If you reset the password for a local account-based consumer on the Azure classic portal (the **Reset Password** command on the **Users** tab), that consumer will not be able to change his or her password on the next sign in, if you use a Sign up or Sign in policy, and will be locked out of your applications. As a workaround, use the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md) to reset the consumer's password (without password expiration) or use a Sign in policy instead of a Sign up or Sign in policy.

## <a name="issues-with-creating-a-custom-attribute"></a>Issues with creating a custom attribute

A [custom attribute added on the Azure portal](active-directory-b2c-reference-custom-attr.md) is not immediately created in your B2C tenant. You'll have to use the custom attribute in at least one of your policies for it to get created in your B2C tenant and to become available via Graph API.

## <a name="issues-with-verifying-a-domain-on-the-azure-classic-portal"></a>Issues with verifying a domain on the Azure classic portal

Currently you can't verify a domain successfully on the [Azure classic portal](https://manage.windowsazure.com/).

## <a name="issues-with-sign-in-with-mfa-policy-on-safari-browsers"></a>Issues with Sign-in with MFA policy on Safari browsers

Requests to sign-in policies (with MFA turned ON) fail intermittently on Safari browsers with HTTP 400 (Bad Request) errors. This is due Safari's low cookie size limits. There are a couple of workarounds for this issue:

* Use the "Sign-up or sign-in policy" instead of the "sign-in policy".
* Reduce the number of **Application claims** being requested in your policy.

## <a name="issues-with-windows-desktop-wpf-apps-using-azure-ad-b2c"></a>Issues with Windows Desktop WPF apps using Azure AD B2C

Requests to Azure AD B2C from a Windows Desktop WPF app sometimes fail with the following error message: "The browser based authentication dialog failed to complete. Reason: The protocol is not known and no pluggable protocols have been entered that match.".

This is due to the size of authorization codes provided by Azure AD B2C; the size is correlated with the number of claims requested in a token. A workaround for this issue is to reduce the number of claims requested in the token and to query Graph API separately for other claims.

