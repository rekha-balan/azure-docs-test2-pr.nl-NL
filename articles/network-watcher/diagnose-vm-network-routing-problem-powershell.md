---
title: Diagnose a virtual machine network routing problem - Azure PowerShell | Microsoft Docs
description: In this article, you learn how to diagnose a virtual machine network routing problem using the next hop capability of Azure Network Watcher.
services: network-watcher
documentationcenter: network-watcher
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I need to diagnose virtual machine (VM) network routing problem that prevents communication to different destinations.
ms.assetid: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: network-watcher
ms.workload: infrastructure
ms.date: 04/20/2018
ms.author: jdial
ms.custom: ''
ms.openlocfilehash: f793a201b3fbf57ac2f420c4f4e57a230bc11468
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855766"
---
# <a name="diagnose-a-virtual-machine-network-routing-problem---azure-powershell"></a><span data-ttu-id="88d4c-103">Diagnose a virtual machine network routing problem - Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="88d4c-103">Diagnose a virtual machine network routing problem - Azure PowerShell</span></span>

<span data-ttu-id="88d4c-104">In this article, you deploy a virtual machine (VM), and then check communications to an IP address and URL.</span><span class="sxs-lookup"><span data-stu-id="88d4c-104">In this article, you deploy a virtual machine (VM), and then check communications to an IP address and URL.</span></span> <span data-ttu-id="88d4c-105">You determine the cause of a communication failure and how you can resolve it.</span><span class="sxs-lookup"><span data-stu-id="88d4c-105">You determine the cause of a communication failure and how you can resolve it.</span></span>

<span data-ttu-id="88d4c-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="88d4c-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="88d4c-107">If you choose to install and use PowerShell locally, this article requires the AzureRM PowerShell module version 5.4.1 or later.</span><span class="sxs-lookup"><span data-stu-id="88d4c-107">If you choose to install and use PowerShell locally, this article requires the AzureRM PowerShell module version 5.4.1 or later.</span></span> <span data-ttu-id="88d4c-108">To find the installed version, run `Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="88d4c-108">To find the installed version, run `Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="88d4c-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="88d4c-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="88d4c-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="88d4c-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="88d4c-111">Create a VM</span><span class="sxs-lookup"><span data-stu-id="88d4c-111">Create a VM</span></span>

<span data-ttu-id="88d4c-112">Before you can create a VM, you must create a resource group to contain the VM.</span><span class="sxs-lookup"><span data-stu-id="88d4c-112">Before you can create a VM, you must create a resource group to contain the VM.</span></span> <span data-ttu-id="88d4c-113">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/AzureRM.Resources/New-AzureRmResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="88d4c-113">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/AzureRM.Resources/New-AzureRmResourceGroup).</span></span> <span data-ttu-id="88d4c-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="88d4c-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

<span data-ttu-id="88d4c-115">Create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="88d4c-115">Create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="88d4c-116">When running this step, you are prompted for credentials.</span><span class="sxs-lookup"><span data-stu-id="88d4c-116">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="88d4c-117">The values that you enter are configured as the user name and password for the VM.</span><span class="sxs-lookup"><span data-stu-id="88d4c-117">The values that you enter are configured as the user name and password for the VM.</span></span>

```azurepowershell-interactive
$vM = New-AzureRmVm `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVm" `
    -Location "East US"
```

<span data-ttu-id="88d4c-118">The VM takes a few minutes to create.</span><span class="sxs-lookup"><span data-stu-id="88d4c-118">The VM takes a few minutes to create.</span></span> <span data-ttu-id="88d4c-119">Don't continue with remaining steps until the VM is created and PowerShell returns output.</span><span class="sxs-lookup"><span data-stu-id="88d4c-119">Don't continue with remaining steps until the VM is created and PowerShell returns output.</span></span>

## <a name="test-network-communication"></a><span data-ttu-id="88d4c-120">Test network communication</span><span class="sxs-lookup"><span data-stu-id="88d4c-120">Test network communication</span></span>

<span data-ttu-id="88d4c-121">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's next hop capability to test communication.</span><span class="sxs-lookup"><span data-stu-id="88d4c-121">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's next hop capability to test communication.</span></span>

## <a name="enable-network-watcher"></a><span data-ttu-id="88d4c-122">Enable network watcher</span><span class="sxs-lookup"><span data-stu-id="88d4c-122">Enable network watcher</span></span>

<span data-ttu-id="88d4c-123">If you already have a network watcher enabled in the East US region, use [Get-AzureRmNetworkWatcher](/powershell/module/azurerm.network/get-azurermnetworkwatcher) to retrieve the network watcher.</span><span class="sxs-lookup"><span data-stu-id="88d4c-123">If you already have a network watcher enabled in the East US region, use [Get-AzureRmNetworkWatcher](/powershell/module/azurerm.network/get-azurermnetworkwatcher) to retrieve the network watcher.</span></span> <span data-ttu-id="88d4c-124">The following example retrieves an existing network watcher named *NetworkWatcher_eastus* that is in the *NetworkWatcherRG* resource group:</span><span class="sxs-lookup"><span data-stu-id="88d4c-124">The following example retrieves an existing network watcher named *NetworkWatcher_eastus* that is in the *NetworkWatcherRG* resource group:</span></span>

```azurepowershell-interactive
$networkWatcher = Get-AzureRmNetworkWatcher `
  -Name NetworkWatcher_eastus `
  -ResourceGroupName NetworkWatcherRG
