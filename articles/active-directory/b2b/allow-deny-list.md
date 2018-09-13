---
title: Allow or block invitations to B2B users from specific organizations - Azure Active Directory | Microsoft Docs
description: Shows how an administrator can use the Azure portal or PowerShell to set an access or deny list to allow or block B2B users from certain domains.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 04/19/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: c354be5308c4db644c5ad7b10e9c754cc261c185
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966080"
---
# <a name="allow-or-block-invitations-to-b2b-users-from-specific-organizations"></a><span data-ttu-id="da872-103">Allow or block invitations to B2B users from specific organizations</span><span class="sxs-lookup"><span data-stu-id="da872-103">Allow or block invitations to B2B users from specific organizations</span></span>

<span data-ttu-id="da872-104">You can use an allow list or a deny list to allow or block invitations to B2B users from specific organizations.</span><span class="sxs-lookup"><span data-stu-id="da872-104">You can use an allow list or a deny list to allow or block invitations to B2B users from specific organizations.</span></span> <span data-ttu-id="da872-105">For example, if you want to block personal email address domains, you can set up a deny list that contains domains like Gmail.com and Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="da872-105">For example, if you want to block personal email address domains, you can set up a deny list that contains domains like Gmail.com and Outlook.com.</span></span> <span data-ttu-id="da872-106">Or, if your business has a partnership with other businesses like Contoso.com, Fabrikam.com, and Litware.com, and you want to restrict invitations to only these organizations, you can add Contoso.com, Fabrikam.com, and Litware.com to your allow list.</span><span class="sxs-lookup"><span data-stu-id="da872-106">Or, if your business has a partnership with other businesses like Contoso.com, Fabrikam.com, and Litware.com, and you want to restrict invitations to only these organizations, you can add Contoso.com, Fabrikam.com, and Litware.com to your allow list.</span></span>
  
## <a name="important-considerations"></a><span data-ttu-id="da872-107">Important considerations</span><span class="sxs-lookup"><span data-stu-id="da872-107">Important considerations</span></span>

