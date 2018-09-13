---
title: 'Azure Active Directory B2C: Overview | Microsoft Docs'
description: Developing consumer-facing applications with Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 851319639f1443c062b87305bbde351f41846433
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556643"
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications"></a>Azure Active Directory B2C: Sign up and sign in consumers in your applications
Azure Active Directory B2C is a comprehensive cloud identity management solution for your consumer-facing web and mobile applications. It is a highly available global service that scales to hundreds of millions of consumer identities. Built on an enterprise-grade secure platform, Azure Active Directory B2C keeps your applications, your business, and your consumers protected.

In the past, application developers who wanted to sign up and sign in consumers into their applications would have written their own code. And they would have used on-premises databases or systems to store usernames and passwords. Azure Active Directory B2C offers developers a better way to integrate consumer identity management into their applications with the help of a secure, standards-based platform and a rich set of extensible policies. When you use Azure Active Directory B2C, your consumers can sign up for your applications by using their existing social accounts (Facebook, Google, Amazon, LinkedIn) or by creating new credentials (email address and password, or username and password); we call the latter "local accounts."

## <a name="get-started"></a>Get started
To build an application that accepts consumer sign up and sign in, you'll first need to register the application with an Azure Active Directory B2C tenant. Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).

You can write your application against the Azure Active Directory B2C service either by choosing to send protocol messages directly, using [OAuth 2.0 or Open ID Connect](active-directory-b2c-reference-protocols.md), or by using our libraries to do the work for you. Choose your favorite platform in the following table and get started.

[!INCLUDE [active-directory-b2c-quickstart-table](../../includes/active-directory-b2c-quickstart-table.md)]

## <a name="whats-new"></a>What's new
Check back here often to learn about future changes to the Azure Active Directory B2C. We'll also tweet about any updates by using @AzureAD.

* Learn about our [extensible policy framework](active-directory-b2c-reference-policies.md) and about the types of policies that you can create and use in your applications.
* Bookmark our [service blog](https://blogs.msdn.microsoft.com/azureadb2c/) for notifications on minor service issues, updates, status and mitigations. Continue to monitor the [Azure status dashboard](https://azure.microsoft.com/status/) as well.
* Current [service limitations, restrictions, and constraints](active-directory-b2c-limitations.md).
* Finally, a [code sample](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-b2c) using Azure AD B2C & ASP.NET Core.

## <a name="how-to-articles"></a>How-to articles
Learn how to use specific Azure Active Directory B2C features:

* Configure [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Microsoft account](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md), and [LinkedIn](active-directory-b2c-setup-li-app.md) accounts for use in your consumer-facing applications.
* [Use custom attributes to collect information about your consumers](active-directory-b2c-reference-custom-attr.md).
* [Enable Azure Multi-Factor Authentication in your consumer-facing applications](active-directory-b2c-reference-mfa.md).
* [Set up self-service password reset for your consumers](active-directory-b2c-reference-sspr.md).
* [Customize the look and feel of sign up, sign in, and other consumer-facing pages](active-directory-b2c-reference-ui-customization.md) that are served by Azure Active Directory B2C.
* [Use the Azure Active Directory Graph API to programmatically create, read, update, and delete consumers](active-directory-b2c-devquickstarts-graph-dotnet.md) in your Azure Active Directory B2C tenant.

## <a name="next-steps"></a>Next steps
These links will be useful for exploring the service in depth:

* See the [Azure Active Directory B2C pricing information](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Review our [code samples](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) for Azure Active Directory B2C. 
* Get help on Stack Overflow by using the [azure-ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) tag.
* Give us your thoughts by using [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)--we want to hear them!
* Review the [Azure AD B2C Protocol Reference](active-directory-b2c-reference-protocols.md).
* Review the [Azure AD B2C Token Reference](active-directory-b2c-reference-tokens.md).
* Read the [Azure Active Directory B2C FAQs](active-directory-b2c-faqs.md).
* [File support requests for Azure Active Directory B2C](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Get security updates for our products
We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.

