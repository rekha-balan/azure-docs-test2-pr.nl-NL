---
title: Change a VMs availability set | Microsoft Docs
description: Learn how to change the availability set for your virtual machines using Azure PowerShell and the Resource Manager deployment model.
keywords: ''
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: cynthn
ms.openlocfilehash: 1982564e4d0371a2febc6af0179548f242a6e0f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783515"
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="0d0dd-103">Change the availability set for a Windows VM</span><span class="sxs-lookup"><span data-stu-id="0d0dd-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="0d0dd-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d0dd-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="0d0dd-105">A VM can only be added to an availability set when it is created.</span><span class="sxs-lookup"><span data-stu-id="0d0dd-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="0d0dd-106">To change the availability set, you need to delete and then recreate the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0d0dd-106">To change the availability set, you need to delete and then recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set"></a><span data-ttu-id="0d0dd-107">Change the availability set</span><span class="sxs-lookup"><span data-stu-id="0d0dd-107">Change the availability set</span></span> 

<span data-ttu-id="0d0dd-108">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span><span class="sxs-lookup"><span data-stu-id="0d0dd-108">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
# Set variables
    $resourceGroup = "myResourceGroup"
    $vmName = "myVM"
    $newAvailSetName = "myAvailabilitySet"

# Get the details of the VM to be moved to the Availablity Set
    $originalVM = Get-AzureRmVM `
       -ResourceGroupName $resourceGroup `
       -Name $vmName

# Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName

# Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet `
       -ResourceGroupName $resourceGroup `
       -Name $newAvailSetName `
       -ErrorAction Ignore
    if (-Not $availSet) {
    $availSet = New-AzureRmAvailabilitySet `
       -Location $originalVM.Location `
       -Name $newAvailSetName `
       -ResourceGroupName $resourceGroup `
       -PlatformFaultDomainCount 2 `
       -PlatformUpdateDomainCount 2 `
       -Sku Aligned
    }

# Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig `
       -VMName $originalVM.Name `
       -VMSize $originalVM.HardwareProfile.VmSize `
       -AvailabilitySetId $availSet.Id
  
    Set-AzureRmVMOSDisk `
       -VM $newVM -CreateOption Attach `
       -ManagedDiskId $originalVM.StorageProfile.OsDisk.ManagedDisk.Id `
       -Name $originalVM.StorageProfile.OsDisk.Name `
       -Windows

# Add Data Disks
    foreach ($disk in $originalVM.StorageProfile.DataDisks) { 
    Add-AzureRmVMDataDisk -VM $newVM `
       -Name $disk.Name `
       -ManagedDiskId $disk.ManagedDisk.Id `
       -Caching $disk.Caching `
       -Lun $disk.Lun `
       -DiskSizeInGB $disk.DiskSizeGB `
       -CreateOption Attach
    }
    
# Add NIC(s)
    foreach ($nic in $originalVM.NetworkProfile.NetworkInterfaces) {
        Add-AzureRmVMNetworkInterface `
           -VM $newVM `
           -Id $nic.Id
    }

# Recreate the VM
    New-AzureRmVM `
       -ResourceGroupName $resourceGroup `
       -Location $originalVM.Location `
       -VM $newVM `
       -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="0d0dd-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d0dd-109">Next steps</span></span>

<span data-ttu-id="0d0dd-110">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d0dd-110">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

