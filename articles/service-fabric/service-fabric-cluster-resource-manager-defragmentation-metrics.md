---
title: Defragmentation of Metrics in Azure Service Fabric | Microsoft Docs
description: An overview of using defragmentation or packing as a strategy for metrics in Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: 6f49df0f0d713504943a813dfbcb0254b4762749
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564652"
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="5cbae-103">Defragmentation of metrics and load in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5cbae-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="5cbae-104">The Service Fabric Cluster Resource Manager mainly is concerned with balancing in terms of distributing the load – making sure that the nodes in the cluster are equally utilized.</span><span class="sxs-lookup"><span data-stu-id="5cbae-104">The Service Fabric Cluster Resource Manager mainly is concerned with balancing in terms of distributing the load – making sure that the nodes in the cluster are equally utilized.</span></span> <span data-ttu-id="5cbae-105">Having workloads distributed is the safest layout in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span><span class="sxs-lookup"><span data-stu-id="5cbae-105">Having workloads distributed is the safest layout in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> <span data-ttu-id="5cbae-106">The Service Fabric Cluster Resource Manager does support a different strategy as well, which is defragmentation.</span><span class="sxs-lookup"><span data-stu-id="5cbae-106">The Service Fabric Cluster Resource Manager does support a different strategy as well, which is defragmentation.</span></span> <span data-ttu-id="5cbae-107">Defragmentation generally means that instead of trying to distribute the utilization of a metric across the cluster, we should actually try to consolidate it.</span><span class="sxs-lookup"><span data-stu-id="5cbae-107">Defragmentation generally means that instead of trying to distribute the utilization of a metric across the cluster, we should actually try to consolidate it.</span></span> <span data-ttu-id="5cbae-108">Consolidation is a fortunate inversion of our normal strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager aims for increases in deviation.</span><span class="sxs-lookup"><span data-stu-id="5cbae-108">Consolidation is a fortunate inversion of our normal strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager aims for increases in deviation.</span></span> <span data-ttu-id="5cbae-109">But why would you want this strategy?</span><span class="sxs-lookup"><span data-stu-id="5cbae-109">But why would you want this strategy?</span></span>

<span data-ttu-id="5cbae-110">Well, if you’ve spread the load out evenly among the nodes in the cluster then you’ve eaten up some of the resources that the nodes have to offer.</span><span class="sxs-lookup"><span data-stu-id="5cbae-110">Well, if you’ve spread the load out evenly among the nodes in the cluster then you’ve eaten up some of the resources that the nodes have to offer.</span></span> <span data-ttu-id="5cbae-111">However, some workloads create services that are exceptionally large and consume most of a node.</span><span class="sxs-lookup"><span data-stu-id="5cbae-111">However, some workloads create services that are exceptionally large and consume most of a node.</span></span> <span data-ttu-id="5cbae-112">In these cases it's possible 75% to 95% of a node’s resources end up dedicated to a single service object.</span><span class="sxs-lookup"><span data-stu-id="5cbae-112">In these cases it's possible 75% to 95% of a node’s resources end up dedicated to a single service object.</span></span> <span data-ttu-id="5cbae-113">Large workloads aren't a problem.</span><span class="sxs-lookup"><span data-stu-id="5cbae-113">Large workloads aren't a problem.</span></span> <span data-ttu-id="5cbae-114">The Cluster Resource Manager determines at service creation time that it needs to reorganize the cluster to make room for this large workload.</span><span class="sxs-lookup"><span data-stu-id="5cbae-114">The Cluster Resource Manager determines at service creation time that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="5cbae-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="5cbae-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="5cbae-117">This is likely if other workloads in the cluster are large and hence take longer to move around.</span><span class="sxs-lookup"><span data-stu-id="5cbae-117">This is likely if other workloads in the cluster are large and hence take longer to move around.</span></span> <span data-ttu-id="5cbae-118">The Service Fabric team measured creation times in simulations of this scenario.</span><span class="sxs-lookup"><span data-stu-id="5cbae-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="5cbae-119">We found that if services were large enough and the cluster was highly utilized that the creation of those large services would be slow.</span><span class="sxs-lookup"><span data-stu-id="5cbae-119">We found that if services were large enough and the cluster was highly utilized that the creation of those large services would be slow.</span></span> <span data-ttu-id="5cbae-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span><span class="sxs-lookup"><span data-stu-id="5cbae-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="5cbae-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="5cbae-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span><span class="sxs-lookup"><span data-stu-id="5cbae-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="5cbae-123">This helps ensure that there is (almost) always room for even large services.</span><span class="sxs-lookup"><span data-stu-id="5cbae-123">This helps ensure that there is (almost) always room for even large services.</span></span> <span data-ttu-id="5cbae-124">This allows such services to be created quickly when necessary.</span><span class="sxs-lookup"><span data-stu-id="5cbae-124">This allows such services to be created quickly when necessary.</span></span>

<span data-ttu-id="5cbae-125">Most people don’t need defragmentation.</span><span class="sxs-lookup"><span data-stu-id="5cbae-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="5cbae-126">Services should usually be small, and hence it’s not hard to find room for them in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-126">Services should usually be small, and hence it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="5cbae-127">However, if you have large services and need them created quickly (and are willing to accept the other tradeoffs) then the defragmentation strategy is for you.</span><span class="sxs-lookup"><span data-stu-id="5cbae-127">However, if you have large services and need them created quickly (and are willing to accept the other tradeoffs) then the defragmentation strategy is for you.</span></span>

