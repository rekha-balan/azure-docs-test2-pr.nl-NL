---
title: Throttling in the Service Fabric cluster resource manager | Microsoft Docs
description: Learn to configure the throttles provided by the Service Fabric Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: 8a8419497bda3f1df523d6aff28028548abc155a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662655"
---
# <a name="throttling-the-behavior-of-the-service-fabric-cluster-resource-manager"></a><span data-ttu-id="0d08e-103">Throttling the behavior of the Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0d08e-103">Throttling the behavior of the Service Fabric Cluster Resource Manager</span></span>
<span data-ttu-id="0d08e-104">Even if you’ve configured the Cluster Resource Manager correctly, the cluster can get disrupted.</span><span class="sxs-lookup"><span data-stu-id="0d08e-104">Even if you’ve configured the Cluster Resource Manager correctly, the cluster can get disrupted.</span></span> <span data-ttu-id="0d08e-105">For example, there could be simultaneous node or fault domain failures - what would happen if that occurred during an upgrade?</span><span class="sxs-lookup"><span data-stu-id="0d08e-105">For example, there could be simultaneous node or fault domain failures - what would happen if that occurred during an upgrade?</span></span> <span data-ttu-id="0d08e-106">The Cluster Resource Manager tries to fix everything, but this can introduce churn in the cluster.</span><span class="sxs-lookup"><span data-stu-id="0d08e-106">The Cluster Resource Manager tries to fix everything, but this can introduce churn in the cluster.</span></span> <span data-ttu-id="0d08e-107">Throttles help provide a backstop so that the cluster can use resources to stabilize itself - the nodes come back, the network partitions heal, corrected bits get deployed.</span><span class="sxs-lookup"><span data-stu-id="0d08e-107">Throttles help provide a backstop so that the cluster can use resources to stabilize itself - the nodes come back, the network partitions heal, corrected bits get deployed.</span></span>

<span data-ttu-id="0d08e-108">To help with these sorts of situations, the Service Fabric Cluster Resource Manager includes several throttles.</span><span class="sxs-lookup"><span data-stu-id="0d08e-108">To help with these sorts of situations, the Service Fabric Cluster Resource Manager includes several throttles.</span></span> <span data-ttu-id="0d08e-109">These throttles are fairly large hammers.</span><span class="sxs-lookup"><span data-stu-id="0d08e-109">These throttles are fairly large hammers.</span></span> <span data-ttu-id="0d08e-110">These settings shouldn’t be changed from the defaults unless there’s been some careful math done around the amount of work that the cluster can do in parallel.</span><span class="sxs-lookup"><span data-stu-id="0d08e-110">These settings shouldn’t be changed from the defaults unless there’s been some careful math done around the amount of work that the cluster can do in parallel.</span></span>

<span data-ttu-id="0d08e-111">The throttles have default values that the Service Fabric team has found through experience to be ok defaults.</span><span class="sxs-lookup"><span data-stu-id="0d08e-111">The throttles have default values that the Service Fabric team has found through experience to be ok defaults.</span></span> <span data-ttu-id="0d08e-112">If you need to change them you should tune them to your expected actual load.</span><span class="sxs-lookup"><span data-stu-id="0d08e-112">If you need to change them you should tune them to your expected actual load.</span></span> <span data-ttu-id="0d08e-113">You may determine you need to have some throttles in place, even if it means the cluster takes longer to stabilize in mainline situations.</span><span class="sxs-lookup"><span data-stu-id="0d08e-113">You may determine you need to have some throttles in place, even if it means the cluster takes longer to stabilize in mainline situations.</span></span>

## <a name="configuring-the-throttles"></a><span data-ttu-id="0d08e-114">Configuring the throttles</span><span class="sxs-lookup"><span data-stu-id="0d08e-114">Configuring the throttles</span></span>
<span data-ttu-id="0d08e-115">The throttles that are included by default are:</span><span class="sxs-lookup"><span data-stu-id="0d08e-115">The throttles that are included by default are:</span></span>

* <span data-ttu-id="0d08e-116">GlobalMovementThrottleThreshold – this setting controls the total number of movements in the cluster over some time (defined as the GlobalMovementThrottleCountingInterval, value in seconds)</span><span class="sxs-lookup"><span data-stu-id="0d08e-116">GlobalMovementThrottleThreshold – this setting controls the total number of movements in the cluster over some time (defined as the GlobalMovementThrottleCountingInterval, value in seconds)</span></span>
* <span data-ttu-id="0d08e-117">MovementPerPartitionThrottleThreshold – this setting controls the total number of movements for any service partition over some time (the MovementPerPartitionThrottleCountingInterval, value in seconds)</span><span class="sxs-lookup"><span data-stu-id="0d08e-117">MovementPerPartitionThrottleThreshold – this setting controls the total number of movements for any service partition over some time (the MovementPerPartitionThrottleCountingInterval, value in seconds)</span></span>

``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThreshold" Value="1000" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
     <Parameter Name="MovementPerPartitionThrottleThreshold" Value="50" />
     <Parameter Name="MovementPerPartitionThrottleCountingInterval" Value="600" />
</Section>
```

<span data-ttu-id="0d08e-118">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="0d08e-118">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThreshold",
          "value": "1000"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      },
      {
          "name": "MovementPerPartitionThrottleThreshold",
          "value": "50"
      },
      {
          "name": "MovementPerPartitionThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

<span data-ttu-id="0d08e-119">Most of the time we’ve seen customers use these throttles it has been because they were already in a resource constrained environment.</span><span class="sxs-lookup"><span data-stu-id="0d08e-119">Most of the time we’ve seen customers use these throttles it has been because they were already in a resource constrained environment.</span></span> <span data-ttu-id="0d08e-120">Some examples of that environment would be limited network bandwidth into individual nodes, or disks that aren't able to build many replicas in parallel due to throughput limitations.</span><span class="sxs-lookup"><span data-stu-id="0d08e-120">Some examples of that environment would be limited network bandwidth into individual nodes, or disks that aren't able to build many replicas in parallel due to throughput limitations.</span></span> <span data-ttu-id="0d08e-121">These types of restrictions meant that operations triggered in response to failures wouldn’t succeed or would be slow, even without the throttles.</span><span class="sxs-lookup"><span data-stu-id="0d08e-121">These types of restrictions meant that operations triggered in response to failures wouldn’t succeed or would be slow, even without the throttles.</span></span> <span data-ttu-id="0d08e-122">In these situations customers knew they were extending the amount of time it would take the cluster to reach a stable state.</span><span class="sxs-lookup"><span data-stu-id="0d08e-122">In these situations customers knew they were extending the amount of time it would take the cluster to reach a stable state.</span></span> <span data-ttu-id="0d08e-123">Customers also understood they could end up running at lower overall reliability while they were throttled.</span><span class="sxs-lookup"><span data-stu-id="0d08e-123">Customers also understood they could end up running at lower overall reliability while they were throttled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d08e-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d08e-124">Next steps</span></span>
* <span data-ttu-id="0d08e-125">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="0d08e-125">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
* <span data-ttu-id="0d08e-126">The Cluster Resource Manager has many options for describing the cluster.</span><span class="sxs-lookup"><span data-stu-id="0d08e-126">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="0d08e-127">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="0d08e-127">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
