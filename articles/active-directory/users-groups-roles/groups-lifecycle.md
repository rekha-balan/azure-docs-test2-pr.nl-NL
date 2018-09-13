---
title: Expiration for Office 365 groups in Azure Active Directory | Microsoft Docs
description: How to set up expiration for Office 365 groups in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 03/09/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 29a53101bff8c384d01f952c4498e09d9d970ee3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866179"
---
# <a name="configure-the-expiration-policy-for-office-365-groups"></a><span data-ttu-id="2fd88-103">Configure the expiration policy for Office 365 groups</span><span class="sxs-lookup"><span data-stu-id="2fd88-103">Configure the expiration policy for Office 365 groups</span></span>

<span data-ttu-id="2fd88-104">You can now manage the lifecycle of Office 365 groups by setting an expiration policy for them.</span><span class="sxs-lookup"><span data-stu-id="2fd88-104">You can now manage the lifecycle of Office 365 groups by setting an expiration policy for them.</span></span> <span data-ttu-id="2fd88-105">You can set expiration policy for only Office 365 groups in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2fd88-105">You can set expiration policy for only Office 365 groups in Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="2fd88-106">Once you set a group to expire:</span><span class="sxs-lookup"><span data-stu-id="2fd88-106">Once you set a group to expire:</span></span>
-   <span data-ttu-id="2fd88-107">Owners of the group are notified to renew the group as the expiration nears</span><span class="sxs-lookup"><span data-stu-id="2fd88-107">Owners of the group are notified to renew the group as the expiration nears</span></span>
-   <span data-ttu-id="2fd88-108">Any group that is not renewed is deleted</span><span class="sxs-lookup"><span data-stu-id="2fd88-108">Any group that is not renewed is deleted</span></span>
-   <span data-ttu-id="2fd88-109">Any Office 365 group that is deleted can be restored within 30 days by the group owners or the administrator</span><span class="sxs-lookup"><span data-stu-id="2fd88-109">Any Office 365 group that is deleted can be restored within 30 days by the group owners or the administrator</span></span>

> [!NOTE]
> <span data-ttu-id="2fd88-110">Configuring and using the expiration policy for Office 365 groups requires you to have on hand Azure AD Premium licenses for all members of the groups to which the expiration policy is applied.</span><span class="sxs-lookup"><span data-stu-id="2fd88-110">Configuring and using the expiration policy for Office 365 groups requires you to have on hand Azure AD Premium licenses for all members of the groups to which the expiration policy is applied.</span></span>

