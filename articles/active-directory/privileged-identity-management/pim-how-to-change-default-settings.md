---
title: Configure Azure AD directory role settings in PIM | Microsoft Docs
description: Learn how to configure Azure AD directory role settings in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 08/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 2d7226f18eb922eaba3c8184656560c33202ef56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868251"
---
# <a name="configure-azure-ad-directory-role-settings-in-pim"></a><span data-ttu-id="6393f-103">Configure Azure AD directory role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="6393f-103">Configure Azure AD directory role settings in PIM</span></span>

<span data-ttu-id="6393f-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span><span class="sxs-lookup"><span data-stu-id="6393f-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="open-role-settings"></a><span data-ttu-id="6393f-105">Open role settings</span><span class="sxs-lookup"><span data-stu-id="6393f-105">Open role settings</span></span>

<span data-ttu-id="6393f-106">Follow these steps to open the settings for an Azure AD directory role.</span><span class="sxs-lookup"><span data-stu-id="6393f-106">Follow these steps to open the settings for an Azure AD directory role.</span></span>

1. <span data-ttu-id="6393f-107">Open **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="6393f-107">Open **Azure AD Privileged Identity Management**.</span></span>

1. <span data-ttu-id="6393f-108">Click **Azure AD directory roles**.</span><span class="sxs-lookup"><span data-stu-id="6393f-108">Click **Azure AD directory roles**.</span></span>

1. <span data-ttu-id="6393f-109">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="6393f-109">Click **Settings**.</span></span>

    ![Azure AD directory roles - Settings](./media/pim-how-to-change-default-settings/pim-directory-roles-settings.png)

1. <span data-ttu-id="6393f-111">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="6393f-111">Click **Roles**.</span></span>

1. <span data-ttu-id="6393f-112">Click the role whose settings you want to configure.</span><span class="sxs-lookup"><span data-stu-id="6393f-112">Click the role whose settings you want to configure.</span></span>

    ![Azure AD directory roles - Settings Roles](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-role.png)

    <span data-ttu-id="6393f-114">On the settings page for each role, there are several settings you can configure.</span><span class="sxs-lookup"><span data-stu-id="6393f-114">On the settings page for each role, there are several settings you can configure.</span></span> <span data-ttu-id="6393f-115">These settings only affect users who are **eligible** assignments, not **permanent** assignments.</span><span class="sxs-lookup"><span data-stu-id="6393f-115">These settings only affect users who are **eligible** assignments, not **permanent** assignments.</span></span>

## <a name="activations"></a><span data-ttu-id="6393f-116">Activations</span><span class="sxs-lookup"><span data-stu-id="6393f-116">Activations</span></span>

<span data-ttu-id="6393f-117">Use the **Activations** slider to set the maximum time, in hours, that a role stays active before it expires.</span><span class="sxs-lookup"><span data-stu-id="6393f-117">Use the **Activations** slider to set the maximum time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="6393f-118">This value can be between 1 and 72 hours.</span><span class="sxs-lookup"><span data-stu-id="6393f-118">This value can be between 1 and 72 hours.</span></span>

## <a name="notifications"></a><span data-ttu-id="6393f-119">Notifications</span><span class="sxs-lookup"><span data-stu-id="6393f-119">Notifications</span></span>

<span data-ttu-id="6393f-120">Use the **Notifications** switch to specify whether the system sends emails to administrators confirming that they have activated a role.</span><span class="sxs-lookup"><span data-stu-id="6393f-120">Use the **Notifications** switch to specify whether the system sends emails to administrators confirming that they have activated a role.</span></span> <span data-ttu-id="6393f-121">This can be useful for detecting unauthorized or illegitimate activations.</span><span class="sxs-lookup"><span data-stu-id="6393f-121">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

## <a name="incidentrequest-ticket"></a><span data-ttu-id="6393f-122">Incident/Request ticket</span><span class="sxs-lookup"><span data-stu-id="6393f-122">Incident/Request ticket</span></span>

<span data-ttu-id="6393f-123">Use the **Incident/Request ticket** switch to specify whether to require eligible administrators to include a ticket number when they activate their role.</span><span class="sxs-lookup"><span data-stu-id="6393f-123">Use the **Incident/Request ticket** switch to specify whether to require eligible administrators to include a ticket number when they activate their role.</span></span> <span data-ttu-id="6393f-124">This can be useful when you perform role access audits.</span><span class="sxs-lookup"><span data-stu-id="6393f-124">This can be useful when you perform role access audits.</span></span>

## <a name="multi-factor-authentication"></a><span data-ttu-id="6393f-125">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6393f-125">Multi-Factor Authentication</span></span>

