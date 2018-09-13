---
title: Migrate a Classic VM to an ARM Managed Disk VM | Microsoft Docs
description: Migrate a single Azure VM from the classic deployment model to Managed Disks in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 9fa01c83a2230c2434ab731c00c16d5c9b2e68fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551029"
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="9820f-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span><span class="sxs-lookup"><span data-stu-id="9820f-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="9820f-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](../../storage/storage-managed-disks-overview.md) in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="9820f-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](../../storage/storage-managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="9820f-105">Plan for the migration to Managed Disks</span><span class="sxs-lookup"><span data-stu-id="9820f-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="9820f-106">This section helps you to make the best decision on VM and disk types.</span><span class="sxs-lookup"><span data-stu-id="9820f-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="9820f-107">Location</span><span class="sxs-lookup"><span data-stu-id="9820f-107">Location</span></span>

<span data-ttu-id="9820f-108">Pick a location where Azure Managed Disks are available.</span><span class="sxs-lookup"><span data-stu-id="9820f-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="9820f-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span><span class="sxs-lookup"><span data-stu-id="9820f-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="9820f-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span><span class="sxs-lookup"><span data-stu-id="9820f-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="9820f-111">VM sizes</span><span class="sxs-lookup"><span data-stu-id="9820f-111">VM sizes</span></span>

<span data-ttu-id="9820f-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span><span class="sxs-lookup"><span data-stu-id="9820f-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="9820f-113">Review the VM sizes that are Premium Storage capable.</span><span class="sxs-lookup"><span data-stu-id="9820f-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="9820f-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="9820f-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="9820f-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span><span class="sxs-lookup"><span data-stu-id="9820f-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="9820f-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span><span class="sxs-lookup"><span data-stu-id="9820f-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="9820f-117">Disk sizes</span><span class="sxs-lookup"><span data-stu-id="9820f-117">Disk sizes</span></span>

<span data-ttu-id="9820f-118">**Premium Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="9820f-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="9820f-119">There are three types of Premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span><span class="sxs-lookup"><span data-stu-id="9820f-119">There are three types of Premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="9820f-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span><span class="sxs-lookup"><span data-stu-id="9820f-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="9820f-121">Premium Disks Type</span><span class="sxs-lookup"><span data-stu-id="9820f-121">Premium Disks Type</span></span>  | <span data-ttu-id="9820f-122">P10</span><span class="sxs-lookup"><span data-stu-id="9820f-122">P10</span></span>               | <span data-ttu-id="9820f-123">P20</span><span class="sxs-lookup"><span data-stu-id="9820f-123">P20</span></span>               | <span data-ttu-id="9820f-124">P30</span><span class="sxs-lookup"><span data-stu-id="9820f-124">P30</span></span>               |
|---------------------|-------------------|-------------------|-------------------|
| <span data-ttu-id="9820f-125">Disk size</span><span class="sxs-lookup"><span data-stu-id="9820f-125">Disk size</span></span>           | <span data-ttu-id="9820f-126">128 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-126">128 GB</span></span>            | <span data-ttu-id="9820f-127">512 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-127">512 GB</span></span>            | <span data-ttu-id="9820f-128">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="9820f-128">1024 GB (1 TB)</span></span>    |
| <span data-ttu-id="9820f-129">IOPS per disk</span><span class="sxs-lookup"><span data-stu-id="9820f-129">IOPS per disk</span></span>       | <span data-ttu-id="9820f-130">500</span><span class="sxs-lookup"><span data-stu-id="9820f-130">500</span></span>               | <span data-ttu-id="9820f-131">2300</span><span class="sxs-lookup"><span data-stu-id="9820f-131">2300</span></span>              | <span data-ttu-id="9820f-132">5000</span><span class="sxs-lookup"><span data-stu-id="9820f-132">5000</span></span>              |
| <span data-ttu-id="9820f-133">Throughput per disk</span><span class="sxs-lookup"><span data-stu-id="9820f-133">Throughput per disk</span></span> | <span data-ttu-id="9820f-134">100 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-134">100 MB per second</span></span> | <span data-ttu-id="9820f-135">150 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-135">150 MB per second</span></span> | <span data-ttu-id="9820f-136">200 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-136">200 MB per second</span></span> |

<span data-ttu-id="9820f-137">**Standard Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="9820f-137">**Standard Managed Disks**</span></span>

<span data-ttu-id="9820f-138">There are five types of Standard Managed disks that can be used with your VM.</span><span class="sxs-lookup"><span data-stu-id="9820f-138">There are five types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="9820f-139">Each of them have different capacity but have same IOPS and throughput limits.</span><span class="sxs-lookup"><span data-stu-id="9820f-139">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="9820f-140">Choose the type of Standard Managed disks based on the capacity needs of your application.</span><span class="sxs-lookup"><span data-stu-id="9820f-140">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="9820f-141">Standard Disk Type</span><span class="sxs-lookup"><span data-stu-id="9820f-141">Standard Disk Type</span></span>  | <span data-ttu-id="9820f-142">S4</span><span class="sxs-lookup"><span data-stu-id="9820f-142">S4</span></span>               | <span data-ttu-id="9820f-143">S6</span><span class="sxs-lookup"><span data-stu-id="9820f-143">S6</span></span>               | <span data-ttu-id="9820f-144">S10</span><span class="sxs-lookup"><span data-stu-id="9820f-144">S10</span></span>              | <span data-ttu-id="9820f-145">S20</span><span class="sxs-lookup"><span data-stu-id="9820f-145">S20</span></span>              | <span data-ttu-id="9820f-146">S30</span><span class="sxs-lookup"><span data-stu-id="9820f-146">S30</span></span>              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| <span data-ttu-id="9820f-147">Disk size</span><span class="sxs-lookup"><span data-stu-id="9820f-147">Disk size</span></span>           | <span data-ttu-id="9820f-148">30 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-148">30 GB</span></span>            | <span data-ttu-id="9820f-149">64 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-149">64 GB</span></span>            | <span data-ttu-id="9820f-150">128 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-150">128 GB</span></span>           | <span data-ttu-id="9820f-151">512 GB</span><span class="sxs-lookup"><span data-stu-id="9820f-151">512 GB</span></span>           | <span data-ttu-id="9820f-152">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="9820f-152">1024 GB (1 TB)</span></span>   |
| <span data-ttu-id="9820f-153">IOPS per disk</span><span class="sxs-lookup"><span data-stu-id="9820f-153">IOPS per disk</span></span>       | <span data-ttu-id="9820f-154">500</span><span class="sxs-lookup"><span data-stu-id="9820f-154">500</span></span>              | <span data-ttu-id="9820f-155">500</span><span class="sxs-lookup"><span data-stu-id="9820f-155">500</span></span>              | <span data-ttu-id="9820f-156">500</span><span class="sxs-lookup"><span data-stu-id="9820f-156">500</span></span>              | <span data-ttu-id="9820f-157">500</span><span class="sxs-lookup"><span data-stu-id="9820f-157">500</span></span>              | <span data-ttu-id="9820f-158">500</span><span class="sxs-lookup"><span data-stu-id="9820f-158">500</span></span>              |
| <span data-ttu-id="9820f-159">Throughput per disk</span><span class="sxs-lookup"><span data-stu-id="9820f-159">Throughput per disk</span></span> | <span data-ttu-id="9820f-160">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-160">60 MB per second</span></span> | <span data-ttu-id="9820f-161">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-161">60 MB per second</span></span> | <span data-ttu-id="9820f-162">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-162">60 MB per second</span></span> | <span data-ttu-id="9820f-163">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-163">60 MB per second</span></span> | <span data-ttu-id="9820f-164">60 MB per second</span><span class="sxs-lookup"><span data-stu-id="9820f-164">60 MB per second</span></span> |

### <a name="disk-caching-policy"></a><span data-ttu-id="9820f-165">Disk caching policy</span><span class="sxs-lookup"><span data-stu-id="9820f-165">Disk caching policy</span></span> 

<span data-ttu-id="9820f-166">**Premium Managed Disks**</span><span class="sxs-lookup"><span data-stu-id="9820f-166">**Premium Managed Disks**</span></span>

<span data-ttu-id="9820f-167">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="9820f-167">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="9820f-168">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span><span class="sxs-lookup"><span data-stu-id="9820f-168">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="9820f-169">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span><span class="sxs-lookup"><span data-stu-id="9820f-169">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="9820f-170">Pricing</span><span class="sxs-lookup"><span data-stu-id="9820f-170">Pricing</span></span>

<span data-ttu-id="9820f-171">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="9820f-171">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="9820f-172">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span><span class="sxs-lookup"><span data-stu-id="9820f-172">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="9820f-173">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span><span class="sxs-lookup"><span data-stu-id="9820f-173">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="9820f-174">Checklist</span><span class="sxs-lookup"><span data-stu-id="9820f-174">Checklist</span></span>

1.  <span data-ttu-id="9820f-175">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="9820f-175">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="9820f-176">Decide the new VM series you will be using.</span><span class="sxs-lookup"><span data-stu-id="9820f-176">Decide the new VM series you will be using.</span></span> <span data-ttu-id="9820f-177">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="9820f-177">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="9820f-178">Decide the exact VM size you will use which are available in the region you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="9820f-178">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="9820f-179">VM size needs to be large enough to support the number of data disks you have.</span><span class="sxs-lookup"><span data-stu-id="9820f-179">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="9820f-180">For example, if you have four data disks, the VM must have two or more cores.</span><span class="sxs-lookup"><span data-stu-id="9820f-180">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="9820f-181">Also, consider processing power, memory and network bandwidth needs.</span><span class="sxs-lookup"><span data-stu-id="9820f-181">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="9820f-182">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span><span class="sxs-lookup"><span data-stu-id="9820f-182">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="9820f-183">Prepare your application for downtime.</span><span class="sxs-lookup"><span data-stu-id="9820f-183">Prepare your application for downtime.</span></span> <span data-ttu-id="9820f-184">To do a clean migration, you have to stop all the processing in the current system.</span><span class="sxs-lookup"><span data-stu-id="9820f-184">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="9820f-185">Only then you can get it to consistent state which you can migrate to the new platform.</span><span class="sxs-lookup"><span data-stu-id="9820f-185">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="9820f-186">Downtime duration depends on the amount of data in the disks to migrate.</span><span class="sxs-lookup"><span data-stu-id="9820f-186">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="9820f-187">Migrate the VM</span><span class="sxs-lookup"><span data-stu-id="9820f-187">Migrate the VM</span></span>

<span data-ttu-id="9820f-188">Prepare your application for downtime.</span><span class="sxs-lookup"><span data-stu-id="9820f-188">Prepare your application for downtime.</span></span> <span data-ttu-id="9820f-189">To do a clean migration, you have to stop all the processing in the current system.</span><span class="sxs-lookup"><span data-stu-id="9820f-189">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="9820f-190">Only then you can get it to consistent state which you can migrate to the new platform.</span><span class="sxs-lookup"><span data-stu-id="9820f-190">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="9820f-191">Downtime duration depends the amount of data in the disks to migrate.</span><span class="sxs-lookup"><span data-stu-id="9820f-191">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="9820f-192">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="9820f-192">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="9820f-193">Create a managed OS disk using the VHD from the classic VM.</span><span class="sxs-lookup"><span data-stu-id="9820f-193">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="9820f-194">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span><span class="sxs-lookup"><span data-stu-id="9820f-194">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="9820f-195">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span><span class="sxs-lookup"><span data-stu-id="9820f-195">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="9820f-196">Attach the OS disk to the new VM.</span><span class="sxs-lookup"><span data-stu-id="9820f-196">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="9820f-197">Create a managed data disk from the data VHD file and add it to the new VM.</span><span class="sxs-lookup"><span data-stu-id="9820f-197">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="9820f-198">Create the new VM by setting public IP, Virtual Network and NIC.</span><span class="sxs-lookup"><span data-stu-id="9820f-198">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="9820f-199">There may be additional steps necessary to support your application that is not be covered by this guide.</span><span class="sxs-lookup"><span data-stu-id="9820f-199">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9820f-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="9820f-200">Next steps</span></span>

- <span data-ttu-id="9820f-201">Connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9820f-201">Connect to the virtual machine.</span></span> <span data-ttu-id="9820f-202">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9820f-202">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