<span data-ttu-id="2fd88-111">For information on how to download and install the Azure AD PowerShell cmdlets, see [Azure Active Directory PowerShell for Graph 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="2fd88-111">For information on how to download and install the Azure AD PowerShell cmdlets, see [Azure Active Directory PowerShell for Graph 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

## <a name="roles-and-permissions"></a><span data-ttu-id="2fd88-112">Roles and permissions</span><span class="sxs-lookup"><span data-stu-id="2fd88-112">Roles and permissions</span></span>
<span data-ttu-id="2fd88-113">The following are roles that can configure and use expiration for Office 365 groups in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fd88-113">The following are roles that can configure and use expiration for Office 365 groups in Azure AD.</span></span>

<span data-ttu-id="2fd88-114">Role</span><span class="sxs-lookup"><span data-stu-id="2fd88-114">Role</span></span> | <span data-ttu-id="2fd88-115">Permissions</span><span class="sxs-lookup"><span data-stu-id="2fd88-115">Permissions</span></span>
-------- | --------
<span data-ttu-id="2fd88-116">Global Administrator or User Account Administrator</span><span class="sxs-lookup"><span data-stu-id="2fd88-116">Global Administrator or User Account Administrator</span></span> | <span data-ttu-id="2fd88-117">Can create, read, update, or delete the Office 365 groups expiration policy settings</span><span class="sxs-lookup"><span data-stu-id="2fd88-117">Can create, read, update, or delete the Office 365 groups expiration policy settings</span></span><br><span data-ttu-id="2fd88-118">Can renew any Office 365 group</span><span class="sxs-lookup"><span data-stu-id="2fd88-118">Can renew any Office 365 group</span></span>
<span data-ttu-id="2fd88-119">User</span><span class="sxs-lookup"><span data-stu-id="2fd88-119">User</span></span> | <span data-ttu-id="2fd88-120">Can renew an Office 365 group that they own</span><span class="sxs-lookup"><span data-stu-id="2fd88-120">Can renew an Office 365 group that they own</span></span><br><span data-ttu-id="2fd88-121">Can restore an Office 365 group that they own</span><span class="sxs-lookup"><span data-stu-id="2fd88-121">Can restore an Office 365 group that they own</span></span><br><span data-ttu-id="2fd88-122">Can read the expiration policy settings</span><span class="sxs-lookup"><span data-stu-id="2fd88-122">Can read the expiration policy settings</span></span>

<span data-ttu-id="2fd88-123">For more information on permissions to restore a deleted group, see [Restore a deleted Office 365 group in Azure Active Directory](groups-restore-deleted.md).</span><span class="sxs-lookup"><span data-stu-id="2fd88-123">For more information on permissions to restore a deleted group, see [Restore a deleted Office 365 group in Azure Active Directory](groups-restore-deleted.md).</span></span>

## <a name="set-group-expiration"></a><span data-ttu-id="2fd88-124">Set group expiration</span><span class="sxs-lookup"><span data-stu-id="2fd88-124">Set group expiration</span></span>

1. <span data-ttu-id="2fd88-125">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="2fd88-125">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="2fd88-126">Select **Groups**,then select **Expiration** to open the expiration settings.</span><span class="sxs-lookup"><span data-stu-id="2fd88-126">Select **Groups**,then select **Expiration** to open the expiration settings.</span></span>
  
  ![Expiration blade](./media/groups-lifecycle/expiration-settings.png)

4. <span data-ttu-id="2fd88-128">On the **Expiration** blade, you can:</span><span class="sxs-lookup"><span data-stu-id="2fd88-128">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="2fd88-129">Set the group lifetime in days.</span><span class="sxs-lookup"><span data-stu-id="2fd88-129">Set the group lifetime in days.</span></span> <span data-ttu-id="2fd88-130">You could select one of the preset values, or a custom value (should be 31 days or more).</span><span class="sxs-lookup"><span data-stu-id="2fd88-130">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="2fd88-131">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span><span class="sxs-lookup"><span data-stu-id="2fd88-131">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="2fd88-132">Select which Office 365 groups expire.</span><span class="sxs-lookup"><span data-stu-id="2fd88-132">Select which Office 365 groups expire.</span></span> <span data-ttu-id="2fd88-133">You can enable expiration for **All** Office 365 groups, you can choose to enable only **Selected** Office 365 groups, or you select **None** to disable expiration for all groups.</span><span class="sxs-lookup"><span data-stu-id="2fd88-133">You can enable expiration for **All** Office 365 groups, you can choose to enable only **Selected** Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="2fd88-134">Save your settings when you're done by selecting **Save**.</span><span class="sxs-lookup"><span data-stu-id="2fd88-134">Save your settings when you're done by selecting **Save**.</span></span>


<span data-ttu-id="2fd88-135">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span><span class="sxs-lookup"><span data-stu-id="2fd88-135">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![Expiration email notification](./media/groups-lifecycle/expiration-notification.png)

<span data-ttu-id="2fd88-137">From the **Renew group** notification email, group owners can directly access the group details page in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2fd88-137">From the **Renew group** notification email, group owners can directly access the group details page in the Access Panel.</span></span> <span data-ttu-id="2fd88-138">There, the users can get more information about the group such as its description, when it was last renewed, when it will expire, and also the ability to renew the group.</span><span class="sxs-lookup"><span data-stu-id="2fd88-138">There, the users can get more information about the group such as its description, when it was last renewed, when it will expire, and also the ability to renew the group.</span></span> <span data-ttu-id="2fd88-139">The group details page now also includes links to the Office 365 group resources, so that the group owner can conveniently view the content and activity in their group.</span><span class="sxs-lookup"><span data-stu-id="2fd88-139">The group details page now also includes links to the Office 365 group resources, so that the group owner can conveniently view the content and activity in their group.</span></span>

<span data-ttu-id="2fd88-140">When a group expires, the group is deleted one day after the expiration date.</span><span class="sxs-lookup"><span data-stu-id="2fd88-140">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="2fd88-141">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span><span class="sxs-lookup"><span data-stu-id="2fd88-141">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![Group deletion email notification](./media/groups-lifecycle/deletion-notification.png)

<span data-ttu-id="2fd88-143">The group can be restored within 30 days of its deletion by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory](groups-restore-deleted.md).</span><span class="sxs-lookup"><span data-stu-id="2fd88-143">The group can be restored within 30 days of its deletion by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory](groups-restore-deleted.md).</span></span>
    