<span data-ttu-id="5cbae-128">So what are the tradeoffs?</span><span class="sxs-lookup"><span data-stu-id="5cbae-128">So what are the tradeoffs?</span></span> <span data-ttu-id="5cbae-129">Mainly defragmentation can increase impactfulness of failures (since more services are running on the node that fails).</span><span class="sxs-lookup"><span data-stu-id="5cbae-129">Mainly defragmentation can increase impactfulness of failures (since more services are running on the node that fails).</span></span> <span data-ttu-id="5cbae-130">Furthermore, defragmentation ensures that some resources in the cluster are unutilized while they wait for workloads to be scheduled.</span><span class="sxs-lookup"><span data-stu-id="5cbae-130">Furthermore, defragmentation ensures that some resources in the cluster are unutilized while they wait for workloads to be scheduled.</span></span>

<span data-ttu-id="5cbae-131">The following diagram gives a visual representation of two different clusters, one that is defragmented and one that is not.</span><span class="sxs-lookup"><span data-stu-id="5cbae-131">The following diagram gives a visual representation of two different clusters, one that is defragmented and one that is not.</span></span> <span data-ttu-id="5cbae-132">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span><span class="sxs-lookup"><span data-stu-id="5cbae-132">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="5cbae-133">Compare that to the defragmented cluster, where the large workload could be immediately placed on nodes four or five.</span><span class="sxs-lookup"><span data-stu-id="5cbae-133">Compare that to the defragmented cluster, where the large workload could be immediately placed on nodes four or five.</span></span>

<span data-ttu-id="5cbae-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5cbae-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="5cbae-135">Defragmentation pros and cons</span><span class="sxs-lookup"><span data-stu-id="5cbae-135">Defragmentation pros and cons</span></span>
<span data-ttu-id="5cbae-136">So what are those other conceptual tradeoffs?</span><span class="sxs-lookup"><span data-stu-id="5cbae-136">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="5cbae-137">We recommend thorough measurement of your workloads before turning on defragmentation metrics.</span><span class="sxs-lookup"><span data-stu-id="5cbae-137">We recommend thorough measurement of your workloads before turning on defragmentation metrics.</span></span> <span data-ttu-id="5cbae-138">Here’s a quick table of things to think about:</span><span class="sxs-lookup"><span data-stu-id="5cbae-138">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="5cbae-139">Defragmentation Pros</span><span class="sxs-lookup"><span data-stu-id="5cbae-139">Defragmentation Pros</span></span> | <span data-ttu-id="5cbae-140">Defragmentation Cons</span><span class="sxs-lookup"><span data-stu-id="5cbae-140">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="5cbae-141">Allows faster creation of large services</span><span class="sxs-lookup"><span data-stu-id="5cbae-141">Allows faster creation of large services</span></span> |<span data-ttu-id="5cbae-142">Concentrates load onto fewer nodes, increasing contention</span><span class="sxs-lookup"><span data-stu-id="5cbae-142">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="5cbae-143">Enables lower data movement during creation</span><span class="sxs-lookup"><span data-stu-id="5cbae-143">Enables lower data movement during creation</span></span> |<span data-ttu-id="5cbae-144">Failures can impact more services and cause more churn</span><span class="sxs-lookup"><span data-stu-id="5cbae-144">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="5cbae-145">Allows rich description of requirements and reclamation of space</span><span class="sxs-lookup"><span data-stu-id="5cbae-145">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="5cbae-146">More complex overall Resource Management configuration</span><span class="sxs-lookup"><span data-stu-id="5cbae-146">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="5cbae-147">You can mix defragmented and normal metrics in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-147">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="5cbae-148">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span><span class="sxs-lookup"><span data-stu-id="5cbae-148">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="5cbae-149">If there are no services that share those metrics results can be good.</span><span class="sxs-lookup"><span data-stu-id="5cbae-149">If there are no services that share those metrics results can be good.</span></span> <span data-ttu-id="5cbae-150">The exact results will depend on the number of balancing metrics compared to the number of defragmentation metrics, how much they overlap, their weights, current loads, and other factors.</span><span class="sxs-lookup"><span data-stu-id="5cbae-150">The exact results will depend on the number of balancing metrics compared to the number of defragmentation metrics, how much they overlap, their weights, current loads, and other factors.</span></span> <span data-ttu-id="5cbae-151">Experimentation is required to determine the exact configuration necessary.</span><span class="sxs-lookup"><span data-stu-id="5cbae-151">Experimentation is required to determine the exact configuration necessary.</span></span>

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="5cbae-152">Configuring defragmentation metrics</span><span class="sxs-lookup"><span data-stu-id="5cbae-152">Configuring defragmentation metrics</span></span>
<span data-ttu-id="5cbae-153">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation:</span><span class="sxs-lookup"><span data-stu-id="5cbae-153">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation:</span></span>

<span data-ttu-id="5cbae-154">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5cbae-154">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Disk" Value="true" />
    <Parameter Name="CPU" Value="false" />
</Section>
```

<span data-ttu-id="5cbae-155">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="5cbae-155">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Disk",
          "value": "true"
      },
      {
          "name": "CPU",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="5cbae-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="5cbae-156">Next steps</span></span>
* <span data-ttu-id="5cbae-157">The Cluster Resource Manager has man options for describing the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-157">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="5cbae-158">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="5cbae-158">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
* <span data-ttu-id="5cbae-159">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5cbae-159">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="5cbae-160">To learn more about them and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="5cbae-160">To learn more about them and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png

