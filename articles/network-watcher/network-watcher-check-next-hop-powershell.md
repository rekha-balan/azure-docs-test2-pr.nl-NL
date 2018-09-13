---
title: Find next hop with Azure Network Watcher Next Hop - PowerShell | Microsoft Docs
description: This article will describe how you can find what the next hop type is and ip address using Next Hop using PowerShell.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9f53c824b6368dc2a6251fd880f1cabefef884b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552595"
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="f8778-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8778-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="f8778-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f8778-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="f8778-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span><span class="sxs-lookup"><span data-stu-id="f8778-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f8778-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f8778-110">Before you begin</span></span>

<span data-ttu-id="f8778-111">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span><span class="sxs-lookup"><span data-stu-id="f8778-111">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="f8778-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="f8778-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="f8778-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="f8778-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f8778-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="f8778-114">Scenario</span></span>

<span data-ttu-id="f8778-115">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span><span class="sxs-lookup"><span data-stu-id="f8778-115">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="f8778-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8778-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f8778-117">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f8778-117">Retrieve Network Watcher</span></span>

<span data-ttu-id="f8778-118">The first step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="f8778-118">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f8778-119">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f8778-119">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="f8778-120">Get a virtual machine</span><span class="sxs-lookup"><span data-stu-id="f8778-120">Get a virtual machine</span></span>

<span data-ttu-id="f8778-121">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f8778-121">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="f8778-122">An Id of a virtual machine is required for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f8778-122">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="f8778-123">If you already know the ID of the virtual machine to use, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="f8778-123">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Next hop requires that the VM resource is allocated to run.

## <a name="get-the-network-interfaces"></a><span data-ttu-id="f8778-125">Get the network interfaces</span><span class="sxs-lookup"><span data-stu-id="f8778-125">Get the network interfaces</span></span>

<span data-ttu-id="f8778-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f8778-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="f8778-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="f8778-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkInterfaceIDs.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="f8778-128">Get Next Hop</span><span class="sxs-lookup"><span data-stu-id="f8778-128">Get Next Hop</span></span>

<span data-ttu-id="f8778-129">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f8778-129">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="f8778-130">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span><span class="sxs-lookup"><span data-stu-id="f8778-130">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="f8778-131">In this example, the destination IP address is to a VM in another virtual network.</span><span class="sxs-lookup"><span data-stu-id="f8778-131">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="f8778-132">There is a virtual network gateway between the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="f8778-132">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="f8778-133">Review results</span><span class="sxs-lookup"><span data-stu-id="f8778-133">Review results</span></span>

<span data-ttu-id="f8778-134">When complete, the results are provided.</span><span class="sxs-lookup"><span data-stu-id="f8778-134">When complete, the results are provided.</span></span> <span data-ttu-id="f8778-135">The next hop IP address is returned as well as the type of resource it is.</span><span class="sxs-lookup"><span data-stu-id="f8778-135">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="f8778-136">In this scenario, it is the public IP address of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="f8778-136">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="f8778-137">The following list shows the currently available NextHopType values:</span><span class="sxs-lookup"><span data-stu-id="f8778-137">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="f8778-138">**Next Hop Type**</span><span class="sxs-lookup"><span data-stu-id="f8778-138">**Next Hop Type**</span></span>

* <span data-ttu-id="f8778-139">Internet</span><span class="sxs-lookup"><span data-stu-id="f8778-139">Internet</span></span>
* <span data-ttu-id="f8778-140">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="f8778-140">VirtualAppliance</span></span>
* <span data-ttu-id="f8778-141">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="f8778-141">VirtualNetworkGateway</span></span>
* <span data-ttu-id="f8778-142">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="f8778-142">VnetLocal</span></span>
* <span data-ttu-id="f8778-143">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="f8778-143">HyperNetGateway</span></span>
* <span data-ttu-id="f8778-144">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="f8778-144">VnetPeering</span></span>
* <span data-ttu-id="f8778-145">None</span><span class="sxs-lookup"><span data-stu-id="f8778-145">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8778-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8778-146">Next steps</span></span>

<span data-ttu-id="f8778-147">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f8778-147">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















