---
title: Azure Stack 1805 Update | Microsoft Docs
description: Learn about what's new in the 1805 update for Azure Stack integrated systems, including the known issues and where to download the update.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2018
ms.author: brenduns
ms.reviewer: justini
ms.openlocfilehash: 4db0ce5e877f3054cc41e8940e8d9e672f7632c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869178"
---
# <a name="azure-stack-1805-update"></a><span data-ttu-id="8c86f-103">Azure Stack 1805 update</span><span class="sxs-lookup"><span data-stu-id="8c86f-103">Azure Stack 1805 update</span></span>

<span data-ttu-id="8c86f-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="8c86f-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="8c86f-105">This article describes the improvements and fixes in the 1805 update package, known issues for this version, and where to download the update.</span><span class="sxs-lookup"><span data-stu-id="8c86f-105">This article describes the improvements and fixes in the 1805 update package, known issues for this version, and where to download the update.</span></span> <span data-ttu-id="8c86f-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="8c86f-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span></span>

> [!IMPORTANT]        
> <span data-ttu-id="8c86f-107">This update package is only for Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="8c86f-107">This update package is only for Azure Stack integrated systems.</span></span> <span data-ttu-id="8c86f-108">Do not apply this update package to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="8c86f-108">Do not apply this update package to the Azure Stack Development Kit.</span></span>

## <a name="build-reference"></a><span data-ttu-id="8c86f-109">Build reference</span><span class="sxs-lookup"><span data-stu-id="8c86f-109">Build reference</span></span>    
<span data-ttu-id="8c86f-110">The Azure Stack 1805 update build number is **1.1805.1.47**.</span><span class="sxs-lookup"><span data-stu-id="8c86f-110">The Azure Stack 1805 update build number is **1.1805.1.47**.</span></span>  

> [!TIP]  
> <span data-ttu-id="8c86f-111">Based on customer feedback, there is an update to the version schema in use for Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-111">Based on customer feedback, there is an update to the version schema in use for Microsoft Azure Stack.</span></span>  <span data-ttu-id="8c86f-112">Starting with this update, 1805, the new schema better represents the current cloud version.</span><span class="sxs-lookup"><span data-stu-id="8c86f-112">Starting with this update, 1805, the new schema better represents the current cloud version.</span></span>  
> 
> <span data-ttu-id="8c86f-113">The version schema is now *Version.YearYearMonthMonth.MinorVersion.BuildNumber* where the second and third sets indicate the version and release.</span><span class="sxs-lookup"><span data-stu-id="8c86f-113">The version schema is now *Version.YearYearMonthMonth.MinorVersion.BuildNumber* where the second and third sets indicate the version and release.</span></span> <span data-ttu-id="8c86f-114">For example, 1805.1 represents the *release to manufacturing* (RTM) version of 1805.</span><span class="sxs-lookup"><span data-stu-id="8c86f-114">For example, 1805.1 represents the *release to manufacturing* (RTM) version of 1805.</span></span>  


### <a name="new-features"></a><span data-ttu-id="8c86f-115">New features</span><span class="sxs-lookup"><span data-stu-id="8c86f-115">New features</span></span>
<span data-ttu-id="8c86f-116">This update includes the following improvements for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-116">This update includes the following improvements for Azure Stack.</span></span>
<!-- 2297790 - IS, ASDK --> 
- <span data-ttu-id="8c86f-117">**Azure Stack now includes a *Syslog* client** as a *preview feature*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-117">**Azure Stack now includes a *Syslog* client** as a *preview feature*.</span></span> <span data-ttu-id="8c86f-118">This client allows the forwarding of audit and security logs related to the Azure Stack infrastructure to a Syslog server or security information and event management (SIEM) software that is external to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-118">This client allows the forwarding of audit and security logs related to the Azure Stack infrastructure to a Syslog server or security information and event management (SIEM) software that is external to Azure Stack.</span></span> <span data-ttu-id="8c86f-119">Currently, the Syslog client only supports unauthenticated UDP connections over default port 514.</span><span class="sxs-lookup"><span data-stu-id="8c86f-119">Currently, the Syslog client only supports unauthenticated UDP connections over default port 514.</span></span> <span data-ttu-id="8c86f-120">The payload of each Syslog message is formatted in Common Event Format (CEF).</span><span class="sxs-lookup"><span data-stu-id="8c86f-120">The payload of each Syslog message is formatted in Common Event Format (CEF).</span></span> 

  <span data-ttu-id="8c86f-121">To configure the Syslog client, use  the **Set-SyslogServer** cmdlet exposed in the Privileged Endpoint.</span><span class="sxs-lookup"><span data-stu-id="8c86f-121">To configure the Syslog client, use  the **Set-SyslogServer** cmdlet exposed in the Privileged Endpoint.</span></span> 

  <span data-ttu-id="8c86f-122">With this preview, you might see the following three alerts.</span><span class="sxs-lookup"><span data-stu-id="8c86f-122">With this preview, you might see the following three alerts.</span></span> <span data-ttu-id="8c86f-123">When presented by Azure Stack, these alerts include *descriptions* and *remediation* guidance.</span><span class="sxs-lookup"><span data-stu-id="8c86f-123">When presented by Azure Stack, these alerts include *descriptions* and *remediation* guidance.</span></span> 
  - <span data-ttu-id="8c86f-124">TITLE: Code Integrity Off</span><span class="sxs-lookup"><span data-stu-id="8c86f-124">TITLE: Code Integrity Off</span></span>  
  - <span data-ttu-id="8c86f-125">TITLE: Code Integrity in Audit Mode</span><span class="sxs-lookup"><span data-stu-id="8c86f-125">TITLE: Code Integrity in Audit Mode</span></span> 
  - <span data-ttu-id="8c86f-126">TITLE: User Account Created</span><span class="sxs-lookup"><span data-stu-id="8c86f-126">TITLE: User Account Created</span></span>

  <span data-ttu-id="8c86f-127">While this feature is in preview, it should not be relied upon in production environments.</span><span class="sxs-lookup"><span data-stu-id="8c86f-127">While this feature is in preview, it should not be relied upon in production environments.</span></span>   




