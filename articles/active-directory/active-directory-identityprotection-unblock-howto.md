---
title: Azure Active Directory Identity Protection - How to unblock users | Microsoft Docs
description: Learn how unblock users that were blocked by an Azure Active Directory Identity Protection policy.
services: active-directory
keywords: azure active directory identity protection, unblock user
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: f0df3c003589b3ba9d882bc32ddbef9dd30e8d52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549380"
---
# <a name="azure-active-directory-identity-protection---how-to-unblock-users"></a><span data-ttu-id="8c81b-104">Azure Active Directory Identity Protection - How to unblock users</span><span class="sxs-lookup"><span data-stu-id="8c81b-104">Azure Active Directory Identity Protection - How to unblock users</span></span>
<span data-ttu-id="8c81b-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span><span class="sxs-lookup"><span data-stu-id="8c81b-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span></span> <span data-ttu-id="8c81b-106">Typically, a blocked user contacts help desk to become unblocked.</span><span class="sxs-lookup"><span data-stu-id="8c81b-106">Typically, a blocked user contacts help desk to become unblocked.</span></span> <span data-ttu-id="8c81b-107">This topics explains the steps you can perform to unblock a blocked user.</span><span class="sxs-lookup"><span data-stu-id="8c81b-107">This topics explains the steps you can perform to unblock a blocked user.</span></span>

## <a name="determine-the-reason-for-blocking"></a><span data-ttu-id="8c81b-108">Determine the reason for blocking</span><span class="sxs-lookup"><span data-stu-id="8c81b-108">Determine the reason for blocking</span></span>
<span data-ttu-id="8c81b-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span><span class="sxs-lookup"><span data-stu-id="8c81b-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span></span>
<span data-ttu-id="8c81b-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span><span class="sxs-lookup"><span data-stu-id="8c81b-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="8c81b-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span><span class="sxs-lookup"><span data-stu-id="8c81b-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span></span>

| <span data-ttu-id="8c81b-112">Policy</span><span class="sxs-lookup"><span data-stu-id="8c81b-112">Policy</span></span> | <span data-ttu-id="8c81b-113">User dialog</span><span class="sxs-lookup"><span data-stu-id="8c81b-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="8c81b-114">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="8c81b-114">Sign-in risk</span></span> |![Blocked sign-in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-unblock-howto/02.png) |
| <span data-ttu-id="8c81b-116">User risk</span><span class="sxs-lookup"><span data-stu-id="8c81b-116">User risk</span></span> |![Blocked account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-unblock-howto/104.png) |

<span data-ttu-id="8c81b-118">A user that is blocked by:</span><span class="sxs-lookup"><span data-stu-id="8c81b-118">A user that is blocked by:</span></span>

* <span data-ttu-id="8c81b-119">A sign-in risk policy is also known as suspicious sign-in</span><span class="sxs-lookup"><span data-stu-id="8c81b-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="8c81b-120">A user risk policy is also known as an account at risk</span><span class="sxs-lookup"><span data-stu-id="8c81b-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="8c81b-121">Unblocking suspicious sign-ins</span><span class="sxs-lookup"><span data-stu-id="8c81b-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="8c81b-122">To unblock a suspicious sign-in, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="8c81b-122">To unblock a suspicious sign-in, you have the following options:</span></span>

1. <span data-ttu-id="8c81b-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span><span class="sxs-lookup"><span data-stu-id="8c81b-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="8c81b-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span><span class="sxs-lookup"><span data-stu-id="8c81b-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="8c81b-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span><span class="sxs-lookup"><span data-stu-id="8c81b-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="8c81b-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="8c81b-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
3. <span data-ttu-id="8c81b-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span><span class="sxs-lookup"><span data-stu-id="8c81b-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="8c81b-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="8c81b-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="8c81b-129">Unblocking accounts at risk</span><span class="sxs-lookup"><span data-stu-id="8c81b-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="8c81b-130">To unblock an account at risk, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="8c81b-130">To unblock an account at risk, you have the following options:</span></span>

1. <span data-ttu-id="8c81b-131">**Reset password** - You can reset the user's password.</span><span class="sxs-lookup"><span data-stu-id="8c81b-131">**Reset password** - You can reset the user's password.</span></span> <span data-ttu-id="8c81b-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span><span class="sxs-lookup"><span data-stu-id="8c81b-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span></span>
2. <span data-ttu-id="8c81b-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span><span class="sxs-lookup"><span data-stu-id="8c81b-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="8c81b-134">You can reduce a user's risk level by manually closing reported risk events.</span><span class="sxs-lookup"><span data-stu-id="8c81b-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="8c81b-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="8c81b-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="8c81b-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span><span class="sxs-lookup"><span data-stu-id="8c81b-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="8c81b-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="8c81b-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
4. <span data-ttu-id="8c81b-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span><span class="sxs-lookup"><span data-stu-id="8c81b-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="8c81b-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="8c81b-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c81b-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c81b-140">Next steps</span></span>
 <span data-ttu-id="8c81b-141">Do you want to know more about Azure AD Identity Protection?</span><span class="sxs-lookup"><span data-stu-id="8c81b-141">Do you want to know more about Azure AD Identity Protection?</span></span> <span data-ttu-id="8c81b-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="8c81b-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>


