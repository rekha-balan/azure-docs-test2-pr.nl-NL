---
title: include file
description: include file
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 06/03/2018
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: e8005da056c08b21bf0b91dc71b3dafac281de1f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965777"
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="147a2-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span><span class="sxs-lookup"><span data-stu-id="147a2-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="147a2-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium SSD disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium SSD disks.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="147a2-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="147a2-105">Managed Disks</span></span>

<span data-ttu-id="147a2-106">**What is Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="147a2-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span><span class="sxs-lookup"><span data-stu-id="147a2-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="147a2-108">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="147a2-108">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="147a2-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span><span class="sxs-lookup"><span data-stu-id="147a2-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="147a2-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="147a2-111">You're charged according to the S10 disk pricing.</span><span class="sxs-lookup"><span data-stu-id="147a2-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="147a2-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="147a2-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="147a2-113">**Are there any transaction costs for standard managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="147a2-114">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-114">Yes.</span></span> <span data-ttu-id="147a2-115">You're charged for each transaction.</span><span class="sxs-lookup"><span data-stu-id="147a2-115">You're charged for each transaction.</span></span> <span data-ttu-id="147a2-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="147a2-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="147a2-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="147a2-118">You're charged based on the provisioned capacity of the disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="147a2-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="147a2-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="147a2-120">**How is pricing of premium managed disks different from unmanaged disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="147a2-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="147a2-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="147a2-123">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-123">Yes.</span></span> <span data-ttu-id="147a2-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="147a2-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="147a2-125">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span><span class="sxs-lookup"><span data-stu-id="147a2-125">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="147a2-126">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-126">Yes.</span></span>

<span data-ttu-id="147a2-127">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span><span class="sxs-lookup"><span data-stu-id="147a2-127">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="147a2-128">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-128">No.</span></span>

<span data-ttu-id="147a2-129">**Are there any scale limitations for customers that use managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-129">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="147a2-130">Managed Disks eliminates the limits associated with storage accounts.</span><span class="sxs-lookup"><span data-stu-id="147a2-130">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="147a2-131">However, the maximum limit is 50,000 managed disks per region and per disk type for a subscription.</span><span class="sxs-lookup"><span data-stu-id="147a2-131">However, the maximum limit is 50,000 managed disks per region and per disk type for a subscription.</span></span>

<span data-ttu-id="147a2-132">**Can I take an incremental snapshot of a managed disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-132">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="147a2-133">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-133">No.</span></span> <span data-ttu-id="147a2-134">The current snapshot capability makes a full copy of a managed disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-134">The current snapshot capability makes a full copy of a managed disk.</span></span>

<span data-ttu-id="147a2-135">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-135">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="147a2-136">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-136">No.</span></span> <span data-ttu-id="147a2-137">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-137">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="147a2-138">When you create an availability set, you can choose which type of disks you want to use.</span><span class="sxs-lookup"><span data-stu-id="147a2-138">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="147a2-139">**Is Managed Disks the default option in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="147a2-139">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="147a2-140">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-140">Yes.</span></span>

<span data-ttu-id="147a2-141">**Can I create an empty managed disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-141">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="147a2-142">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-142">Yes.</span></span> <span data-ttu-id="147a2-143">You can create an empty disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-143">You can create an empty disk.</span></span> <span data-ttu-id="147a2-144">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span><span class="sxs-lookup"><span data-stu-id="147a2-144">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="147a2-145">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-145">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="147a2-146">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span><span class="sxs-lookup"><span data-stu-id="147a2-146">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="147a2-147">**How is the standard storage account for diagnostics set up?**</span><span class="sxs-lookup"><span data-stu-id="147a2-147">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="147a2-148">You set up a private storage account for VM diagnostics.</span><span class="sxs-lookup"><span data-stu-id="147a2-148">You set up a private storage account for VM diagnostics.</span></span>

