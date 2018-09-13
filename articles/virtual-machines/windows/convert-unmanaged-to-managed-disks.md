---
title: Convert a VM from unmanaged to managed disks - Azure | Microsoft Docs
description: Convert a VM from unmanaged disks to managed disks using PowerShell in the Resource Manager deployment model
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
ms.date: 02/22/2017
ms.author: cynthn
ms.openlocfilehash: b9da473a5229fde22f71c3becf3dfe37d881a33a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540857"
---
# <a name="convert-a-vm-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="01984-103">Convert a VM from unmanaged disks to managed disks</span><span class="sxs-lookup"><span data-stu-id="01984-103">Convert a VM from unmanaged disks to managed disks</span></span>

<span data-ttu-id="01984-104">If you have existing Azure VMs that use unmanaged disks in storage accounts and you want to be able to take advantage of [Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), you can convert the VMs.</span><span class="sxs-lookup"><span data-stu-id="01984-104">If you have existing Azure VMs that use unmanaged disks in storage accounts and you want to be able to take advantage of [Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), you can convert the VMs.</span></span> <span data-ttu-id="01984-105">The process converts both the OS disk and any attached data disks from using an unmanaged disks in a storage account to using managed disks.</span><span class="sxs-lookup"><span data-stu-id="01984-105">The process converts both the OS disk and any attached data disks from using an unmanaged disks in a storage account to using managed disks.</span></span> <span data-ttu-id="01984-106">The VMs are shut down and deallocated, then you use Powershell to convert the VM to use managed disks.</span><span class="sxs-lookup"><span data-stu-id="01984-106">The VMs are shut down and deallocated, then you use Powershell to convert the VM to use managed disks.</span></span> <span data-ttu-id="01984-107">After the conversion, you restart the VM and it will now be using managed disks.</span><span class="sxs-lookup"><span data-stu-id="01984-107">After the conversion, you restart the VM and it will now be using managed disks.</span></span>

<span data-ttu-id="01984-108">Before starting,  make sure that you review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="01984-108">Before starting,  make sure that you review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>
<span data-ttu-id="01984-109">Test the migration process by migrating a test virtual machine before performing the migration in production because the migration process is not reversible.</span><span class="sxs-lookup"><span data-stu-id="01984-109">Test the migration process by migrating a test virtual machine before performing the migration in production because the migration process is not reversible.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="01984-110">During the conversion, you will be deallocating the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-110">During the conversion, you will be deallocating the VM.</span></span> <span data-ttu-id="01984-111">Deallocating the VM means that it will have a new IP address when it is started after the conversion.</span><span class="sxs-lookup"><span data-stu-id="01984-111">Deallocating the VM means that it will have a new IP address when it is started after the conversion.</span></span> <span data-ttu-id="01984-112">If you have a dependency on a fixed IP, you should use a reserved IP.</span><span class="sxs-lookup"><span data-stu-id="01984-112">If you have a dependency on a fixed IP, you should use a reserved IP.</span></span>


## <a name="managed-disks-and-azure-storage-service-encryption-sse"></a><span data-ttu-id="01984-113">Managed Disks and Azure Storage Service Encryption (SSE)</span><span class="sxs-lookup"><span data-stu-id="01984-113">Managed Disks and Azure Storage Service Encryption (SSE)</span></span>

