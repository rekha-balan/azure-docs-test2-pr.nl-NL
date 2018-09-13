---
title: Balance your Azure Service Fabric cluster | Microsoft Docs
description: An introduction to balancing your cluster with the Service Fabric Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: c96965b766c8cd32f1061bdae18a95c6379ffdca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671907"
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="bea14-103">Balancing your service fabric cluster</span><span class="sxs-lookup"><span data-stu-id="bea14-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="bea14-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services, correcting constraint violations, and rebalancing the cluster.</span><span class="sxs-lookup"><span data-stu-id="bea14-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services, correcting constraint violations, and rebalancing the cluster.</span></span> <span data-ttu-id="bea14-105">But how often does it do these things, and what triggers it?</span><span class="sxs-lookup"><span data-stu-id="bea14-105">But how often does it do these things, and what triggers it?</span></span>

<span data-ttu-id="bea14-106">The first set of controls around balancing are a set of timers.</span><span class="sxs-lookup"><span data-stu-id="bea14-106">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="bea14-107">These timers govern how often the Cluster Resource Manager examines the state of the cluster for things that need to be addressed.</span><span class="sxs-lookup"><span data-stu-id="bea14-107">These timers govern how often the Cluster Resource Manager examines the state of the cluster for things that need to be addressed.</span></span> <span data-ttu-id="bea14-108">There are three different categories of work, each with their own corresponding timer.</span><span class="sxs-lookup"><span data-stu-id="bea14-108">There are three different categories of work, each with their own corresponding timer.</span></span> <span data-ttu-id="bea14-109">They are:</span><span class="sxs-lookup"><span data-stu-id="bea14-109">They are:</span></span>

1. <span data-ttu-id="bea14-110">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span><span class="sxs-lookup"><span data-stu-id="bea14-110">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="bea14-111">This covers both new services and handling stateful replicas or stateless instances that have failed.</span><span class="sxs-lookup"><span data-stu-id="bea14-111">This covers both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="bea14-112">Deleting and dropping replicas or instances are handled here.</span><span class="sxs-lookup"><span data-stu-id="bea14-112">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="bea14-113">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span><span class="sxs-lookup"><span data-stu-id="bea14-113">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="bea14-114">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span><span class="sxs-lookup"><span data-stu-id="bea14-114">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="bea14-115">Balancing – this stage checks to see if proactive rebalancing is necessary based on the configured desired level of balance for different metrics.</span><span class="sxs-lookup"><span data-stu-id="bea14-115">Balancing – this stage checks to see if proactive rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="bea14-116">If so it attempts to find an arrangement in the cluster that is more balanced.</span><span class="sxs-lookup"><span data-stu-id="bea14-116">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-steps-and-timers"></a><span data-ttu-id="bea14-117">Configuring Cluster Resource Manager Steps and Timers</span><span class="sxs-lookup"><span data-stu-id="bea14-117">Configuring Cluster Resource Manager Steps and Timers</span></span>
<span data-ttu-id="bea14-118">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span><span class="sxs-lookup"><span data-stu-id="bea14-118">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="bea14-119">When each timer fires, the task is scheduled.</span><span class="sxs-lookup"><span data-stu-id="bea14-119">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="bea14-120">By default the Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="bea14-120">By default the Resource Manager:</span></span>

* <span data-ttu-id="bea14-121">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span><span class="sxs-lookup"><span data-stu-id="bea14-121">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="bea14-122">sets the placement and constraint check flags every second</span><span class="sxs-lookup"><span data-stu-id="bea14-122">sets the placement and constraint check flags every second</span></span>
* <span data-ttu-id="bea14-123">sets the balancing flag every five seconds.</span><span class="sxs-lookup"><span data-stu-id="bea14-123">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="bea14-124">We can see this reflected in the following configuration information:</span><span class="sxs-lookup"><span data-stu-id="bea14-124">We can see this reflected in the following configuration information:</span></span>