<span data-ttu-id="147a2-149">**What kind of Role-Based Access Control support is available for Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-149">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="147a2-150">Managed Disks supports three key default roles:</span><span class="sxs-lookup"><span data-stu-id="147a2-150">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="147a2-151">Owner: Can manage everything, including access</span><span class="sxs-lookup"><span data-stu-id="147a2-151">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="147a2-152">Contributor: Can manage everything except access</span><span class="sxs-lookup"><span data-stu-id="147a2-152">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="147a2-153">Reader: Can view everything, but can't make changes</span><span class="sxs-lookup"><span data-stu-id="147a2-153">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="147a2-154">**Is there a way that I can copy or export a managed disk to a private storage account?**</span><span class="sxs-lookup"><span data-stu-id="147a2-154">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="147a2-155">You can generate a read-only shared access signature (SAS) URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span><span class="sxs-lookup"><span data-stu-id="147a2-155">You can generate a read-only shared access signature (SAS) URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span> <span data-ttu-id="147a2-156">You can use the SAS URI using the Azure portal, Azure PowerShell, the Azure CLI, or [AzCopy](../articles/storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="147a2-156">You can use the SAS URI using the Azure portal, Azure PowerShell, the Azure CLI, or [AzCopy](../articles/storage/common/storage-use-azcopy.md)</span></span>

<span data-ttu-id="147a2-157">**Can I create a copy of my managed disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-157">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="147a2-158">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-158">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="147a2-159">**Are unmanaged disks still supported?**</span><span class="sxs-lookup"><span data-stu-id="147a2-159">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="147a2-160">Yes, both unmanaged and managed disks are supported.</span><span class="sxs-lookup"><span data-stu-id="147a2-160">Yes, both unmanaged and managed disks are supported.</span></span> <span data-ttu-id="147a2-161">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-161">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>

<span data-ttu-id="147a2-162">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (256 GB)?**</span><span class="sxs-lookup"><span data-stu-id="147a2-162">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (256 GB)?**</span></span>

<span data-ttu-id="147a2-163">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-163">Yes.</span></span>

<span data-ttu-id="147a2-164">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-164">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="147a2-165">Azure Managed Disks currently supports only locally redundant storage managed disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-165">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="147a2-166">**Can I shrink or downsize my managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-166">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="147a2-167">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-167">No.</span></span> <span data-ttu-id="147a2-168">This feature is not supported currently.</span><span class="sxs-lookup"><span data-stu-id="147a2-168">This feature is not supported currently.</span></span> 

<span data-ttu-id="147a2-169">**Can I break a lease on my disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-169">**Can I break a lease on my disk?**</span></span>

<span data-ttu-id="147a2-170">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-170">No.</span></span> <span data-ttu-id="147a2-171">This is not supported currently as a lease is present to prevent accidental deletion when the disk is being used.</span><span class="sxs-lookup"><span data-stu-id="147a2-171">This is not supported currently as a lease is present to prevent accidental deletion when the disk is being used.</span></span>

<span data-ttu-id="147a2-172">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span><span class="sxs-lookup"><span data-stu-id="147a2-172">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="147a2-173">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-173">No.</span></span> <span data-ttu-id="147a2-174">You can't update the computer name property.</span><span class="sxs-lookup"><span data-stu-id="147a2-174">You can't update the computer name property.</span></span> <span data-ttu-id="147a2-175">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-175">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="147a2-176">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-176">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="147a2-177">List of templates using Managed Disks</span><span class="sxs-lookup"><span data-stu-id="147a2-177">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

<span data-ttu-id="147a2-178">**Can I co-locate unmanaged and managed disks on the same VM?**</span><span class="sxs-lookup"><span data-stu-id="147a2-178">**Can I co-locate unmanaged and managed disks on the same VM?**</span></span>

<span data-ttu-id="147a2-179">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-179">No.</span></span>

<span data-ttu-id="147a2-180">**When creating a disk from a blob, is there any continually existing relationship with that source blob?**</span><span class="sxs-lookup"><span data-stu-id="147a2-180">**When creating a disk from a blob, is there any continually existing relationship with that source blob?**</span></span>

<span data-ttu-id="147a2-181">No, when the new disk is created it is a full standalone copy of that blob at that time and there is no connection between the two.</span><span class="sxs-lookup"><span data-stu-id="147a2-181">No, when the new disk is created it is a full standalone copy of that blob at that time and there is no connection between the two.</span></span> <span data-ttu-id="147a2-182">If you like, once you've created the disk, the source blob may be deleted without affecting the newly created disk in any way.</span><span class="sxs-lookup"><span data-stu-id="147a2-182">If you like, once you've created the disk, the source blob may be deleted without affecting the newly created disk in any way.</span></span>

<span data-ttu-id="147a2-183">**Can I rename a managed or unmanaged disk after it has been created?**</span><span class="sxs-lookup"><span data-stu-id="147a2-183">**Can I rename a managed or unmanaged disk after it has been created?**</span></span>

