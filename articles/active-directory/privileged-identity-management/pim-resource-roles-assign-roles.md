---
title: Assign Azure resource roles in PIM | Microsoft Docs
description: Learn how to assign Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 08/30/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 7b82be6cdc8b64595c11eef84e8071fad9c07191
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966990"
---
# <a name="assign-azure-resource-roles-in-pim"></a><span data-ttu-id="0c4ec-103">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="0c4ec-103">Assign Azure resource roles in PIM</span></span>

<span data-ttu-id="0c4ec-104">Azure AD PIM can manage the built-in Azure resource roles, as well as custom roles, including (but not limited to):</span><span class="sxs-lookup"><span data-stu-id="0c4ec-104">Azure AD PIM can manage the built-in Azure resource roles, as well as custom roles, including (but not limited to):</span></span>

- <span data-ttu-id="0c4ec-105">Owner</span><span class="sxs-lookup"><span data-stu-id="0c4ec-105">Owner</span></span>
- <span data-ttu-id="0c4ec-106">User Access Administrator</span><span class="sxs-lookup"><span data-stu-id="0c4ec-106">User Access Administrator</span></span>
- <span data-ttu-id="0c4ec-107">Contributor</span><span class="sxs-lookup"><span data-stu-id="0c4ec-107">Contributor</span></span>
- <span data-ttu-id="0c4ec-108">Security Admin</span><span class="sxs-lookup"><span data-stu-id="0c4ec-108">Security Admin</span></span>
- <span data-ttu-id="0c4ec-109">Security Manager, and more</span><span class="sxs-lookup"><span data-stu-id="0c4ec-109">Security Manager, and more</span></span>

