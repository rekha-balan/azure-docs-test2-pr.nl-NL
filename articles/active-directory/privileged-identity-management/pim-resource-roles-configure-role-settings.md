---
title: Configure Azure resource role settings in PIM | Microsoft Docs
description: Learn how to configure Azure resource role settings in Azure AD Privileged Identity Management (PIM).
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
ms.openlocfilehash: a4aecd276df8e5453f0c35d6290bbe8a8d156ffa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869335"
---
# <a name="configure-azure-resource-role-settings-in-pim"></a><span data-ttu-id="d36b1-103">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="d36b1-103">Configure Azure resource role settings in PIM</span></span>

<span data-ttu-id="d36b1-104">When you configure Azure resource role settings, you define the default settings that are applied to Azure resource role assignments in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="d36b1-104">When you configure Azure resource role settings, you define the default settings that are applied to Azure resource role assignments in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="d36b1-105">Use the following procedures to configure the approval workflow and specify who can approve or deny requests.</span><span class="sxs-lookup"><span data-stu-id="d36b1-105">Use the following procedures to configure the approval workflow and specify who can approve or deny requests.</span></span>

## <a name="open-role-settings"></a><span data-ttu-id="d36b1-106">Open role settings</span><span class="sxs-lookup"><span data-stu-id="d36b1-106">Open role settings</span></span>

<span data-ttu-id="d36b1-107">Follow these steps to open the settings for an Azure resource role.</span><span class="sxs-lookup"><span data-stu-id="d36b1-107">Follow these steps to open the settings for an Azure resource role.</span></span>

