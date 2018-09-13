---
title: Attach a disk to a classic Azure VM | Microsoft Docs
description: Attach a data disk to a Windows virtual machine created with the classic deployment model and initialize it.
services: virtual-machines-windows, storage
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: 2e37753b97d869b2591e04b004e15e8ec33d82db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553781"
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="03f8d-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="03f8d-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="03f8d-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03f8d-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="03f8d-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03f8d-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="03f8d-106">Before you attach a disk, review these tips:</span><span class="sxs-lookup"><span data-stu-id="03f8d-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="03f8d-107">The size of the virtual machine controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="03f8d-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="03f8d-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03f8d-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="03f8d-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03f8d-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="03f8d-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="03f8d-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="03f8d-111">Premium storage is available in certain regions.</span><span class="sxs-lookup"><span data-stu-id="03f8d-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="03f8d-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03f8d-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="03f8d-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span><span class="sxs-lookup"><span data-stu-id="03f8d-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="03f8d-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="03f8d-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03f8d-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03f8d-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="03f8d-116">Find the virtual machine</span><span class="sxs-lookup"><span data-stu-id="03f8d-116">Find the virtual machine</span></span>
1. <span data-ttu-id="03f8d-117">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="03f8d-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="03f8d-118">Select the virtual machine from the resource listed on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="03f8d-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="03f8d-119">In the left pane under **Settings**, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Open disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="03f8d-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="03f8d-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="03f8d-122">Option 1: Attach and initialize a new disk</span><span class="sxs-lookup"><span data-stu-id="03f8d-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="03f8d-123">On the **Disks** blade, click **Attach new**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="03f8d-124">Review the default settings, update as necessary, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/attach-disk/attach-new.png)

3. <span data-ttu-id="03f8d-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="03f8d-127">Initialize a new data disk</span><span class="sxs-lookup"><span data-stu-id="03f8d-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="03f8d-128">Connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03f8d-128">Connect to the virtual machine.</span></span> <span data-ttu-id="03f8d-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03f8d-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="03f8d-130">After you log on to the virtual machine, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="03f8d-131">In the left pane, select **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Open Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="03f8d-133">Select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-133">Select **Disks**.</span></span>
4. <span data-ttu-id="03f8d-134">The **Disks** section lists the disks.</span><span class="sxs-lookup"><span data-stu-id="03f8d-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="03f8d-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span><span class="sxs-lookup"><span data-stu-id="03f8d-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="03f8d-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="03f8d-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="03f8d-137">The data disk lists the Partition as **Unknown**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="03f8d-138">Right-click the disk and select **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="03f8d-139">You're notified that all data will be erased when the disk is initialized.</span><span class="sxs-lookup"><span data-stu-id="03f8d-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="03f8d-140">Click **Yes** to acknowledge the warning and initialize the disk.</span><span class="sxs-lookup"><span data-stu-id="03f8d-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="03f8d-141">Once complete, the partition will be listed as **GPT**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="03f8d-142">Right-click the disk again and select **New Volume**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="03f8d-143">Complete the wizard using the default values.</span><span class="sxs-lookup"><span data-stu-id="03f8d-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="03f8d-144">When the wizard is done, the **Volumes** section lists the new volume.</span><span class="sxs-lookup"><span data-stu-id="03f8d-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="03f8d-145">The disk is now online and ready to store data.</span><span class="sxs-lookup"><span data-stu-id="03f8d-145">The disk is now online and ready to store data.</span></span>

    ![Volume successfully initialized](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="03f8d-147">Option 2: Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="03f8d-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="03f8d-148">On the **Disks** blade, click **Attach existing**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="03f8d-149">Under **Attach existing disk**, click **Location**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Attach existing disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="03f8d-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="03f8d-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Find VHD location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="03f8d-153">Select the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="03f8d-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="03f8d-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="03f8d-155">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-155">Click **OK**.</span></span>
6. <span data-ttu-id="03f8d-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="03f8d-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="03f8d-157">Use TRIM with standard storage</span><span class="sxs-lookup"><span data-stu-id="03f8d-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="03f8d-158">If you use standard storage (HDD), you should enable TRIM.</span><span class="sxs-lookup"><span data-stu-id="03f8d-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="03f8d-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span><span class="sxs-lookup"><span data-stu-id="03f8d-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="03f8d-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span><span class="sxs-lookup"><span data-stu-id="03f8d-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="03f8d-161">You can run this command to check the TRIM setting.</span><span class="sxs-lookup"><span data-stu-id="03f8d-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="03f8d-162">Open a command prompt on your Windows VM and type:</span><span class="sxs-lookup"><span data-stu-id="03f8d-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="03f8d-163">If the command returns 0, TRIM is enabled correctly.</span><span class="sxs-lookup"><span data-stu-id="03f8d-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="03f8d-164">If it returns 1, run the following command to enable TRIM:</span><span class="sxs-lookup"><span data-stu-id="03f8d-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="03f8d-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="03f8d-165">Next steps</span></span>
<span data-ttu-id="03f8d-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="03f8d-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03f8d-167">Additional resources</span><span class="sxs-lookup"><span data-stu-id="03f8d-167">Additional resources</span></span>
[<span data-ttu-id="03f8d-168">About disks and VHDs for virtual machines</span><span class="sxs-lookup"><span data-stu-id="03f8d-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)






