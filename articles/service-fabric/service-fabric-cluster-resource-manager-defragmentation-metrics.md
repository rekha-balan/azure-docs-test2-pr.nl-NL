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
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 6c6131fcd27f6911ea69b10acf74e1d0414cd7a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789573"
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="1f73d-103">Defragmentation of metrics and load in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1f73d-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="1f73d-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span><span class="sxs-lookup"><span data-stu-id="1f73d-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span></span> <span data-ttu-id="1f73d-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span><span class="sxs-lookup"><span data-stu-id="1f73d-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span></span> <span data-ttu-id="1f73d-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span><span class="sxs-lookup"><span data-stu-id="1f73d-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="1f73d-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span><span class="sxs-lookup"><span data-stu-id="1f73d-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="1f73d-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span><span class="sxs-lookup"><span data-stu-id="1f73d-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span></span> <span data-ttu-id="1f73d-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span><span class="sxs-lookup"><span data-stu-id="1f73d-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span></span>

## <a name="when-to-use-defragmentation"></a><span data-ttu-id="1f73d-110">When to use defragmentation</span><span class="sxs-lookup"><span data-stu-id="1f73d-110">When to use defragmentation</span></span>
<span data-ttu-id="1f73d-111">Distributing load in the cluster consumes some of the resources on each node.</span><span class="sxs-lookup"><span data-stu-id="1f73d-111">Distributing load in the cluster consumes some of the resources on each node.</span></span> <span data-ttu-id="1f73d-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span><span class="sxs-lookup"><span data-stu-id="1f73d-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="1f73d-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span><span class="sxs-lookup"><span data-stu-id="1f73d-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span></span> <span data-ttu-id="1f73d-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span><span class="sxs-lookup"><span data-stu-id="1f73d-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="1f73d-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="1f73d-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="1f73d-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span><span class="sxs-lookup"><span data-stu-id="1f73d-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span></span> <span data-ttu-id="1f73d-118">The Service Fabric team measured creation times in simulations of this scenario.</span><span class="sxs-lookup"><span data-stu-id="1f73d-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="1f73d-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span><span class="sxs-lookup"><span data-stu-id="1f73d-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="1f73d-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span><span class="sxs-lookup"><span data-stu-id="1f73d-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="1f73d-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="1f73d-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span><span class="sxs-lookup"><span data-stu-id="1f73d-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="1f73d-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span></span> <span data-ttu-id="1f73d-124">Not having to reorganize the cluster allows creating large workloads quickly.</span><span class="sxs-lookup"><span data-stu-id="1f73d-124">Not having to reorganize the cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="1f73d-125">Most people don’t need defragmentation.</span><span class="sxs-lookup"><span data-stu-id="1f73d-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="1f73d-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="1f73d-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span><span class="sxs-lookup"><span data-stu-id="1f73d-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="1f73d-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span><span class="sxs-lookup"><span data-stu-id="1f73d-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span></span> <span data-ttu-id="1f73d-129">We'll discuss the tradeoffs of using defragmentation next.</span><span class="sxs-lookup"><span data-stu-id="1f73d-129">We'll discuss the tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="1f73d-130">Defragmentation tradeoffs</span><span class="sxs-lookup"><span data-stu-id="1f73d-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="1f73d-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span><span class="sxs-lookup"><span data-stu-id="1f73d-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="1f73d-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span><span class="sxs-lookup"><span data-stu-id="1f73d-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span></span>

<span data-ttu-id="1f73d-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span><span class="sxs-lookup"><span data-stu-id="1f73d-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="1f73d-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="1f73d-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="1f73d-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span><span class="sxs-lookup"><span data-stu-id="1f73d-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="1f73d-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span><span class="sxs-lookup"><span data-stu-id="1f73d-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="1f73d-137">Defragmentation pros and cons</span><span class="sxs-lookup"><span data-stu-id="1f73d-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="1f73d-138">So what are those other conceptual tradeoffs?</span><span class="sxs-lookup"><span data-stu-id="1f73d-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="1f73d-139">Here’s a quick table of things to think about:</span><span class="sxs-lookup"><span data-stu-id="1f73d-139">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="1f73d-140">Defragmentation Pros</span><span class="sxs-lookup"><span data-stu-id="1f73d-140">Defragmentation Pros</span></span> | <span data-ttu-id="1f73d-141">Defragmentation Cons</span><span class="sxs-lookup"><span data-stu-id="1f73d-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="1f73d-142">Allows faster creation of large services</span><span class="sxs-lookup"><span data-stu-id="1f73d-142">Allows faster creation of large services</span></span> |<span data-ttu-id="1f73d-143">Concentrates load onto fewer nodes, increasing contention</span><span class="sxs-lookup"><span data-stu-id="1f73d-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="1f73d-144">Enables lower data movement during creation</span><span class="sxs-lookup"><span data-stu-id="1f73d-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="1f73d-145">Failures can impact more services and cause more churn</span><span class="sxs-lookup"><span data-stu-id="1f73d-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="1f73d-146">Allows rich description of requirements and reclamation of space</span><span class="sxs-lookup"><span data-stu-id="1f73d-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="1f73d-147">More complex overall Resource Management configuration</span><span class="sxs-lookup"><span data-stu-id="1f73d-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="1f73d-148">You can mix defragmented and normal metrics in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-148">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="1f73d-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span><span class="sxs-lookup"><span data-stu-id="1f73d-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="1f73d-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span><span class="sxs-lookup"><span data-stu-id="1f73d-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="1f73d-151">the number of balancing metrics vs. the number of defragmentation metrics</span><span class="sxs-lookup"><span data-stu-id="1f73d-151">the number of balancing metrics vs. the number of defragmentation metrics</span></span>
  - <span data-ttu-id="1f73d-152">Whether any service uses both types of metrics</span><span class="sxs-lookup"><span data-stu-id="1f73d-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="1f73d-153">the metric weights</span><span class="sxs-lookup"><span data-stu-id="1f73d-153">the metric weights</span></span>
  - <span data-ttu-id="1f73d-154">current metric loads</span><span class="sxs-lookup"><span data-stu-id="1f73d-154">current metric loads</span></span>
  
<span data-ttu-id="1f73d-155">Experimentation is required to determine the exact configuration necessary.</span><span class="sxs-lookup"><span data-stu-id="1f73d-155">Experimentation is required to determine the exact configuration necessary.</span></span> <span data-ttu-id="1f73d-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span><span class="sxs-lookup"><span data-stu-id="1f73d-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="1f73d-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span><span class="sxs-lookup"><span data-stu-id="1f73d-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="1f73d-158">Configuring defragmentation metrics</span><span class="sxs-lookup"><span data-stu-id="1f73d-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="1f73d-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span><span class="sxs-lookup"><span data-stu-id="1f73d-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="1f73d-160">The following config snippets show how to configure metrics for defragmentation.</span><span class="sxs-lookup"><span data-stu-id="1f73d-160">The following config snippets show how to configure metrics for defragmentation.</span></span> <span data-ttu-id="1f73d-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span><span class="sxs-lookup"><span data-stu-id="1f73d-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span></span> 

<span data-ttu-id="1f73d-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="1f73d-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="1f73d-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="1f73d-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="1f73d-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f73d-164">Next steps</span></span>
- <span data-ttu-id="1f73d-165">The Cluster Resource Manager has man options for describing the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-165">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="1f73d-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="1f73d-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="1f73d-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f73d-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="1f73d-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="1f73d-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
