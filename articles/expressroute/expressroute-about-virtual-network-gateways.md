---
title: About ExpressRoute virtual network gateways| Microsoft Docs
description: Learn about virtual network gateways for ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: ''
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: cherylmc
ms.openlocfilehash: b58a8f7f87a231bd44c9224e3c889c31336ee0b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563203"
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="481b4-103">About virtual network gateways for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="481b4-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="481b4-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span><span class="sxs-lookup"><span data-stu-id="481b4-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="481b4-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span><span class="sxs-lookup"><span data-stu-id="481b4-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="481b4-106">When you create a virtual network gateway, you specify several settings.</span><span class="sxs-lookup"><span data-stu-id="481b4-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="481b4-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span><span class="sxs-lookup"><span data-stu-id="481b4-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="481b4-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="481b4-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="481b4-109">When network traffic is sent on a dedicated private connection, you use the gateway type 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="481b4-109">When network traffic is sent on a dedicated private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="481b4-110">This is also referred to as an ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="481b4-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="481b4-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="481b4-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="481b4-112">This is referred to as a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="481b4-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="481b4-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="481b4-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span> 

<span data-ttu-id="481b4-114">Each virtual network can have only one virtual network gateway per gateway type.</span><span class="sxs-lookup"><span data-stu-id="481b4-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="481b4-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="481b4-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="481b4-116">This article focuses on the ExpressRoute virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="481b4-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <a name="gwsku"></a><span data-ttu-id="481b4-117">Gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="481b4-117">Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="481b4-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="481b4-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="481b4-119">This will work for upgrades to Standard and HighPerformance SKUs.</span><span class="sxs-lookup"><span data-stu-id="481b4-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="481b4-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span><span class="sxs-lookup"><span data-stu-id="481b4-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <a name="aggthroughput"></a><span data-ttu-id="481b4-121">Estimated aggregate throughput by gateway SKU</span><span class="sxs-lookup"><span data-stu-id="481b4-121">Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="481b4-122">The following table shows the gateway types and the estimated aggregate throughput.</span><span class="sxs-lookup"><span data-stu-id="481b4-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="481b4-123">This table applies to both the Resource Manager and classic deployment models.</span><span class="sxs-lookup"><span data-stu-id="481b4-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="481b4-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span><span class="sxs-lookup"><span data-stu-id="481b4-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="481b4-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span><span class="sxs-lookup"><span data-stu-id="481b4-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <a name="resources"></a><span data-ttu-id="481b4-126">REST APIs and PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="481b4-126">REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="481b4-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span><span class="sxs-lookup"><span data-stu-id="481b4-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="481b4-128">**Classic**</span><span class="sxs-lookup"><span data-stu-id="481b4-128">**Classic**</span></span> | <span data-ttu-id="481b4-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="481b4-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="481b4-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="481b4-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="481b4-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="481b4-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="481b4-132">REST API</span><span class="sxs-lookup"><span data-stu-id="481b4-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="481b4-133">REST API</span><span class="sxs-lookup"><span data-stu-id="481b4-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="481b4-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="481b4-134">Next steps</span></span>
<span data-ttu-id="481b4-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span><span class="sxs-lookup"><span data-stu-id="481b4-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

