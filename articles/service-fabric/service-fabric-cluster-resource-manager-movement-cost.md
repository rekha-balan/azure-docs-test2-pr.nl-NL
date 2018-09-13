---
title: 'Service Fabric Cluster Resource Manager: Movement cost | Microsoft Docs'
description: Overview of movement cost for Service Fabric services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: b118fc01ffa7a3b798b12ba37ea983bf8ba12286
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660575"
---
# <a name="service-movement-cost-for-influencing-cluster-resource-manager-choices"></a><span data-ttu-id="00cc5-103">Service movement cost for influencing Cluster Resource Manager choices</span><span class="sxs-lookup"><span data-stu-id="00cc5-103">Service movement cost for influencing Cluster Resource Manager choices</span></span>
<span data-ttu-id="00cc5-104">An important factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the overall cost of achieving that solution.</span><span class="sxs-lookup"><span data-stu-id="00cc5-104">An important factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the overall cost of achieving that solution.</span></span> <span data-ttu-id="00cc5-105">The notion of "cost" is traded off against the amount of balance that can be achieved.</span><span class="sxs-lookup"><span data-stu-id="00cc5-105">The notion of "cost" is traded off against the amount of balance that can be achieved.</span></span>

<span data-ttu-id="00cc5-106">Moving service instances or replicas costs CPU time and network bandwidth at a minimum.</span><span class="sxs-lookup"><span data-stu-id="00cc5-106">Moving service instances or replicas costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="00cc5-107">For stateful services, it also costs the amount of space on disk and in memory that you need to create a copy of the state before shutting down old replicas.</span><span class="sxs-lookup"><span data-stu-id="00cc5-107">For stateful services, it also costs the amount of space on disk and in memory that you need to create a copy of the state before shutting down old replicas.</span></span> <span data-ttu-id="00cc5-108">Clearly you’d want to minimize the cost of any solution that Azure Service Fabric Cluster Resource Manager comes up with.</span><span class="sxs-lookup"><span data-stu-id="00cc5-108">Clearly you’d want to minimize the cost of any solution that Azure Service Fabric Cluster Resource Manager comes up with.</span></span> <span data-ttu-id="00cc5-109">But you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span><span class="sxs-lookup"><span data-stu-id="00cc5-109">But you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="00cc5-110">The Cluster Resource Manager has two ways of computing costs and limiting them, even while it tries to manage the cluster according to its other goals.</span><span class="sxs-lookup"><span data-stu-id="00cc5-110">The Cluster Resource Manager has two ways of computing costs and limiting them, even while it tries to manage the cluster according to its other goals.</span></span> <span data-ttu-id="00cc5-111">The first is that when Cluster Resource Manager is planning a new layout for the cluster, it counts every move that it would make.</span><span class="sxs-lookup"><span data-stu-id="00cc5-111">The first is that when Cluster Resource Manager is planning a new layout for the cluster, it counts every move that it would make.</span></span> <span data-ttu-id="00cc5-112">If two solutions are generated with about the same balance (score), then prefer the one with the lowest cost (total number of moves).</span><span class="sxs-lookup"><span data-stu-id="00cc5-112">If two solutions are generated with about the same balance (score), then prefer the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="00cc5-113">This strategy works well.</span><span class="sxs-lookup"><span data-stu-id="00cc5-113">This strategy works well.</span></span> <span data-ttu-id="00cc5-114">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span><span class="sxs-lookup"><span data-stu-id="00cc5-114">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="00cc5-115">Some are likely to be much more expensive.</span><span class="sxs-lookup"><span data-stu-id="00cc5-115">Some are likely to be much more expensive.</span></span>

## <a name="changing-a-replicas-move-cost-and-factors-to-consider"></a><span data-ttu-id="00cc5-116">Changing a replica's move cost and factors to consider</span><span class="sxs-lookup"><span data-stu-id="00cc5-116">Changing a replica's move cost and factors to consider</span></span>
<span data-ttu-id="00cc5-117">As with reporting load (another feature of Cluster Resource Manager), services can dynamically self-report how costly it is to move at any time.</span><span class="sxs-lookup"><span data-stu-id="00cc5-117">As with reporting load (another feature of Cluster Resource Manager), services can dynamically self-report how costly it is to move at any time.</span></span>

<span data-ttu-id="00cc5-118">Code:</span><span class="sxs-lookup"><span data-stu-id="00cc5-118">Code:</span></span>

```csharp
this.ServicePartition.ReportMoveCost(MoveCost.Medium);
```

<span data-ttu-id="00cc5-119">A default move cost can also be specified when a service is created.</span><span class="sxs-lookup"><span data-stu-id="00cc5-119">A default move cost can also be specified when a service is created.</span></span>

<span data-ttu-id="00cc5-120">MoveCost has four levels: Zero, Low, Medium, and High.</span><span class="sxs-lookup"><span data-stu-id="00cc5-120">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="00cc5-121">MoveCosts are relative to each other, except for Zero.</span><span class="sxs-lookup"><span data-stu-id="00cc5-121">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="00cc5-122">Zero move cost means that movement is free and should not count against the score of the solution.</span><span class="sxs-lookup"><span data-stu-id="00cc5-122">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="00cc5-123">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span><span class="sxs-lookup"><span data-stu-id="00cc5-123">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="00cc5-124"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="00cc5-124"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="00cc5-125">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span><span class="sxs-lookup"><span data-stu-id="00cc5-125">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="00cc5-126">A service’s notion of cost can be relative to many things.</span><span class="sxs-lookup"><span data-stu-id="00cc5-126">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="00cc5-127">The most common factors in calculating your move cost are:</span><span class="sxs-lookup"><span data-stu-id="00cc5-127">The most common factors in calculating your move cost are:</span></span>

* <span data-ttu-id="00cc5-128">The amount of state or data that the service has to move.</span><span class="sxs-lookup"><span data-stu-id="00cc5-128">The amount of state or data that the service has to move.</span></span>
* <span data-ttu-id="00cc5-129">The cost of disconnection of clients.</span><span class="sxs-lookup"><span data-stu-id="00cc5-129">The cost of disconnection of clients.</span></span> <span data-ttu-id="00cc5-130">The cost of moving a primary replica is usually higher than the cost of moving a secondary replica.</span><span class="sxs-lookup"><span data-stu-id="00cc5-130">The cost of moving a primary replica is usually higher than the cost of moving a secondary replica.</span></span>
* <span data-ttu-id="00cc5-131">The cost of interrupting an in-flight operation.</span><span class="sxs-lookup"><span data-stu-id="00cc5-131">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="00cc5-132">Some operations at the data store level or operations performed in response to a client call are costly.</span><span class="sxs-lookup"><span data-stu-id="00cc5-132">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="00cc5-133">After a certain point, you don’t want to stop them if you don’t have to.</span><span class="sxs-lookup"><span data-stu-id="00cc5-133">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="00cc5-134">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span><span class="sxs-lookup"><span data-stu-id="00cc5-134">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="00cc5-135">When the operation is done, you set the cost back to normal.</span><span class="sxs-lookup"><span data-stu-id="00cc5-135">When the operation is done, you set the cost back to normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00cc5-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="00cc5-136">Next steps</span></span>
* <span data-ttu-id="00cc5-137">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span><span class="sxs-lookup"><span data-stu-id="00cc5-137">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="00cc5-138">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="00cc5-138">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
* <span data-ttu-id="00cc5-139">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="00cc5-139">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png