- <span data-ttu-id="da872-108">You can create either an allow list or a deny list.</span><span class="sxs-lookup"><span data-stu-id="da872-108">You can create either an allow list or a deny list.</span></span> <span data-ttu-id="da872-109">You can't set up both types of lists.</span><span class="sxs-lookup"><span data-stu-id="da872-109">You can't set up both types of lists.</span></span> <span data-ttu-id="da872-110">By default, whatever domains are not in the allow list are on the deny list, and vice versa.</span><span class="sxs-lookup"><span data-stu-id="da872-110">By default, whatever domains are not in the allow list are on the deny list, and vice versa.</span></span> 
- <span data-ttu-id="da872-111">You can create only one policy per organization.</span><span class="sxs-lookup"><span data-stu-id="da872-111">You can create only one policy per organization.</span></span> <span data-ttu-id="da872-112">You can update the policy to include more domains, or you can delete the policy to create a new one.</span><span class="sxs-lookup"><span data-stu-id="da872-112">You can update the policy to include more domains, or you can delete the policy to create a new one.</span></span> 
- <span data-ttu-id="da872-113">This list works independently from OneDrive for Business and SharePoint Online allow/block lists.</span><span class="sxs-lookup"><span data-stu-id="da872-113">This list works independently from OneDrive for Business and SharePoint Online allow/block lists.</span></span> <span data-ttu-id="da872-114">If you want to restrict individual file sharing in SharePoint Online, you need to set up an allow or deny list for OneDrive for Business and SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="da872-114">If you want to restrict individual file sharing in SharePoint Online, you need to set up an allow or deny list for OneDrive for Business and SharePoint Online.</span></span> <span data-ttu-id="da872-115">For more information, see [Restricted domains sharing in SharePoint Online and OneDrive for Business](https://support.office.com/article/restricted-domains-sharing-in-sharepoint-online-and-onedrive-for-business-5d7589cd-0997-4a00-a2ba-2320ec49c4e9).</span><span class="sxs-lookup"><span data-stu-id="da872-115">For more information, see [Restricted domains sharing in SharePoint Online and OneDrive for Business](https://support.office.com/article/restricted-domains-sharing-in-sharepoint-online-and-onedrive-for-business-5d7589cd-0997-4a00-a2ba-2320ec49c4e9).</span></span>
- <span data-ttu-id="da872-116">This list does not apply to external users who have already redeemed the invitation.</span><span class="sxs-lookup"><span data-stu-id="da872-116">This list does not apply to external users who have already redeemed the invitation.</span></span> <span data-ttu-id="da872-117">The list will be enforced after the list is set up.</span><span class="sxs-lookup"><span data-stu-id="da872-117">The list will be enforced after the list is set up.</span></span> <span data-ttu-id="da872-118">If a user invitation is in a pending state, and you set a policy that blocks their domain, the user's attempt to redeem the invitation will fail.</span><span class="sxs-lookup"><span data-stu-id="da872-118">If a user invitation is in a pending state, and you set a policy that blocks their domain, the user's attempt to redeem the invitation will fail.</span></span>

## <a name="set-the-allow-or-deny-list-policy-in-the-portal"></a><span data-ttu-id="da872-119">Set the allow or deny list policy in the portal</span><span class="sxs-lookup"><span data-stu-id="da872-119">Set the allow or deny list policy in the portal</span></span>

<span data-ttu-id="da872-120">By default, the **Allow invitations to be sent to any domain (most inclusive)** setting is enabled.</span><span class="sxs-lookup"><span data-stu-id="da872-120">By default, the **Allow invitations to be sent to any domain (most inclusive)** setting is enabled.</span></span> <span data-ttu-id="da872-121">In this case, you can invite B2B users from any organization.</span><span class="sxs-lookup"><span data-stu-id="da872-121">In this case, you can invite B2B users from any organization.</span></span>

### <a name="add-a-deny-list"></a><span data-ttu-id="da872-122">Add a deny list</span><span class="sxs-lookup"><span data-stu-id="da872-122">Add a deny list</span></span>

<span data-ttu-id="da872-123">This is the most typical scenario, where your organization wants to work with almost any organization, but wants to prevent users from specific domains to be invited as B2B users.</span><span class="sxs-lookup"><span data-stu-id="da872-123">This is the most typical scenario, where your organization wants to work with almost any organization, but wants to prevent users from specific domains to be invited as B2B users.</span></span>

<span data-ttu-id="da872-124">To add a deny list:</span><span class="sxs-lookup"><span data-stu-id="da872-124">To add a deny list:</span></span>

1. <span data-ttu-id="da872-125">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da872-125">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="da872-126">Select **Azure Active Directory** > **Users** > **User settings**.</span><span class="sxs-lookup"><span data-stu-id="da872-126">Select **Azure Active Directory** > **Users** > **User settings**.</span></span>
3. <span data-ttu-id="da872-127">Under **External users**, select **Manage external collaboration settings**.</span><span class="sxs-lookup"><span data-stu-id="da872-127">Under **External users**, select **Manage external collaboration settings**.</span></span>
4. <span data-ttu-id="da872-128">Under **Collaboration restrictions**, select **Deny invitations to the specified domains**.</span><span class="sxs-lookup"><span data-stu-id="da872-128">Under **Collaboration restrictions**, select **Deny invitations to the specified domains**.</span></span>
5. <span data-ttu-id="da872-129">Under **TARGET DOMAINS**, enter the name of one of the domains that you want to block.</span><span class="sxs-lookup"><span data-stu-id="da872-129">Under **TARGET DOMAINS**, enter the name of one of the domains that you want to block.</span></span> <span data-ttu-id="da872-130">For multiple domains, enter each domain on a new line.</span><span class="sxs-lookup"><span data-stu-id="da872-130">For multiple domains, enter each domain on a new line.</span></span> <span data-ttu-id="da872-131">For example:</span><span class="sxs-lookup"><span data-stu-id="da872-131">For example:</span></span>

   ![Shows the deny option with added domains](./media/allow-deny-list/DenyListSettings.png)
 
6. <span data-ttu-id="da872-133">When you're done, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="da872-133">When you're done, click **Save**.</span></span>

<span data-ttu-id="da872-134">After you set the policy, if you try to invite a user from a blocked domain, you receive a message saying that the domain of the user is currently blocked by your invitation policy.</span><span class="sxs-lookup"><span data-stu-id="da872-134">After you set the policy, if you try to invite a user from a blocked domain, you receive a message saying that the domain of the user is currently blocked by your invitation policy.</span></span>
 
### <a name="add-an-allow-list"></a><span data-ttu-id="da872-135">Add an allow list</span><span class="sxs-lookup"><span data-stu-id="da872-135">Add an allow list</span></span>

<span data-ttu-id="da872-136">This is a more restrictive configuration, where you can set specific domains in the allow list and restrict invitations to any other organizations or domains that aren't mentioned.</span><span class="sxs-lookup"><span data-stu-id="da872-136">This is a more restrictive configuration, where you can set specific domains in the allow list and restrict invitations to any other organizations or domains that aren't mentioned.</span></span> 

<span data-ttu-id="da872-137">If you want to use an allow list, make sure that you spend time to fully evaluate what your business needs are.</span><span class="sxs-lookup"><span data-stu-id="da872-137">If you want to use an allow list, make sure that you spend time to fully evaluate what your business needs are.</span></span> <span data-ttu-id="da872-138">If you make this policy too restrictive, your users may choose to send documents over email, or find other non-IT sanctioned ways of collaborating.</span><span class="sxs-lookup"><span data-stu-id="da872-138">If you make this policy too restrictive, your users may choose to send documents over email, or find other non-IT sanctioned ways of collaborating.</span></span>


<span data-ttu-id="da872-139">To add an allow list:</span><span class="sxs-lookup"><span data-stu-id="da872-139">To add an allow list:</span></span>

1. <span data-ttu-id="da872-140">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da872-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="da872-141">Select **Azure Active Directory** > **Users** > **User settings**.</span><span class="sxs-lookup"><span data-stu-id="da872-141">Select **Azure Active Directory** > **Users** > **User settings**.</span></span>
3. <span data-ttu-id="da872-142">Under **External users**, select **Manage external collaboration settings**.</span><span class="sxs-lookup"><span data-stu-id="da872-142">Under **External users**, select **Manage external collaboration settings**.</span></span>
4. <span data-ttu-id="da872-143">Under **Collaboration restrictions**, select **Allow invitations only to the specified domains (most restrictive)**.</span><span class="sxs-lookup"><span data-stu-id="da872-143">Under **Collaboration restrictions**, select **Allow invitations only to the specified domains (most restrictive)**.</span></span>
5. <span data-ttu-id="da872-144">Under **TARGET DOMAINS**, enter the name of one of the domains that you want to allow.</span><span class="sxs-lookup"><span data-stu-id="da872-144">Under **TARGET DOMAINS**, enter the name of one of the domains that you want to allow.</span></span> <span data-ttu-id="da872-145">For multiple domains, enter each domain on a new line.</span><span class="sxs-lookup"><span data-stu-id="da872-145">For multiple domains, enter each domain on a new line.</span></span> <span data-ttu-id="da872-146">For example:</span><span class="sxs-lookup"><span data-stu-id="da872-146">For example:</span></span>

   ![Shows the allow option with added domains](./media/allow-deny-list/AllowListSettings.png)
 
6. <span data-ttu-id="da872-148">When you're done, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="da872-148">When you're done, click **Save**.</span></span>

<span data-ttu-id="da872-149">After you set the policy, if you try to invite a user from a domain that's not on the allow list, you receive a message saying that the domain of the user is currently blocked by your invitation policy.</span><span class="sxs-lookup"><span data-stu-id="da872-149">After you set the policy, if you try to invite a user from a domain that's not on the allow list, you receive a message saying that the domain of the user is currently blocked by your invitation policy.</span></span>

### <a name="switch-from-allow-to-deny-list-and-vice-versa"></a><span data-ttu-id="da872-150">Switch from allow to deny list and vice versa</span><span class="sxs-lookup"><span data-stu-id="da872-150">Switch from allow to deny list and vice versa</span></span> 

<span data-ttu-id="da872-151">If you switch from one policy to the other, this discards the existing policy configuration.</span><span class="sxs-lookup"><span data-stu-id="da872-151">If you switch from one policy to the other, this discards the existing policy configuration.</span></span> <span data-ttu-id="da872-152">Make sure to back up details of your configuration before you perform the switch.</span><span class="sxs-lookup"><span data-stu-id="da872-152">Make sure to back up details of your configuration before you perform the switch.</span></span> 

## <a name="set-the-allow-or-deny-list-policy-using-powershell"></a><span data-ttu-id="da872-153">Set the allow or deny list policy using PowerShell</span><span class="sxs-lookup"><span data-stu-id="da872-153">Set the allow or deny list policy using PowerShell</span></span>

### <a name="prerequisite"></a><span data-ttu-id="da872-154">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="da872-154">Prerequisite</span></span>

<span data-ttu-id="da872-155">To set the allow or deny list by using PowerShell, you must install the preview version of the Azure Active Directory Module for Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da872-155">To set the allow or deny list by using PowerShell, you must install the preview version of the Azure Active Directory Module for Windows PowerShell.</span></span> <span data-ttu-id="da872-156">Specifically, install the AzureADPreview module version 2.0.0.98 or later.</span><span class="sxs-lookup"><span data-stu-id="da872-156">Specifically, install the AzureADPreview module version 2.0.0.98 or later.</span></span>

<span data-ttu-id="da872-157">To check the version of the module (and see if it's installed):</span><span class="sxs-lookup"><span data-stu-id="da872-157">To check the version of the module (and see if it's installed):</span></span>
 
1. <span data-ttu-id="da872-158">Open Windows PowerShell as an elevated user (Run as Administrator).</span><span class="sxs-lookup"><span data-stu-id="da872-158">Open Windows PowerShell as an elevated user (Run as Administrator).</span></span> 
2. <span data-ttu-id="da872-159">Run the following command to see if you have any versions of the Azure Active Directory Module for Windows PowerShell installed on your computer:</span><span class="sxs-lookup"><span data-stu-id="da872-159">Run the following command to see if you have any versions of the Azure Active Directory Module for Windows PowerShell installed on your computer:</span></span>

   ````powershell  
   Get-Module -ListAvailable AzureAD*
   ````

<span data-ttu-id="da872-160">If the module is not installed, or you don't have a required version, do one of the following:</span><span class="sxs-lookup"><span data-stu-id="da872-160">If the module is not installed, or you don't have a required version, do one of the following:</span></span>

- <span data-ttu-id="da872-161">If no results are returned, run the following command to install the latest version of the AzureADPreview module:</span><span class="sxs-lookup"><span data-stu-id="da872-161">If no results are returned, run the following command to install the latest version of the AzureADPreview module:</span></span>
  
   ````powershell  
   Install-Module AzureADPreview
   ````
- <span data-ttu-id="da872-162">If only the AzureAD module is shown in the results, run the following commands to install the AzureADPreview module:</span><span class="sxs-lookup"><span data-stu-id="da872-162">If only the AzureAD module is shown in the results, run the following commands to install the AzureADPreview module:</span></span> 

   ````powershell 
   Uninstall-Module AzureAD 
   Install-Module AzureADPreview 
   ````
- <span data-ttu-id="da872-163">If only the AzureADPreview module is shown in the results, but the version is less than 2.0.0.98, run the following commands to update it:</span><span class="sxs-lookup"><span data-stu-id="da872-163">If only the AzureADPreview module is shown in the results, but the version is less than 2.0.0.98, run the following commands to update it:</span></span> 

   ````powershell 
   Uninstall-Module AzureADPreview 
   Install-Module AzureADPreview 
   ````

- <span data-ttu-id="da872-164">If both the AzureAD and AzureADPreview modules are shown in the results, but the version of the AzureADPreview module is less than 2.0.0.98, run the following commands to update it:</span><span class="sxs-lookup"><span data-stu-id="da872-164">If both the AzureAD and AzureADPreview modules are shown in the results, but the version of the AzureADPreview module is less than 2.0.0.98, run the following commands to update it:</span></span> 

   ````powershell 
   Uninstall-Module AzureAD 
   Uninstall-Module AzureADPreview 
   Install-Module AzureADPreview 
    ````

### <a name="use-the-azureadpolicy-cmdlets-to-configure-the-policy"></a><span data-ttu-id="da872-165">Use the AzureADPolicy cmdlets to configure the policy</span><span class="sxs-lookup"><span data-stu-id="da872-165">Use the AzureADPolicy cmdlets to configure the policy</span></span>

<span data-ttu-id="da872-166">To create an allow or deny list, use the [New-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/new-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="da872-166">To create an allow or deny list, use the [New-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/new-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span></span> <span data-ttu-id="da872-167">The following example shows how to set a deny list that blocks the "live.com" domain.</span><span class="sxs-lookup"><span data-stu-id="da872-167">The following example shows how to set a deny list that blocks the "live.com" domain.</span></span>

````powershell 
$policyValue = @("{`"B2BManagementPolicy`":{`"InvitationsAllowedAndBlockedDomainsPolicy`":{`"AllowedDomains`": [],`"BlockedDomains`": [`"live.com`"]}}}")

New-AzureADPolicy -Definition $policyValue -DisplayName B2BManagementPolicy -Type B2BManagementPolicy -IsOrganizationDefault $true 
````

<span data-ttu-id="da872-168">The following shows the same example, but with the policy definition inline.</span><span class="sxs-lookup"><span data-stu-id="da872-168">The following shows the same example, but with the policy definition inline.</span></span>

````powershell  
New-AzureADPolicy -Definition @("{`"B2BManagementPolicy`":{`"InvitationsAllowedAndBlockedDomainsPolicy`":{`"AllowedDomains`": [],`"BlockedDomains`": [`"live.com`"]}}}") -DisplayName B2BManagementPolicy -Type B2BManagementPolicy -IsOrganizationDefault $true 
````

