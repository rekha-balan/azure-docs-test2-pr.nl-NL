---
title: Azure PowerShell script sample - Route traffic through a network virtual appliance | Microsoft Docs
description: Azure PowerShell script sample - Route traffic through a firewall network virtual appliance.
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
ms.openlocfilehash: 3b3aabed8c74dcb7561d7a40d09af9e3cf17ad8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855666"
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="930dc-103">Route traffic through a network virtual appliance</span><span class="sxs-lookup"><span data-stu-id="930dc-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="930dc-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="930dc-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="930dc-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span><span class="sxs-lookup"><span data-stu-id="930dc-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="930dc-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span><span class="sxs-lookup"><span data-stu-id="930dc-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="930dc-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="930dc-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="930dc-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="930dc-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="930dc-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="930dc-109">Clean up deployment</span></span> 

<span data-ttu-id="930dc-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="930dc-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="930dc-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="930dc-111">Script explanation</span></span>

<span data-ttu-id="930dc-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="930dc-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="930dc-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="930dc-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="930dc-114">Command</span><span class="sxs-lookup"><span data-stu-id="930dc-114">Command</span></span> | <span data-ttu-id="930dc-115">Notes</span><span class="sxs-lookup"><span data-stu-id="930dc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="930dc-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="930dc-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="930dc-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="930dc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="930dc-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="930dc-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="930dc-119">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="930dc-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="930dc-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="930dc-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="930dc-121">Creates back-end and DMZ subnets.</span><span class="sxs-lookup"><span data-stu-id="930dc-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="930dc-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="930dc-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="930dc-123">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="930dc-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="930dc-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="930dc-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="930dc-125">Creates a virtual network interface and enable IP forwarding for it.</span><span class="sxs-lookup"><span data-stu-id="930dc-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="930dc-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="930dc-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="930dc-127">Creates a network security group (NSG).</span><span class="sxs-lookup"><span data-stu-id="930dc-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="930dc-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="930dc-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="930dc-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span><span class="sxs-lookup"><span data-stu-id="930dc-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="930dc-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="930dc-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="930dc-131">Associates the NSGs and route tables to subnets.</span><span class="sxs-lookup"><span data-stu-id="930dc-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="930dc-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="930dc-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="930dc-133">Creates a route table for all routes.</span><span class="sxs-lookup"><span data-stu-id="930dc-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="930dc-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="930dc-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="930dc-135">Creates routes to route traffic between subnets and the Internet through the VM.</span><span class="sxs-lookup"><span data-stu-id="930dc-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="930dc-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="930dc-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="930dc-137">Creates a virtual machine and attaches the NIC to it.</span><span class="sxs-lookup"><span data-stu-id="930dc-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="930dc-138">This command also specifies the virtual machine image to use and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="930dc-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="930dc-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="930dc-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="930dc-140">Deletes a resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="930dc-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="930dc-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="930dc-141">Next steps</span></span>

<span data-ttu-id="930dc-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="930dc-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="930dc-143">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="930dc-143">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
