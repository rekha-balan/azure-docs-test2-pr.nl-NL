---
title: Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs in a Resource Manager deployment | Microsoft Docs
description: Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs in a Resource Manager deployment
services: storage
documentationcenter: ''
author: genlin
manager: felixwu
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: genli
ms.openlocfilehash: cb83f09e1ec5f1223fd225fc26188e4f08140eb8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669999"
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds-in-a-resource-manager-deployment"></a><span data-ttu-id="5a923-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs in a Resource Manager deployment</span><span class="sxs-lookup"><span data-stu-id="5a923-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs in a Resource Manager deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="5a923-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a923-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5a923-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span><span class="sxs-lookup"><span data-stu-id="5a923-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="5a923-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5a923-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5a923-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span><span class="sxs-lookup"><span data-stu-id="5a923-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="5a923-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="5a923-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="5a923-109">Symptoms</span><span class="sxs-lookup"><span data-stu-id="5a923-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="5a923-110">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="5a923-110">Scenario 1</span></span>
<span data-ttu-id="5a923-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="5a923-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5a923-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span><span class="sxs-lookup"><span data-stu-id="5a923-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5a923-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span><span class="sxs-lookup"><span data-stu-id="5a923-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="5a923-114">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="5a923-114">Scenario 2</span></span>
<span data-ttu-id="5a923-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="5a923-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5a923-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span><span class="sxs-lookup"><span data-stu-id="5a923-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5a923-117">This problem can occur because the container has a VHD that is locked in the lease state.</span><span class="sxs-lookup"><span data-stu-id="5a923-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="5a923-118">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="5a923-118">Scenario 3</span></span>
<span data-ttu-id="5a923-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="5a923-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5a923-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span><span class="sxs-lookup"><span data-stu-id="5a923-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="5a923-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span><span class="sxs-lookup"><span data-stu-id="5a923-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="5a923-122">Solution</span><span class="sxs-lookup"><span data-stu-id="5a923-122">Solution</span></span>
<span data-ttu-id="5a923-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span><span class="sxs-lookup"><span data-stu-id="5a923-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="5a923-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span><span class="sxs-lookup"><span data-stu-id="5a923-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="5a923-125">This removes the lease from the VHD and allows it to be deleted.</span><span class="sxs-lookup"><span data-stu-id="5a923-125">This removes the lease from the VHD and allows it to be deleted.</span></span>

### <a name="step-1-identify-the-problem-vhd-and-the-associated-vm"></a><span data-ttu-id="5a923-126">Step 1: Identify the problem VHD and the associated VM</span><span class="sxs-lookup"><span data-stu-id="5a923-126">Step 1: Identify the problem VHD and the associated VM</span></span>
1. <span data-ttu-id="5a923-127">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a923-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5a923-128">On the **Hub** menu, select **All resources**.</span><span class="sxs-lookup"><span data-stu-id="5a923-128">On the **Hub** menu, select **All resources**.</span></span> <span data-ttu-id="5a923-129">Go to the storage account that you want to delete, and then select **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5a923-129">Go to the storage account that you want to delete, and then select **Blobs** > **vhds**.</span></span>

    ![Screenshot of the portal, with the storage account and the "vhds" container highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)
3. <span data-ttu-id="5a923-131">Check the properties of each VHD in the container.</span><span class="sxs-lookup"><span data-stu-id="5a923-131">Check the properties of each VHD in the container.</span></span> <span data-ttu-id="5a923-132">Locate the VHD that is in the **Leased** state.</span><span class="sxs-lookup"><span data-stu-id="5a923-132">Locate the VHD that is in the **Leased** state.</span></span> <span data-ttu-id="5a923-133">Then, determine which VM is using the VHD.</span><span class="sxs-lookup"><span data-stu-id="5a923-133">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="5a923-134">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span><span class="sxs-lookup"><span data-stu-id="5a923-134">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

   * <span data-ttu-id="5a923-135">OS disks generally follow this naming convention: VMNameYYYYMMDDHHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5a923-135">OS disks generally follow this naming convention: VMNameYYYYMMDDHHMMSS.vhd</span></span>
   * <span data-ttu-id="5a923-136">Data disks generally follow this naming convention: VMName-YYYYMMDD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5a923-136">Data disks generally follow this naming convention: VMName-YYYYMMDD-HHMMSS.vhd</span></span>

     ![Screenshot of the container info in the portal, with the name of the VM, the lease status of "Locked", and the lease state of "Leased" highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-resource-manager-cannot-delete-storage-account-container-vhd/locatevm.png)

### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="5a923-138">Step 2: Remove the lease from the VHD</span><span class="sxs-lookup"><span data-stu-id="5a923-138">Step 2: Remove the lease from the VHD</span></span>
<span data-ttu-id="5a923-139">To delete the VM that is using the VHD (for OS disks):</span><span class="sxs-lookup"><span data-stu-id="5a923-139">To delete the VM that is using the VHD (for OS disks):</span></span>

1. <span data-ttu-id="5a923-140">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a923-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5a923-141">On the **Hub** menu, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="5a923-141">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5a923-142">Select the VM that holds a lease on the VHD.</span><span class="sxs-lookup"><span data-stu-id="5a923-142">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5a923-143">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a923-143">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="5a923-144">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="5a923-144">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="5a923-145">The VM should be deleted, but the VHD should be retained.</span><span class="sxs-lookup"><span data-stu-id="5a923-145">The VM should be deleted, but the VHD should be retained.</span></span> <span data-ttu-id="5a923-146">However, the VHD should no longer have a lease on it.</span><span class="sxs-lookup"><span data-stu-id="5a923-146">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5a923-147">It may take a few minutes for the lease to be released.</span><span class="sxs-lookup"><span data-stu-id="5a923-147">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5a923-148">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5a923-148">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5a923-149">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span><span class="sxs-lookup"><span data-stu-id="5a923-149">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="5a923-150">To detach the VHD from the VM that is using it (for data disks):</span><span class="sxs-lookup"><span data-stu-id="5a923-150">To detach the VHD from the VM that is using it (for data disks):</span></span>

1. <span data-ttu-id="5a923-151">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a923-151">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5a923-152">On the **Hub** menu, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="5a923-152">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5a923-153">Select the VM that holds a lease on the VHD.</span><span class="sxs-lookup"><span data-stu-id="5a923-153">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5a923-154">Select **Disks** on the **VM details** blade.</span><span class="sxs-lookup"><span data-stu-id="5a923-154">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="5a923-155">Select the data disk that holds a lease on the VHD.</span><span class="sxs-lookup"><span data-stu-id="5a923-155">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="5a923-156">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span><span class="sxs-lookup"><span data-stu-id="5a923-156">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="5a923-157">Determine with certainty that nothing is actively using the data disk.</span><span class="sxs-lookup"><span data-stu-id="5a923-157">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="5a923-158">Click **Detach** on the **Disk details** blade.</span><span class="sxs-lookup"><span data-stu-id="5a923-158">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="5a923-159">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span><span class="sxs-lookup"><span data-stu-id="5a923-159">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5a923-160">It may take a few minutes for the lease to be released.</span><span class="sxs-lookup"><span data-stu-id="5a923-160">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5a923-161">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5a923-161">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5a923-162">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span><span class="sxs-lookup"><span data-stu-id="5a923-162">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="5a923-163">What is a lease?</span><span class="sxs-lookup"><span data-stu-id="5a923-163">What is a lease?</span></span>
<span data-ttu-id="5a923-164">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span><span class="sxs-lookup"><span data-stu-id="5a923-164">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="5a923-165">When a blob is leased, only the owners of the lease can access the blob.</span><span class="sxs-lookup"><span data-stu-id="5a923-165">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="5a923-166">A lease is important for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="5a923-166">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="5a923-167">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span><span class="sxs-lookup"><span data-stu-id="5a923-167">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="5a923-168">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span><span class="sxs-lookup"><span data-stu-id="5a923-168">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="5a923-169">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span><span class="sxs-lookup"><span data-stu-id="5a923-169">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a923-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a923-170">Next steps</span></span>
* [<span data-ttu-id="5a923-171">Delete a storage account</span><span class="sxs-lookup"><span data-stu-id="5a923-171">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="5a923-172">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5a923-172">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)


