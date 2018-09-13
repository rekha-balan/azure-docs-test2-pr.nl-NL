---
title: Create a VM availability set in Azure | Microsoft Docs
description: Learn how to create a managed availability set or unmanaged availability set for your virtual machines using Azure PowerShell or the portal in the Resource Manager deployment model.
keywords: availability set
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 34c30b45cfc4cad9e61b0193d76824c5c040aed4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564314"
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="b94bd-104">Increase VM availability by creating an Azure availability set</span><span class="sxs-lookup"><span data-stu-id="b94bd-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="b94bd-105">Availability sets provide redundancy to your application.</span><span class="sxs-lookup"><span data-stu-id="b94bd-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="b94bd-106">We recommend that you group two or more virtual machines in an availability set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="b94bd-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span><span class="sxs-lookup"><span data-stu-id="b94bd-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="b94bd-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="b94bd-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b94bd-109">VMs must be created in the same resource group as the availability set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="b94bd-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="b94bd-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="b94bd-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b94bd-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="b94bd-113">Use the portal to create an availability set before creating your VMs</span><span class="sxs-lookup"><span data-stu-id="b94bd-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="b94bd-114">In the hub menu, click **Browse** and select **Availability sets**.</span><span class="sxs-lookup"><span data-stu-id="b94bd-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="b94bd-115">On the **Availability sets blade**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b94bd-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Screenshot that shows the add button for creating a new availability set.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="b94bd-117">On the **Create availability set** blade, complete the information for your set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Screenshot that shows the information you need to enter to create the availability set.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="b94bd-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span><span class="sxs-lookup"><span data-stu-id="b94bd-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="b94bd-120">The first character must be a letter or number.</span><span class="sxs-lookup"><span data-stu-id="b94bd-120">The first character must be a letter or number.</span></span> <span data-ttu-id="b94bd-121">The last character must be a letter, number or underscore.</span><span class="sxs-lookup"><span data-stu-id="b94bd-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="b94bd-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span><span class="sxs-lookup"><span data-stu-id="b94bd-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="b94bd-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span><span class="sxs-lookup"><span data-stu-id="b94bd-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="b94bd-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span><span class="sxs-lookup"><span data-stu-id="b94bd-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="b94bd-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span><span class="sxs-lookup"><span data-stu-id="b94bd-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="b94bd-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span><span class="sxs-lookup"><span data-stu-id="b94bd-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="b94bd-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span><span class="sxs-lookup"><span data-stu-id="b94bd-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="b94bd-128">**Subscription** - select the subscription to use if you have more than one.</span><span class="sxs-lookup"><span data-stu-id="b94bd-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="b94bd-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span><span class="sxs-lookup"><span data-stu-id="b94bd-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="b94bd-130">You can also create a new resource group by typing in a name.</span><span class="sxs-lookup"><span data-stu-id="b94bd-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="b94bd-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span><span class="sxs-lookup"><span data-stu-id="b94bd-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="b94bd-132">The name cannot end in a period.</span><span class="sxs-lookup"><span data-stu-id="b94bd-132">The name cannot end in a period.</span></span> <span data-ttu-id="b94bd-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="b94bd-134">**Location** - select a location from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="b94bd-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="b94bd-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span><span class="sxs-lookup"><span data-stu-id="b94bd-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="b94bd-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span><span class="sxs-lookup"><span data-stu-id="b94bd-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="b94bd-137">When you are done entering the information, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b94bd-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="b94bd-138">Use the portal to create a virtual machine and an availability set at the same time</span><span class="sxs-lookup"><span data-stu-id="b94bd-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="b94bd-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="b94bd-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span><span class="sxs-lookup"><span data-stu-id="b94bd-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Screenshot that shows the process for creating a new availability set while you create the VM.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="b94bd-142">Add a new VM to an existing availability set in the portal</span><span class="sxs-lookup"><span data-stu-id="b94bd-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="b94bd-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span><span class="sxs-lookup"><span data-stu-id="b94bd-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Screenshot showing how to select an existing availability set to use for your VM.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="b94bd-145">Use PowerShell to create an availability set</span><span class="sxs-lookup"><span data-stu-id="b94bd-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="b94bd-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span><span class="sxs-lookup"><span data-stu-id="b94bd-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="b94bd-147">This needs to be done before you create the first VM that will be in the set.</span><span class="sxs-lookup"><span data-stu-id="b94bd-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="b94bd-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="b94bd-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b94bd-149">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="b94bd-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b94bd-150">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="b94bd-150">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


<span data-ttu-id="b94bd-151">If you are using managed disks for your VMs, type:</span><span class="sxs-lookup"><span data-stu-id="b94bd-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="b94bd-152">If you are using your own storage accounts for your VMs, type:</span><span class="sxs-lookup"><span data-stu-id="b94bd-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="b94bd-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="b94bd-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b94bd-154">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b94bd-154">Troubleshooting</span></span>
* <span data-ttu-id="b94bd-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span><span class="sxs-lookup"><span data-stu-id="b94bd-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="b94bd-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span><span class="sxs-lookup"><span data-stu-id="b94bd-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b94bd-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="b94bd-157">Next steps</span></span>
<span data-ttu-id="b94bd-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b94bd-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>