```

<span data-ttu-id="88d4c-125">If you don't already have a network watcher enabled in the East US region, use [New-AzureRmNetworkWatcher](/powershell/module/azurerm.network/new-azurermnetworkwatcher) to create a network watcher in the East US region:</span><span class="sxs-lookup"><span data-stu-id="88d4c-125">If you don't already have a network watcher enabled in the East US region, use [New-AzureRmNetworkWatcher](/powershell/module/azurerm.network/new-azurermnetworkwatcher) to create a network watcher in the East US region:</span></span>

```azurepowershell-interactive
$networkWatcher = New-AzureRmNetworkWatcher `
  -Name "NetworkWatcher_eastus" `
  -ResourceGroupName "NetworkWatcherRG" `
  -Location "East US"
```

### <a name="use-next-hop"></a><span data-ttu-id="88d4c-126">Use next hop</span><span class="sxs-lookup"><span data-stu-id="88d4c-126">Use next hop</span></span>

<span data-ttu-id="88d4c-127">Azure automatically creates routes to default destinations.</span><span class="sxs-lookup"><span data-stu-id="88d4c-127">Azure automatically creates routes to default destinations.</span></span> <span data-ttu-id="88d4c-128">You may create custom routes that override the default routes.</span><span class="sxs-lookup"><span data-stu-id="88d4c-128">You may create custom routes that override the default routes.</span></span> <span data-ttu-id="88d4c-129">Sometimes, custom routes can cause communication to fail.</span><span class="sxs-lookup"><span data-stu-id="88d4c-129">Sometimes, custom routes can cause communication to fail.</span></span> <span data-ttu-id="88d4c-130">To test routing from a VM, use the [Get-AzureRmNetworkWatcherNextHop](/powershell/module/azurerm.network/get-azurermnetworkwatchernexthop) command to determine the next routing hop when traffic is destined for a specific address.</span><span class="sxs-lookup"><span data-stu-id="88d4c-130">To test routing from a VM, use the [Get-AzureRmNetworkWatcherNextHop](/powershell/module/azurerm.network/get-azurermnetworkwatchernexthop) command to determine the next routing hop when traffic is destined for a specific address.</span></span>

<span data-ttu-id="88d4c-131">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span><span class="sxs-lookup"><span data-stu-id="88d4c-131">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span></span>

```azurepowershell-interactive
Get-AzureRmNetworkWatcherNextHop `
  -NetworkWatcher $networkWatcher `
  -TargetVirtualMachineId $VM.Id `
  -SourceIPAddress 192.168.1.4 `
  -DestinationIPAddress 13.107.21.200
```

<span data-ttu-id="88d4c-132">After a few seconds, the output informs you that the **NextHopType** is **Internet**, and that the **RouteTableId** is **System Route**.</span><span class="sxs-lookup"><span data-stu-id="88d4c-132">After a few seconds, the output informs you that the **NextHopType** is **Internet**, and that the **RouteTableId** is **System Route**.</span></span> <span data-ttu-id="88d4c-133">This result lets you know that there is a valid route to the destination.</span><span class="sxs-lookup"><span data-stu-id="88d4c-133">This result lets you know that there is a valid route to the destination.</span></span>

<span data-ttu-id="88d4c-134">Test outbound communication from the VM to 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="88d4c-134">Test outbound communication from the VM to 172.31.0.100:</span></span>

```azurepowershell-interactive
Get-AzureRmNetworkWatcherNextHop `
  -NetworkWatcher $networkWatcher `
  -TargetVirtualMachineId $VM.Id `
  -SourceIPAddress 192.168.1.4 `
  -DestinationIPAddress 172.31.0.100
```

<span data-ttu-id="88d4c-135">The output returned informs you that **None** is the **NextHopType**, and that the **RouteTableId** is also **System Route**.</span><span class="sxs-lookup"><span data-stu-id="88d4c-135">The output returned informs you that **None** is the **NextHopType**, and that the **RouteTableId** is also **System Route**.</span></span> <span data-ttu-id="88d4c-136">This result lets you know that, while there is a valid system route to the destination, there is no next hop to route the traffic to the destination.</span><span class="sxs-lookup"><span data-stu-id="88d4c-136">This result lets you know that, while there is a valid system route to the destination, there is no next hop to route the traffic to the destination.</span></span>

## <a name="view-details-of-a-route"></a><span data-ttu-id="88d4c-137">View details of a route</span><span class="sxs-lookup"><span data-stu-id="88d4c-137">View details of a route</span></span>

