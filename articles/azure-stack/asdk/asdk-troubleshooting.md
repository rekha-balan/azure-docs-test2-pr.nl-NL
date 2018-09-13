---
title: Microsoft Azure Stack troubleshooting | Microsoft Docs
description: Azure Stack Development Kit (ASDK) troubleshooting information.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 6c715f07f75c9196b7cf2cc8659c6e541e1260da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856861"
---
# <a name="microsoft-azure-stack-development-kit-asdk-troubleshooting"></a><span data-ttu-id="3f3ed-103">Microsoft Azure Stack Development Kit (ASDK) troubleshooting</span><span class="sxs-lookup"><span data-stu-id="3f3ed-103">Microsoft Azure Stack Development Kit (ASDK) troubleshooting</span></span>
<span data-ttu-id="3f3ed-104">This document provides common troubleshooting information for the ASDK.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-104">This document provides common troubleshooting information for the ASDK.</span></span> <span data-ttu-id="3f3ed-105">If you are experiencing an issue that is not documented, make sure to check the [Azure Stack MSDN Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) for further assistance and information.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-105">If you are experiencing an issue that is not documented, make sure to check the [Azure Stack MSDN Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) for further assistance and information.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3f3ed-106">Because the ASDK is an evaluation environment, there is no official support offered through Microsoft Customer Support Services (CSS).</span><span class="sxs-lookup"><span data-stu-id="3f3ed-106">Because the ASDK is an evaluation environment, there is no official support offered through Microsoft Customer Support Services (CSS).</span></span>

<span data-ttu-id="3f3ed-107">The recommendations for troubleshooting issues that are described in this section are derived from several sources and may or may not resolve your particular issue.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-107">The recommendations for troubleshooting issues that are described in this section are derived from several sources and may or may not resolve your particular issue.</span></span> <span data-ttu-id="3f3ed-108">Code examples are provided "as is" and expected results cannot be guaranteed.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-108">Code examples are provided "as is" and expected results cannot be guaranteed.</span></span> <span data-ttu-id="3f3ed-109">This section is subject to frequent edits and updates as improvements to the product are implemented.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-109">This section is subject to frequent edits and updates as improvements to the product are implemented.</span></span>

## <a name="deployment"></a><span data-ttu-id="3f3ed-110">Deployment</span><span class="sxs-lookup"><span data-stu-id="3f3ed-110">Deployment</span></span>
### <a name="deployment-failure"></a><span data-ttu-id="3f3ed-111">Deployment failure</span><span class="sxs-lookup"><span data-stu-id="3f3ed-111">Deployment failure</span></span>
<span data-ttu-id="3f3ed-112">If you experience a failure during installation, you can restart the deployment from the failed step by using the -rerun option of the deployment script as in the following example:</span><span class="sxs-lookup"><span data-stu-id="3f3ed-112">If you experience a failure during installation, you can restart the deployment from the failed step by using the -rerun option of the deployment script as in the following example:</span></span>

  ```powershell
  cd C:\CloudDeployment\Setup
  .\InstallAzureStackPOC.ps1 -Rerun
  ```

### <a name="at-the-end-of-the-deployment-the-powershell-session-is-still-open-and-doesnt-show-any-output"></a><span data-ttu-id="3f3ed-113">At the end of the deployment, the PowerShell session is still open and doesn’t show any output</span><span class="sxs-lookup"><span data-stu-id="3f3ed-113">At the end of the deployment, the PowerShell session is still open and doesn’t show any output</span></span>
<span data-ttu-id="3f3ed-114">This behavior is probably just the result of the default behavior of a PowerShell command window, when it has been selected.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-114">This behavior is probably just the result of the default behavior of a PowerShell command window, when it has been selected.</span></span> <span data-ttu-id="3f3ed-115">The development kit deployment has succeeded but the script was paused when selecting the window.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-115">The development kit deployment has succeeded but the script was paused when selecting the window.</span></span> <span data-ttu-id="3f3ed-116">You can verify setup has completed by looking for the word "select" in the titlebar of the command window.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-116">You can verify setup has completed by looking for the word "select" in the titlebar of the command window.</span></span> <span data-ttu-id="3f3ed-117">Press the ESC key to unselect it, and the completion message should be shown after it.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-117">Press the ESC key to unselect it, and the completion message should be shown after it.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="3f3ed-118">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="3f3ed-118">Virtual machines</span></span>
### <a name="default-image-and-gallery-item"></a><span data-ttu-id="3f3ed-119">Default image and gallery item</span><span class="sxs-lookup"><span data-stu-id="3f3ed-119">Default image and gallery item</span></span>
<span data-ttu-id="3f3ed-120">A Windows Server image and gallery item must be added before deploying VMs in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-120">A Windows Server image and gallery item must be added before deploying VMs in Azure Stack.</span></span>

