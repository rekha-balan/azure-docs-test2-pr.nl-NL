---
title: QoS Requirements for ExpressRoute | Microsoft Docs
description: This page provides detailed requirements for configuring and managing QoS for ExpressRoute circuits.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: ''
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 62c74f59768c8bb28839659945b812d5aeb72625
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662778"
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="1362d-103">ExpressRoute QoS requirements</span><span class="sxs-lookup"><span data-stu-id="1362d-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="1362d-104">Skype for Business has various workloads that require differentiated QoS treatment.</span><span class="sxs-lookup"><span data-stu-id="1362d-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="1362d-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span><span class="sxs-lookup"><span data-stu-id="1362d-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="1362d-106">QoS requirements apply to the Microsoft peering only.</span><span class="sxs-lookup"><span data-stu-id="1362d-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="1362d-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span><span class="sxs-lookup"><span data-stu-id="1362d-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="1362d-108">The following table provides a list of DSCP markings used by Skype for Business.</span><span class="sxs-lookup"><span data-stu-id="1362d-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="1362d-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="1362d-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="1362d-110">**Traffic Class**</span><span class="sxs-lookup"><span data-stu-id="1362d-110">**Traffic Class**</span></span> | <span data-ttu-id="1362d-111">**Treatment (DSCP Marking)**</span><span class="sxs-lookup"><span data-stu-id="1362d-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="1362d-112">**Skype for Business Workloads**</span><span class="sxs-lookup"><span data-stu-id="1362d-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1362d-113">**Voice**</span><span class="sxs-lookup"><span data-stu-id="1362d-113">**Voice**</span></span> |<span data-ttu-id="1362d-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="1362d-114">EF (46)</span></span> |<span data-ttu-id="1362d-115">Skype / Lync voice</span><span class="sxs-lookup"><span data-stu-id="1362d-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="1362d-116">**Interactive**</span><span class="sxs-lookup"><span data-stu-id="1362d-116">**Interactive**</span></span> |<span data-ttu-id="1362d-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="1362d-117">AF41 (34)</span></span> |<span data-ttu-id="1362d-118">Video</span><span class="sxs-lookup"><span data-stu-id="1362d-118">Video</span></span> |
| <span data-ttu-id="1362d-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="1362d-119">AF21 (18)</span></span> |<span data-ttu-id="1362d-120">App sharing</span><span class="sxs-lookup"><span data-stu-id="1362d-120">App sharing</span></span> | |
| <span data-ttu-id="1362d-121">**Default**</span><span class="sxs-lookup"><span data-stu-id="1362d-121">**Default**</span></span> |<span data-ttu-id="1362d-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="1362d-122">AF11 (10)</span></span> |<span data-ttu-id="1362d-123">File transfer</span><span class="sxs-lookup"><span data-stu-id="1362d-123">File transfer</span></span> |
| <span data-ttu-id="1362d-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="1362d-124">CS0 (0)</span></span> |<span data-ttu-id="1362d-125">Anything else</span><span class="sxs-lookup"><span data-stu-id="1362d-125">Anything else</span></span> | |

* <span data-ttu-id="1362d-126">You should classify the workloads and mark the right DSCP values.</span><span class="sxs-lookup"><span data-stu-id="1362d-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="1362d-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span><span class="sxs-lookup"><span data-stu-id="1362d-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="1362d-128">You should configure and support multiple QoS queues within your network.</span><span class="sxs-lookup"><span data-stu-id="1362d-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="1362d-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="1362d-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="1362d-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span><span class="sxs-lookup"><span data-stu-id="1362d-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="1362d-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span><span class="sxs-lookup"><span data-stu-id="1362d-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="1362d-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1362d-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="1362d-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span><span class="sxs-lookup"><span data-stu-id="1362d-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1362d-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="1362d-134">Next steps</span></span>
* <span data-ttu-id="1362d-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="1362d-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="1362d-136">See the following links to configure your ExpressRoute connection.</span><span class="sxs-lookup"><span data-stu-id="1362d-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="1362d-137">Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1362d-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="1362d-138">Configure routing</span><span class="sxs-lookup"><span data-stu-id="1362d-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="1362d-139">Link a VNet to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1362d-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)