<span data-ttu-id="bea14-125">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="bea14-125">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="bea14-126">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="bea14-126">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="bea14-127">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially (that’s why we refer to these timers as “minimum intervals”).</span><span class="sxs-lookup"><span data-stu-id="bea14-127">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially (that’s why we refer to these timers as “minimum intervals”).</span></span> <span data-ttu-id="bea14-128">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span><span class="sxs-lookup"><span data-stu-id="bea14-128">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="bea14-129">As you can see by the default time intervals specified, the Cluster Resource Manager scans and checks for anything it needs to do frequently, so the set of changes made at the end of each step is usually small.</span><span class="sxs-lookup"><span data-stu-id="bea14-129">As you can see by the default time intervals specified, the Cluster Resource Manager scans and checks for anything it needs to do frequently, so the set of changes made at the end of each step is usually small.</span></span> <span data-ttu-id="bea14-130">Making small changes frequently makes the Cluster Resource Manager responsive to things that happen in the cluster.</span><span class="sxs-lookup"><span data-stu-id="bea14-130">Making small changes frequently makes the Cluster Resource Manager responsive to things that happen in the cluster.</span></span> <span data-ttu-id="bea14-131">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span><span class="sxs-lookup"><span data-stu-id="bea14-131">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> <span data-ttu-id="bea14-132">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span><span class="sxs-lookup"><span data-stu-id="bea14-132">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="bea14-133">Doing so would lead to bursts of churn.</span><span class="sxs-lookup"><span data-stu-id="bea14-133">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="bea14-134">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span><span class="sxs-lookup"><span data-stu-id="bea14-134">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="bea14-135">For that we have two other pieces of configuration: *Balancing Thresholds* and *Activity Thresholds*.</span><span class="sxs-lookup"><span data-stu-id="bea14-135">For that we have two other pieces of configuration: *Balancing Thresholds* and *Activity Thresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="bea14-136">Balancing thresholds</span><span class="sxs-lookup"><span data-stu-id="bea14-136">Balancing thresholds</span></span>
<span data-ttu-id="bea14-137">A Balancing Threshold is the main control for triggering proactive rebalancing.</span><span class="sxs-lookup"><span data-stu-id="bea14-137">A Balancing Threshold is the main control for triggering proactive rebalancing.</span></span> <span data-ttu-id="bea14-138">The MinLoadBalancingInterval timer is just for how often the Cluster Resource Manager should check - it doesn't mean that anything happens.</span><span class="sxs-lookup"><span data-stu-id="bea14-138">The MinLoadBalancingInterval timer is just for how often the Cluster Resource Manager should check - it doesn't mean that anything happens.</span></span> <span data-ttu-id="bea14-139">The Balancing Threshold defines how imbalanced the cluster needs to be for a specific metric in order for the Cluster Resource Manager to consider it imbalanced and trigger balancing.</span><span class="sxs-lookup"><span data-stu-id="bea14-139">The Balancing Threshold defines how imbalanced the cluster needs to be for a specific metric in order for the Cluster Resource Manager to consider it imbalanced and trigger balancing.</span></span>