### <a name="after-restarting-my-azure-stack-host-some-vms-may-not-automatically-start"></a><span data-ttu-id="3f3ed-121">After restarting my Azure Stack host, some VMs may not automatically start.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-121">After restarting my Azure Stack host, some VMs may not automatically start.</span></span>
<span data-ttu-id="3f3ed-122">After rebooting your host, you may notice Azure Stack services are not immediately available.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-122">After rebooting your host, you may notice Azure Stack services are not immediately available.</span></span> <span data-ttu-id="3f3ed-123">This is because Azure Stack [infrastructure VMs](asdk-architecture.md#virtual-machine-roles) and RPs take some time to check consistency, but will eventually start automatically.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-123">This is because Azure Stack [infrastructure VMs](asdk-architecture.md#virtual-machine-roles) and RPs take some time to check consistency, but will eventually start automatically.</span></span>

<span data-ttu-id="3f3ed-124">You may also notice that tenant VMs don't automatically start after a reboot of the Azure Stack development kit host.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-124">You may also notice that tenant VMs don't automatically start after a reboot of the Azure Stack development kit host.</span></span> <span data-ttu-id="3f3ed-125">This is a known issue, and just requires a few manual steps to bring them online:</span><span class="sxs-lookup"><span data-stu-id="3f3ed-125">This is a known issue, and just requires a few manual steps to bring them online:</span></span>

1.  <span data-ttu-id="3f3ed-126">On the Azure Stack development kit host, start **Failover Cluster Manager** from the Start Menu.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-126">On the Azure Stack development kit host, start **Failover Cluster Manager** from the Start Menu.</span></span>
2.  <span data-ttu-id="3f3ed-127">Select the cluster **S-Cluster.azurestack.local**.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-127">Select the cluster **S-Cluster.azurestack.local**.</span></span>
3.  <span data-ttu-id="3f3ed-128">Select **Roles**.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-128">Select **Roles**.</span></span>
4.  <span data-ttu-id="3f3ed-129">Tenant VMs appear in a *saved* state.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-129">Tenant VMs appear in a *saved* state.</span></span> <span data-ttu-id="3f3ed-130">Once all Infrastructure VMs are running, right-click the tenant VMs and select **Start** to resume the VM.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-130">Once all Infrastructure VMs are running, right-click the tenant VMs and select **Start** to resume the VM.</span></span>

### <a name="i-have-deleted-some-virtual-machines-but-still-see-the-vhd-files-on-disk-is-this-behavior-expected"></a><span data-ttu-id="3f3ed-131">I have deleted some virtual machines, but still see the VHD files on disk.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-131">I have deleted some virtual machines, but still see the VHD files on disk.</span></span> <span data-ttu-id="3f3ed-132">Is this behavior expected?</span><span class="sxs-lookup"><span data-stu-id="3f3ed-132">Is this behavior expected?</span></span>
<span data-ttu-id="3f3ed-133">Yes, this is behavior expected.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-133">Yes, this is behavior expected.</span></span> <span data-ttu-id="3f3ed-134">It was designed this way because:</span><span class="sxs-lookup"><span data-stu-id="3f3ed-134">It was designed this way because:</span></span>

* <span data-ttu-id="3f3ed-135">When you delete a VM, VHDs are not deleted.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-135">When you delete a VM, VHDs are not deleted.</span></span> <span data-ttu-id="3f3ed-136">Disks are separate resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-136">Disks are separate resources in the resource group.</span></span>
* <span data-ttu-id="3f3ed-137">When a storage account gets deleted, the deletion is visible immediately through Azure Resource Manager, but the disks it may contain are still kept in storage until garbage collection runs.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-137">When a storage account gets deleted, the deletion is visible immediately through Azure Resource Manager, but the disks it may contain are still kept in storage until garbage collection runs.</span></span>

<span data-ttu-id="3f3ed-138">If you see "orphan" VHDs, it is important to know if they are part of the folder for a storage account that was deleted.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-138">If you see "orphan" VHDs, it is important to know if they are part of the folder for a storage account that was deleted.</span></span> <span data-ttu-id="3f3ed-139">If the storage account was not deleted, it's normal they are still there.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-139">If the storage account was not deleted, it's normal they are still there.</span></span>

<span data-ttu-id="3f3ed-140">You can read more about configuring the retention threshold and on-demand reclamation in [manage storage accounts](.\.\azure-stack-manage-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3f3ed-140">You can read more about configuring the retention threshold and on-demand reclamation in [manage storage accounts](.\.\azure-stack-manage-storage-accounts.md).</span></span>

## <a name="storage"></a><span data-ttu-id="3f3ed-141">Storage</span><span class="sxs-lookup"><span data-stu-id="3f3ed-141">Storage</span></span>
### <a name="storage-reclamation"></a><span data-ttu-id="3f3ed-142">Storage reclamation</span><span class="sxs-lookup"><span data-stu-id="3f3ed-142">Storage reclamation</span></span>
<span data-ttu-id="3f3ed-143">It may take up to 14 hours for reclaimed capacity to show up in the portal.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-143">It may take up to 14 hours for reclaimed capacity to show up in the portal.</span></span> <span data-ttu-id="3f3ed-144">Space reclamation depends on various factors including usage percentage of internal container files in block blob store.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-144">Space reclamation depends on various factors including usage percentage of internal container files in block blob store.</span></span> <span data-ttu-id="3f3ed-145">Therefore, depending on how much data is deleted, there is no guarantee on the amount of space that could be reclaimed when garbage collector runs.</span><span class="sxs-lookup"><span data-stu-id="3f3ed-145">Therefore, depending on how much data is deleted, there is no guarantee on the amount of space that could be reclaimed when garbage collector runs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f3ed-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f3ed-146">Next steps</span></span>
[<span data-ttu-id="3f3ed-147">Visit the Azure Stack support forum</span><span class="sxs-lookup"><span data-stu-id="3f3ed-147">Visit the Azure Stack support forum</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)

