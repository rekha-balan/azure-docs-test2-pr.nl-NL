---
title: How to configure a new multi-tenant application | Microsoft Docs
description: How to configure single sign-on for a custom application you are developing and registering with Azure AD.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: celested
ms.openlocfilehash: 2aa3efcdec57a3e236d2b9739636656b35d16cd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869860"
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="09767-103">How to configure a new multi-tenant application</span><span class="sxs-lookup"><span data-stu-id="09767-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="09767-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="09767-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="09767-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span><span class="sxs-lookup"><span data-stu-id="09767-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="09767-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span><span class="sxs-lookup"><span data-stu-id="09767-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="09767-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span><span class="sxs-lookup"><span data-stu-id="09767-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="09767-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="09767-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="09767-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="09767-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09767-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="09767-110">Next steps</span></span>

[<span data-ttu-id="09767-111">Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="09767-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="09767-112">Enabling Cross App SSO in Android</span><span class="sxs-lookup"><span data-stu-id="09767-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="09767-113">Enabling Cross App SSO in iOS</span><span class="sxs-lookup"><span data-stu-id="09767-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="09767-114">Integrating Apps to AzureAD</span><span class="sxs-lookup"><span data-stu-id="09767-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="09767-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span><span class="sxs-lookup"><span data-stu-id="09767-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="09767-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="09767-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
