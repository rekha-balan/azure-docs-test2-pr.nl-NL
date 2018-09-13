---
title: Unexpected consent prompt when signing in to an application | Microsoft Docs
description: How to troubleshoot when a user sees a consent prompt for an application you have integrated with Azure AD that you did not expect
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
ms.openlocfilehash: d7121d439cc13bde907ec569a6fda3705d3a7491
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549777"
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="7293f-103">Unexpected consent prompt when signing in to an application</span><span class="sxs-lookup"><span data-stu-id="7293f-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="7293f-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span><span class="sxs-lookup"><span data-stu-id="7293f-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="7293f-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span><span class="sxs-lookup"><span data-stu-id="7293f-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="7293f-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span><span class="sxs-lookup"><span data-stu-id="7293f-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="7293f-107">Scenarios in which users see consent prompts</span><span class="sxs-lookup"><span data-stu-id="7293f-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="7293f-108">Additional prompts can be expected in various scenarios:</span><span class="sxs-lookup"><span data-stu-id="7293f-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="7293f-109">The set of permissions required by the application have changed.</span><span class="sxs-lookup"><span data-stu-id="7293f-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="7293f-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span><span class="sxs-lookup"><span data-stu-id="7293f-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="7293f-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span><span class="sxs-lookup"><span data-stu-id="7293f-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="7293f-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span><span class="sxs-lookup"><span data-stu-id="7293f-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="7293f-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span><span class="sxs-lookup"><span data-stu-id="7293f-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="7293f-114">Consent was revoked after being granted initially.</span><span class="sxs-lookup"><span data-stu-id="7293f-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="7293f-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span><span class="sxs-lookup"><span data-stu-id="7293f-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7293f-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7293f-116">Next steps</span></span>

-   [<span data-ttu-id="7293f-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span><span class="sxs-lookup"><span data-stu-id="7293f-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="7293f-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span><span class="sxs-lookup"><span data-stu-id="7293f-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


