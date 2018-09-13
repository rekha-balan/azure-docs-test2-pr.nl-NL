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
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a>Increase the size of a data disk attached to a Windows VM

If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell. After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a>Use Powershell to increase the size of a managed data disk

To increase the size of a managed data disk, use the following PowerShell cmdlets:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/Get-AzureRMReseourceGroup) | [Get-AzureRMVM](/powershell/getazurermvm)                  |
| [Stop-AzureRMVM](/powershell/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/Set-AzureRmVMDataDisk) |
| [Update-AzureRmVM](/powershell/update-azurermvm)                   | [Start-AzureRmVM](/powershell/start-azurermvm)             |
<br>

The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.

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

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a>Use PowerShell to increase the size of an unmanaged data disk

To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/Get-AzureRMStorageAccount) | [Get-AzureRMVM](/powershell/getazurermvm)                  |
| [Stop-AzureRMVM](/powershell/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/Set-AzureRmVMDataDisk) |
| [Update-AzureRmVM](/powershell/update-azurermvm)                   | [Start-AzureRmVM](/powershell/start-azurermvm)             |

<br>

The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.

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

## <a name="allocate-the-unallocated-disk-space"></a>Allocate the unallocated disk space 

Once you have made the drive larger, you need to allocate the new unallocated space from within the VM. To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc). Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk. You can also use a custom script extension: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
The script file can contain something like this code to increase the drive allocation to the maximum size the disks:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Next Steps
- [Learn more about disks and VHDs](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)