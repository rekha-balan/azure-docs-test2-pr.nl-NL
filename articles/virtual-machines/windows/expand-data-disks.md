---
title: Expand a data disk attached to a Windows VM in Azure | Microsoft Docs
description: Expand the size of a data disk that is attached to a Windows virtual machine using PowerShell.
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b40645721fce80d1120561d17239efc77bb6c97b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670063"
---
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a><span data-ttu-id="45890-103">Increase the size of a data disk attached to a Windows VM</span><span class="sxs-lookup"><span data-stu-id="45890-103">Increase the size of a data disk attached to a Windows VM</span></span>

<span data-ttu-id="45890-104">If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45890-104">If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell.</span></span> <span data-ttu-id="45890-105">After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.</span><span class="sxs-lookup"><span data-stu-id="45890-105">After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.</span></span>


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a><span data-ttu-id="45890-106">Use Powershell to increase the size of a managed data disk</span><span class="sxs-lookup"><span data-stu-id="45890-106">Use Powershell to increase the size of a managed data disk</span></span>

<span data-ttu-id="45890-107">To increase the size of a managed data disk, use the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="45890-107">To increase the size of a managed data disk, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="45890-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="45890-108">Get-AzureRMReseourceGroup</span></span>](/powershell/Get-AzureRMReseourceGroup) | [<span data-ttu-id="45890-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="45890-109">Get-AzureRMVM</span></span>](/powershell/getazurermvm)                  |
| [<span data-ttu-id="45890-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="45890-110">Stop-AzureRMVM</span></span>](/powershell/stop-azurermvm)                       | [<span data-ttu-id="45890-111">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="45890-111">Set-AzureRmVMDataDisk</span></span>](/powershell/Set-AzureRmVMDataDisk) |
| [<span data-ttu-id="45890-112">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="45890-112">Update-AzureRmVM</span></span>](/powershell/update-azurermvm)                   | [<span data-ttu-id="45890-113">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="45890-113">Start-AzureRmVM</span></span>](/powershell/start-azurermvm)             |
<br>

<span data-ttu-id="45890-114">The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.</span><span class="sxs-lookup"><span data-stu-id="45890-114">The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.</span></span>

```powershell
# Select resource group
     
    $rg = Get-AzureRMReseourceGroup | Out-GridView `
        -Title "Select the resource group" `
        -PassThru
     
    $rgName = $rg.ResourceGroupName

# Select the VM
     
    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk
     
    $disk = $vm.dataDiskNames | Out-GridView `
        -Title "Select a data disk" `
        -PassThru
    
# Specify a larger size for the data disk 
       
    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk
     
    $vm | Stop-AzureRMVM -Force

# Set the new disk size
    
    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" -DiskSizeInGB $size

# View the new size of the data disk(s)
    
    $vm.StorageProfile.DataDisks

# Update the configuration in Azure
    
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    
    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name

```

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="45890-115">Use PowerShell to increase the size of an unmanaged data disk</span><span class="sxs-lookup"><span data-stu-id="45890-115">Use PowerShell to increase the size of an unmanaged data disk</span></span>

<span data-ttu-id="45890-116">To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="45890-116">To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="45890-117">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="45890-117">Get-AzureRMStorageAccount</span></span>](/powershell/Get-AzureRMStorageAccount) | [<span data-ttu-id="45890-118">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="45890-118">Get-AzureRMVM</span></span>](/powershell/getazurermvm)                  |
| [<span data-ttu-id="45890-119">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="45890-119">Stop-AzureRMVM</span></span>](/powershell/stop-azurermvm)                       | [<span data-ttu-id="45890-120">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="45890-120">Set-AzureRmVMDataDisk</span></span>](/powershell/Set-AzureRmVMDataDisk) |
| [<span data-ttu-id="45890-121">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="45890-121">Update-AzureRmVM</span></span>](/powershell/update-azurermvm)                   | [<span data-ttu-id="45890-122">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="45890-122">Start-AzureRmVM</span></span>](/powershell/start-azurermvm)             |

<br>

<span data-ttu-id="45890-123">The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.</span><span class="sxs-lookup"><span data-stu-id="45890-123">The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.</span></span>

```powershell

# Select Azure Storage Account
     
    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru
     
    $rgName = $storageAccount.ResourceGroupName

# Select the VM
     
    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk to resize
     
    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk to resize" `
            -PassThru
     
    
# Specify a larger data disk size 
       
    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk
     
    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update the configuration in Azure
    
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name
    
```

## <a name="allocate-the-unallocated-disk-space"></a><span data-ttu-id="45890-124">Allocate the unallocated disk space</span><span class="sxs-lookup"><span data-stu-id="45890-124">Allocate the unallocated disk space</span></span> 

<span data-ttu-id="45890-125">Once you have made the drive larger, you need to allocate the new unallocated space from within the VM.</span><span class="sxs-lookup"><span data-stu-id="45890-125">Once you have made the drive larger, you need to allocate the new unallocated space from within the VM.</span></span> <span data-ttu-id="45890-126">To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="45890-126">To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="45890-127">Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span><span class="sxs-lookup"><span data-stu-id="45890-127">Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="45890-128">You can also use a custom script extension:</span><span class="sxs-lookup"><span data-stu-id="45890-128">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="45890-129">The script file can contain something like this code to increase the drive allocation to the maximum size the disks:</span><span class="sxs-lookup"><span data-stu-id="45890-129">The script file can contain something like this code to increase the drive allocation to the maximum size the disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="45890-130">Next Steps</span><span class="sxs-lookup"><span data-stu-id="45890-130">Next Steps</span></span>
- [<span data-ttu-id="45890-131">Learn more about disks and VHDs</span><span class="sxs-lookup"><span data-stu-id="45890-131">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)