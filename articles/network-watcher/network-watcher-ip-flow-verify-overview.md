---
title: Introduction to IP flow verify in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher IP flow verify capability
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c960a45a5e237e13f7cce6b4b2e3bd4827754b30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556008"
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="10bd3-103">Introduction to IP flow verify in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="10bd3-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="10bd3-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span><span class="sxs-lookup"><span data-stu-id="10bd3-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="10bd3-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span><span class="sxs-lookup"><span data-stu-id="10bd3-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="10bd3-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span><span class="sxs-lookup"><span data-stu-id="10bd3-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="10bd3-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="10bd3-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="10bd3-108">IP flow verify targets a network interface of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="10bd3-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="10bd3-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span><span class="sxs-lookup"><span data-stu-id="10bd3-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="10bd3-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="10bd3-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="10bd3-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span><span class="sxs-lookup"><span data-stu-id="10bd3-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="10bd3-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span><span class="sxs-lookup"><span data-stu-id="10bd3-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="10bd3-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span><span class="sxs-lookup"><span data-stu-id="10bd3-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="10bd3-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="10bd3-115">Next steps</span></span>

<span data-ttu-id="10bd3-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span><span class="sxs-lookup"><span data-stu-id="10bd3-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="10bd3-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span><span class="sxs-lookup"><span data-stu-id="10bd3-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-ip-flow-verify-overview/figure1.png













