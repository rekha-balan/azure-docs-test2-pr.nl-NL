---
title: About disks and VHDs for Microsoft Azure Windows VMs | Microsoft Docs
description: Learn about the basics of disks and VHDs for Windows virtual machines in Azure.
services: storage
documentationcenter: ''
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: robinsh
ms.openlocfilehash: 3b9d6eb9bcc4afe0e68920bbd5da7c259ceb0c67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562688"
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="124a9-103">About disks and VHDs for Azure Windows VMs</span><span class="sxs-lookup"><span data-stu-id="124a9-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="124a9-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span><span class="sxs-lookup"><span data-stu-id="124a9-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="124a9-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span><span class="sxs-lookup"><span data-stu-id="124a9-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="124a9-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="124a9-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="124a9-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span><span class="sxs-lookup"><span data-stu-id="124a9-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="124a9-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span><span class="sxs-lookup"><span data-stu-id="124a9-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="124a9-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span><span class="sxs-lookup"><span data-stu-id="124a9-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="124a9-110">Disks used by VMs</span><span class="sxs-lookup"><span data-stu-id="124a9-110">Disks used by VMs</span></span>

<span data-ttu-id="124a9-111">Let's take a look at how the disks are used by the VMs.</span><span class="sxs-lookup"><span data-stu-id="124a9-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="124a9-112">Operating system disk</span><span class="sxs-lookup"><span data-stu-id="124a9-112">Operating system disk</span></span>
<span data-ttu-id="124a9-113">Every virtual machine has one attached operating system disk.</span><span class="sxs-lookup"><span data-stu-id="124a9-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="124a9-114">It's registered as a SATA drive and labeled as the C: drive by default.</span><span class="sxs-lookup"><span data-stu-id="124a9-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="124a9-115">This disk has a maximum capacity of 1023 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="124a9-115">This disk has a maximum capacity of 1023 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="124a9-116">Temporary disk</span><span class="sxs-lookup"><span data-stu-id="124a9-116">Temporary disk</span></span>
<span data-ttu-id="124a9-117">Each VM contains a temporary disk.</span><span class="sxs-lookup"><span data-stu-id="124a9-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="124a9-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span><span class="sxs-lookup"><span data-stu-id="124a9-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="124a9-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-planned-vs-unplanned-maintenance) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="124a9-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-planned-vs-unplanned-maintenance) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="124a9-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span><span class="sxs-lookup"><span data-stu-id="124a9-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="124a9-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="124a9-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="124a9-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="124a9-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="124a9-123">The size of the temporary disk varies, based on the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="124a9-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="124a9-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="124a9-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="124a9-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="124a9-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="124a9-126">Data disk</span><span class="sxs-lookup"><span data-stu-id="124a9-126">Data disk</span></span>
<span data-ttu-id="124a9-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span><span class="sxs-lookup"><span data-stu-id="124a9-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="124a9-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span><span class="sxs-lookup"><span data-stu-id="124a9-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="124a9-129">Each data disk has a maximum capacity of 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="124a9-129">Each data disk has a maximum capacity of 1023 GB.</span></span> <span data-ttu-id="124a9-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span><span class="sxs-lookup"><span data-stu-id="124a9-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="124a9-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="124a9-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="124a9-132">Azure creates an operating system disk when you create a virtual machine from an image.</span><span class="sxs-lookup"><span data-stu-id="124a9-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="124a9-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="124a9-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="124a9-134">Otherwise, you add data disks after you create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="124a9-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="124a9-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="124a9-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="124a9-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span><span class="sxs-lookup"><span data-stu-id="124a9-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="124a9-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span><span class="sxs-lookup"><span data-stu-id="124a9-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="124a9-138">One last recommendation: Use TRIM with unmanaged standard disks</span><span class="sxs-lookup"><span data-stu-id="124a9-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="124a9-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span><span class="sxs-lookup"><span data-stu-id="124a9-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="124a9-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span><span class="sxs-lookup"><span data-stu-id="124a9-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="124a9-141">This can save on costs if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="124a9-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="124a9-142">You can run this command to check the TRIM setting.</span><span class="sxs-lookup"><span data-stu-id="124a9-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="124a9-143">Open a command prompt on your Windows VM and type:</span><span class="sxs-lookup"><span data-stu-id="124a9-143">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="124a9-144">If the command returns 0, TRIM is enabled correctly.</span><span class="sxs-lookup"><span data-stu-id="124a9-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="124a9-145">If it returns 1, run the following command to enable TRIM:</span><span class="sxs-lookup"><span data-stu-id="124a9-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="124a9-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="124a9-146">Next steps</span></span>
* <span data-ttu-id="124a9-147">[Attach a disk](../virtual-machines/windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span><span class="sxs-lookup"><span data-stu-id="124a9-147">[Attach a disk](../virtual-machines/windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="124a9-148">[Upload a Windows VM image to Azure](../virtual-machines/windows/upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to use when creating a new VM.</span><span class="sxs-lookup"><span data-stu-id="124a9-148">[Upload a Windows VM image to Azure](../virtual-machines/windows/upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to use when creating a new VM.</span></span>
* <span data-ttu-id="124a9-149">[Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span><span class="sxs-lookup"><span data-stu-id="124a9-149">[Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