<span data-ttu-id="88d4c-138">To analyze routing further, review the effective routes for the network interface with the [Get-AzureRmEffectiveRouteTable](/powershell/module/azurerm.network/get-azurermeffectiveroutetable) command:</span><span class="sxs-lookup"><span data-stu-id="88d4c-138">To analyze routing further, review the effective routes for the network interface with the [Get-AzureRmEffectiveRouteTable](/powershell/module/azurerm.network/get-azurermeffectiveroutetable) command:</span></span>

```azurepowershell-interactive
Get-AzureRmEffectiveRouteTable `
  -NetworkInterfaceName myVm `
  -ResourceGroupName myResourceGroup |
  Format-table
```

<span data-ttu-id="88d4c-139">Output that includes the following text is returned:</span><span class="sxs-lookup"><span data-stu-id="88d4c-139">Output that includes the following text is returned:</span></span>

```powershell
Name State  Source  AddressPrefix           NextHopType NextHopIpAddress
---- -----  ------  -------------           ----------- ----------------
     Active Default {192.168.0.0/16}        VnetLocal   {}              
     Active Default {0.0.0.0/0}             Internet    {}              
     Active Default {10.0.0.0/8}            None        {}              
     Active Default {100.64.0.0/10}         None        {}              
     Active Default {172.16.0.0/12}         None        {}              
```

<span data-ttu-id="88d4c-140">As you can see in the previous output, the route with the **AaddressPrefix** of **0.0.0.0/0** routes all traffic not destined for addresses within other route's address prefixes with a next hop of **Internet**.</span><span class="sxs-lookup"><span data-stu-id="88d4c-140">As you can see in the previous output, the route with the **AaddressPrefix** of **0.0.0.0/0** routes all traffic not destined for addresses within other route's address prefixes with a next hop of **Internet**.</span></span> <span data-ttu-id="88d4c-141">As you can also see in the output, though there is a default route to the 172.16.0.0/12 prefix, which includes the 172.31.0.100 address, the **nextHopType** is **None**.</span><span class="sxs-lookup"><span data-stu-id="88d4c-141">As you can also see in the output, though there is a default route to the 172.16.0.0/12 prefix, which includes the 172.31.0.100 address, the **nextHopType** is **None**.</span></span> <span data-ttu-id="88d4c-142">Azure creates a default route to 172.16.0.0/12, but doesn't specify a next hop type until there is a reason to.</span><span class="sxs-lookup"><span data-stu-id="88d4c-142">Azure creates a default route to 172.16.0.0/12, but doesn't specify a next hop type until there is a reason to.</span></span> <span data-ttu-id="88d4c-143">If, for example, you added the 172.16.0.0/12 address range to the address space of the virtual network, Azure changes the **nextHopType** to **Virtual network** for the route.</span><span class="sxs-lookup"><span data-stu-id="88d4c-143">If, for example, you added the 172.16.0.0/12 address range to the address space of the virtual network, Azure changes the **nextHopType** to **Virtual network** for the route.</span></span> <span data-ttu-id="88d4c-144">A check would then show **Virtual network** as the **nextHopType**.</span><span class="sxs-lookup"><span data-stu-id="88d4c-144">A check would then show **Virtual network** as the **nextHopType**.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="88d4c-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="88d4c-145">Clean up resources</span></span>

<span data-ttu-id="88d4c-146">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="88d4c-146">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="88d4c-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="88d4c-147">Next steps</span></span>

<span data-ttu-id="88d4c-148">In this article, you created a VM and diagnosed network routing from the VM.</span><span class="sxs-lookup"><span data-stu-id="88d4c-148">In this article, you created a VM and diagnosed network routing from the VM.</span></span> <span data-ttu-id="88d4c-149">You learned that Azure creates several default routes and tested routing to two different destinations.</span><span class="sxs-lookup"><span data-stu-id="88d4c-149">You learned that Azure creates several default routes and tested routing to two different destinations.</span></span> <span data-ttu-id="88d4c-150">Learn more about [routing in Azure](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create custom routes](../virtual-network/manage-route-table.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-route).</span><span class="sxs-lookup"><span data-stu-id="88d4c-150">Learn more about [routing in Azure](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create custom routes](../virtual-network/manage-route-table.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-route).</span></span>

<span data-ttu-id="88d4c-151">For outbound VM connections, you can also determine the latency and allowed and denied network traffic between the VM and an endpoint using Network Watcher's [connection troubleshoot](network-watcher-connectivity-powershell.md) capability.</span><span class="sxs-lookup"><span data-stu-id="88d4c-151">For outbound VM connections, you can also determine the latency and allowed and denied network traffic between the VM and an endpoint using Network Watcher's [connection troubleshoot](network-watcher-connectivity-powershell.md) capability.</span></span> <span data-ttu-id="88d4c-152">You can monitor communication between a VM and an endpoint, such as an IP address or URL, over time using the Network Watcher connection monitor capability.</span><span class="sxs-lookup"><span data-stu-id="88d4c-152">You can monitor communication between a VM and an endpoint, such as an IP address or URL, over time using the Network Watcher connection monitor capability.</span></span> <span data-ttu-id="88d4c-153">To learn how, see [Monitor a network connection](connection-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="88d4c-153">To learn how, see [Monitor a network connection](connection-monitor.md).</span></span>