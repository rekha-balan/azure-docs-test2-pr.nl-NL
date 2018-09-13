---
title: Assign Azure AD directory roles in PIM | Microsoft Docs
description: Learn how to assign Azure AD directory roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 07/23/2018
ms.author: rolyon
ms.openlocfilehash: 33bfe28bf612c47c9f42345dabccc017337c3d45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856300"
---
# <a name="assign-azure-ad-directory-roles-in-pim"></a><span data-ttu-id="3c258-103">Assign Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="3c258-103">Assign Azure AD directory roles in PIM</span></span>

<span data-ttu-id="3c258-104">With Azure Active Directory (Azure AD), a Global Administrator can make **permanent** directory role assignments.</span><span class="sxs-lookup"><span data-stu-id="3c258-104">With Azure Active Directory (Azure AD), a Global Administrator can make **permanent** directory role assignments.</span></span> <span data-ttu-id="3c258-105">These role assignments can be created using the [Azure portal](../users-groups-roles/directory-assign-admin-roles.md) or using [PowerShell commands](/powershell/module/azuread#directory_roles).</span><span class="sxs-lookup"><span data-stu-id="3c258-105">These role assignments can be created using the [Azure portal](../users-groups-roles/directory-assign-admin-roles.md) or using [PowerShell commands](/powershell/module/azuread#directory_roles).</span></span>

<span data-ttu-id="3c258-106">The Azure AD Privileged Identity Management (PIM) service also allows privileged role administrators to make permanent directory role assignments.</span><span class="sxs-lookup"><span data-stu-id="3c258-106">The Azure AD Privileged Identity Management (PIM) service also allows privileged role administrators to make permanent directory role assignments.</span></span> <span data-ttu-id="3c258-107">Additionally, privileged role administrators can make users **eligible** for directory roles.</span><span class="sxs-lookup"><span data-stu-id="3c258-107">Additionally, privileged role administrators can make users **eligible** for directory roles.</span></span> <span data-ttu-id="3c258-108">An eligible administrator can activate the role when they need it, and then their permissions expire once they're done.</span><span class="sxs-lookup"><span data-stu-id="3c258-108">An eligible administrator can activate the role when they need it, and then their permissions expire once they're done.</span></span> <span data-ttu-id="3c258-109">For information about the roles that you can manage using PIM, see [Azure AD directory roles you can manage in PIM](pim-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3c258-109">For information about the roles that you can manage using PIM, see [Azure AD directory roles you can manage in PIM](pim-roles.md).</span></span>

## <a name="make-a-user-eligible-for-a-role"></a><span data-ttu-id="3c258-110">Make a user eligible for a role</span><span class="sxs-lookup"><span data-stu-id="3c258-110">Make a user eligible for a role</span></span>

<span data-ttu-id="3c258-111">Follow these steps to make a user eligible for an Azure AD directory role.</span><span class="sxs-lookup"><span data-stu-id="3c258-111">Follow these steps to make a user eligible for an Azure AD directory role.</span></span>

1. <span data-ttu-id="3c258-112">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="3c258-112">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span></span>

    <span data-ttu-id="3c258-113">For information about how to grant another administrator access to manage PIM, see [Grant access to other administrators to manage PIM](pim-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="3c258-113">For information about how to grant another administrator access to manage PIM, see [Grant access to other administrators to manage PIM](pim-how-to-give-access-to-pim.md).</span></span>

1. <span data-ttu-id="3c258-114">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="3c258-114">Open **Azure AD Privileged Identity Management**.</span></span>

    <span data-ttu-id="3c258-115">If you haven't started PIM in the Azure portal yet, go to [Start using PIM](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c258-115">If you haven't started PIM in the Azure portal yet, go to [Start using PIM](pim-getting-started.md).</span></span>

1. <span data-ttu-id="3c258-116">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="3c258-116">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="3c258-117">Click **Roles** or **Members**.</span><span class="sxs-lookup"><span data-stu-id="3c258-117">Click **Roles** or **Members**.</span></span>

    ![Azure AD directory roles](./media/pim-how-to-add-role-to-user/pim-directory-roles.png)

1. <span data-ttu-id="3c258-119">Click **Add member** to open Add managed members.</span><span class="sxs-lookup"><span data-stu-id="3c258-119">Click **Add member** to open Add managed members.</span></span>

1. <span data-ttu-id="3c258-120">Click **Select a role**, click a role you want to manage, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="3c258-120">Click **Select a role**, click a role you want to manage, and then click **Select**.</span></span>

    ![Select a role](./media/pim-how-to-add-role-to-user/pim-select-a-role.png)

1. <span data-ttu-id="3c258-122">Click **Select members**, select the users you want to assign to the role, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="3c258-122">Click **Select members**, select the users you want to assign to the role, and then click **Select**.</span></span>

    ![Select a role](./media/pim-how-to-add-role-to-user/pim-select-members.png)

1. <span data-ttu-id="3c258-124">In Add managed members, click **OK** to add the user to the role.</span><span class="sxs-lookup"><span data-stu-id="3c258-124">In Add managed members, click **OK** to add the user to the role.</span></span>

1. <span data-ttu-id="3c258-125">In the list of roles, click the role you just assigned to see the list of members.</span><span class="sxs-lookup"><span data-stu-id="3c258-125">In the list of roles, click the role you just assigned to see the list of members.</span></span>

     <span data-ttu-id="3c258-126">When the role is assigned, the user you selected will appear in the members list as **Eligible** for the role.</span><span class="sxs-lookup"><span data-stu-id="3c258-126">When the role is assigned, the user you selected will appear in the members list as **Eligible** for the role.</span></span>

    ![User eligible for a role](./media/pim-how-to-add-role-to-user/pim-directory-role-eligible.png)

1. <span data-ttu-id="3c258-128">Now that the user is eligible for the role, let them know that they can activate it according to the instructions in [Activate my Azure AD directory roles in PIM](pim-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="3c258-128">Now that the user is eligible for the role, let them know that they can activate it according to the instructions in [Activate my Azure AD directory roles in PIM](pim-how-to-activate-role.md).</span></span>

    <span data-ttu-id="3c258-129">Eligible administrators are asked to register for Azure Multi-Factor Authentication (MFA) during activation.</span><span class="sxs-lookup"><span data-stu-id="3c258-129">Eligible administrators are asked to register for Azure Multi-Factor Authentication (MFA) during activation.</span></span> <span data-ttu-id="3c258-130">If a user cannot register for MFA, or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span><span class="sxs-lookup"><span data-stu-id="3c258-130">If a user cannot register for MFA, or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span>

## <a name="make-a-role-assignment-permanent"></a><span data-ttu-id="3c258-131">Make a role assignment permanent</span><span class="sxs-lookup"><span data-stu-id="3c258-131">Make a role assignment permanent</span></span>

<span data-ttu-id="3c258-132">By default, new users are only eligible for a directory role.</span><span class="sxs-lookup"><span data-stu-id="3c258-132">By default, new users are only eligible for a directory role.</span></span> <span data-ttu-id="3c258-133">Follow these steps if you want to make a role assignment permanent.</span><span class="sxs-lookup"><span data-stu-id="3c258-133">Follow these steps if you want to make a role assignment permanent.</span></span>

1. <span data-ttu-id="3c258-134">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="3c258-134">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="3c258-135">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="3c258-135">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="3c258-136">Click **Members**.</span><span class="sxs-lookup"><span data-stu-id="3c258-136">Click **Members**.</span></span>

    ![List of members](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members.png)

1. <span data-ttu-id="3c258-138">Click an **Eligible** role that you want to make permanent.</span><span class="sxs-lookup"><span data-stu-id="3c258-138">Click an **Eligible** role that you want to make permanent.</span></span>

1. <span data-ttu-id="3c258-139">Click **More** and then click **Make perm**.</span><span class="sxs-lookup"><span data-stu-id="3c258-139">Click **More** and then click **Make perm**.</span></span>

    ![Make role assignment permanent](./media/pim-how-to-add-role-to-user/pim-make-perm.png)

    <span data-ttu-id="3c258-141">The role is now listed as **permanent**.</span><span class="sxs-lookup"><span data-stu-id="3c258-141">The role is now listed as **permanent**.</span></span>

    ![List of members with permanent change](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members-permanent.png)

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="3c258-143">Remove a user from a role</span><span class="sxs-lookup"><span data-stu-id="3c258-143">Remove a user from a role</span></span>

<span data-ttu-id="3c258-144">You can remove users from role assignments, but make sure there is always at least one user who is a permanent Global Administrator.</span><span class="sxs-lookup"><span data-stu-id="3c258-144">You can remove users from role assignments, but make sure there is always at least one user who is a permanent Global Administrator.</span></span> <span data-ttu-id="3c258-145">If you're not sure which users still need their role assignments, you can [start an access review for the role](pim-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="3c258-145">If you're not sure which users still need their role assignments, you can [start an access review for the role](pim-how-to-start-security-review.md).</span></span>

<span data-ttu-id="3c258-146">Follow these steps to remove a specific user from a directory role.</span><span class="sxs-lookup"><span data-stu-id="3c258-146">Follow these steps to remove a specific user from a directory role.</span></span>

1. <span data-ttu-id="3c258-147">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="3c258-147">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="3c258-148">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="3c258-148">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="3c258-149">Click **Members**.</span><span class="sxs-lookup"><span data-stu-id="3c258-149">Click **Members**.</span></span>

    ![List of members](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members.png)

1. <span data-ttu-id="3c258-151">Click a role assignment you want to remove.</span><span class="sxs-lookup"><span data-stu-id="3c258-151">Click a role assignment you want to remove.</span></span>

1. <span data-ttu-id="3c258-152">Click **More** and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="3c258-152">Click **More** and then click **Remove**.</span></span>

    ![Remove a role](./media/pim-how-to-add-role-to-user/pim-remove-role.png)

1. <span data-ttu-id="3c258-154">In the message that asks you to confirm, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3c258-154">In the message that asks you to confirm, click **Yes**.</span></span>

    ![Remove a role](./media/pim-how-to-add-role-to-user/pim-remove-role-confirm.png)

    <span data-ttu-id="3c258-156">The role assignment is removed.</span><span class="sxs-lookup"><span data-stu-id="3c258-156">The role assignment is removed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c258-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c258-157">Next steps</span></span>

- [<span data-ttu-id="3c258-158">Configure Azure AD directory role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="3c258-158">Configure Azure AD directory role settings in PIM</span></span>](pim-how-to-change-default-settings.md)
- [<span data-ttu-id="3c258-159">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="3c258-159">Assign Azure resource roles in PIM</span></span>](pim-resource-roles-assign-roles.md)
