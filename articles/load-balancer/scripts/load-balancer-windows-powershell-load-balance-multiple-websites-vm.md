---
title: PowerShell Example - Load balance multiple websites with Azure PowerShell | Microsoft Docs
description: This Azure PowerShell script example hows how to load balance multiple websites to the same virtual machine
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: jeconnoc
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 04/20/2018
ms.author: kumud
ms.openlocfilehash: f0058c8c4c4b170b12d2e888073aa0c731e87725
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869610"
---
# <a name="azure-powershell-script-example-load-balance-multiple-websites"></a><span data-ttu-id="9dd4a-103">Azure PowerShell script example: Load balance multiple websites</span><span class="sxs-lookup"><span data-stu-id="9dd4a-103">Azure PowerShell script example: Load balance multiple websites</span></span>

<span data-ttu-id="9dd4a-104">This Azure PowerShell script example creates a virtual network with two virtual machines (VM) that are members of an availability set.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-104">This Azure PowerShell script example creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="9dd4a-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="9dd4a-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="9dd4a-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9dd4a-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="9dd4a-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9dd4a-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9dd4a-109">Clean up deployment</span></span> 

<span data-ttu-id="9dd4a-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9dd4a-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9dd4a-111">Script explanation</span></span>

<span data-ttu-id="9dd4a-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="9dd4a-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9dd4a-114">Command</span><span class="sxs-lookup"><span data-stu-id="9dd4a-114">Command</span></span> | <span data-ttu-id="9dd4a-115">Notes</span><span class="sxs-lookup"><span data-stu-id="9dd4a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9dd4a-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9dd4a-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9dd4a-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9dd4a-118">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="9dd4a-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="9dd4a-119">Creates an Azure availability set to provide high availability.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-119">Creates an Azure availability set to provide high availability.</span></span> |
| [<span data-ttu-id="9dd4a-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9dd4a-121">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-121">Creates a subnet configuration.</span></span> <span data-ttu-id="9dd4a-122">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-122">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="9dd4a-123">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9dd4a-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9dd4a-124">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9dd4a-125">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9dd4a-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9dd4a-126">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9dd4a-127">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="9dd4a-128">Creates a front end IP config for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="9dd4a-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="9dd4a-130">Creates a backend address pool configuration for a load balancer.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9dd4a-131">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="9dd4a-132">Creates an NLB probe.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-132">Creates an NLB probe.</span></span> <span data-ttu-id="9dd4a-133">An NLB probe is used to monitor each VM in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-133">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="9dd4a-134">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-134">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="9dd4a-135">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="9dd4a-136">Creates an NLB rule.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-136">Creates an NLB rule.</span></span> <span data-ttu-id="9dd4a-137">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="9dd4a-138">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-138">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="9dd4a-139">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="9dd4a-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="9dd4a-140">Creates a load balancer.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="9dd4a-141">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="9dd4a-142">Defines advanced features for a virtual network interface.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="9dd4a-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9dd4a-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9dd4a-144">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="9dd4a-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9dd4a-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9dd4a-146">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-146">Creates a VM configuration.</span></span> <span data-ttu-id="9dd4a-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9dd4a-148">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-148">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9dd4a-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9dd4a-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9dd4a-150">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="9dd4a-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9dd4a-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9dd4a-152">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="9dd4a-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9dd4a-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="9dd4a-153">Next steps</span></span>

<span data-ttu-id="9dd4a-154">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9dd4a-154">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9dd4a-155">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9dd4a-155">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
