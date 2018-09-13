---
title: Use PowerShell to resize a Windows VM in Azure | Microsoft Docs
description: Resize a Windows virtual machine created in the Resource Manager deployment model, using Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: cynthn
ms.openlocfilehash: 55cec3074ced65cf874537af395cfff3aded4755
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828308"
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="7f63f-103">Resize a Windows VM</span><span class="sxs-lookup"><span data-stu-id="7f63f-103">Resize a Windows VM</span></span>

<span data-ttu-id="7f63f-104">This article shows you how to move a VM to a different [VM size](sizes.md) using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="7f63f-104">This article shows you how to move a VM to a different [VM size](sizes.md) using Azure Powershell.</span></span>

<span data-ttu-id="7f63f-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span><span class="sxs-lookup"><span data-stu-id="7f63f-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="7f63f-106">In some cases, you must deallocate the VM first.</span><span class="sxs-lookup"><span data-stu-id="7f63f-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="7f63f-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

<span data-ttu-id="7f63f-108">If your VM uses Premium Storage, make sure that you choose an **s** version of the size to get Premium Storage support.</span><span class="sxs-lookup"><span data-stu-id="7f63f-108">If your VM uses Premium Storage, make sure that you choose an **s** version of the size to get Premium Storage support.</span></span> <span data-ttu-id="7f63f-109">For example, choose Standard_E4**s**_v3 instead of Standard_E4_v3.</span><span class="sxs-lookup"><span data-stu-id="7f63f-109">For example, choose Standard_E4**s**_v3 instead of Standard_E4_v3.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="7f63f-110">Resize a Windows VM not in an availability set</span><span class="sxs-lookup"><span data-stu-id="7f63f-110">Resize a Windows VM not in an availability set</span></span>

<span data-ttu-id="7f63f-111">Set some variables.</span><span class="sxs-lookup"><span data-stu-id="7f63f-111">Set some variables.</span></span> <span data-ttu-id="7f63f-112">Replace the values with your own information.</span><span class="sxs-lookup"><span data-stu-id="7f63f-112">Replace the values with your own information.</span></span>

```powershell
$resourceGroup = "myResourceGroup"
$vmName = "myVM"
```

<span data-ttu-id="7f63f-113">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span><span class="sxs-lookup"><span data-stu-id="7f63f-113">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
```powershell
Get-AzureRmVMSize -ResourceGroupName $resourceGroup -VMName $vmName 
```

<span data-ttu-id="7f63f-114">If the size you want is listed, run the following commands to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-114">If the size you want is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="7f63f-115">If the desired size is not listed, go on to step 3.</span><span class="sxs-lookup"><span data-stu-id="7f63f-115">If the desired size is not listed, go on to step 3.</span></span>
   
```powershell
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName
$vm.HardwareProfile.VmSize = "<newVMsize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
```

<span data-ttu-id="7f63f-116">If the size you want is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-116">If the size you want is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span> <span data-ttu-id="7f63f-117">Replace **<newVMsize>** with the size you want.</span><span class="sxs-lookup"><span data-stu-id="7f63f-117">Replace **<newVMsize>** with the size you want.</span></span>
   
```powershell
Stop-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName -Force
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName
$vm.HardwareProfile.VmSize = "<newVMSize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
Start-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
```

> [!WARNING]
> <span data-ttu-id="7f63f-118">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-118">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="7f63f-119">The OS and data disks are not affected.</span><span class="sxs-lookup"><span data-stu-id="7f63f-119">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="7f63f-120">Resize a Windows VM in an availability set</span><span class="sxs-lookup"><span data-stu-id="7f63f-120">Resize a Windows VM in an availability set</span></span>

<span data-ttu-id="7f63f-121">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-121">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="7f63f-122">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span><span class="sxs-lookup"><span data-stu-id="7f63f-122">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="7f63f-123">To resize a VM in an availability set, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="7f63f-123">To resize a VM in an availability set, perform the following steps.</span></span>

```powershell
$resourceGroup = "myResourceGroup"
$vmName = "myVM"
```

<span data-ttu-id="7f63f-124">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span><span class="sxs-lookup"><span data-stu-id="7f63f-124">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
```powershell
Get-AzureRmVMSize -ResourceGroupName $resourceGroup -VMName $vmName 
```

<span data-ttu-id="7f63f-125">If the desired size is listed, run the following commands to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="7f63f-125">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="7f63f-126">If it is not listed, go to the next section.</span><span class="sxs-lookup"><span data-stu-id="7f63f-126">If it is not listed, go to the next section.</span></span>
   
```powershell
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName 
$vm.HardwareProfile.VmSize = "<newVmSize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
```
    
<span data-ttu-id="7f63f-127">If the size you want is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span><span class="sxs-lookup"><span data-stu-id="7f63f-127">If the size you want is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>

<span data-ttu-id="7f63f-128">Stop all VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="7f63f-128">Stop all VMs in the availability set.</span></span>
   
```powershell
$as = Get-AzureRmAvailabilitySet -ResourceGroupName $resourceGroup
$vmIds = $as.VirtualMachinesReferences
foreach ($vmId in $vmIDs){
    $string = $vmID.Id.Split("/")
    $vmName = $string[8]
    Stop-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName -Force
    } 
```

<span data-ttu-id="7f63f-129">Resize and restart the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="7f63f-129">Resize and restart the VMs in the availability set.</span></span>
   
```powershell
$newSize = "<newVmSize>"
$as = Get-AzureRmAvailabilitySet -ResourceGroupName $resourceGroup
$vmIds = $as.VirtualMachinesReferences
  foreach ($vmId in $vmIDs){
    $string = $vmID.Id.Split("/")
    $vmName = $string[8]
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
    $vm.HardwareProfile.VmSize = $newSize
    Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
    Start-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
    }
```

## <a name="next-steps"></a><span data-ttu-id="7f63f-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f63f-130">Next steps</span></span>

<span data-ttu-id="7f63f-131">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="7f63f-131">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

