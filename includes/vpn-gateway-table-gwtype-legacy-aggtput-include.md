---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 6efec75884857d93f2e128104136bf59a1114594
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871383"
---
<span data-ttu-id="658d1-103">The following table shows the gateway types and the estimated aggregate throughput by gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="658d1-103">The following table shows the gateway types and the estimated aggregate throughput by gateway SKU.</span></span> <span data-ttu-id="658d1-104">This table applies to the Resource Manager and classic deployment models.</span><span class="sxs-lookup"><span data-stu-id="658d1-104">This table applies to the Resource Manager and classic deployment models.</span></span> 

<span data-ttu-id="658d1-105">Pricing differs between gateway SKUs.</span><span class="sxs-lookup"><span data-stu-id="658d1-105">Pricing differs between gateway SKUs.</span></span> <span data-ttu-id="658d1-106">For more information, see [VPN Gateway Pricing](https://azure.microsoft.com/pricing/details/vpn-gateway).</span><span class="sxs-lookup"><span data-stu-id="658d1-106">For more information, see [VPN Gateway Pricing](https://azure.microsoft.com/pricing/details/vpn-gateway).</span></span>

<span data-ttu-id="658d1-107">Note that the UltraPerformance gateway SKU is not represented in this table.</span><span class="sxs-lookup"><span data-stu-id="658d1-107">Note that the UltraPerformance gateway SKU is not represented in this table.</span></span> <span data-ttu-id="658d1-108">For information about the UltraPerformance SKU, see the [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="658d1-108">For information about the UltraPerformance SKU, see the [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.</span></span>

|  | <span data-ttu-id="658d1-109">**VPN Gateway throughput (1)**</span><span class="sxs-lookup"><span data-stu-id="658d1-109">**VPN Gateway throughput (1)**</span></span> | <span data-ttu-id="658d1-110">**VPN Gateway max IPsec tunnels (2)**</span><span class="sxs-lookup"><span data-stu-id="658d1-110">**VPN Gateway max IPsec tunnels (2)**</span></span> | <span data-ttu-id="658d1-111">**ExpressRoute Gateway throughput**</span><span class="sxs-lookup"><span data-stu-id="658d1-111">**ExpressRoute Gateway throughput**</span></span> | <span data-ttu-id="658d1-112">**VPN Gateway and ExpressRoute coexist**</span><span class="sxs-lookup"><span data-stu-id="658d1-112">**VPN Gateway and ExpressRoute coexist**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="658d1-113">**Basic SKU (3)(5)(6)**</span><span class="sxs-lookup"><span data-stu-id="658d1-113">**Basic SKU (3)(5)(6)**</span></span> |<span data-ttu-id="658d1-114">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="658d1-114">100 Mbps</span></span> |<span data-ttu-id="658d1-115">10</span><span class="sxs-lookup"><span data-stu-id="658d1-115">10</span></span> |<span data-ttu-id="658d1-116">500 Mbps (6)</span><span class="sxs-lookup"><span data-stu-id="658d1-116">500 Mbps (6)</span></span> |<span data-ttu-id="658d1-117">No</span><span class="sxs-lookup"><span data-stu-id="658d1-117">No</span></span> |
| <span data-ttu-id="658d1-118">**Standard SKU (4)(5)**</span><span class="sxs-lookup"><span data-stu-id="658d1-118">**Standard SKU (4)(5)**</span></span> |<span data-ttu-id="658d1-119">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="658d1-119">100 Mbps</span></span> |<span data-ttu-id="658d1-120">10</span><span class="sxs-lookup"><span data-stu-id="658d1-120">10</span></span> |<span data-ttu-id="658d1-121">1000 Mbps</span><span class="sxs-lookup"><span data-stu-id="658d1-121">1000 Mbps</span></span> |<span data-ttu-id="658d1-122">Yes</span><span class="sxs-lookup"><span data-stu-id="658d1-122">Yes</span></span> |
| <span data-ttu-id="658d1-123">**High Performance SKU (4)**</span><span class="sxs-lookup"><span data-stu-id="658d1-123">**High Performance SKU (4)**</span></span> |<span data-ttu-id="658d1-124">200 Mbps</span><span class="sxs-lookup"><span data-stu-id="658d1-124">200 Mbps</span></span> |<span data-ttu-id="658d1-125">30</span><span class="sxs-lookup"><span data-stu-id="658d1-125">30</span></span> |<span data-ttu-id="658d1-126">2000 Mbps</span><span class="sxs-lookup"><span data-stu-id="658d1-126">2000 Mbps</span></span> |<span data-ttu-id="658d1-127">Yes</span><span class="sxs-lookup"><span data-stu-id="658d1-127">Yes</span></span> |


<span data-ttu-id="658d1-128">(1) The VPN throughput is a rough estimate based on the measurements between VNets in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="658d1-128">(1) The VPN throughput is a rough estimate based on the measurements between VNets in the same Azure region.</span></span> <span data-ttu-id="658d1-129">It is not a guaranteed throughput for cross-premises connections across the Internet.</span><span class="sxs-lookup"><span data-stu-id="658d1-129">It is not a guaranteed throughput for cross-premises connections across the Internet.</span></span> <span data-ttu-id="658d1-130">It is the maximum possible throughput measurement.</span><span class="sxs-lookup"><span data-stu-id="658d1-130">It is the maximum possible throughput measurement.</span></span>

<span data-ttu-id="658d1-131">(2) The number of tunnels refer to RouteBased VPNs.</span><span class="sxs-lookup"><span data-stu-id="658d1-131">(2) The number of tunnels refer to RouteBased VPNs.</span></span> <span data-ttu-id="658d1-132">A PolicyBased VPN can only support one Site-to-Site VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="658d1-132">A PolicyBased VPN can only support one Site-to-Site VPN tunnel.</span></span>

<span data-ttu-id="658d1-133">(3) BGP is not supported for the Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="658d1-133">(3) BGP is not supported for the Basic SKU.</span></span>

<span data-ttu-id="658d1-134">(4) PolicyBased VPNs are not supported for this SKU.</span><span class="sxs-lookup"><span data-stu-id="658d1-134">(4) PolicyBased VPNs are not supported for this SKU.</span></span> <span data-ttu-id="658d1-135">They are supported for the Basic SKU only.</span><span class="sxs-lookup"><span data-stu-id="658d1-135">They are supported for the Basic SKU only.</span></span>

<span data-ttu-id="658d1-136">(5) Active-active S2S VPN Gateway connections are not supported for this SKU.</span><span class="sxs-lookup"><span data-stu-id="658d1-136">(5) Active-active S2S VPN Gateway connections are not supported for this SKU.</span></span> <span data-ttu-id="658d1-137">Active-active is supported on the HighPerformance SKU only.</span><span class="sxs-lookup"><span data-stu-id="658d1-137">Active-active is supported on the HighPerformance SKU only.</span></span>

<span data-ttu-id="658d1-138">(6) Basic SKU is deprecated for use with ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="658d1-138">(6) Basic SKU is deprecated for use with ExpressRoute.</span></span>
