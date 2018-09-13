---
title: Attach a data disk to a Windows VM in Azure using PowerShell | Microsoft Docs
description: How to attach new or existing data disk to a Windows VM using PowerShell with the Resource Manager deployment model.
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
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: b991d1cef88495e61db53a0003f0386f40a6d5bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564039"
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="5fcd7-103">Attach a data disk to a Windows VM using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fcd7-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="5fcd7-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="5fcd7-105">If your VM uses managed disks, you can attach additional managed data disks.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="5fcd7-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="5fcd7-107">Before you do this, review these tips:</span><span class="sxs-lookup"><span data-stu-id="5fcd7-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="5fcd7-108">The size of the virtual machine controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5fcd7-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fcd7-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5fcd7-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5fcd7-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="5fcd7-112">Premium storage is available in certain regions.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5fcd7-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fcd7-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5fcd7-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5fcd7-114">Before you begin</span></span>
<span data-ttu-id="5fcd7-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5fcd7-116">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5fcd7-117">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="5fcd7-117">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="5fcd7-118">Add an empty data disk to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5fcd7-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="5fcd7-119">This example shows how to add an empty data disk to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="5fcd7-120">Using managed disks</span><span class="sxs-lookup"><span data-stu-id="5fcd7-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="5fcd7-121">Using unmanaged disks in a storage account</span><span class="sxs-lookup"><span data-stu-id="5fcd7-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="5fcd7-122">Initialize the disk</span><span class="sxs-lookup"><span data-stu-id="5fcd7-122">Initialize the disk</span></span>

<span data-ttu-id="5fcd7-123">After you add an empty disk, you need to initialize it.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="5fcd7-124">To initialize the disk, you can log in to a VM and use disk management.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="5fcd7-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="5fcd7-126">You can also use a custom script extension:</span><span class="sxs-lookup"><span data-stu-id="5fcd7-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="5fcd7-127">The script file can contain something like this code to initialize the disks:</span><span class="sxs-lookup"><span data-stu-id="5fcd7-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="5fcd7-128">Attach an existing data disk to a VM</span><span class="sxs-lookup"><span data-stu-id="5fcd7-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="5fcd7-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5fcd7-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="5fcd7-130">Using managed disks</span><span class="sxs-lookup"><span data-stu-id="5fcd7-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="5fcd7-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="5fcd7-131">Next steps</span></span>

<span data-ttu-id="5fcd7-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5fcd7-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
