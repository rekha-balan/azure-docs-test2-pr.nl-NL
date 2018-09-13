---
title: Create a VM with a static public IP address - PowerShell | Microsoft Docs
description: Learn how to create a VM with a static public IP address using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/08/2018
ms.author: jdial
ms.openlocfilehash: b59157b0f17380dbe4386fbd9ac75776e22f749e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804224"
---
# <a name="create-a-virtual-machine-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="20aa5-103">Create a virtual machine with a static public IP address using PowerShell</span><span class="sxs-lookup"><span data-stu-id="20aa5-103">Create a virtual machine with a static public IP address using PowerShell</span></span>

<span data-ttu-id="20aa5-104">You can create a virtual machine with a static public IP address.</span><span class="sxs-lookup"><span data-stu-id="20aa5-104">You can create a virtual machine with a static public IP address.</span></span> <span data-ttu-id="20aa5-105">A public IP address enables you to communicate to a virtual machine from the internet.</span><span class="sxs-lookup"><span data-stu-id="20aa5-105">A public IP address enables you to communicate to a virtual machine from the internet.</span></span> <span data-ttu-id="20aa5-106">Assign a static public IP address, rather than a dynamic address, to ensure that the address never changes.</span><span class="sxs-lookup"><span data-stu-id="20aa5-106">Assign a static public IP address, rather than a dynamic address, to ensure that the address never changes.</span></span> <span data-ttu-id="20aa5-107">Learn more about [static public IP addresses](virtual-network-ip-addresses-overview-arm.md#allocation-method).</span><span class="sxs-lookup"><span data-stu-id="20aa5-107">Learn more about [static public IP addresses](virtual-network-ip-addresses-overview-arm.md#allocation-method).</span></span> <span data-ttu-id="20aa5-108">To change a public IP address assigned to an existing virtual machine from dynamic to static, or to work with private IP addresses, see [Add, change, or remove IP addresses](virtual-network-network-interface-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="20aa5-108">To change a public IP address assigned to an existing virtual machine from dynamic to static, or to work with private IP addresses, see [Add, change, or remove IP addresses](virtual-network-network-interface-addresses.md).</span></span> <span data-ttu-id="20aa5-109">Public IP addresses have a [nominal charge](https://azure.microsoft.com/pricing/details/ip-addresses), and there is a [limit](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) to the number of public IP addresses that you can use per subscription.</span><span class="sxs-lookup"><span data-stu-id="20aa5-109">Public IP addresses have a [nominal charge](https://azure.microsoft.com/pricing/details/ip-addresses), and there is a [limit](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) to the number of public IP addresses that you can use per subscription.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="20aa5-110">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="20aa5-110">Create a virtual machine</span></span>

<span data-ttu-id="20aa5-111">You can complete the following steps from your local computer or by using the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="20aa5-111">You can complete the following steps from your local computer or by using the Azure Cloud Shell.</span></span> <span data-ttu-id="20aa5-112">To use your local computer, ensure you have the [Azure PowerShell installed](/powershell/azure/install-azurerm-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20aa5-112">To use your local computer, ensure you have the [Azure PowerShell installed](/powershell/azure/install-azurerm-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="20aa5-113">To use the Azure Cloud Shell, select **Try It** in the top right corner of any command box that follows.</span><span class="sxs-lookup"><span data-stu-id="20aa5-113">To use the Azure Cloud Shell, select **Try It** in the top right corner of any command box that follows.</span></span> <span data-ttu-id="20aa5-114">The Cloud Shell signs you into Azure.</span><span class="sxs-lookup"><span data-stu-id="20aa5-114">The Cloud Shell signs you into Azure.</span></span>

1. <span data-ttu-id="20aa5-115">If using the Cloud Shell, skip to step 2.</span><span class="sxs-lookup"><span data-stu-id="20aa5-115">If using the Cloud Shell, skip to step 2.</span></span> <span data-ttu-id="20aa5-116">Open a command session and sign into Azure with `Connect-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="20aa5-116">Open a command session and sign into Azure with `Connect-AzureRmAccount`.</span></span>
2. <span data-ttu-id="20aa5-117">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="20aa5-117">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="20aa5-118">The following example creates a resource group in the East US Azure region:</span><span class="sxs-lookup"><span data-stu-id="20aa5-118">The following example creates a resource group in the East US Azure region:</span></span>

   ```azurepowershell-interactive
   New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
   ```

3. <span data-ttu-id="20aa5-119">Create a virtual machine with the [New-AzureRmVM](/powershell/module/AzureRM.Compute/New-AzureRmVM) command.</span><span class="sxs-lookup"><span data-stu-id="20aa5-119">Create a virtual machine with the [New-AzureRmVM](/powershell/module/AzureRM.Compute/New-AzureRmVM) command.</span></span> <span data-ttu-id="20aa5-120">The `-AllocationMethod "Static"` option assigns a static public IP address to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="20aa5-120">The `-AllocationMethod "Static"` option assigns a static public IP address to the virtual machine.</span></span> <span data-ttu-id="20aa5-121">The following example creates a Windows Server virtual machine with a static, basic SKU public IP address named *myPublicIpAddress*.</span><span class="sxs-lookup"><span data-stu-id="20aa5-121">The following example creates a Windows Server virtual machine with a static, basic SKU public IP address named *myPublicIpAddress*.</span></span> <span data-ttu-id="20aa5-122">When prompted, provide a username and password to be used as the sign in credentials for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="20aa5-122">When prompted, provide a username and password to be used as the sign in credentials for the virtual machine:</span></span>

   ```azurepowershell-interactive
   New-AzureRmVm `
     -ResourceGroupName "myResourceGroup" `
     -Name "myVM" `
     -Location "East US" `
     -PublicIpAddressName "myPublicIpAddress" `
     -AllocationMethod "Static"
   ```

   <span data-ttu-id="20aa5-123">If the public IP address must be a standard SKU, you have to [create a public IP address](virtual-network-public-ip-address.md#create-a-public-ip-address), [create a network interface](virtual-network-network-interface.md#create-a-network-interface), [assign the public IP address to the network interface](virtual-network-network-interface-addresses.md#add-ip-addresses), and then [create a virtual machine with the network interface](virtual-network-network-interface-vm.md#add-existing-network-interfaces-to-a-new-vm), in separate steps.</span><span class="sxs-lookup"><span data-stu-id="20aa5-123">If the public IP address must be a standard SKU, you have to [create a public IP address](virtual-network-public-ip-address.md#create-a-public-ip-address), [create a network interface](virtual-network-network-interface.md#create-a-network-interface), [assign the public IP address to the network interface](virtual-network-network-interface-addresses.md#add-ip-addresses), and then [create a virtual machine with the network interface](virtual-network-network-interface-vm.md#add-existing-network-interfaces-to-a-new-vm), in separate steps.</span></span> <span data-ttu-id="20aa5-124">Learn more about [Public IP address SKUs](virtual-network-ip-addresses-overview-arm.md#sku).</span><span class="sxs-lookup"><span data-stu-id="20aa5-124">Learn more about [Public IP address SKUs](virtual-network-ip-addresses-overview-arm.md#sku).</span></span> <span data-ttu-id="20aa5-125">If the virtual machine will be added to the back-end pool of a public Azure Load Balancer, the SKU of the virtual machine's public IP address must match the SKU of the load balancer's public IP address.</span><span class="sxs-lookup"><span data-stu-id="20aa5-125">If the virtual machine will be added to the back-end pool of a public Azure Load Balancer, the SKU of the virtual machine's public IP address must match the SKU of the load balancer's public IP address.</span></span> <span data-ttu-id="20aa5-126">For details, see [Azure Load Balancer](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#skus).</span><span class="sxs-lookup"><span data-stu-id="20aa5-126">For details, see [Azure Load Balancer](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#skus).</span></span>

4. <span data-ttu-id="20aa5-127">View the public IP address assigned and confirm that it was created as a static address, with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="20aa5-127">View the public IP address assigned and confirm that it was created as a static address, with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress):</span></span>

   ```azurepowershell-interactive
   Get-AzureRmPublicIpAddress `
     -ResourceGroupName "myResourceGroup" `
     -Name "myPublicIpAddress" `
     | Select "IpAddress", "PublicIpAllocationMethod" `
     | Format-Table
   ```

   <span data-ttu-id="20aa5-128">Azure assigned a public IP address from addresses used in the region you created the virtual machine in.</span><span class="sxs-lookup"><span data-stu-id="20aa5-128">Azure assigned a public IP address from addresses used in the region you created the virtual machine in.</span></span> <span data-ttu-id="20aa5-129">You can download the list of ranges (prefixes) for the Azure [Public](https://www.microsoft.com/download/details.aspx?id=56519), [US government](https://www.microsoft.com/download/details.aspx?id=57063), [China](https://www.microsoft.com/download/details.aspx?id=57062), and [Germany](https://www.microsoft.com/download/details.aspx?id=57064) clouds.</span><span class="sxs-lookup"><span data-stu-id="20aa5-129">You can download the list of ranges (prefixes) for the Azure [Public](https://www.microsoft.com/download/details.aspx?id=56519), [US government](https://www.microsoft.com/download/details.aspx?id=57063), [China](https://www.microsoft.com/download/details.aspx?id=57062), and [Germany](https://www.microsoft.com/download/details.aspx?id=57064) clouds.</span></span>

> [!WARNING]
<span data-ttu-id="20aa5-130">Do not modify the IP address settings within the virtual machine's operating system.</span><span class="sxs-lookup"><span data-stu-id="20aa5-130">Do not modify the IP address settings within the virtual machine's operating system.</span></span> <span data-ttu-id="20aa5-131">The operating system is unaware of Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="20aa5-131">The operating system is unaware of Azure public IP addresses.</span></span> <span data-ttu-id="20aa5-132">Though you can add private IP address settings to the operating system, we recommend not doing so unless necessary, and not until after reading [Add a private IP address to an operating system](virtual-network-network-interface-addresses.md#private).</span><span class="sxs-lookup"><span data-stu-id="20aa5-132">Though you can add private IP address settings to the operating system, we recommend not doing so unless necessary, and not until after reading [Add a private IP address to an operating system](virtual-network-network-interface-addresses.md#private).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="20aa5-133">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="20aa5-133">Clean up resources</span></span>

<span data-ttu-id="20aa5-134">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="20aa5-134">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="20aa5-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="20aa5-135">Next steps</span></span>

- <span data-ttu-id="20aa5-136">Learn more about [public IP addresses](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) in Azure</span><span class="sxs-lookup"><span data-stu-id="20aa5-136">Learn more about [public IP addresses](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) in Azure</span></span>
- <span data-ttu-id="20aa5-137">Learn more about all [public IP address settings](virtual-network-public-ip-address.md#create-a-public-ip-address)</span><span class="sxs-lookup"><span data-stu-id="20aa5-137">Learn more about all [public IP address settings](virtual-network-public-ip-address.md#create-a-public-ip-address)</span></span>
- <span data-ttu-id="20aa5-138">Learn more about [private IP addresses](virtual-network-ip-addresses-overview-arm.md#private-ip-addresses) and assigning a [static private IP address](virtual-network-network-interface-addresses.md#add-ip-addresses) to an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="20aa5-138">Learn more about [private IP addresses](virtual-network-ip-addresses-overview-arm.md#private-ip-addresses) and assigning a [static private IP address](virtual-network-network-interface-addresses.md#add-ip-addresses) to an Azure virtual machine</span></span>
- <span data-ttu-id="20aa5-139">Learn more about creating [Linux](../virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Windows](../virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machines</span><span class="sxs-lookup"><span data-stu-id="20aa5-139">Learn more about creating [Linux](../virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Windows](../virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machines</span></span>