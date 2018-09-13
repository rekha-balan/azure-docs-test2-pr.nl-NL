---
title: High availability ports overview in Azure | Microsoft Docs
description: Learn about high availability ports load balancing on an internal load balancer.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/07/2018
ms.author: kumud
ms.openlocfilehash: 716a3dafe08e896924bd28e44d69141e4c229687
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966216"
---
# <a name="high-availability-ports-overview"></a><span data-ttu-id="568d1-103">High availability ports overview</span><span class="sxs-lookup"><span data-stu-id="568d1-103">High availability ports overview</span></span>

<span data-ttu-id="568d1-104">Azure Standard Load Balancer helps you load-balance TCP and UDP flows on all ports simultaneously when you're using an internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="568d1-104">Azure Standard Load Balancer helps you load-balance TCP and UDP flows on all ports simultaneously when you're using an internal load balancer.</span></span> 

<span data-ttu-id="568d1-105">A high availability (HA) ports rule is a variant of a load-balancing rule, configured on an internal Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="568d1-105">A high availability (HA) ports rule is a variant of a load-balancing rule, configured on an internal Standard Load Balancer.</span></span> <span data-ttu-id="568d1-106">You can simplify the use of a load balancer by providing a single rule to load-balance all TCP and UDP flows that arrive on all ports of an internal Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="568d1-106">You can simplify the use of a load balancer by providing a single rule to load-balance all TCP and UDP flows that arrive on all ports of an internal Standard Load Balancer.</span></span> <span data-ttu-id="568d1-107">The load-balancing decision is made per flow.</span><span class="sxs-lookup"><span data-stu-id="568d1-107">The load-balancing decision is made per flow.</span></span> <span data-ttu-id="568d1-108">This action is based on the following five-tuple connection: source IP address, source port, destination IP address, destination port, and protocol.</span><span class="sxs-lookup"><span data-stu-id="568d1-108">This action is based on the following five-tuple connection: source IP address, source port, destination IP address, destination port, and protocol.</span></span>

<span data-ttu-id="568d1-109">The HA ports feature helps you with critical scenarios, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks.</span><span class="sxs-lookup"><span data-stu-id="568d1-109">The HA ports feature helps you with critical scenarios, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks.</span></span> <span data-ttu-id="568d1-110">The feature can also help when a large number of ports must be load-balanced.</span><span class="sxs-lookup"><span data-stu-id="568d1-110">The feature can also help when a large number of ports must be load-balanced.</span></span> 

<span data-ttu-id="568d1-111">The HA ports feature is configured when you set the front-end and back-end ports to **0** and the protocol to **All**.</span><span class="sxs-lookup"><span data-stu-id="568d1-111">The HA ports feature is configured when you set the front-end and back-end ports to **0** and the protocol to **All**.</span></span> <span data-ttu-id="568d1-112">The internal load balancer resource then balances all TCP and UDP flows, regardless of port number.</span><span class="sxs-lookup"><span data-stu-id="568d1-112">The internal load balancer resource then balances all TCP and UDP flows, regardless of port number.</span></span>

## <a name="why-use-ha-ports"></a><span data-ttu-id="568d1-113">Why use HA ports?</span><span class="sxs-lookup"><span data-stu-id="568d1-113">Why use HA ports?</span></span>

### <a name="nva"></a><span data-ttu-id="568d1-114">Network virtual appliances</span><span class="sxs-lookup"><span data-stu-id="568d1-114">Network virtual appliances</span></span>

<span data-ttu-id="568d1-115">You can use NVAs to help secure your Azure workload from multiple types of security threats.</span><span class="sxs-lookup"><span data-stu-id="568d1-115">You can use NVAs to help secure your Azure workload from multiple types of security threats.</span></span> <span data-ttu-id="568d1-116">When you use NVAs in these scenarios, they must be reliable and highly available, and they must scale out for demand.</span><span class="sxs-lookup"><span data-stu-id="568d1-116">When you use NVAs in these scenarios, they must be reliable and highly available, and they must scale out for demand.</span></span>

<span data-ttu-id="568d1-117">You can achieve these goals simply by adding NVA instances to the back-end pool of your internal load balancer and configuring an HA ports load-balancer rule.</span><span class="sxs-lookup"><span data-stu-id="568d1-117">You can achieve these goals simply by adding NVA instances to the back-end pool of your internal load balancer and configuring an HA ports load-balancer rule.</span></span>

