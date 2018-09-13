---
title: Find next hop with Azure Network Watcher Next Hop - Azure CLI | Microsoft Docs
description: This article will describe how you can find what the next hop type is and ip address using Next Hop using Azure CLI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 27872fa3db7571c386b3f269dfe98715d8f7be67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552763"
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli"></a><span data-ttu-id="a9088-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a9088-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)


<span data-ttu-id="a9088-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a9088-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a9088-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span><span class="sxs-lookup"><span data-stu-id="a9088-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="a9088-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="a9088-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="a9088-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="a9088-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a9088-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a9088-112">Before you begin</span></span>

<span data-ttu-id="a9088-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span><span class="sxs-lookup"><span data-stu-id="a9088-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="a9088-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a9088-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="a9088-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="a9088-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a9088-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="a9088-116">Scenario</span></span>

<span data-ttu-id="a9088-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span><span class="sxs-lookup"><span data-stu-id="a9088-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="a9088-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9088-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="a9088-119">Get Next Hop</span><span class="sxs-lookup"><span data-stu-id="a9088-119">Get Next Hop</span></span>

<span data-ttu-id="a9088-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9088-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="a9088-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span><span class="sxs-lookup"><span data-stu-id="a9088-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="a9088-122">In this example, the destination IP address is to a VM in another virtual network.</span><span class="sxs-lookup"><span data-stu-id="a9088-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="a9088-123">There is a virtual network gateway between the two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="a9088-123">There is a virtual network gateway between the two virtual networks.</span></span>

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified. Otherwise it is optional.

## <a name="review-results"></a><span data-ttu-id="a9088-126">Review results</span><span class="sxs-lookup"><span data-stu-id="a9088-126">Review results</span></span>

<span data-ttu-id="a9088-127">When complete, the results are provided.</span><span class="sxs-lookup"><span data-stu-id="a9088-127">When complete, the results are provided.</span></span> <span data-ttu-id="a9088-128">The next hop IP address is returned as well as the type of resource it is.</span><span class="sxs-lookup"><span data-stu-id="a9088-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="a9088-129">The following list shows the currently available NextHopType values:</span><span class="sxs-lookup"><span data-stu-id="a9088-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="a9088-130">**Next Hop Type**</span><span class="sxs-lookup"><span data-stu-id="a9088-130">**Next Hop Type**</span></span>

* <span data-ttu-id="a9088-131">Internet</span><span class="sxs-lookup"><span data-stu-id="a9088-131">Internet</span></span>
* <span data-ttu-id="a9088-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a9088-132">VirtualAppliance</span></span>
* <span data-ttu-id="a9088-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a9088-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a9088-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a9088-134">VnetLocal</span></span>
* <span data-ttu-id="a9088-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a9088-135">HyperNetGateway</span></span>
* <span data-ttu-id="a9088-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a9088-136">VnetPeering</span></span>
* <span data-ttu-id="a9088-137">None</span><span class="sxs-lookup"><span data-stu-id="a9088-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9088-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9088-138">Next steps</span></span>

<span data-ttu-id="a9088-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a9088-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
