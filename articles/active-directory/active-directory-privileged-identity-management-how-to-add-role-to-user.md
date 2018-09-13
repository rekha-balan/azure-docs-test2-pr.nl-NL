---
title: How to add or remove a user role | Microsoft Docs
description: Learn how to add roles to privileged identities with the Azure Active Directory Privileged Identity Management application.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 289c6a61bc74d1e34f5bd176b8bb6ae624383d74
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564164"
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="4caa0-103">Azure AD Privileged Identity Management: How to add or remove a user role</span><span class="sxs-lookup"><span data-stu-id="4caa0-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="4caa0-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4caa0-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="4caa0-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span><span class="sxs-lookup"><span data-stu-id="4caa0-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="4caa0-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4caa0-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="4caa0-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span><span class="sxs-lookup"><span data-stu-id="4caa0-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="4caa0-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span><span class="sxs-lookup"><span data-stu-id="4caa0-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="4caa0-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span><span class="sxs-lookup"><span data-stu-id="4caa0-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="4caa0-110">Manage roles with PIM in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4caa0-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="4caa0-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span><span class="sxs-lookup"><span data-stu-id="4caa0-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="4caa0-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4caa0-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="4caa0-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span><span class="sxs-lookup"><span data-stu-id="4caa0-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="4caa0-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span><span class="sxs-lookup"><span data-stu-id="4caa0-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="4caa0-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="4caa0-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="4caa0-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="4caa0-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="4caa0-117">Add a user to a role</span><span class="sxs-lookup"><span data-stu-id="4caa0-117">Add a user to a role</span></span>
1. <span data-ttu-id="4caa0-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="4caa0-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="4caa0-119">Select **Manage privileged roles**.</span><span class="sxs-lookup"><span data-stu-id="4caa0-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="4caa0-120">In the **Role summary** table, select the role you want to manage.</span><span class="sxs-lookup"><span data-stu-id="4caa0-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="4caa0-121">In the role blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="4caa0-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="4caa0-122">Click **Select users** and search for the user on the **Select users** blade.</span><span class="sxs-lookup"><span data-stu-id="4caa0-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="4caa0-123">Select the user from the search results list, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="4caa0-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="4caa0-124">Click **OK** to save your selection.</span><span class="sxs-lookup"><span data-stu-id="4caa0-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="4caa0-125">The user you have selected will appear in the list as eligible for the role.</span><span class="sxs-lookup"><span data-stu-id="4caa0-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="4caa0-126">New users in a role are only eligible for the role by default.</span><span class="sxs-lookup"><span data-stu-id="4caa0-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="4caa0-127">If you want to make the role permanent, click the user in the list.</span><span class="sxs-lookup"><span data-stu-id="4caa0-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="4caa0-128">The user's information will appear in a new blade.</span><span class="sxs-lookup"><span data-stu-id="4caa0-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="4caa0-129">Select **Make perm** in the user information menu.</span><span class="sxs-lookup"><span data-stu-id="4caa0-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="4caa0-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span><span class="sxs-lookup"><span data-stu-id="4caa0-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="4caa0-131">Eligible admins are asked to register for MFA during activation.</span><span class="sxs-lookup"><span data-stu-id="4caa0-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="4caa0-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="4caa0-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="4caa0-133">Remove a user from a role</span><span class="sxs-lookup"><span data-stu-id="4caa0-133">Remove a user from a role</span></span>
<span data-ttu-id="4caa0-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span><span class="sxs-lookup"><span data-stu-id="4caa0-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="4caa0-135">Follow these steps to remove a specific user from a role:</span><span class="sxs-lookup"><span data-stu-id="4caa0-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="4caa0-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span><span class="sxs-lookup"><span data-stu-id="4caa0-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="4caa0-137">Click on the user in the user list.</span><span class="sxs-lookup"><span data-stu-id="4caa0-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="4caa0-138">Click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="4caa0-138">Click **Remove**.</span></span> <span data-ttu-id="4caa0-139">A message will ask you to confirm.</span><span class="sxs-lookup"><span data-stu-id="4caa0-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="4caa0-140">Click **Yes** to remove the role from the user.</span><span class="sxs-lookup"><span data-stu-id="4caa0-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="4caa0-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="4caa0-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4caa0-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="4caa0-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