<span data-ttu-id="bea14-140">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span><span class="sxs-lookup"><span data-stu-id="bea14-140">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="bea14-141">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bea14-141">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="bea14-142">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="bea14-142">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="bea14-143">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="bea14-143">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="bea14-144">The Balancing Threshold for a metric is a ratio.</span><span class="sxs-lookup"><span data-stu-id="bea14-144">The Balancing Threshold for a metric is a ratio.</span></span> <span data-ttu-id="bea14-145">If the amount of load on the most loaded node divided by the amount of load on the least loaded node exceeds this number, then the cluster is considered imbalanced.</span><span class="sxs-lookup"><span data-stu-id="bea14-145">If the amount of load on the most loaded node divided by the amount of load on the least loaded node exceeds this number, then the cluster is considered imbalanced.</span></span> <span data-ttu-id="bea14-146">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span><span class="sxs-lookup"><span data-stu-id="bea14-146">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="bea14-147"><center>
![Balancing Threshold Example][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="bea14-147"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="bea14-148">In this example, each service is consuming one unit of some metric.</span><span class="sxs-lookup"><span data-stu-id="bea14-148">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="bea14-149">In the top example, the maximum load on a node is five and the minimum is two.</span><span class="sxs-lookup"><span data-stu-id="bea14-149">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="bea14-150">Let’s say that the balancing threshold for this metric is three.</span><span class="sxs-lookup"><span data-stu-id="bea14-150">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="bea14-151">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span><span class="sxs-lookup"><span data-stu-id="bea14-151">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="bea14-152">No balancing is triggered when the Cluster Resource Manager checks.</span><span class="sxs-lookup"><span data-stu-id="bea14-152">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="bea14-153">In the bottom example, the maximum load on a node is ten, while the minimum is two, resulting in a ratio of five.</span><span class="sxs-lookup"><span data-stu-id="bea14-153">In the bottom example, the maximum load on a node is ten, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="bea14-154">Five is greater than the designated balancing threshold of three for that metric.</span><span class="sxs-lookup"><span data-stu-id="bea14-154">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="bea14-155">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span><span class="sxs-lookup"><span data-stu-id="bea14-155">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="bea14-156">In a situation like this some load will almost certainly be distributed to Node3.</span><span class="sxs-lookup"><span data-stu-id="bea14-156">In a situation like this some load will almost certainly be distributed to Node3.</span></span> <span data-ttu-id="bea14-157">Since the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span><span class="sxs-lookup"><span data-stu-id="bea14-157">Since the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> <span data-ttu-id="bea14-158">Doing so results in minimization of the overall differences between nodes, which is one of the goals of the Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bea14-158">Doing so results in minimization of the overall differences between nodes, which is one of the goals of the Cluster Resource Manager.</span></span>

<span data-ttu-id="bea14-159"><center>
![Balancing Threshold Example Actions][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="bea14-159"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

<span data-ttu-id="bea14-160">Getting below the balancing threshold is not an explicit goal.</span><span class="sxs-lookup"><span data-stu-id="bea14-160">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="bea14-161">Balancing Thresholds are just a *trigger* that tells the Cluster Resource Manager that it should look into the cluster to determine what improvements it can make, if any.</span><span class="sxs-lookup"><span data-stu-id="bea14-161">Balancing Thresholds are just a *trigger* that tells the Cluster Resource Manager that it should look into the cluster to determine what improvements it can make, if any.</span></span> <span data-ttu-id="bea14-162">Indeed, just because a balancing search is kicked off doesn't mean anything moves - sometimes the cluster is imbalanced but the situation can't be improved.</span><span class="sxs-lookup"><span data-stu-id="bea14-162">Indeed, just because a balancing search is kicked off doesn't mean anything moves - sometimes the cluster is imbalanced but the situation can't be improved.</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="bea14-163">Activity thresholds</span><span class="sxs-lookup"><span data-stu-id="bea14-163">Activity thresholds</span></span>
<span data-ttu-id="bea14-164">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span><span class="sxs-lookup"><span data-stu-id="bea14-164">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="bea14-165">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span><span class="sxs-lookup"><span data-stu-id="bea14-165">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="bea14-166">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span><span class="sxs-lookup"><span data-stu-id="bea14-166">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="bea14-167">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any *absolute* difference.</span><span class="sxs-lookup"><span data-stu-id="bea14-167">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any *absolute* difference.</span></span> <span data-ttu-id="bea14-168">To avoid this, there’s another control known as Activity Thresholds.</span><span class="sxs-lookup"><span data-stu-id="bea14-168">To avoid this, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="bea14-169">Activity Thresholds allows you to specify some absolute lower bound for activity.</span><span class="sxs-lookup"><span data-stu-id="bea14-169">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="bea14-170">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span><span class="sxs-lookup"><span data-stu-id="bea14-170">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="bea14-171">As an example, let's look at the following diagram.</span><span class="sxs-lookup"><span data-stu-id="bea14-171">As an example, let's look at the following diagram.</span></span> <span data-ttu-id="bea14-172">Let’s also say that we retain our Balancing Threshold of three for this metric, but now we also have an Activity Threshold of 1536.</span><span class="sxs-lookup"><span data-stu-id="bea14-172">Let’s also say that we retain our Balancing Threshold of three for this metric, but now we also have an Activity Threshold of 1536.</span></span> <span data-ttu-id="bea14-173">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span><span class="sxs-lookup"><span data-stu-id="bea14-173">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="bea14-174">In the bottom example, Node1 is way over the Activity Threshold.</span><span class="sxs-lookup"><span data-stu-id="bea14-174">In the bottom example, Node1 is way over the Activity Threshold.</span></span> <span data-ttu-id="bea14-175">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, so balancing is scheduled.</span><span class="sxs-lookup"><span data-stu-id="bea14-175">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, so balancing is scheduled.</span></span>

<span data-ttu-id="bea14-176"><center>
![Activity Threshold Example][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="bea14-176"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="bea14-177">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span><span class="sxs-lookup"><span data-stu-id="bea14-177">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="bea14-178">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="bea14-178">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="bea14-179">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="bea14-179">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="bea14-180">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span><span class="sxs-lookup"><span data-stu-id="bea14-180">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="bea14-181">Balancing services together</span><span class="sxs-lookup"><span data-stu-id="bea14-181">Balancing services together</span></span>
<span data-ttu-id="bea14-182">Something that’s interesting to note is that whether the cluster is imbalanced or not is a cluster-wide decision.</span><span class="sxs-lookup"><span data-stu-id="bea14-182">Something that’s interesting to note is that whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="bea14-183">However, the way we go about fixing it is moving individual service replicas and instances around.</span><span class="sxs-lookup"><span data-stu-id="bea14-183">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="bea14-184">This makes sense, right?</span><span class="sxs-lookup"><span data-stu-id="bea14-184">This makes sense, right?</span></span> <span data-ttu-id="bea14-185">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span><span class="sxs-lookup"><span data-stu-id="bea14-185">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="bea14-186">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span><span class="sxs-lookup"><span data-stu-id="bea14-186">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="bea14-187">Occasionally though, a service that wasn’t imbalanced gets moved.</span><span class="sxs-lookup"><span data-stu-id="bea14-187">Occasionally though, a service that wasn’t imbalanced gets moved.</span></span> <span data-ttu-id="bea14-188">How could it happen that a service gets moved around even if all of that service’s metrics were balanced, even perfectly so, at the time of the other imbalance?</span><span class="sxs-lookup"><span data-stu-id="bea14-188">How could it happen that a service gets moved around even if all of that service’s metrics were balanced, even perfectly so, at the time of the other imbalance?</span></span> <span data-ttu-id="bea14-189">Let’s see!</span><span class="sxs-lookup"><span data-stu-id="bea14-189">Let’s see!</span></span>

<span data-ttu-id="bea14-190">Take for example four services, Service1, Service2, Service3, and Service4.</span><span class="sxs-lookup"><span data-stu-id="bea14-190">Take for example four services, Service1, Service2, Service3, and Service4.</span></span> <span data-ttu-id="bea14-191">Service1 reports against metrics Metric1 and Metric2, Service2 against Metric2 and Mmetric3, Service3 against Metric3 and Metric4, and Service4 against some metric Metric99.</span><span class="sxs-lookup"><span data-stu-id="bea14-191">Service1 reports against metrics Metric1 and Metric2, Service2 against Metric2 and Mmetric3, Service3 against Metric3 and Metric4, and Service4 against some metric Metric99.</span></span> <span data-ttu-id="bea14-192">Surely you can see where we’re going here.</span><span class="sxs-lookup"><span data-stu-id="bea14-192">Surely you can see where we’re going here.</span></span> <span data-ttu-id="bea14-193">We have a chain!</span><span class="sxs-lookup"><span data-stu-id="bea14-193">We have a chain!</span></span> <span data-ttu-id="bea14-194">We don’t really have four independent services, we have a bunch of services that are related (Service1, Service2, and Service3) and one that is off on its own.</span><span class="sxs-lookup"><span data-stu-id="bea14-194">We don’t really have four independent services, we have a bunch of services that are related (Service1, Service2, and Service3) and one that is off on its own.</span></span>

<span data-ttu-id="bea14-195"><center>
![Balancing Services Together][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="bea14-195"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="bea14-196">So it is possible that an imbalance in Metric1 can cause replicas or instances belonging to Service3 (which doesn't report Metric1) to move around.</span><span class="sxs-lookup"><span data-stu-id="bea14-196">So it is possible that an imbalance in Metric1 can cause replicas or instances belonging to Service3 (which doesn't report Metric1) to move around.</span></span> <span data-ttu-id="bea14-197">Usually these movements are limited, but can be larger depending on exactly how imbalanced Metric1 got and what changes were necessary in the cluster to correct it.</span><span class="sxs-lookup"><span data-stu-id="bea14-197">Usually these movements are limited, but can be larger depending on exactly how imbalanced Metric1 got and what changes were necessary in the cluster to correct it.</span></span> <span data-ttu-id="bea14-198">We can also say with certainty that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span><span class="sxs-lookup"><span data-stu-id="bea14-198">We can also say with certainty that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="bea14-199">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1, 2, or 3.</span><span class="sxs-lookup"><span data-stu-id="bea14-199">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1, 2, or 3.</span></span>

<span data-ttu-id="bea14-200">The Cluster Resource Manager automatically figures out what services are related, since services may have been added, removed, or had their metric configuration change.</span><span class="sxs-lookup"><span data-stu-id="bea14-200">The Cluster Resource Manager automatically figures out what services are related, since services may have been added, removed, or had their metric configuration change.</span></span> <span data-ttu-id="bea14-201">For example, between two runs of balancing Service2 may have been reconfigured to remove Metric2.</span><span class="sxs-lookup"><span data-stu-id="bea14-201">For example, between two runs of balancing Service2 may have been reconfigured to remove Metric2.</span></span> <span data-ttu-id="bea14-202">This change breaks the chain between Service1 and Service2.</span><span class="sxs-lookup"><span data-stu-id="bea14-202">This change breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="bea14-203">Now instead of two groups of related services, you have three:</span><span class="sxs-lookup"><span data-stu-id="bea14-203">Now instead of two groups of related services, you have three:</span></span>

<span data-ttu-id="bea14-204"><center>
![Balancing Services Together][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="bea14-204"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="bea14-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="bea14-205">Next steps</span></span>
* <span data-ttu-id="bea14-206">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span><span class="sxs-lookup"><span data-stu-id="bea14-206">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="bea14-207">To learn more about them and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="bea14-207">To learn more about them and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="bea14-208">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span><span class="sxs-lookup"><span data-stu-id="bea14-208">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="bea14-209">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="bea14-209">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="bea14-210">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span><span class="sxs-lookup"><span data-stu-id="bea14-210">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="bea14-211">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="bea14-211">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png