<span data-ttu-id="2fd88-144">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span><span class="sxs-lookup"><span data-stu-id="2fd88-144">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="2fd88-145">When you first set up expiration, any groups that are older than the expiration interval are set to 30 days until expiration.</span><span class="sxs-lookup"><span data-stu-id="2fd88-145">When you first set up expiration, any groups that are older than the expiration interval are set to 30 days until expiration.</span></span> <span data-ttu-id="2fd88-146">The first renewal notification email is sent out within a day.</span><span class="sxs-lookup"><span data-stu-id="2fd88-146">The first renewal notification email is sent out within a day.</span></span> 
>   <span data-ttu-id="2fd88-147">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span><span class="sxs-lookup"><span data-stu-id="2fd88-147">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="2fd88-148">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span><span class="sxs-lookup"><span data-stu-id="2fd88-148">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="2fd88-149">Currently only one expiration policy can be configured for Office 365 groups on a tenant.</span><span class="sxs-lookup"><span data-stu-id="2fd88-149">Currently only one expiration policy can be configured for Office 365 groups on a tenant.</span></span>
> * <span data-ttu-id="2fd88-150">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span><span class="sxs-lookup"><span data-stu-id="2fd88-150">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="2fd88-151">This process might take up to 24 hours.</span><span class="sxs-lookup"><span data-stu-id="2fd88-151">This process might take up to 24 hours.</span></span>

## <a name="how-office-365-group-expiration-works-with-a-mailbox-on-legal-hold"></a><span data-ttu-id="2fd88-152">How Office 365 group expiration works with a mailbox on legal hold</span><span class="sxs-lookup"><span data-stu-id="2fd88-152">How Office 365 group expiration works with a mailbox on legal hold</span></span>
<span data-ttu-id="2fd88-153">When a group expires and is deleted, then 30 days after deletion the group's data from apps like Planner, Sites, or Teams is permanently deleted, but the group mailbox that is on legal hold is retained and is not permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="2fd88-153">When a group expires and is deleted, then 30 days after deletion the group's data from apps like Planner, Sites, or Teams is permanently deleted, but the group mailbox that is on legal hold is retained and is not permanently deleted.</span></span> <span data-ttu-id="2fd88-154">The administrator can use Exchange cmdlets to restore the mailbox to fetch the data.</span><span class="sxs-lookup"><span data-stu-id="2fd88-154">The administrator can use Exchange cmdlets to restore the mailbox to fetch the data.</span></span> 

## <a name="how-office-365-group-expiration-works-with-retention-policy"></a><span data-ttu-id="2fd88-155">How Office 365 group expiration works with retention policy</span><span class="sxs-lookup"><span data-stu-id="2fd88-155">How Office 365 group expiration works with retention policy</span></span>
<span data-ttu-id="2fd88-156">The retention policy is configured by way of the Security and Compliance Center.</span><span class="sxs-lookup"><span data-stu-id="2fd88-156">The retention policy is configured by way of the Security and Compliance Center.</span></span> <span data-ttu-id="2fd88-157">If you have set up a retention policy for Office 365 groups, when a group expires and is deleted, the group conversations in the group mailbox and files in the group site are retained in the retention container for the specific number of days defined in the retention policy.</span><span class="sxs-lookup"><span data-stu-id="2fd88-157">If you have set up a retention policy for Office 365 groups, when a group expires and is deleted, the group conversations in the group mailbox and files in the group site are retained in the retention container for the specific number of days defined in the retention policy.</span></span> <span data-ttu-id="2fd88-158">Users won't see the group or its content after expiration, but can recover the site and mailbox data via e-discovery.</span><span class="sxs-lookup"><span data-stu-id="2fd88-158">Users won't see the group or its content after expiration, but can recover the site and mailbox data via e-discovery.</span></span>

## <a name="powershell-examples"></a><span data-ttu-id="2fd88-159">PowerShell examples</span><span class="sxs-lookup"><span data-stu-id="2fd88-159">PowerShell examples</span></span>
<span data-ttu-id="2fd88-160">Here are examples of how you can use PowerShell cmdlets to configure the expiration settings for Office 365 groups in your tenant:</span><span class="sxs-lookup"><span data-stu-id="2fd88-160">Here are examples of how you can use PowerShell cmdlets to configure the expiration settings for Office 365 groups in your tenant:</span></span>

