---
title: Overview of BGP with Azure VPN Gateways | Microsoft Docs
description: This article provides an overview of BGP with Azure VPN Gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: ''
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: 13a17eb3d78e70a09864bf218f1027d6e98486a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782670"
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="fc360-103">Overview of BGP with Azure VPN Gateways</span><span class="sxs-lookup"><span data-stu-id="fc360-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="fc360-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span><span class="sxs-lookup"><span data-stu-id="fc360-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="fc360-105">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span><span class="sxs-lookup"><span data-stu-id="fc360-105">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="fc360-106">When used in the context of Azure Virtual Networks, BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span><span class="sxs-lookup"><span data-stu-id="fc360-106">When used in the context of Azure Virtual Networks, BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="fc360-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span><span class="sxs-lookup"><span data-stu-id="fc360-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span> 

## <a name="why"></a><span data-ttu-id="fc360-108">Why use BGP?</span><span class="sxs-lookup"><span data-stu-id="fc360-108">Why use BGP?</span></span>
<span data-ttu-id="fc360-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="fc360-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="fc360-110">You should also make sure your on-premises VPN devices support BGP before you enable the feature.</span><span class="sxs-lookup"><span data-stu-id="fc360-110">You should also make sure your on-premises VPN devices support BGP before you enable the feature.</span></span> <span data-ttu-id="fc360-111">You can continue to use Azure VPN gateways and your on-premises VPN devices without BGP.</span><span class="sxs-lookup"><span data-stu-id="fc360-111">You can continue to use Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="fc360-112">It is the equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span><span class="sxs-lookup"><span data-stu-id="fc360-112">It is the equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="fc360-113">There are several advantages and new capabilities with BGP:</span><span class="sxs-lookup"><span data-stu-id="fc360-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="prefix"></a><span data-ttu-id="fc360-114">Support automatic and flexible prefix updates</span><span class="sxs-lookup"><span data-stu-id="fc360-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="fc360-115">With BGP, you only need to declare a minimum prefix to a specific BGP peer over the IPsec S2S VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="fc360-115">With BGP, you only need to declare a minimum prefix to a specific BGP peer over the IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="fc360-116">It can be as small as a host prefix (/32) of the BGP peer IP address of your on-premises VPN device.</span><span class="sxs-lookup"><span data-stu-id="fc360-116">It can be as small as a host prefix (/32) of the BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="fc360-117">You can control which on-premises network prefixes you want to advertise to Azure to allow your Azure Virtual Network to access.</span><span class="sxs-lookup"><span data-stu-id="fc360-117">You can control which on-premises network prefixes you want to advertise to Azure to allow your Azure Virtual Network to access.</span></span>

<span data-ttu-id="fc360-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span><span class="sxs-lookup"><span data-stu-id="fc360-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="fc360-119">Note though the prefixes cannot be identical with any one of your VNet prefixes.</span><span class="sxs-lookup"><span data-stu-id="fc360-119">Note though the prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="fc360-120">Those routes identical to your VNet prefixes will be rejected.</span><span class="sxs-lookup"><span data-stu-id="fc360-120">Those routes identical to your VNet prefixes will be rejected.</span></span>

### <a name="multitunnel"></a><span data-ttu-id="fc360-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span><span class="sxs-lookup"><span data-stu-id="fc360-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="fc360-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in the same location.</span><span class="sxs-lookup"><span data-stu-id="fc360-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in the same location.</span></span> <span data-ttu-id="fc360-123">This capability provides multiple tunnels (paths) between the two networks in an active-active configuration.</span><span class="sxs-lookup"><span data-stu-id="fc360-123">This capability provides multiple tunnels (paths) between the two networks in an active-active configuration.</span></span> <span data-ttu-id="fc360-124">If one of the tunnels is disconnected, the corresponding routes will be withdrawn via BGP and the traffic automatically shifts to the remaining tunnels.</span><span class="sxs-lookup"><span data-stu-id="fc360-124">If one of the tunnels is disconnected, the corresponding routes will be withdrawn via BGP and the traffic automatically shifts to the remaining tunnels.</span></span>

<span data-ttu-id="fc360-125">The following diagram shows a simple example of this highly available setup:</span><span class="sxs-lookup"><span data-stu-id="fc360-125">The following diagram shows a simple example of this highly available setup:</span></span>

![Multiple active paths](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="transitrouting"></a><span data-ttu-id="fc360-127">Support transit routing between your on-premises networks and multiple Azure VNets</span><span class="sxs-lookup"><span data-stu-id="fc360-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="fc360-128">BGP enables multiple gateways to learn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span><span class="sxs-lookup"><span data-stu-id="fc360-128">BGP enables multiple gateways to learn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="fc360-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="fc360-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="fc360-130">The following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between the two on-premises networks through Azure VPN gateways within the Microsoft Networks:</span><span class="sxs-lookup"><span data-stu-id="fc360-130">The following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between the two on-premises networks through Azure VPN gateways within the Microsoft Networks:</span></span>

![Multi-hop transit](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="faq"></a><span data-ttu-id="fc360-132">BGP FAQ</span><span class="sxs-lookup"><span data-stu-id="fc360-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-faq-bgp-include](../../includes/vpn-gateway-faq-bgp-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fc360-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc360-133">Next steps</span></span>
<span data-ttu-id="fc360-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps to configure BGP for your cross-premises and VNet-to-VNet connections.</span><span class="sxs-lookup"><span data-stu-id="fc360-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps to configure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

