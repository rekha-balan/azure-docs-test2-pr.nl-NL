---
title: Manage storage capacity in Azure Stack | Microsoft Docs
description: Monitor and manage available storage space for Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: b0e694e4-3575-424c-afda-7d48c2025a62
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: get-started-article
ms.date: 05/10/2018
ms.author: mabrigg
ms.reviewer: xiaofmao
ms.openlocfilehash: cdfdaf9195f14e3cbe3db2a4507bd91a3133a26e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864439"
---
# <a name="manage-storage-capacity-for-azure-stack"></a><span data-ttu-id="04a0c-103">Manage storage capacity for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="04a0c-103">Manage storage capacity for Azure Stack</span></span>

<span data-ttu-id="04a0c-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="04a0c-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="04a0c-105">The information in this article helps the Azure Stack cloud operator monitor and manage the storage capacity of their Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="04a0c-105">The information in this article helps the Azure Stack cloud operator monitor and manage the storage capacity of their Azure Stack deployment.</span></span> <span data-ttu-id="04a0c-106">The Azure Stack storage infrastructure allocates a subset of the total storage capacity of the Azure Stack deployment, to be used for **storage services**.</span><span class="sxs-lookup"><span data-stu-id="04a0c-106">The Azure Stack storage infrastructure allocates a subset of the total storage capacity of the Azure Stack deployment, to be used for **storage services**.</span></span> <span data-ttu-id="04a0c-107">The storage services store a tenant’s data in shares on volumes that correspond to the nodes of the deployment.</span><span class="sxs-lookup"><span data-stu-id="04a0c-107">The storage services store a tenant’s data in shares on volumes that correspond to the nodes of the deployment.</span></span>

<span data-ttu-id="04a0c-108">As a cloud operator, you have a limited amount of storage to work with.</span><span class="sxs-lookup"><span data-stu-id="04a0c-108">As a cloud operator, you have a limited amount of storage to work with.</span></span> <span data-ttu-id="04a0c-109">The amount of storage is defined by the solution you implement.</span><span class="sxs-lookup"><span data-stu-id="04a0c-109">The amount of storage is defined by the solution you implement.</span></span> <span data-ttu-id="04a0c-110">Your solution is provided by your OEM vendor when you use a multi-node solution, or by the hardware on which you install the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="04a0c-110">Your solution is provided by your OEM vendor when you use a multi-node solution, or by the hardware on which you install the Azure Stack Development Kit.</span></span>

