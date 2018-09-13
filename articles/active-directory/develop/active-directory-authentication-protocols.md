---
title: Azure Active Directory authentication protocols | Microsoft Docs
description: An overview of the authentication protocols supported by Azure Active Directory (AD)
documentationcenter: dev-center-name
author: CelesteDG
services: active-directory
manager: mtillman
editor: ''
ms.assetid: 7a838ae2-c24c-4304-b6c0-e77fb888e6c0
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: celested
ms.custom: aaddev
ms.reviewer: hirsin
ms.openlocfilehash: 04cdba261d67e20762fd4bb4835568f763124fef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805264"
---
# <a name="azure-active-directory-authentication-protocols"></a><span data-ttu-id="9708a-103">Azure Active Directory authentication protocols</span><span class="sxs-lookup"><span data-stu-id="9708a-103">Azure Active Directory authentication protocols</span></span>
<span data-ttu-id="9708a-104">Azure Active Directory (Azure AD) supports several of the most widely used authentication and authorization protocols.</span><span class="sxs-lookup"><span data-stu-id="9708a-104">Azure Active Directory (Azure AD) supports several of the most widely used authentication and authorization protocols.</span></span> <span data-ttu-id="9708a-105">The topics in this section describe the supported protocols and their implementation in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9708a-105">The topics in this section describe the supported protocols and their implementation in Azure AD.</span></span> <span data-ttu-id="9708a-106">The topics included a review of supported claim types, an introduction to the use of federation metadata, detailed OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="9708a-106">The topics included a review of supported claim types, an introduction to the use of federation metadata, detailed OAuth 2.0.</span></span> <span data-ttu-id="9708a-107">and SAML 2.0 protocol reference documentation, and a troubleshooting section.</span><span class="sxs-lookup"><span data-stu-id="9708a-107">and SAML 2.0 protocol reference documentation, and a troubleshooting section.</span></span>

## <a name="authentication-protocols-articles-and-reference"></a><span data-ttu-id="9708a-108">Authentication Protocols Articles and Reference</span><span class="sxs-lookup"><span data-stu-id="9708a-108">Authentication Protocols Articles and Reference</span></span>
* <span data-ttu-id="9708a-109">[Important Information About Signing Key Rollover in Azure AD](active-directory-signing-key-rollover.md) – Learn about Azure AD’s signing key rollover cadence, changes you can make to update the key automatically, and discussion for how to update the most common application scenarios.</span><span class="sxs-lookup"><span data-stu-id="9708a-109">[Important Information About Signing Key Rollover in Azure AD](active-directory-signing-key-rollover.md) – Learn about Azure AD’s signing key rollover cadence, changes you can make to update the key automatically, and discussion for how to update the most common application scenarios.</span></span>
* <span data-ttu-id="9708a-110">[Supported Token and Claim Types](v1-id-and-access-tokens.md) - Learn about the claims in the tokens that Azure AD issues.</span><span class="sxs-lookup"><span data-stu-id="9708a-110">[Supported Token and Claim Types](v1-id-and-access-tokens.md) - Learn about the claims in the tokens that Azure AD issues.</span></span>
* <span data-ttu-id="9708a-111">[Federation Metadata](azure-ad-federation-metadata.md) - Learn how to find and interpret the metadata documents that Azure AD generates.</span><span class="sxs-lookup"><span data-stu-id="9708a-111">[Federation Metadata](azure-ad-federation-metadata.md) - Learn how to find and interpret the metadata documents that Azure AD generates.</span></span>
* <span data-ttu-id="9708a-112">[OAuth 2.0 in Azure AD](v1-protocols-oauth-code.md) - Learn about the implementation of OAuth 2.0 in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9708a-112">[OAuth 2.0 in Azure AD](v1-protocols-oauth-code.md) - Learn about the implementation of OAuth 2.0 in Azure AD.</span></span>
* <span data-ttu-id="9708a-113">[OpenID Connect 1.0](v1-protocols-openid-connect-code.md) - Learn how to use OAuth 2.0, an authorization protocol, for authentication.</span><span class="sxs-lookup"><span data-stu-id="9708a-113">[OpenID Connect 1.0](v1-protocols-openid-connect-code.md) - Learn how to use OAuth 2.0, an authorization protocol, for authentication.</span></span>
* <span data-ttu-id="9708a-114">[Service to Service Calls with Client Credentials](v1-oauth2-client-creds-grant-flow.md) - Learn how to use OAuth 2.0 client credentials grant flow for service to service calls.</span><span class="sxs-lookup"><span data-stu-id="9708a-114">[Service to Service Calls with Client Credentials](v1-oauth2-client-creds-grant-flow.md) - Learn how to use OAuth 2.0 client credentials grant flow for service to service calls.</span></span>
* <span data-ttu-id="9708a-115">[Service to Service Calls with On-Behalf-Of Flow](v1-oauth2-on-behalf-of-flow.md) - Learn how to use OAuth 2.0 On-Behalf-Of flow for service to service calls.</span><span class="sxs-lookup"><span data-stu-id="9708a-115">[Service to Service Calls with On-Behalf-Of Flow](v1-oauth2-on-behalf-of-flow.md) - Learn how to use OAuth 2.0 On-Behalf-Of flow for service to service calls.</span></span>
* <span data-ttu-id="9708a-116">[SAML Protocol Reference](active-directory-saml-protocol-reference.md) - Learn about the Single Sign-On and Single Sign-out SAML profiles of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9708a-116">[SAML Protocol Reference](active-directory-saml-protocol-reference.md) - Learn about the Single Sign-On and Single Sign-out SAML profiles of Azure AD.</span></span>

## <a name="see-also"></a><span data-ttu-id="9708a-117">See Also</span><span class="sxs-lookup"><span data-stu-id="9708a-117">See Also</span></span>
[<span data-ttu-id="9708a-118">Azure Active Directory Developer's Guide</span><span class="sxs-lookup"><span data-stu-id="9708a-118">Azure Active Directory Developer's Guide</span></span>](azure-ad-developers-guide.md)

[<span data-ttu-id="9708a-119">Active Directory Code Samples</span><span class="sxs-lookup"><span data-stu-id="9708a-119">Active Directory Code Samples</span></span>](sample-v1-code.md)
