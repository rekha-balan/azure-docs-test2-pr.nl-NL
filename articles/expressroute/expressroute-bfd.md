---
title: Configure BFD over ExpressRoute | Microsoft Docs
description: This document provides instructions on how to configure BFD over private-peering of an ExpressRoute circuit.
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: ''
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 8/17/2018
ms.author: rambala
ms.openlocfilehash: acac0a866d1f494830be45c23ebca6844431c9de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866873"
---
# <a name="configure-bfd-over-expressroute"></a><span data-ttu-id="3f493-103">Configure BFD over ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3f493-103">Configure BFD over ExpressRoute</span></span>

<span data-ttu-id="3f493-104">ExpressRoute supports Bidirectional Forwarding Detection (BFD) over private peering.</span><span class="sxs-lookup"><span data-stu-id="3f493-104">ExpressRoute supports Bidirectional Forwarding Detection (BFD) over private peering.</span></span> <span data-ttu-id="3f493-105">By enabling BFD over ExpressRoute, you can expedite link failure detection between Microsoft Enterprise edge (MSEE) devices and the routers on which you terminate the ExpressRoute circuit (PE).</span><span class="sxs-lookup"><span data-stu-id="3f493-105">By enabling BFD over ExpressRoute, you can expedite link failure detection between Microsoft Enterprise edge (MSEE) devices and the routers on which you terminate the ExpressRoute circuit (PE).</span></span> <span data-ttu-id="3f493-106">You can terminate ExpressRoute over Customer Edge routing devices or Partner Edge routing devices (if you went with managed Layer 3 connection service).</span><span class="sxs-lookup"><span data-stu-id="3f493-106">You can terminate ExpressRoute over Customer Edge routing devices or Partner Edge routing devices (if you went with managed Layer 3 connection service).</span></span> <span data-ttu-id="3f493-107">This document walks you through the need for BFD, and how to enable BFD over ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3f493-107">This document walks you through the need for BFD, and how to enable BFD over ExpressRoute.</span></span>

## <a name="need-for-bfd"></a><span data-ttu-id="3f493-108">Need for BFD</span><span class="sxs-lookup"><span data-stu-id="3f493-108">Need for BFD</span></span>

<span data-ttu-id="3f493-109">The following diagram shows the benefit of enabling BFD over ExpressRoute circuit: [![1]][1]</span><span class="sxs-lookup"><span data-stu-id="3f493-109">The following diagram shows the benefit of enabling BFD over ExpressRoute circuit: [![1]][1]</span></span>

<span data-ttu-id="3f493-110">You can enable ExpressRoute circuit either by Layer 2 connections or managed Layer 3 connections.</span><span class="sxs-lookup"><span data-stu-id="3f493-110">You can enable ExpressRoute circuit either by Layer 2 connections or managed Layer 3 connections.</span></span> <span data-ttu-id="3f493-111">In either case, if there are one or more Layer-2 devices in the ExpressRoute connection path, responsibility of detecting any link failures in the path lies with the overlying BGP.</span><span class="sxs-lookup"><span data-stu-id="3f493-111">In either case, if there are one or more Layer-2 devices in the ExpressRoute connection path, responsibility of detecting any link failures in the path lies with the overlying BGP.</span></span>

<span data-ttu-id="3f493-112">On the MSEE devices, BGP keepalive and hold-time are typically configured as 60 and 180 seconds respectively.</span><span class="sxs-lookup"><span data-stu-id="3f493-112">On the MSEE devices, BGP keepalive and hold-time are typically configured as 60 and 180 seconds respectively.</span></span> <span data-ttu-id="3f493-113">Therefore, following a link failure it would take up to three minutes to detect any link failure and switch traffic to alternate connection.</span><span class="sxs-lookup"><span data-stu-id="3f493-113">Therefore, following a link failure it would take up to three minutes to detect any link failure and switch traffic to alternate connection.</span></span>

<span data-ttu-id="3f493-114">You can control the BGP timers by configuring lower BGP keepalive and hold-time on the customer edge peering device.</span><span class="sxs-lookup"><span data-stu-id="3f493-114">You can control the BGP timers by configuring lower BGP keepalive and hold-time on the customer edge peering device.</span></span> <span data-ttu-id="3f493-115">If the BGP timers are mismatched between the two peering devices, the BGP session between the peers would use the lower timer value.</span><span class="sxs-lookup"><span data-stu-id="3f493-115">If the BGP timers are mismatched between the two peering devices, the BGP session between the peers would use the lower timer value.</span></span> <span data-ttu-id="3f493-116">The BGP keepalive can be set as low as three seconds, and the hold-time in the order of tens of seconds.</span><span class="sxs-lookup"><span data-stu-id="3f493-116">The BGP keepalive can be set as low as three seconds, and the hold-time in the order of tens of seconds.</span></span> <span data-ttu-id="3f493-117">However, setting BGP timers aggressively less preferable because the protocol is process intensive.</span><span class="sxs-lookup"><span data-stu-id="3f493-117">However, setting BGP timers aggressively less preferable because the protocol is process intensive.</span></span>