<span data-ttu-id="01984-114">You cannot convert an unmanaged VM created in the Resource Manager deployment model to Managed Disks if any of the attached unmanaged disks is in a storage account that is, or at any time has been, encrypted using [Azure Storage Service Encryption (SSE)](../../storage/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01984-114">You cannot convert an unmanaged VM created in the Resource Manager deployment model to Managed Disks if any of the attached unmanaged disks is in a storage account that is, or at any time has been, encrypted using [Azure Storage Service Encryption (SSE)](../../storage/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="01984-115">The following steps detail how to convert unmanaged VM that are, or have been, in an encrypted storage account:</span><span class="sxs-lookup"><span data-stu-id="01984-115">The following steps detail how to convert unmanaged VM that are, or have been, in an encrypted storage account:</span></span>

<span data-ttu-id="01984-116">**Data Disks**:</span><span class="sxs-lookup"><span data-stu-id="01984-116">**Data Disks**:</span></span>
1.  <span data-ttu-id="01984-117">Detach the Data Disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-117">Detach the Data Disk from the VM.</span></span>
2.  <span data-ttu-id="01984-118">Copy the VHD to a storage account that has never been enabled for SSE.</span><span class="sxs-lookup"><span data-stu-id="01984-118">Copy the VHD to a storage account that has never been enabled for SSE.</span></span> <span data-ttu-id="01984-119">To copy the disk to another storage account, use [AzCopy](../../storage/storage-use-azcopy.md): `AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:myDataDisk.vhd`</span><span class="sxs-lookup"><span data-stu-id="01984-119">To copy the disk to another storage account, use [AzCopy](../../storage/storage-use-azcopy.md): `AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:myDataDisk.vhd`</span></span>
3.  <span data-ttu-id="01984-120">Attach the copied disk to the VM and convert the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-120">Attach the copied disk to the VM and convert the VM.</span></span>

<span data-ttu-id="01984-121">**OS Disk**:</span><span class="sxs-lookup"><span data-stu-id="01984-121">**OS Disk**:</span></span>
1.  <span data-ttu-id="01984-122">Stop deallocated the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-122">Stop deallocated the VM.</span></span> <span data-ttu-id="01984-123">Save the VM configuration if needed.</span><span class="sxs-lookup"><span data-stu-id="01984-123">Save the VM configuration if needed.</span></span>
2.  <span data-ttu-id="01984-124">Copy the OS VHD to a storage account that has never been enabled for SSE.</span><span class="sxs-lookup"><span data-stu-id="01984-124">Copy the OS VHD to a storage account that has never been enabled for SSE.</span></span> <span data-ttu-id="01984-125">To copy the disk to another storage account, use [AzCopy](../../storage/storage-use-azcopy.md): `AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:myVhd.vhd`</span><span class="sxs-lookup"><span data-stu-id="01984-125">To copy the disk to another storage account, use [AzCopy](../../storage/storage-use-azcopy.md): `AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:myVhd.vhd`</span></span>
3.  <span data-ttu-id="01984-126">Create a VM that uses managed disks and attach that VHD file as the OS disk during creation.</span><span class="sxs-lookup"><span data-stu-id="01984-126">Create a VM that uses managed disks and attach that VHD file as the OS disk during creation.</span></span>

## <a name="convert-vms-in-an-availability-set-to-managed-disks-in-a-managed-availability-set"></a><span data-ttu-id="01984-127">Convert VMs in an availability set to managed disks in a managed availability set</span><span class="sxs-lookup"><span data-stu-id="01984-127">Convert VMs in an availability set to managed disks in a managed availability set</span></span>

<span data-ttu-id="01984-128">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="01984-128">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="01984-129">The following script updates the availability set to be a managed availability set, then it deallocates, coverts the disks and then restarts each VM in the availability set.</span><span class="sxs-lookup"><span data-stu-id="01984-129">The following script updates the availability set to be a managed availability set, then it deallocates, coverts the disks and then restarts each VM in the availability set.</span></span>

```powershell
$rgName = 'myResourceGroup'
$avSetName = 'myAvailabilitySet'

$avSet =  Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Managed

foreach($vmInfo in $avSet.VirtualMachinesReferences)
    {
   $vm =  Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}

   Stop-AzureRmVM -ResourceGroupName $rgName -Name  $vm.Name -Force

   ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
   
    }
```

## <a name="convert-existing-azure-vms-to-managed-disks-of-the-same-storage-type"></a><span data-ttu-id="01984-130">Convert existing Azure VMs to managed disks of the same storage type</span><span class="sxs-lookup"><span data-stu-id="01984-130">Convert existing Azure VMs to managed disks of the same storage type</span></span>

<span data-ttu-id="01984-131">This section covers how to convert your existing Azure VMs from unmanaged disks in storage accounts to managed disks when you will be using the same storage type.</span><span class="sxs-lookup"><span data-stu-id="01984-131">This section covers how to convert your existing Azure VMs from unmanaged disks in storage accounts to managed disks when you will be using the same storage type.</span></span> <span data-ttu-id="01984-132">You can use this process to go from Premium (SSD) unmanaged disks to Premium managed disks or from standard (HDD) unmanaged disks to standard managed disks.</span><span class="sxs-lookup"><span data-stu-id="01984-132">You can use this process to go from Premium (SSD) unmanaged disks to Premium managed disks or from standard (HDD) unmanaged disks to standard managed disks.</span></span> 

1. <span data-ttu-id="01984-133">Create variables and deallocate the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-133">Create variables and deallocate the VM.</span></span> <span data-ttu-id="01984-134">This example sets the resource group name to **myResourceGroup** and the VM name to **myVM**.</span><span class="sxs-lookup"><span data-stu-id="01984-134">This example sets the resource group name to **myResourceGroup** and the VM name to **myVM**.</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $vmName = "myVM"
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
   
    <span data-ttu-id="01984-135">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="01984-135">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
    
2. <span data-ttu-id="01984-136">Convert all of the disks associated with the VM including the OS disk and any data disks.</span><span class="sxs-lookup"><span data-stu-id="01984-136">Convert all of the disks associated with the VM including the OS disk and any data disks.</span></span>

    ```powershell
    ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
    ```


## <a name="migrate-existing-azure-vms-using-standard-unmanaged-disks-to-premium-managed-disks"></a><span data-ttu-id="01984-137">Migrate existing Azure VMs using standard unmanaged disks to Premium managed disks</span><span class="sxs-lookup"><span data-stu-id="01984-137">Migrate existing Azure VMs using standard unmanaged disks to Premium managed disks</span></span>

<span data-ttu-id="01984-138">This section will show you how to convert your existing Azure VMs on Standard unmanaged disks to Premium managed disks.</span><span class="sxs-lookup"><span data-stu-id="01984-138">This section will show you how to convert your existing Azure VMs on Standard unmanaged disks to Premium managed disks.</span></span> <span data-ttu-id="01984-139">In order to use Premium Managed Disks, your VM must use a [VM size](sizes.md) that supports Premium storage.</span><span class="sxs-lookup"><span data-stu-id="01984-139">In order to use Premium Managed Disks, your VM must use a [VM size](sizes.md) that supports Premium storage.</span></span>


1.  <span data-ttu-id="01984-140">First, set the common parameters.</span><span class="sxs-lookup"><span data-stu-id="01984-140">First, set the common parameters.</span></span> <span data-ttu-id="01984-141">Make sure the [VM size](sizes.md) you select supports Premium storage.</span><span class="sxs-lookup"><span data-stu-id="01984-141">Make sure the [VM size](sizes.md) you select supports Premium storage.</span></span>

    ```powershell
    $resourceGroupName = 'YourResourceGroupName'
    $vmName = 'YourVMName'
    $size = 'Standard_DS2_v2'
    ```
1.  <span data-ttu-id="01984-142">Get the VM with Unmanaged disks</span><span class="sxs-lookup"><span data-stu-id="01984-142">Get the VM with Unmanaged disks</span></span>

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
    ```
    
1.  <span data-ttu-id="01984-143">Stop (Deallocate) the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-143">Stop (Deallocate) the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName -Force
    ```

1.  <span data-ttu-id="01984-144">Update the size of the VM to Premium Storage capable size available in the region where VM is located.</span><span class="sxs-lookup"><span data-stu-id="01984-144">Update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span>

    ```powershell
    $vm.HardwareProfile.VmSize = $size
    Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroupName
    ```

1.  <span data-ttu-id="01984-145">Convert virtual machine with unmanaged disks to Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="01984-145">Convert virtual machine with unmanaged disks to Managed Disks.</span></span> 

    <span data-ttu-id="01984-146">If you get internal server error, please retry 2-3 times before reaching out to our support team.</span><span class="sxs-lookup"><span data-stu-id="01984-146">If you get internal server error, please retry 2-3 times before reaching out to our support team.</span></span>

    ```powershell
    ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $resourceGroupName -VMName $vmName
    ```
1. <span data-ttu-id="01984-147">Stop (deallocate) the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-147">Stop (deallocate) the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName -Force
    ```
2.  <span data-ttu-id="01984-148">Upgrade all of the disks to Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="01984-148">Upgrade all of the disks to Premium Storage.</span></span>

    ```powershell
    $vmDisks = Get-AzureRmDisk -ResourceGroupName $resourceGroupName 
    foreach ($disk in $vmDisks) 
        {
        if($disk.OwnerId -eq $vm.Id)
            {
             $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType PremiumLRS
             Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $resourceGroupName `
             -DiskName $disk.Name
            }
        }
    ```
1. <span data-ttu-id="01984-149">Start the VM.</span><span class="sxs-lookup"><span data-stu-id="01984-149">Start the VM.</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    ```
    
<span data-ttu-id="01984-150">You can also have a mixture of disks that use standard and Premium storage.</span><span class="sxs-lookup"><span data-stu-id="01984-150">You can also have a mixture of disks that use standard and Premium storage.</span></span>
    

## <a name="next-steps"></a><span data-ttu-id="01984-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="01984-151">Next steps</span></span>

<span data-ttu-id="01984-152">Take a read-only copy of a VM using [snapshots](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="01984-152">Take a read-only copy of a VM using [snapshots](snapshot-copy-managed-disk.md).</span></span>