<span data-ttu-id="6393f-126">Use the **Multi-Factor Authentication** switch to specify whether to require users to verify their identity with MFA before they can activate their roles.</span><span class="sxs-lookup"><span data-stu-id="6393f-126">Use the **Multi-Factor Authentication** switch to specify whether to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="6393f-127">They only have to verify this once per session, not every time they activate a role.</span><span class="sxs-lookup"><span data-stu-id="6393f-127">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="6393f-128">There are two tips to keep in mind when you enable MFA:</span><span class="sxs-lookup"><span data-stu-id="6393f-128">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="6393f-129">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="6393f-129">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="6393f-130">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span><span class="sxs-lookup"><span data-stu-id="6393f-130">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="6393f-131">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span><span class="sxs-lookup"><span data-stu-id="6393f-131">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="6393f-132">This is a safety feature because these roles should be carefully protected:</span><span class="sxs-lookup"><span data-stu-id="6393f-132">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="6393f-133">Application administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-133">Application administrator</span></span>
  * <span data-ttu-id="6393f-134">Application Proxy server administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-134">Application Proxy server administrator</span></span>
  * <span data-ttu-id="6393f-135">Billing administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-135">Billing administrator</span></span>  
  * <span data-ttu-id="6393f-136">Compliance administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-136">Compliance administrator</span></span>  
  * <span data-ttu-id="6393f-137">CRM service administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-137">CRM service administrator</span></span>
  * <span data-ttu-id="6393f-138">Customer LockBox access approver</span><span class="sxs-lookup"><span data-stu-id="6393f-138">Customer LockBox access approver</span></span>
  * <span data-ttu-id="6393f-139">Directory writer</span><span class="sxs-lookup"><span data-stu-id="6393f-139">Directory writer</span></span>  
  * <span data-ttu-id="6393f-140">Exchange administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-140">Exchange administrator</span></span>  
  * <span data-ttu-id="6393f-141">Global administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-141">Global administrator</span></span>
  * <span data-ttu-id="6393f-142">Intune service administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-142">Intune service administrator</span></span>
  * <span data-ttu-id="6393f-143">Mailbox administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-143">Mailbox administrator</span></span>  
  * <span data-ttu-id="6393f-144">Partner tier1 support</span><span class="sxs-lookup"><span data-stu-id="6393f-144">Partner tier1 support</span></span>  
  * <span data-ttu-id="6393f-145">Partner tier2 support</span><span class="sxs-lookup"><span data-stu-id="6393f-145">Partner tier2 support</span></span>  
  * <span data-ttu-id="6393f-146">Privileged role administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-146">Privileged role administrator</span></span>
  * <span data-ttu-id="6393f-147">Security administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-147">Security administrator</span></span>  
  * <span data-ttu-id="6393f-148">SharePoint administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-148">SharePoint administrator</span></span>  
  * <span data-ttu-id="6393f-149">Skype for Business administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-149">Skype for Business administrator</span></span>  
  * <span data-ttu-id="6393f-150">User account administrator</span><span class="sxs-lookup"><span data-stu-id="6393f-150">User account administrator</span></span>  

<span data-ttu-id="6393f-151">For more information, see [Multi-factor authentication (MFA) and PIM](pim-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="6393f-151">For more information, see [Multi-factor authentication (MFA) and PIM](pim-how-to-require-mfa.md).</span></span>

## <a name="require-approval"></a><span data-ttu-id="6393f-152">Require approval</span><span class="sxs-lookup"><span data-stu-id="6393f-152">Require approval</span></span>

<span data-ttu-id="6393f-153">If you want to require approval to activate a role, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="6393f-153">If you want to require approval to activate a role, follow these steps.</span></span>

1. <span data-ttu-id="6393f-154">Set the **Require approval** switch to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="6393f-154">Set the **Require approval** switch to **Enabled**.</span></span> <span data-ttu-id="6393f-155">The pane expands with options to select approvers.</span><span class="sxs-lookup"><span data-stu-id="6393f-155">The pane expands with options to select approvers.</span></span>

    ![Azure AD directory roles - Settings - Require approval](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-require-approval.png)

    <span data-ttu-id="6393f-157">If you **DO NOT** specify any approvers, the Privileged Role Administrators become the default approvers.</span><span class="sxs-lookup"><span data-stu-id="6393f-157">If you **DO NOT** specify any approvers, the Privileged Role Administrators become the default approvers.</span></span> <span data-ttu-id="6393f-158">Privileged Role Administrators would be required to approve **ALL** activation requests for this role.</span><span class="sxs-lookup"><span data-stu-id="6393f-158">Privileged Role Administrators would be required to approve **ALL** activation requests for this role.</span></span>

1. <span data-ttu-id="6393f-159">To specify approvers, click **Select approvers**.</span><span class="sxs-lookup"><span data-stu-id="6393f-159">To specify approvers, click **Select approvers**.</span></span>

    ![Azure AD directory roles - Settings - Require approval](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-require-approval-select-approvers.png)

1. <span data-ttu-id="6393f-161">Select one or more approvers and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="6393f-161">Select one or more approvers and then click **Select**.</span></span> <span data-ttu-id="6393f-162">You can select users or groups.</span><span class="sxs-lookup"><span data-stu-id="6393f-162">You can select users or groups.</span></span> <span data-ttu-id="6393f-163">At least 2 approvers is recommended.</span><span class="sxs-lookup"><span data-stu-id="6393f-163">At least 2 approvers is recommended.</span></span> <span data-ttu-id="6393f-164">Self-approval is not allowed.</span><span class="sxs-lookup"><span data-stu-id="6393f-164">Self-approval is not allowed.</span></span>

    <span data-ttu-id="6393f-165">Your selections will appear in the list of selected approvers.</span><span class="sxs-lookup"><span data-stu-id="6393f-165">Your selections will appear in the list of selected approvers.</span></span>

1. <span data-ttu-id="6393f-166">Once you have specified your all your role settings, click **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="6393f-166">Once you have specified your all your role settings, click **Save** to save your changes.</span></span>


<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

## <a name="next-steps"></a><span data-ttu-id="6393f-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="6393f-167">Next steps</span></span>

- [<span data-ttu-id="6393f-168">Assign Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="6393f-168">Assign Azure AD directory roles in PIM</span></span>](pim-how-to-add-role-to-user.md)
- [<span data-ttu-id="6393f-169">Configure security alerts for Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="6393f-169">Configure security alerts for Azure AD directory roles in PIM</span></span>](pim-how-to-configure-security-alerts.md)
