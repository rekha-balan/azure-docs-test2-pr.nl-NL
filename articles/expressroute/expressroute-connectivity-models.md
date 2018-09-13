---
title: 'ExpressRoute connectivity models: Connect to Microsoft Azure through network service providers, exchanges, and Ethernet providers | Microsoft Docs'
description: This article describes the different modes of connectivity between the customer's network and Microsoft Azure, Office 365 and Dynamics 365 services. Customers can use MPLS providers, cloud exchanges and Ethernet providers.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: ''
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: c6c3fe06942e40e56a0e0738301345076c7d4390
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550846"
---
# <a name="expressroute-connectivity-models"></a><span data-ttu-id="7c8c7-104">ExpressRoute connectivity models</span><span class="sxs-lookup"><span data-stu-id="7c8c7-104">ExpressRoute connectivity models</span></span>
<span data-ttu-id="7c8c7-105">You can create a connection between your on-premises network and the Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span><span class="sxs-lookup"><span data-stu-id="7c8c7-105">You can create a connection between your on-premises network and the Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span></span> <span data-ttu-id="7c8c7-106">Connectivity providers can offer one or more connectivity models.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-106">Connectivity providers can offer one or more connectivity models.</span></span> <span data-ttu-id="7c8c7-107">You can work with your connectivity provider to pick the model that works best for you.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-107">You can work with your connectivity provider to pick the model that works best for you.</span></span>
<br><br>

![ExpressRoute connectivity model diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a><span data-ttu-id="7c8c7-109">Co-located at a cloud exchange</span><span class="sxs-lookup"><span data-stu-id="7c8c7-109">Co-located at a cloud exchange</span></span>
<span data-ttu-id="7c8c7-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections to the Microsoft cloud through the co-location provider’s Ethernet exchange.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections to the Microsoft cloud through the co-location provider’s Ethernet exchange.</span></span> <span data-ttu-id="7c8c7-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in the co-location facility and the Microsoft cloud.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in the co-location facility and the Microsoft cloud.</span></span>

## <a name="Ethernet"></a><span data-ttu-id="7c8c7-112">Point-to-point Ethernet connections</span><span class="sxs-lookup"><span data-stu-id="7c8c7-112">Point-to-point Ethernet connections</span></span>
<span data-ttu-id="7c8c7-113">You can connect your on-premises datacenters/offices to the Microsoft cloud through point-to-point Ethernet links.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-113">You can connect your on-premises datacenters/offices to the Microsoft cloud through point-to-point Ethernet links.</span></span> <span data-ttu-id="7c8c7-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and the Microsoft cloud.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and the Microsoft cloud.</span></span>

## <a name="IPVPN"></a><span data-ttu-id="7c8c7-115">Any-to-any (IPVPN) networks</span><span class="sxs-lookup"><span data-stu-id="7c8c7-115">Any-to-any (IPVPN) networks</span></span>
<span data-ttu-id="7c8c7-116">You can integrate your WAN with the Microsoft cloud.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-116">You can integrate your WAN with the Microsoft cloud.</span></span> <span data-ttu-id="7c8c7-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span></span> <span data-ttu-id="7c8c7-118">The Microsoft cloud can be interconnected to your WAN to make it look just like any other branch office.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-118">The Microsoft cloud can be interconnected to your WAN to make it look just like any other branch office.</span></span> <span data-ttu-id="7c8c7-119">WAN providers typically offer managed Layer 3 connectivity.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-119">WAN providers typically offer managed Layer 3 connectivity.</span></span> <span data-ttu-id="7c8c7-120">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-120">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c8c7-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c8c7-121">Next steps</span></span>
* <span data-ttu-id="7c8c7-122">Learn about ExpressRoute connections and routing domains.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-122">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="7c8c7-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="7c8c7-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="7c8c7-124">Learn about ExpressRoute features.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-124">Learn about ExpressRoute features.</span></span> <span data-ttu-id="7c8c7-125">See the [ExpressRoute Technical Overview](expressroute-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7c8c7-125">See the [ExpressRoute Technical Overview](expressroute-introduction.md)</span></span>
* <span data-ttu-id="7c8c7-126">Find a service provider.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-126">Find a service provider.</span></span> <span data-ttu-id="7c8c7-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span><span class="sxs-lookup"><span data-stu-id="7c8c7-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="7c8c7-128">Ensure that all prerequisites are met.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-128">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="7c8c7-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7c8c7-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="7c8c7-130">Refer to the requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span><span class="sxs-lookup"><span data-stu-id="7c8c7-130">Refer to the requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="7c8c7-131">Configure your ExpressRoute connection.</span><span class="sxs-lookup"><span data-stu-id="7c8c7-131">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="7c8c7-132">Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="7c8c7-132">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="7c8c7-133">Configure routing</span><span class="sxs-lookup"><span data-stu-id="7c8c7-133">Configure routing</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="7c8c7-134">Link a VNet to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="7c8c7-134">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
