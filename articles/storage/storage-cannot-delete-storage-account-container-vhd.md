---
title: Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment| Microsoft Docs
description: Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment
services: storage
documentationcenter: ''
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: genli
ms.openlocfilehash: f385e87ebacfc8e39326c0148adefc05dbb68e67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562684"
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="4d635-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span><span class="sxs-lookup"><span data-stu-id="4d635-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="4d635-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d635-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="4d635-105">The issues can be caused by the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="4d635-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="4d635-106">When you delete a VM, the disk and VHD are not automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="4d635-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="4d635-107">That might be the reason for failure on storage account deletion.</span><span class="sxs-lookup"><span data-stu-id="4d635-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="4d635-108">We don't delete the disk so that you can use the disk to mount another VM.</span><span class="sxs-lookup"><span data-stu-id="4d635-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="4d635-109">There is still a lease on a disk or the blob that's associated with the disk.</span><span class="sxs-lookup"><span data-stu-id="4d635-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="4d635-110">There is still a VM image that is using a blob, container, or storage account.</span><span class="sxs-lookup"><span data-stu-id="4d635-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="4d635-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="4d635-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="4d635-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span><span class="sxs-lookup"><span data-stu-id="4d635-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="4d635-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="4d635-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="4d635-114">Symptoms</span><span class="sxs-lookup"><span data-stu-id="4d635-114">Symptoms</span></span>
<span data-ttu-id="4d635-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span><span class="sxs-lookup"><span data-stu-id="4d635-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="4d635-116">Scenario 1: Unable to delete a storage account</span><span class="sxs-lookup"><span data-stu-id="4d635-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="4d635-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span><span class="sxs-lookup"><span data-stu-id="4d635-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Image of error when delete the Storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="4d635-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span><span class="sxs-lookup"><span data-stu-id="4d635-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="4d635-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span><span class="sxs-lookup"><span data-stu-id="4d635-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="4d635-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span><span class="sxs-lookup"><span data-stu-id="4d635-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="4d635-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span><span class="sxs-lookup"><span data-stu-id="4d635-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="4d635-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span><span class="sxs-lookup"><span data-stu-id="4d635-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="4d635-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span><span class="sxs-lookup"><span data-stu-id="4d635-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="4d635-125">Scenario 2: Unable to delete a container</span><span class="sxs-lookup"><span data-stu-id="4d635-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="4d635-126">When you try to delete the storage container, you might see the following error:</span><span class="sxs-lookup"><span data-stu-id="4d635-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="4d635-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span><span class="sxs-lookup"><span data-stu-id="4d635-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="4d635-128">Or</span><span class="sxs-lookup"><span data-stu-id="4d635-128">Or</span></span>

<span data-ttu-id="4d635-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span><span class="sxs-lookup"><span data-stu-id="4d635-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="4d635-130">Scenario 3: Unable to delete a VHD</span><span class="sxs-lookup"><span data-stu-id="4d635-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="4d635-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span><span class="sxs-lookup"><span data-stu-id="4d635-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="4d635-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span><span class="sxs-lookup"><span data-stu-id="4d635-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="4d635-133">Or</span><span class="sxs-lookup"><span data-stu-id="4d635-133">Or</span></span>

