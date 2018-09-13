---
title: Convert a Windows virtual machine from unmanaged disks to managed disks - Azure Managed Disks | Microsoft Docs
description: How to convert a Windows VM from unmanaged disks to managed disks by using PowerShell in the Resource Manager deployment model
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/12/2018
ms.author: cynthn
ms.openlocfilehash: 131f60ac4529835f4c19d85640ad720942a0cd8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828672"
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="033ac-103">Convert a Windows virtual machine from unmanaged disks to managed disks</span><span class="sxs-lookup"><span data-stu-id="033ac-103">Convert a Windows virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="033ac-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](managed-disks-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="033ac-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="033ac-105">This process converts both the OS disk and any attached data disks.</span><span class="sxs-lookup"><span data-stu-id="033ac-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="033ac-106">This article shows you how to convert VMs by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="033ac-106">This article shows you how to convert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="033ac-107">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="033ac-107">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="033ac-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="033ac-108">Before you begin</span></span>


* <span data-ttu-id="033ac-109">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="033ac-109">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

* <span data-ttu-id="033ac-110">Review [the FAQ about migration to Managed Disks](faq-for-disks.md#migrate-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="033ac-110">Review [the FAQ about migration to Managed Disks](faq-for-disks.md#migrate-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="033ac-111">Convert single-instance VMs</span><span class="sxs-lookup"><span data-stu-id="033ac-111">Convert single-instance VMs</span></span>
<span data-ttu-id="033ac-112">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="033ac-112">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="033ac-113">(If your VMs are in an availability set, see the next section.)</span><span class="sxs-lookup"><span data-stu-id="033ac-113">(If your VMs are in an availability set, see the next section.)</span></span> 

1. <span data-ttu-id="033ac-114">Deallocate the VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="033ac-114">Deallocate the VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="033ac-115">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="033ac-115">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span> 

  ```azurepowershell-interactive
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="033ac-116">Convert the VM to managed disks by using the [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="033ac-116">Convert the VM to managed disks by using the [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="033ac-117">The following process converts the previous VM, including the OS disk and any data disks, and starts the Virtual Machine:</span><span class="sxs-lookup"><span data-stu-id="033ac-117">The following process converts the previous VM, including the OS disk and any data disks, and starts the Virtual Machine:</span></span>

  ```azurepowershell-interactive
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```



## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="033ac-118">Convert VMs in an availability set</span><span class="sxs-lookup"><span data-stu-id="033ac-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="033ac-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="033ac-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

1. <span data-ttu-id="033ac-120">Convert the availability set by using the [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="033ac-120">Convert the availability set by using the [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="033ac-121">The following example updates the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="033ac-121">The following example updates the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

  ```azurepowershell-interactive
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="033ac-122">If the region where your availability set is located has only 2 managed fault domains but the number of unmanaged fault domains is 3, this command shows an error similar to "The specified fault domain count 3 must fall in the range 1 to 2."</span><span class="sxs-lookup"><span data-stu-id="033ac-122">If the region where your availability set is located has only 2 managed fault domains but the number of unmanaged fault domains is 3, this command shows an error similar to "The specified fault domain count 3 must fall in the range 1 to 2."</span></span> <span data-ttu-id="033ac-123">To resolve the error, update the fault domain to 2 and update `Sku` to `Aligned` as follows:</span><span class="sxs-lookup"><span data-stu-id="033ac-123">To resolve the error, update the fault domain to 2 and update `Sku` to `Aligned` as follows:</span></span>

  ```azurepowershell-interactive
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="033ac-124">Deallocate and convert the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="033ac-124">Deallocate and convert the VMs in the availability set.</span></span> <span data-ttu-id="033ac-125">The following script deallocates each VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it automatically as apart of the conversion process:</span><span class="sxs-lookup"><span data-stu-id="033ac-125">The following script deallocates each VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it automatically as apart of the conversion process:</span></span>

  ```azurepowershell-interactive
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
  }
  ```


## <a name="troubleshooting"></a><span data-ttu-id="033ac-126">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="033ac-126">Troubleshooting</span></span>

<span data-ttu-id="033ac-127">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run the `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span><span class="sxs-lookup"><span data-stu-id="033ac-127">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run the `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="033ac-128">A simple retry usually unblocks the situation.</span><span class="sxs-lookup"><span data-stu-id="033ac-128">A simple retry usually unblocks the situation.</span></span>
<span data-ttu-id="033ac-129">Before converting, make sure all the VM extensions are in the 'Provisioning succeeded' state or the conversion will fail with the error code 409.</span><span class="sxs-lookup"><span data-stu-id="033ac-129">Before converting, make sure all the VM extensions are in the 'Provisioning succeeded' state or the conversion will fail with the error code 409.</span></span>


## <a name="convert-using-the-azure-portal"></a><span data-ttu-id="033ac-130">Convert using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="033ac-130">Convert using the Azure portal</span></span>

<span data-ttu-id="033ac-131">You can also convert unmanaged disks to managed disks using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="033ac-131">You can also convert unmanaged disks to managed disks using the Azure portal.</span></span>

1. <span data-ttu-id="033ac-132">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="033ac-132">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="033ac-133">Select the VM from the list of VMs in the portal.</span><span class="sxs-lookup"><span data-stu-id="033ac-133">Select the VM from the list of VMs in the portal.</span></span>
3. <span data-ttu-id="033ac-134">In the blade for the VM, select **Disks** from the menu.</span><span class="sxs-lookup"><span data-stu-id="033ac-134">In the blade for the VM, select **Disks** from the menu.</span></span>
4. <span data-ttu-id="033ac-135">At the top of the **Disks** blade, select **Migrate to managed disks**.</span><span class="sxs-lookup"><span data-stu-id="033ac-135">At the top of the **Disks** blade, select **Migrate to managed disks**.</span></span>
5. <span data-ttu-id="033ac-136">If your VM is in an availability set, there will be a warning on the **Migrate to managed disks** blade that you need to convert the availability set first.</span><span class="sxs-lookup"><span data-stu-id="033ac-136">If your VM is in an availability set, there will be a warning on the **Migrate to managed disks** blade that you need to convert the availability set first.</span></span> <span data-ttu-id="033ac-137">The warning should have a link you can click to convert the availability set.</span><span class="sxs-lookup"><span data-stu-id="033ac-137">The warning should have a link you can click to convert the availability set.</span></span> <span data-ttu-id="033ac-138">Once the availability set is converted or if your VM is not in an availability set, click **Migrate** to start the process of migrating your disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="033ac-138">Once the availability set is converted or if your VM is not in an availability set, click **Migrate** to start the process of migrating your disks to managed disks.</span></span> 

<span data-ttu-id="033ac-139">The VM will be stopped and restarted after migration is complete.</span><span class="sxs-lookup"><span data-stu-id="033ac-139">The VM will be stopped and restarted after migration is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="033ac-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="033ac-140">Next steps</span></span>

[<span data-ttu-id="033ac-141">Convert standard managed disks to premium</span><span class="sxs-lookup"><span data-stu-id="033ac-141">Convert standard managed disks to premium</span></span>](convert-disk-storage.md)

<span data-ttu-id="033ac-142">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="033ac-142">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

