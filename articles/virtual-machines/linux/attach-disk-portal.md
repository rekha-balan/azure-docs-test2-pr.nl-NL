---
title: Attach a data disk to a Linux VM | Microsoft Docs
description: How to attach new or existing data disk to a Linux VM in the Azure portal using the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 23ef6f16c1e104e559d29790a13e554a36ab8054
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555194"
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="1b522-103">How to attach a data disk to a Linux VM in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1b522-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="1b522-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b522-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="1b522-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b522-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1b522-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="1b522-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="1b522-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="1b522-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="1b522-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="1b522-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="1b522-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b522-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="1b522-110">Before you attach disks to your VM, review these tips:</span><span class="sxs-lookup"><span data-stu-id="1b522-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="1b522-111">The size of the virtual machine controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="1b522-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1b522-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b522-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1b522-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1b522-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="1b522-114">You can use both Premium and Standard disks with these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1b522-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="1b522-115">Premium storage is available in certain regions.</span><span class="sxs-lookup"><span data-stu-id="1b522-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="1b522-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b522-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1b522-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b522-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="1b522-118">For details, see [About disks and VHDs for virtual machines](../../storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b522-118">For details, see [About disks and VHDs for virtual machines](../../storage/storage-about-disks-and-vhds-linux.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="1b522-119">Find the virtual machine</span><span class="sxs-lookup"><span data-stu-id="1b522-119">Find the virtual machine</span></span>
1. <span data-ttu-id="1b522-120">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b522-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b522-121">On the Hub menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="1b522-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="1b522-122">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="1b522-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="1b522-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="1b522-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Open disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="1b522-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="1b522-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="1b522-126">Use Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="1b522-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1b522-127">Attach a new disk</span><span class="sxs-lookup"><span data-stu-id="1b522-127">Attach a new disk</span></span>

1. <span data-ttu-id="1b522-128">On the **Disks** blade, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="1b522-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1b522-129">Click the drop-down menu for **Name** and select **Create disk**:</span><span class="sxs-lookup"><span data-stu-id="1b522-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Create Azure managed disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="1b522-131">Enter a name for your managed disk.</span><span class="sxs-lookup"><span data-stu-id="1b522-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="1b522-132">Review the default settings, update as necessary, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b522-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="1b522-134">Click **Save** to create the managed disk and update the VM configuration:</span><span class="sxs-lookup"><span data-stu-id="1b522-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Save new Azure Managed Disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="1b522-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="1b522-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="1b522-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span><span class="sxs-lookup"><span data-stu-id="1b522-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Azure Managed Disk in resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1b522-139">Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="1b522-139">Attach an existing disk</span></span>
1. <span data-ttu-id="1b522-140">On the **Disks** blade, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="1b522-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1b522-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1b522-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="1b522-142">Select the managed disk to attach:</span><span class="sxs-lookup"><span data-stu-id="1b522-142">Select the managed disk to attach:</span></span>

   ![Attach existing Azure Managed Disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="1b522-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span><span class="sxs-lookup"><span data-stu-id="1b522-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Save Azure Managed Disk updates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="1b522-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="1b522-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="1b522-147">Use unmanaged disks</span><span class="sxs-lookup"><span data-stu-id="1b522-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1b522-148">Attach a new disk</span><span class="sxs-lookup"><span data-stu-id="1b522-148">Attach a new disk</span></span>

1. <span data-ttu-id="1b522-149">On the **Disks** blade, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="1b522-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1b522-150">Review the default settings, update as necessary, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b522-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Review disk settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="1b522-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="1b522-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1b522-153">Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="1b522-153">Attach an existing disk</span></span>
1. <span data-ttu-id="1b522-154">On the **Disks** blade, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="1b522-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1b522-155">Under **Attach existing disk**, click **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="1b522-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Attach existing disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="1b522-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="1b522-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Find VHD location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="1b522-159">Select the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="1b522-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="1b522-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="1b522-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="1b522-161">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b522-161">Click **OK**.</span></span>
6. <span data-ttu-id="1b522-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="1b522-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b522-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b522-163">Next steps</span></span>
<span data-ttu-id="1b522-164">After the disk is added, you need to prepare it for use.</span><span class="sxs-lookup"><span data-stu-id="1b522-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="1b522-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1b522-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>










