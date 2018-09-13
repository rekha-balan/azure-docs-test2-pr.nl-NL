---
title: Border connectivity network integration considerations for Azure Stack integrated systems | Microsoft Docs
description: Learn what you can do to plan for datacenter border network connectivity with multi-node Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2018
ms.author: jeffgilb
ms.reviewer: wamota
ms.openlocfilehash: 39edcb97f062693d11fd5c0ce332c206ebd4b54a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869917"
---
# <a name="border-connectivity"></a><span data-ttu-id="63ef9-103">Border connectivity</span><span class="sxs-lookup"><span data-stu-id="63ef9-103">Border connectivity</span></span> 
<span data-ttu-id="63ef9-104">Network integration planning is an important prerequisite for successful Azure Stack integrated systems deployment, operation, and management.</span><span class="sxs-lookup"><span data-stu-id="63ef9-104">Network integration planning is an important prerequisite for successful Azure Stack integrated systems deployment, operation, and management.</span></span> <span data-ttu-id="63ef9-105">Border connectivity planning begins by choosing whether or not to use dynamic routing with border gateway protocol (BGP).</span><span class="sxs-lookup"><span data-stu-id="63ef9-105">Border connectivity planning begins by choosing whether or not to use dynamic routing with border gateway protocol (BGP).</span></span> <span data-ttu-id="63ef9-106">This requires assigning a 16-bit BGP autonomous system number (public or private) or using static routing, where a static default route is assigned to the border devices.</span><span class="sxs-lookup"><span data-stu-id="63ef9-106">This requires assigning a 16-bit BGP autonomous system number (public or private) or using static routing, where a static default route is assigned to the border devices.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63ef9-107">The top of rack (TOR) switches require Layer 3 uplinks with Point-to-Point IPs (/30 networks) configured on the physical interfaces.</span><span class="sxs-lookup"><span data-stu-id="63ef9-107">The top of rack (TOR) switches require Layer 3 uplinks with Point-to-Point IPs (/30 networks) configured on the physical interfaces.</span></span> <span data-ttu-id="63ef9-108">It is not supported to use Layer 2 uplinks with TOR switches supporting Azure Stack operations.</span><span class="sxs-lookup"><span data-stu-id="63ef9-108">It is not supported to use Layer 2 uplinks with TOR switches supporting Azure Stack operations.</span></span> 

## <a name="bgp-routing"></a><span data-ttu-id="63ef9-109">BGP routing</span><span class="sxs-lookup"><span data-stu-id="63ef9-109">BGP routing</span></span>
<span data-ttu-id="63ef9-110">Using a dynamic routing protocol like BGP guarantees that your system is always aware of network changes and facilitates administration.</span><span class="sxs-lookup"><span data-stu-id="63ef9-110">Using a dynamic routing protocol like BGP guarantees that your system is always aware of network changes and facilitates administration.</span></span> 

<span data-ttu-id="63ef9-111">As shown in the following diagram, advertising of the private IP space on the TOR switch is restricted using a prefix-list.</span><span class="sxs-lookup"><span data-stu-id="63ef9-111">As shown in the following diagram, advertising of the private IP space on the TOR switch is restricted using a prefix-list.</span></span> <span data-ttu-id="63ef9-112">The prefix list defines the private IP subnets and applying it as a route-map on the connection between the TOR and the border.</span><span class="sxs-lookup"><span data-stu-id="63ef9-112">The prefix list defines the private IP subnets and applying it as a route-map on the connection between the TOR and the border.</span></span>

<span data-ttu-id="63ef9-113">The Software Load Balancer (SLB) running inside the Azure Stack solution peers to the TOR devices so it can dynamically advertise the VIP addresses.</span><span class="sxs-lookup"><span data-stu-id="63ef9-113">The Software Load Balancer (SLB) running inside the Azure Stack solution peers to the TOR devices so it can dynamically advertise the VIP addresses.</span></span>

<span data-ttu-id="63ef9-114">To ensure that user traffic immediately and transparently recovers from failure, the VPC or MLAG configured between the TOR devices allows the use of multi-chassis link aggregation to the hosts and HSRP or VRRP that provides network redundancy for the IP networks.</span><span class="sxs-lookup"><span data-stu-id="63ef9-114">To ensure that user traffic immediately and transparently recovers from failure, the VPC or MLAG configured between the TOR devices allows the use of multi-chassis link aggregation to the hosts and HSRP or VRRP that provides network redundancy for the IP networks.</span></span>

![BGP routing](media/azure-stack-border-connectivity/bgp-routing.png)

## <a name="static-routing"></a><span data-ttu-id="63ef9-116">Static routing</span><span class="sxs-lookup"><span data-stu-id="63ef9-116">Static routing</span></span>
<span data-ttu-id="63ef9-117">Static routing requires additional configuration to the border devices.</span><span class="sxs-lookup"><span data-stu-id="63ef9-117">Static routing requires additional configuration to the border devices.</span></span> <span data-ttu-id="63ef9-118">It requires more manual intervention and management as well as thorough analysis before any change and issues caused by a configuration error may take more time to rollback depending on the changes made.</span><span class="sxs-lookup"><span data-stu-id="63ef9-118">It requires more manual intervention and management as well as thorough analysis before any change and issues caused by a configuration error may take more time to rollback depending on the changes made.</span></span> <span data-ttu-id="63ef9-119">It is not the recommended routing method, but it is supported.</span><span class="sxs-lookup"><span data-stu-id="63ef9-119">It is not the recommended routing method, but it is supported.</span></span>