<span data-ttu-id="04a0c-111">Because Azure Stack does not support expansion of the storage capacity, it is important to [monitor](#monitor-shares) the available storage to ensure efficient operations are maintained.</span><span class="sxs-lookup"><span data-stu-id="04a0c-111">Because Azure Stack does not support expansion of the storage capacity, it is important to [monitor](#monitor-shares) the available storage to ensure efficient operations are maintained.</span></span>  

<span data-ttu-id="04a0c-112">When the remaining free capacity of a share becomes limited, plan to [manage space](#manage-available-space) to prevent the shares from running out of capacity.</span><span class="sxs-lookup"><span data-stu-id="04a0c-112">When the remaining free capacity of a share becomes limited, plan to [manage space](#manage-available-space) to prevent the shares from running out of capacity.</span></span>

<span data-ttu-id="04a0c-113">Options to manage capacity include:</span><span class="sxs-lookup"><span data-stu-id="04a0c-113">Options to manage capacity include:</span></span>
- <span data-ttu-id="04a0c-114">Reclaim capacity</span><span class="sxs-lookup"><span data-stu-id="04a0c-114">Reclaim capacity</span></span>
- <span data-ttu-id="04a0c-115">Migrate a container</span><span class="sxs-lookup"><span data-stu-id="04a0c-115">Migrate a container</span></span>

<span data-ttu-id="04a0c-116">When a share is 100% utilized, the storage service no longer functions for that share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-116">When a share is 100% utilized, the storage service no longer functions for that share.</span></span> <span data-ttu-id="04a0c-117">To get assistance in restoring operations for the share, contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="04a0c-117">To get assistance in restoring operations for the share, contact Microsoft support.</span></span>

## <a name="understand-volumes-and-shares-containers-and-disks"></a><span data-ttu-id="04a0c-118">Understand volumes and shares, containers, and disks</span><span class="sxs-lookup"><span data-stu-id="04a0c-118">Understand volumes and shares, containers, and disks</span></span>
### <a name="volumes-and-shares"></a><span data-ttu-id="04a0c-119">Volumes and shares</span><span class="sxs-lookup"><span data-stu-id="04a0c-119">Volumes and shares</span></span>
<span data-ttu-id="04a0c-120">The *storage service* partitions the available storage into separate and equal volumes that are allocated to hold tenant data.</span><span class="sxs-lookup"><span data-stu-id="04a0c-120">The *storage service* partitions the available storage into separate and equal volumes that are allocated to hold tenant data.</span></span> <span data-ttu-id="04a0c-121">The number of volumes is equal to the number of the nodes in the Azure Stack deployment:</span><span class="sxs-lookup"><span data-stu-id="04a0c-121">The number of volumes is equal to the number of the nodes in the Azure Stack deployment:</span></span>

- <span data-ttu-id="04a0c-122">On a four-node deployment, there are four volumes.</span><span class="sxs-lookup"><span data-stu-id="04a0c-122">On a four-node deployment, there are four volumes.</span></span> <span data-ttu-id="04a0c-123">Each volume has a single share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-123">Each volume has a single share.</span></span> <span data-ttu-id="04a0c-124">On a multi-node deployment, the number of shares is not reduced if a node is removed or malfunctioning.</span><span class="sxs-lookup"><span data-stu-id="04a0c-124">On a multi-node deployment, the number of shares is not reduced if a node is removed or malfunctioning.</span></span>
- <span data-ttu-id="04a0c-125">If you use the Azure Stack Developer Kit, there is a single volume with a single share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-125">If you use the Azure Stack Developer Kit, there is a single volume with a single share.</span></span>

<span data-ttu-id="04a0c-126">Because the storage service shares are for the exclusive use of storage services, you must not directly modify, add, or remove any files on the shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-126">Because the storage service shares are for the exclusive use of storage services, you must not directly modify, add, or remove any files on the shares.</span></span> <span data-ttu-id="04a0c-127">Only storage services should work on the files stored in these volumes.</span><span class="sxs-lookup"><span data-stu-id="04a0c-127">Only storage services should work on the files stored in these volumes.</span></span>

<span data-ttu-id="04a0c-128">Shares on volumes hold tenant data.</span><span class="sxs-lookup"><span data-stu-id="04a0c-128">Shares on volumes hold tenant data.</span></span> <span data-ttu-id="04a0c-129">Tenant data includes page blobs, block blobs, append blobs, tables, queues, databases, and related metadata stores.</span><span class="sxs-lookup"><span data-stu-id="04a0c-129">Tenant data includes page blobs, block blobs, append blobs, tables, queues, databases, and related metadata stores.</span></span> <span data-ttu-id="04a0c-130">Because the storage objects (blobs, etc.) are individually contained within a single share, the maximum size of each object cannot exceed the size of a share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-130">Because the storage objects (blobs, etc.) are individually contained within a single share, the maximum size of each object cannot exceed the size of a share.</span></span> <span data-ttu-id="04a0c-131">The maximum size of new objects depends on the capacity that remains in a share as unused space when that new object is created.</span><span class="sxs-lookup"><span data-stu-id="04a0c-131">The maximum size of new objects depends on the capacity that remains in a share as unused space when that new object is created.</span></span>

<span data-ttu-id="04a0c-132">When a share is low on free space and actions to [reclaim](#reclaim-capacity) space are not successful or available, the Azure Stack cloud operator can [migrate](#migrate-a-container-between) the blob containers from one share to another.</span><span class="sxs-lookup"><span data-stu-id="04a0c-132">When a share is low on free space and actions to [reclaim](#reclaim-capacity) space are not successful or available, the Azure Stack cloud operator can [migrate](#migrate-a-container-between) the blob containers from one share to another.</span></span>

- <span data-ttu-id="04a0c-133">For more information about containers and blobs, see [Blob storage](azure-stack-key-features.md#blob-storage) in Key features and concepts in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="04a0c-133">For more information about containers and blobs, see [Blob storage](azure-stack-key-features.md#blob-storage) in Key features and concepts in Azure Stack.</span></span>
- <span data-ttu-id="04a0c-134">For information about how tenant users work with blob storage in Azure Stack, see [Azure Stack Storage services](/azure/azure-stack/user/azure-stack-storage-overview#azure-stack-storage-services).</span><span class="sxs-lookup"><span data-stu-id="04a0c-134">For information about how tenant users work with blob storage in Azure Stack, see [Azure Stack Storage services](/azure/azure-stack/user/azure-stack-storage-overview#azure-stack-storage-services).</span></span>


### <a name="containers"></a><span data-ttu-id="04a0c-135">Containers</span><span class="sxs-lookup"><span data-stu-id="04a0c-135">Containers</span></span>
<span data-ttu-id="04a0c-136">Tenant users create containers that are then used to store blob data.</span><span class="sxs-lookup"><span data-stu-id="04a0c-136">Tenant users create containers that are then used to store blob data.</span></span> <span data-ttu-id="04a0c-137">While the user decides in which container to place blobs, the storage service uses an algorithm to determine on which volume to put the container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-137">While the user decides in which container to place blobs, the storage service uses an algorithm to determine on which volume to put the container.</span></span> <span data-ttu-id="04a0c-138">The algorithm typically chooses the volume with the most available space.</span><span class="sxs-lookup"><span data-stu-id="04a0c-138">The algorithm typically chooses the volume with the most available space.</span></span>  

<span data-ttu-id="04a0c-139">After a blob is placed in a container, that blob can grow to use more space.</span><span class="sxs-lookup"><span data-stu-id="04a0c-139">After a blob is placed in a container, that blob can grow to use more space.</span></span> <span data-ttu-id="04a0c-140">As you add new blobs and existing blobs grow, the available space in the volume that holds that container shrinks.</span><span class="sxs-lookup"><span data-stu-id="04a0c-140">As you add new blobs and existing blobs grow, the available space in the volume that holds that container shrinks.</span></span>  

<span data-ttu-id="04a0c-141">Containers are not limited to a single share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-141">Containers are not limited to a single share.</span></span> <span data-ttu-id="04a0c-142">When the combined blob data in a container grows  use 80% or more of the available space, the container enters *overflow* mode.</span><span class="sxs-lookup"><span data-stu-id="04a0c-142">When the combined blob data in a container grows  use 80% or more of the available space, the container enters *overflow* mode.</span></span> <span data-ttu-id="04a0c-143">When in overflow mode, any new blobs that are created in that container are allocated to a different volume that has sufficient space.</span><span class="sxs-lookup"><span data-stu-id="04a0c-143">When in overflow mode, any new blobs that are created in that container are allocated to a different volume that has sufficient space.</span></span> <span data-ttu-id="04a0c-144">Over time, a container in overflow mode can have blobs that are distributed across multiple volumes.</span><span class="sxs-lookup"><span data-stu-id="04a0c-144">Over time, a container in overflow mode can have blobs that are distributed across multiple volumes.</span></span>

<span data-ttu-id="04a0c-145">When 80%, and then 90% of the available space in a volume is used, the system raises alerts in the Azure Stack administrator portal.</span><span class="sxs-lookup"><span data-stu-id="04a0c-145">When 80%, and then 90% of the available space in a volume is used, the system raises alerts in the Azure Stack administrator portal.</span></span> <span data-ttu-id="04a0c-146">Cloud operators should review available storage capacity, and plan to rebalance the content.</span><span class="sxs-lookup"><span data-stu-id="04a0c-146">Cloud operators should review available storage capacity, and plan to rebalance the content.</span></span> <span data-ttu-id="04a0c-147">The storage service stops working when a disk is 100% used, and no additional alerts are raised.</span><span class="sxs-lookup"><span data-stu-id="04a0c-147">The storage service stops working when a disk is 100% used, and no additional alerts are raised.</span></span>

### <a name="disks"></a><span data-ttu-id="04a0c-148">Disks</span><span class="sxs-lookup"><span data-stu-id="04a0c-148">Disks</span></span>
<span data-ttu-id="04a0c-149">VM disks are added to containers by tenants and include an operating system disk.</span><span class="sxs-lookup"><span data-stu-id="04a0c-149">VM disks are added to containers by tenants and include an operating system disk.</span></span> <span data-ttu-id="04a0c-150">VMs can also have one or more data disks.</span><span class="sxs-lookup"><span data-stu-id="04a0c-150">VMs can also have one or more data disks.</span></span> <span data-ttu-id="04a0c-151">Both types of disks are stored as page blobs.</span><span class="sxs-lookup"><span data-stu-id="04a0c-151">Both types of disks are stored as page blobs.</span></span> <span data-ttu-id="04a0c-152">The guidance to tenants is to place each disk into a separate container to improve performance of the VM.</span><span class="sxs-lookup"><span data-stu-id="04a0c-152">The guidance to tenants is to place each disk into a separate container to improve performance of the VM.</span></span>
- <span data-ttu-id="04a0c-153">Each container that holds a disk (page blob) from a VM is considered an attached container to the VM that owns the disk.</span><span class="sxs-lookup"><span data-stu-id="04a0c-153">Each container that holds a disk (page blob) from a VM is considered an attached container to the VM that owns the disk.</span></span>
- <span data-ttu-id="04a0c-154">A container that does not hold any disk from a VM is considered a free container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-154">A container that does not hold any disk from a VM is considered a free container.</span></span>

<span data-ttu-id="04a0c-155">The options to free up space on an attached container [are limited](#move-vm-disks).</span><span class="sxs-lookup"><span data-stu-id="04a0c-155">The options to free up space on an attached container [are limited](#move-vm-disks).</span></span>
> [!TIP]  
> <span data-ttu-id="04a0c-156">Cloud operators do not directly manage disks, which are attached to virtual machines (VMs) that tenants might add to a container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-156">Cloud operators do not directly manage disks, which are attached to virtual machines (VMs) that tenants might add to a container.</span></span> <span data-ttu-id="04a0c-157">However, when planning to manage space on storage shares, it can be of use to understand how disks relate to containers and shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-157">However, when planning to manage space on storage shares, it can be of use to understand how disks relate to containers and shares.</span></span>

## <a name="monitor-shares"></a><span data-ttu-id="04a0c-158">Monitor shares</span><span class="sxs-lookup"><span data-stu-id="04a0c-158">Monitor shares</span></span>
<span data-ttu-id="04a0c-159">Use PowerShell or the admin portal to monitor shares so you can understand when free space is limited.</span><span class="sxs-lookup"><span data-stu-id="04a0c-159">Use PowerShell or the admin portal to monitor shares so you can understand when free space is limited.</span></span> <span data-ttu-id="04a0c-160">When you use the portal, you receive alerts about shares that are low on space.</span><span class="sxs-lookup"><span data-stu-id="04a0c-160">When you use the portal, you receive alerts about shares that are low on space.</span></span>    

### <a name="use-powershell"></a><span data-ttu-id="04a0c-161">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="04a0c-161">Use PowerShell</span></span>
<span data-ttu-id="04a0c-162">As a cloud operator, you can monitor the storage capacity of a share using the PowerShell **Get-AzsStorageShare** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="04a0c-162">As a cloud operator, you can monitor the storage capacity of a share using the PowerShell **Get-AzsStorageShare** cmdlet.</span></span> <span data-ttu-id="04a0c-163">The Get-AzsStorageShare cmdlet returns the total, allocated, and free space in bytes on each of the shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-163">The Get-AzsStorageShare cmdlet returns the total, allocated, and free space in bytes on each of the shares.</span></span>   
<span data-ttu-id="04a0c-164">![Example: Return free space for shares](media/azure-stack-manage-storage-shares/free-space.png)</span><span class="sxs-lookup"><span data-stu-id="04a0c-164">![Example: Return free space for shares](media/azure-stack-manage-storage-shares/free-space.png)</span></span>

- <span data-ttu-id="04a0c-165">**Total capacity** is the total space in bytes that are available on the share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-165">**Total capacity** is the total space in bytes that are available on the share.</span></span> <span data-ttu-id="04a0c-166">This space is used for data and metadata that is maintained by the storage services.</span><span class="sxs-lookup"><span data-stu-id="04a0c-166">This space is used for data and metadata that is maintained by the storage services.</span></span>
- <span data-ttu-id="04a0c-167">**Used capacity** is the amount of data in bytes that is used by the all the extents from the files that store the tenant data and associated metadata.</span><span class="sxs-lookup"><span data-stu-id="04a0c-167">**Used capacity** is the amount of data in bytes that is used by the all the extents from the files that store the tenant data and associated metadata.</span></span>

### <a name="use-the-administrator-portal"></a><span data-ttu-id="04a0c-168">Use the administrator portal</span><span class="sxs-lookup"><span data-stu-id="04a0c-168">Use the administrator portal</span></span>
<span data-ttu-id="04a0c-169">As a cloud operator, you can use the admin portal to view the storage capacity of all shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-169">As a cloud operator, you can use the admin portal to view the storage capacity of all shares.</span></span> <span data-ttu-id="04a0c-170">**Go to Storage** > **File Shares** to open the file share list where you can view the usage information.</span><span class="sxs-lookup"><span data-stu-id="04a0c-170">**Go to Storage** > **File Shares** to open the file share list where you can view the usage information.</span></span>
<span data-ttu-id="04a0c-171">![Example: Storage file shares](media/azure-stack-manage-storage-shares/storage-file-shares.png)</span><span class="sxs-lookup"><span data-stu-id="04a0c-171">![Example: Storage file shares](media/azure-stack-manage-storage-shares/storage-file-shares.png)</span></span>
- <span data-ttu-id="04a0c-172">**TOTAL** is the total space in bytes that are available on the share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-172">**TOTAL** is the total space in bytes that are available on the share.</span></span> <span data-ttu-id="04a0c-173">This space is used for data and metadata that is maintained by the storage services.</span><span class="sxs-lookup"><span data-stu-id="04a0c-173">This space is used for data and metadata that is maintained by the storage services.</span></span>
- <span data-ttu-id="04a0c-174">**USED** is the amount of data in bytes that is used by the all the extents from the files that store the tenant data and associated metadata.</span><span class="sxs-lookup"><span data-stu-id="04a0c-174">**USED** is the amount of data in bytes that is used by the all the extents from the files that store the tenant data and associated metadata.</span></span>

### <a name="storage-space-alerts"></a><span data-ttu-id="04a0c-175">Storage space alerts</span><span class="sxs-lookup"><span data-stu-id="04a0c-175">Storage space alerts</span></span>
<span data-ttu-id="04a0c-176">When you use the admin portal, you receive alerts about shares that are low on space.</span><span class="sxs-lookup"><span data-stu-id="04a0c-176">When you use the admin portal, you receive alerts about shares that are low on space.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04a0c-177">As a cloud operator, keep shares from reaching full usage.</span><span class="sxs-lookup"><span data-stu-id="04a0c-177">As a cloud operator, keep shares from reaching full usage.</span></span> <span data-ttu-id="04a0c-178">When a share is 100% utilized, the storage service no longer functions for that share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-178">When a share is 100% utilized, the storage service no longer functions for that share.</span></span> <span data-ttu-id="04a0c-179">To recover free space and restore operations on a share that is 100% utilized, you must contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="04a0c-179">To recover free space and restore operations on a share that is 100% utilized, you must contact Microsoft support.</span></span>

<span data-ttu-id="04a0c-180">**Warning**: When a file share is over 80% utilized, you receive a *Warning* alert in the admin portal: ![Example: Warning alert](media/azure-stack-manage-storage-shares/alert-warning.png)</span><span class="sxs-lookup"><span data-stu-id="04a0c-180">**Warning**: When a file share is over 80% utilized, you receive a *Warning* alert in the admin portal: ![Example: Warning alert](media/azure-stack-manage-storage-shares/alert-warning.png)</span></span>


<span data-ttu-id="04a0c-181">**Critical**: When a file share is over 90% utilized, you receive a *Critical* alert in the admin portal: ![Example: Critical alert](media/azure-stack-manage-storage-shares/alert-critical.png)</span><span class="sxs-lookup"><span data-stu-id="04a0c-181">**Critical**: When a file share is over 90% utilized, you receive a *Critical* alert in the admin portal: ![Example: Critical alert](media/azure-stack-manage-storage-shares/alert-critical.png)</span></span>

<span data-ttu-id="04a0c-182">**View details**: In the admin portal you can open the details for an alert to view mitigation options: ![Example: View alert details](media/azure-stack-manage-storage-shares/alert-details.png)</span><span class="sxs-lookup"><span data-stu-id="04a0c-182">**View details**: In the admin portal you can open the details for an alert to view mitigation options: ![Example: View alert details](media/azure-stack-manage-storage-shares/alert-details.png)</span></span>


## <a name="manage-available-space"></a><span data-ttu-id="04a0c-183">Manage available space</span><span class="sxs-lookup"><span data-stu-id="04a0c-183">Manage available space</span></span>
<span data-ttu-id="04a0c-184">When it's necessary to free space on a share, use the least invasive methods first.</span><span class="sxs-lookup"><span data-stu-id="04a0c-184">When it's necessary to free space on a share, use the least invasive methods first.</span></span> <span data-ttu-id="04a0c-185">For example, try to reclaim space before you choose to migrate a container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-185">For example, try to reclaim space before you choose to migrate a container.</span></span>  

### <a name="reclaim-capacity"></a><span data-ttu-id="04a0c-186">Reclaim capacity</span><span class="sxs-lookup"><span data-stu-id="04a0c-186">Reclaim capacity</span></span>
<span data-ttu-id="04a0c-187">*This option applies to both multi-node deployments and the Azure Stack Development Kit.*</span><span class="sxs-lookup"><span data-stu-id="04a0c-187">*This option applies to both multi-node deployments and the Azure Stack Development Kit.*</span></span>

<span data-ttu-id="04a0c-188">You can reclaim the capacity used by tenant accounts that have been deleted.</span><span class="sxs-lookup"><span data-stu-id="04a0c-188">You can reclaim the capacity used by tenant accounts that have been deleted.</span></span> <span data-ttu-id="04a0c-189">This capacity is automatically reclaimed when the data [retention period](azure-stack-manage-storage-accounts.md#set-the-retention-period) is reached, or you can act to reclaim it immediately.</span><span class="sxs-lookup"><span data-stu-id="04a0c-189">This capacity is automatically reclaimed when the data [retention period](azure-stack-manage-storage-accounts.md#set-the-retention-period) is reached, or you can act to reclaim it immediately.</span></span>

<span data-ttu-id="04a0c-190">For more information, see [Reclaim capacity](azure-stack-manage-storage-accounts.md#reclaim) in Manage storage resources.</span><span class="sxs-lookup"><span data-stu-id="04a0c-190">For more information, see [Reclaim capacity](azure-stack-manage-storage-accounts.md#reclaim) in Manage storage resources.</span></span>

### <a name="migrate-a-container-between-volumes"></a><span data-ttu-id="04a0c-191">Migrate a container between volumes</span><span class="sxs-lookup"><span data-stu-id="04a0c-191">Migrate a container between volumes</span></span>
<span data-ttu-id="04a0c-192">*This option applies only to multi-node deployments.*</span><span class="sxs-lookup"><span data-stu-id="04a0c-192">*This option applies only to multi-node deployments.*</span></span>

<span data-ttu-id="04a0c-193">Due to tenant usage patterns, some tenant shares use more space than others.</span><span class="sxs-lookup"><span data-stu-id="04a0c-193">Due to tenant usage patterns, some tenant shares use more space than others.</span></span> <span data-ttu-id="04a0c-194">The result can be a share that runs low on space before other shares that are relatively unused.</span><span class="sxs-lookup"><span data-stu-id="04a0c-194">The result can be a share that runs low on space before other shares that are relatively unused.</span></span>

<span data-ttu-id="04a0c-195">You can try to free up space on an overused share by manually migrating some blob containers to a different share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-195">You can try to free up space on an overused share by manually migrating some blob containers to a different share.</span></span> <span data-ttu-id="04a0c-196">You can migrate several smaller containers to a single share that has capacity to hold them all.</span><span class="sxs-lookup"><span data-stu-id="04a0c-196">You can migrate several smaller containers to a single share that has capacity to hold them all.</span></span> <span data-ttu-id="04a0c-197">You can use migration to move *free* containers.</span><span class="sxs-lookup"><span data-stu-id="04a0c-197">You can use migration to move *free* containers.</span></span> <span data-ttu-id="04a0c-198">Free containers are containers that do not contain a disk for a VM.</span><span class="sxs-lookup"><span data-stu-id="04a0c-198">Free containers are containers that do not contain a disk for a VM.</span></span>   

<span data-ttu-id="04a0c-199">Migration consolidates all a containers blob on the new share.</span><span class="sxs-lookup"><span data-stu-id="04a0c-199">Migration consolidates all a containers blob on the new share.</span></span>

- <span data-ttu-id="04a0c-200">If a container has entered overflow mode and has placed blobs on additional volumes, the new share must have sufficient capacity to hold all of the blobs for the container you migrate.</span><span class="sxs-lookup"><span data-stu-id="04a0c-200">If a container has entered overflow mode and has placed blobs on additional volumes, the new share must have sufficient capacity to hold all of the blobs for the container you migrate.</span></span> <span data-ttu-id="04a0c-201">This includes the blobs that are located on additional shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-201">This includes the blobs that are located on additional shares.</span></span>

- <span data-ttu-id="04a0c-202">The PowerShell cmdlet *Get-AzsStorageContainer* identifies only the space in use on the initial volume for a container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-202">The PowerShell cmdlet *Get-AzsStorageContainer* identifies only the space in use on the initial volume for a container.</span></span> <span data-ttu-id="04a0c-203">The cmdlet does not identify space that is used by blobs put on additional volumes.</span><span class="sxs-lookup"><span data-stu-id="04a0c-203">The cmdlet does not identify space that is used by blobs put on additional volumes.</span></span> <span data-ttu-id="04a0c-204">Therefore, the full size of a container might not be evident.</span><span class="sxs-lookup"><span data-stu-id="04a0c-204">Therefore, the full size of a container might not be evident.</span></span> <span data-ttu-id="04a0c-205">It is possible that consolidation of a container on a new share can send that new share into an overflow condition where it places data onto additional shares.</span><span class="sxs-lookup"><span data-stu-id="04a0c-205">It is possible that consolidation of a container on a new share can send that new share into an overflow condition where it places data onto additional shares.</span></span> <span data-ttu-id="04a0c-206">As a result, you might need to rebalance shares again.</span><span class="sxs-lookup"><span data-stu-id="04a0c-206">As a result, you might need to rebalance shares again.</span></span>

- <span data-ttu-id="04a0c-207">If you lack permissions to a resource group and cannot use PowerShell to query the additional volumes for overflow data, work with the owner of those resource groups and containers to understand the total size of data to migrate before migrating that data.</span><span class="sxs-lookup"><span data-stu-id="04a0c-207">If you lack permissions to a resource group and cannot use PowerShell to query the additional volumes for overflow data, work with the owner of those resource groups and containers to understand the total size of data to migrate before migrating that data.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="04a0c-208">Migration of blobs for a container is an offline operation that requires the use of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04a0c-208">Migration of blobs for a container is an offline operation that requires the use of PowerShell.</span></span> <span data-ttu-id="04a0c-209">Until migration completes, all blobs for the container you are migrating remain offline and cannot be used.</span><span class="sxs-lookup"><span data-stu-id="04a0c-209">Until migration completes, all blobs for the container you are migrating remain offline and cannot be used.</span></span> <span data-ttu-id="04a0c-210">You should also avoid upgrading Azure Stack until all ongoing migration completes.</span><span class="sxs-lookup"><span data-stu-id="04a0c-210">You should also avoid upgrading Azure Stack until all ongoing migration completes.</span></span>

#### <a name="to-migrate-containers-using-powershell"></a><span data-ttu-id="04a0c-211">To migrate containers using PowerShell</span><span class="sxs-lookup"><span data-stu-id="04a0c-211">To migrate containers using PowerShell</span></span>
1. <span data-ttu-id="04a0c-212">Confirm that you have [Azure PowerShell installed and configured](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="04a0c-212">Confirm that you have [Azure PowerShell installed and configured](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="04a0c-213">For more information, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="04a0c-213">For more information, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span></span>
2.  <span data-ttu-id="04a0c-214">Examine the container to understand what data is on the share that you plan to migrate.</span><span class="sxs-lookup"><span data-stu-id="04a0c-214">Examine the container to understand what data is on the share that you plan to migrate.</span></span> <span data-ttu-id="04a0c-215">To identify the best candidate containers for migration in a volume, use the **Get-AzsStorageContainer** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="04a0c-215">To identify the best candidate containers for migration in a volume, use the **Get-AzsStorageContainer** cmdlet:</span></span>

    ````PowerShell  
    $farm_name = (Get-AzsStorageFarm)[0].name
    $shares = Get-AzsStorageShare -FarmName $farm_name
    $containers = Get-AzsStorageContainer -ShareName $shares[0].ShareName -FarmName $farm_name
    ````
    <span data-ttu-id="04a0c-216">Then examine $containers:</span><span class="sxs-lookup"><span data-stu-id="04a0c-216">Then examine $containers:</span></span>

    ````PowerShell
    $containers
    ````

    ![Example: $Containers](media/azure-stack-manage-storage-shares/containers.png)

3.  <span data-ttu-id="04a0c-218">Identify the best destination shares to hold the container you migrate:</span><span class="sxs-lookup"><span data-stu-id="04a0c-218">Identify the best destination shares to hold the container you migrate:</span></span>

    ````PowerShell
    $destinationshares = Get-AzsStorageShare -SourceShareName
    $shares[0].ShareName -Intent ContainerMigration
    ````

    <span data-ttu-id="04a0c-219">Then examine $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="04a0c-219">Then examine $destinationshares:</span></span>

    ````PowerShell 
    $destinationshares
    ````

    ![Example: $destination shares](media/azure-stack-manage-storage-shares/examine-destinationshares.png)

4. <span data-ttu-id="04a0c-221">Start migration for a container.</span><span class="sxs-lookup"><span data-stu-id="04a0c-221">Start migration for a container.</span></span> <span data-ttu-id="04a0c-222">Migration is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="04a0c-222">Migration is asynchronous.</span></span> <span data-ttu-id="04a0c-223">If you start migration of additional containers before the first migration completes, use the job id to track the status of each.</span><span class="sxs-lookup"><span data-stu-id="04a0c-223">If you start migration of additional containers before the first migration completes, use the job id to track the status of each.</span></span>

  ````PowerShell
  $job_id = Start-AzsStorageContainerMigration -StorageAccountName $containers[0].Accountname -ContainerName $containers[0].Containername -ShareName $containers[0].Sharename -DestinationShareUncPath $destinationshares[0].UncPath -FarmName $farm_name
  ````

  <span data-ttu-id="04a0c-224">Then examine $jobId.</span><span class="sxs-lookup"><span data-stu-id="04a0c-224">Then examine $jobId.</span></span> <span data-ttu-id="04a0c-225">In the following example, replace *d62f8f7a-8b46-4f59-a8aa-5db96db4ebb0* with the job id you want to examine:</span><span class="sxs-lookup"><span data-stu-id="04a0c-225">In the following example, replace *d62f8f7a-8b46-4f59-a8aa-5db96db4ebb0* with the job id you want to examine:</span></span>

  ````PowerShell
  $jobId
  d62f8f7a-8b46-4f59-a8aa-5db96db4ebb0
  ````

5. <span data-ttu-id="04a0c-226">Use the job id to check on the status of the migration job.</span><span class="sxs-lookup"><span data-stu-id="04a0c-226">Use the job id to check on the status of the migration job.</span></span> <span data-ttu-id="04a0c-227">When the container migration is complete, **MigrationStatus** is set to **Complete**.</span><span class="sxs-lookup"><span data-stu-id="04a0c-227">When the container migration is complete, **MigrationStatus** is set to **Complete**.</span></span>

  ````PowerShell 
  Get-AzsStorageContainerMigrationStatus -JobId $job_id -FarmName $farm_name
  ````

  ![Example: Migration status](media/azure-stack-manage-storage-shares/migration-status1.png)

6.  <span data-ttu-id="04a0c-229">You can cancel an in-progress migration job.</span><span class="sxs-lookup"><span data-stu-id="04a0c-229">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="04a0c-230">Canceled migration jobs are processed asynchronously.</span><span class="sxs-lookup"><span data-stu-id="04a0c-230">Canceled migration jobs are processed asynchronously.</span></span> <span data-ttu-id="04a0c-231">You can track cancellation by using $jobid:</span><span class="sxs-lookup"><span data-stu-id="04a0c-231">You can track cancellation by using $jobid:</span></span>

  ````PowerShell
  Stop-AzsStorageContainerMigration -JobId $job_id -FarmName $farm_name
  ````

  ![Example: Rollback status](media/azure-stack-manage-storage-shares/rollback.png)

7. <span data-ttu-id="04a0c-233">You can run the command from step 6 again, until the status confirms the migration job is **Canceled**:</span><span class="sxs-lookup"><span data-stu-id="04a0c-233">You can run the command from step 6 again, until the status confirms the migration job is **Canceled**:</span></span>  

    ![Example: Canceled status](media/azure-stack-manage-storage-shares/cancelled.png)

### <a name="move-vm-disks"></a><span data-ttu-id="04a0c-235">Move VM disks</span><span class="sxs-lookup"><span data-stu-id="04a0c-235">Move VM disks</span></span>
<span data-ttu-id="04a0c-236">*This option applies only to multi-node deployments.*</span><span class="sxs-lookup"><span data-stu-id="04a0c-236">*This option applies only to multi-node deployments.*</span></span>

<span data-ttu-id="04a0c-237">The most extreme method to manage space involves the move of virtual machine disks.</span><span class="sxs-lookup"><span data-stu-id="04a0c-237">The most extreme method to manage space involves the move of virtual machine disks.</span></span> <span data-ttu-id="04a0c-238">Because moving an attached container (one that contains a VM disk) is complex, contact Microsoft Support to accomplish this action.</span><span class="sxs-lookup"><span data-stu-id="04a0c-238">Because moving an attached container (one that contains a VM disk) is complex, contact Microsoft Support to accomplish this action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04a0c-239">Next Steps</span><span class="sxs-lookup"><span data-stu-id="04a0c-239">Next Steps</span></span>
<span data-ttu-id="04a0c-240">Learn more about [offering virtual machines to users](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="04a0c-240">Learn more about [offering virtual machines to users](azure-stack-tutorial-tenant-vm.md).</span></span>
