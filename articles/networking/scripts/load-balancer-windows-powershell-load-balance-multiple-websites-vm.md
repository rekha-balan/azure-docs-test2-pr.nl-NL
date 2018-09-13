---
title: Azure PowerShell Script Sample - Load balance multiple websites with Azure PowerShell | Microsoft Docs
description: Azure PowerShell Script Sample - Load balance multiple websites to the same virtual machine
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 44cb76a09cdaacd1bffd653bae6a5735a81dc6f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868848"
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="583ed-103">Load balance multiple websites</span><span class="sxs-lookup"><span data-stu-id="583ed-103">Load balance multiple websites</span></span>

<span data-ttu-id="583ed-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span><span class="sxs-lookup"><span data-stu-id="583ed-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="583ed-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span><span class="sxs-lookup"><span data-stu-id="583ed-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="583ed-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span><span class="sxs-lookup"><span data-stu-id="583ed-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="583ed-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="583ed-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="583ed-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="583ed-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="583ed-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="583ed-109">Clean up deployment</span></span> 

<span data-ttu-id="583ed-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="583ed-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="583ed-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="583ed-111">Script explanation</span></span>

<span data-ttu-id="583ed-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="583ed-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="583ed-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="583ed-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="583ed-114">Command</span><span class="sxs-lookup"><span data-stu-id="583ed-114">Command</span></span> | <span data-ttu-id="583ed-115">Notes</span><span class="sxs-lookup"><span data-stu-id="583ed-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="583ed-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="583ed-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="583ed-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="583ed-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="583ed-118">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="583ed-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="583ed-119">Creates an Azure availability set to provide high availability.</span><span class="sxs-lookup"><span data-stu-id="583ed-119">Creates an Azure availability set to provide high availability.</span></span> |
| [<span data-ttu-id="583ed-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="583ed-121">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="583ed-121">Creates a subnet configuration.</span></span> <span data-ttu-id="583ed-122">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="583ed-122">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="583ed-123">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="583ed-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="583ed-124">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="583ed-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="583ed-125">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="583ed-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="583ed-126">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="583ed-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="583ed-127">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="583ed-128">Creates a front end IP config for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="583ed-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="583ed-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="583ed-130">Creates a backend address pool configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="583ed-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="583ed-131">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="583ed-132">Creates an NLB probe.</span><span class="sxs-lookup"><span data-stu-id="583ed-132">Creates an NLB probe.</span></span> <span data-ttu-id="583ed-133">An NLB probe is used to monitor each VM in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="583ed-133">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="583ed-134">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="583ed-134">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="583ed-135">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="583ed-136">Creates an NLB rule.</span><span class="sxs-lookup"><span data-stu-id="583ed-136">Creates an NLB rule.</span></span> <span data-ttu-id="583ed-137">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="583ed-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="583ed-138">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="583ed-138">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="583ed-139">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="583ed-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="583ed-140">Creates a load balancer.</span><span class="sxs-lookup"><span data-stu-id="583ed-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="583ed-141">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="583ed-142">Defines advanced features for a virtual network interface.</span><span class="sxs-lookup"><span data-stu-id="583ed-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="583ed-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="583ed-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="583ed-144">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="583ed-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="583ed-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="583ed-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="583ed-146">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="583ed-146">Creates a VM configuration.</span></span> <span data-ttu-id="583ed-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="583ed-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="583ed-148">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="583ed-148">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="583ed-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="583ed-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="583ed-150">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="583ed-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="583ed-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="583ed-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="583ed-152">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="583ed-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="583ed-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="583ed-153">Next steps</span></span>

<span data-ttu-id="583ed-154">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="583ed-154">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="583ed-155">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="583ed-155">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