<span data-ttu-id="568d1-118">For NVA HA scenarios, HA ports offer the following advantages:</span><span class="sxs-lookup"><span data-stu-id="568d1-118">For NVA HA scenarios, HA ports offer the following advantages:</span></span>
- <span data-ttu-id="568d1-119">Provide fast failover to healthy instances, with per-instance health probes</span><span class="sxs-lookup"><span data-stu-id="568d1-119">Provide fast failover to healthy instances, with per-instance health probes</span></span>
- <span data-ttu-id="568d1-120">Ensure higher performance with scale-out to *n*-active instances</span><span class="sxs-lookup"><span data-stu-id="568d1-120">Ensure higher performance with scale-out to *n*-active instances</span></span>
- <span data-ttu-id="568d1-121">Provide *n*-active and active-passive scenarios</span><span class="sxs-lookup"><span data-stu-id="568d1-121">Provide *n*-active and active-passive scenarios</span></span>
- <span data-ttu-id="568d1-122">Eliminate the need for complex solutions, such as Apache ZooKeeper nodes for monitoring appliances</span><span class="sxs-lookup"><span data-stu-id="568d1-122">Eliminate the need for complex solutions, such as Apache ZooKeeper nodes for monitoring appliances</span></span>

<span data-ttu-id="568d1-123">The following diagram presents a hub-and-spoke virtual network deployment.</span><span class="sxs-lookup"><span data-stu-id="568d1-123">The following diagram presents a hub-and-spoke virtual network deployment.</span></span> <span data-ttu-id="568d1-124">The spokes force-tunnel their traffic to the hub virtual network and through the NVA, before leaving the trusted space.</span><span class="sxs-lookup"><span data-stu-id="568d1-124">The spokes force-tunnel their traffic to the hub virtual network and through the NVA, before leaving the trusted space.</span></span> <span data-ttu-id="568d1-125">The NVAs are behind an internal Standard Load Balancer with an HA ports configuration.</span><span class="sxs-lookup"><span data-stu-id="568d1-125">The NVAs are behind an internal Standard Load Balancer with an HA ports configuration.</span></span> <span data-ttu-id="568d1-126">All traffic can be processed and forwarded accordingly.</span><span class="sxs-lookup"><span data-stu-id="568d1-126">All traffic can be processed and forwarded accordingly.</span></span>

![Diagram of hub-and-spoke virtual network, with NVAs deployed in HA mode](./media/load-balancer-ha-ports-overview/nvaha.png)

>[!NOTE]
> <span data-ttu-id="568d1-128">If you are using NVAs, confirm with their providers how to best use HA ports and to learn which scenarios are supported.</span><span class="sxs-lookup"><span data-stu-id="568d1-128">If you are using NVAs, confirm with their providers how to best use HA ports and to learn which scenarios are supported.</span></span>

### <a name="load-balancing-large-numbers-of-ports"></a><span data-ttu-id="568d1-129">Load-balancing large numbers of ports</span><span class="sxs-lookup"><span data-stu-id="568d1-129">Load-balancing large numbers of ports</span></span>

<span data-ttu-id="568d1-130">You can also use HA ports for applications that require load balancing of large numbers of ports.</span><span class="sxs-lookup"><span data-stu-id="568d1-130">You can also use HA ports for applications that require load balancing of large numbers of ports.</span></span> <span data-ttu-id="568d1-131">You can simplify these scenarios by using an internal [Standard Load Balancer](load-balancer-standard-overview.md) with HA ports.</span><span class="sxs-lookup"><span data-stu-id="568d1-131">You can simplify these scenarios by using an internal [Standard Load Balancer](load-balancer-standard-overview.md) with HA ports.</span></span> <span data-ttu-id="568d1-132">A single load-balancing rule replaces multiple individual load-balancing rules, one for each port.</span><span class="sxs-lookup"><span data-stu-id="568d1-132">A single load-balancing rule replaces multiple individual load-balancing rules, one for each port.</span></span>

## <a name="region-availability"></a><span data-ttu-id="568d1-133">Region availability</span><span class="sxs-lookup"><span data-stu-id="568d1-133">Region availability</span></span>

<span data-ttu-id="568d1-134">The HA ports feature is available in all the global Azure regions.</span><span class="sxs-lookup"><span data-stu-id="568d1-134">The HA ports feature is available in all the global Azure regions.</span></span>

