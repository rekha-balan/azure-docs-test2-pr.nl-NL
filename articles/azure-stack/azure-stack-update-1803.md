---
title: Azure Stack 1803 Update | Microsoft Docs
description: Learn about what's in the 1803 update for Azure Stack integrated systems, the known issues, and where to download the update.
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
ms.date: 07/11/2018
ms.author: brenduns
ms.reviewer: justini
ms.openlocfilehash: 11430a0d194a722c0c0520c936db3c08b1a6b863
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867899"
---
# <a name="azure-stack-1803-update"></a><span data-ttu-id="8b327-103">Azure Stack 1803 update</span><span class="sxs-lookup"><span data-stu-id="8b327-103">Azure Stack 1803 update</span></span>

<span data-ttu-id="8b327-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="8b327-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="8b327-105">This article describes the improvements and fixes in the 1803 update package, known issues for this release, and where to download the update.</span><span class="sxs-lookup"><span data-stu-id="8b327-105">This article describes the improvements and fixes in the 1803 update package, known issues for this release, and where to download the update.</span></span> <span data-ttu-id="8b327-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="8b327-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span></span>

> [!IMPORTANT]        
> <span data-ttu-id="8b327-107">This update package is only for Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="8b327-107">This update package is only for Azure Stack integrated systems.</span></span> <span data-ttu-id="8b327-108">Do not apply this update package to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="8b327-108">Do not apply this update package to the Azure Stack Development Kit.</span></span>

## <a name="build-reference"></a><span data-ttu-id="8b327-109">Build reference</span><span class="sxs-lookup"><span data-stu-id="8b327-109">Build reference</span></span>    
<span data-ttu-id="8b327-110">The Azure Stack 1803 update build number is **20180329.1**.</span><span class="sxs-lookup"><span data-stu-id="8b327-110">The Azure Stack 1803 update build number is **20180329.1**.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="8b327-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8b327-111">Before you begin</span></span>    
> [!IMPORTANT]    
> <span data-ttu-id="8b327-112">Do not attempt to create virtual machines during the installation of this update.</span><span class="sxs-lookup"><span data-stu-id="8b327-112">Do not attempt to create virtual machines during the installation of this update.</span></span> <span data-ttu-id="8b327-113">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span><span class="sxs-lookup"><span data-stu-id="8b327-113">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span></span>


### <a name="prerequisites"></a><span data-ttu-id="8b327-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b327-114">Prerequisites</span></span>
- <span data-ttu-id="8b327-115">Install the Azure Stack [1802 Update](azure-stack-update-1802.md) before you apply the Azure Stack 1803 update.</span><span class="sxs-lookup"><span data-stu-id="8b327-115">Install the Azure Stack [1802 Update](azure-stack-update-1802.md) before you apply the Azure Stack 1803 update.</span></span>   

