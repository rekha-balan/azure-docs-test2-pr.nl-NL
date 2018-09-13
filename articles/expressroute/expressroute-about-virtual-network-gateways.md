---
title: About Azure ExpressRoute virtual network gateways| Microsoft Docs
description: Learn about virtual network gateways for ExpressRoute.
services: expressroute
author: cherylmc
ms.service: expressroute
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: cherylmc
ms.openlocfilehash: 34d84a27406f0ebabd7bca576ee443da1d0c9bcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800025"
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="a24e7-103">About virtual network gateways for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a24e7-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="a24e7-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span><span class="sxs-lookup"><span data-stu-id="a24e7-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="a24e7-105">You can use a virtual network gateway can be used for either ExpressRoute traffic, or VPN traffic.</span><span class="sxs-lookup"><span data-stu-id="a24e7-105">You can use a virtual network gateway can be used for either ExpressRoute traffic, or VPN traffic.</span></span> <span data-ttu-id="a24e7-106">This article focuses on ExpressRoute virtual network gateways.</span><span class="sxs-lookup"><span data-stu-id="a24e7-106">This article focuses on ExpressRoute virtual network gateways.</span></span>

## <a name="gateway-types"></a><span data-ttu-id="a24e7-107">Gateway types</span><span class="sxs-lookup"><span data-stu-id="a24e7-107">Gateway types</span></span>

<span data-ttu-id="a24e7-108">When you create a virtual network gateway, you specify several settings.</span><span class="sxs-lookup"><span data-stu-id="a24e7-108">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="a24e7-109">One of the required settings, '-GatewayType', specifies whether the gateway is used for ExpressRoute, or VPN traffic.</span><span class="sxs-lookup"><span data-stu-id="a24e7-109">One of the required settings, '-GatewayType', specifies whether the gateway is used for ExpressRoute, or VPN traffic.</span></span> <span data-ttu-id="a24e7-110">The two gateway types are:</span><span class="sxs-lookup"><span data-stu-id="a24e7-110">The two gateway types are:</span></span> 

* <span data-ttu-id="a24e7-111">**Vpn** - To send encrypted traffic across the public Internet, you use the gateway type 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="a24e7-111">**Vpn** - To send encrypted traffic across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="a24e7-112">This is also referred to as a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="a24e7-112">This is also referred to as a VPN gateway.</span></span> <span data-ttu-id="a24e7-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="a24e7-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

* <span data-ttu-id="a24e7-114">**ExpressRoute** - To send network traffic on a private connection, you use the gateway type 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="a24e7-114">**ExpressRoute** - To send network traffic on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="a24e7-115">This is also referred to as an ExpressRoute gateway and is the type of gateway that you use when configuring ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a24e7-115">This is also referred to as an ExpressRoute gateway and is the type of gateway that you use when configuring ExpressRoute.</span></span>


<span data-ttu-id="a24e7-116">Each virtual network can have only one virtual network gateway per gateway type.</span><span class="sxs-lookup"><span data-stu-id="a24e7-116">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="a24e7-117">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a24e7-117">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span>

## <a name="gwsku"></a><span data-ttu-id="a24e7-118">Gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="a24e7-118">Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="a24e7-119">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a24e7-119">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="a24e7-120">This will work for upgrades to Standard and HighPerformance SKUs.</span><span class="sxs-lookup"><span data-stu-id="a24e7-120">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="a24e7-121">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span><span class="sxs-lookup"><span data-stu-id="a24e7-121">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span> <span data-ttu-id="a24e7-122">Recreating a gateway incurs downtime.</span><span class="sxs-lookup"><span data-stu-id="a24e7-122">Recreating a gateway incurs downtime.</span></span>

### <a name="aggthroughput"></a><span data-ttu-id="a24e7-123">Estimated performances by gateway SKU</span><span class="sxs-lookup"><span data-stu-id="a24e7-123">Estimated performances by gateway SKU</span></span>
<span data-ttu-id="a24e7-124">The following table shows the gateway types and the estimated performances.</span><span class="sxs-lookup"><span data-stu-id="a24e7-124">The following table shows the gateway types and the estimated performances.</span></span> <span data-ttu-id="a24e7-125">This table applies to both the Resource Manager and classic deployment models.</span><span class="sxs-lookup"><span data-stu-id="a24e7-125">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a24e7-126">Application performance depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span><span class="sxs-lookup"><span data-stu-id="a24e7-126">Application performance depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="a24e7-127">The numbers in the table represent the upper limit that the application can theoretically achieve in an ideal environment.</span><span class="sxs-lookup"><span data-stu-id="a24e7-127">The numbers in the table represent the upper limit that the application can theoretically achieve in an ideal environment.</span></span> 
> 
>