## <a name="supported-configurations"></a><span data-ttu-id="568d1-135">Supported configurations</span><span class="sxs-lookup"><span data-stu-id="568d1-135">Supported configurations</span></span>

### <a name="a-single-non-floating-ip-non-direct-server-return-ha-ports-configuration-on-an-internal-standard-load-balancer"></a><span data-ttu-id="568d1-136">A single, non-floating IP (non-Direct Server Return) HA-ports configuration on an internal Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="568d1-136">A single, non-floating IP (non-Direct Server Return) HA-ports configuration on an internal Standard Load Balancer</span></span>

<span data-ttu-id="568d1-137">This configuration is a basic HA ports configuration.</span><span class="sxs-lookup"><span data-stu-id="568d1-137">This configuration is a basic HA ports configuration.</span></span> <span data-ttu-id="568d1-138">You can configure an HA ports load-balancing rule on a single front-end IP address by doing the following:</span><span class="sxs-lookup"><span data-stu-id="568d1-138">You can configure an HA ports load-balancing rule on a single front-end IP address by doing the following:</span></span>
1. <span data-ttu-id="568d1-139">While configuring Standard Load Balancer, select the **HA ports** check box in the Load Balancer rule configuration.</span><span class="sxs-lookup"><span data-stu-id="568d1-139">While configuring Standard Load Balancer, select the **HA ports** check box in the Load Balancer rule configuration.</span></span>
2. <span data-ttu-id="568d1-140">For **Floating IP**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="568d1-140">For **Floating IP**, select **Disabled**.</span></span>

<span data-ttu-id="568d1-141">This configuration does not allow any other load-balancing rule configuration on the current load balancer resource.</span><span class="sxs-lookup"><span data-stu-id="568d1-141">This configuration does not allow any other load-balancing rule configuration on the current load balancer resource.</span></span> <span data-ttu-id="568d1-142">It also allows no other internal load balancer resource configuration for the given set of back-end instances.</span><span class="sxs-lookup"><span data-stu-id="568d1-142">It also allows no other internal load balancer resource configuration for the given set of back-end instances.</span></span>

<span data-ttu-id="568d1-143">However, you can configure a public Standard Load Balancer for the back-end instances in addition to this HA ports rule.</span><span class="sxs-lookup"><span data-stu-id="568d1-143">However, you can configure a public Standard Load Balancer for the back-end instances in addition to this HA ports rule.</span></span>

### <a name="a-single-floating-ip-direct-server-return-ha-ports-configuration-on-an-internal-standard-load-balancer"></a><span data-ttu-id="568d1-144">A single, floating IP (Direct Server Return) HA-ports configuration on an internal Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="568d1-144">A single, floating IP (Direct Server Return) HA-ports configuration on an internal Standard Load Balancer</span></span>

<span data-ttu-id="568d1-145">You can similarly configure your load balancer to use a load-balancing rule with **HA Port** with a single front end by setting the **Floating IP** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="568d1-145">You can similarly configure your load balancer to use a load-balancing rule with **HA Port** with a single front end by setting the **Floating IP** to **Enabled**.</span></span> 

<span data-ttu-id="568d1-146">By using this configuration, you can add more floating IP load-balancing rules and/or a public load balancer.</span><span class="sxs-lookup"><span data-stu-id="568d1-146">By using this configuration, you can add more floating IP load-balancing rules and/or a public load balancer.</span></span> <span data-ttu-id="568d1-147">However, you cannot use a non-floating IP, HA-ports load-balancing configuration on top of this configuration.</span><span class="sxs-lookup"><span data-stu-id="568d1-147">However, you cannot use a non-floating IP, HA-ports load-balancing configuration on top of this configuration.</span></span>

### <a name="multiple-ha-ports-configurations-on-an-internal-standard-load-balancer"></a><span data-ttu-id="568d1-148">Multiple HA-ports configurations on an internal Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="568d1-148">Multiple HA-ports configurations on an internal Standard Load Balancer</span></span>