- <span data-ttu-id="8b327-116">Install **AzS Hotfix – 1.0.180312.1- Build 20180222.2** before you apply the Azure Stack 1803 update.</span><span class="sxs-lookup"><span data-stu-id="8b327-116">Install **AzS Hotfix – 1.0.180312.1- Build 20180222.2** before you apply the Azure Stack 1803 update.</span></span> <span data-ttu-id="8b327-117">This hotfix updates Windows Defender, and is available when you download updates for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-117">This hotfix updates Windows Defender, and is available when you download updates for Azure Stack.</span></span>

  <span data-ttu-id="8b327-118">To install the hotfix, follow the normal procedures for [installing updates for Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-118">To install the hotfix, follow the normal procedures for [installing updates for Azure Stack](azure-stack-apply-updates.md).</span></span> <span data-ttu-id="8b327-119">The name of the update appears as **AzS Hotfix – 1.0.180312.1**, and includes the following files:</span><span class="sxs-lookup"><span data-stu-id="8b327-119">The name of the update appears as **AzS Hotfix – 1.0.180312.1**, and includes the following files:</span></span> 
    - <span data-ttu-id="8b327-120">PUPackageHotFix_20180222.2-1.exe</span><span class="sxs-lookup"><span data-stu-id="8b327-120">PUPackageHotFix_20180222.2-1.exe</span></span>
    - <span data-ttu-id="8b327-121">PUPackageHotFix_20180222.2-1.bin</span><span class="sxs-lookup"><span data-stu-id="8b327-121">PUPackageHotFix_20180222.2-1.bin</span></span>
    - <span data-ttu-id="8b327-122">Metadata.xml</span><span class="sxs-lookup"><span data-stu-id="8b327-122">Metadata.xml</span></span>

  <span data-ttu-id="8b327-123">After uploading these files to a storage account and container, run the install from the Update tile in the admin portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-123">After uploading these files to a storage account and container, run the install from the Update tile in the admin portal.</span></span> 
  
  <span data-ttu-id="8b327-124">Unlike updates to Azure Stack, installing this update does not change the version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-124">Unlike updates to Azure Stack, installing this update does not change the version of Azure Stack.</span></span> <span data-ttu-id="8b327-125">To confirm this update is installed, view the list of **Installed updates**.</span><span class="sxs-lookup"><span data-stu-id="8b327-125">To confirm this update is installed, view the list of **Installed updates**.</span></span>



### <a name="new-features"></a><span data-ttu-id="8b327-126">New features</span><span class="sxs-lookup"><span data-stu-id="8b327-126">New features</span></span> 
<span data-ttu-id="8b327-127">This update includes the following improvements and fixes for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-127">This update includes the following improvements and fixes for Azure Stack.</span></span>

- <span data-ttu-id="8b327-128">**Update Azure Stack secrets** - (Accounts and Certificates).</span><span class="sxs-lookup"><span data-stu-id="8b327-128">**Update Azure Stack secrets** - (Accounts and Certificates).</span></span> <span data-ttu-id="8b327-129">For more information about managing secrets, see [Rotate secrets in Azure Stack](azure-stack-rotate-secrets.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-129">For more information about managing secrets, see [Rotate secrets in Azure Stack](azure-stack-rotate-secrets.md).</span></span> 

- <span data-ttu-id="8b327-130"><!-- 1914853 --> **Automatic redirect to HTTPS** when you use HTTP to access the administrator and user portals.</span><span class="sxs-lookup"><span data-stu-id="8b327-130"><!-- 1914853 --> **Automatic redirect to HTTPS** when you use HTTP to access the administrator and user portals.</span></span> <span data-ttu-id="8b327-131">This improvement was made based on [UserVoice](https://feedback.azure.com/forums/344565-azure-stack/suggestions/32205385-it-would-be-great-if-there-was-a-automatic-redirec) feedback for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-131">This improvement was made based on [UserVoice](https://feedback.azure.com/forums/344565-azure-stack/suggestions/32205385-it-would-be-great-if-there-was-a-automatic-redirec) feedback for Azure Stack.</span></span> 

- <span data-ttu-id="8b327-132"><!-- 2202621  --> **Access the Marketplace** – You can now open the Azure Stack Marketplace by using the [+New](https://ms.portal.azure.com/#create/hub) option from within the admin and user portals the same way you do in the Azure portals.</span><span class="sxs-lookup"><span data-stu-id="8b327-132"><!-- 2202621  --> **Access the Marketplace** – You can now open the Azure Stack Marketplace by using the [+New](https://ms.portal.azure.com/#create/hub) option from within the admin and user portals the same way you do in the Azure portals.</span></span>
 
- <span data-ttu-id="8b327-133"><!-- 2202621 --> **Azure Monitor** - Azure Stack adds [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) to the admin and user portals.</span><span class="sxs-lookup"><span data-stu-id="8b327-133"><!-- 2202621 --> **Azure Monitor** - Azure Stack adds [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) to the admin and user portals.</span></span> <span data-ttu-id="8b327-134">This includes new explorers for metrics and activity logs.</span><span class="sxs-lookup"><span data-stu-id="8b327-134">This includes new explorers for metrics and activity logs.</span></span> <span data-ttu-id="8b327-135">To access this Azure Monitor from external networks, port **13012** must be open in firewall configurations.</span><span class="sxs-lookup"><span data-stu-id="8b327-135">To access this Azure Monitor from external networks, port **13012** must be open in firewall configurations.</span></span> <span data-ttu-id="8b327-136">For more information about ports required by Azure Stack, see [Azure Stack datacenter integration - Publish endpoints](azure-stack-integrate-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-136">For more information about ports required by Azure Stack, see [Azure Stack datacenter integration - Publish endpoints](azure-stack-integrate-endpoints.md).</span></span>

   <span data-ttu-id="8b327-137">Also as part of this change, under **More services**, *Audit logs* now appears as *Activity logs*.</span><span class="sxs-lookup"><span data-stu-id="8b327-137">Also as part of this change, under **More services**, *Audit logs* now appears as *Activity logs*.</span></span> <span data-ttu-id="8b327-138">The functionality is now consistent with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-138">The functionality is now consistent with the Azure portal.</span></span> 

- <span data-ttu-id="8b327-139"><!-- 1664791 --> **Sparse files** -  When you add a New image to Azure Stack, or add an image through marketplace syndication, the image is converted to a sparse file.</span><span class="sxs-lookup"><span data-stu-id="8b327-139"><!-- 1664791 --> **Sparse files** -  When you add a New image to Azure Stack, or add an image through marketplace syndication, the image is converted to a sparse file.</span></span> <span data-ttu-id="8b327-140">Images that were added prior to using Azure Stack version 1803 cannot be converted.</span><span class="sxs-lookup"><span data-stu-id="8b327-140">Images that were added prior to using Azure Stack version 1803 cannot be converted.</span></span> <span data-ttu-id="8b327-141">Instead, you must use marketplace syndication to resubmit those images to take advantage of this feature.</span><span class="sxs-lookup"><span data-stu-id="8b327-141">Instead, you must use marketplace syndication to resubmit those images to take advantage of this feature.</span></span> 
 
   <span data-ttu-id="8b327-142">Sparse files are an efficient file format used to reduce storage space use, and improve I/O.</span><span class="sxs-lookup"><span data-stu-id="8b327-142">Sparse files are an efficient file format used to reduce storage space use, and improve I/O.</span></span> <span data-ttu-id="8b327-143"> For more information, see [Fsutil sparse](https://docs.microsoft.com/windows-server/administration/windows-commands/fsutil-sparse) for Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8b327-143"> For more information, see [Fsutil sparse](https://docs.microsoft.com/windows-server/administration/windows-commands/fsutil-sparse) for Windows Server.</span></span> 

### <a name="fixed-issues"></a><span data-ttu-id="8b327-144">Fixed issues</span><span class="sxs-lookup"><span data-stu-id="8b327-144">Fixed issues</span></span>

- <span data-ttu-id="8b327-145"><!-- 1739988 --> Internal Load Balancing (ILB) now properly handles MAC addresses for back-end VMs, which causes ILB to drop packets to the back-end network when using Linux instances on the back-end network.</span><span class="sxs-lookup"><span data-stu-id="8b327-145"><!-- 1739988 --> Internal Load Balancing (ILB) now properly handles MAC addresses for back-end VMs, which causes ILB to drop packets to the back-end network when using Linux instances on the back-end network.</span></span> <span data-ttu-id="8b327-146">ILB works fine with Windows instances on the back-end network.</span><span class="sxs-lookup"><span data-stu-id="8b327-146">ILB works fine with Windows instances on the back-end network.</span></span> 

- <span data-ttu-id="8b327-147"><!-- 1805496 --> An issue where VPN Connections between Azure Stack would become disconnected due to Azure Stack using different settings for the IKE policy than Azure.</span><span class="sxs-lookup"><span data-stu-id="8b327-147"><!-- 1805496 --> An issue where VPN Connections between Azure Stack would become disconnected due to Azure Stack using different settings for the IKE policy than Azure.</span></span> <span data-ttu-id="8b327-148">The values for SALifetime (Time) and SALiftetime (Bytes) were not compatible with Azure and have changed in 1803 to match the Azure settings.</span><span class="sxs-lookup"><span data-stu-id="8b327-148">The values for SALifetime (Time) and SALiftetime (Bytes) were not compatible with Azure and have changed in 1803 to match the Azure settings.</span></span> <span data-ttu-id="8b327-149">The value for SALifetime (Seconds) prior to 1803 was 14,400 and now changes to 27,000 in 1803.</span><span class="sxs-lookup"><span data-stu-id="8b327-149">The value for SALifetime (Seconds) prior to 1803 was 14,400 and now changes to 27,000 in 1803.</span></span> <span data-ttu-id="8b327-150">The value for SALifetime (Bytes) prior to 1803 was 819,200 and changes to 33,553,408 in 1803.</span><span class="sxs-lookup"><span data-stu-id="8b327-150">The value for SALifetime (Bytes) prior to 1803 was 819,200 and changes to 33,553,408 in 1803.</span></span>

- <span data-ttu-id="8b327-151"><!-- 2209262 --> The IP issue where VPN Connections was previously visible in the portal; however enabling or toggling IP Forwarding has no effect.</span><span class="sxs-lookup"><span data-stu-id="8b327-151"><!-- 2209262 --> The IP issue where VPN Connections was previously visible in the portal; however enabling or toggling IP Forwarding has no effect.</span></span> <span data-ttu-id="8b327-152">The feature is turned on by default and the ability to change this not yet supported.</span><span class="sxs-lookup"><span data-stu-id="8b327-152">The feature is turned on by default and the ability to change this not yet supported.</span></span>  <span data-ttu-id="8b327-153">The control has been removed from the portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-153">The control has been removed from the portal.</span></span> 

- <span data-ttu-id="8b327-154"><!-- 1766332 --> Azure Stack does not support Policy Based VPN Gateways, even though the option appears in the Portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-154"><!-- 1766332 --> Azure Stack does not support Policy Based VPN Gateways, even though the option appears in the Portal.</span></span>  <span data-ttu-id="8b327-155">The option has been removed from the Portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-155">The option has been removed from the Portal.</span></span> 

- <span data-ttu-id="8b327-156"><!-- 1868283 --> Azure Stack now prevents resizing of a virtual machine that is created with dynamic disks.</span><span class="sxs-lookup"><span data-stu-id="8b327-156"><!-- 1868283 --> Azure Stack now prevents resizing of a virtual machine that is created with dynamic disks.</span></span> 

- <span data-ttu-id="8b327-157"><!-- 1756324 --> Usage data for virtual machines is now separated at hourly intervals.</span><span class="sxs-lookup"><span data-stu-id="8b327-157"><!-- 1756324 --> Usage data for virtual machines is now separated at hourly intervals.</span></span> <span data-ttu-id="8b327-158">This is consistent with Azure.</span><span class="sxs-lookup"><span data-stu-id="8b327-158">This is consistent with Azure.</span></span> 

- <span data-ttu-id="8b327-159"><!--  2253274 --> The issue where in the admin and user portals, the Settings blade for vNet Subnets fails to load.</span><span class="sxs-lookup"><span data-stu-id="8b327-159"><!--  2253274 --> The issue where in the admin and user portals, the Settings blade for vNet Subnets fails to load.</span></span> <span data-ttu-id="8b327-160">As a workaround, use PowerShell and the [Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig?view=azurermps-5.5.0) cmdlet to view and manage this information.</span><span class="sxs-lookup"><span data-stu-id="8b327-160">As a workaround, use PowerShell and the [Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig?view=azurermps-5.5.0) cmdlet to view and manage this information.</span></span>

- <span data-ttu-id="8b327-161">When you create a virtual machine, the message *Unable to display pricing* no longer appears when choosing a size for the VM size.</span><span class="sxs-lookup"><span data-stu-id="8b327-161">When you create a virtual machine, the message *Unable to display pricing* no longer appears when choosing a size for the VM size.</span></span>

- <span data-ttu-id="8b327-162">Various fixes for performance, stability, security, and the operating system that is used by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-162">Various fixes for performance, stability, security, and the operating system that is used by Azure Stack.</span></span>


### <a name="changes"></a><span data-ttu-id="8b327-163">Changes</span><span class="sxs-lookup"><span data-stu-id="8b327-163">Changes</span></span>
- <span data-ttu-id="8b327-164">The way to change the state of a newly created offer from *private* to *public* or *decommissioned* has changed.</span><span class="sxs-lookup"><span data-stu-id="8b327-164">The way to change the state of a newly created offer from *private* to *public* or *decommissioned* has changed.</span></span> <span data-ttu-id="8b327-165">For more information, see [Create an offer](azure-stack-create-offer.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-165">For more information, see [Create an offer](azure-stack-create-offer.md).</span></span>


### <a name="known-issues-with-the-update-process"></a><span data-ttu-id="8b327-166">Known issues with the update process</span><span class="sxs-lookup"><span data-stu-id="8b327-166">Known issues with the update process</span></span>    
<span data-ttu-id="8b327-167"><!-- 2328416 --> During installation of the 1803 update, there can be downtime of the blob service and internal services that use blob service.</span><span class="sxs-lookup"><span data-stu-id="8b327-167"><!-- 2328416 --> During installation of the 1803 update, there can be downtime of the blob service and internal services that use blob service.</span></span> <span data-ttu-id="8b327-168">This includes some virtual machine operations.</span><span class="sxs-lookup"><span data-stu-id="8b327-168">This includes some virtual machine operations.</span></span> <span data-ttu-id="8b327-169">This down time can cause failures of tenant operations or alerts from services that can’t access data.</span><span class="sxs-lookup"><span data-stu-id="8b327-169">This down time can cause failures of tenant operations or alerts from services that can’t access data.</span></span> <span data-ttu-id="8b327-170">This issue resolves itself when the update completes installation.</span><span class="sxs-lookup"><span data-stu-id="8b327-170">This issue resolves itself when the update completes installation.</span></span> 



### <a name="post-update-steps"></a><span data-ttu-id="8b327-171">Post-update steps</span><span class="sxs-lookup"><span data-stu-id="8b327-171">Post-update steps</span></span>
- <span data-ttu-id="8b327-172">After the installation of 1803, install any applicable Hotfixes.</span><span class="sxs-lookup"><span data-stu-id="8b327-172">After the installation of 1803, install any applicable Hotfixes.</span></span> <span data-ttu-id="8b327-173">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-173">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span></span>

  - <span data-ttu-id="8b327-174">[KB 4344115 - Azure Stack Hotfix 1.0.180427.15](https://support.microsoft.com/help/4344115).</span><span class="sxs-lookup"><span data-stu-id="8b327-174">[KB 4344115 - Azure Stack Hotfix 1.0.180427.15](https://support.microsoft.com/help/4344115).</span></span>

- <span data-ttu-id="8b327-175">After installing this update, review your firewall configuration to ensure [necessary ports](azure-stack-integrate-endpoints.md) are open.</span><span class="sxs-lookup"><span data-stu-id="8b327-175">After installing this update, review your firewall configuration to ensure [necessary ports](azure-stack-integrate-endpoints.md) are open.</span></span> <span data-ttu-id="8b327-176">For example, this update introduces *Azure Monitor* which includes a change of Audit logs to Activity logs.</span><span class="sxs-lookup"><span data-stu-id="8b327-176">For example, this update introduces *Azure Monitor* which includes a change of Audit logs to Activity logs.</span></span> <span data-ttu-id="8b327-177">With this change, port 13012 is now used and must also be open.</span><span class="sxs-lookup"><span data-stu-id="8b327-177">With this change, port 13012 is now used and must also be open.</span></span>  


### <a name="known-issues-post-installation"></a><span data-ttu-id="8b327-178">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="8b327-178">Known issues (post-installation)</span></span>
<span data-ttu-id="8b327-179">The following are post-installation known issues for build  **20180323.2**.</span><span class="sxs-lookup"><span data-stu-id="8b327-179">The following are post-installation known issues for build  **20180323.2**.</span></span>

#### <a name="portal"></a><span data-ttu-id="8b327-180">Portal</span><span class="sxs-lookup"><span data-stu-id="8b327-180">Portal</span></span>
- <span data-ttu-id="8b327-181"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span><span class="sxs-lookup"><span data-stu-id="8b327-181"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span></span>  
  <span data-ttu-id="8b327-182">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="8b327-182">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span></span>   

- <span data-ttu-id="8b327-183">The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span><span class="sxs-lookup"><span data-stu-id="8b327-183">The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span></span> <span data-ttu-id="8b327-184">Instead, use the following link:</span><span class="sxs-lookup"><span data-stu-id="8b327-184">Instead, use the following link:</span></span>     
    - <span data-ttu-id="8b327-185">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span><span class="sxs-lookup"><span data-stu-id="8b327-185">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span></span>

- <span data-ttu-id="8b327-186"><!-- 2050709 --> In the admin portal, it is not possible to edit storage metrics for Blob service, Table service, or Queue service.</span><span class="sxs-lookup"><span data-stu-id="8b327-186"><!-- 2050709 --> In the admin portal, it is not possible to edit storage metrics for Blob service, Table service, or Queue service.</span></span> <span data-ttu-id="8b327-187">When you go to Storage, and then select the blob, table, or queue service tile, a new blade opens that displays a metrics chart for that service.</span><span class="sxs-lookup"><span data-stu-id="8b327-187">When you go to Storage, and then select the blob, table, or queue service tile, a new blade opens that displays a metrics chart for that service.</span></span> <span data-ttu-id="8b327-188">If you then select Edit from the top of the metrics chart tile, the Edit Chart blade opens but does not display options to edit metrics.</span><span class="sxs-lookup"><span data-stu-id="8b327-188">If you then select Edit from the top of the metrics chart tile, the Edit Chart blade opens but does not display options to edit metrics.</span></span>

- <span data-ttu-id="8b327-189">It might not be possible to view compute or storage resources in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-189">It might not be possible to view compute or storage resources in the administrator portal.</span></span> <span data-ttu-id="8b327-190">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span><span class="sxs-lookup"><span data-stu-id="8b327-190">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span></span> <span data-ttu-id="8b327-191">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span><span class="sxs-lookup"><span data-stu-id="8b327-191">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span></span>

- <span data-ttu-id="8b327-192">You might see a blank dashboard in the portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-192">You might see a blank dashboard in the portal.</span></span> <span data-ttu-id="8b327-193">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span><span class="sxs-lookup"><span data-stu-id="8b327-193">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span></span>

- <span data-ttu-id="8b327-194">Deleting user subscriptions results in orphaned resources.</span><span class="sxs-lookup"><span data-stu-id="8b327-194">Deleting user subscriptions results in orphaned resources.</span></span> <span data-ttu-id="8b327-195">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8b327-195">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span></span>

- <span data-ttu-id="8b327-196">You cannot view permissions to your subscription using the Azure Stack portals.</span><span class="sxs-lookup"><span data-stu-id="8b327-196">You cannot view permissions to your subscription using the Azure Stack portals.</span></span> <span data-ttu-id="8b327-197">As a workaround, use PowerShell to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="8b327-197">As a workaround, use PowerShell to verify permissions.</span></span>

- <span data-ttu-id="8b327-198">In the dashboard of the admin portal, the Update tile fails to display information about updates.</span><span class="sxs-lookup"><span data-stu-id="8b327-198">In the dashboard of the admin portal, the Update tile fails to display information about updates.</span></span> <span data-ttu-id="8b327-199">To resolve this issue, click on the tile to refresh it.</span><span class="sxs-lookup"><span data-stu-id="8b327-199">To resolve this issue, click on the tile to refresh it.</span></span>

- <span data-ttu-id="8b327-200">In the admin portal, you might see a critical alert for the *Microsoft.Update.Admin* component.</span><span class="sxs-lookup"><span data-stu-id="8b327-200">In the admin portal, you might see a critical alert for the *Microsoft.Update.Admin* component.</span></span> <span data-ttu-id="8b327-201">The Alert name, description, and remediation all display as:</span><span class="sxs-lookup"><span data-stu-id="8b327-201">The Alert name, description, and remediation all display as:</span></span>  
    - <span data-ttu-id="8b327-202">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span><span class="sxs-lookup"><span data-stu-id="8b327-202">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span></span>

  <span data-ttu-id="8b327-203">This alert can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="8b327-203">This alert can be safely ignored.</span></span> 


#### <a name="health-and-monitoring"></a><span data-ttu-id="8b327-204">Health and monitoring</span><span class="sxs-lookup"><span data-stu-id="8b327-204">Health and monitoring</span></span>
- <span data-ttu-id="8b327-205"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span><span class="sxs-lookup"><span data-stu-id="8b327-205"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span></span>  

   <span data-ttu-id="8b327-206">Alert #1:</span><span class="sxs-lookup"><span data-stu-id="8b327-206">Alert #1:</span></span>
   - <span data-ttu-id="8b327-207">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="8b327-207">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="8b327-208">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="8b327-208">SEVERITY: Warning</span></span>
   - <span data-ttu-id="8b327-209">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="8b327-209">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="8b327-210">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="8b327-210">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span></span> <span data-ttu-id="8b327-211">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="8b327-211">This may affect health reports and metrics.</span></span>  

  <span data-ttu-id="8b327-212">Alert #2:</span><span class="sxs-lookup"><span data-stu-id="8b327-212">Alert #2:</span></span>
   - <span data-ttu-id="8b327-213">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="8b327-213">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="8b327-214">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="8b327-214">SEVERITY: Warning</span></span>
   - <span data-ttu-id="8b327-215">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="8b327-215">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="8b327-216">DESCRIPTION: The health controller Fault Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="8b327-216">DESCRIPTION: The health controller Fault Scanner is unavailable.</span></span> <span data-ttu-id="8b327-217">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="8b327-217">This may affect health reports and metrics.</span></span>

  <span data-ttu-id="8b327-218">Both alerts can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="8b327-218">Both alerts can be safely ignored.</span></span> <span data-ttu-id="8b327-219">They will close automatically over time.</span><span class="sxs-lookup"><span data-stu-id="8b327-219">They will close automatically over time.</span></span>  


#### <a name="marketplace"></a><span data-ttu-id="8b327-220">Marketplace</span><span class="sxs-lookup"><span data-stu-id="8b327-220">Marketplace</span></span>
- <span data-ttu-id="8b327-221">Users can browse the full marketplace without a subscription and can see administrative items like plans and offers.</span><span class="sxs-lookup"><span data-stu-id="8b327-221">Users can browse the full marketplace without a subscription and can see administrative items like plans and offers.</span></span> <span data-ttu-id="8b327-222">These items are non-functional to users.</span><span class="sxs-lookup"><span data-stu-id="8b327-222">These items are non-functional to users.</span></span>



#### <a name="compute"></a><span data-ttu-id="8b327-223">Compute</span><span class="sxs-lookup"><span data-stu-id="8b327-223">Compute</span></span>
- <span data-ttu-id="8b327-224">Scaling settings for virtual machine scale sets are not available in the portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-224">Scaling settings for virtual machine scale sets are not available in the portal.</span></span> <span data-ttu-id="8b327-225">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span><span class="sxs-lookup"><span data-stu-id="8b327-225">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span></span> <span data-ttu-id="8b327-226">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span><span class="sxs-lookup"><span data-stu-id="8b327-226">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span></span>

- <span data-ttu-id="8b327-227">When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span><span class="sxs-lookup"><span data-stu-id="8b327-227">When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span></span> <span data-ttu-id="8b327-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span><span class="sxs-lookup"><span data-stu-id="8b327-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span></span>

- <span data-ttu-id="8b327-229">When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span><span class="sxs-lookup"><span data-stu-id="8b327-229">When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span></span> <span data-ttu-id="8b327-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="8b327-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span></span>

- <span data-ttu-id="8b327-231">When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span><span class="sxs-lookup"><span data-stu-id="8b327-231">When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span></span>

  <span data-ttu-id="8b327-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span><span class="sxs-lookup"><span data-stu-id="8b327-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span></span> <span data-ttu-id="8b327-233">This process should fix the problem that prevents deleting the failed item.</span><span class="sxs-lookup"><span data-stu-id="8b327-233">This process should fix the problem that prevents deleting the failed item.</span></span> <span data-ttu-id="8b327-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span><span class="sxs-lookup"><span data-stu-id="8b327-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span></span>

  <span data-ttu-id="8b327-235">You can then try to redownload the VM image that previously failed.</span><span class="sxs-lookup"><span data-stu-id="8b327-235">You can then try to redownload the VM image that previously failed.</span></span>

-  <span data-ttu-id="8b327-236">If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span><span class="sxs-lookup"><span data-stu-id="8b327-236">If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span></span>  

- <span data-ttu-id="8b327-237"><!-- 1662991 --> Linux VM diagnostics is not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b327-237"><!-- 1662991 --> Linux VM diagnostics is not supported in Azure Stack.</span></span> <span data-ttu-id="8b327-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="8b327-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span></span> <span data-ttu-id="8b327-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="8b327-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span></span>  


#### <a name="networking"></a><span data-ttu-id="8b327-240">Networking</span><span class="sxs-lookup"><span data-stu-id="8b327-240">Networking</span></span>
- <span data-ttu-id="8b327-241">After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span><span class="sxs-lookup"><span data-stu-id="8b327-241">After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span></span> <span data-ttu-id="8b327-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span><span class="sxs-lookup"><span data-stu-id="8b327-242">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span></span>

  <span data-ttu-id="8b327-243">Currently, you must use only new public IP addresses for new VMs you create.</span><span class="sxs-lookup"><span data-stu-id="8b327-243">Currently, you must use only new public IP addresses for new VMs you create.</span></span>

  <span data-ttu-id="8b327-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span><span class="sxs-lookup"><span data-stu-id="8b327-244">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span></span> <span data-ttu-id="8b327-245">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span><span class="sxs-lookup"><span data-stu-id="8b327-245">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span></span>



- <span data-ttu-id="8b327-246">Azure Stack supports a single *local network gateway* per IP address.</span><span class="sxs-lookup"><span data-stu-id="8b327-246">Azure Stack supports a single *local network gateway* per IP address.</span></span> <span data-ttu-id="8b327-247">This is true across all tenant subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8b327-247">This is true across all tenant subscriptions.</span></span> <span data-ttu-id="8b327-248">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span><span class="sxs-lookup"><span data-stu-id="8b327-248">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span></span>

- <span data-ttu-id="8b327-249">On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span><span class="sxs-lookup"><span data-stu-id="8b327-249">On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span></span> <span data-ttu-id="8b327-250">The updated settings are not pushed to VMs in that Vnet.</span><span class="sxs-lookup"><span data-stu-id="8b327-250">The updated settings are not pushed to VMs in that Vnet.</span></span>

- <span data-ttu-id="8b327-251">Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="8b327-251">Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span></span> <span data-ttu-id="8b327-252">If the VM requires more than one network interface, they must be defined at deployment time.</span><span class="sxs-lookup"><span data-stu-id="8b327-252">If the VM requires more than one network interface, they must be defined at deployment time.</span></span>

- <span data-ttu-id="8b327-253"><!-- 2096388 --> You cannot use the admin portal to update rules for a network security group.</span><span class="sxs-lookup"><span data-stu-id="8b327-253"><!-- 2096388 --> You cannot use the admin portal to update rules for a network security group.</span></span> 

    <span data-ttu-id="8b327-254">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b327-254">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span></span>  <span data-ttu-id="8b327-255">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span><span class="sxs-lookup"><span data-stu-id="8b327-255">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span></span>  
    
    - <span data-ttu-id="8b327-256">*Allow:*</span><span class="sxs-lookup"><span data-stu-id="8b327-256">*Allow:*</span></span>
 
      ```powershell    
      Add-AzureRmAccount -EnvironmentName AzureStackAdmin
      
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

    - <span data-ttu-id="8b327-257">*Deny:*</span><span class="sxs-lookup"><span data-stu-id="8b327-257">*Deny:*</span></span>

        ```powershell
        
        Add-AzureRmAccount -EnvironmentName AzureStackAdmin
        
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


#### <a name="sql-and-mysql"></a><span data-ttu-id="8b327-258">SQL and MySQL</span><span class="sxs-lookup"><span data-stu-id="8b327-258">SQL and MySQL</span></span>
- <span data-ttu-id="8b327-259">Before proceeding, review the important note in [before you begin](#before-you-begin) near the start of these release notes.</span><span class="sxs-lookup"><span data-stu-id="8b327-259">Before proceeding, review the important note in [before you begin](#before-you-begin) near the start of these release notes.</span></span>

- <span data-ttu-id="8b327-260">It can take up to one hour before users can create databases in a new SQL or MySQL deployment.</span><span class="sxs-lookup"><span data-stu-id="8b327-260">It can take up to one hour before users can create databases in a new SQL or MySQL deployment.</span></span>

- <span data-ttu-id="8b327-261">Only the resource provider is supported to create items on servers that host SQL or MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b327-261">Only the resource provider is supported to create items on servers that host SQL or MySQL.</span></span> <span data-ttu-id="8b327-262">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span><span class="sxs-lookup"><span data-stu-id="8b327-262">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span></span>  

- <span data-ttu-id="8b327-263"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** name when you create a SKU for the SQL and MySQL resource providers.</span><span class="sxs-lookup"><span data-stu-id="8b327-263"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** name when you create a SKU for the SQL and MySQL resource providers.</span></span>

> [!NOTE]  
> <span data-ttu-id="8b327-264">After you update to Azure Stack 1803, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span><span class="sxs-lookup"><span data-stu-id="8b327-264">After you update to Azure Stack 1803, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span></span>  <span data-ttu-id="8b327-265">We recommend you update SQL and MySQL when a new release becomes available.</span><span class="sxs-lookup"><span data-stu-id="8b327-265">We recommend you update SQL and MySQL when a new release becomes available.</span></span> <span data-ttu-id="8b327-266">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span><span class="sxs-lookup"><span data-stu-id="8b327-266">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span></span>  <span data-ttu-id="8b327-267">For example, if you use version 1711, first apply version 1712, then 1802, and then update to 1803.</span><span class="sxs-lookup"><span data-stu-id="8b327-267">For example, if you use version 1711, first apply version 1712, then 1802, and then update to 1803.</span></span>      
>   
> <span data-ttu-id="8b327-268">The install of update 1803 does not affect the current use of SQL or MySQL resource providers by your users.</span><span class="sxs-lookup"><span data-stu-id="8b327-268">The install of update 1803 does not affect the current use of SQL or MySQL resource providers by your users.</span></span>
> <span data-ttu-id="8b327-269">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span><span class="sxs-lookup"><span data-stu-id="8b327-269">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span></span>    



#### <a name="app-service"></a><span data-ttu-id="8b327-270">App Service</span><span class="sxs-lookup"><span data-stu-id="8b327-270">App Service</span></span>
- <span data-ttu-id="8b327-271">Users must register the storage resource provider before they create their first Azure Function in the subscription.</span><span class="sxs-lookup"><span data-stu-id="8b327-271">Users must register the storage resource provider before they create their first Azure Function in the subscription.</span></span>

- <span data-ttu-id="8b327-272">In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span><span class="sxs-lookup"><span data-stu-id="8b327-272">In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span></span>


#### <a name="usage"></a><span data-ttu-id="8b327-273">Usage</span><span class="sxs-lookup"><span data-stu-id="8b327-273">Usage</span></span>  
- <span data-ttu-id="8b327-274">Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span><span class="sxs-lookup"><span data-stu-id="8b327-274">Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span></span> <span data-ttu-id="8b327-275">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span><span class="sxs-lookup"><span data-stu-id="8b327-275">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span></span>

<!--
#### Identity
-->



#### <a name="downloading-azure-stack-tools-from-github"></a><span data-ttu-id="8b327-276">Downloading Azure Stack Tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="8b327-276">Downloading Azure Stack Tools from GitHub</span></span>
- <span data-ttu-id="8b327-277">When using the *invoke-webrequest* PowerShell cmdlet to download the Azure Stack tools from Github, you receive an error:</span><span class="sxs-lookup"><span data-stu-id="8b327-277">When using the *invoke-webrequest* PowerShell cmdlet to download the Azure Stack tools from Github, you receive an error:</span></span>     
    -  <span data-ttu-id="8b327-278">*invoke-webrequest : The request was aborted: Could not create SSL/TLS secure channel.*</span><span class="sxs-lookup"><span data-stu-id="8b327-278">*invoke-webrequest : The request was aborted: Could not create SSL/TLS secure channel.*</span></span>     

  <span data-ttu-id="8b327-279">This error occurs because of a recent GitHub support deprecation of the Tlsv1 and Tlsv1.1 cryptographic standards (the default for PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8b327-279">This error occurs because of a recent GitHub support deprecation of the Tlsv1 and Tlsv1.1 cryptographic standards (the default for PowerShell).</span></span> <span data-ttu-id="8b327-280">For more information, see [Weak cryptographic standards removal notice](https://githubengineering.com/crypto-removal-notice/).</span><span class="sxs-lookup"><span data-stu-id="8b327-280">For more information, see [Weak cryptographic standards removal notice](https://githubengineering.com/crypto-removal-notice/).</span></span>

  <span data-ttu-id="8b327-281">To resolve this issue, add `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12` to the top of the script to force the PowerShell console to use TLSv1.2 when downloading from GitHub repositories.</span><span class="sxs-lookup"><span data-stu-id="8b327-281">To resolve this issue, add `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12` to the top of the script to force the PowerShell console to use TLSv1.2 when downloading from GitHub repositories.</span></span>


## <a name="download-the-update"></a><span data-ttu-id="8b327-282">Download the update</span><span class="sxs-lookup"><span data-stu-id="8b327-282">Download the update</span></span>
<span data-ttu-id="8b327-283">You can download the Azure Stack 1803 update package from [here](https://aka.ms/azurestackupdatedownload).</span><span class="sxs-lookup"><span data-stu-id="8b327-283">You can download the Azure Stack 1803 update package from [here](https://aka.ms/azurestackupdatedownload).</span></span>


## <a name="see-also"></a><span data-ttu-id="8b327-284">See also</span><span class="sxs-lookup"><span data-stu-id="8b327-284">See also</span></span>
- <span data-ttu-id="8b327-285">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-285">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span></span>
- <span data-ttu-id="8b327-286">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-286">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span></span>
- <span data-ttu-id="8b327-287">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="8b327-287">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span></span>