### <a name="fixed-issues"></a><span data-ttu-id="8c86f-128">Fixed issues</span><span class="sxs-lookup"><span data-stu-id="8c86f-128">Fixed issues</span></span>

<!-- # - applicability -->
- <span data-ttu-id="8c86f-129">We fixed the issue that blocked [opening a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the admin portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-129">We fixed the issue that blocked [opening a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the admin portal.</span></span> <span data-ttu-id="8c86f-130">This option now works as intended.</span><span class="sxs-lookup"><span data-stu-id="8c86f-130">This option now works as intended.</span></span> 

- <span data-ttu-id="8c86f-131">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-131">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span></span>


<!-- # Additional releases timed with this update    -->



## <a name="before-you-begin"></a><span data-ttu-id="8c86f-132">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8c86f-132">Before you begin</span></span>    

### <a name="prerequisites"></a><span data-ttu-id="8c86f-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c86f-133">Prerequisites</span></span>
- <span data-ttu-id="8c86f-134">Install the Azure Stack [1804 Update](azure-stack-update-1804.md) before you apply the Azure Stack 1805 update.</span><span class="sxs-lookup"><span data-stu-id="8c86f-134">Install the Azure Stack [1804 Update](azure-stack-update-1804.md) before you apply the Azure Stack 1805 update.</span></span>  
- <span data-ttu-id="8c86f-135">Install the latest available [update or hotfix for version 1804](azure-stack-update-1804.md#post-update-steps).</span><span class="sxs-lookup"><span data-stu-id="8c86f-135">Install the latest available [update or hotfix for version 1804](azure-stack-update-1804.md#post-update-steps).</span></span>   
- <span data-ttu-id="8c86f-136">Before you start installation of update 1805, run [Test-AzureStack](azure-stack-diagnostic-test.md) to validate the status of your Azure Stack and resolve any operational issues found.</span><span class="sxs-lookup"><span data-stu-id="8c86f-136">Before you start installation of update 1805, run [Test-AzureStack](azure-stack-diagnostic-test.md) to validate the status of your Azure Stack and resolve any operational issues found.</span></span> <span data-ttu-id="8c86f-137">Also review active alerts, and resolve any that require action.</span><span class="sxs-lookup"><span data-stu-id="8c86f-137">Also review active alerts, and resolve any that require action.</span></span> 

### <a name="known-issues-with-the-update-process"></a><span data-ttu-id="8c86f-138">Known issues with the update process</span><span class="sxs-lookup"><span data-stu-id="8c86f-138">Known issues with the update process</span></span>   
- <span data-ttu-id="8c86f-139">During installation of the 1805 update, you might see alerts with the title *Error – Template for FaultType UserAccounts.New is missing.*</span><span class="sxs-lookup"><span data-stu-id="8c86f-139">During installation of the 1805 update, you might see alerts with the title *Error – Template for FaultType UserAccounts.New is missing.*</span></span>  <span data-ttu-id="8c86f-140">You can safely ignore these alerts.</span><span class="sxs-lookup"><span data-stu-id="8c86f-140">You can safely ignore these alerts.</span></span> <span data-ttu-id="8c86f-141">These alerts will close automatically after the update to 1805 completes.</span><span class="sxs-lookup"><span data-stu-id="8c86f-141">These alerts will close automatically after the update to 1805 completes.</span></span>   

- <span data-ttu-id="8c86f-142"><!-- 2489559 - IS --> Do not attempt to create virtual machines during the installation of this update.</span><span class="sxs-lookup"><span data-stu-id="8c86f-142"><!-- 2489559 - IS --> Do not attempt to create virtual machines during the installation of this update.</span></span> <span data-ttu-id="8c86f-143">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span><span class="sxs-lookup"><span data-stu-id="8c86f-143">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span></span>


### <a name="post-update-steps"></a><span data-ttu-id="8c86f-144">Post-update steps</span><span class="sxs-lookup"><span data-stu-id="8c86f-144">Post-update steps</span></span>
<span data-ttu-id="8c86f-145">After the installation of 1805, install any applicable Hotfixes.</span><span class="sxs-lookup"><span data-stu-id="8c86f-145">After the installation of 1805, install any applicable Hotfixes.</span></span> <span data-ttu-id="8c86f-146">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8c86f-146">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span></span>  
 - <span data-ttu-id="8c86f-147">[KB 4344102 - Azure Stack Hotfix 1.1805.7.57](https://support.microsoft.com/help/4344102).</span><span class="sxs-lookup"><span data-stu-id="8c86f-147">[KB 4344102 - Azure Stack Hotfix 1.1805.7.57](https://support.microsoft.com/help/4344102).</span></span>


## <a name="known-issues-post-installation"></a><span data-ttu-id="8c86f-148">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="8c86f-148">Known issues (post-installation)</span></span>
<span data-ttu-id="8c86f-149">The following are post-installation known issues for this build version.</span><span class="sxs-lookup"><span data-stu-id="8c86f-149">The following are post-installation known issues for this build version.</span></span>

### <a name="portal"></a><span data-ttu-id="8c86f-150">Portal</span><span class="sxs-lookup"><span data-stu-id="8c86f-150">Portal</span></span>  
- <span data-ttu-id="8c86f-151"><!-- 2931230 – IS  ASDK --> Plans that are added to a user subscription as an add-on plan cannot be deleted, even when you remove the plan from the user subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-151"><!-- 2931230 – IS  ASDK --> Plans that are added to a user subscription as an add-on plan cannot be deleted, even when you remove the plan from the user subscription.</span></span> <span data-ttu-id="8c86f-152">The plan will remain until the subscriptions that reference the add-on plan are also deleted.</span><span class="sxs-lookup"><span data-stu-id="8c86f-152">The plan will remain until the subscriptions that reference the add-on plan are also deleted.</span></span> 

- <span data-ttu-id="8c86f-153"><!-- TBD - IS ASDK --> You cannot apply driver updates by using an OEM Extension package with this version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-153"><!-- TBD - IS ASDK --> You cannot apply driver updates by using an OEM Extension package with this version of Azure Stack.</span></span>  <span data-ttu-id="8c86f-154">There is no workaround for this problem.</span><span class="sxs-lookup"><span data-stu-id="8c86f-154">There is no workaround for this problem.</span></span>

- <span data-ttu-id="8c86f-155"><!-- 2551834 - IS, ASDK --> When you select **Overview** for a storage account in either the admin or user portals, the information from the *Essentials* pane does not display.</span><span class="sxs-lookup"><span data-stu-id="8c86f-155"><!-- 2551834 - IS, ASDK --> When you select **Overview** for a storage account in either the admin or user portals, the information from the *Essentials* pane does not display.</span></span>  <span data-ttu-id="8c86f-156">The Essentials pane displays information about the account like its *Resource group*, *Location*, and *Subscription ID*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-156">The Essentials pane displays information about the account like its *Resource group*, *Location*, and *Subscription ID*.</span></span>  <span data-ttu-id="8c86f-157">Other options for Overview  are accessible, like *Services* and *Monitoring*, as well as options to *Open in Explorer* or to *Delete storage account*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-157">Other options for Overview  are accessible, like *Services* and *Monitoring*, as well as options to *Open in Explorer* or to *Delete storage account*.</span></span> 

  <span data-ttu-id="8c86f-158">To view the unavailable information, use the [Get-azureRMstorageaccount](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccount?view=azurermps-6.2.0) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c86f-158">To view the unavailable information, use the [Get-azureRMstorageaccount](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccount?view=azurermps-6.2.0) PowerShell cmdlet.</span></span> 

- <span data-ttu-id="8c86f-159"><!-- 2551834 - IS, ASDK --> When you select **Tags** for a storage account in either the admin or user portals, the information fails to load and does not display.</span><span class="sxs-lookup"><span data-stu-id="8c86f-159"><!-- 2551834 - IS, ASDK --> When you select **Tags** for a storage account in either the admin or user portals, the information fails to load and does not display.</span></span>  

  <span data-ttu-id="8c86f-160">To view the unavailable information, use the [Get-AzureRmTag](https://docs.microsoft.com/powershell/module/azurerm.tags/get-azurermtag?view=azurermps-6.2.0) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c86f-160">To view the unavailable information, use the [Get-AzureRmTag](https://docs.microsoft.com/powershell/module/azurerm.tags/get-azurermtag?view=azurermps-6.2.0) PowerShell cmdlet.</span></span>


- <span data-ttu-id="8c86f-161"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span><span class="sxs-lookup"><span data-stu-id="8c86f-161"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span></span>  
  <span data-ttu-id="8c86f-162">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-162">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span></span>   

- <span data-ttu-id="8c86f-163"><!-- TBD - IS ASDK --> Some administrative subscription types are not available.</span><span class="sxs-lookup"><span data-stu-id="8c86f-163"><!-- TBD - IS ASDK --> Some administrative subscription types are not available.</span></span>  <span data-ttu-id="8c86f-164">When you upgrade Azure Stack to this version, the two subscription types that were [introduced with version 1804](azure-stack-update-1804.md#new-features) are not visible in the console.</span><span class="sxs-lookup"><span data-stu-id="8c86f-164">When you upgrade Azure Stack to this version, the two subscription types that were [introduced with version 1804](azure-stack-update-1804.md#new-features) are not visible in the console.</span></span> <span data-ttu-id="8c86f-165">This is expected.</span><span class="sxs-lookup"><span data-stu-id="8c86f-165">This is expected.</span></span> <span data-ttu-id="8c86f-166">The unavailable subscription types are *Metering subscription*, and *Consumption subscription*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-166">The unavailable subscription types are *Metering subscription*, and *Consumption subscription*.</span></span> <span data-ttu-id="8c86f-167">These subscription types are visible in new Azure Stack environments beginning with version 1804 but are not yet ready for use.</span><span class="sxs-lookup"><span data-stu-id="8c86f-167">These subscription types are visible in new Azure Stack environments beginning with version 1804 but are not yet ready for use.</span></span> <span data-ttu-id="8c86f-168">You should continue to use the *Default Provider* subscription type.</span><span class="sxs-lookup"><span data-stu-id="8c86f-168">You should continue to use the *Default Provider* subscription type.</span></span>  

- <span data-ttu-id="8c86f-169"><!-- 2403291 - IS ASDK --> You might not have use of the horizontal scroll bar along the bottom of the admin and user portals.</span><span class="sxs-lookup"><span data-stu-id="8c86f-169"><!-- 2403291 - IS ASDK --> You might not have use of the horizontal scroll bar along the bottom of the admin and user portals.</span></span> <span data-ttu-id="8c86f-170">If you can’t access the horizontal scroll bar, use the breadcrumbs to navigate to a previous blade in the portal by selecting the name of the blade you want to view from the breadcrumb list found at the top left of the portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-170">If you can’t access the horizontal scroll bar, use the breadcrumbs to navigate to a previous blade in the portal by selecting the name of the blade you want to view from the breadcrumb list found at the top left of the portal.</span></span>
  <span data-ttu-id="8c86f-171">![Breadcrumb](media/azure-stack-update-1804/breadcrumb.png)</span><span class="sxs-lookup"><span data-stu-id="8c86f-171">![Breadcrumb](media/azure-stack-update-1804/breadcrumb.png)</span></span>

- <span data-ttu-id="8c86f-172"><!-- TBD - IS --> It might not be possible to view compute or storage resources in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-172"><!-- TBD - IS --> It might not be possible to view compute or storage resources in the administrator portal.</span></span> <span data-ttu-id="8c86f-173">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span><span class="sxs-lookup"><span data-stu-id="8c86f-173">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span></span> <span data-ttu-id="8c86f-174">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span><span class="sxs-lookup"><span data-stu-id="8c86f-174">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span></span>

- <span data-ttu-id="8c86f-175"><!-- TBD - IS --> You might see a blank dashboard in the portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-175"><!-- TBD - IS --> You might see a blank dashboard in the portal.</span></span> <span data-ttu-id="8c86f-176">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span><span class="sxs-lookup"><span data-stu-id="8c86f-176">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span></span>

- <span data-ttu-id="8c86f-177"><!-- TBD - IS ASDK --> Deleting user subscriptions results in orphaned resources.</span><span class="sxs-lookup"><span data-stu-id="8c86f-177"><!-- TBD - IS ASDK --> Deleting user subscriptions results in orphaned resources.</span></span> <span data-ttu-id="8c86f-178">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8c86f-178">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span></span>

- <span data-ttu-id="8c86f-179"><!-- TBD - IS ASDK --> You cannot view permissions to your subscription using the Azure Stack portals.</span><span class="sxs-lookup"><span data-stu-id="8c86f-179"><!-- TBD - IS ASDK --> You cannot view permissions to your subscription using the Azure Stack portals.</span></span> <span data-ttu-id="8c86f-180">As a workaround, use PowerShell to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="8c86f-180">As a workaround, use PowerShell to verify permissions.</span></span>


### <a name="health-and-monitoring"></a><span data-ttu-id="8c86f-181">Health and monitoring</span><span class="sxs-lookup"><span data-stu-id="8c86f-181">Health and monitoring</span></span>
- <span data-ttu-id="8c86f-182"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span><span class="sxs-lookup"><span data-stu-id="8c86f-182"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span></span>  
- 
   <span data-ttu-id="8c86f-183">Alert #1:</span><span class="sxs-lookup"><span data-stu-id="8c86f-183">Alert #1:</span></span>
   - <span data-ttu-id="8c86f-184">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="8c86f-184">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="8c86f-185">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="8c86f-185">SEVERITY: Warning</span></span>
   - <span data-ttu-id="8c86f-186">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="8c86f-186">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="8c86f-187">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="8c86f-187">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span></span> <span data-ttu-id="8c86f-188">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="8c86f-188">This may affect health reports and metrics.</span></span>  

  <span data-ttu-id="8c86f-189">Alert #2:</span><span class="sxs-lookup"><span data-stu-id="8c86f-189">Alert #2:</span></span>
   - <span data-ttu-id="8c86f-190">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="8c86f-190">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="8c86f-191">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="8c86f-191">SEVERITY: Warning</span></span>
   - <span data-ttu-id="8c86f-192">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="8c86f-192">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="8c86f-193">DESCRIPTION: The health controller Fault Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="8c86f-193">DESCRIPTION: The health controller Fault Scanner is unavailable.</span></span> <span data-ttu-id="8c86f-194">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="8c86f-194">This may affect health reports and metrics.</span></span>

  <span data-ttu-id="8c86f-195">Both alerts #1 and #2 can be safely ignored and they'll close automatically over time.</span><span class="sxs-lookup"><span data-stu-id="8c86f-195">Both alerts #1 and #2 can be safely ignored and they'll close automatically over time.</span></span> 

  <span data-ttu-id="8c86f-196">You might also see the following alert for *Capacity*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-196">You might also see the following alert for *Capacity*.</span></span> <span data-ttu-id="8c86f-197">For this alert, the percentage of available memory identified in the description can vary:</span><span class="sxs-lookup"><span data-stu-id="8c86f-197">For this alert, the percentage of available memory identified in the description can vary:</span></span>  

  <span data-ttu-id="8c86f-198">Alert #3:</span><span class="sxs-lookup"><span data-stu-id="8c86f-198">Alert #3:</span></span>
   - <span data-ttu-id="8c86f-199">NAME:  Low memory capacity</span><span class="sxs-lookup"><span data-stu-id="8c86f-199">NAME:  Low memory capacity</span></span>
   - <span data-ttu-id="8c86f-200">SEVERITY: Critical</span><span class="sxs-lookup"><span data-stu-id="8c86f-200">SEVERITY: Critical</span></span>
   - <span data-ttu-id="8c86f-201">COMPONENT: Capacity</span><span class="sxs-lookup"><span data-stu-id="8c86f-201">COMPONENT: Capacity</span></span>
   - <span data-ttu-id="8c86f-202">DESCRIPTION: The region has consumed more than 80.00% of available memory.</span><span class="sxs-lookup"><span data-stu-id="8c86f-202">DESCRIPTION: The region has consumed more than 80.00% of available memory.</span></span> <span data-ttu-id="8c86f-203">Creating virtual machines with large amounts of memory may fail.</span><span class="sxs-lookup"><span data-stu-id="8c86f-203">Creating virtual machines with large amounts of memory may fail.</span></span>  

  <span data-ttu-id="8c86f-204">In this version of Azure Stack, this alert can fire incorrectly.</span><span class="sxs-lookup"><span data-stu-id="8c86f-204">In this version of Azure Stack, this alert can fire incorrectly.</span></span> <span data-ttu-id="8c86f-205">If tenant virtual machines continue to deploy successfully, you can safely ignore this alert.</span><span class="sxs-lookup"><span data-stu-id="8c86f-205">If tenant virtual machines continue to deploy successfully, you can safely ignore this alert.</span></span> 
  
  <span data-ttu-id="8c86f-206">Alert #3 does not automatically close.</span><span class="sxs-lookup"><span data-stu-id="8c86f-206">Alert #3 does not automatically close.</span></span> <span data-ttu-id="8c86f-207">If you close this alert Azure Stack will create the same alert within 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="8c86f-207">If you close this alert Azure Stack will create the same alert within 15 minutes.</span></span>  

- <span data-ttu-id="8c86f-208"><!-- 2368581 - IS. ASDK --> As an Azure Stack operator, if you receive a low memory alert and tenant virtual machines fail to deploy with a *Fabric VM creation error*, it is possible that the Azure Stack stamp is out of available memory.</span><span class="sxs-lookup"><span data-stu-id="8c86f-208"><!-- 2368581 - IS. ASDK --> As an Azure Stack operator, if you receive a low memory alert and tenant virtual machines fail to deploy with a *Fabric VM creation error*, it is possible that the Azure Stack stamp is out of available memory.</span></span> <span data-ttu-id="8c86f-209">Use the [Azure Stack Capacity Planner](https://gallery.technet.microsoft.com/Azure-Stack-Capacity-24ccd822) to best understand the capacity available for your workloads.</span><span class="sxs-lookup"><span data-stu-id="8c86f-209">Use the [Azure Stack Capacity Planner](https://gallery.technet.microsoft.com/Azure-Stack-Capacity-24ccd822) to best understand the capacity available for your workloads.</span></span> 


### <a name="compute"></a><span data-ttu-id="8c86f-210">Compute</span><span class="sxs-lookup"><span data-stu-id="8c86f-210">Compute</span></span>
- <span data-ttu-id="8c86f-211"><!-- TBD - IS, ASDK --> When selecting a virtual machine size for a virtual machine deployment, some F-Series VM sizes are not visible as part of the size selector when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="8c86f-211"><!-- TBD - IS, ASDK --> When selecting a virtual machine size for a virtual machine deployment, some F-Series VM sizes are not visible as part of the size selector when you create a VM.</span></span> <span data-ttu-id="8c86f-212">The following VM sizes do not appear in the selector: *F8s_v2*, *F16s_v2*, *F32s_v2*, and *F64s_v2*.</span><span class="sxs-lookup"><span data-stu-id="8c86f-212">The following VM sizes do not appear in the selector: *F8s_v2*, *F16s_v2*, *F32s_v2*, and *F64s_v2*.</span></span>  
  <span data-ttu-id="8c86f-213">As a workaround, use one of the following methods to deploy a VM.</span><span class="sxs-lookup"><span data-stu-id="8c86f-213">As a workaround, use one of the following methods to deploy a VM.</span></span> <span data-ttu-id="8c86f-214">In each method, you need to specify the VM size you want to use.</span><span class="sxs-lookup"><span data-stu-id="8c86f-214">In each method, you need to specify the VM size you want to use.</span></span>

  - <span data-ttu-id="8c86f-215">**Azure Resource Manager template:** When you use a template, set the *vmSize* in the template to equal the VM size you want to use.</span><span class="sxs-lookup"><span data-stu-id="8c86f-215">**Azure Resource Manager template:** When you use a template, set the *vmSize* in the template to equal the VM size you want to use.</span></span> <span data-ttu-id="8c86f-216">For example, the following entry is used to deploy a VM that uses the *F32s_v2* size:</span><span class="sxs-lookup"><span data-stu-id="8c86f-216">For example, the following entry is used to deploy a VM that uses the *F32s_v2* size:</span></span>  

    ```
        "properties": {
        "hardwareProfile": {
                "vmSize": "Standard_F32s_v2"
        },
    ```  
  - <span data-ttu-id="8c86f-217">**Azure CLI:** You can use the [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) command and specify the VM size as a parameter, similar to `--size "Standard_F32s_v2"`.</span><span class="sxs-lookup"><span data-stu-id="8c86f-217">**Azure CLI:** You can use the [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) command and specify the VM size as a parameter, similar to `--size "Standard_F32s_v2"`.</span></span>

  - <span data-ttu-id="8c86f-218">**PowerShell:** With PowerShell you can use [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) with the parameter that specifies the VM size, similar to `-VMSize "Standard_F32s_v2"`.</span><span class="sxs-lookup"><span data-stu-id="8c86f-218">**PowerShell:** With PowerShell you can use [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) with the parameter that specifies the VM size, similar to `-VMSize "Standard_F32s_v2"`.</span></span>


- <span data-ttu-id="8c86f-219"><!-- TBD - IS ASDK --> Scaling settings for virtual machine scale sets are not available in the portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-219"><!-- TBD - IS ASDK --> Scaling settings for virtual machine scale sets are not available in the portal.</span></span> <span data-ttu-id="8c86f-220">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span><span class="sxs-lookup"><span data-stu-id="8c86f-220">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span></span> <span data-ttu-id="8c86f-221">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span><span class="sxs-lookup"><span data-stu-id="8c86f-221">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span></span>

- <span data-ttu-id="8c86f-222"><!-- TBD - IS --> When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span><span class="sxs-lookup"><span data-stu-id="8c86f-222"><!-- TBD - IS --> When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span></span> <span data-ttu-id="8c86f-223">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-223">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span></span>

- <span data-ttu-id="8c86f-224"><!-- TBD - IS ASDK --> When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a DS series VM.</span><span class="sxs-lookup"><span data-stu-id="8c86f-224"><!-- TBD - IS ASDK --> When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a DS series VM.</span></span> <span data-ttu-id="8c86f-225">DS series VMs can accommodate as many data disks as the Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="8c86f-225">DS series VMs can accommodate as many data disks as the Azure configuration.</span></span>

- <span data-ttu-id="8c86f-226"><!-- TBD - IS ASDK --> When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span><span class="sxs-lookup"><span data-stu-id="8c86f-226"><!-- TBD - IS ASDK --> When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span></span>

  <span data-ttu-id="8c86f-227">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span><span class="sxs-lookup"><span data-stu-id="8c86f-227">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span></span> <span data-ttu-id="8c86f-228">This process should fix the problem that prevents deleting the failed item.</span><span class="sxs-lookup"><span data-stu-id="8c86f-228">This process should fix the problem that prevents deleting the failed item.</span></span> <span data-ttu-id="8c86f-229">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span><span class="sxs-lookup"><span data-stu-id="8c86f-229">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span></span>

  <span data-ttu-id="8c86f-230">You can then try to redownload the VM image that previously failed.</span><span class="sxs-lookup"><span data-stu-id="8c86f-230">You can then try to redownload the VM image that previously failed.</span></span>

- <span data-ttu-id="8c86f-231"><!-- TBD - IS ASDK --> If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span><span class="sxs-lookup"><span data-stu-id="8c86f-231"><!-- TBD - IS ASDK --> If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span></span>  

- <span data-ttu-id="8c86f-232"><!-- 1662991 IS ASDK --> Linux VM diagnostics is not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-232"><!-- 1662991 IS ASDK --> Linux VM diagnostics is not supported in Azure Stack.</span></span> <span data-ttu-id="8c86f-233">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="8c86f-233">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span></span> <span data-ttu-id="8c86f-234">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="8c86f-234">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span></span>  


### <a name="networking"></a><span data-ttu-id="8c86f-235">Networking</span><span class="sxs-lookup"><span data-stu-id="8c86f-235">Networking</span></span>
- <span data-ttu-id="8c86f-236"><!-- TBD - IS ASDK --> You cannot create user-defined routes in either the admin or user portal.</span><span class="sxs-lookup"><span data-stu-id="8c86f-236"><!-- TBD - IS ASDK --> You cannot create user-defined routes in either the admin or user portal.</span></span> <span data-ttu-id="8c86f-237">As a workaround, use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-powershell).</span><span class="sxs-lookup"><span data-stu-id="8c86f-237">As a workaround, use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-powershell).</span></span>

- <span data-ttu-id="8c86f-238"><!-- 1766332 - IS ASDK --> Under **Networking**, if you click **Create VPN Gateway** to set up a VPN connection, **Policy Based** is listed as a VPN type.</span><span class="sxs-lookup"><span data-stu-id="8c86f-238"><!-- 1766332 - IS ASDK --> Under **Networking**, if you click **Create VPN Gateway** to set up a VPN connection, **Policy Based** is listed as a VPN type.</span></span> <span data-ttu-id="8c86f-239">Do not select this option.</span><span class="sxs-lookup"><span data-stu-id="8c86f-239">Do not select this option.</span></span> <span data-ttu-id="8c86f-240">Only the **Route Based** option is supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8c86f-240">Only the **Route Based** option is supported in Azure Stack.</span></span>

- <span data-ttu-id="8c86f-241"><!-- 2388980 - IS ASDK --> After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span><span class="sxs-lookup"><span data-stu-id="8c86f-241"><!-- 2388980 - IS ASDK --> After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span></span> <span data-ttu-id="8c86f-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span><span class="sxs-lookup"><span data-stu-id="8c86f-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span></span>

  <span data-ttu-id="8c86f-243">Currently, you must use only new public IP addresses for new VMs you create.</span><span class="sxs-lookup"><span data-stu-id="8c86f-243">Currently, you must use only new public IP addresses for new VMs you create.</span></span>

  <span data-ttu-id="8c86f-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span><span class="sxs-lookup"><span data-stu-id="8c86f-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span></span> <span data-ttu-id="8c86f-245">All future attempts to connect through this IP address result in a connection to the original VM, and not to the new one.</span><span class="sxs-lookup"><span data-stu-id="8c86f-245">All future attempts to connect through this IP address result in a connection to the original VM, and not to the new one.</span></span>

- <span data-ttu-id="8c86f-246"><!-- 2292271 - IS ASDK --> If you raise a Quota limit for a Network resource that is part of an Offer and Plan that is associated with a tenant subscription, the new limit is not applied to that subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-246"><!-- 2292271 - IS ASDK --> If you raise a Quota limit for a Network resource that is part of an Offer and Plan that is associated with a tenant subscription, the new limit is not applied to that subscription.</span></span> <span data-ttu-id="8c86f-247">However, the new limit does apply to new subscriptions that are created after the quota is increased.</span><span class="sxs-lookup"><span data-stu-id="8c86f-247">However, the new limit does apply to new subscriptions that are created after the quota is increased.</span></span>

  <span data-ttu-id="8c86f-248">To work around this problem, use an Add-On plan to increase a Network Quota when the plan is already associated with a subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-248">To work around this problem, use an Add-On plan to increase a Network Quota when the plan is already associated with a subscription.</span></span> <span data-ttu-id="8c86f-249">For more information, see how to [make an add-on plan available](azure-stack-subscribe-plan-provision-vm.md#to-make-an-add-on-plan-available).</span><span class="sxs-lookup"><span data-stu-id="8c86f-249">For more information, see how to [make an add-on plan available](azure-stack-subscribe-plan-provision-vm.md#to-make-an-add-on-plan-available).</span></span>

- <span data-ttu-id="8c86f-250"><!-- 2304134 IS ASDK --> You cannot delete a subscription that has DNS Zone resources or Route Table resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="8c86f-250"><!-- 2304134 IS ASDK --> You cannot delete a subscription that has DNS Zone resources or Route Table resources associated with it.</span></span> <span data-ttu-id="8c86f-251">To successfully delete the subscription, you must first delete DNS Zone and Route Table resources from the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-251">To successfully delete the subscription, you must first delete DNS Zone and Route Table resources from the tenant subscription.</span></span>


- <span data-ttu-id="8c86f-252"><!-- 1902460 - IS ASDK --> Azure Stack supports a single *local network gateway* per IP address.</span><span class="sxs-lookup"><span data-stu-id="8c86f-252"><!-- 1902460 - IS ASDK --> Azure Stack supports a single *local network gateway* per IP address.</span></span> <span data-ttu-id="8c86f-253">This is true across all tenant subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8c86f-253">This is true across all tenant subscriptions.</span></span> <span data-ttu-id="8c86f-254">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span><span class="sxs-lookup"><span data-stu-id="8c86f-254">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span></span>

- <span data-ttu-id="8c86f-255"><!-- 16309153 - IS ASDK --> On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span><span class="sxs-lookup"><span data-stu-id="8c86f-255"><!-- 16309153 - IS ASDK --> On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span></span> <span data-ttu-id="8c86f-256">The updated settings are not pushed to VMs in that Vnet.</span><span class="sxs-lookup"><span data-stu-id="8c86f-256">The updated settings are not pushed to VMs in that Vnet.</span></span>

- <span data-ttu-id="8c86f-257"><!-- TBD - IS ASDK --> Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="8c86f-257"><!-- TBD - IS ASDK --> Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span></span> <span data-ttu-id="8c86f-258">If the VM requires more than one network interface, they must be defined at deployment time.</span><span class="sxs-lookup"><span data-stu-id="8c86f-258">If the VM requires more than one network interface, they must be defined at deployment time.</span></span>

- <span data-ttu-id="8c86f-259"><!-- 2096388 IS --> You cannot use the admin portal to update rules for a network security group.</span><span class="sxs-lookup"><span data-stu-id="8c86f-259"><!-- 2096388 IS --> You cannot use the admin portal to update rules for a network security group.</span></span>

    <span data-ttu-id="8c86f-260">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c86f-260">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span></span>  <span data-ttu-id="8c86f-261">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span><span class="sxs-lookup"><span data-stu-id="8c86f-261">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span></span>  

    - <span data-ttu-id="8c86f-262">*Allow:*</span><span class="sxs-lookup"><span data-stu-id="8c86f-262">*Allow:*</span></span>

      ```powershell    
      Connect-AzureRmAccount -EnvironmentName AzureStackAdmin

      $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"

      $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"

      ##This doesn’t work. Need to set properties again even in case of edit

      #Set-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389" -NetworkSecurityGroup $nsg -Access Allow  

      Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
        -Name $RuleConfig_Inbound_Rdp_3389.Name `
        -Description "Inbound_Rdp_3389" `
        -Access Allow `
        -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
        -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
        -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
        -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
        -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
        -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
        -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange

      # Commit the changes back to NSG
      Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
      ```

    - <span data-ttu-id="8c86f-263">*Deny:*</span><span class="sxs-lookup"><span data-stu-id="8c86f-263">*Deny:*</span></span>

        ```powershell

        Connect-AzureRmAccount -EnvironmentName AzureStackAdmin

        $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"

        $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"

        ##This doesn’t work. Need to set properties again even in case of edit

        #Set-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389" -NetworkSecurityGroup $nsg -Access Allow  

        Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
          -Name $RuleConfig_Inbound_Rdp_3389.Name `
          -Description "Inbound_Rdp_3389" `
          -Access Deny `
          -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
          -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
          -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
          -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
          -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
          -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
          -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange

        # Commit the changes back to NSG
        Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
        ```


### <a name="sql-and-mysql"></a><span data-ttu-id="8c86f-264">SQL and MySQL</span><span class="sxs-lookup"><span data-stu-id="8c86f-264">SQL and MySQL</span></span>

- <span data-ttu-id="8c86f-265"><!-- TBD - IS --> Only the resource provider is supported to create items on servers that host SQL or MySQL.</span><span class="sxs-lookup"><span data-stu-id="8c86f-265"><!-- TBD - IS --> Only the resource provider is supported to create items on servers that host SQL or MySQL.</span></span> <span data-ttu-id="8c86f-266">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span><span class="sxs-lookup"><span data-stu-id="8c86f-266">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span></span>  

- <span data-ttu-id="8c86f-267"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** or **Tier** names when you create a SKU for the SQL and MySQL resource providers.</span><span class="sxs-lookup"><span data-stu-id="8c86f-267"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** or **Tier** names when you create a SKU for the SQL and MySQL resource providers.</span></span>


> [!NOTE]  
> <span data-ttu-id="8c86f-268"><!-- TBD - IS --> After you update to Azure Stack 1805, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span><span class="sxs-lookup"><span data-stu-id="8c86f-268"><!-- TBD - IS --> After you update to Azure Stack 1805, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span></span>  <span data-ttu-id="8c86f-269">We recommend you update SQL and MySQL when a new release becomes available.</span><span class="sxs-lookup"><span data-stu-id="8c86f-269">We recommend you update SQL and MySQL when a new release becomes available.</span></span> <span data-ttu-id="8c86f-270">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span><span class="sxs-lookup"><span data-stu-id="8c86f-270">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span></span> <span data-ttu-id="8c86f-271">For example, if you use version 1803, first apply version 1804, and then update to 1805.</span><span class="sxs-lookup"><span data-stu-id="8c86f-271">For example, if you use version 1803, first apply version 1804, and then update to 1805.</span></span>      
>   
> <span data-ttu-id="8c86f-272">The install of update 1805 does not affect the current use of SQL or MySQL resource providers by your users.</span><span class="sxs-lookup"><span data-stu-id="8c86f-272">The install of update 1805 does not affect the current use of SQL or MySQL resource providers by your users.</span></span>
> <span data-ttu-id="8c86f-273">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span><span class="sxs-lookup"><span data-stu-id="8c86f-273">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span></span>    



### <a name="app-service"></a><span data-ttu-id="8c86f-274">App Service</span><span class="sxs-lookup"><span data-stu-id="8c86f-274">App Service</span></span>
- <span data-ttu-id="8c86f-275"><!-- 2352906 - IS ASDK --> Users must register the storage resource provider before they create their first Azure Function in the subscription.</span><span class="sxs-lookup"><span data-stu-id="8c86f-275"><!-- 2352906 - IS ASDK --> Users must register the storage resource provider before they create their first Azure Function in the subscription.</span></span>

- <span data-ttu-id="8c86f-276"><!-- 2489178 - IS ASDK --> In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span><span class="sxs-lookup"><span data-stu-id="8c86f-276"><!-- 2489178 - IS ASDK --> In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span></span>

- <span data-ttu-id="8c86f-277"><!-- TBD - IS ASDK --> App Service can only be deployed into the *Default Provider subscription* at this time.</span><span class="sxs-lookup"><span data-stu-id="8c86f-277"><!-- TBD - IS ASDK --> App Service can only be deployed into the *Default Provider subscription* at this time.</span></span> <span data-ttu-id="8c86f-278">In a future update, App Service will deploy into the new *Metering subscription* that was introduced in Azure Stack 1804.</span><span class="sxs-lookup"><span data-stu-id="8c86f-278">In a future update, App Service will deploy into the new *Metering subscription* that was introduced in Azure Stack 1804.</span></span> <span data-ttu-id="8c86f-279">When Metering is supported for use, all existing deployments will be migrated to this new subscription type.</span><span class="sxs-lookup"><span data-stu-id="8c86f-279">When Metering is supported for use, all existing deployments will be migrated to this new subscription type.</span></span>


### <a name="usage"></a><span data-ttu-id="8c86f-280">Usage</span><span class="sxs-lookup"><span data-stu-id="8c86f-280">Usage</span></span>  
- <span data-ttu-id="8c86f-281"><!-- TBD - IS ASDK --> Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span><span class="sxs-lookup"><span data-stu-id="8c86f-281"><!-- TBD - IS ASDK --> Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span></span> <span data-ttu-id="8c86f-282">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span><span class="sxs-lookup"><span data-stu-id="8c86f-282">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span></span>


<!-- #### Identity -->
<!-- #### Marketplace -->


## <a name="download-the-update"></a><span data-ttu-id="8c86f-283">Download the update</span><span class="sxs-lookup"><span data-stu-id="8c86f-283">Download the update</span></span>
<span data-ttu-id="8c86f-284">You can download the Azure Stack 1805 update package from [here](https://aka.ms/azurestackupdatedownload).</span><span class="sxs-lookup"><span data-stu-id="8c86f-284">You can download the Azure Stack 1805 update package from [here](https://aka.ms/azurestackupdatedownload).</span></span>


## <a name="see-also"></a><span data-ttu-id="8c86f-285">See also</span><span class="sxs-lookup"><span data-stu-id="8c86f-285">See also</span></span>
- <span data-ttu-id="8c86f-286">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span><span class="sxs-lookup"><span data-stu-id="8c86f-286">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span></span>
- <span data-ttu-id="8c86f-287">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span><span class="sxs-lookup"><span data-stu-id="8c86f-287">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span></span>
- <span data-ttu-id="8c86f-288">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="8c86f-288">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span></span>
