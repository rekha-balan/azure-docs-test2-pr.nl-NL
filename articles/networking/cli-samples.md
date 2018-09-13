---
title: Azure CLI Samples | Microsoft Docs
description: Azure CLI Samples
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865198"
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="175b7-103">Azure CLI Samples for networking</span><span class="sxs-lookup"><span data-stu-id="175b7-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="175b7-104">The following table includes links to bash scripts built using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="175b7-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="175b7-105">**Connectivity between Azure resources**</span><span class="sxs-lookup"><span data-stu-id="175b7-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="175b7-106">Create a virtual network for multi-tier applications</span><span class="sxs-lookup"><span data-stu-id="175b7-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-107">Creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="175b7-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="175b7-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="175b7-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="175b7-109">Peer two virtual networks</span><span class="sxs-lookup"><span data-stu-id="175b7-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-110">Creates and connects two virtual networks in the same region.</span><span class="sxs-lookup"><span data-stu-id="175b7-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="175b7-111">Route traffic through a network virtual appliance</span><span class="sxs-lookup"><span data-stu-id="175b7-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span><span class="sxs-lookup"><span data-stu-id="175b7-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="175b7-113">Filter inbound and outbound VM network traffic</span><span class="sxs-lookup"><span data-stu-id="175b7-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-114">Creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="175b7-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="175b7-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span><span class="sxs-lookup"><span data-stu-id="175b7-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="175b7-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span><span class="sxs-lookup"><span data-stu-id="175b7-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="175b7-117">**Load balancing and traffic direction**</span><span class="sxs-lookup"><span data-stu-id="175b7-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="175b7-118">Load balance traffic to VMs for high availability</span><span class="sxs-lookup"><span data-stu-id="175b7-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-119">Creates several virtual machines in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="175b7-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="175b7-120">Load balance multiple websites on VMs</span><span class="sxs-lookup"><span data-stu-id="175b7-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="175b7-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="175b7-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="175b7-122">Direct traffic across multiple regions for high application availability</span><span class="sxs-lookup"><span data-stu-id="175b7-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="175b7-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="175b7-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