1. <span data-ttu-id="2fd88-161">Install the PowerShell v2.0 Preview module (2.0.0.137) and sign in at the PowerShell prompt:</span><span class="sxs-lookup"><span data-stu-id="2fd88-161">Install the PowerShell v2.0 Preview module (2.0.0.137) and sign in at the PowerShell prompt:</span></span>
  ````
  Install-Module -Name AzureADPreview
  connect-azuread 
  ````
2. <span data-ttu-id="2fd88-162">Configure the expiration settings New-AzureADMSGroupLifecyclePolicy:  This cmdlet sets the lifetime for all Office 365 groups in the tenant to 365 days.</span><span class="sxs-lookup"><span data-stu-id="2fd88-162">Configure the expiration settings New-AzureADMSGroupLifecyclePolicy:  This cmdlet sets the lifetime for all Office 365 groups in the tenant to 365 days.</span></span> <span data-ttu-id="2fd88-163">Renewal notifications for Office 365 groups without owners will be sent to ‘emailaddress@contoso.com’</span><span class="sxs-lookup"><span data-stu-id="2fd88-163">Renewal notifications for Office 365 groups without owners will be sent to ‘emailaddress@contoso.com’</span></span>
  
  ````
  New-AzureADMSGroupLifecyclePolicy -GroupLifetimeInDays 365 -ManagedGroupTypes All -AlternateNotificationEmails emailaddress@contoso.com
  ````
3. <span data-ttu-id="2fd88-164">Retrieve the existing policy Get-AzureADMSGroupLifecyclePolicy: This cmdlet retrieves the current Office 365 group expiration  settings that have been configured.</span><span class="sxs-lookup"><span data-stu-id="2fd88-164">Retrieve the existing policy Get-AzureADMSGroupLifecyclePolicy: This cmdlet retrieves the current Office 365 group expiration  settings that have been configured.</span></span> <span data-ttu-id="2fd88-165">In this example, you can see:</span><span class="sxs-lookup"><span data-stu-id="2fd88-165">In this example, you can see:</span></span>
  * <span data-ttu-id="2fd88-166">The policy ID</span><span class="sxs-lookup"><span data-stu-id="2fd88-166">The policy ID</span></span> 
  * <span data-ttu-id="2fd88-167">The lifetime for all Office 365 groups in the tenant is set to 365 days</span><span class="sxs-lookup"><span data-stu-id="2fd88-167">The lifetime for all Office 365 groups in the tenant is set to 365 days</span></span>
  * <span data-ttu-id="2fd88-168">Renewal notifications for Office 365 groups without owners will be sent to ‘emailaddress@contoso.com.’</span><span class="sxs-lookup"><span data-stu-id="2fd88-168">Renewal notifications for Office 365 groups without owners will be sent to ‘emailaddress@contoso.com.’</span></span>
  
  ````
  Get-AzureADMSGroupLifecyclePolicy
  
  ID                                    GroupLifetimeInDays ManagedGroupTypes AlternateNotificationEmails
  --                                    ------------------- ----------------- ---------------------------
  26fcc232-d1c3-4375-b68d-15c296f1f077  365                 All               emailaddress@contoso.com
  ```` 
   
4. <span data-ttu-id="2fd88-169">Update the existing policy Set-AzureADMSGroupLifecyclePolicy: This cmdlet is used to update an existing policy.</span><span class="sxs-lookup"><span data-stu-id="2fd88-169">Update the existing policy Set-AzureADMSGroupLifecyclePolicy: This cmdlet is used to update an existing policy.</span></span> <span data-ttu-id="2fd88-170">In the example below, the group lifetime in the existing policy is changed from 365 days to 180 days.</span><span class="sxs-lookup"><span data-stu-id="2fd88-170">In the example below, the group lifetime in the existing policy is changed from 365 days to 180 days.</span></span> 
  
  ````
  Set-AzureADMSGroupLifecyclePolicy -Id “26fcc232-d1c3-4375-b68d-15c296f1f077”   -GroupLifetimeInDays 180 -AlternateNotificationEmails "emailaddress@contoso.com"
  ````
  