### <a name="zrgw"></a><span data-ttu-id="a24e7-128">Zone-redundant gateway SKUs (Preview)</span><span class="sxs-lookup"><span data-stu-id="a24e7-128">Zone-redundant gateway SKUs (Preview)</span></span>

<span data-ttu-id="a24e7-129">You can also deploy ExpressRoute gateways in Azure Availability Zones.</span><span class="sxs-lookup"><span data-stu-id="a24e7-129">You can also deploy ExpressRoute gateways in Azure Availability Zones.</span></span> <span data-ttu-id="a24e7-130">This physically and logically separates them into different Availability Zones, protecting your on-premises network connectivity to Azure from zone-level failures.</span><span class="sxs-lookup"><span data-stu-id="a24e7-130">This physically and logically separates them into different Availability Zones, protecting your on-premises network connectivity to Azure from zone-level failures.</span></span>

![Zone-redundant ExpressRoute gateway](./media/expressroute-about-virtual-network-gateways/zone-redundant.png)

<span data-ttu-id="a24e7-132">Zone-redundant gateways use specific new gateway SKUs for ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="a24e7-132">Zone-redundant gateways use specific new gateway SKUs for ExpressRoute gateway.</span></span> <span data-ttu-id="a24e7-133">The new SKUs are currently available in **Public Preview**.</span><span class="sxs-lookup"><span data-stu-id="a24e7-133">The new SKUs are currently available in **Public Preview**.</span></span>

* <span data-ttu-id="a24e7-134">ErGw1AZ</span><span class="sxs-lookup"><span data-stu-id="a24e7-134">ErGw1AZ</span></span>
* <span data-ttu-id="a24e7-135">ErGw2AZ</span><span class="sxs-lookup"><span data-stu-id="a24e7-135">ErGw2AZ</span></span>
* <span data-ttu-id="a24e7-136">ErGw3AZ</span><span class="sxs-lookup"><span data-stu-id="a24e7-136">ErGw3AZ</span></span>

<span data-ttu-id="a24e7-137">The new gateway SKUs also support other deployment options to best match your needs.</span><span class="sxs-lookup"><span data-stu-id="a24e7-137">The new gateway SKUs also support other deployment options to best match your needs.</span></span> <span data-ttu-id="a24e7-138">When creating a virtual network gateway using the new gateway SKUs, you also have the option to deploy the gateway in a specific zone.</span><span class="sxs-lookup"><span data-stu-id="a24e7-138">When creating a virtual network gateway using the new gateway SKUs, you also have the option to deploy the gateway in a specific zone.</span></span> <span data-ttu-id="a24e7-139">This is referred to as a zonal gateway.</span><span class="sxs-lookup"><span data-stu-id="a24e7-139">This is referred to as a zonal gateway.</span></span> <span data-ttu-id="a24e7-140">When you deploy a zonal gateway, all the instances of the gateway are deployed in the same Availability Zone.</span><span class="sxs-lookup"><span data-stu-id="a24e7-140">When you deploy a zonal gateway, all the instances of the gateway are deployed in the same Availability Zone.</span></span> <span data-ttu-id="a24e7-141">To enroll in the Preview, see [Create a zone-redundant virtual network gateway](../../articles/vpn-gateway/create-zone-redundant-vnet-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a24e7-141">To enroll in the Preview, see [Create a zone-redundant virtual network gateway](../../articles/vpn-gateway/create-zone-redundant-vnet-gateway.md).</span></span>

## <a name="resources"></a><span data-ttu-id="a24e7-142">REST APIs and PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="a24e7-142">REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="a24e7-143">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span><span class="sxs-lookup"><span data-stu-id="a24e7-143">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="a24e7-144">**Classic**</span><span class="sxs-lookup"><span data-stu-id="a24e7-144">**Classic**</span></span> | <span data-ttu-id="a24e7-145">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="a24e7-145">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="a24e7-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a24e7-146">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="a24e7-147">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a24e7-147">PowerShell</span></span>](https://docs.microsoft.com/powershell/module/azurerm.network#networking) |
| [<span data-ttu-id="a24e7-148">REST API</span><span class="sxs-lookup"><span data-stu-id="a24e7-148">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="a24e7-149">REST API</span><span class="sxs-lookup"><span data-stu-id="a24e7-149">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="a24e7-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="a24e7-150">Next steps</span></span>
<span data-ttu-id="a24e7-151">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span><span class="sxs-lookup"><span data-stu-id="a24e7-151">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span>

<span data-ttu-id="a24e7-152">See [Create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md) for more information about creating ExpressRoute gateways.</span><span class="sxs-lookup"><span data-stu-id="a24e7-152">See [Create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md) for more information about creating ExpressRoute gateways.</span></span>