1. <span data-ttu-id="d36b1-108">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="d36b1-108">Sign in to [Azure portal](https://portal.azure.com/) with a user that is a member of the [Privileged Role Administrator](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) role.</span></span>

1. <span data-ttu-id="d36b1-109">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="d36b1-109">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="d36b1-110">Click **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="d36b1-110">Click **Azure resources**.</span></span>

1. <span data-ttu-id="d36b1-111">Click the resource you want to manage, such as a subscription or management group.</span><span class="sxs-lookup"><span data-stu-id="d36b1-111">Click the resource you want to manage, such as a subscription or management group.</span></span>

    ![List of Azure resources to manage](./media/pim-resource-roles-configure-role-settings/resources-list.png)

1. <span data-ttu-id="d36b1-113">Click **Role settings**.</span><span class="sxs-lookup"><span data-stu-id="d36b1-113">Click **Role settings**.</span></span>

    ![Role settings](./media/pim-resource-roles-configure-role-settings/resources-role-settings.png)

1. <span data-ttu-id="d36b1-115">Click the role whose settings you want to configure.</span><span class="sxs-lookup"><span data-stu-id="d36b1-115">Click the role whose settings you want to configure.</span></span>

    ![Role setting details](./media/pim-resource-roles-configure-role-settings/resources-role-setting-details.png)

1. <span data-ttu-id="d36b1-117">Click **Edit** to open the Role settings pane.</span><span class="sxs-lookup"><span data-stu-id="d36b1-117">Click **Edit** to open the Role settings pane.</span></span>

    ![Edit role settings](./media/pim-resource-roles-configure-role-settings/resources-role-settings-edit.png)

    <span data-ttu-id="d36b1-119">On the Role setting pane for each role, there are several settings you can configure.</span><span class="sxs-lookup"><span data-stu-id="d36b1-119">On the Role setting pane for each role, there are several settings you can configure.</span></span>

## <a name="assignment-duration"></a><span data-ttu-id="d36b1-120">Assignment duration</span><span class="sxs-lookup"><span data-stu-id="d36b1-120">Assignment duration</span></span>

<span data-ttu-id="d36b1-121">You can choose from two assignment duration options for each assignment type (eligible and active) when you configure settings for a role.</span><span class="sxs-lookup"><span data-stu-id="d36b1-121">You can choose from two assignment duration options for each assignment type (eligible and active) when you configure settings for a role.</span></span> <span data-ttu-id="d36b1-122">These options become the default maximum duration when a member is assigned to the role in PIM.</span><span class="sxs-lookup"><span data-stu-id="d36b1-122">These options become the default maximum duration when a member is assigned to the role in PIM.</span></span>

<span data-ttu-id="d36b1-123">You can choose one of these **eligible** assignment duration options:</span><span class="sxs-lookup"><span data-stu-id="d36b1-123">You can choose one of these **eligible** assignment duration options:</span></span>

| | |
| --- | --- |
| <span data-ttu-id="d36b1-124">**Allow permanent eligible assignment**</span><span class="sxs-lookup"><span data-stu-id="d36b1-124">**Allow permanent eligible assignment**</span></span> | <span data-ttu-id="d36b1-125">Resource administrators can assign permanent eligible membership.</span><span class="sxs-lookup"><span data-stu-id="d36b1-125">Resource administrators can assign permanent eligible membership.</span></span> |
| <span data-ttu-id="d36b1-126">**Expire eligible assignment after**</span><span class="sxs-lookup"><span data-stu-id="d36b1-126">**Expire eligible assignment after**</span></span> | <span data-ttu-id="d36b1-127">Resource administrators can require that all eligible assignments have a specified start and end date.</span><span class="sxs-lookup"><span data-stu-id="d36b1-127">Resource administrators can require that all eligible assignments have a specified start and end date.</span></span> |

<span data-ttu-id="d36b1-128">And, you can choose one of these **active** assignment duration options:</span><span class="sxs-lookup"><span data-stu-id="d36b1-128">And, you can choose one of these **active** assignment duration options:</span></span>

| | |
| --- | --- |
| <span data-ttu-id="d36b1-129">**Allow permanent active assignment**</span><span class="sxs-lookup"><span data-stu-id="d36b1-129">**Allow permanent active assignment**</span></span> | <span data-ttu-id="d36b1-130">Resource administrators can assign permanent active membership.</span><span class="sxs-lookup"><span data-stu-id="d36b1-130">Resource administrators can assign permanent active membership.</span></span> |
| <span data-ttu-id="d36b1-131">**Expire active assignment after**</span><span class="sxs-lookup"><span data-stu-id="d36b1-131">**Expire active assignment after**</span></span> | <span data-ttu-id="d36b1-132">Resource administrators can require that all active assignments have a specified start and end date.</span><span class="sxs-lookup"><span data-stu-id="d36b1-132">Resource administrators can require that all active assignments have a specified start and end date.</span></span> |

> [!NOTE] 
> <span data-ttu-id="d36b1-133">All assignments that have a specified end date can be renewed by resource administrators.</span><span class="sxs-lookup"><span data-stu-id="d36b1-133">All assignments that have a specified end date can be renewed by resource administrators.</span></span> <span data-ttu-id="d36b1-134">Also, members can initiate self-service requests to [extend or renew role assignments](pim-resource-roles-renew-extend.md).</span><span class="sxs-lookup"><span data-stu-id="d36b1-134">Also, members can initiate self-service requests to [extend or renew role assignments](pim-resource-roles-renew-extend.md).</span></span>

## <a name="require-multi-factor-authentication"></a><span data-ttu-id="d36b1-135">Require multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="d36b1-135">Require multi-factor authentication</span></span>

<span data-ttu-id="d36b1-136">PIM provides optional enforcement of Azure Multi-Factor Authentication (MFA) for two distinct scenarios.</span><span class="sxs-lookup"><span data-stu-id="d36b1-136">PIM provides optional enforcement of Azure Multi-Factor Authentication (MFA) for two distinct scenarios.</span></span>

### <a name="require-multi-factor-authentication-on-active-assignment"></a><span data-ttu-id="d36b1-137">Require Multi-Factor Authentication on active assignment</span><span class="sxs-lookup"><span data-stu-id="d36b1-137">Require Multi-Factor Authentication on active assignment</span></span>

<span data-ttu-id="d36b1-138">In some cases, you might want to assign a member to a role for a short duration (one day, for example).</span><span class="sxs-lookup"><span data-stu-id="d36b1-138">In some cases, you might want to assign a member to a role for a short duration (one day, for example).</span></span> <span data-ttu-id="d36b1-139">In this case, they don't need the assigned members to request activation.</span><span class="sxs-lookup"><span data-stu-id="d36b1-139">In this case, they don't need the assigned members to request activation.</span></span> <span data-ttu-id="d36b1-140">In this scenario, PIM cannot enforce MFA when the member uses their role assignment, since they are already active in the role from the moment they are assigned.</span><span class="sxs-lookup"><span data-stu-id="d36b1-140">In this scenario, PIM cannot enforce MFA when the member uses their role assignment, since they are already active in the role from the moment they are assigned.</span></span>

<span data-ttu-id="d36b1-141">To ensure that the resource administrator fulfilling the assignment is who they say they are, you can enforce MFA on active assignment by checking the **Require Multi-Factor Authentication on active assignment** box.</span><span class="sxs-lookup"><span data-stu-id="d36b1-141">To ensure that the resource administrator fulfilling the assignment is who they say they are, you can enforce MFA on active assignment by checking the **Require Multi-Factor Authentication on active assignment** box.</span></span>

### <a name="require-multi-factor-authentication-on-activation"></a><span data-ttu-id="d36b1-142">Require Multi-Factor Authentication on activation</span><span class="sxs-lookup"><span data-stu-id="d36b1-142">Require Multi-Factor Authentication on activation</span></span>

<span data-ttu-id="d36b1-143">You can require eligible members of a role to run MFA before they can activate.</span><span class="sxs-lookup"><span data-stu-id="d36b1-143">You can require eligible members of a role to run MFA before they can activate.</span></span> <span data-ttu-id="d36b1-144">This process ensures that the user who is requesting activation is who they say they are with reasonable certainty.</span><span class="sxs-lookup"><span data-stu-id="d36b1-144">This process ensures that the user who is requesting activation is who they say they are with reasonable certainty.</span></span> <span data-ttu-id="d36b1-145">Enforcing this option protects critical resources in situations when the user account might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="d36b1-145">Enforcing this option protects critical resources in situations when the user account might have been compromised.</span></span>

<span data-ttu-id="d36b1-146">To require an eligible member to run MFA before activation, check the **Require Multi-Factor Authentication on activation** box.</span><span class="sxs-lookup"><span data-stu-id="d36b1-146">To require an eligible member to run MFA before activation, check the **Require Multi-Factor Authentication on activation** box.</span></span>

<span data-ttu-id="d36b1-147">For more information, see [Multi-factor authentication (MFA) and PIM](pim-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="d36b1-147">For more information, see [Multi-factor authentication (MFA) and PIM](pim-how-to-require-mfa.md).</span></span>

## <a name="activation-maximum-duration"></a><span data-ttu-id="d36b1-148">Activation maximum duration</span><span class="sxs-lookup"><span data-stu-id="d36b1-148">Activation maximum duration</span></span>

<span data-ttu-id="d36b1-149">Use the **Activation maximum duration** slider to set the maximum time, in hours, that a role stays active before it expires.</span><span class="sxs-lookup"><span data-stu-id="d36b1-149">Use the **Activation maximum duration** slider to set the maximum time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="d36b1-150">This value can be between 1 and 24 hours.</span><span class="sxs-lookup"><span data-stu-id="d36b1-150">This value can be between 1 and 24 hours.</span></span>

## <a name="require-justification"></a><span data-ttu-id="d36b1-151">Require justification</span><span class="sxs-lookup"><span data-stu-id="d36b1-151">Require justification</span></span>

<span data-ttu-id="d36b1-152">You can require that members enter a justification on active assignment or when they activate.</span><span class="sxs-lookup"><span data-stu-id="d36b1-152">You can require that members enter a justification on active assignment or when they activate.</span></span> <span data-ttu-id="d36b1-153">To require justification, check the **Require justification on active assignment** box or the **Require justification on activation** box.</span><span class="sxs-lookup"><span data-stu-id="d36b1-153">To require justification, check the **Require justification on active assignment** box or the **Require justification on activation** box.</span></span>

## <a name="require-approval-to-activate"></a><span data-ttu-id="d36b1-154">Require approval to activate</span><span class="sxs-lookup"><span data-stu-id="d36b1-154">Require approval to activate</span></span>

<span data-ttu-id="d36b1-155">If you want to require approval to activate a role, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="d36b1-155">If you want to require approval to activate a role, follow these steps.</span></span>

1. <span data-ttu-id="d36b1-156">Check the **Require approval to activate** check box.</span><span class="sxs-lookup"><span data-stu-id="d36b1-156">Check the **Require approval to activate** check box.</span></span>

1. <span data-ttu-id="d36b1-157">Click **Select approvers** to open the Select a member or group pane.</span><span class="sxs-lookup"><span data-stu-id="d36b1-157">Click **Select approvers** to open the Select a member or group pane.</span></span>

    ![Select a member or group](./media/pim-resource-roles-configure-role-settings/resources-role-settings-select-approvers.png)

1. <span data-ttu-id="d36b1-159">Select at least one member or group and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="d36b1-159">Select at least one member or group and then click **Select**.</span></span> <span data-ttu-id="d36b1-160">You can add any combination of members and groups.</span><span class="sxs-lookup"><span data-stu-id="d36b1-160">You can add any combination of members and groups.</span></span> <span data-ttu-id="d36b1-161">You must select at least one approver.</span><span class="sxs-lookup"><span data-stu-id="d36b1-161">You must select at least one approver.</span></span> <span data-ttu-id="d36b1-162">There are no default approvers.</span><span class="sxs-lookup"><span data-stu-id="d36b1-162">There are no default approvers.</span></span>

    <span data-ttu-id="d36b1-163">Your selections will appear in the list of selected approvers.</span><span class="sxs-lookup"><span data-stu-id="d36b1-163">Your selections will appear in the list of selected approvers.</span></span>

1. <span data-ttu-id="d36b1-164">Once you have specified your all your role settings, click **Update** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="d36b1-164">Once you have specified your all your role settings, click **Update** to save your changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d36b1-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="d36b1-165">Next steps</span></span>

- [<span data-ttu-id="d36b1-166">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d36b1-166">Assign Azure resource roles in PIM</span></span>](pim-resource-roles-assign-roles.md)
- [<span data-ttu-id="d36b1-167">Configure security alerts for Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="d36b1-167">Configure security alerts for Azure resource roles in PIM</span></span>](pim-resource-roles-configure-alerts.md)