<span data-ttu-id="147a2-184">For managed disks you cannot rename them.</span><span class="sxs-lookup"><span data-stu-id="147a2-184">For managed disks you cannot rename them.</span></span> <span data-ttu-id="147a2-185">However, you may rename an unmanaged disk as long as it is not currently attached to a VHD or VM.</span><span class="sxs-lookup"><span data-stu-id="147a2-185">However, you may rename an unmanaged disk as long as it is not currently attached to a VHD or VM.</span></span>

## <a name="standard-ssd-disks-preview"></a><span data-ttu-id="147a2-186">Standard SSD disks (Preview)</span><span class="sxs-lookup"><span data-stu-id="147a2-186">Standard SSD disks (Preview)</span></span>

<span data-ttu-id="147a2-187">**What are Azure Standard SSD disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-187">**What are Azure Standard SSD disks?**</span></span>
<span data-ttu-id="147a2-188">Standard SSD disks are standard disks backed by solid-state media, optimized as cost effective storage for workloads that need consistent performance at lower IOPS levels.</span><span class="sxs-lookup"><span data-stu-id="147a2-188">Standard SSD disks are standard disks backed by solid-state media, optimized as cost effective storage for workloads that need consistent performance at lower IOPS levels.</span></span> <span data-ttu-id="147a2-189">In preview, they are available in a limited number of regions, with limited manageability (available through Resource Manager templates).</span><span class="sxs-lookup"><span data-stu-id="147a2-189">In preview, they are available in a limited number of regions, with limited manageability (available through Resource Manager templates).</span></span>

<a id="standard-ssds-azure-regions"></a><span data-ttu-id="147a2-190">**What are the regions currently supported for Standard SSD disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-190">**What are the regions currently supported for Standard SSD disks?**</span></span>
<span data-ttu-id="147a2-191">All Azure regions now support Standard SSD disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-191">All Azure regions now support Standard SSD disks.</span></span>

<span data-ttu-id="147a2-192">**How do I create Standard SSD disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-192">**How do I create Standard SSD disks?**</span></span>
<span data-ttu-id="147a2-193">You can create Standard SSD disks using Azure Resource Manager templates, SDK, PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="147a2-193">You can create Standard SSD disks using Azure Resource Manager templates, SDK, PowerShell or CLI.</span></span> <span data-ttu-id="147a2-194">Below are the parameters needed in the Resource Manager template to create Standard SSD Disks:</span><span class="sxs-lookup"><span data-stu-id="147a2-194">Below are the parameters needed in the Resource Manager template to create Standard SSD Disks:</span></span>

* <span data-ttu-id="147a2-195">*apiVersion* for Microsoft.Compute must be set as `2018-04-01` (or later)</span><span class="sxs-lookup"><span data-stu-id="147a2-195">*apiVersion* for Microsoft.Compute must be set as `2018-04-01` (or later)</span></span>
* <span data-ttu-id="147a2-196">Specify *managedDisk.storageAccountType* as `StandardSSD_LRS`</span><span class="sxs-lookup"><span data-stu-id="147a2-196">Specify *managedDisk.storageAccountType* as `StandardSSD_LRS`</span></span>

<span data-ttu-id="147a2-197">The following example shows the *properties.storageProfile.osDisk* section for a VM that uses Standard SSD Disks:</span><span class="sxs-lookup"><span data-stu-id="147a2-197">The following example shows the *properties.storageProfile.osDisk* section for a VM that uses Standard SSD Disks:</span></span>

```json
"osDisk": {
    "osType": "Windows",
    "name": "myOsDisk",
    "caching": "ReadWrite",
    "createOption": "FromImage",
    "managedDisk": {
        "storageAccountType": "StandardSSD_LRS"
    }
}
```

