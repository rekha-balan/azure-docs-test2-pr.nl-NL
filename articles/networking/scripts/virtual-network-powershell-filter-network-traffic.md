---
title: Azure PowerShell script sample - Filter VM network traffic | Microsoft Docs
description: Azure PowerShell script sample - Filter inbound and outbound VM network traffic.
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 0cac36b8dec530dc5b4fa00ccd6e775a39c2d80d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868425"
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="8a08c-103">Filter inbound and outbound VM network traffic</span><span class="sxs-lookup"><span data-stu-id="8a08c-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="8a08c-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="8a08c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="8a08c-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span><span class="sxs-lookup"><span data-stu-id="8a08c-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="8a08c-106">After running the script, you will have one virtual machine with two NICs.</span><span class="sxs-lookup"><span data-stu-id="8a08c-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="8a08c-107">Each NIC is connected to a different subnet.</span><span class="sxs-lookup"><span data-stu-id="8a08c-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="8a08c-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="8a08c-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8a08c-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="8a08c-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8a08c-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8a08c-110">Clean up deployment</span></span> 

<span data-ttu-id="8a08c-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="8a08c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8a08c-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8a08c-112">Script explanation</span></span>

<span data-ttu-id="8a08c-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="8a08c-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="8a08c-114">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8a08c-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="8a08c-115">Command</span><span class="sxs-lookup"><span data-stu-id="8a08c-115">Command</span></span> | <span data-ttu-id="8a08c-116">Notes</span><span class="sxs-lookup"><span data-stu-id="8a08c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a08c-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a08c-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8a08c-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8a08c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8a08c-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8a08c-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8a08c-120">Creates a subnet configuration object</span><span class="sxs-lookup"><span data-stu-id="8a08c-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="8a08c-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8a08c-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8a08c-122">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="8a08c-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="8a08c-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8a08c-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8a08c-124">Creates security rules to be assigned to a network security group.</span><span class="sxs-lookup"><span data-stu-id="8a08c-124">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="8a08c-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8a08c-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="8a08c-126">Creates NSG rules that allow or block specific ports to specific subnets.</span><span class="sxs-lookup"><span data-stu-id="8a08c-126">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="8a08c-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8a08c-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8a08c-128">Associates NSGs to subnets.</span><span class="sxs-lookup"><span data-stu-id="8a08c-128">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="8a08c-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8a08c-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8a08c-130">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="8a08c-130">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="8a08c-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8a08c-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8a08c-132">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="8a08c-132">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="8a08c-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="8a08c-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="8a08c-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="8a08c-134">Creates a VM configuration.</span></span> <span data-ttu-id="8a08c-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="8a08c-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="8a08c-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="8a08c-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="8a08c-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8a08c-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8a08c-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8a08c-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="8a08c-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a08c-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8a08c-140">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="8a08c-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a08c-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a08c-141">Next steps</span></span>

<span data-ttu-id="8a08c-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a08c-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="8a08c-143">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a08c-143">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