5. <span data-ttu-id="2fd88-171">Add specific groups to the policy Add-AzureADMSLifecyclePolicyGroup: This cmdlet adds a group to the lifecycle policy.</span><span class="sxs-lookup"><span data-stu-id="2fd88-171">Add specific groups to the policy Add-AzureADMSLifecyclePolicyGroup: This cmdlet adds a group to the lifecycle policy.</span></span> <span data-ttu-id="2fd88-172">As an example:</span><span class="sxs-lookup"><span data-stu-id="2fd88-172">As an example:</span></span> 
  
  ````
  Add-AzureADMSLifecyclePolicyGroup -Id “26fcc232-d1c3-4375-b68d-15c296f1f077” -groupId "cffd97bd-6b91-4c4e-b553-6918a320211c"
  ````
  
6. <span data-ttu-id="2fd88-173">Remove the existing Policy Remove-AzureADMSGroupLifecyclePolicy: This cmdlet deletes the Office 365 group expiration settings but requires the policy ID.</span><span class="sxs-lookup"><span data-stu-id="2fd88-173">Remove the existing Policy Remove-AzureADMSGroupLifecyclePolicy: This cmdlet deletes the Office 365 group expiration settings but requires the policy ID.</span></span> <span data-ttu-id="2fd88-174">This will disable expiration for Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="2fd88-174">This will disable expiration for Office 365 groups.</span></span> 
  
  ````
  Remove-AzureADMSGroupLifecyclePolicy -Id “26fcc232-d1c3-4375-b68d-15c296f1f077”
  ````
  
<span data-ttu-id="2fd88-175">The following cmdlets can be used to configure the policy in more detail.</span><span class="sxs-lookup"><span data-stu-id="2fd88-175">The following cmdlets can be used to configure the policy in more detail.</span></span> <span data-ttu-id="2fd88-176">For more informatin, see [PowerShell documentation](https://docs.microsoft.com/powershell/module/azuread/?view=azureadps-2.0-preview&branch=master#groups).</span><span class="sxs-lookup"><span data-stu-id="2fd88-176">For more informatin, see [PowerShell documentation](https://docs.microsoft.com/powershell/module/azuread/?view=azureadps-2.0-preview&branch=master#groups).</span></span>

* <span data-ttu-id="2fd88-177">Get-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="2fd88-177">Get-AzureADMSGroupLifecyclePolicy</span></span>
* <span data-ttu-id="2fd88-178">New-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="2fd88-178">New-AzureADMSGroupLifecyclePolicy</span></span>
* <span data-ttu-id="2fd88-179">Get-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="2fd88-179">Get-AzureADMSGroupLifecyclePolicy</span></span>
* <span data-ttu-id="2fd88-180">Set-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="2fd88-180">Set-AzureADMSGroupLifecyclePolicy</span></span>
* <span data-ttu-id="2fd88-181">Remove-AzureADMSGroupLifecyclePolicy</span><span class="sxs-lookup"><span data-stu-id="2fd88-181">Remove-AzureADMSGroupLifecyclePolicy</span></span>
* <span data-ttu-id="2fd88-182">Add-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="2fd88-182">Add-AzureADMSLifecyclePolicyGroup</span></span>
* <span data-ttu-id="2fd88-183">Remove-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="2fd88-183">Remove-AzureADMSLifecyclePolicyGroup</span></span>
* <span data-ttu-id="2fd88-184">Reset-AzureADMSLifeCycleGroup</span><span class="sxs-lookup"><span data-stu-id="2fd88-184">Reset-AzureADMSLifeCycleGroup</span></span>   
* <span data-ttu-id="2fd88-185">Get-AzureADMSLifecyclePolicyGroup</span><span class="sxs-lookup"><span data-stu-id="2fd88-185">Get-AzureADMSLifecyclePolicyGroup</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fd88-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fd88-186">Next steps</span></span>
<span data-ttu-id="2fd88-187">These articles provide additional information on Azure AD groups.</span><span class="sxs-lookup"><span data-stu-id="2fd88-187">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="2fd88-188">See existing groups</span><span class="sxs-lookup"><span data-stu-id="2fd88-188">See existing groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="2fd88-189">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="2fd88-189">Manage settings of a group</span></span>](../fundamentals/active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="2fd88-190">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="2fd88-190">Manage members of a group</span></span>](../fundamentals/active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="2fd88-191">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="2fd88-191">Manage memberships of a group</span></span>](../fundamentals/active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="2fd88-192">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="2fd88-192">Manage dynamic rules for users in a group</span></span>](groups-dynamic-membership.md)
