---
title: Azure Stack 1802 Update | Microsoft Docs
description: Learn about what's in the 1802 update for Azure Stack integrated systems, the known issues, and where to download the update.
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
ms.date: 05/30/2018
ms.author: brenduns
ms.reviewer: justini
ms.openlocfilehash: af65ffc088c2beadf415b72ec284ef77f3e4f6d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869968"
---
# <a name="azure-stack-1802-update"></a><span data-ttu-id="a829d-103">Azure Stack 1802 update</span><span class="sxs-lookup"><span data-stu-id="a829d-103">Azure Stack 1802 update</span></span>

<span data-ttu-id="a829d-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="a829d-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="a829d-105">This article describes the improvements and fixes in the 1802 update package, known issues for this release, and where to download the update.</span><span class="sxs-lookup"><span data-stu-id="a829d-105">This article describes the improvements and fixes in the 1802 update package, known issues for this release, and where to download the update.</span></span> <span data-ttu-id="a829d-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="a829d-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span></span>

> [!IMPORTANT]        
> <span data-ttu-id="a829d-107">This update package is only for Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="a829d-107">This update package is only for Azure Stack integrated systems.</span></span> <span data-ttu-id="a829d-108">Do not apply this update package to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="a829d-108">Do not apply this update package to the Azure Stack Development Kit.</span></span>

## <a name="build-reference"></a><span data-ttu-id="a829d-109">Build reference</span><span class="sxs-lookup"><span data-stu-id="a829d-109">Build reference</span></span>    
<span data-ttu-id="a829d-110">The Azure Stack 1802 update build number is **20180302.1**.</span><span class="sxs-lookup"><span data-stu-id="a829d-110">The Azure Stack 1802 update build number is **20180302.1**.</span></span>  


## <a name="before-you-begin"></a><span data-ttu-id="a829d-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a829d-111">Before you begin</span></span>    
> [!IMPORTANT]    
> <span data-ttu-id="a829d-112">Do not attempt to create virtual machines during the installation of this update.</span><span class="sxs-lookup"><span data-stu-id="a829d-112">Do not attempt to create virtual machines during the installation of this update.</span></span> <span data-ttu-id="a829d-113">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span><span class="sxs-lookup"><span data-stu-id="a829d-113">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span></span>


### <a name="prerequisites"></a><span data-ttu-id="a829d-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a829d-114">Prerequisites</span></span>
- <span data-ttu-id="a829d-115">Install the Azure Stack [1712 Update](azure-stack-update-1712.md) before you apply the Azure Stack 1802 update.</span><span class="sxs-lookup"><span data-stu-id="a829d-115">Install the Azure Stack [1712 Update](azure-stack-update-1712.md) before you apply the Azure Stack 1802 update.</span></span>    