>[!NOTE]
<span data-ttu-id="0c4ec-110">Users or members of a group assigned to the Owner or User Access Administrator roles, and Global Administrators that enable subscription management in Azure AD are Resource Administrators.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-110">Users or members of a group assigned to the Owner or User Access Administrator roles, and Global Administrators that enable subscription management in Azure AD are Resource Administrators.</span></span> <span data-ttu-id="0c4ec-111">These administrators may assign roles, configure role settings, and review access using PIM for Azure Resources.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-111">These administrators may assign roles, configure role settings, and review access using PIM for Azure Resources.</span></span> <span data-ttu-id="0c4ec-112">View the list of [built-in roles for Azure resources](../../role-based-access-control/built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ec-112">View the list of [built-in roles for Azure resources](../../role-based-access-control/built-in-roles.md).</span></span>

## <a name="assign-a-role"></a><span data-ttu-id="0c4ec-113">Assign a role</span><span class="sxs-lookup"><span data-stu-id="0c4ec-113">Assign a role</span></span>

<span data-ttu-id="0c4ec-114">Follow these steps to make a user eligible for an Azure resource role.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-114">Follow these steps to make a user eligible for an Azure resource role.</span></span>

1. <span data-ttu-id="0c4ec-115">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-115">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span></span>

    <span data-ttu-id="0c4ec-116">For information about how to grant another administrator access to manage PIM, see [Grant access to other administrators to manage PIM](pim-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ec-116">For information about how to grant another administrator access to manage PIM, see [Grant access to other administrators to manage PIM](pim-how-to-give-access-to-pim.md).</span></span>

1. <span data-ttu-id="0c4ec-117">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-117">Open **Azure AD Privileged Identity Management**.</span></span>

    <span data-ttu-id="0c4ec-118">If you haven't started PIM in the Azure portal yet, go to [Start using PIM](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ec-118">If you haven't started PIM in the Azure portal yet, go to [Start using PIM](pim-getting-started.md).</span></span>

1. <span data-ttu-id="0c4ec-119">Click **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-119">Click **Azure resources**.</span></span>

1. <span data-ttu-id="0c4ec-120">Use the **Resource filter** to filter the list of managed resources.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-120">Use the **Resource filter** to filter the list of managed resources.</span></span>

    ![List of Azure resources to manage](./media/pim-resource-roles-assign-roles/resources-list.png)

1. <span data-ttu-id="0c4ec-122">Click the resource you want to manage, such as a subscription or management group.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-122">Click the resource you want to manage, such as a subscription or management group.</span></span>

1. <span data-ttu-id="0c4ec-123">Under Manage, click **Roles** to see the list of roles for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-123">Under Manage, click **Roles** to see the list of roles for Azure resources.</span></span>

    ![Azure resources roles](./media/pim-resource-roles-assign-roles/resources-roles.png)

1. <span data-ttu-id="0c4ec-125">Click **Add member** to open the New assignment pane.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-125">Click **Add member** to open the New assignment pane.</span></span>

1. <span data-ttu-id="0c4ec-126">Click **Select a role** to open the Select a role pane.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-126">Click **Select a role** to open the Select a role pane.</span></span>

    ![New assignment pane](./media/pim-resource-roles-assign-roles/resources-select-role.png)

1. <span data-ttu-id="0c4ec-128">Click a role you want to assign and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-128">Click a role you want to assign and then click **Select**.</span></span>

    <span data-ttu-id="0c4ec-129">The Select a member or group pane opens.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-129">The Select a member or group pane opens.</span></span>

1. <span data-ttu-id="0c4ec-130">Click a member or group you want to assign to the role and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-130">Click a member or group you want to assign to the role and then click **Select**.</span></span>

    ![Select a member or group pane](./media/pim-resource-roles-assign-roles/resources-select-member-or-group.png)

    <span data-ttu-id="0c4ec-132">The Membership settings pane opens.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-132">The Membership settings pane opens.</span></span>

1. <span data-ttu-id="0c4ec-133">In the **Assignment type** list, select **Eligible** or **Active**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-133">In the **Assignment type** list, select **Eligible** or **Active**.</span></span>

    ![Memberships settings pane](./media/pim-resource-roles-assign-roles/resources-membership-settings-type.png)

    <span data-ttu-id="0c4ec-135">PIM for Azure resources provides two distinct assignment types:</span><span class="sxs-lookup"><span data-stu-id="0c4ec-135">PIM for Azure resources provides two distinct assignment types:</span></span>

    - <span data-ttu-id="0c4ec-136">**Eligible** assignments require the member of the role to perform an action to use the role.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-136">**Eligible** assignments require the member of the role to perform an action to use the role.</span></span> <span data-ttu-id="0c4ec-137">Actions might include performing a multi-factor authentication (MFA) check, providing a business justification, or requesting approval from designated approvers.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-137">Actions might include performing a multi-factor authentication (MFA) check, providing a business justification, or requesting approval from designated approvers.</span></span>

    - <span data-ttu-id="0c4ec-138">**Active** assignments don't require the member to perform any action to use the role.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-138">**Active** assignments don't require the member to perform any action to use the role.</span></span> <span data-ttu-id="0c4ec-139">Members assigned as active have the privileges assigned to the role at all times.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-139">Members assigned as active have the privileges assigned to the role at all times.</span></span>

1. <span data-ttu-id="0c4ec-140">If the assignment should be permanent (permanently eligible or permanently assigned), select the **Permanently** check box.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-140">If the assignment should be permanent (permanently eligible or permanently assigned), select the **Permanently** check box.</span></span>

    <span data-ttu-id="0c4ec-141">Depending on the role settings, the check box might not appear or might be unmodifiable.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-141">Depending on the role settings, the check box might not appear or might be unmodifiable.</span></span>

1. <span data-ttu-id="0c4ec-142">To specify a specific assignment duration, clear the check box and modify the start and/or end date and time boxes.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-142">To specify a specific assignment duration, clear the check box and modify the start and/or end date and time boxes.</span></span>

    ![Memberships settings - date and time](./media/pim-resource-roles-assign-roles/resources-membership-settings-date.png)

1. <span data-ttu-id="0c4ec-144">When finished, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-144">When finished, click **Done**.</span></span>

    ![New assignment - Add](./media/pim-resource-roles-assign-roles/resources-new-assignment-add.png)

1. <span data-ttu-id="0c4ec-146">To create the new role assignment, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-146">To create the new role assignment, click **Add**.</span></span> <span data-ttu-id="0c4ec-147">A notification of the status is displayed.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-147">A notification of the status is displayed.</span></span>

    ![New assignment - Notification](./media/pim-resource-roles-assign-roles/resources-new-assignment-notification.png)

## <a name="update-or-remove-an-existing-role-assignment"></a><span data-ttu-id="0c4ec-149">Update or remove an existing role assignment</span><span class="sxs-lookup"><span data-stu-id="0c4ec-149">Update or remove an existing role assignment</span></span>

<span data-ttu-id="0c4ec-150">Follow these steps to update or remove an existing role assignment.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-150">Follow these steps to update or remove an existing role assignment.</span></span>

1. <span data-ttu-id="0c4ec-151">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-151">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="0c4ec-152">Click **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-152">Click **Azure resources**.</span></span>

1. <span data-ttu-id="0c4ec-153">Click the resource you want to manage, such as a subscription or management group.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-153">Click the resource you want to manage, such as a subscription or management group.</span></span>

1. <span data-ttu-id="0c4ec-154">Under Manage, click **Roles** to see the list of roles for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-154">Under Manage, click **Roles** to see the list of roles for Azure resources.</span></span>

    ![Azure resource roles - Select role](./media/pim-resource-roles-assign-roles/resources-update-select-role.png)

1. <span data-ttu-id="0c4ec-156">Click the role that you want to update or remove.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-156">Click the role that you want to update or remove.</span></span>

1. <span data-ttu-id="0c4ec-157">Find the role assignment on the **Eligible roles** or **Active roles** tabs.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-157">Find the role assignment on the **Eligible roles** or **Active roles** tabs.</span></span>

    ![Update or remove role assignment](./media/pim-resource-roles-assign-roles/resources-update-remove.png)

1. <span data-ttu-id="0c4ec-159">Click **Update** or **Remove** to update or remove the role assignment.</span><span class="sxs-lookup"><span data-stu-id="0c4ec-159">Click **Update** or **Remove** to update or remove the role assignment.</span></span>

    <span data-ttu-id="0c4ec-160">For information about extending a role assignment, see [Extend or renew Azure resource roles in PIM](pim-resource-roles-renew-extend.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ec-160">For information about extending a role assignment, see [Extend or renew Azure resource roles in PIM](pim-resource-roles-renew-extend.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c4ec-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c4ec-161">Next steps</span></span>

- [<span data-ttu-id="0c4ec-162">Extend or renew Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="0c4ec-162">Extend or renew Azure resource roles in PIM</span></span>](pim-resource-roles-renew-extend.md)
- [<span data-ttu-id="0c4ec-163">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="0c4ec-163">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
- [<span data-ttu-id="0c4ec-164">Assign Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="0c4ec-164">Assign Azure AD directory roles in PIM</span></span>](pim-how-to-add-role-to-user.md)
