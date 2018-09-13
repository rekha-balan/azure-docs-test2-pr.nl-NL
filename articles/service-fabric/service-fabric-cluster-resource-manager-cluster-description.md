---
title: Resource Balancer cluster description | Microsoft Docs
description: Describing a Service Fabric cluster by specifying Fault Domains, Upgrade Domains, node properties, and node capacities to the Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: 704bd53a254dd930c500432cea45074ff2d19d82
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549090"
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="40fab-103">Describing a service fabric cluster</span><span class="sxs-lookup"><span data-stu-id="40fab-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="40fab-104">The Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-104">The Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="40fab-105">During runtime, the Cluster Resource Manager uses this information to ensure high availability of the services running in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-105">During runtime, the Cluster Resource Manager uses this information to ensure high availability of the services running in the cluster.</span></span> <span data-ttu-id="40fab-106">While enforcing these important rules, it also attempts to optimize the cluster's resource consumption.</span><span class="sxs-lookup"><span data-stu-id="40fab-106">While enforcing these important rules, it also attempts to optimize the cluster's resource consumption.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="40fab-107">Key concepts</span><span class="sxs-lookup"><span data-stu-id="40fab-107">Key concepts</span></span>
<span data-ttu-id="40fab-108">The Cluster Resource Manager supports several features that describe a cluster:</span><span class="sxs-lookup"><span data-stu-id="40fab-108">The Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="40fab-109">Fault Domains</span><span class="sxs-lookup"><span data-stu-id="40fab-109">Fault Domains</span></span>
* <span data-ttu-id="40fab-110">Upgrade Domains</span><span class="sxs-lookup"><span data-stu-id="40fab-110">Upgrade Domains</span></span>
* <span data-ttu-id="40fab-111">Node Properties</span><span class="sxs-lookup"><span data-stu-id="40fab-111">Node Properties</span></span>
* <span data-ttu-id="40fab-112">Node Capacities</span><span class="sxs-lookup"><span data-stu-id="40fab-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="40fab-113">Fault domains</span><span class="sxs-lookup"><span data-stu-id="40fab-113">Fault domains</span></span>
<span data-ttu-id="40fab-114">A Fault Domain is any area of coordinated failure.</span><span class="sxs-lookup"><span data-stu-id="40fab-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="40fab-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures to drive failures to bad NIC firmware).</span><span class="sxs-lookup"><span data-stu-id="40fab-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures to drive failures to bad NIC firmware).</span></span> <span data-ttu-id="40fab-116">Machines connected to the same Ethernet switch are in the same Fault Domain, as are those machines sharing a single source of power.</span><span class="sxs-lookup"><span data-stu-id="40fab-116">Machines connected to the same Ethernet switch are in the same Fault Domain, as are those machines sharing a single source of power.</span></span> <span data-ttu-id="40fab-117">Since it's natural for hardware faults to overlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="40fab-117">Since it's natural for hardware faults to overlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="40fab-118">When you set up your own cluster, you need to think through these different areas of failure.</span><span class="sxs-lookup"><span data-stu-id="40fab-118">When you set up your own cluster, you need to think through these different areas of failure.</span></span> <span data-ttu-id="40fab-119">It is important that Fault Domains are set up correctly since Service Fabric uses this information to safely place services.</span><span class="sxs-lookup"><span data-stu-id="40fab-119">It is important that Fault Domains are set up correctly since Service Fabric uses this information to safely place services.</span></span> <span data-ttu-id="40fab-120">Service Fabric doesn't want to place services such that the loss of a Fault Domain (caused by the failure of some component) causes services to go down.</span><span class="sxs-lookup"><span data-stu-id="40fab-120">Service Fabric doesn't want to place services such that the loss of a Fault Domain (caused by the failure of some component) causes services to go down.</span></span> <span data-ttu-id="40fab-121">In the Azure environment Service Fabric uses the Fault Domain information provided by the environment to correctly configure the nodes in the cluster on your behalf.</span><span class="sxs-lookup"><span data-stu-id="40fab-121">In the Azure environment Service Fabric uses the Fault Domain information provided by the environment to correctly configure the nodes in the cluster on your behalf.</span></span>

<span data-ttu-id="40fab-122">In the graphic below we color all the entities that contribute to Fault Domains and list all the different Fault Domains that result.</span><span class="sxs-lookup"><span data-stu-id="40fab-122">In the graphic below we color all the entities that contribute to Fault Domains and list all the different Fault Domains that result.</span></span> <span data-ttu-id="40fab-123">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span><span class="sxs-lookup"><span data-stu-id="40fab-123">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="40fab-124">Conceivably, if each blade holds more than one virtual machine, there could be another layer in the Fault Domain hierarchy.</span><span class="sxs-lookup"><span data-stu-id="40fab-124">Conceivably, if each blade holds more than one virtual machine, there could be another layer in the Fault Domain hierarchy.</span></span>