<span data-ttu-id="568d1-149">If your scenario requires that you configure more than one HA port front end for the same back-end pool, you can do the following:</span><span class="sxs-lookup"><span data-stu-id="568d1-149">If your scenario requires that you configure more than one HA port front end for the same back-end pool, you can do the following:</span></span> 
- <span data-ttu-id="568d1-150">Configure more than one front-end private IP address for a single internal Standard Load Balancer resource.</span><span class="sxs-lookup"><span data-stu-id="568d1-150">Configure more than one front-end private IP address for a single internal Standard Load Balancer resource.</span></span>
- <span data-ttu-id="568d1-151">Configure multiple load-balancing rules, where each rule has a single unique front-end IP address selected.</span><span class="sxs-lookup"><span data-stu-id="568d1-151">Configure multiple load-balancing rules, where each rule has a single unique front-end IP address selected.</span></span>
- <span data-ttu-id="568d1-152">Select the **HA ports** option, and then set **Floating IP** to **Enabled** for all the load-balancing rules.</span><span class="sxs-lookup"><span data-stu-id="568d1-152">Select the **HA ports** option, and then set **Floating IP** to **Enabled** for all the load-balancing rules.</span></span>

### <a name="an-internal-load-balancer-with-ha-ports-and-a-public-load-balancer-on-the-same-back-end-instance"></a><span data-ttu-id="568d1-153">An internal load balancer with HA ports and a public load balancer on the same back-end instance</span><span class="sxs-lookup"><span data-stu-id="568d1-153">An internal load balancer with HA ports and a public load balancer on the same back-end instance</span></span>

<span data-ttu-id="568d1-154">You can configure *one* public Standard Load Balancer resource for the back-end resources, along with a single internal Standard Load Balancer with HA ports.</span><span class="sxs-lookup"><span data-stu-id="568d1-154">You can configure *one* public Standard Load Balancer resource for the back-end resources, along with a single internal Standard Load Balancer with HA ports.</span></span>

>[!NOTE]
><span data-ttu-id="568d1-155">This capability is currently available via Azure Resource Manager templates, but it is not available via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="568d1-155">This capability is currently available via Azure Resource Manager templates, but it is not available via the Azure portal.</span></span>

## <a name="limitations"></a><span data-ttu-id="568d1-156">Limitations</span><span class="sxs-lookup"><span data-stu-id="568d1-156">Limitations</span></span>

- <span data-ttu-id="568d1-157">HA ports configuration is available only for internal load balancers.</span><span class="sxs-lookup"><span data-stu-id="568d1-157">HA ports configuration is available only for internal load balancers.</span></span> <span data-ttu-id="568d1-158">It is not available for public load balancers.</span><span class="sxs-lookup"><span data-stu-id="568d1-158">It is not available for public load balancers.</span></span>

- <span data-ttu-id="568d1-159">The combining of an HA ports load-balancing rule and a non-HA ports load-balancing rule is not supported.</span><span class="sxs-lookup"><span data-stu-id="568d1-159">The combining of an HA ports load-balancing rule and a non-HA ports load-balancing rule is not supported.</span></span>

- <span data-ttu-id="568d1-160">The HA ports feature is not available for IPv6.</span><span class="sxs-lookup"><span data-stu-id="568d1-160">The HA ports feature is not available for IPv6.</span></span>

- <span data-ttu-id="568d1-161">Flow symmetry for NVA scenarios is supported with a single NIC only.</span><span class="sxs-lookup"><span data-stu-id="568d1-161">Flow symmetry for NVA scenarios is supported with a single NIC only.</span></span> <span data-ttu-id="568d1-162">See the description and diagram for [network virtual appliances](#nva).</span><span class="sxs-lookup"><span data-stu-id="568d1-162">See the description and diagram for [network virtual appliances](#nva).</span></span> <span data-ttu-id="568d1-163">However, if a destination NAT can work for your scenario, you could use it to make sure the internal load balancer sends the return traffic to the same NVA.</span><span class="sxs-lookup"><span data-stu-id="568d1-163">However, if a destination NAT can work for your scenario, you could use it to make sure the internal load balancer sends the return traffic to the same NVA.</span></span>


## <a name="next-steps"></a><span data-ttu-id="568d1-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="568d1-164">Next steps</span></span>

- [<span data-ttu-id="568d1-165">Configure HA ports on an internal Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="568d1-165">Configure HA ports on an internal Standard Load Balancer</span></span>](load-balancer-configure-ha-ports.md)
- [<span data-ttu-id="568d1-166">Learn about Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="568d1-166">Learn about Standard Load Balancer</span></span>](load-balancer-standard-overview.md)
