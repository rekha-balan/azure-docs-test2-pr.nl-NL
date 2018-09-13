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
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e7bf769cd1a91bbc876b9a484be93e7c7d8d5171
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800545"
---
# <a name="service-movement-cost"></a><span data-ttu-id="a6bf2-103">Service movement cost</span><span class="sxs-lookup"><span data-stu-id="a6bf2-103">Service movement cost</span></span>
<span data-ttu-id="a6bf2-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="a6bf2-105">The notion of "cost" is traded off against how much the cluster can be improved.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="a6bf2-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="a6bf2-107">The goal is to meet the requirements in the least disruptive or expensive way.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="a6bf2-108">Moving services costs CPU time and network bandwidth at a minimum.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="a6bf2-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="a6bf2-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="a6bf2-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="a6bf2-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="a6bf2-113">The first mechanism is simply counting every move that it would make.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="a6bf2-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span><span class="sxs-lookup"><span data-stu-id="a6bf2-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="a6bf2-115">This strategy works well.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-115">This strategy works well.</span></span> <span data-ttu-id="a6bf2-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="a6bf2-117">Some are likely to be much more expensive.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="a6bf2-118">Setting Move Costs</span><span class="sxs-lookup"><span data-stu-id="a6bf2-118">Setting Move Costs</span></span> 
<span data-ttu-id="a6bf2-119">You can specify the default move cost for a service when it is created:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="a6bf2-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="a6bf2-121">C#:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="a6bf2-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="a6bf2-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="a6bf2-124">C#:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="a6bf2-125">Dynamically specifying move cost on a per-replica basis</span><span class="sxs-lookup"><span data-stu-id="a6bf2-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="a6bf2-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="a6bf2-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="a6bf2-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="a6bf2-129">C#:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="a6bf2-130">Impact of move cost</span><span class="sxs-lookup"><span data-stu-id="a6bf2-130">Impact of move cost</span></span>
<span data-ttu-id="a6bf2-131">MoveCost has four levels: Zero, Low, Medium, and High.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="a6bf2-132">MoveCosts are relative to each other, except for Zero.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="a6bf2-133">Zero move cost means that movement is free and should not count against the score of the solution.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="a6bf2-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="a6bf2-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="a6bf2-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="a6bf2-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="a6bf2-137">A service’s notion of cost can be relative to many things.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="a6bf2-138">The most common factors in calculating your move cost are:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="a6bf2-139">The amount of state or data that the service has to move.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="a6bf2-140">The cost of disconnection of clients.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="a6bf2-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="a6bf2-142">The cost of interrupting an in-flight operation.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="a6bf2-143">Some operations at the data store level or operations performed in response to a client call are costly.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="a6bf2-144">After a certain point, you don’t want to stop them if you don’t have to.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="a6bf2-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="a6bf2-146">When the operation is done, you set the cost back to normal.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="a6bf2-147">Enabling move cost in your cluster</span><span class="sxs-lookup"><span data-stu-id="a6bf2-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="a6bf2-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="a6bf2-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="a6bf2-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="a6bf2-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="a6bf2-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="a6bf2-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6bf2-152">Next steps</span></span>
- <span data-ttu-id="a6bf2-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bf2-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="a6bf2-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a6bf2-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="a6bf2-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="a6bf2-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