<span data-ttu-id="4d635-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span><span class="sxs-lookup"><span data-stu-id="4d635-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="4d635-135">Solution</span><span class="sxs-lookup"><span data-stu-id="4d635-135">Solution</span></span>
<span data-ttu-id="4d635-136">To resolve the most common issues, try the following method:</span><span class="sxs-lookup"><span data-stu-id="4d635-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="4d635-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span><span class="sxs-lookup"><span data-stu-id="4d635-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="4d635-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d635-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="4d635-139">Select **VIRTUAL MACHINE** > **DISKS**.</span><span class="sxs-lookup"><span data-stu-id="4d635-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Image of disks on virtual machines on Azure classic portal.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="4d635-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="4d635-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="4d635-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span><span class="sxs-lookup"><span data-stu-id="4d635-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Image that shows location information for disks on Azure classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="4d635-144">Delete the disks by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="4d635-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="4d635-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span><span class="sxs-lookup"><span data-stu-id="4d635-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="4d635-146">If the disk is a data disk, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d635-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="4d635-147">Check the name of the VM that the disk is attached to.</span><span class="sxs-lookup"><span data-stu-id="4d635-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="4d635-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span><span class="sxs-lookup"><span data-stu-id="4d635-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="4d635-149">Make sure that nothing is actively using the disk.</span><span class="sxs-lookup"><span data-stu-id="4d635-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="4d635-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span><span class="sxs-lookup"><span data-stu-id="4d635-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="4d635-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span><span class="sxs-lookup"><span data-stu-id="4d635-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="4d635-152">This indicates the disk has successfully detached from the VM.</span><span class="sxs-lookup"><span data-stu-id="4d635-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="4d635-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span><span class="sxs-lookup"><span data-stu-id="4d635-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="4d635-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span><span class="sxs-lookup"><span data-stu-id="4d635-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="4d635-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span><span class="sxs-lookup"><span data-stu-id="4d635-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="4d635-156">Check the name of the Virtual Machine the Data Disk is attached to.</span><span class="sxs-lookup"><span data-stu-id="4d635-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="4d635-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span><span class="sxs-lookup"><span data-stu-id="4d635-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="4d635-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4d635-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="4d635-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span><span class="sxs-lookup"><span data-stu-id="4d635-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="4d635-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span><span class="sxs-lookup"><span data-stu-id="4d635-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="4d635-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span><span class="sxs-lookup"><span data-stu-id="4d635-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="4d635-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span><span class="sxs-lookup"><span data-stu-id="4d635-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="4d635-163">This indicates the disk has fully detached from the VM.</span><span class="sxs-lookup"><span data-stu-id="4d635-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="4d635-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span><span class="sxs-lookup"><span data-stu-id="4d635-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="4d635-165">If a disk is attached to a VM, you will not be able to delete it.</span><span class="sxs-lookup"><span data-stu-id="4d635-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="4d635-166">Disks are detached from a deleted VM asynchronously.</span><span class="sxs-lookup"><span data-stu-id="4d635-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="4d635-167">It might take a few minutes after the VM is deleted for this field to clear up.</span><span class="sxs-lookup"><span data-stu-id="4d635-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="4d635-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span><span class="sxs-lookup"><span data-stu-id="4d635-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="4d635-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d635-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="4d635-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span><span class="sxs-lookup"><span data-stu-id="4d635-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="4d635-171">After that, try to delete the storage account, container, or VHD again.</span><span class="sxs-lookup"><span data-stu-id="4d635-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="4d635-172">Be sure to back up anything you want to save before you delete the account.</span><span class="sxs-lookup"><span data-stu-id="4d635-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="4d635-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="4d635-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="4d635-174">Ensure that the resource is not in use.</span><span class="sxs-lookup"><span data-stu-id="4d635-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="4d635-175">About the Stopped (deallocated) status</span><span class="sxs-lookup"><span data-stu-id="4d635-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="4d635-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d635-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="4d635-177">**Azure classic portal**:</span><span class="sxs-lookup"><span data-stu-id="4d635-177">**Azure classic portal**:</span></span>

![Stopped (Deallocated) status for VMs on Azure portal.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="4d635-179">**Azure portal**:</span><span class="sxs-lookup"><span data-stu-id="4d635-179">**Azure portal**:</span></span>

![Stopped (deallocated) status for VMs on Azure classic portal.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="4d635-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span><span class="sxs-lookup"><span data-stu-id="4d635-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="4d635-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span><span class="sxs-lookup"><span data-stu-id="4d635-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="4d635-183">These disks are created on top of VHDs, which are backed by Azure storage.</span><span class="sxs-lookup"><span data-stu-id="4d635-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="4d635-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span><span class="sxs-lookup"><span data-stu-id="4d635-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d635-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d635-185">Next steps</span></span>
* [<span data-ttu-id="4d635-186">Delete a storage account</span><span class="sxs-lookup"><span data-stu-id="4d635-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="4d635-187">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4d635-187">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)