<span data-ttu-id="3f493-118">In this scenario, BFD can help.</span><span class="sxs-lookup"><span data-stu-id="3f493-118">In this scenario, BFD can help.</span></span> <span data-ttu-id="3f493-119">BFD provides low-overhead link failure detection in a subsecond time interval.</span><span class="sxs-lookup"><span data-stu-id="3f493-119">BFD provides low-overhead link failure detection in a subsecond time interval.</span></span> 


## <a name="enabling-bfd"></a><span data-ttu-id="3f493-120">Enabling BFD</span><span class="sxs-lookup"><span data-stu-id="3f493-120">Enabling BFD</span></span>

<span data-ttu-id="3f493-121">BFD is configured by default under all the newly created ExpressRoute private peering interfaces on the MSEEs.</span><span class="sxs-lookup"><span data-stu-id="3f493-121">BFD is configured by default under all the newly created ExpressRoute private peering interfaces on the MSEEs.</span></span> <span data-ttu-id="3f493-122">Therefore, to enable BFD, you need to just configure BFD on your PEs.</span><span class="sxs-lookup"><span data-stu-id="3f493-122">Therefore, to enable BFD, you need to just configure BFD on your PEs.</span></span> <span data-ttu-id="3f493-123">Configuring BFD is two-step process: you need configure the BFD on the interface and then link it to the BGP session.</span><span class="sxs-lookup"><span data-stu-id="3f493-123">Configuring BFD is two-step process: you need configure the BFD on the interface and then link it to the BGP session.</span></span>

<span data-ttu-id="3f493-124">An example PE (using Cisco IOS XE) configuration is shown below.</span><span class="sxs-lookup"><span data-stu-id="3f493-124">An example PE (using Cisco IOS XE) configuration is shown below.</span></span> 

    interface TenGigabitEthernet2/0/0.150
      description private peering to Azure
      encapsulation dot1Q 15 second-dot1q 150
      ip vrf forwarding 15
      ip address 192.168.15.17 255.255.255.252
      bfd interval 300 min_rx 300 multiplier 3


    router bgp 65020
      address-family ipv4 vrf 15
        network 10.1.15.0 mask 255.255.255.128
        neighbor 192.168.15.18 remote-as 12076
        neighbor 192.168.15.18 fall-over bfd
        neighbor 192.168.15.18 activate
        neighbor 192.168.15.18 soft-reconfiguration inbound
      exit-address-family

>[!NOTE]
><span data-ttu-id="3f493-125">To enable BFD under an already existing private peering; you need to reset the peering.</span><span class="sxs-lookup"><span data-stu-id="3f493-125">To enable BFD under an already existing private peering; you need to reset the peering.</span></span> <span data-ttu-id="3f493-126">See [Reset ExpressRoute peerings][ResetPeering]</span><span class="sxs-lookup"><span data-stu-id="3f493-126">See [Reset ExpressRoute peerings][ResetPeering]</span></span>
>

## <a name="bfd-timer-negotiation"></a><span data-ttu-id="3f493-127">BFD Timer Negotiation</span><span class="sxs-lookup"><span data-stu-id="3f493-127">BFD Timer Negotiation</span></span>

<span data-ttu-id="3f493-128">Between BFD peers, the slower of the two peers determine the transmission rate.</span><span class="sxs-lookup"><span data-stu-id="3f493-128">Between BFD peers, the slower of the two peers determine the transmission rate.</span></span> <span data-ttu-id="3f493-129">MSEEs BFD transmission/receive intervals are set to 300 milliseconds.</span><span class="sxs-lookup"><span data-stu-id="3f493-129">MSEEs BFD transmission/receive intervals are set to 300 milliseconds.</span></span> <span data-ttu-id="3f493-130">By configuring higher values, you can force these intervals to be longer; but, not shorter.</span><span class="sxs-lookup"><span data-stu-id="3f493-130">By configuring higher values, you can force these intervals to be longer; but, not shorter.</span></span>

>[!NOTE]
><span data-ttu-id="3f493-131">If you have configured Geo-redundant ExpressRoute private peering circuits or use Site-to-Site IPSec VPN connectivity as backup for ExpressRoute private peering; enabling BFD over the private peering would help failover quicker following an ExpressRoute connectivity failure.</span><span class="sxs-lookup"><span data-stu-id="3f493-131">If you have configured Geo-redundant ExpressRoute private peering circuits or use Site-to-Site IPSec VPN connectivity as backup for ExpressRoute private peering; enabling BFD over the private peering would help failover quicker following an ExpressRoute connectivity failure.</span></span> 
>

## <a name="next-steps"></a><span data-ttu-id="3f493-132">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3f493-132">Next Steps</span></span>

<span data-ttu-id="3f493-133">For more information or help, check out the following links:</span><span class="sxs-lookup"><span data-stu-id="3f493-133">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="3f493-134">[Create and modify an ExpressRoute circuit][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="3f493-134">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="3f493-135">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="3f493-135">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-bfd/BFD_Need.png "BFD expedites link failure deduction time"

<!--Link References-->
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[ResetPeering]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-reset-peering






