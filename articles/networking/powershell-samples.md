---
title: Azure PowerShell Samples | Microsoft Docs
description: Azure PowerShell Samples
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855838"
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="3e3ea-103">Azure PowerShell Samples for networking</span><span class="sxs-lookup"><span data-stu-id="3e3ea-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="3e3ea-104">The following table includes links to scripts built using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="3e3ea-105">**Connectivity between Azure resources**</span><span class="sxs-lookup"><span data-stu-id="3e3ea-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="3e3ea-106">Create a virtual network for multi-tier applications</span><span class="sxs-lookup"><span data-stu-id="3e3ea-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-107">Creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="3e3ea-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="3e3ea-109">Peer two virtual networks</span><span class="sxs-lookup"><span data-stu-id="3e3ea-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-110">Creates and connects two virtual networks in the same region.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="3e3ea-111">Route traffic through a network virtual appliance</span><span class="sxs-lookup"><span data-stu-id="3e3ea-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="3e3ea-113">Filter inbound and outbound VM network traffic</span><span class="sxs-lookup"><span data-stu-id="3e3ea-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-114">Creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="3e3ea-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span><span class="sxs-lookup"><span data-stu-id="3e3ea-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="3e3ea-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="3e3ea-117">**Load balancing and traffic direction**</span><span class="sxs-lookup"><span data-stu-id="3e3ea-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="3e3ea-118">Load balance traffic to VMs for high availability</span><span class="sxs-lookup"><span data-stu-id="3e3ea-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-119">Creates several virtual machines in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="3e3ea-120">Load balance multiple websites on VMs</span><span class="sxs-lookup"><span data-stu-id="3e3ea-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="3e3ea-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="3e3ea-122">Direct traffic across multiple regions for high application availability</span><span class="sxs-lookup"><span data-stu-id="3e3ea-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="3e3ea-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="3e3ea-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