<span data-ttu-id="40fab-125"><center>
![Nodes organized via Fault Domains][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-125"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="40fab-126">During runtime, the Service Fabric Cluster Resource Manager considers the Fault Domains in the cluster and plans a layout.</span><span class="sxs-lookup"><span data-stu-id="40fab-126">During runtime, the Service Fabric Cluster Resource Manager considers the Fault Domains in the cluster and plans a layout.</span></span>  <span data-ttu-id="40fab-127">It attempts to spread out the stateful replicas or stateless instances for a given service so that they are in separate Fault Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-127">It attempts to spread out the stateful replicas or stateless instances for a given service so that they are in separate Fault Domains.</span></span> <span data-ttu-id="40fab-128">This process helps ensure that if there is a failure of any one Fault Domain (at any level in the hierarchy), that the availability of that service is not compromised.</span><span class="sxs-lookup"><span data-stu-id="40fab-128">This process helps ensure that if there is a failure of any one Fault Domain (at any level in the hierarchy), that the availability of that service is not compromised.</span></span>

<span data-ttu-id="40fab-129">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in the Fault Domain hierarchy.</span><span class="sxs-lookup"><span data-stu-id="40fab-129">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in the Fault Domain hierarchy.</span></span> <span data-ttu-id="40fab-130">However, it tries to ensure that the loss of any one portion of the hierarchy doesn’t impact the services running on top of it.</span><span class="sxs-lookup"><span data-stu-id="40fab-130">However, it tries to ensure that the loss of any one portion of the hierarchy doesn’t impact the services running on top of it.</span></span> <span data-ttu-id="40fab-131">Because of this, it is best if there are the same number of nodes at each level of depth in the Fault Domain hierarchy.</span><span class="sxs-lookup"><span data-stu-id="40fab-131">Because of this, it is best if there are the same number of nodes at each level of depth in the Fault Domain hierarchy.</span></span> <span data-ttu-id="40fab-132">Keeping the levels balanced prevents one portion of the hierarchy from containing more services than others.</span><span class="sxs-lookup"><span data-stu-id="40fab-132">Keeping the levels balanced prevents one portion of the hierarchy from containing more services than others.</span></span> <span data-ttu-id="40fab-133">Doing otherwise would contribute to imbalances in the load of individual nodes and make the failure of certain domains more critical than others.</span><span class="sxs-lookup"><span data-stu-id="40fab-133">Doing otherwise would contribute to imbalances in the load of individual nodes and make the failure of certain domains more critical than others.</span></span>

<span data-ttu-id="40fab-134">If the “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for the Cluster Resource Manager to figure the best allocation of services.</span><span class="sxs-lookup"><span data-stu-id="40fab-134">If the “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for the Cluster Resource Manager to figure the best allocation of services.</span></span> <span data-ttu-id="40fab-135">Imbalanced Fault Domains layouts mean that the loss of a particular domain can impact the availability of the cluster more than others.</span><span class="sxs-lookup"><span data-stu-id="40fab-135">Imbalanced Fault Domains layouts mean that the loss of a particular domain can impact the availability of the cluster more than others.</span></span> <span data-ttu-id="40fab-136">As a result, the Cluster Resource Manager is torn between its two goals: It was to use the machines in that “heavy” domain by placing services on them, and it wants to place services so that the loss of a domain doesn’t cause problems.</span><span class="sxs-lookup"><span data-stu-id="40fab-136">As a result, the Cluster Resource Manager is torn between its two goals: It was to use the machines in that “heavy” domain by placing services on them, and it wants to place services so that the loss of a domain doesn’t cause problems.</span></span> <span data-ttu-id="40fab-137">What does this look like?</span><span class="sxs-lookup"><span data-stu-id="40fab-137">What does this look like?</span></span>

<span data-ttu-id="40fab-138"><center>
![Two different cluster layouts][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-138"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="40fab-139">In the diagram above, we show two different example cluster layouts.</span><span class="sxs-lookup"><span data-stu-id="40fab-139">In the diagram above, we show two different example cluster layouts.</span></span> <span data-ttu-id="40fab-140">In the first example the nodes are distributed evenly across the Fault Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-140">In the first example the nodes are distributed evenly across the Fault Domains.</span></span> <span data-ttu-id="40fab-141">In the other one Fault Domain ends up with many more nodes.</span><span class="sxs-lookup"><span data-stu-id="40fab-141">In the other one Fault Domain ends up with many more nodes.</span></span> <span data-ttu-id="40fab-142">If you ever stand up your own cluster on-premise or in another environment, it’s something you have to think about.</span><span class="sxs-lookup"><span data-stu-id="40fab-142">If you ever stand up your own cluster on-premise or in another environment, it’s something you have to think about.</span></span>

<span data-ttu-id="40fab-143">In Azure the choice of which Fault Domain contains a node is managed for you.</span><span class="sxs-lookup"><span data-stu-id="40fab-143">In Azure the choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="40fab-144">However, depending on the number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span><span class="sxs-lookup"><span data-stu-id="40fab-144">However, depending on the number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="40fab-145">For example, say you have five Fault Domains but provision seven nodes for a given NodeType.</span><span class="sxs-lookup"><span data-stu-id="40fab-145">For example, say you have five Fault Domains but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="40fab-146">In this case the first two Fault Domains end up with more nodes.</span><span class="sxs-lookup"><span data-stu-id="40fab-146">In this case the first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="40fab-147">If you continue to deploy more NodeTypes with only a couple instances, the problem gets worse.</span><span class="sxs-lookup"><span data-stu-id="40fab-147">If you continue to deploy more NodeTypes with only a couple instances, the problem gets worse.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="40fab-148">Upgrade domains</span><span class="sxs-lookup"><span data-stu-id="40fab-148">Upgrade domains</span></span>
<span data-ttu-id="40fab-149">Upgrade Domains are another feature that helps the Service Fabric Cluster Resource Manager understand the layout of the cluster so that it can plan ahead for failures.</span><span class="sxs-lookup"><span data-stu-id="40fab-149">Upgrade Domains are another feature that helps the Service Fabric Cluster Resource Manager understand the layout of the cluster so that it can plan ahead for failures.</span></span> <span data-ttu-id="40fab-150">Upgrade Domains define sets of nodes that are upgraded at the same time.</span><span class="sxs-lookup"><span data-stu-id="40fab-150">Upgrade Domains define sets of nodes that are upgraded at the same time.</span></span>

<span data-ttu-id="40fab-151">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span><span class="sxs-lookup"><span data-stu-id="40fab-151">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="40fab-152">First, while Fault Domains are rigorously defined by the areas of coordinated hardware failures, Upgrade Domains are defined by policy.</span><span class="sxs-lookup"><span data-stu-id="40fab-152">First, while Fault Domains are rigorously defined by the areas of coordinated hardware failures, Upgrade Domains are defined by policy.</span></span> <span data-ttu-id="40fab-153">With Upgrade Domains, you get to decide how many you want rather than it being dictated by the environment.</span><span class="sxs-lookup"><span data-stu-id="40fab-153">With Upgrade Domains, you get to decide how many you want rather than it being dictated by the environment.</span></span> <span data-ttu-id="40fab-154">Another difference is that (today at least) Upgrade Domains are not hierarchical – they are more like a simple tag.</span><span class="sxs-lookup"><span data-stu-id="40fab-154">Another difference is that (today at least) Upgrade Domains are not hierarchical – they are more like a simple tag.</span></span>

<span data-ttu-id="40fab-155">The following diagram shows three Upgrade Domains are striped across three Fault Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-155">The following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="40fab-156">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-156">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="40fab-157">This placement allows us to lose a Fault Domain while in the middle of a service upgrade and still have one copy of the code and data.</span><span class="sxs-lookup"><span data-stu-id="40fab-157">This placement allows us to lose a Fault Domain while in the middle of a service upgrade and still have one copy of the code and data.</span></span>

<span data-ttu-id="40fab-158"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-158"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="40fab-159">There are pros and cons to having large numbers of Upgrade Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-159">There are pros and cons to having large numbers of Upgrade Domains.</span></span> <span data-ttu-id="40fab-160">With more Upgrade Domains each step of the upgrade is more granular and therefore affects a smaller number of nodes or services.</span><span class="sxs-lookup"><span data-stu-id="40fab-160">With more Upgrade Domains each step of the upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="40fab-161">This results in fewer services having to move at a time, introducing less churn into the system.</span><span class="sxs-lookup"><span data-stu-id="40fab-161">This results in fewer services having to move at a time, introducing less churn into the system.</span></span> <span data-ttu-id="40fab-162">This tends to also improve reliability (since less of the service is impacted by any issue introduced during the upgrade).</span><span class="sxs-lookup"><span data-stu-id="40fab-162">This tends to also improve reliability (since less of the service is impacted by any issue introduced during the upgrade).</span></span> <span data-ttu-id="40fab-163">More Upgrade Domains also means that you need less available overhead on other nodes to handle the impact of the upgrade.</span><span class="sxs-lookup"><span data-stu-id="40fab-163">More Upgrade Domains also means that you need less available overhead on other nodes to handle the impact of the upgrade.</span></span> <span data-ttu-id="40fab-164">For example, if you have five Upgrade Domains, the nodes in each are handling roughly 20% of your traffic.</span><span class="sxs-lookup"><span data-stu-id="40fab-164">For example, if you have five Upgrade Domains, the nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="40fab-165">If you need to take down that Upgrade Domain for an upgrade, that load needs to go somewhere.</span><span class="sxs-lookup"><span data-stu-id="40fab-165">If you need to take down that Upgrade Domain for an upgrade, that load needs to go somewhere.</span></span> <span data-ttu-id="40fab-166">More Upgrade Domains means less overhead that must be maintained on the other nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-166">More Upgrade Domains means less overhead that must be maintained on the other nodes in the cluster.</span></span>

<span data-ttu-id="40fab-167">The downside of having many Upgrade Domains is that upgrades tend to take longer.</span><span class="sxs-lookup"><span data-stu-id="40fab-167">The downside of having many Upgrade Domains is that upgrades tend to take longer.</span></span> <span data-ttu-id="40fab-168">Service Fabric waits a short period of time after an Upgrade Domain is completed before proceeding.</span><span class="sxs-lookup"><span data-stu-id="40fab-168">Service Fabric waits a short period of time after an Upgrade Domain is completed before proceeding.</span></span> <span data-ttu-id="40fab-169">This delay is so that issues introduced by the upgrade have a chance to show up and be detected.</span><span class="sxs-lookup"><span data-stu-id="40fab-169">This delay is so that issues introduced by the upgrade have a chance to show up and be detected.</span></span> <span data-ttu-id="40fab-170">The tradeoff is acceptable because it prevents bad changes from affecting too much of the service at a time.</span><span class="sxs-lookup"><span data-stu-id="40fab-170">The tradeoff is acceptable because it prevents bad changes from affecting too much of the service at a time.</span></span>

<span data-ttu-id="40fab-171">Too few Upgrade Domains has its own side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span><span class="sxs-lookup"><span data-stu-id="40fab-171">Too few Upgrade Domains has its own side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="40fab-172">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span><span class="sxs-lookup"><span data-stu-id="40fab-172">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="40fab-173">Having so much of your service down at once isn’t desirable since you have to have enough capacity in the rest of your cluster to handle the workload.</span><span class="sxs-lookup"><span data-stu-id="40fab-173">Having so much of your service down at once isn’t desirable since you have to have enough capacity in the rest of your cluster to handle the workload.</span></span> <span data-ttu-id="40fab-174">Maintaining that buffer means that in the normal case those nodes are less-loaded than they would otherwise be, increasing the cost of running your service.</span><span class="sxs-lookup"><span data-stu-id="40fab-174">Maintaining that buffer means that in the normal case those nodes are less-loaded than they would otherwise be, increasing the cost of running your service.</span></span>

<span data-ttu-id="40fab-175">There’s no real limit to the total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span><span class="sxs-lookup"><span data-stu-id="40fab-175">There’s no real limit to the total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="40fab-176">Common structures that we’ve seen are:</span><span class="sxs-lookup"><span data-stu-id="40fab-176">Common structures that we’ve seen are:</span></span>

* <span data-ttu-id="40fab-177">Fault Domains and Upgrade Domains mapped 1:1</span><span class="sxs-lookup"><span data-stu-id="40fab-177">Fault Domains and Upgrade Domains mapped 1:1</span></span>
* <span data-ttu-id="40fab-178">One Upgrade Domain per Node (physical or virtual OS instance)</span><span class="sxs-lookup"><span data-stu-id="40fab-178">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
* <span data-ttu-id="40fab-179">A “striped” or “matrix” model where the Fault Domains and Upgrade Domains form a matrix with machines usually running down the diagonals</span><span class="sxs-lookup"><span data-stu-id="40fab-179">A “striped” or “matrix” model where the Fault Domains and Upgrade Domains form a matrix with machines usually running down the diagonals</span></span>

<span data-ttu-id="40fab-180"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-180"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="40fab-181">There’s no best answer which layout to choose, each has some pros and cons.</span><span class="sxs-lookup"><span data-stu-id="40fab-181">There’s no best answer which layout to choose, each has some pros and cons.</span></span> <span data-ttu-id="40fab-182">For example, the 1FD:1UD model is fairly simple to set up.</span><span class="sxs-lookup"><span data-stu-id="40fab-182">For example, the 1FD:1UD model is fairly simple to set up.</span></span> <span data-ttu-id="40fab-183">The 1 UD per Node model is most like what people are used to from managing small sets of machines in the past where each would be taken down independently.</span><span class="sxs-lookup"><span data-stu-id="40fab-183">The 1 UD per Node model is most like what people are used to from managing small sets of machines in the past where each would be taken down independently.</span></span>

<span data-ttu-id="40fab-184">The most common model (and the one used in Azure) is the FD/UD matrix, where the FDs and UDs form a table and nodes are placed starting along the diagonal.</span><span class="sxs-lookup"><span data-stu-id="40fab-184">The most common model (and the one used in Azure) is the FD/UD matrix, where the FDs and UDs form a table and nodes are placed starting along the diagonal.</span></span> <span data-ttu-id="40fab-185">Whether this ends up sparse or packed depends on the total number of nodes compared to the number of FDs and UDs.</span><span class="sxs-lookup"><span data-stu-id="40fab-185">Whether this ends up sparse or packed depends on the total number of nodes compared to the number of FDs and UDs.</span></span> <span data-ttu-id="40fab-186">Put differently, for sufficiently large clusters, almost everything ends up looking like the dense matrix pattern, shown in the bottom right option of the image above.</span><span class="sxs-lookup"><span data-stu-id="40fab-186">Put differently, for sufficiently large clusters, almost everything ends up looking like the dense matrix pattern, shown in the bottom right option of the image above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="40fab-187">Fault and Upgrade Domain constraints and resulting behavior</span><span class="sxs-lookup"><span data-stu-id="40fab-187">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="40fab-188">The Cluster Resource Manager treats the desire to keep a service balanced across fault and Upgrade Domains as a constraint.</span><span class="sxs-lookup"><span data-stu-id="40fab-188">The Cluster Resource Manager treats the desire to keep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="40fab-189">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span><span class="sxs-lookup"><span data-stu-id="40fab-189">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="40fab-190">The Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in the number of service objects (stateless service instances or stateful service replicas) between two domains."</span><span class="sxs-lookup"><span data-stu-id="40fab-190">The Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in the number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span>  <span data-ttu-id="40fab-191">Practically what this means is that for a given service certain moves or arrangements might not be valid, because they would violate the Fault or Upgrade Domain constraints.</span><span class="sxs-lookup"><span data-stu-id="40fab-191">Practically what this means is that for a given service certain moves or arrangements might not be valid, because they would violate the Fault or Upgrade Domain constraints.</span></span>

<span data-ttu-id="40fab-192">Let's look at one example.</span><span class="sxs-lookup"><span data-stu-id="40fab-192">Let's look at one example.</span></span> <span data-ttu-id="40fab-193">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span><span class="sxs-lookup"><span data-stu-id="40fab-193">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="40fab-194">FD0</span><span class="sxs-lookup"><span data-stu-id="40fab-194">FD0</span></span> | <span data-ttu-id="40fab-195">FD1</span><span class="sxs-lookup"><span data-stu-id="40fab-195">FD1</span></span> | <span data-ttu-id="40fab-196">FD2</span><span class="sxs-lookup"><span data-stu-id="40fab-196">FD2</span></span> | <span data-ttu-id="40fab-197">FD3</span><span class="sxs-lookup"><span data-stu-id="40fab-197">FD3</span></span> | <span data-ttu-id="40fab-198">FD4</span><span class="sxs-lookup"><span data-stu-id="40fab-198">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="40fab-199">**UD0**</span><span class="sxs-lookup"><span data-stu-id="40fab-199">**UD0**</span></span> |<span data-ttu-id="40fab-200">N1</span><span class="sxs-lookup"><span data-stu-id="40fab-200">N1</span></span> | | | | |
| <span data-ttu-id="40fab-201">**UD1**</span><span class="sxs-lookup"><span data-stu-id="40fab-201">**UD1**</span></span> |<span data-ttu-id="40fab-202">N6</span><span class="sxs-lookup"><span data-stu-id="40fab-202">N6</span></span> |<span data-ttu-id="40fab-203">N2</span><span class="sxs-lookup"><span data-stu-id="40fab-203">N2</span></span> | | | |
| <span data-ttu-id="40fab-204">**UD2**</span><span class="sxs-lookup"><span data-stu-id="40fab-204">**UD2**</span></span> | | |<span data-ttu-id="40fab-205">N3</span><span class="sxs-lookup"><span data-stu-id="40fab-205">N3</span></span> | | |
| <span data-ttu-id="40fab-206">**UD3**</span><span class="sxs-lookup"><span data-stu-id="40fab-206">**UD3**</span></span> | | | |<span data-ttu-id="40fab-207">N4</span><span class="sxs-lookup"><span data-stu-id="40fab-207">N4</span></span> | |
| <span data-ttu-id="40fab-208">**UD4**</span><span class="sxs-lookup"><span data-stu-id="40fab-208">**UD4**</span></span> | | | | |<span data-ttu-id="40fab-209">N5</span><span class="sxs-lookup"><span data-stu-id="40fab-209">N5</span></span> |

<span data-ttu-id="40fab-210">Now let's say that we create a service with a TargetReplicaSetSize of five.</span><span class="sxs-lookup"><span data-stu-id="40fab-210">Now let's say that we create a service with a TargetReplicaSetSize of five.</span></span> <span data-ttu-id="40fab-211">The replicas land on N1-N5.</span><span class="sxs-lookup"><span data-stu-id="40fab-211">The replicas land on N1-N5.</span></span> <span data-ttu-id="40fab-212">In fact, N6 will never be used no matter how many services you create.</span><span class="sxs-lookup"><span data-stu-id="40fab-212">In fact, N6 will never be used no matter how many services you create.</span></span> <span data-ttu-id="40fab-213">But why?</span><span class="sxs-lookup"><span data-stu-id="40fab-213">But why?</span></span> <span data-ttu-id="40fab-214">Let's look at the difference between the current layout and what would happen if N6 is chosen.</span><span class="sxs-lookup"><span data-stu-id="40fab-214">Let's look at the difference between the current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="40fab-215">Here's the layout we got and the total number of replicas per Fault and Upgrade Domain:</span><span class="sxs-lookup"><span data-stu-id="40fab-215">Here's the layout we got and the total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="40fab-216">FD0</span><span class="sxs-lookup"><span data-stu-id="40fab-216">FD0</span></span> | <span data-ttu-id="40fab-217">FD1</span><span class="sxs-lookup"><span data-stu-id="40fab-217">FD1</span></span> | <span data-ttu-id="40fab-218">FD2</span><span class="sxs-lookup"><span data-stu-id="40fab-218">FD2</span></span> | <span data-ttu-id="40fab-219">FD3</span><span class="sxs-lookup"><span data-stu-id="40fab-219">FD3</span></span> | <span data-ttu-id="40fab-220">FD4</span><span class="sxs-lookup"><span data-stu-id="40fab-220">FD4</span></span> | <span data-ttu-id="40fab-221">UDTotal</span><span class="sxs-lookup"><span data-stu-id="40fab-221">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="40fab-222">**UD0**</span><span class="sxs-lookup"><span data-stu-id="40fab-222">**UD0**</span></span> |<span data-ttu-id="40fab-223">R1</span><span class="sxs-lookup"><span data-stu-id="40fab-223">R1</span></span> | | | | |<span data-ttu-id="40fab-224">1</span><span class="sxs-lookup"><span data-stu-id="40fab-224">1</span></span> |
| <span data-ttu-id="40fab-225">**UD1**</span><span class="sxs-lookup"><span data-stu-id="40fab-225">**UD1**</span></span> | |<span data-ttu-id="40fab-226">R2</span><span class="sxs-lookup"><span data-stu-id="40fab-226">R2</span></span> | | | |<span data-ttu-id="40fab-227">1</span><span class="sxs-lookup"><span data-stu-id="40fab-227">1</span></span> |
| <span data-ttu-id="40fab-228">**UD2**</span><span class="sxs-lookup"><span data-stu-id="40fab-228">**UD2**</span></span> | | |<span data-ttu-id="40fab-229">R3</span><span class="sxs-lookup"><span data-stu-id="40fab-229">R3</span></span> | | |<span data-ttu-id="40fab-230">1</span><span class="sxs-lookup"><span data-stu-id="40fab-230">1</span></span> |
| <span data-ttu-id="40fab-231">**UD3**</span><span class="sxs-lookup"><span data-stu-id="40fab-231">**UD3**</span></span> | | | |<span data-ttu-id="40fab-232">R4</span><span class="sxs-lookup"><span data-stu-id="40fab-232">R4</span></span> | |<span data-ttu-id="40fab-233">1</span><span class="sxs-lookup"><span data-stu-id="40fab-233">1</span></span> |
| <span data-ttu-id="40fab-234">**UD4**</span><span class="sxs-lookup"><span data-stu-id="40fab-234">**UD4**</span></span> | | | | |<span data-ttu-id="40fab-235">R5</span><span class="sxs-lookup"><span data-stu-id="40fab-235">R5</span></span> |<span data-ttu-id="40fab-236">1</span><span class="sxs-lookup"><span data-stu-id="40fab-236">1</span></span> |
| <span data-ttu-id="40fab-237">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="40fab-237">**FDTotal**</span></span> |<span data-ttu-id="40fab-238">1</span><span class="sxs-lookup"><span data-stu-id="40fab-238">1</span></span> |<span data-ttu-id="40fab-239">1</span><span class="sxs-lookup"><span data-stu-id="40fab-239">1</span></span> |<span data-ttu-id="40fab-240">1</span><span class="sxs-lookup"><span data-stu-id="40fab-240">1</span></span> |<span data-ttu-id="40fab-241">1</span><span class="sxs-lookup"><span data-stu-id="40fab-241">1</span></span> |<span data-ttu-id="40fab-242">1</span><span class="sxs-lookup"><span data-stu-id="40fab-242">1</span></span> |- |

<span data-ttu-id="40fab-243">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span><span class="sxs-lookup"><span data-stu-id="40fab-243">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="40fab-244">It is also balanced in terms of the number of replicas per Fault and Upgrade Domain.</span><span class="sxs-lookup"><span data-stu-id="40fab-244">It is also balanced in terms of the number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="40fab-245">Each domain has the same number of nodes and the same number of replicas.</span><span class="sxs-lookup"><span data-stu-id="40fab-245">Each domain has the same number of nodes and the same number of replicas.</span></span>

<span data-ttu-id="40fab-246">Now, let's look at what would happen if we'd used N6 instead of N2.</span><span class="sxs-lookup"><span data-stu-id="40fab-246">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="40fab-247">How would the replicas be distributed then?</span><span class="sxs-lookup"><span data-stu-id="40fab-247">How would the replicas be distributed then?</span></span>

|  | <span data-ttu-id="40fab-248">FD0</span><span class="sxs-lookup"><span data-stu-id="40fab-248">FD0</span></span> | <span data-ttu-id="40fab-249">FD1</span><span class="sxs-lookup"><span data-stu-id="40fab-249">FD1</span></span> | <span data-ttu-id="40fab-250">FD2</span><span class="sxs-lookup"><span data-stu-id="40fab-250">FD2</span></span> | <span data-ttu-id="40fab-251">FD3</span><span class="sxs-lookup"><span data-stu-id="40fab-251">FD3</span></span> | <span data-ttu-id="40fab-252">FD4</span><span class="sxs-lookup"><span data-stu-id="40fab-252">FD4</span></span> | <span data-ttu-id="40fab-253">UDTotal</span><span class="sxs-lookup"><span data-stu-id="40fab-253">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="40fab-254">**UD0**</span><span class="sxs-lookup"><span data-stu-id="40fab-254">**UD0**</span></span> |<span data-ttu-id="40fab-255">R1</span><span class="sxs-lookup"><span data-stu-id="40fab-255">R1</span></span> | | | | |<span data-ttu-id="40fab-256">1</span><span class="sxs-lookup"><span data-stu-id="40fab-256">1</span></span> |
| <span data-ttu-id="40fab-257">**UD1**</span><span class="sxs-lookup"><span data-stu-id="40fab-257">**UD1**</span></span> |<span data-ttu-id="40fab-258">R5</span><span class="sxs-lookup"><span data-stu-id="40fab-258">R5</span></span> | | | | |<span data-ttu-id="40fab-259">1</span><span class="sxs-lookup"><span data-stu-id="40fab-259">1</span></span> |
| <span data-ttu-id="40fab-260">**UD2**</span><span class="sxs-lookup"><span data-stu-id="40fab-260">**UD2**</span></span> | | |<span data-ttu-id="40fab-261">R2</span><span class="sxs-lookup"><span data-stu-id="40fab-261">R2</span></span> | | |<span data-ttu-id="40fab-262">1</span><span class="sxs-lookup"><span data-stu-id="40fab-262">1</span></span> |
| <span data-ttu-id="40fab-263">**UD3**</span><span class="sxs-lookup"><span data-stu-id="40fab-263">**UD3**</span></span> | | | |<span data-ttu-id="40fab-264">R3</span><span class="sxs-lookup"><span data-stu-id="40fab-264">R3</span></span> | |<span data-ttu-id="40fab-265">1</span><span class="sxs-lookup"><span data-stu-id="40fab-265">1</span></span> |
| <span data-ttu-id="40fab-266">**UD4**</span><span class="sxs-lookup"><span data-stu-id="40fab-266">**UD4**</span></span> | | | | |<span data-ttu-id="40fab-267">R4</span><span class="sxs-lookup"><span data-stu-id="40fab-267">R4</span></span> |<span data-ttu-id="40fab-268">1</span><span class="sxs-lookup"><span data-stu-id="40fab-268">1</span></span> |
| <span data-ttu-id="40fab-269">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="40fab-269">**FDTotal**</span></span> |<span data-ttu-id="40fab-270">2</span><span class="sxs-lookup"><span data-stu-id="40fab-270">2</span></span> |<span data-ttu-id="40fab-271">0</span><span class="sxs-lookup"><span data-stu-id="40fab-271">0</span></span> |<span data-ttu-id="40fab-272">1</span><span class="sxs-lookup"><span data-stu-id="40fab-272">1</span></span> |<span data-ttu-id="40fab-273">1</span><span class="sxs-lookup"><span data-stu-id="40fab-273">1</span></span> |<span data-ttu-id="40fab-274">1</span><span class="sxs-lookup"><span data-stu-id="40fab-274">1</span></span> |- |

<span data-ttu-id="40fab-275">Notice anything?</span><span class="sxs-lookup"><span data-stu-id="40fab-275">Notice anything?</span></span> <span data-ttu-id="40fab-276">This layout violates our definition for the Fault Domain constraint.</span><span class="sxs-lookup"><span data-stu-id="40fab-276">This layout violates our definition for the Fault Domain constraint.</span></span> <span data-ttu-id="40fab-277">FD0 has two replicas, while FD1 has zero, making the difference between FD0 and FD1 a total of two.</span><span class="sxs-lookup"><span data-stu-id="40fab-277">FD0 has two replicas, while FD1 has zero, making the difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="40fab-278">The Cluster Resource Manager does not allow this arrangement.</span><span class="sxs-lookup"><span data-stu-id="40fab-278">The Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="40fab-279">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span><span class="sxs-lookup"><span data-stu-id="40fab-279">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="40fab-280">FD0</span><span class="sxs-lookup"><span data-stu-id="40fab-280">FD0</span></span> | <span data-ttu-id="40fab-281">FD1</span><span class="sxs-lookup"><span data-stu-id="40fab-281">FD1</span></span> | <span data-ttu-id="40fab-282">FD2</span><span class="sxs-lookup"><span data-stu-id="40fab-282">FD2</span></span> | <span data-ttu-id="40fab-283">FD3</span><span class="sxs-lookup"><span data-stu-id="40fab-283">FD3</span></span> | <span data-ttu-id="40fab-284">FD4</span><span class="sxs-lookup"><span data-stu-id="40fab-284">FD4</span></span> | <span data-ttu-id="40fab-285">UDTotal</span><span class="sxs-lookup"><span data-stu-id="40fab-285">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="40fab-286">**UD0**</span><span class="sxs-lookup"><span data-stu-id="40fab-286">**UD0**</span></span> | | | | | |<span data-ttu-id="40fab-287">0</span><span class="sxs-lookup"><span data-stu-id="40fab-287">0</span></span> |
| <span data-ttu-id="40fab-288">**UD1**</span><span class="sxs-lookup"><span data-stu-id="40fab-288">**UD1**</span></span> |<span data-ttu-id="40fab-289">R5</span><span class="sxs-lookup"><span data-stu-id="40fab-289">R5</span></span> |<span data-ttu-id="40fab-290">R1</span><span class="sxs-lookup"><span data-stu-id="40fab-290">R1</span></span> | | | |<span data-ttu-id="40fab-291">2</span><span class="sxs-lookup"><span data-stu-id="40fab-291">2</span></span> |
| <span data-ttu-id="40fab-292">**UD2**</span><span class="sxs-lookup"><span data-stu-id="40fab-292">**UD2**</span></span> | | |<span data-ttu-id="40fab-293">R2</span><span class="sxs-lookup"><span data-stu-id="40fab-293">R2</span></span> | | |<span data-ttu-id="40fab-294">1</span><span class="sxs-lookup"><span data-stu-id="40fab-294">1</span></span> |
| <span data-ttu-id="40fab-295">**UD3**</span><span class="sxs-lookup"><span data-stu-id="40fab-295">**UD3**</span></span> | | | |<span data-ttu-id="40fab-296">R3</span><span class="sxs-lookup"><span data-stu-id="40fab-296">R3</span></span> | |<span data-ttu-id="40fab-297">1</span><span class="sxs-lookup"><span data-stu-id="40fab-297">1</span></span> |
| <span data-ttu-id="40fab-298">**UD4**</span><span class="sxs-lookup"><span data-stu-id="40fab-298">**UD4**</span></span> | | | | |<span data-ttu-id="40fab-299">R4</span><span class="sxs-lookup"><span data-stu-id="40fab-299">R4</span></span> |<span data-ttu-id="40fab-300">1</span><span class="sxs-lookup"><span data-stu-id="40fab-300">1</span></span> |
| <span data-ttu-id="40fab-301">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="40fab-301">**FDTotal**</span></span> |<span data-ttu-id="40fab-302">1</span><span class="sxs-lookup"><span data-stu-id="40fab-302">1</span></span> |<span data-ttu-id="40fab-303">1</span><span class="sxs-lookup"><span data-stu-id="40fab-303">1</span></span> |<span data-ttu-id="40fab-304">1</span><span class="sxs-lookup"><span data-stu-id="40fab-304">1</span></span> |<span data-ttu-id="40fab-305">1</span><span class="sxs-lookup"><span data-stu-id="40fab-305">1</span></span> |<span data-ttu-id="40fab-306">1</span><span class="sxs-lookup"><span data-stu-id="40fab-306">1</span></span> |- |

<span data-ttu-id="40fab-307">While this layout is balanced in terms of Fault Domains, it is now violating the Upgrade Domain constraint (since UD0 has zero replicas while UD1 has two).</span><span class="sxs-lookup"><span data-stu-id="40fab-307">While this layout is balanced in terms of Fault Domains, it is now violating the Upgrade Domain constraint (since UD0 has zero replicas while UD1 has two).</span></span> <span data-ttu-id="40fab-308">This layout is also invalid</span><span class="sxs-lookup"><span data-stu-id="40fab-308">This layout is also invalid</span></span>

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="40fab-309">Configuring fault and Upgrade Domains</span><span class="sxs-lookup"><span data-stu-id="40fab-309">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="40fab-310">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span><span class="sxs-lookup"><span data-stu-id="40fab-310">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="40fab-311">Service Fabric picks up and uses the environment information from Azure.</span><span class="sxs-lookup"><span data-stu-id="40fab-311">Service Fabric picks up and uses the environment information from Azure.</span></span>

<span data-ttu-id="40fab-312">If you’re creating your own cluster (or want to run a particular topology in development), you provide the Fault Domain and Upgrade Domain information yourself.</span><span class="sxs-lookup"><span data-stu-id="40fab-312">If you’re creating your own cluster (or want to run a particular topology in development), you provide the Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="40fab-313">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span><span class="sxs-lookup"><span data-stu-id="40fab-313">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="40fab-314">This cluster also has three Upgrade Domains striped across those three datacenters.</span><span class="sxs-lookup"><span data-stu-id="40fab-314">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="40fab-315">In the cluster manifest template, it looks something like this:</span><span class="sxs-lookup"><span data-stu-id="40fab-315">In the cluster manifest template, it looks something like this:</span></span>

<span data-ttu-id="40fab-316">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="40fab-316">ClusterManifest.xml</span></span>

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

<span data-ttu-id="40fab-317">via ClusterConfig.json for Standalone deployments</span><span class="sxs-lookup"><span data-stu-id="40fab-317">via ClusterConfig.json for Standalone deployments</span></span>

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> <span data-ttu-id="40fab-318">In Azure deployments, Fault Domains and Upgrade Domains are assigned by Azure.</span><span class="sxs-lookup"><span data-stu-id="40fab-318">In Azure deployments, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="40fab-319">Therefore, the definition of your nodes and roles within the infrastructure option for Azure does not include Fault Domain or Upgrade Domain information.</span><span class="sxs-lookup"><span data-stu-id="40fab-319">Therefore, the definition of your nodes and roles within the infrastructure option for Azure does not include Fault Domain or Upgrade Domain information.</span></span>
>
>

## <a name="placement-constraints-and-node-properties"></a><span data-ttu-id="40fab-320">Placement constraints and node properties</span><span class="sxs-lookup"><span data-stu-id="40fab-320">Placement constraints and node properties</span></span>
<span data-ttu-id="40fab-321">Sometimes (in fact, most of the time) you’re going to want to ensure that certain workloads run only on certain nodes or certain sets of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-321">Sometimes (in fact, most of the time) you’re going to want to ensure that certain workloads run only on certain nodes or certain sets of nodes in the cluster.</span></span> <span data-ttu-id="40fab-322">For example, some workload may require GPUs or SSDs while others may not.</span><span class="sxs-lookup"><span data-stu-id="40fab-322">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="40fab-323">A great example of targeting hardware to particular workloads is almost every n-tier architecture out there.</span><span class="sxs-lookup"><span data-stu-id="40fab-323">A great example of targeting hardware to particular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="40fab-324">In these architectures certain machines serve as the front end/interface serving side of the application (and hence are probably exposed to the internet).</span><span class="sxs-lookup"><span data-stu-id="40fab-324">In these architectures certain machines serve as the front end/interface serving side of the application (and hence are probably exposed to the internet).</span></span> <span data-ttu-id="40fab-325">Different sets of machines (often with different hardware resources) handle the work of the compute or storage layers (and usually are not exposed to the internet).</span><span class="sxs-lookup"><span data-stu-id="40fab-325">Different sets of machines (often with different hardware resources) handle the work of the compute or storage layers (and usually are not exposed to the internet).</span></span> <span data-ttu-id="40fab-326">Service Fabric expects that even in a microservices world there are cases where particular workloads need to run on particular hardware configurations, for example:</span><span class="sxs-lookup"><span data-stu-id="40fab-326">Service Fabric expects that even in a microservices world there are cases where particular workloads need to run on particular hardware configurations, for example:</span></span>

* <span data-ttu-id="40fab-327">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span><span class="sxs-lookup"><span data-stu-id="40fab-327">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="40fab-328">a workload wants to run on specific hardware for performance, scale, or security isolation reasons</span><span class="sxs-lookup"><span data-stu-id="40fab-328">a workload wants to run on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="40fab-329">A workload should be isolated from other workloads for policy or resource consumption reasons</span><span class="sxs-lookup"><span data-stu-id="40fab-329">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="40fab-330">To support these sorts of configurations, Service Fabric has a first class notion of tags that can be applied to nodes.</span><span class="sxs-lookup"><span data-stu-id="40fab-330">To support these sorts of configurations, Service Fabric has a first class notion of tags that can be applied to nodes.</span></span> <span data-ttu-id="40fab-331">These are called placement constraints.</span><span class="sxs-lookup"><span data-stu-id="40fab-331">These are called placement constraints.</span></span> <span data-ttu-id="40fab-332">Placement constraints can be used to indicate where certain services should run.</span><span class="sxs-lookup"><span data-stu-id="40fab-332">Placement constraints can be used to indicate where certain services should run.</span></span> <span data-ttu-id="40fab-333">The set of constraints is extensible - any key/value pair can work.</span><span class="sxs-lookup"><span data-stu-id="40fab-333">The set of constraints is extensible - any key/value pair can work.</span></span>

<span data-ttu-id="40fab-334"><center>
![Cluster Layout Different Workloads][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-334"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

<span data-ttu-id="40fab-335">The different key/value tags on nodes are known as node placement *properties* (or just node properties).</span><span class="sxs-lookup"><span data-stu-id="40fab-335">The different key/value tags on nodes are known as node placement *properties* (or just node properties).</span></span> <span data-ttu-id="40fab-336">The value specified in the node property can be a string, bool, or signed long.</span><span class="sxs-lookup"><span data-stu-id="40fab-336">The value specified in the node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="40fab-337">The statement at the service is called a placement *constraint* since it constrains where the service can run in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-337">The statement at the service is called a placement *constraint* since it constrains where the service can run in the cluster.</span></span> <span data-ttu-id="40fab-338">The constraint can be any Boolean statement that operates on the different node properties in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-338">The constraint can be any Boolean statement that operates on the different node properties in the cluster.</span></span> <span data-ttu-id="40fab-339">The valid selectors in these boolean statements are:</span><span class="sxs-lookup"><span data-stu-id="40fab-339">The valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="40fab-340">conditional checks for creating particular statements</span><span class="sxs-lookup"><span data-stu-id="40fab-340">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="40fab-341">Statement</span><span class="sxs-lookup"><span data-stu-id="40fab-341">Statement</span></span> | <span data-ttu-id="40fab-342">Syntax</span><span class="sxs-lookup"><span data-stu-id="40fab-342">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="40fab-343">"equal to"</span><span class="sxs-lookup"><span data-stu-id="40fab-343">"equal to"</span></span> | <span data-ttu-id="40fab-344">"=="</span><span class="sxs-lookup"><span data-stu-id="40fab-344">"=="</span></span> |
| <span data-ttu-id="40fab-345">"not equal to"</span><span class="sxs-lookup"><span data-stu-id="40fab-345">"not equal to"</span></span> | <span data-ttu-id="40fab-346">"!="</span><span class="sxs-lookup"><span data-stu-id="40fab-346">"!="</span></span> |
| <span data-ttu-id="40fab-347">"greater than"</span><span class="sxs-lookup"><span data-stu-id="40fab-347">"greater than"</span></span> | <span data-ttu-id="40fab-348">">"</span><span class="sxs-lookup"><span data-stu-id="40fab-348">">"</span></span> |
| <span data-ttu-id="40fab-349">"greater than or equal to"</span><span class="sxs-lookup"><span data-stu-id="40fab-349">"greater than or equal to"</span></span> | <span data-ttu-id="40fab-350">">="</span><span class="sxs-lookup"><span data-stu-id="40fab-350">">="</span></span> |
| <span data-ttu-id="40fab-351">"less than"</span><span class="sxs-lookup"><span data-stu-id="40fab-351">"less than"</span></span> | <span data-ttu-id="40fab-352">"<"</span><span class="sxs-lookup"><span data-stu-id="40fab-352">"<"</span></span> |
| <span data-ttu-id="40fab-353">"less than or equal to"</span><span class="sxs-lookup"><span data-stu-id="40fab-353">"less than or equal to"</span></span> | <span data-ttu-id="40fab-354">"<="</span><span class="sxs-lookup"><span data-stu-id="40fab-354">"<="</span></span> |

2) <span data-ttu-id="40fab-355">boolean statements for grouping and logical operations</span><span class="sxs-lookup"><span data-stu-id="40fab-355">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="40fab-356">Statement</span><span class="sxs-lookup"><span data-stu-id="40fab-356">Statement</span></span> | <span data-ttu-id="40fab-357">Syntax</span><span class="sxs-lookup"><span data-stu-id="40fab-357">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="40fab-358">"and"</span><span class="sxs-lookup"><span data-stu-id="40fab-358">"and"</span></span> | <span data-ttu-id="40fab-359">"&&"</span><span class="sxs-lookup"><span data-stu-id="40fab-359">"&&"</span></span> |
| <span data-ttu-id="40fab-360">"or"</span><span class="sxs-lookup"><span data-stu-id="40fab-360">"or"</span></span> | <span data-ttu-id="40fab-361">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="40fab-361">"&#124;&#124;"</span></span> |
| <span data-ttu-id="40fab-362">"not"</span><span class="sxs-lookup"><span data-stu-id="40fab-362">"not"</span></span> | <span data-ttu-id="40fab-363">"!"</span><span class="sxs-lookup"><span data-stu-id="40fab-363">"!"</span></span> |
| <span data-ttu-id="40fab-364">"group as single statement"</span><span class="sxs-lookup"><span data-stu-id="40fab-364">"group as single statement"</span></span> | <span data-ttu-id="40fab-365">"()"</span><span class="sxs-lookup"><span data-stu-id="40fab-365">"()"</span></span> |

<span data-ttu-id="40fab-366">Here are some examples of basic constraint statements.</span><span class="sxs-lookup"><span data-stu-id="40fab-366">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="40fab-367">Only nodes where the overall statement evaluates to “True” can have the service placed on it.</span><span class="sxs-lookup"><span data-stu-id="40fab-367">Only nodes where the overall statement evaluates to “True” can have the service placed on it.</span></span> <span data-ttu-id="40fab-368">Nodes that do not have a property defined do not match any placement constraint containing that property.</span><span class="sxs-lookup"><span data-stu-id="40fab-368">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="40fab-369">Service Fabric defines some default node properties that can be used automatically without the user having to define them.</span><span class="sxs-lookup"><span data-stu-id="40fab-369">Service Fabric defines some default node properties that can be used automatically without the user having to define them.</span></span> <span data-ttu-id="40fab-370">As of this writing the default properties defined at each node are the **NodeType** and the **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="40fab-370">As of this writing the default properties defined at each node are the **NodeType** and the **NodeName**.</span></span> <span data-ttu-id="40fab-371">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span><span class="sxs-lookup"><span data-stu-id="40fab-371">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="40fab-372">Generally we have found NodeType to be one of the most commonly used properties.</span><span class="sxs-lookup"><span data-stu-id="40fab-372">Generally we have found NodeType to be one of the most commonly used properties.</span></span> <span data-ttu-id="40fab-373">It is useful since it corresponds 1:1 with a type of a machine, which in turn corresponds to a type of workload in a traditional n-tier application architecture.</span><span class="sxs-lookup"><span data-stu-id="40fab-373">It is useful since it corresponds 1:1 with a type of a machine, which in turn corresponds to a type of workload in a traditional n-tier application architecture.</span></span>

<span data-ttu-id="40fab-374"><center>
![Placement Constraints and Node Properties][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-374"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

<span data-ttu-id="40fab-375">Let’s say that the following node properties were defined for a given node type:</span><span class="sxs-lookup"><span data-stu-id="40fab-375">Let’s say that the following node properties were defined for a given node type:</span></span>

<span data-ttu-id="40fab-376">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="40fab-376">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="40fab-377">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span><span class="sxs-lookup"><span data-stu-id="40fab-377">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> <span data-ttu-id="40fab-378">In your Azure Resource Manager template for a cluster things like the node type name are likely parameterized, and would look something like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span><span class="sxs-lookup"><span data-stu-id="40fab-378">In your Azure Resource Manager template for a cluster things like the node type name are likely parameterized, and would look something like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

<span data-ttu-id="40fab-379">You can create service placement *constraints* for a service like as follows:</span><span class="sxs-lookup"><span data-stu-id="40fab-379">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="40fab-380">C#</span><span class="sxs-lookup"><span data-stu-id="40fab-380">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="40fab-381">Powershell:</span><span class="sxs-lookup"><span data-stu-id="40fab-381">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="40fab-382">If you are sure that all nodes of NodeType01 are valid, you could also select that node type.</span><span class="sxs-lookup"><span data-stu-id="40fab-382">If you are sure that all nodes of NodeType01 are valid, you could also select that node type.</span></span>

<span data-ttu-id="40fab-383">One of the cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span><span class="sxs-lookup"><span data-stu-id="40fab-383">One of the cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="40fab-384">So if you need to, you can move a service around in the cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that the service stays up and available even when these types of changes are ongoing.</span><span class="sxs-lookup"><span data-stu-id="40fab-384">So if you need to, you can move a service around in the cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that the service stays up and available even when these types of changes are ongoing.</span></span>

<span data-ttu-id="40fab-385">C#:</span><span class="sxs-lookup"><span data-stu-id="40fab-385">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="40fab-386">Powershell:</span><span class="sxs-lookup"><span data-stu-id="40fab-386">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="40fab-387">Placement constraints (along with many other orchestrator controls that we’re going to talk about) are specified for every different named service instance.</span><span class="sxs-lookup"><span data-stu-id="40fab-387">Placement constraints (along with many other orchestrator controls that we’re going to talk about) are specified for every different named service instance.</span></span> <span data-ttu-id="40fab-388">Updates always take the place of (overwrite) what was previously specified.</span><span class="sxs-lookup"><span data-stu-id="40fab-388">Updates always take the place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="40fab-389">The properties on a node are defined via the cluster definition and hence cannot be updated without an upgrade to the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-389">The properties on a node are defined via the cluster definition and hence cannot be updated without an upgrade to the cluster.</span></span> <span data-ttu-id="40fab-390">The upgrade of a node's properties and requires each affected node to go down and then come back up.</span><span class="sxs-lookup"><span data-stu-id="40fab-390">The upgrade of a node's properties and requires each affected node to go down and then come back up.</span></span>

## <a name="capacity"></a><span data-ttu-id="40fab-391">Capacity</span><span class="sxs-lookup"><span data-stu-id="40fab-391">Capacity</span></span>
<span data-ttu-id="40fab-392">One of the most important jobs of any orchestrator is to help manage resource consumption in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-392">One of the most important jobs of any orchestrator is to help manage resource consumption in the cluster.</span></span> <span data-ttu-id="40fab-393">The last thing you want if you’re trying to run services efficiently is a bunch of nodes that are hot while others are cold.</span><span class="sxs-lookup"><span data-stu-id="40fab-393">The last thing you want if you’re trying to run services efficiently is a bunch of nodes that are hot while others are cold.</span></span> <span data-ttu-id="40fab-394">Hot nodes lead to resource contention and poor performance, and cold nodes represent wasted resources/increased cost.</span><span class="sxs-lookup"><span data-stu-id="40fab-394">Hot nodes lead to resource contention and poor performance, and cold nodes represent wasted resources/increased cost.</span></span> <span data-ttu-id="40fab-395">Before we talk about balancing, what about just ensuring that nodes don’t run out of resources in the first place?</span><span class="sxs-lookup"><span data-stu-id="40fab-395">Before we talk about balancing, what about just ensuring that nodes don’t run out of resources in the first place?</span></span>

<span data-ttu-id="40fab-396">Service Fabric represents resources as `Metrics`.</span><span class="sxs-lookup"><span data-stu-id="40fab-396">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="40fab-397">Metrics are any logical or physical resource that you want to describe to Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="40fab-397">Metrics are any logical or physical resource that you want to describe to Service Fabric.</span></span> <span data-ttu-id="40fab-398">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span><span class="sxs-lookup"><span data-stu-id="40fab-398">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="40fab-399">For information configuring metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="40fab-399">For information configuring metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="40fab-400">Metrics are different from placements constraints and node properties.</span><span class="sxs-lookup"><span data-stu-id="40fab-400">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="40fab-401">Node properties are static descriptors of the nodes themselves, whereas metrics are about resources that nodes have and that services consume when they are running on a node.</span><span class="sxs-lookup"><span data-stu-id="40fab-401">Node properties are static descriptors of the nodes themselves, whereas metrics are about resources that nodes have and that services consume when they are running on a node.</span></span> <span data-ttu-id="40fab-402">A node property could be "HasSSD" and could be set to true or false.</span><span class="sxs-lookup"><span data-stu-id="40fab-402">A node property could be "HasSSD" and could be set to true or false.</span></span> <span data-ttu-id="40fab-403">The amount of space available on that SSD (and consumed by services) would be a metric like “DriveSpaceInMb”.</span><span class="sxs-lookup"><span data-stu-id="40fab-403">The amount of space available on that SSD (and consumed by services) would be a metric like “DriveSpaceInMb”.</span></span> <span data-ttu-id="40fab-404">The node would have its capacity for “DriveSpaceInMb” to the amount of total non-reserved space on the drive.</span><span class="sxs-lookup"><span data-stu-id="40fab-404">The node would have its capacity for “DriveSpaceInMb” to the amount of total non-reserved space on the drive.</span></span> <span data-ttu-id="40fab-405">Services would report how much of the metric they used during runtime.</span><span class="sxs-lookup"><span data-stu-id="40fab-405">Services would report how much of the metric they used during runtime.</span></span>

<span data-ttu-id="40fab-406">It is important to note that just like for placement constraints and node properties, the Service Fabric Cluster Resource Manager doesn't understand what the names of the metrics mean.</span><span class="sxs-lookup"><span data-stu-id="40fab-406">It is important to note that just like for placement constraints and node properties, the Service Fabric Cluster Resource Manager doesn't understand what the names of the metrics mean.</span></span> <span data-ttu-id="40fab-407">Metric names are just strings.</span><span class="sxs-lookup"><span data-stu-id="40fab-407">Metric names are just strings.</span></span> <span data-ttu-id="40fab-408">It is a good practice to declare units as a part of the metric names that you create when it could be ambiguous.</span><span class="sxs-lookup"><span data-stu-id="40fab-408">It is a good practice to declare units as a part of the metric names that you create when it could be ambiguous.</span></span>

<span data-ttu-id="40fab-409">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still try to ensure that no node ended up over its capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-409">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still try to ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="40fab-410">Generally this is possible unless the cluster as a whole is too full.</span><span class="sxs-lookup"><span data-stu-id="40fab-410">Generally this is possible unless the cluster as a whole is too full.</span></span> <span data-ttu-id="40fab-411">Capacity is another *constraint* that the Cluster Resource Manager uses to understand how much of a resource a node has.</span><span class="sxs-lookup"><span data-stu-id="40fab-411">Capacity is another *constraint* that the Cluster Resource Manager uses to understand how much of a resource a node has.</span></span> <span data-ttu-id="40fab-412">Remaining capacity is also tracked for the cluster as a whole.</span><span class="sxs-lookup"><span data-stu-id="40fab-412">Remaining capacity is also tracked for the cluster as a whole.</span></span> <span data-ttu-id="40fab-413">Both the capacity and the consumption at the service level are expressed in terms of metrics.</span><span class="sxs-lookup"><span data-stu-id="40fab-413">Both the capacity and the consumption at the service level are expressed in terms of metrics.</span></span> <span data-ttu-id="40fab-414">So for example, the metric might be "MemoryInMb" and a given Node may have a capacity for "MemoryInMb" of 2048.</span><span class="sxs-lookup"><span data-stu-id="40fab-414">So for example, the metric might be "MemoryInMb" and a given Node may have a capacity for "MemoryInMb" of 2048.</span></span> <span data-ttu-id="40fab-415">Some service running on that node can say it is currently consuming 64 of "MemoryInMb".</span><span class="sxs-lookup"><span data-stu-id="40fab-415">Some service running on that node can say it is currently consuming 64 of "MemoryInMb".</span></span>

<span data-ttu-id="40fab-416">During runtime, the Cluster Resource Manager tracks how much of each resource is present on each node and how much is remaining.</span><span class="sxs-lookup"><span data-stu-id="40fab-416">During runtime, the Cluster Resource Manager tracks how much of each resource is present on each node and how much is remaining.</span></span> <span data-ttu-id="40fab-417">It does this by subtracting any declared usage of each service running on that node from the node's capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-417">It does this by subtracting any declared usage of each service running on that node from the node's capacity.</span></span> <span data-ttu-id="40fab-418">With this information, the Service Fabric Cluster Resource Manager can figure out where to place or move replicas so that nodes don’t go over capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-418">With this information, the Service Fabric Cluster Resource Manager can figure out where to place or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="40fab-419">C#:</span><span class="sxs-lookup"><span data-stu-id="40fab-419">C#:</span></span>

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "MemoryInMb";
metric.PrimaryDefaultLoad = 64;
metric.SecondaryDefaultLoad = 64;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="40fab-420">Powershell:</span><span class="sxs-lookup"><span data-stu-id="40fab-420">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("Memory,High,64,64)
```
<span data-ttu-id="40fab-421"><center>
![Cluster nodes and capacity][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="40fab-421"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="40fab-422">You can see capacities defined in the cluster manifest:</span><span class="sxs-lookup"><span data-stu-id="40fab-422">You can see capacities defined in the cluster manifest:</span></span>

<span data-ttu-id="40fab-423">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="40fab-423">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType02">
      <Capacities>
        <Capacity Name="MemoryInMb" Value="2048"/>
        <Capacity Name="DiskInMb" Value="512000"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="40fab-424">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span><span class="sxs-lookup"><span data-stu-id="40fab-424">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> <span data-ttu-id="40fab-425">In your Azure Resource Manager template for a cluster things like the node type name are likely parameterized, and would look something like "[parameters('vmNodeType2Name')]" rather than "NodeType02".</span><span class="sxs-lookup"><span data-stu-id="40fab-425">In your Azure Resource Manager template for a cluster things like the node type name are likely parameterized, and would look something like "[parameters('vmNodeType2Name')]" rather than "NodeType02".</span></span>

```json
"nodeTypes": [
    {
        "name": "NodeType02",
        "capacities": {
            "MemoryInMb": "2048",
            "DiskInMb": "512000"
        }
    }
],
```

<span data-ttu-id="40fab-426">It is also possible (and in fact common) that a service’s load changes dynamically.</span><span class="sxs-lookup"><span data-stu-id="40fab-426">It is also possible (and in fact common) that a service’s load changes dynamically.</span></span> <span data-ttu-id="40fab-427">Say that a replica's load changed from 64 to 1024, but the node it was running on then only had 512 (of the "MemoryInMb" metric) remaining.</span><span class="sxs-lookup"><span data-stu-id="40fab-427">Say that a replica's load changed from 64 to 1024, but the node it was running on then only had 512 (of the "MemoryInMb" metric) remaining.</span></span> <span data-ttu-id="40fab-428">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span><span class="sxs-lookup"><span data-stu-id="40fab-428">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="40fab-429">This can also happen if the combined usage of the replicas and instances on that node exceeds that node’s capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-429">This can also happen if the combined usage of the replicas and instances on that node exceeds that node’s capacity.</span></span> <span data-ttu-id="40fab-430">In either case the Cluster Resource Manager has to kick in and get the node back below capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-430">In either case the Cluster Resource Manager has to kick in and get the node back below capacity.</span></span> <span data-ttu-id="40fab-431">It does this by moving one or more of the replicas or instances on that node to different nodes.</span><span class="sxs-lookup"><span data-stu-id="40fab-431">It does this by moving one or more of the replicas or instances on that node to different nodes.</span></span> <span data-ttu-id="40fab-432">When moving replicas, the Cluster Resource Manager tries to minimize the cost of those movements.</span><span class="sxs-lookup"><span data-stu-id="40fab-432">When moving replicas, the Cluster Resource Manager tries to minimize the cost of those movements.</span></span> <span data-ttu-id="40fab-433">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="40fab-433">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="40fab-434">Cluster capacity</span><span class="sxs-lookup"><span data-stu-id="40fab-434">Cluster capacity</span></span>
<span data-ttu-id="40fab-435">So how do we keep the overall cluster from being too full?</span><span class="sxs-lookup"><span data-stu-id="40fab-435">So how do we keep the overall cluster from being too full?</span></span> <span data-ttu-id="40fab-436">Well, with dynamic load there’s not a lot the Cluster Resource Manager can do.</span><span class="sxs-lookup"><span data-stu-id="40fab-436">Well, with dynamic load there’s not a lot the Cluster Resource Manager can do.</span></span> <span data-ttu-id="40fab-437">Services can have their load spike independently of actions taken by the Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40fab-437">Services can have their load spike independently of actions taken by the Cluster Resource Manager.</span></span> <span data-ttu-id="40fab-438">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span><span class="sxs-lookup"><span data-stu-id="40fab-438">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="40fab-439">That said, there are some controls that are baked in to prevent basic problems.</span><span class="sxs-lookup"><span data-stu-id="40fab-439">That said, there are some controls that are baked in to prevent basic problems.</span></span> <span data-ttu-id="40fab-440">The first thing we can do is prevent the creation of new workloads that would cause the cluster to become full.</span><span class="sxs-lookup"><span data-stu-id="40fab-440">The first thing we can do is prevent the creation of new workloads that would cause the cluster to become full.</span></span>

<span data-ttu-id="40fab-441">Say that you go to create a stateless service and it has some load associated with it (more on default and dynamic load reporting later).</span><span class="sxs-lookup"><span data-stu-id="40fab-441">Say that you go to create a stateless service and it has some load associated with it (more on default and dynamic load reporting later).</span></span> <span data-ttu-id="40fab-442">Let’s say that the service cares about the "DiskSpaceInMb" metric.</span><span class="sxs-lookup"><span data-stu-id="40fab-442">Let’s say that the service cares about the "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="40fab-443">Let's also say that it is going to consume five units of "DiskSpaceInMb" for every instance of the service.</span><span class="sxs-lookup"><span data-stu-id="40fab-443">Let's also say that it is going to consume five units of "DiskSpaceInMb" for every instance of the service.</span></span> <span data-ttu-id="40fab-444">You want to create three instances of the service.</span><span class="sxs-lookup"><span data-stu-id="40fab-444">You want to create three instances of the service.</span></span> <span data-ttu-id="40fab-445">Great!</span><span class="sxs-lookup"><span data-stu-id="40fab-445">Great!</span></span> <span data-ttu-id="40fab-446">So that means that we need 15 units of "DiskSpaceInMb" to be present in the cluster in order for us to even be able to create these service instances.</span><span class="sxs-lookup"><span data-stu-id="40fab-446">So that means that we need 15 units of "DiskSpaceInMb" to be present in the cluster in order for us to even be able to create these service instances.</span></span> <span data-ttu-id="40fab-447">The Cluster Resource Manager is continually calculating the overall capacity and consumption of each metric, so it can easily determine if there's sufficient space in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-447">The Cluster Resource Manager is continually calculating the overall capacity and consumption of each metric, so it can easily determine if there's sufficient space in the cluster.</span></span> <span data-ttu-id="40fab-448">If there isn't sufficient space, the Cluster Resource Manager rejects the create service call.</span><span class="sxs-lookup"><span data-stu-id="40fab-448">If there isn't sufficient space, the Cluster Resource Manager rejects the create service call.</span></span>

<span data-ttu-id="40fab-449">Since the requirement is only that there be 15 units available, this space could be allocated many different ways.</span><span class="sxs-lookup"><span data-stu-id="40fab-449">Since the requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="40fab-450">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span><span class="sxs-lookup"><span data-stu-id="40fab-450">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="40fab-451">As long as the Cluster Resource Manager can rearrange things so there's five units available on three nodes, it will eventually place the service.</span><span class="sxs-lookup"><span data-stu-id="40fab-451">As long as the Cluster Resource Manager can rearrange things so there's five units available on three nodes, it will eventually place the service.</span></span> <span data-ttu-id="40fab-452">Such rearrangement is almost always possible unless the cluster as a whole is almost entirely full, the services are all very "bulky", or both.</span><span class="sxs-lookup"><span data-stu-id="40fab-452">Such rearrangement is almost always possible unless the cluster as a whole is almost entirely full, the services are all very "bulky", or both.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="40fab-453">Buffered Capacity</span><span class="sxs-lookup"><span data-stu-id="40fab-453">Buffered Capacity</span></span>
<span data-ttu-id="40fab-454">Another feature the Cluster Resource Manager has that helps manage overall cluster capacity is the notion of some reserved buffer to the capacity specified at each node.</span><span class="sxs-lookup"><span data-stu-id="40fab-454">Another feature the Cluster Resource Manager has that helps manage overall cluster capacity is the notion of some reserved buffer to the capacity specified at each node.</span></span> <span data-ttu-id="40fab-455">Buffered Capacity allows reservation of some portion of the overall node capacity so that it is only used to place services during upgrades and node failures.</span><span class="sxs-lookup"><span data-stu-id="40fab-455">Buffered Capacity allows reservation of some portion of the overall node capacity so that it is only used to place services during upgrades and node failures.</span></span> <span data-ttu-id="40fab-456">Today buffer is specified globally per metric for all nodes via the cluster definition.</span><span class="sxs-lookup"><span data-stu-id="40fab-456">Today buffer is specified globally per metric for all nodes via the cluster definition.</span></span> <span data-ttu-id="40fab-457">The value you pick for the reserved capacity is a function of the number of Fault and Upgrade Domains you have in the cluster and how much overhead you want.</span><span class="sxs-lookup"><span data-stu-id="40fab-457">The value you pick for the reserved capacity is a function of the number of Fault and Upgrade Domains you have in the cluster and how much overhead you want.</span></span> <span data-ttu-id="40fab-458">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-458">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="40fab-459">If you have more domains, you can expect smaller amounts of your cluster to be unavailable during upgrades and failures.</span><span class="sxs-lookup"><span data-stu-id="40fab-459">If you have more domains, you can expect smaller amounts of your cluster to be unavailable during upgrades and failures.</span></span> <span data-ttu-id="40fab-460">Specifying the buffer percentage only makes sense if you have also specified the node capacity for a metric.</span><span class="sxs-lookup"><span data-stu-id="40fab-460">Specifying the buffer percentage only makes sense if you have also specified the node capacity for a metric.</span></span>

<span data-ttu-id="40fab-461">Here's an example of how to specify buffered capacity:</span><span class="sxs-lookup"><span data-stu-id="40fab-461">Here's an example of how to specify buffered capacity:</span></span>

<span data-ttu-id="40fab-462">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="40fab-462">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="DiskSpace" Value="0.10" />
            <Parameter Name="Memory" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="40fab-463">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span><span class="sxs-lookup"><span data-stu-id="40fab-463">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "DiskSpace",
          "value": "0.10"
      },
      {
          "name": "Memory",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

<span data-ttu-id="40fab-464">The creation of new services fails when the cluster is out of buffered capacity for a metric.</span><span class="sxs-lookup"><span data-stu-id="40fab-464">The creation of new services fails when the cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="40fab-465">This ensures that the cluster retains enough spare overhead so that upgrades and failures don’t cause nodes to go over capacity.</span><span class="sxs-lookup"><span data-stu-id="40fab-465">This ensures that the cluster retains enough spare overhead so that upgrades and failures don’t cause nodes to go over capacity.</span></span> <span data-ttu-id="40fab-466">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span><span class="sxs-lookup"><span data-stu-id="40fab-466">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="40fab-467">The Cluster Resource Manager exposes this information via PowerShell and the Query APIs.</span><span class="sxs-lookup"><span data-stu-id="40fab-467">The Cluster Resource Manager exposes this information via PowerShell and the Query APIs.</span></span> <span data-ttu-id="40fab-468">This lets you see the buffered capacity settings, the total capacity, and the current consumption for every metric in use in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40fab-468">This lets you see the buffered capacity settings, the total capacity, and the current consumption for every metric in use in the cluster.</span></span> <span data-ttu-id="40fab-469">Here we see an example of that output:</span><span class="sxs-lookup"><span data-stu-id="40fab-469">Here we see an example of that output:</span></span>

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a><span data-ttu-id="40fab-470">Next steps</span><span class="sxs-lookup"><span data-stu-id="40fab-470">Next steps</span></span>
* <span data-ttu-id="40fab-471">For information on the architecture and information flow within the Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="40fab-471">For information on the architecture and information flow within the Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="40fab-472">Defining Defragmentation Metrics is one way to consolidate load on nodes instead of spreading it out. To learn how to configure defragmentation, refer to [this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="40fab-472">Defining Defragmentation Metrics is one way to consolidate load on nodes instead of spreading it out. To learn how to configure defragmentation, refer to [this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="40fab-473">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="40fab-473">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="40fab-474">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="40fab-474">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png







