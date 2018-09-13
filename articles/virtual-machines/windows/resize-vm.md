---
title: Use PowerShell to resize a Windows VM in Azure | Microsoft Docs
description: Resize a Windows virtual machine created in the Resource Manager deployment model, using Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: Drewm3
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 29fd031933eb625db3ba94697b9a17ed89e39f0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670074"
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="5908e-103">Resize a Windows VM</span><span class="sxs-lookup"><span data-stu-id="5908e-103">Resize a Windows VM</span></span>
<span data-ttu-id="5908e-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="5908e-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="5908e-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span><span class="sxs-lookup"><span data-stu-id="5908e-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="5908e-106">In some cases, you must deallocate the VM first.</span><span class="sxs-lookup"><span data-stu-id="5908e-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="5908e-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="5908e-108">Resize a Windows VM not in an availability set</span><span class="sxs-lookup"><span data-stu-id="5908e-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="5908e-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span><span class="sxs-lookup"><span data-stu-id="5908e-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="5908e-110">If the desired size is listed, run the following commands to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="5908e-111">If the desired size is not listed, go on to step 3.</span><span class="sxs-lookup"><span data-stu-id="5908e-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="5908e-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="5908e-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="5908e-114">The OS and data disks are not affected.</span><span class="sxs-lookup"><span data-stu-id="5908e-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="5908e-115">Resize a Windows VM in an availability set</span><span class="sxs-lookup"><span data-stu-id="5908e-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="5908e-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="5908e-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span><span class="sxs-lookup"><span data-stu-id="5908e-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="5908e-118">To resize a VM in an availability set, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="5908e-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="5908e-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span><span class="sxs-lookup"><span data-stu-id="5908e-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="5908e-120">If the desired size is listed, run the following commands to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="5908e-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="5908e-121">If it is not listed, go to step 3.</span><span class="sxs-lookup"><span data-stu-id="5908e-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="5908e-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span><span class="sxs-lookup"><span data-stu-id="5908e-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="5908e-123">Stop all VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="5908e-123">Stop all VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="5908e-124">Resize and restart the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="5908e-124">Resize and restart the VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="5908e-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="5908e-125">Next steps</span></span>
* <span data-ttu-id="5908e-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="5908e-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