<span data-ttu-id="da872-169">To set the allow or deny list policy, use the [Set-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/set-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="da872-169">To set the allow or deny list policy, use the [Set-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/set-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span></span> <span data-ttu-id="da872-170">For example:</span><span class="sxs-lookup"><span data-stu-id="da872-170">For example:</span></span>

````powershell   
Set-AzureADPolicy -Definition $policyValue -Id $currentpolicy.Id 
````

<span data-ttu-id="da872-171">To get the policy, use the [Get-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/get-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="da872-171">To get the policy, use the [Get-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/get-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span></span> <span data-ttu-id="da872-172">For example:</span><span class="sxs-lookup"><span data-stu-id="da872-172">For example:</span></span>

````powershell
$currentpolicy = Get-AzureADPolicy | ?{$_.Type -eq 'B2BManagementPolicy'} | select -First 1 
````

<span data-ttu-id="da872-173">To remove the policy, use the [Remove-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/remove-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="da872-173">To remove the policy, use the [Remove-AzureADPolicy](https://docs.microsoft.com/powershell/module/azuread/remove-azureadpolicy?view=azureadps-2.0-preview) cmdlet.</span></span> <span data-ttu-id="da872-174">For example:</span><span class="sxs-lookup"><span data-stu-id="da872-174">For example:</span></span>

````powershell
Remove-AzureADPolicy -Id $currentpolicy.Id 
````

## <a name="next-steps"></a><span data-ttu-id="da872-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="da872-175">Next steps</span></span>

- <span data-ttu-id="da872-176">For an overview of Azure AD B2B, see [What is Azure AD B2B collaboration?](what-is-b2b.md)</span><span class="sxs-lookup"><span data-stu-id="da872-176">For an overview of Azure AD B2B, see [What is Azure AD B2B collaboration?](what-is-b2b.md)</span></span>
- <span data-ttu-id="da872-177">For information about conditional access and B2B collaboration, see [Conditional access for B2B collaboration users](conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="da872-177">For information about conditional access and B2B collaboration, see [Conditional access for B2B collaboration users](conditional-access.md).</span></span>



