---
title: How to use public IP addresses in a virtual network
description: Learn how to configure a virtual network to use public IP addresses
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: b6e5dd7c-84ea-491d-8314-88e63a4da108
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: ad4402f17ef830c60ea0dd2342171fc05b7745c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671069"
---
# <a name="public-ip-address-space-in-a-virtual-network-vnet"></a><span data-ttu-id="41a7d-103">Public IP address space in a Virtual Network (VNet)</span><span class="sxs-lookup"><span data-stu-id="41a7d-103">Public IP address space in a Virtual Network (VNet)</span></span>
<span data-ttu-id="41a7d-104">Virtual networks (VNets) can contain both public and private (RFC 1918 address blocks) IP address spaces.</span><span class="sxs-lookup"><span data-stu-id="41a7d-104">Virtual networks (VNets) can contain both public and private (RFC 1918 address blocks) IP address spaces.</span></span> <span data-ttu-id="41a7d-105">When you add a public IP address range, it will be treated as part of the private VNet IP address space that is only reachable within the VNet, interconnected VNets, and from your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="41a7d-105">When you add a public IP address range, it will be treated as part of the private VNet IP address space that is only reachable within the VNet, interconnected VNets, and from your on-premises location.</span></span>

<span data-ttu-id="41a7d-106">The picture below shows a VNet that includes public and private IP adress spaces.</span><span class="sxs-lookup"><span data-stu-id="41a7d-106">The picture below shows a VNet that includes public and private IP adress spaces.</span></span>

![Public IP Conceptual](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-public-ip-within-vnet/IC775683.jpg)

## <a name="how-do-i-add-a-public-ip-address-range"></a><span data-ttu-id="41a7d-108">How do I add a public IP address range?</span><span class="sxs-lookup"><span data-stu-id="41a7d-108">How do I add a public IP address range?</span></span>
<span data-ttu-id="41a7d-109">You add a public IP address range the same way you would add a private IP address range; by either using a *netcfg* file, or by adding the configuration in the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41a7d-109">You add a public IP address range the same way you would add a private IP address range; by either using a *netcfg* file, or by adding the configuration in the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="41a7d-110">You can add a public IP address range when you create your VNet, or you can go back and add it afterward.</span><span class="sxs-lookup"><span data-stu-id="41a7d-110">You can add a public IP address range when you create your VNet, or you can go back and add it afterward.</span></span> <span data-ttu-id="41a7d-111">The example below shows both public and private IP address spaces configured in the same VNet.</span><span class="sxs-lookup"><span data-stu-id="41a7d-111">The example below shows both public and private IP address spaces configured in the same VNet.</span></span>

![Public IP Address in Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-public-ip-within-vnet/IC775684.png)

## <a name="are-there-any-limitations"></a><span data-ttu-id="41a7d-113">Are there any limitations?</span><span class="sxs-lookup"><span data-stu-id="41a7d-113">Are there any limitations?</span></span>
<span data-ttu-id="41a7d-114">There are a few IP address ranges that are not allowed:</span><span class="sxs-lookup"><span data-stu-id="41a7d-114">There are a few IP address ranges that are not allowed:</span></span>

* <span data-ttu-id="41a7d-115">224.0.0.0/4 (Multicast)</span><span class="sxs-lookup"><span data-stu-id="41a7d-115">224.0.0.0/4 (Multicast)</span></span>
* <span data-ttu-id="41a7d-116">255.255.255.255/32 (Broadcast)</span><span class="sxs-lookup"><span data-stu-id="41a7d-116">255.255.255.255/32 (Broadcast)</span></span>
* <span data-ttu-id="41a7d-117">127.0.0.0/8 (loopback)</span><span class="sxs-lookup"><span data-stu-id="41a7d-117">127.0.0.0/8 (loopback)</span></span>
* <span data-ttu-id="41a7d-118">169.254.0.0/16 (link-local)</span><span class="sxs-lookup"><span data-stu-id="41a7d-118">169.254.0.0/16 (link-local)</span></span>
* <span data-ttu-id="41a7d-119">168.63.129.16/32 (Internal DNS)</span><span class="sxs-lookup"><span data-stu-id="41a7d-119">168.63.129.16/32 (Internal DNS)</span></span>

## <a name="next-steps"></a><span data-ttu-id="41a7d-120">Next Steps</span><span class="sxs-lookup"><span data-stu-id="41a7d-120">Next Steps</span></span>
[<span data-ttu-id="41a7d-121">How to manage DNS servers used by a VNet</span><span class="sxs-lookup"><span data-stu-id="41a7d-121">How to manage DNS servers used by a VNet</span></span>](virtual-networks-manage-dns-in-vnet.md)



