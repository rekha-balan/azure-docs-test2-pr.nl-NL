---
title: Attach a data disk to a Windows VM | Microsoft Docs
description: How to attach new or existing data disk to a Windows VM in the Azure portal using the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: cynthn
ms.openlocfilehash: 413bcc645db582bc8716227ab0b863b0cfcaad8c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551169"
---
# <a name="how-to-attach-a-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="16a17-103">How to attach a data disk to a Windows VM in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="16a17-103">How to attach a data disk to a Windows VM in the Azure portal</span></span>
<span data-ttu-id="16a17-104">This article shows you how to attach both new and existing disks to a Windows virtual machine through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="16a17-104">This article shows you how to attach both new and existing disks to a Windows virtual machine through the Azure portal.</span></span> <span data-ttu-id="16a17-105">You can also [attach a data disk to a Linux VM in the Azure portal](../linux/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16a17-105">You can also [attach a data disk to a Linux VM in the Azure portal](../linux/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="16a17-106">Before you do this, review these tips:</span><span class="sxs-lookup"><span data-stu-id="16a17-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="16a17-107">The size of the virtual machine controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="16a17-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="16a17-108">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16a17-108">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="16a17-109">To use Premium storage, you'll need a DS-series or GS-series virtual machine.</span><span class="sxs-lookup"><span data-stu-id="16a17-109">To use Premium storage, you'll need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="16a17-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="16a17-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="16a17-111">Premium storage is available in certain regions.</span><span class="sxs-lookup"><span data-stu-id="16a17-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="16a17-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16a17-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="16a17-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span><span class="sxs-lookup"><span data-stu-id="16a17-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>
* <span data-ttu-id="16a17-114">For an existing disk, the .vhd file must be available in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="16a17-114">For an existing disk, the .vhd file must be available in an Azure storage account.</span></span> <span data-ttu-id="16a17-115">You can use a .vhd that's already there, if it's not attached to another virtual machine, or upload your own .vhd file to the storage account.</span><span class="sxs-lookup"><span data-stu-id="16a17-115">You can use a .vhd that's already there, if it's not attached to another virtual machine, or upload your own .vhd file to the storage account.</span></span>

<span data-ttu-id="16a17-116">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="16a17-116">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="find-the-virtual-machine"></a><span data-ttu-id="16a17-117">Find the virtual machine</span><span class="sxs-lookup"><span data-stu-id="16a17-117">Find the virtual machine</span></span>
1. <span data-ttu-id="16a17-118">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16a17-118">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="16a17-119">On the Hub menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="16a17-119">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="16a17-120">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="16a17-120">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="16a17-121">To the Virtual machines blade, in **Essentials**, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="16a17-121">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Open disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="16a17-123">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="16a17-123">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="16a17-124">Option 1: Attach and initialize a new disk</span><span class="sxs-lookup"><span data-stu-id="16a17-124">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="16a17-125">On the **Disks** blade, click **Attach new**.</span><span class="sxs-lookup"><span data-stu-id="16a17-125">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="16a17-126">Review the default settings, update as necessary, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="16a17-126">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="16a17-128">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="16a17-128">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="16a17-129">Initialize a new data disk</span><span class="sxs-lookup"><span data-stu-id="16a17-129">Initialize a new data disk</span></span>

1. <span data-ttu-id="16a17-130">Connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="16a17-130">Connect to the virtual machine.</span></span> <span data-ttu-id="16a17-131">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16a17-131">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="16a17-132">After you log on to the virtual machine, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="16a17-132">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="16a17-133">In the left pane, select **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="16a17-133">In the left pane, select **File and Storage Services**.</span></span>
   
    ![Open Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/fileandstorageservices.png)
3. <span data-ttu-id="16a17-135">Expand the menu and select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="16a17-135">Expand the menu and select **Disks**.</span></span>
4. <span data-ttu-id="16a17-136">The **Disks** section lists the disks.</span><span class="sxs-lookup"><span data-stu-id="16a17-136">The **Disks** section lists the disks.</span></span> <span data-ttu-id="16a17-137">In most cases, it will have disk 0, disk 1, and disk 2.</span><span class="sxs-lookup"><span data-stu-id="16a17-137">In most cases, it will have disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="16a17-138">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk you just attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="16a17-138">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk you just attached to the VM.</span></span> <span data-ttu-id="16a17-139">The new data disk will list the Partition as **Unknown**.</span><span class="sxs-lookup"><span data-stu-id="16a17-139">The new data disk will list the Partition as **Unknown**.</span></span> <span data-ttu-id="16a17-140">Right-click the disk and select **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="16a17-140">Right-click the disk and select **Initialize**.</span></span>
5. <span data-ttu-id="16a17-141">You're notified that all data will be erased when the disk is initialized.</span><span class="sxs-lookup"><span data-stu-id="16a17-141">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="16a17-142">Click **Yes** to acknowledge the warning and initialize the disk.</span><span class="sxs-lookup"><span data-stu-id="16a17-142">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="16a17-143">Once complete, the partition will be listed as **GPT**.</span><span class="sxs-lookup"><span data-stu-id="16a17-143">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="16a17-144">Right-click the disk again and select **New Volume**.</span><span class="sxs-lookup"><span data-stu-id="16a17-144">Right-click the disk again and select **New Volume**.</span></span>
6. <span data-ttu-id="16a17-145">Complete the wizard using the default values.</span><span class="sxs-lookup"><span data-stu-id="16a17-145">Complete the wizard using the default values.</span></span> <span data-ttu-id="16a17-146">When the wizard is done, the **Volumes** section lists the new volume.</span><span class="sxs-lookup"><span data-stu-id="16a17-146">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="16a17-147">The disk is now online and ready to store data.</span><span class="sxs-lookup"><span data-stu-id="16a17-147">The disk is now online and ready to store data.</span></span>

    ![Volume successfully initialized](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/newvolumecreated.png)


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="16a17-149">Option 2: Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="16a17-149">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="16a17-150">On the **Disks** blade, click **Attach existing**.</span><span class="sxs-lookup"><span data-stu-id="16a17-150">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="16a17-151">Under **Attach existing disk**, click **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="16a17-151">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Attach existing disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="16a17-153">Under **Storage accounts**, select the account and container that holds the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="16a17-153">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Find VHD location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="16a17-155">Select the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="16a17-155">Select the .vhd file.</span></span>
5. <span data-ttu-id="16a17-156">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="16a17-156">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="16a17-157">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="16a17-157">Click **OK**.</span></span>
6. <span data-ttu-id="16a17-158">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="16a17-158">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>



## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="16a17-159">Use TRIM with standard storage</span><span class="sxs-lookup"><span data-stu-id="16a17-159">Use TRIM with standard storage</span></span>

<span data-ttu-id="16a17-160">If you use standard storage (HDD), you should enable TRIM.</span><span class="sxs-lookup"><span data-stu-id="16a17-160">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="16a17-161">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span><span class="sxs-lookup"><span data-stu-id="16a17-161">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="16a17-162">This can save on costs if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="16a17-162">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="16a17-163">You can run this command to check the TRIM setting.</span><span class="sxs-lookup"><span data-stu-id="16a17-163">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="16a17-164">Open a command prompt on your Windows VM and type:</span><span class="sxs-lookup"><span data-stu-id="16a17-164">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="16a17-165">If the command returns 0, TRIM is enabled correctly.</span><span class="sxs-lookup"><span data-stu-id="16a17-165">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="16a17-166">If it returns 1, run the following command to enable TRIM:</span><span class="sxs-lookup"><span data-stu-id="16a17-166">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```
                
<span data-ttu-id="16a17-167">After deleting data from your disk you can ensure the TRIM operations flush properly by running defrag with TRIM:</span><span class="sxs-lookup"><span data-stu-id="16a17-167">After deleting data from your disk you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

## <a name="next-steps"></a><span data-ttu-id="16a17-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="16a17-168">Next steps</span></span>
<span data-ttu-id="16a17-169">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16a17-169">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>







