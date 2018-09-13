---
title: How to configure a new multi-tenant application | Microsoft Docs
description: How to configure single sign-on for a custom application you are developing and registering with Azure AD.
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: c6057026fadc643e9ce321bc862f99c29fbe1662
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549789"
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="d2a5c-103">How to configure a new multi-tenant application</span><span class="sxs-lookup"><span data-stu-id="d2a5c-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="d2a5c-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="d2a5c-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="d2a5c-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span><span class="sxs-lookup"><span data-stu-id="d2a5c-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="d2a5c-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span><span class="sxs-lookup"><span data-stu-id="d2a5c-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="d2a5c-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span><span class="sxs-lookup"><span data-stu-id="d2a5c-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="d2a5c-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="d2a5c-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="d2a5c-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="d2a5c-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2a5c-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2a5c-110">Next steps</span></span>

[<span data-ttu-id="d2a5c-111">Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d2a5c-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="d2a5c-112">Enabling Cross App SSO in Android</span><span class="sxs-lookup"><span data-stu-id="d2a5c-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="d2a5c-113">Enabling Cross App SSO in iOS</span><span class="sxs-lookup"><span data-stu-id="d2a5c-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="d2a5c-114">Integrating Apps to AzureAD</span><span class="sxs-lookup"><span data-stu-id="d2a5c-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="d2a5c-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span><span class="sxs-lookup"><span data-stu-id="d2a5c-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d2a5c-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="d2a5c-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