<span data-ttu-id="147a2-198">For a complete template example of how to create a Standard SSD disk with a template, see [Create a VM from a Windows Image with Standard SSD Data Disks](https://github.com/azure/azure-quickstart-templates/tree/master/101-vm-with-standardssd-disk/).</span><span class="sxs-lookup"><span data-stu-id="147a2-198">For a complete template example of how to create a Standard SSD disk with a template, see [Create a VM from a Windows Image with Standard SSD Data Disks](https://github.com/azure/azure-quickstart-templates/tree/master/101-vm-with-standardssd-disk/).</span></span>

<span data-ttu-id="147a2-199">**Can I convert my existing disks to Standard SSD?**</span><span class="sxs-lookup"><span data-stu-id="147a2-199">**Can I convert my existing disks to Standard SSD?**</span></span>
<span data-ttu-id="147a2-200">Yes, you can.</span><span class="sxs-lookup"><span data-stu-id="147a2-200">Yes, you can.</span></span> <span data-ttu-id="147a2-201">Refer to [Convert Azure managed disks storage from standard to premium, and vice versa](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/convert-disk-storage) for the general guidelines for converting Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-201">Refer to [Convert Azure managed disks storage from standard to premium, and vice versa](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/convert-disk-storage) for the general guidelines for converting Managed Disks.</span></span> <span data-ttu-id="147a2-202">And, use the following value to update the disk type to Standard SSD.</span><span class="sxs-lookup"><span data-stu-id="147a2-202">And, use the following value to update the disk type to Standard SSD.</span></span>
<span data-ttu-id="147a2-203">-AccountType StandardSSD_LRS</span><span class="sxs-lookup"><span data-stu-id="147a2-203">-AccountType StandardSSD_LRS</span></span>

<span data-ttu-id="147a2-204">**What is the benefit of using Standard SSD disks instead of HDD?**</span><span class="sxs-lookup"><span data-stu-id="147a2-204">**What is the benefit of using Standard SSD disks instead of HDD?**</span></span>
<span data-ttu-id="147a2-205">Standard SSD disks deliver better latency, consistency, availability and reliability compared to HDD disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-205">Standard SSD disks deliver better latency, consistency, availability and reliability compared to HDD disks.</span></span> <span data-ttu-id="147a2-206">Application workloads run a lot more smoothly on Standard SSD because of that.</span><span class="sxs-lookup"><span data-stu-id="147a2-206">Application workloads run a lot more smoothly on Standard SSD because of that.</span></span> <span data-ttu-id="147a2-207">Note, Premium SSD disks are the recommended solution for most IO-intensive production workloads.</span><span class="sxs-lookup"><span data-stu-id="147a2-207">Note, Premium SSD disks are the recommended solution for most IO-intensive production workloads.</span></span> 

<span data-ttu-id="147a2-208">**Can I use Standard SSDs as Unmanaged Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-208">**Can I use Standard SSDs as Unmanaged Disks?**</span></span>
<span data-ttu-id="147a2-209">No, Standard SSDs disks are only available as Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-209">No, Standard SSDs disks are only available as Managed Disks.</span></span>

<span data-ttu-id="147a2-210">**Do Standard SSD Disks support "single instance VM SLA"?**</span><span class="sxs-lookup"><span data-stu-id="147a2-210">**Do Standard SSD Disks support "single instance VM SLA"?**</span></span>
<span data-ttu-id="147a2-211">No, Standard SSDs do not have single instance VM SLA.</span><span class="sxs-lookup"><span data-stu-id="147a2-211">No, Standard SSDs do not have single instance VM SLA.</span></span> <span data-ttu-id="147a2-212">Use Premium SSD disks for single instance VM SLA.</span><span class="sxs-lookup"><span data-stu-id="147a2-212">Use Premium SSD disks for single instance VM SLA.</span></span>

## <a name="migrate-to-managed-disks"></a><span data-ttu-id="147a2-213">Migrate to Managed Disks</span><span class="sxs-lookup"><span data-stu-id="147a2-213">Migrate to Managed Disks</span></span>

<span data-ttu-id="147a2-214">**What changes are required in a pre-existing Azure Backup service configuration prior/after migration to Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-214">**What changes are required in a pre-existing Azure Backup service configuration prior/after migration to Managed Disks?**</span></span>

<span data-ttu-id="147a2-215">No changes are required.</span><span class="sxs-lookup"><span data-stu-id="147a2-215">No changes are required.</span></span>

<span data-ttu-id="147a2-216">**Will my VM backups created via Azure Backup service before the migration continue to work?**</span><span class="sxs-lookup"><span data-stu-id="147a2-216">**Will my VM backups created via Azure Backup service before the migration continue to work?**</span></span>

<span data-ttu-id="147a2-217">Yes, backups work seamlessly.</span><span class="sxs-lookup"><span data-stu-id="147a2-217">Yes, backups work seamlessly.</span></span>

<span data-ttu-id="147a2-218">**What changes are required in a pre-existing Azure Disks Encryption configuration prior/after migration to Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-218">**What changes are required in a pre-existing Azure Disks Encryption configuration prior/after migration to Managed Disks?**</span></span>

<span data-ttu-id="147a2-219">No changes are required.</span><span class="sxs-lookup"><span data-stu-id="147a2-219">No changes are required.</span></span>

<span data-ttu-id="147a2-220">**Is automated migration of an existing virtual machine scale sets from unmanaged disks to Managed Disks supported?**</span><span class="sxs-lookup"><span data-stu-id="147a2-220">**Is automated migration of an existing virtual machine scale sets from unmanaged disks to Managed Disks supported?**</span></span>

<span data-ttu-id="147a2-221">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-221">No.</span></span> <span data-ttu-id="147a2-222">You can create a new scale set with Managed Disks using the image from your old scale set with unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-222">You can create a new scale set with Managed Disks using the image from your old scale set with unmanaged disks.</span></span>

<span data-ttu-id="147a2-223">**Can I create a Managed Disk from a page blob snapshot taken before migrating to Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-223">**Can I create a Managed Disk from a page blob snapshot taken before migrating to Managed Disks?**</span></span>

<span data-ttu-id="147a2-224">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-224">No.</span></span> <span data-ttu-id="147a2-225">You can export a page blob snapshot as a page blob and then create a Managed Disk from the exported page blob.</span><span class="sxs-lookup"><span data-stu-id="147a2-225">You can export a page blob snapshot as a page blob and then create a Managed Disk from the exported page blob.</span></span>

<span data-ttu-id="147a2-226">**Can I fail over my on-premises machines protected by Azure Site Recovery to a VM with Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-226">**Can I fail over my on-premises machines protected by Azure Site Recovery to a VM with Managed Disks?**</span></span>

<span data-ttu-id="147a2-227">Yes, you can choose to failover to a VM with Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-227">Yes, you can choose to failover to a VM with Managed Disks.</span></span>

<span data-ttu-id="147a2-228">**Is there any impact of migration on Azure VMs protected by Azure Site Recovery via Azure to Azure replication?**</span><span class="sxs-lookup"><span data-stu-id="147a2-228">**Is there any impact of migration on Azure VMs protected by Azure Site Recovery via Azure to Azure replication?**</span></span>

<span data-ttu-id="147a2-229">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-229">Yes.</span></span> <span data-ttu-id="147a2-230">Currently, Azure Site Recovery Azure to Azure protection for VMs with Managed Disks is only available as a public preview service.</span><span class="sxs-lookup"><span data-stu-id="147a2-230">Currently, Azure Site Recovery Azure to Azure protection for VMs with Managed Disks is only available as a public preview service.</span></span>

<span data-ttu-id="147a2-231">**Can I migrate VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-231">**Can I migrate VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="147a2-232">Yes</span><span class="sxs-lookup"><span data-stu-id="147a2-232">Yes</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="147a2-233">Managed Disks and Storage Service Encryption</span><span class="sxs-lookup"><span data-stu-id="147a2-233">Managed Disks and Storage Service Encryption</span></span>

<span data-ttu-id="147a2-234">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span><span class="sxs-lookup"><span data-stu-id="147a2-234">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="147a2-235">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-235">Yes.</span></span>

<span data-ttu-id="147a2-236">**Who manages the encryption keys?**</span><span class="sxs-lookup"><span data-stu-id="147a2-236">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="147a2-237">Microsoft manages the encryption keys.</span><span class="sxs-lookup"><span data-stu-id="147a2-237">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="147a2-238">**Can I disable Storage Service Encryption for my managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-238">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="147a2-239">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-239">No.</span></span>

<span data-ttu-id="147a2-240">**Is Storage Service Encryption only available in specific regions?**</span><span class="sxs-lookup"><span data-stu-id="147a2-240">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="147a2-241">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-241">No.</span></span> <span data-ttu-id="147a2-242">It's available in all the regions where Managed Disks are available.</span><span class="sxs-lookup"><span data-stu-id="147a2-242">It's available in all the regions where Managed Disks are available.</span></span> <span data-ttu-id="147a2-243">Managed Disks is available in all public regions and Germany.</span><span class="sxs-lookup"><span data-stu-id="147a2-243">Managed Disks is available in all public regions and Germany.</span></span> <span data-ttu-id="147a2-244">It is also available in China, however, only for Microsoft managed keys, not customer managed keys.</span><span class="sxs-lookup"><span data-stu-id="147a2-244">It is also available in China, however, only for Microsoft managed keys, not customer managed keys.</span></span>

<span data-ttu-id="147a2-245">**How can I find out if my managed disk is encrypted?**</span><span class="sxs-lookup"><span data-stu-id="147a2-245">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="147a2-246">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="147a2-246">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="147a2-247">If the time is after June 9, 2017, then your disk is encrypted.</span><span class="sxs-lookup"><span data-stu-id="147a2-247">If the time is after June 9, 2017, then your disk is encrypted.</span></span>

<span data-ttu-id="147a2-248">**How can I encrypt my existing disks that were created before June 10, 2017?**</span><span class="sxs-lookup"><span data-stu-id="147a2-248">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="147a2-249">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span><span class="sxs-lookup"><span data-stu-id="147a2-249">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="147a2-250">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span><span class="sxs-lookup"><span data-stu-id="147a2-250">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="147a2-251">If you must encrypt existing data now, create a copy of your disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-251">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="147a2-252">New disks will be encrypted.</span><span class="sxs-lookup"><span data-stu-id="147a2-252">New disks will be encrypted.</span></span>

* [<span data-ttu-id="147a2-253">Copy managed disks by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="147a2-253">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="147a2-254">Copy managed disks by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="147a2-254">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="147a2-255">**Are managed snapshots and images encrypted?**</span><span class="sxs-lookup"><span data-stu-id="147a2-255">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="147a2-256">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-256">Yes.</span></span> <span data-ttu-id="147a2-257">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span><span class="sxs-lookup"><span data-stu-id="147a2-257">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="147a2-258">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-258">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="147a2-259">Yes</span><span class="sxs-lookup"><span data-stu-id="147a2-259">Yes</span></span>

<span data-ttu-id="147a2-260">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span><span class="sxs-lookup"><span data-stu-id="147a2-260">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="147a2-261">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-261">No.</span></span> <span data-ttu-id="147a2-262">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span><span class="sxs-lookup"><span data-stu-id="147a2-262">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="147a2-263">Premium disks: Managed and unmanaged</span><span class="sxs-lookup"><span data-stu-id="147a2-263">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="147a2-264">**If a VM uses a size series that supports Premium SSD disks, such as a DSv2, can I attach both premium and standard data disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-264">**If a VM uses a size series that supports Premium SSD disks, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="147a2-265">Yes.</span><span class="sxs-lookup"><span data-stu-id="147a2-265">Yes.</span></span>

<span data-ttu-id="147a2-266">**Can I attach both premium and standard data disks to a size series that doesn't support Premium SSD disks, such as D, Dv2, G, or F series?**</span><span class="sxs-lookup"><span data-stu-id="147a2-266">**Can I attach both premium and standard data disks to a size series that doesn't support Premium SSD disks, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="147a2-267">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-267">No.</span></span> <span data-ttu-id="147a2-268">You can attach only standard data disks to VMs that don't use a size series that supports Premium SSD disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-268">You can attach only standard data disks to VMs that don't use a size series that supports Premium SSD disks.</span></span>

<span data-ttu-id="147a2-269">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span><span class="sxs-lookup"><span data-stu-id="147a2-269">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="147a2-270">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span><span class="sxs-lookup"><span data-stu-id="147a2-270">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="147a2-271">You're charged according to the P10 disk pricing.</span><span class="sxs-lookup"><span data-stu-id="147a2-271">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="147a2-272">**Are there transaction costs to use Premium SSD disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-272">**Are there transaction costs to use Premium SSD disks?**</span></span>

<span data-ttu-id="147a2-273">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span><span class="sxs-lookup"><span data-stu-id="147a2-273">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="147a2-274">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span><span class="sxs-lookup"><span data-stu-id="147a2-274">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="147a2-275">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="147a2-275">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="147a2-276">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span><span class="sxs-lookup"><span data-stu-id="147a2-276">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="147a2-277">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span><span class="sxs-lookup"><span data-stu-id="147a2-277">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="147a2-278">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span><span class="sxs-lookup"><span data-stu-id="147a2-278">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="147a2-279">**Is the local SSD supported for a Managed Disks VM?**</span><span class="sxs-lookup"><span data-stu-id="147a2-279">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="147a2-280">The local SSD is temporary storage that is included with a Managed Disks VM.</span><span class="sxs-lookup"><span data-stu-id="147a2-280">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="147a2-281">There is no extra cost for this temporary storage.</span><span class="sxs-lookup"><span data-stu-id="147a2-281">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="147a2-282">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="147a2-282">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="147a2-283">**Are there any repercussions for the use of TRIM on premium disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-283">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="147a2-284">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-284">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="147a2-285">New disk sizes: Managed and unmanaged</span><span class="sxs-lookup"><span data-stu-id="147a2-285">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="147a2-286">**What is the largest disk size supported for operating system and data disks?**</span><span class="sxs-lookup"><span data-stu-id="147a2-286">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="147a2-287">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span><span class="sxs-lookup"><span data-stu-id="147a2-287">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="147a2-288">The MBR format supports a disk size up to 2 TB.</span><span class="sxs-lookup"><span data-stu-id="147a2-288">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="147a2-289">The largest size that Azure supports for an operating system disk is 2 TB.</span><span class="sxs-lookup"><span data-stu-id="147a2-289">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="147a2-290">Azure supports up to 4 TB for data disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-290">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="147a2-291">**What is the largest page blob size that's supported?**</span><span class="sxs-lookup"><span data-stu-id="147a2-291">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="147a2-292">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span><span class="sxs-lookup"><span data-stu-id="147a2-292">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="147a2-293">The maximum page blog size when attached to a VM as data or operating system disks is 4 TB (4,095 GB).</span><span class="sxs-lookup"><span data-stu-id="147a2-293">The maximum page blog size when attached to a VM as data or operating system disks is 4 TB (4,095 GB).</span></span>

<span data-ttu-id="147a2-294">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="147a2-294">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="147a2-295">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span><span class="sxs-lookup"><span data-stu-id="147a2-295">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="147a2-296">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span><span class="sxs-lookup"><span data-stu-id="147a2-296">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="147a2-297">Azure tools</span><span class="sxs-lookup"><span data-stu-id="147a2-297">Azure tools</span></span>      | <span data-ttu-id="147a2-298">Supported versions</span><span class="sxs-lookup"><span data-stu-id="147a2-298">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="147a2-299">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="147a2-299">Azure PowerShell</span></span> | <span data-ttu-id="147a2-300">Version number 4.1.0: June 2017 release or later</span><span class="sxs-lookup"><span data-stu-id="147a2-300">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="147a2-301">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="147a2-301">Azure CLI v1</span></span>     | <span data-ttu-id="147a2-302">Version number 0.10.13: May 2017 release or later</span><span class="sxs-lookup"><span data-stu-id="147a2-302">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="147a2-303">AzCopy</span><span class="sxs-lookup"><span data-stu-id="147a2-303">AzCopy</span></span>           | <span data-ttu-id="147a2-304">Version number 6.1.0: June 2017 release or later</span><span class="sxs-lookup"><span data-stu-id="147a2-304">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="147a2-305">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span><span class="sxs-lookup"><span data-stu-id="147a2-305">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="147a2-306">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span><span class="sxs-lookup"><span data-stu-id="147a2-306">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="147a2-307">No.</span><span class="sxs-lookup"><span data-stu-id="147a2-307">No.</span></span> <span data-ttu-id="147a2-308">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span><span class="sxs-lookup"><span data-stu-id="147a2-308">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="147a2-309">Support for unmanaged disks and page blobs is coming soon.</span><span class="sxs-lookup"><span data-stu-id="147a2-309">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="147a2-310">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span><span class="sxs-lookup"><span data-stu-id="147a2-310">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="147a2-311">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span><span class="sxs-lookup"><span data-stu-id="147a2-311">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="147a2-312">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span><span class="sxs-lookup"><span data-stu-id="147a2-312">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="147a2-313">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span><span class="sxs-lookup"><span data-stu-id="147a2-313">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="147a2-314">What if my question isn't answered here?</span><span class="sxs-lookup"><span data-stu-id="147a2-314">What if my question isn't answered here?</span></span>

<span data-ttu-id="147a2-315">If your question isn't listed here, let us know and we'll help you find an answer.</span><span class="sxs-lookup"><span data-stu-id="147a2-315">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="147a2-316">You can post a question at the end of this article in the comments.</span><span class="sxs-lookup"><span data-stu-id="147a2-316">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="147a2-317">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="147a2-317">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="147a2-318">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="147a2-318">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
