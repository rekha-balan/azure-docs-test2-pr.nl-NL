---
title: Find next hop with Azure Network Watcher Next Hop - Azure portal | Microsoft Docs
description: This article will describe how you can find what the next hop type is and ip address using Next Hop using the Azure portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 73369b7477fe651ee7b99ce270bc4866b52d7b32
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548779"
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="7872b-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span><span class="sxs-lookup"><span data-stu-id="7872b-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="7872b-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7872b-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="7872b-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span><span class="sxs-lookup"><span data-stu-id="7872b-109">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7872b-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="7872b-110">Before you begin</span></span>

<span data-ttu-id="7872b-111">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="7872b-111">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="7872b-112">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="7872b-112">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="7872b-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="7872b-113">Scenario</span></span>

<span data-ttu-id="7872b-114">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span><span class="sxs-lookup"><span data-stu-id="7872b-114">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="7872b-115">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7872b-115">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="7872b-116">In this scenario, you will:</span><span class="sxs-lookup"><span data-stu-id="7872b-116">In this scenario, you will:</span></span>

* <span data-ttu-id="7872b-117">Retrieve the next hop from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7872b-117">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="7872b-118">Get Next Hop</span><span class="sxs-lookup"><span data-stu-id="7872b-118">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="7872b-119">Step 1</span><span class="sxs-lookup"><span data-stu-id="7872b-119">Step 1</span></span>

<span data-ttu-id="7872b-120">Navigate to your Network Watcher resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7872b-120">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="7872b-121">Step 2</span><span class="sxs-lookup"><span data-stu-id="7872b-121">Step 2</span></span>

<span data-ttu-id="7872b-122">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span><span class="sxs-lookup"><span data-stu-id="7872b-122">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> Next hop requires that the VM resource is allocated to run.

![get next hop overview][1]

### <a name="step-3"></a><span data-ttu-id="7872b-125">Step 3</span><span class="sxs-lookup"><span data-stu-id="7872b-125">Step 3</span></span>

<span data-ttu-id="7872b-126">Once the task is complete, the results are provided.</span><span class="sxs-lookup"><span data-stu-id="7872b-126">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="7872b-127">The IP address and type of device the next hop is, is displayed.</span><span class="sxs-lookup"><span data-stu-id="7872b-127">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="7872b-128">The following table shows the available returned values in the portal.</span><span class="sxs-lookup"><span data-stu-id="7872b-128">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="7872b-129">**Next Hop Type**</span><span class="sxs-lookup"><span data-stu-id="7872b-129">**Next Hop Type**</span></span>

* <span data-ttu-id="7872b-130">Internet</span><span class="sxs-lookup"><span data-stu-id="7872b-130">Internet</span></span>
* <span data-ttu-id="7872b-131">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="7872b-131">VirtualAppliance</span></span>
* <span data-ttu-id="7872b-132">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="7872b-132">VirtualNetworkGateway</span></span>
* <span data-ttu-id="7872b-133">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="7872b-133">VnetLocal</span></span>
* <span data-ttu-id="7872b-134">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="7872b-134">HyperNetGateway</span></span>
* <span data-ttu-id="7872b-135">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="7872b-135">VnetPeering</span></span>
* <span data-ttu-id="7872b-136">None</span><span class="sxs-lookup"><span data-stu-id="7872b-136">None</span></span>

<span data-ttu-id="7872b-137">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span><span class="sxs-lookup"><span data-stu-id="7872b-137">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![get next hop results][2]

## <a name="next-steps"></a><span data-ttu-id="7872b-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="7872b-139">Next steps</span></span>

<span data-ttu-id="7872b-140">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="7872b-140">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-next-hop-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-next-hop-portal/figure2.png
