- <span data-ttu-id="a829d-116">Install **AzS Hotfix – 1.0.180312.1- Build 20180222.2** before you apply the Azure Stack 1802 update.</span><span class="sxs-lookup"><span data-stu-id="a829d-116">Install **AzS Hotfix – 1.0.180312.1- Build 20180222.2** before you apply the Azure Stack 1802 update.</span></span> <span data-ttu-id="a829d-117">This hotfix updates Windows Defender, and is available when you download updates for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-117">This hotfix updates Windows Defender, and is available when you download updates for Azure Stack.</span></span>

  <span data-ttu-id="a829d-118">To install the hotfix, follow the normal procedures for [installing updates for Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-118">To install the hotfix, follow the normal procedures for [installing updates for Azure Stack](azure-stack-apply-updates.md).</span></span> <span data-ttu-id="a829d-119">The name of the update appears as **AzS Hotfix – 1.0.180312.1**, and includes the following files:</span><span class="sxs-lookup"><span data-stu-id="a829d-119">The name of the update appears as **AzS Hotfix – 1.0.180312.1**, and includes the following files:</span></span> 
    - <span data-ttu-id="a829d-120">PUPackageHotFix_20180222.2-1.exe</span><span class="sxs-lookup"><span data-stu-id="a829d-120">PUPackageHotFix_20180222.2-1.exe</span></span>
    - <span data-ttu-id="a829d-121">PUPackageHotFix_20180222.2-1.bin</span><span class="sxs-lookup"><span data-stu-id="a829d-121">PUPackageHotFix_20180222.2-1.bin</span></span>
    - <span data-ttu-id="a829d-122">Metadata.xml</span><span class="sxs-lookup"><span data-stu-id="a829d-122">Metadata.xml</span></span>

  <span data-ttu-id="a829d-123">After uploading these files to a storage account and container, run the install from the Update tile in the admin portal.</span><span class="sxs-lookup"><span data-stu-id="a829d-123">After uploading these files to a storage account and container, run the install from the Update tile in the admin portal.</span></span> 
  
  <span data-ttu-id="a829d-124">Unlike updates to Azure Stack, installing this update does not change the version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-124">Unlike updates to Azure Stack, installing this update does not change the version of Azure Stack.</span></span>  <span data-ttu-id="a829d-125">To confirm this update is installed, view the list of **Installed updates**.</span><span class="sxs-lookup"><span data-stu-id="a829d-125">To confirm this update is installed, view the list of **Installed updates**.</span></span>
 


### <a name="post-update-steps"></a><span data-ttu-id="a829d-126">Post-update steps</span><span class="sxs-lookup"><span data-stu-id="a829d-126">Post-update steps</span></span>
<span data-ttu-id="a829d-127">After the installation of 1802, install any applicable Hotfixes.</span><span class="sxs-lookup"><span data-stu-id="a829d-127">After the installation of 1802, install any applicable Hotfixes.</span></span> <span data-ttu-id="a829d-128">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-128">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span></span> 
- <span data-ttu-id="a829d-129">Azure Stack hotfix **1.0.180302.4**.</span><span class="sxs-lookup"><span data-stu-id="a829d-129">Azure Stack hotfix **1.0.180302.4**.</span></span> [<span data-ttu-id="a829d-130">KB 4131152 - Existing Virtual Machine Scale Sets may become unusable</span><span class="sxs-lookup"><span data-stu-id="a829d-130">KB 4131152 - Existing Virtual Machine Scale Sets may become unusable</span></span>]( https://support.microsoft.com/help/4131152) 

  <span data-ttu-id="a829d-131">This fix also resolves the issues detailed in  [KB 4103348 - Network Controller API service crashes when you try to install an Azure Stack update](https://support.microsoft.com/help/4103348).</span><span class="sxs-lookup"><span data-stu-id="a829d-131">This fix also resolves the issues detailed in  [KB 4103348 - Network Controller API service crashes when you try to install an Azure Stack update](https://support.microsoft.com/help/4103348).</span></span>


### <a name="new-features-and-fixes"></a><span data-ttu-id="a829d-132">New features and fixes</span><span class="sxs-lookup"><span data-stu-id="a829d-132">New features and fixes</span></span>
<span data-ttu-id="a829d-133">This update includes the following improvements and fixes for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-133">This update includes the following improvements and fixes for Azure Stack.</span></span>

- <span data-ttu-id="a829d-134">**Support is added for the following Azure Storage Service API versions**:</span><span class="sxs-lookup"><span data-stu-id="a829d-134">**Support is added for the following Azure Storage Service API versions**:</span></span>
    - <span data-ttu-id="a829d-135">2017-04-17</span><span class="sxs-lookup"><span data-stu-id="a829d-135">2017-04-17</span></span> 
    - <span data-ttu-id="a829d-136">2016-05-31</span><span class="sxs-lookup"><span data-stu-id="a829d-136">2016-05-31</span></span> 
    - <span data-ttu-id="a829d-137">2015-12-11</span><span class="sxs-lookup"><span data-stu-id="a829d-137">2015-12-11</span></span> 
    - <span data-ttu-id="a829d-138">2015-07-08</span><span class="sxs-lookup"><span data-stu-id="a829d-138">2015-07-08</span></span> 
    
    <span data-ttu-id="a829d-139">For more information, see [Azure Stack Storage: Differences and considerations](/azure/azure-stack/user/azure-stack-acs-differences).</span><span class="sxs-lookup"><span data-stu-id="a829d-139">For more information, see [Azure Stack Storage: Differences and considerations](/azure/azure-stack/user/azure-stack-acs-differences).</span></span>

- <span data-ttu-id="a829d-140">**Support for larger [Block Blobs](azure-stack-acs-differences.md)**:</span><span class="sxs-lookup"><span data-stu-id="a829d-140">**Support for larger [Block Blobs](azure-stack-acs-differences.md)**:</span></span>
    - <span data-ttu-id="a829d-141">The maximum allowable block size is increased from 4 MB to 100 MB.</span><span class="sxs-lookup"><span data-stu-id="a829d-141">The maximum allowable block size is increased from 4 MB to 100 MB.</span></span>
    - <span data-ttu-id="a829d-142">The maximum blob size is increased from 195 GB to 4.75 TB.</span><span class="sxs-lookup"><span data-stu-id="a829d-142">The maximum blob size is increased from 195 GB to 4.75 TB.</span></span>  

- <span data-ttu-id="a829d-143">**Infrastructure backup** now appears in the Resource Providers tile, and alerts for backup are enabled.</span><span class="sxs-lookup"><span data-stu-id="a829d-143">**Infrastructure backup** now appears in the Resource Providers tile, and alerts for backup are enabled.</span></span> <span data-ttu-id="a829d-144">For more information about the Infrastructure Backup Service, see [Backup and data recovery for Azure Stack with the Infrastructure Backup Service](azure-stack-backup-infrastructure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-144">For more information about the Infrastructure Backup Service, see [Backup and data recovery for Azure Stack with the Infrastructure Backup Service](azure-stack-backup-infrastructure-backup.md).</span></span>

- <span data-ttu-id="a829d-145">**Update to the *Test-AzureStack* cmdlet** to improve diagnostics for storage.</span><span class="sxs-lookup"><span data-stu-id="a829d-145">**Update to the *Test-AzureStack* cmdlet** to improve diagnostics for storage.</span></span> <span data-ttu-id="a829d-146">For more information on this cmdlet, see [Validation for Azure Stack](azure-stack-diagnostic-test.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-146">For more information on this cmdlet, see [Validation for Azure Stack](azure-stack-diagnostic-test.md).</span></span>

- <span data-ttu-id="a829d-147">**Role-Based Access Control (RBAC) improvements** - You can now use RBAC to delegate permissions to Universal User Groups when Azure Stack is deployed with AD FS.</span><span class="sxs-lookup"><span data-stu-id="a829d-147">**Role-Based Access Control (RBAC) improvements** - You can now use RBAC to delegate permissions to Universal User Groups when Azure Stack is deployed with AD FS.</span></span> <span data-ttu-id="a829d-148">To learn more about RBAC, see [Manage RBAC](azure-stack-manage-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-148">To learn more about RBAC, see [Manage RBAC](azure-stack-manage-permissions.md).</span></span>

- <span data-ttu-id="a829d-149">**Support is added for multiple fault domains**.</span><span class="sxs-lookup"><span data-stu-id="a829d-149">**Support is added for multiple fault domains**.</span></span>  <span data-ttu-id="a829d-150">For more information, see [High availability for Azure Stack](azure-stack-key-features.md#high-availability-for-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="a829d-150">For more information, see [High availability for Azure Stack](azure-stack-key-features.md#high-availability-for-azure-stack).</span></span>

- <span data-ttu-id="a829d-151">**Support for physical memory upgrades** - You can now expand the memory capacity of Azure Stack integrated system after your initial deployment.</span><span class="sxs-lookup"><span data-stu-id="a829d-151">**Support for physical memory upgrades** - You can now expand the memory capacity of Azure Stack integrated system after your initial deployment.</span></span> <span data-ttu-id="a829d-152">For more information, see [Manage physical memory capacity for Azure Stack](azure-stack-manage-storage-physical-memory-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-152">For more information, see [Manage physical memory capacity for Azure Stack](azure-stack-manage-storage-physical-memory-capacity.md).</span></span>

- <span data-ttu-id="a829d-153">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-153">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span></span>

<!--
#### New features
-->


<!--
#### Fixes
-->


### <a name="known-issues-with-the-update-process"></a><span data-ttu-id="a829d-154">Known issues with the update process</span><span class="sxs-lookup"><span data-stu-id="a829d-154">Known issues with the update process</span></span>    
<span data-ttu-id="a829d-155">*There are no known issues for the installation of update 1802.*</span><span class="sxs-lookup"><span data-stu-id="a829d-155">*There are no known issues for the installation of update 1802.*</span></span>


### <a name="known-issues-post-installation"></a><span data-ttu-id="a829d-156">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="a829d-156">Known issues (post-installation)</span></span>
<span data-ttu-id="a829d-157">The following are post-installation known issues for build  **20180302.1**</span><span class="sxs-lookup"><span data-stu-id="a829d-157">The following are post-installation known issues for build  **20180302.1**</span></span>

#### <a name="portal"></a><span data-ttu-id="a829d-158">Portal</span><span class="sxs-lookup"><span data-stu-id="a829d-158">Portal</span></span>
- <span data-ttu-id="a829d-159"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span><span class="sxs-lookup"><span data-stu-id="a829d-159"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span></span>  
  <span data-ttu-id="a829d-160">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="a829d-160">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span></span>   

- <span data-ttu-id="a829d-161">The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span><span class="sxs-lookup"><span data-stu-id="a829d-161">The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span></span> <span data-ttu-id="a829d-162">Instead, use the following link:</span><span class="sxs-lookup"><span data-stu-id="a829d-162">Instead, use the following link:</span></span>     
    - <span data-ttu-id="a829d-163">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span><span class="sxs-lookup"><span data-stu-id="a829d-163">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span></span>

- <span data-ttu-id="a829d-164"><!-- 2050709 --> In the admin portal, it is not possible to edit storage metrics for Blob service, Table service, or Queue service.</span><span class="sxs-lookup"><span data-stu-id="a829d-164"><!-- 2050709 --> In the admin portal, it is not possible to edit storage metrics for Blob service, Table service, or Queue service.</span></span> <span data-ttu-id="a829d-165">When you go to Storage, and then select the blob, table, or queue service tile, a new blade opens that displays a metrics chart for that service.</span><span class="sxs-lookup"><span data-stu-id="a829d-165">When you go to Storage, and then select the blob, table, or queue service tile, a new blade opens that displays a metrics chart for that service.</span></span> <span data-ttu-id="a829d-166">If you then select Edit from the top of the metrics chart tile, the Edit Chart blade opens but does not display options to edit metrics.</span><span class="sxs-lookup"><span data-stu-id="a829d-166">If you then select Edit from the top of the metrics chart tile, the Edit Chart blade opens but does not display options to edit metrics.</span></span>

- <span data-ttu-id="a829d-167">It might not be possible to view compute or storage resources in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="a829d-167">It might not be possible to view compute or storage resources in the administrator portal.</span></span> <span data-ttu-id="a829d-168">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span><span class="sxs-lookup"><span data-stu-id="a829d-168">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span></span> <span data-ttu-id="a829d-169">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span><span class="sxs-lookup"><span data-stu-id="a829d-169">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span></span>

- <span data-ttu-id="a829d-170">You might see a blank dashboard in the portal.</span><span class="sxs-lookup"><span data-stu-id="a829d-170">You might see a blank dashboard in the portal.</span></span> <span data-ttu-id="a829d-171">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span><span class="sxs-lookup"><span data-stu-id="a829d-171">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span></span>

- <span data-ttu-id="a829d-172">Deleting user subscriptions results in orphaned resources.</span><span class="sxs-lookup"><span data-stu-id="a829d-172">Deleting user subscriptions results in orphaned resources.</span></span> <span data-ttu-id="a829d-173">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a829d-173">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span></span>

- <span data-ttu-id="a829d-174">You cannot view permissions to your subscription using the Azure Stack portals.</span><span class="sxs-lookup"><span data-stu-id="a829d-174">You cannot view permissions to your subscription using the Azure Stack portals.</span></span> <span data-ttu-id="a829d-175">As a workaround, use PowerShell to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="a829d-175">As a workaround, use PowerShell to verify permissions.</span></span>

- <span data-ttu-id="a829d-176">In the dashboard of the admin portal, the Update tile fails to display information about updates.</span><span class="sxs-lookup"><span data-stu-id="a829d-176">In the dashboard of the admin portal, the Update tile fails to display information about updates.</span></span> <span data-ttu-id="a829d-177">To resolve this issue, click on the tile to refresh it.</span><span class="sxs-lookup"><span data-stu-id="a829d-177">To resolve this issue, click on the tile to refresh it.</span></span>

-   <span data-ttu-id="a829d-178">In the admin portal you might see a critical alert for the Microsoft.Update.Admin component.</span><span class="sxs-lookup"><span data-stu-id="a829d-178">In the admin portal you might see a critical alert for the Microsoft.Update.Admin component.</span></span> <span data-ttu-id="a829d-179">The Alert name, description, and remediation all display as:</span><span class="sxs-lookup"><span data-stu-id="a829d-179">The Alert name, description, and remediation all display as:</span></span>  
    - <span data-ttu-id="a829d-180">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span><span class="sxs-lookup"><span data-stu-id="a829d-180">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span></span>

    <span data-ttu-id="a829d-181">This alert can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="a829d-181">This alert can be safely ignored.</span></span> 

- <span data-ttu-id="a829d-182"><!-- 2253274 --> In the admin and user portals, the Settings blade for vNet Subnets fails to load.</span><span class="sxs-lookup"><span data-stu-id="a829d-182"><!-- 2253274 --> In the admin and user portals, the Settings blade for vNet Subnets fails to load.</span></span> <span data-ttu-id="a829d-183">As a workaround, use PowerShell and the [Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig?view=azurermps-5.5.0) cmdlet to view and  manage this information.</span><span class="sxs-lookup"><span data-stu-id="a829d-183">As a workaround, use PowerShell and the [Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig?view=azurermps-5.5.0) cmdlet to view and  manage this information.</span></span>

- <span data-ttu-id="a829d-184">In both the admin portal and user portal, the Overview blade fails to load when you select the Overview blade for storage accounts that were created with an older API version (example: 2015-06-15).</span><span class="sxs-lookup"><span data-stu-id="a829d-184">In both the admin portal and user portal, the Overview blade fails to load when you select the Overview blade for storage accounts that were created with an older API version (example: 2015-06-15).</span></span> <span data-ttu-id="a829d-185">This includes system storage accounts like **updateadminaccount** that is used during patch and update.</span><span class="sxs-lookup"><span data-stu-id="a829d-185">This includes system storage accounts like **updateadminaccount** that is used during patch and update.</span></span> 

  <span data-ttu-id="a829d-186">As a workaround, use PowerShell to run the **Start-ResourceSynchronization.ps1** script to restore access to the storage account details.</span><span class="sxs-lookup"><span data-stu-id="a829d-186">As a workaround, use PowerShell to run the **Start-ResourceSynchronization.ps1** script to restore access to the storage account details.</span></span> <span data-ttu-id="a829d-187">[The script is available from GitHub]( https://github.com/Azure/AzureStack-Tools/tree/master/Support/scripts), and must run with service administrator credentials on the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="a829d-187">[The script is available from GitHub]( https://github.com/Azure/AzureStack-Tools/tree/master/Support/scripts), and must run with service administrator credentials on the privileged endpoint.</span></span> 

- <span data-ttu-id="a829d-188">The **Service Health** blade fails to load.</span><span class="sxs-lookup"><span data-stu-id="a829d-188">The **Service Health** blade fails to load.</span></span> <span data-ttu-id="a829d-189">When you open the Service Health blade in either the admin or user portal, Azure Stack displays an error and does not load information.</span><span class="sxs-lookup"><span data-stu-id="a829d-189">When you open the Service Health blade in either the admin or user portal, Azure Stack displays an error and does not load information.</span></span> <span data-ttu-id="a829d-190">This is expected behavior.</span><span class="sxs-lookup"><span data-stu-id="a829d-190">This is expected behavior.</span></span> <span data-ttu-id="a829d-191">Although you can select and open Service Health, this feature is not yet available but will be implemented in a future version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-191">Although you can select and open Service Health, this feature is not yet available but will be implemented in a future version of Azure Stack.</span></span>


#### <a name="health-and-monitoring"></a><span data-ttu-id="a829d-192">Health and monitoring</span><span class="sxs-lookup"><span data-stu-id="a829d-192">Health and monitoring</span></span>
- <span data-ttu-id="a829d-193"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span><span class="sxs-lookup"><span data-stu-id="a829d-193"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span></span>  

  <span data-ttu-id="a829d-194">Alert #1:</span><span class="sxs-lookup"><span data-stu-id="a829d-194">Alert #1:</span></span>
   - <span data-ttu-id="a829d-195">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="a829d-195">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="a829d-196">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="a829d-196">SEVERITY: Warning</span></span>
   - <span data-ttu-id="a829d-197">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="a829d-197">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="a829d-198">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="a829d-198">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span></span> <span data-ttu-id="a829d-199">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="a829d-199">This may affect health reports and metrics.</span></span>  

  <span data-ttu-id="a829d-200">Alert #2:</span><span class="sxs-lookup"><span data-stu-id="a829d-200">Alert #2:</span></span>
   - <span data-ttu-id="a829d-201">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="a829d-201">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="a829d-202">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="a829d-202">SEVERITY: Warning</span></span>
   - <span data-ttu-id="a829d-203">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="a829d-203">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="a829d-204">DESCRIPTION: The health controller Fault Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="a829d-204">DESCRIPTION: The health controller Fault Scanner is unavailable.</span></span> <span data-ttu-id="a829d-205">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="a829d-205">This may affect health reports and metrics.</span></span>

  <span data-ttu-id="a829d-206">Both alerts can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="a829d-206">Both alerts can be safely ignored.</span></span> <span data-ttu-id="a829d-207">They will close automatically over time.</span><span class="sxs-lookup"><span data-stu-id="a829d-207">They will close automatically over time.</span></span>  


#### <a name="marketplace"></a><span data-ttu-id="a829d-208">Marketplace</span><span class="sxs-lookup"><span data-stu-id="a829d-208">Marketplace</span></span>
- <span data-ttu-id="a829d-209">Users can browse the full marketplace without a subscription and can see administrative items like plans and offers.</span><span class="sxs-lookup"><span data-stu-id="a829d-209">Users can browse the full marketplace without a subscription and can see administrative items like plans and offers.</span></span> <span data-ttu-id="a829d-210">These items are non-functional to users.</span><span class="sxs-lookup"><span data-stu-id="a829d-210">These items are non-functional to users.</span></span>

#### <a name="compute"></a><span data-ttu-id="a829d-211">Compute</span><span class="sxs-lookup"><span data-stu-id="a829d-211">Compute</span></span>
- <span data-ttu-id="a829d-212">Scaling settings for virtual machine scale sets are not available in the portal.</span><span class="sxs-lookup"><span data-stu-id="a829d-212">Scaling settings for virtual machine scale sets are not available in the portal.</span></span> <span data-ttu-id="a829d-213">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span><span class="sxs-lookup"><span data-stu-id="a829d-213">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span></span> <span data-ttu-id="a829d-214">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span><span class="sxs-lookup"><span data-stu-id="a829d-214">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span></span>

- <span data-ttu-id="a829d-215"><!-- 2290877  --> You cannot scale up a virtual machine scale set (VMSS) that was created when using Azure Stack prior to version 1802.</span><span class="sxs-lookup"><span data-stu-id="a829d-215"><!-- 2290877  --> You cannot scale up a virtual machine scale set (VMSS) that was created when using Azure Stack prior to version 1802.</span></span> <span data-ttu-id="a829d-216">This is due to the change in support for using availability sets with virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="a829d-216">This is due to the change in support for using availability sets with virtual machine scale sets.</span></span> <span data-ttu-id="a829d-217">This support was added with version 1802.</span><span class="sxs-lookup"><span data-stu-id="a829d-217">This support was added with version 1802.</span></span>  <span data-ttu-id="a829d-218">When you attempt to add additional instances to scale a VMSS that was created prior to this support being added, the action fails with the message *Provisioning state failed*.</span><span class="sxs-lookup"><span data-stu-id="a829d-218">When you attempt to add additional instances to scale a VMSS that was created prior to this support being added, the action fails with the message *Provisioning state failed*.</span></span> 

  <span data-ttu-id="a829d-219">This issue is resolved in version 1803.</span><span class="sxs-lookup"><span data-stu-id="a829d-219">This issue is resolved in version 1803.</span></span> <span data-ttu-id="a829d-220">To resolve this issue for version 1802, install Azure Stack hotfix **1.0.180302.4**.</span><span class="sxs-lookup"><span data-stu-id="a829d-220">To resolve this issue for version 1802, install Azure Stack hotfix **1.0.180302.4**.</span></span> <span data-ttu-id="a829d-221">For more information, see [KB 4131152: Existing Virtual Machine Scale Sets may become unusable]( https://support.microsoft.com/help/4131152).</span><span class="sxs-lookup"><span data-stu-id="a829d-221">For more information, see [KB 4131152: Existing Virtual Machine Scale Sets may become unusable]( https://support.microsoft.com/help/4131152).</span></span> 

- <span data-ttu-id="a829d-222">Azure Stack supports using only Fixed type VHDs.</span><span class="sxs-lookup"><span data-stu-id="a829d-222">Azure Stack supports using only Fixed type VHDs.</span></span> <span data-ttu-id="a829d-223">Some images offered through the marketplace on Azure Stack use dynamic VHDs but those have been removed.</span><span class="sxs-lookup"><span data-stu-id="a829d-223">Some images offered through the marketplace on Azure Stack use dynamic VHDs but those have been removed.</span></span> <span data-ttu-id="a829d-224">Resizing a virtual machine (VM) with a dynamic disk attached to it leaves the VM in a failed state.</span><span class="sxs-lookup"><span data-stu-id="a829d-224">Resizing a virtual machine (VM) with a dynamic disk attached to it leaves the VM in a failed state.</span></span>

  <span data-ttu-id="a829d-225">To mitigate this issue, delete the VM without deleting the VM’s disk, a VHD blob in a storage account.</span><span class="sxs-lookup"><span data-stu-id="a829d-225">To mitigate this issue, delete the VM without deleting the VM’s disk, a VHD blob in a storage account.</span></span> <span data-ttu-id="a829d-226">Then convert the VHD from a dynamic disk to a fixed disk, and then re-create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a829d-226">Then convert the VHD from a dynamic disk to a fixed disk, and then re-create the virtual machine.</span></span>

- <span data-ttu-id="a829d-227">When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span><span class="sxs-lookup"><span data-stu-id="a829d-227">When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span></span> <span data-ttu-id="a829d-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span><span class="sxs-lookup"><span data-stu-id="a829d-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span></span>

- <span data-ttu-id="a829d-229">When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span><span class="sxs-lookup"><span data-stu-id="a829d-229">When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span></span> <span data-ttu-id="a829d-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="a829d-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span></span>

- <span data-ttu-id="a829d-231">When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span><span class="sxs-lookup"><span data-stu-id="a829d-231">When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span></span>

  <span data-ttu-id="a829d-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span><span class="sxs-lookup"><span data-stu-id="a829d-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span></span> <span data-ttu-id="a829d-233">This process should fix the problem that prevents deleting the failed item.</span><span class="sxs-lookup"><span data-stu-id="a829d-233">This process should fix the problem that prevents deleting the failed item.</span></span> <span data-ttu-id="a829d-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span><span class="sxs-lookup"><span data-stu-id="a829d-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span></span>

  <span data-ttu-id="a829d-235">You can then try to redownload the VM image that previously failed.</span><span class="sxs-lookup"><span data-stu-id="a829d-235">You can then try to redownload the VM image that previously failed.</span></span>

-  <span data-ttu-id="a829d-236">If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span><span class="sxs-lookup"><span data-stu-id="a829d-236">If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span></span>  

- <span data-ttu-id="a829d-237"><!-- 1662991 --> Linux VM diagnostics is not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a829d-237"><!-- 1662991 --> Linux VM diagnostics is not supported in Azure Stack.</span></span> <span data-ttu-id="a829d-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="a829d-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span></span> <span data-ttu-id="a829d-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="a829d-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span></span>  




#### <a name="networking"></a><span data-ttu-id="a829d-240">Networking</span><span class="sxs-lookup"><span data-stu-id="a829d-240">Networking</span></span>
- <span data-ttu-id="a829d-241">After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span><span class="sxs-lookup"><span data-stu-id="a829d-241">After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span></span> <span data-ttu-id="a829d-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span><span class="sxs-lookup"><span data-stu-id="a829d-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span></span>

  <span data-ttu-id="a829d-243">Currently, you must use only new public IP addresses for new VMs you create.</span><span class="sxs-lookup"><span data-stu-id="a829d-243">Currently, you must use only new public IP addresses for new VMs you create.</span></span>

  <span data-ttu-id="a829d-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span><span class="sxs-lookup"><span data-stu-id="a829d-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span></span> <span data-ttu-id="a829d-245">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span><span class="sxs-lookup"><span data-stu-id="a829d-245">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span></span>

- <span data-ttu-id="a829d-246">Internal Load Balancing (ILB) improperly handles MAC addresses for back-end VMs, which causes ILB to break when using Linux instances on the Back-End network.</span><span class="sxs-lookup"><span data-stu-id="a829d-246">Internal Load Balancing (ILB) improperly handles MAC addresses for back-end VMs, which causes ILB to break when using Linux instances on the Back-End network.</span></span>  <span data-ttu-id="a829d-247">ILB works fine with Windows instances on the Back-End Network.</span><span class="sxs-lookup"><span data-stu-id="a829d-247">ILB works fine with Windows instances on the Back-End Network.</span></span>

-   <span data-ttu-id="a829d-248">The IP Forwarding feature is visible in the portal, however enabling IP Forwarding has no effect.</span><span class="sxs-lookup"><span data-stu-id="a829d-248">The IP Forwarding feature is visible in the portal, however enabling IP Forwarding has no effect.</span></span> <span data-ttu-id="a829d-249">This feature is not yet supported.</span><span class="sxs-lookup"><span data-stu-id="a829d-249">This feature is not yet supported.</span></span>

- <span data-ttu-id="a829d-250">Azure Stack supports a single *local network gateway* per IP address.</span><span class="sxs-lookup"><span data-stu-id="a829d-250">Azure Stack supports a single *local network gateway* per IP address.</span></span> <span data-ttu-id="a829d-251">This is true across all tenant subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a829d-251">This is true across all tenant subscriptions.</span></span> <span data-ttu-id="a829d-252">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span><span class="sxs-lookup"><span data-stu-id="a829d-252">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span></span>

- <span data-ttu-id="a829d-253">On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span><span class="sxs-lookup"><span data-stu-id="a829d-253">On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span></span> <span data-ttu-id="a829d-254">The updated settings are not pushed to VMs in that Vnet.</span><span class="sxs-lookup"><span data-stu-id="a829d-254">The updated settings are not pushed to VMs in that Vnet.</span></span>

- <span data-ttu-id="a829d-255">Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="a829d-255">Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span></span> <span data-ttu-id="a829d-256">If the VM requires more than one network interface, they must be defined at deployment time.</span><span class="sxs-lookup"><span data-stu-id="a829d-256">If the VM requires more than one network interface, they must be defined at deployment time.</span></span>

-   <span data-ttu-id="a829d-257"><!-- 2096388 --> You cannot use the admin portal to update rules for a network security group.</span><span class="sxs-lookup"><span data-stu-id="a829d-257"><!-- 2096388 --> You cannot use the admin portal to update rules for a network security group.</span></span> 

    <span data-ttu-id="a829d-258">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a829d-258">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span></span>  <span data-ttu-id="a829d-259">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span><span class="sxs-lookup"><span data-stu-id="a829d-259">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span></span>  
    
    - <span data-ttu-id="a829d-260">*Allow:*</span><span class="sxs-lookup"><span data-stu-id="a829d-260">*Allow:*</span></span>
 
      ```powershell    
      Login-AzureRMAccount -EnvironmentName AzureStackAdmin
      
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

    - <span data-ttu-id="a829d-261">*Deny:*</span><span class="sxs-lookup"><span data-stu-id="a829d-261">*Deny:*</span></span>

        ```powershell
        
        Login-AzureRMAccount -EnvironmentName AzureStackAdmin
        
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





#### <a name="sql-and-mysql"></a><span data-ttu-id="a829d-262">SQL and MySQL</span><span class="sxs-lookup"><span data-stu-id="a829d-262">SQL and MySQL</span></span>
 - <span data-ttu-id="a829d-263">Before proceeding, review the important note in [before you begin](#before-you-begin) near the start of these release notes.</span><span class="sxs-lookup"><span data-stu-id="a829d-263">Before proceeding, review the important note in [before you begin](#before-you-begin) near the start of these release notes.</span></span>
- <span data-ttu-id="a829d-264">It can take up to one hour before users can create databases in a new SQL or MySQL deployment.</span><span class="sxs-lookup"><span data-stu-id="a829d-264">It can take up to one hour before users can create databases in a new SQL or MySQL deployment.</span></span>

- <span data-ttu-id="a829d-265">Only the resource provider is supported to create items on servers that host SQL or MySQL.</span><span class="sxs-lookup"><span data-stu-id="a829d-265">Only the resource provider is supported to create items on servers that host SQL or MySQL.</span></span> <span data-ttu-id="a829d-266">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span><span class="sxs-lookup"><span data-stu-id="a829d-266">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span></span>  

- <span data-ttu-id="a829d-267"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** name when you create a SKU for the SQL and MySQL resource providers.</span><span class="sxs-lookup"><span data-stu-id="a829d-267"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** name when you create a SKU for the SQL and MySQL resource providers.</span></span>

> [!NOTE]  
> <span data-ttu-id="a829d-268">After you update to Azure Stack 1802, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span><span class="sxs-lookup"><span data-stu-id="a829d-268">After you update to Azure Stack 1802, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span></span>  <span data-ttu-id="a829d-269">We recommend you update SQL and MySQL when a new release becomes available.</span><span class="sxs-lookup"><span data-stu-id="a829d-269">We recommend you update SQL and MySQL when a new release becomes available.</span></span> <span data-ttu-id="a829d-270">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span><span class="sxs-lookup"><span data-stu-id="a829d-270">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span></span>  <span data-ttu-id="a829d-271">For example, if you use version 1710, first apply version 1711, then 1712, and then update to 1802.</span><span class="sxs-lookup"><span data-stu-id="a829d-271">For example, if you use version 1710, first apply version 1711, then 1712, and then update to 1802.</span></span>      
>   
> <span data-ttu-id="a829d-272">The install of update 1802 does not affect the current use of SQL or MySQL resource providers by your users.</span><span class="sxs-lookup"><span data-stu-id="a829d-272">The install of update 1802 does not affect the current use of SQL or MySQL resource providers by your users.</span></span>
> <span data-ttu-id="a829d-273">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span><span class="sxs-lookup"><span data-stu-id="a829d-273">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span></span>    


#### <a name="app-service"></a><span data-ttu-id="a829d-274">App Service</span><span class="sxs-lookup"><span data-stu-id="a829d-274">App Service</span></span>
- <span data-ttu-id="a829d-275">Users must register the storage resource provider before they create their first Azure Function in the subscription.</span><span class="sxs-lookup"><span data-stu-id="a829d-275">Users must register the storage resource provider before they create their first Azure Function in the subscription.</span></span>

- <span data-ttu-id="a829d-276">In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span><span class="sxs-lookup"><span data-stu-id="a829d-276">In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span></span>

<!--
#### Identity
-->



#### <a name="downloading-azure-stack-tools-from-github"></a><span data-ttu-id="a829d-277">Downloading Azure Stack Tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="a829d-277">Downloading Azure Stack Tools from GitHub</span></span>
- <span data-ttu-id="a829d-278">When using the *invoke-webrequest* PowerShell cmdlet to download the Azure Stack tools from Github, you receive an error:</span><span class="sxs-lookup"><span data-stu-id="a829d-278">When using the *invoke-webrequest* PowerShell cmdlet to download the Azure Stack tools from Github, you receive an error:</span></span>     
    -  <span data-ttu-id="a829d-279">*invoke-webrequest : The request was aborted: Could not create SSL/TLS secure channel.*</span><span class="sxs-lookup"><span data-stu-id="a829d-279">*invoke-webrequest : The request was aborted: Could not create SSL/TLS secure channel.*</span></span>     

  <span data-ttu-id="a829d-280">This error occurs because of a recent GitHub support deprecation of the Tlsv1 and Tlsv1.1 cryptographic standards (the default for PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a829d-280">This error occurs because of a recent GitHub support deprecation of the Tlsv1 and Tlsv1.1 cryptographic standards (the default for PowerShell).</span></span> <span data-ttu-id="a829d-281">For more information, see [Weak cryptographic standards removal notice](https://githubengineering.com/crypto-removal-notice/).</span><span class="sxs-lookup"><span data-stu-id="a829d-281">For more information, see [Weak cryptographic standards removal notice](https://githubengineering.com/crypto-removal-notice/).</span></span>

  <span data-ttu-id="a829d-282">To resolve this issue, add `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12` to the top of the script to force the PowerShell console to use TLSv1.2 when downloading from GitHub repositories.</span><span class="sxs-lookup"><span data-stu-id="a829d-282">To resolve this issue, add `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12` to the top of the script to force the PowerShell console to use TLSv1.2 when downloading from GitHub repositories.</span></span>


## <a name="download-the-update"></a><span data-ttu-id="a829d-283">Download the update</span><span class="sxs-lookup"><span data-stu-id="a829d-283">Download the update</span></span>
<span data-ttu-id="a829d-284">You can download the Azure Stack 1802 update package from [here](https://aka.ms/azurestackupdatedownload).</span><span class="sxs-lookup"><span data-stu-id="a829d-284">You can download the Azure Stack 1802 update package from [here](https://aka.ms/azurestackupdatedownload).</span></span>


## <a name="more-information"></a><span data-ttu-id="a829d-285">More information</span><span class="sxs-lookup"><span data-stu-id="a829d-285">More information</span></span>
<span data-ttu-id="a829d-286">Microsoft has provided a way to monitor and resume updates using the Privileged End Point (PEP) installed with Update 1710.</span><span class="sxs-lookup"><span data-stu-id="a829d-286">Microsoft has provided a way to monitor and resume updates using the Privileged End Point (PEP) installed with Update 1710.</span></span>

- <span data-ttu-id="a829d-287">See the [Monitor updates in Azure Stack using the privileged endpoint documentation](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-update).</span><span class="sxs-lookup"><span data-stu-id="a829d-287">See the [Monitor updates in Azure Stack using the privileged endpoint documentation](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-update).</span></span>

## <a name="see-also"></a><span data-ttu-id="a829d-288">See also</span><span class="sxs-lookup"><span data-stu-id="a829d-288">See also</span></span>

- <span data-ttu-id="a829d-289">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-289">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span></span>
- <span data-ttu-id="a829d-290">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="a829d-290">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span></span>
