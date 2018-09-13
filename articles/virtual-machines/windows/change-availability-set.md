---
title: Change a VMs availability set | Microsoft Docs
description: Learn how to change the availability set for your virtual machines using Azure PowerShell and the Resource Manager deployment model.
keywords: ''
services: virtual-machines-windows
documentationcenter: ''
author: Drewm3
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: d1d62d8c98664d1f64610f2e71fd19f069565b69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540800"
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="1e6c4-103">Change the availability set for a Windows VM</span><span class="sxs-lookup"><span data-stu-id="1e6c4-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="1e6c4-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="1e6c4-105">A VM can only be added to an availability set when it is created.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="1e6c4-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="1e6c4-107">Change the availability set using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e6c4-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="1e6c4-108">Capture the following key details from the VM to be modified.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="1e6c4-109">Name of the VM</span><span class="sxs-lookup"><span data-stu-id="1e6c4-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="1e6c4-110">VM Size</span><span class="sxs-lookup"><span data-stu-id="1e6c4-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="1e6c4-111">Network primary network interface and optional network interfaces if they exist on the VM</span><span class="sxs-lookup"><span data-stu-id="1e6c4-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="1e6c4-112">OS Disk Profile</span><span class="sxs-lookup"><span data-stu-id="1e6c4-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="1e6c4-113">Disk profiles for each data disk</span><span class="sxs-lookup"><span data-stu-id="1e6c4-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="1e6c4-114">VM extensions installed</span><span class="sxs-lookup"><span data-stu-id="1e6c4-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="1e6c4-115">Delete the VM without deleting any of the disks or the network interfaces.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="1e6c4-116">Create the availability set if it does not already exist</span><span class="sxs-lookup"><span data-stu-id="1e6c4-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="1e6c4-117">Recreate the VM using the new availability set</span><span class="sxs-lookup"><span data-stu-id="1e6c4-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="1e6c4-118">Add data disks and extensions.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-118">Add data disks and extensions.</span></span> <span data-ttu-id="1e6c4-119">For more information, see [Attach Data Disk to VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extension Configuration Samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e6c4-119">For more information, see [Attach Data Disk to VM](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extension Configuration Samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1e6c4-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="1e6c4-121">Example Script</span><span class="sxs-lookup"><span data-stu-id="1e6c4-121">Example Script</span></span>
<span data-ttu-id="1e6c4-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span><span class="sxs-lookup"><span data-stu-id="1e6c4-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="1e6c4-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e6c4-123">Next steps</span></span>
<span data-ttu-id="1e6c4-124">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e6c4-124">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

