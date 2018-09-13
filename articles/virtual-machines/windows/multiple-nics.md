---
title: Create a Windows VM with multiple NICs | Microsoft Docs
description: Learn how to create a Windows VM with multiple NICs attached to it using Azure PowerShell or Resource Manager templates.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 314af433945de8e7ce04446ccf353bee4b0f9c36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553929"
---
# <a name="create-a-windows-vm-with-multiple-nics"></a><span data-ttu-id="8fefd-103">Create a Windows VM with multiple NICs</span><span class="sxs-lookup"><span data-stu-id="8fefd-103">Create a Windows VM with multiple NICs</span></span>
<span data-ttu-id="8fefd-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span><span class="sxs-lookup"><span data-stu-id="8fefd-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="8fefd-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span><span class="sxs-lookup"><span data-stu-id="8fefd-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="8fefd-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span><span class="sxs-lookup"><span data-stu-id="8fefd-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="8fefd-107">For detailed information, including how to create multiple NICs within your own PowerShell scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8fefd-107">For detailed information, including how to create multiple NICs within your own PowerShell scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span> <span data-ttu-id="8fefd-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span><span class="sxs-lookup"><span data-stu-id="8fefd-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span></span>

## <a name="create-core-resources"></a><span data-ttu-id="8fefd-109">Create core resources</span><span class="sxs-lookup"><span data-stu-id="8fefd-109">Create core resources</span></span>
<span data-ttu-id="8fefd-110">Make sure that you have the [latest Azure PowerShell installed and configured](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8fefd-110">Make sure that you have the [latest Azure PowerShell installed and configured](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8fefd-111">Log in to your Azure account:</span><span class="sxs-lookup"><span data-stu-id="8fefd-111">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8fefd-112">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8fefd-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8fefd-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="8fefd-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="8fefd-114">First, create a resource group.</span><span class="sxs-lookup"><span data-stu-id="8fefd-114">First, create a resource group.</span></span> <span data-ttu-id="8fefd-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span><span class="sxs-lookup"><span data-stu-id="8fefd-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "WestUS"
```

<span data-ttu-id="8fefd-116">Create a storage account to hold your VMs.</span><span class="sxs-lookup"><span data-stu-id="8fefd-116">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="8fefd-117">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="8fefd-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```powershell
$storageAcc = New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" `
    -Location "WestUS" -Name "mystorageaccount" `
    -Kind "Storage" -SkuName "Premium_LRS" 
```

## <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="8fefd-118">Create virtual network and subnets</span><span class="sxs-lookup"><span data-stu-id="8fefd-118">Create virtual network and subnets</span></span>
<span data-ttu-id="8fefd-119">Define two virtual network subnets - one for front-end traffic and one for back-end traffic.</span><span class="sxs-lookup"><span data-stu-id="8fefd-119">Define two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="8fefd-120">The following example defines two subnets, named `mySubnetFrontEnd` and `mySubnetBackEnd`:</span><span class="sxs-lookup"><span data-stu-id="8fefd-120">The following example defines two subnets, named `mySubnetFrontEnd` and `mySubnetBackEnd`:</span></span>

```powershell
$mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
    -AddressPrefix "192.168.1.0/24"
$mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
    -AddressPrefix "192.168.2.0/24"
```

<span data-ttu-id="8fefd-121">Create your virtual network and subnets.</span><span class="sxs-lookup"><span data-stu-id="8fefd-121">Create your virtual network and subnets.</span></span> <span data-ttu-id="8fefd-122">The following example creates a virtual network named `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="8fefd-122">The following example creates a virtual network named `myVnet`:</span></span>

```powershell
$myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
    -Location "WestUS" -Name "myVnet" -AddressPrefix "192.168.0.0/16" `
    -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
```


## <a name="create-multiple-nics"></a><span data-ttu-id="8fefd-123">Create multiple NICs</span><span class="sxs-lookup"><span data-stu-id="8fefd-123">Create multiple NICs</span></span>
<span data-ttu-id="8fefd-124">Create two NICs, attaching one NIC to the front-end subnet and one NIC to the back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="8fefd-124">Create two NICs, attaching one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="8fefd-125">The following example creates two NICs, named `myNic1` and `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="8fefd-125">The following example creates two NICs, named `myNic1` and `myNic2`:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Location "WestUS" -Name "myNic1" -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Location "WestUS" -Name "myNic2" -SubnetId $backEnd.Id
```

<span data-ttu-id="8fefd-126">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span><span class="sxs-lookup"><span data-stu-id="8fefd-126">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="8fefd-127">The [more detailed multi-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a Network Security Group and assigning NICs.</span><span class="sxs-lookup"><span data-stu-id="8fefd-127">The [more detailed multi-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a Network Security Group and assigning NICs.</span></span>

## <a name="create-the-virtual-machine"></a><span data-ttu-id="8fefd-128">Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="8fefd-128">Create the virtual machine</span></span>
<span data-ttu-id="8fefd-129">Now start to build your VM configuration.</span><span class="sxs-lookup"><span data-stu-id="8fefd-129">Now start to build your VM configuration.</span></span> <span data-ttu-id="8fefd-130">Each VM size has a limit for the total number of NICs that you can add to a VM.</span><span class="sxs-lookup"><span data-stu-id="8fefd-130">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="8fefd-131">Read more about [Windows VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8fefd-131">Read more about [Windows VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="8fefd-132">First, set your VM credentials to the `$cred` variable as follows:</span><span class="sxs-lookup"><span data-stu-id="8fefd-132">First, set your VM credentials to the `$cred` variable as follows:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8fefd-133">The following example defines a VM named `myVM` and uses a VM size that supports up to two NICs (`Standard_DS2_v2`):</span><span class="sxs-lookup"><span data-stu-id="8fefd-133">The following example defines a VM named `myVM` and uses a VM size that supports up to two NICs (`Standard_DS2_v2`):</span></span>

```powershell
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2_v2"
```

<span data-ttu-id="8fefd-134">Create the rest of your VM config. The following example creates a Windows Server 2012 R2 VM:</span><span class="sxs-lookup"><span data-stu-id="8fefd-134">Create the rest of your VM config. The following example creates a Windows Server 2012 R2 VM:</span></span>

```powershell
$vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName "myVM" `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
```

<span data-ttu-id="8fefd-135">Attach the two NICs you previously created:</span><span class="sxs-lookup"><span data-stu-id="8fefd-135">Attach the two NICs you previously created:</span></span>

```powershell
$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
```

<span data-ttu-id="8fefd-136">Configure the storage and virtual disk for your new VM:</span><span class="sxs-lookup"><span data-stu-id="8fefd-136">Configure the storage and virtual disk for your new VM:</span></span>

```powershell
$blobPath = "vhds/WindowsVMosDisk.vhd"
$osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + $blobPath
$diskName = "windowsvmosdisk"
$vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $diskName -VhdUri $osDiskUri `
    -CreateOption "fromImage"
```

<span data-ttu-id="8fefd-137">Finally, create a VM:</span><span class="sxs-lookup"><span data-stu-id="8fefd-137">Finally, create a VM:</span></span>

```powershell
New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "WestUS"
```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="8fefd-138">Add a NIC to an existing VM</span><span class="sxs-lookup"><span data-stu-id="8fefd-138">Add a NIC to an existing VM</span></span>

<span data-ttu-id="8fefd-139">It is now possible to add a NIC to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="8fefd-139">It is now possible to add a NIC to an existing VM.</span></span> <span data-ttu-id="8fefd-140">To use this feature, you'll first need to deallocate the VM using the Stop-AzureRmVM cmdlet below.</span><span class="sxs-lookup"><span data-stu-id="8fefd-140">To use this feature, you'll first need to deallocate the VM using the Stop-AzureRmVM cmdlet below.</span></span>

```powershell
Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
```

<span data-ttu-id="8fefd-141">Next, get the existing configuration of the VM using the Get-AzureRmVM cmdlet</span><span class="sxs-lookup"><span data-stu-id="8fefd-141">Next, get the existing configuration of the VM using the Get-AzureRmVM cmdlet</span></span>

```powershell
$vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
```

<span data-ttu-id="8fefd-142">You can create a new NIC in the **same VNET as the VM** as shown at the beginning of this article or attach an existing NIC.</span><span class="sxs-lookup"><span data-stu-id="8fefd-142">You can create a new NIC in the **same VNET as the VM** as shown at the beginning of this article or attach an existing NIC.</span></span> <span data-ttu-id="8fefd-143">We'll assume you're attaching an existing NIC `MyNic3` in the VNET.</span><span class="sxs-lookup"><span data-stu-id="8fefd-143">We'll assume you're attaching an existing NIC `MyNic3` in the VNET.</span></span> 

```powershell
$nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId -Primary | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
```

> [!NOTE]
> <span data-ttu-id="8fefd-144">One of the NICs on a multi-NIC VM needs to be Primary so we're setting the new NIC as primary.</span><span class="sxs-lookup"><span data-stu-id="8fefd-144">One of the NICs on a multi-NIC VM needs to be Primary so we're setting the new NIC as primary.</span></span> <span data-ttu-id="8fefd-145">If your previous NIC on the VM is Primary, then you do not need to specify the -Primary switch.</span><span class="sxs-lookup"><span data-stu-id="8fefd-145">If your previous NIC on the VM is Primary, then you do not need to specify the -Primary switch.</span></span> <span data-ttu-id="8fefd-146">If you want to switch the Primary NIC on the VM, follow the steps below</span><span class="sxs-lookup"><span data-stu-id="8fefd-146">If you want to switch the Primary NIC on the VM, follow the steps below</span></span>

```powershell
$vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"

# Find out all the NICs on the VM and find which one is Primary
$vm.NetworkProfile.NetworkInterfaces

# Set the NIC 0 to be primary
$vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
$vm.NetworkProfile.NetworkInterfaces[1].Primary = $false

# Update the VM state in Azure
Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="8fefd-147">Remove a NIC from an existing VM</span><span class="sxs-lookup"><span data-stu-id="8fefd-147">Remove a NIC from an existing VM</span></span>

<span data-ttu-id="8fefd-148">A NIC can also be removed from a VM.</span><span class="sxs-lookup"><span data-stu-id="8fefd-148">A NIC can also be removed from a VM.</span></span> <span data-ttu-id="8fefd-149">To use this feature, you'll first need to deallocate the VM using the Stop-AzureRmVM cmdlet below.</span><span class="sxs-lookup"><span data-stu-id="8fefd-149">To use this feature, you'll first need to deallocate the VM using the Stop-AzureRmVM cmdlet below.</span></span>

```powershell
Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
```

<span data-ttu-id="8fefd-150">Next, get the existing configuration of the VM using the Get-AzureRmVM cmdlet</span><span class="sxs-lookup"><span data-stu-id="8fefd-150">Next, get the existing configuration of the VM using the Get-AzureRmVM cmdlet</span></span>

```powershell
$vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
```

<span data-ttu-id="8fefd-151">Now view all the NICs on the VM and copy the name of the one you want to remove</span><span class="sxs-lookup"><span data-stu-id="8fefd-151">Now view all the NICs on the VM and copy the name of the one you want to remove</span></span>

```powershell
$vm.NetworkProfile.NetworkInterfaces

Remove-AzureRmNetworkInterface -Name "myNic3" -ResourceGroupName "myResourceGroup"
```

## <a name="creating-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="8fefd-152">Creating multiple NICs using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="8fefd-152">Creating multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="8fefd-153">Azure Resource Manager templates use declarative JSON files to define your environment.</span><span class="sxs-lookup"><span data-stu-id="8fefd-153">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="8fefd-154">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fefd-154">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8fefd-155">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="8fefd-155">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="8fefd-156">You use *copy* to specify the number of instances to create:</span><span class="sxs-lookup"><span data-stu-id="8fefd-156">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="8fefd-157">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8fefd-157">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="8fefd-158">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `MyNic2`, etc. The following shows an example of appending the index value:</span><span class="sxs-lookup"><span data-stu-id="8fefd-158">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `MyNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="8fefd-159">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8fefd-159">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fefd-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fefd-160">Next steps</span></span>
<span data-ttu-id="8fefd-161">Make sure to review [Windows VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) when trying to creating a VM with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="8fefd-161">Make sure to review [Windows VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="8fefd-162">Pay attention to the maximum number of NICs each VM size supports.</span><span class="sxs-lookup"><span data-stu-id="8fefd-162">Pay attention to the maximum number of NICs each VM size supports.</span></span> 


