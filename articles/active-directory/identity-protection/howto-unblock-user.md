---
title: Azure Active Directory Identity Protection - How to unblock users | Microsoft Docs
description: Learn how unblock users that were blocked by an Azure Active Directory Identity Protection policy.
services: active-directory
keywords: azure active directory identity protection, unblock user
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 1bfc70680ecef2ee4fe162f81aac71430c773740
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967128"
---
# <a name="azure-active-directory-identity-protection---how-to-unblock-users"></a><span data-ttu-id="e2e2b-104">Azure Active Directory Identity Protection - How to unblock users</span><span class="sxs-lookup"><span data-stu-id="e2e2b-104">Azure Active Directory Identity Protection - How to unblock users</span></span>
<span data-ttu-id="e2e2b-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span></span> <span data-ttu-id="e2e2b-106">Typically, a blocked user contacts help desk to become unblocked.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-106">Typically, a blocked user contacts help desk to become unblocked.</span></span> <span data-ttu-id="e2e2b-107">This article explains the steps you can perform to unblock a blocked user.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-107">This article explains the steps you can perform to unblock a blocked user.</span></span>

## <a name="determine-the-reason-for-blocking"></a><span data-ttu-id="e2e2b-108">Determine the reason for blocking</span><span class="sxs-lookup"><span data-stu-id="e2e2b-108">Determine the reason for blocking</span></span>
<span data-ttu-id="e2e2b-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span></span>
<span data-ttu-id="e2e2b-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="e2e2b-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span><span class="sxs-lookup"><span data-stu-id="e2e2b-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span></span>

| <span data-ttu-id="e2e2b-112">Policy</span><span class="sxs-lookup"><span data-stu-id="e2e2b-112">Policy</span></span> | <span data-ttu-id="e2e2b-113">User dialog</span><span class="sxs-lookup"><span data-stu-id="e2e2b-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="e2e2b-114">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="e2e2b-114">Sign-in risk</span></span> |![Blocked sign-in](./media/howto-unblock-user/02.png) |
| <span data-ttu-id="e2e2b-116">User risk</span><span class="sxs-lookup"><span data-stu-id="e2e2b-116">User risk</span></span> |![Blocked account](./media/howto-unblock-user/104.png) |

<span data-ttu-id="e2e2b-118">A user that is blocked by:</span><span class="sxs-lookup"><span data-stu-id="e2e2b-118">A user that is blocked by:</span></span>

* <span data-ttu-id="e2e2b-119">A sign-in risk policy is also known as suspicious sign-in</span><span class="sxs-lookup"><span data-stu-id="e2e2b-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="e2e2b-120">A user risk policy is also known as an account at risk</span><span class="sxs-lookup"><span data-stu-id="e2e2b-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="e2e2b-121">Unblocking suspicious sign-ins</span><span class="sxs-lookup"><span data-stu-id="e2e2b-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="e2e2b-122">To unblock a suspicious sign-in, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="e2e2b-122">To unblock a suspicious sign-in, you have the following options:</span></span>

1. <span data-ttu-id="e2e2b-123">**Sign in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-123">**Sign in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="e2e2b-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="e2e2b-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="e2e2b-126">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-126">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>
3. <span data-ttu-id="e2e2b-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="e2e2b-128">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-128">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="e2e2b-129">Unblocking accounts at risk</span><span class="sxs-lookup"><span data-stu-id="e2e2b-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="e2e2b-130">To unblock an account at risk, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="e2e2b-130">To unblock an account at risk, you have the following options:</span></span>

1. <span data-ttu-id="e2e2b-131">**Reset password** - You can reset the user's password.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-131">**Reset password** - You can reset the user's password.</span></span> <span data-ttu-id="e2e2b-132">For more information, see [manual secure password reset](overview.md#manual-secure-password-reset).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-132">For more information, see [manual secure password reset](overview.md#manual-secure-password-reset).</span></span>
2. <span data-ttu-id="e2e2b-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="e2e2b-134">You can reduce a user's risk level by manually closing reported risk events.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="e2e2b-135">For more information, see [closing risk events manually](overview.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-135">For more information, see [closing risk events manually](overview.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="e2e2b-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="e2e2b-137">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-137">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>
4. <span data-ttu-id="e2e2b-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span><span class="sxs-lookup"><span data-stu-id="e2e2b-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="e2e2b-139">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-139">For more information, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e2b-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2e2b-140">Next steps</span></span>
 
<span data-ttu-id="e2e2b-141">Do you want to know more about Azure AD Identity Protection?</span><span class="sxs-lookup"><span data-stu-id="e2e2b-141">Do you want to know more about Azure AD Identity Protection?</span></span> <span data-ttu-id="e2e2b-142">Check out [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e2e2b-142">Check out [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>
