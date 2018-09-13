---
title: Introduction to IP flow verify in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher IP flow verify capability
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: a175f01a28ca60d4d8b3a68647059a5313cf948d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774910"
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="c066c-103">Introduction to IP flow verify in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="c066c-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="c066c-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c066c-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine.</span></span> <span data-ttu-id="c066c-105">The information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span><span class="sxs-lookup"><span data-stu-id="c066c-105">The information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="c066c-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span><span class="sxs-lookup"><span data-stu-id="c066c-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="c066c-107">While any source or destination IP can be chosen, IP flow verify helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="c066c-107">While any source or destination IP can be chosen, IP flow verify helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="c066c-108">IP flow verify targets a network interface of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c066c-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="c066c-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span><span class="sxs-lookup"><span data-stu-id="c066c-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="c066c-110">IP flow verify is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c066c-110">IP flow verify is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="c066c-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span><span class="sxs-lookup"><span data-stu-id="c066c-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="c066c-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span><span class="sxs-lookup"><span data-stu-id="c066c-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="c066c-113">The instance used does not affect the results of IP flow verify, as the route associated with the NIC is still be returned.</span><span class="sxs-lookup"><span data-stu-id="c066c-113">The instance used does not affect the results of IP flow verify, as the route associated with the NIC is still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="c066c-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="c066c-115">Next steps</span></span>

<span data-ttu-id="c066c-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span><span class="sxs-lookup"><span data-stu-id="c066c-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="c066c-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span><span class="sxs-lookup"><span data-stu-id="c066c-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](diagnose-vm-network-traffic-filtering-problem.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












