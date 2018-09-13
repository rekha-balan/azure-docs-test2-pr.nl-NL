---
title: Introduction to topology in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher topology capabilities
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: dc0d0890b53bb22ec08170f368c1e06480ae66d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548780"
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="21795-103">Introduction to topology in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="21795-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="21795-104">Topology returns a graph of network resources in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="21795-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="21795-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span><span class="sxs-lookup"><span data-stu-id="21795-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![topology overview][1]

<span data-ttu-id="21795-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span><span class="sxs-lookup"><span data-stu-id="21795-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="21795-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span><span class="sxs-lookup"><span data-stu-id="21795-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="21795-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span><span class="sxs-lookup"><span data-stu-id="21795-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="21795-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="21795-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="21795-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span><span class="sxs-lookup"><span data-stu-id="21795-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="21795-112">As resources are returned the connection between them are modeled under two relationships.</span><span class="sxs-lookup"><span data-stu-id="21795-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="21795-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span><span class="sxs-lookup"><span data-stu-id="21795-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="21795-114">**Associated** - Example: A NIC is associated with a VM</span><span class="sxs-lookup"><span data-stu-id="21795-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="21795-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="21795-115">Next steps</span></span>

<span data-ttu-id="21795-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="21795-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-topology-overview/topology.png