<span data-ttu-id="63ef9-120">To integrate Azure Stack into your networking environment using static routing, all four physical links between the border and the TOR device must be connected and high availability cannot be guaranteed because of how static routing works.</span><span class="sxs-lookup"><span data-stu-id="63ef9-120">To integrate Azure Stack into your networking environment using static routing, all four physical links between the border and the TOR device must be connected and high availability cannot be guaranteed because of how static routing works.</span></span>

<span data-ttu-id="63ef9-121">The border device must be configured with static routes pointing to the TOR devices P2P for traffic destined to the *External* network or Public VIPs and the *Infrastructure* network.</span><span class="sxs-lookup"><span data-stu-id="63ef9-121">The border device must be configured with static routes pointing to the TOR devices P2P for traffic destined to the *External* network or Public VIPs and the *Infrastructure* network.</span></span> <span data-ttu-id="63ef9-122">It will require static routes to the *BMC* and the *External* networks for the deployment.</span><span class="sxs-lookup"><span data-stu-id="63ef9-122">It will require static routes to the *BMC* and the *External* networks for the deployment.</span></span> <span data-ttu-id="63ef9-123">Operators can choose to leave static routes in the border to access management resources that reside on the *BMC* network.</span><span class="sxs-lookup"><span data-stu-id="63ef9-123">Operators can choose to leave static routes in the border to access management resources that reside on the *BMC* network.</span></span> <span data-ttu-id="63ef9-124">Adding static routes to *switch infrastructure* and *switch management* networks is optional.</span><span class="sxs-lookup"><span data-stu-id="63ef9-124">Adding static routes to *switch infrastructure* and *switch management* networks is optional.</span></span>

<span data-ttu-id="63ef9-125">The TOR devices come configured with a static default route sending all traffic to the border devices.</span><span class="sxs-lookup"><span data-stu-id="63ef9-125">The TOR devices come configured with a static default route sending all traffic to the border devices.</span></span> <span data-ttu-id="63ef9-126">The one traffic exception to the default rule is for the private space, which is blocked using an Access Control List applied on the TOR to border connection.</span><span class="sxs-lookup"><span data-stu-id="63ef9-126">The one traffic exception to the default rule is for the private space, which is blocked using an Access Control List applied on the TOR to border connection.</span></span>

<span data-ttu-id="63ef9-127">Static routing applies only to the uplinks between the TOR and border switches.</span><span class="sxs-lookup"><span data-stu-id="63ef9-127">Static routing applies only to the uplinks between the TOR and border switches.</span></span> <span data-ttu-id="63ef9-128">BGP dynamic routing is used inside the rack because it is an essential tool for the SLB and other components and can’t be disabled or removed.</span><span class="sxs-lookup"><span data-stu-id="63ef9-128">BGP dynamic routing is used inside the rack because it is an essential tool for the SLB and other components and can’t be disabled or removed.</span></span>

![Static routing](media/azure-stack-border-connectivity/static-routing.png)

<span data-ttu-id="63ef9-130"><sup>\*</sup> The BMC network is optional after deployment.</span><span class="sxs-lookup"><span data-stu-id="63ef9-130"><sup>\*</sup> The BMC network is optional after deployment.</span></span>

<span data-ttu-id="63ef9-131"><sup>\*\*</sup> The Switch Infrastructure network is optional, as the whole network can be included in the Switch Management network.</span><span class="sxs-lookup"><span data-stu-id="63ef9-131"><sup>\*\*</sup> The Switch Infrastructure network is optional, as the whole network can be included in the Switch Management network.</span></span>

<span data-ttu-id="63ef9-132"><sup>\*\*\*</sup> The Switch Management network is required and can be added separately from the Switch Infrastructure network.</span><span class="sxs-lookup"><span data-stu-id="63ef9-132"><sup>\*\*\*</sup> The Switch Management network is required and can be added separately from the Switch Infrastructure network.</span></span>

## <a name="transparent-proxy"></a><span data-ttu-id="63ef9-133">Transparent proxy</span><span class="sxs-lookup"><span data-stu-id="63ef9-133">Transparent proxy</span></span>
<span data-ttu-id="63ef9-134">If your datacenter requires all traffic to use a proxy, you must configure a *transparent proxy* to process all traffic from the rack to handle it according to policy, separating traffic between the zones on your network.</span><span class="sxs-lookup"><span data-stu-id="63ef9-134">If your datacenter requires all traffic to use a proxy, you must configure a *transparent proxy* to process all traffic from the rack to handle it according to policy, separating traffic between the zones on your network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63ef9-135">The Azure Stack solution doesn’t support normal web proxies.</span><span class="sxs-lookup"><span data-stu-id="63ef9-135">The Azure Stack solution doesn’t support normal web proxies.</span></span>  

<span data-ttu-id="63ef9-136">A transparent proxy (also known as an intercepting, inline, or forced proxy) intercepts normal communication at the network layer without requiring any special client configuration.</span><span class="sxs-lookup"><span data-stu-id="63ef9-136">A transparent proxy (also known as an intercepting, inline, or forced proxy) intercepts normal communication at the network layer without requiring any special client configuration.</span></span> <span data-ttu-id="63ef9-137">Clients need not to be aware of the existence of the proxy.</span><span class="sxs-lookup"><span data-stu-id="63ef9-137">Clients need not to be aware of the existence of the proxy.</span></span>

![Transparent proxy](media/azure-stack-border-connectivity/transparent-proxy.png)

## <a name="next-steps"></a><span data-ttu-id="63ef9-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="63ef9-139">Next steps</span></span>
[<span data-ttu-id="63ef9-140">DNS integration</span><span class="sxs-lookup"><span data-stu-id="63ef9-140">DNS integration</span></span>](azure-stack-integrate-dns.md)