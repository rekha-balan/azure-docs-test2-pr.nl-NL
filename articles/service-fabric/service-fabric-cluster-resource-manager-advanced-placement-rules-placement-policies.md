---
title: Service Fabric Cluster Resource Manager - Placement Policies | Microsoft Docs
description: Overview of additional placement policies and rules for Service Fabric Services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: 3e4530ca23f2e1be8520c220172811b7cda18ba1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669783"
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="c8b5b-103">Placement policies for service fabric services</span><span class="sxs-lookup"><span data-stu-id="c8b5b-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="c8b5b-104">There are many different additional rules that you may need to configure in some rare scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-104">There are many different additional rules that you may need to configure in some rare scenarios.</span></span> <span data-ttu-id="c8b5b-105">Some examples of those scenarios are:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-105">Some examples of those scenarios are:</span></span>
* <span data-ttu-id="c8b5b-106">If your Service Fabric cluster is spanned across a geographic distance, such as multiple on-premises datacenters or across Azure regions</span><span class="sxs-lookup"><span data-stu-id="c8b5b-106">If your Service Fabric cluster is spanned across a geographic distance, such as multiple on-premises datacenters or across Azure regions</span></span>
* <span data-ttu-id="c8b5b-107">If your environment spans multiple areas of geopolitical control (or some other case where you have legal or policy boundaries you care about</span><span class="sxs-lookup"><span data-stu-id="c8b5b-107">If your environment spans multiple areas of geopolitical control (or some other case where you have legal or policy boundaries you care about</span></span>
* <span data-ttu-id="c8b5b-108">There are actual performance/latency considerations due to communication in the cluster traveling large distances or transiting certain slower or less reliable networks.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-108">There are actual performance/latency considerations due to communication in the cluster traveling large distances or transiting certain slower or less reliable networks.</span></span>

<span data-ttu-id="c8b5b-109">In these types of situations, it may be important for a given service to always run or never run in certain regions.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-109">In these types of situations, it may be important for a given service to always run or never run in certain regions.</span></span> <span data-ttu-id="c8b5b-110">Similarly it may be important to try to place the Primary in a certain region to minimize end-user latency.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-110">Similarly it may be important to try to place the Primary in a certain region to minimize end-user latency.</span></span>

<span data-ttu-id="c8b5b-111">The advanced placement policies are:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-111">The advanced placement policies are:</span></span>

1. <span data-ttu-id="c8b5b-112">Invalid domains</span><span class="sxs-lookup"><span data-stu-id="c8b5b-112">Invalid domains</span></span>
2. <span data-ttu-id="c8b5b-113">Required domains</span><span class="sxs-lookup"><span data-stu-id="c8b5b-113">Required domains</span></span>
3. <span data-ttu-id="c8b5b-114">Preferred domains</span><span class="sxs-lookup"><span data-stu-id="c8b5b-114">Preferred domains</span></span>
4. <span data-ttu-id="c8b5b-115">Disallowing replica packing</span><span class="sxs-lookup"><span data-stu-id="c8b5b-115">Disallowing replica packing</span></span>

<span data-ttu-id="c8b5b-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="c8b5b-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="c8b5b-118">Like with other placement constraints, placement policies can be configured on a per-named service instance basis and updated dynamically.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-118">Like with other placement constraints, placement policies can be configured on a per-named service instance basis and updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="c8b5b-119">Specifying invalid domains</span><span class="sxs-lookup"><span data-stu-id="c8b5b-119">Specifying invalid domains</span></span>
<span data-ttu-id="c8b5b-120">The InvalidDomain placement policy allows you to specify that a particular Fault Domain is invalid for this workload.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-120">The InvalidDomain placement policy allows you to specify that a particular Fault Domain is invalid for this workload.</span></span> <span data-ttu-id="c8b5b-121">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-121">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="c8b5b-122">Multiple invalid domains may be specified via separate policies.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-122">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="c8b5b-123"><center>
![Invalid Domain Example][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="c8b5b-123"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="c8b5b-124">Code:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-124">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="c8b5b-125">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-125">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="c8b5b-126">Specifying required domains</span><span class="sxs-lookup"><span data-stu-id="c8b5b-126">Specifying required domains</span></span>
<span data-ttu-id="c8b5b-127">The required domain placement policy requires that all the stateful replicas or stateless service instances for the service be present in the specified domain.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-127">The required domain placement policy requires that all the stateful replicas or stateless service instances for the service be present in the specified domain.</span></span> <span data-ttu-id="c8b5b-128">Multiple required domains can be specified via separate policies.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-128">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="c8b5b-129"><center>
![Required Domain Example][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="c8b5b-129"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="c8b5b-130">Code:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-130">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="c8b5b-131">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-131">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-the-primary-replicas"></a><span data-ttu-id="c8b5b-132">Specifying a preferred domain for the primary replicas</span><span class="sxs-lookup"><span data-stu-id="c8b5b-132">Specifying a preferred domain for the primary replicas</span></span>
<span data-ttu-id="c8b5b-133">The Preferred Primary Domain is an interesting control, since it allows selection of the fault domain in which the Primary should be placed if it is possible to do so.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-133">The Preferred Primary Domain is an interesting control, since it allows selection of the fault domain in which the Primary should be placed if it is possible to do so.</span></span> <span data-ttu-id="c8b5b-134">The Primary ends up in this domain when everything is healthy.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-134">The Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="c8b5b-135">If the domain or the Primary replica fails or is shut down for some reason, the Primary is migrated to some other location.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-135">If the domain or the Primary replica fails or is shut down for some reason, the Primary is migrated to some other location.</span></span> <span data-ttu-id="c8b5b-136">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-136">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span></span> <span data-ttu-id="c8b5b-137">Naturally this setting only makes sense for stateful services.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-137">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="c8b5b-138">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but would prefer that the Primary replicas be placed in a certain location.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-138">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but would prefer that the Primary replicas be placed in a certain location.</span></span> <span data-ttu-id="c8b5b-139">Keeping Primaries close to their users helps provide lower latency, especially for reads.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-139">Keeping Primaries close to their users helps provide lower latency, especially for reads.</span></span>

<span data-ttu-id="c8b5b-140"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="c8b5b-140"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="c8b5b-141">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-141">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replicas-to-be-distributed-among-all-domains-and-disallowing-packing"></a><span data-ttu-id="c8b5b-142">Requiring replicas to be distributed among all domains and disallowing packing</span><span class="sxs-lookup"><span data-stu-id="c8b5b-142">Requiring replicas to be distributed among all domains and disallowing packing</span></span>
<span data-ttu-id="c8b5b-143">Replicas are _normally_ distributed across the domains the cluster is healthy, but there are cases where replicas for a given partition may end up temporarily packed into a single domain.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-143">Replicas are _normally_ distributed across the domains the cluster is healthy, but there are cases where replicas for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="c8b5b-144">For example, let's say that the cluster has nine nodes in three fault domains (fd:/0, fd:/1, and fd:/2), and your service has three replicas.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-144">For example, let's say that the cluster has nine nodes in three fault domains (fd:/0, fd:/1, and fd:/2), and your service has three replicas.</span></span> <span data-ttu-id="c8b5b-145">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-145">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="c8b5b-146">Now, normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-146">Now, normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="c8b5b-147">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-147">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span></span> <span data-ttu-id="c8b5b-148">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-148">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span></span> <span data-ttu-id="c8b5b-149">However, doing _that_ creates a situation where the Fault Domain constraint is being violated.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-149">However, doing _that_ creates a situation where the Fault Domain constraint is being violated.</span></span> <span data-ttu-id="c8b5b-150">It also increases the chance that the whole replica set could go down or be lost (if FD 0 were to be permanently lost).</span><span class="sxs-lookup"><span data-stu-id="c8b5b-150">It also increases the chance that the whole replica set could go down or be lost (if FD 0 were to be permanently lost).</span></span> <span data-ttu-id="c8b5b-151">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="c8b5b-151">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>

<span data-ttu-id="c8b5b-152">If you've ever seen a health warning like `The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain` you've hit this condition or something like it.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-152">If you've ever seen a health warning like `The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain` you've hit this condition or something like it.</span></span> <span data-ttu-id="c8b5b-153">This is rare, but it can happen, and usually these situations are transient since the nodes come back.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-153">This is rare, but it can happen, and usually these situations are transient since the nodes come back.</span></span> <span data-ttu-id="c8b5b-154">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-154">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span></span>

<span data-ttu-id="c8b5b-155">Some workloads would rather always have the target number of replicas, even if they are packed into fewer domains.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-155">Some workloads would rather always have the target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="c8b5b-156">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-156">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="c8b5b-157">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-157">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="c8b5b-158">Since most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain, the default is to not require domain distribution.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-158">Since most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain, the default is to not require domain distribution.</span></span> <span data-ttu-id="c8b5b-159">This lets normal balancing and failover handle these cases, even if that means that temporarily a domain may have multiple replicas packed into it.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-159">This lets normal balancing and failover handle these cases, even if that means that temporarily a domain may have multiple replicas packed into it.</span></span>

<span data-ttu-id="c8b5b-160">If you want to disable such packing for a given workload, you can specify the "RequireDomainDistribution" policy on the service.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-160">If you want to disable such packing for a given workload, you can specify the "RequireDomainDistribution" policy on the service.</span></span> <span data-ttu-id="c8b5b-161">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition are ever allowed in the same fault or upgrade domain.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-161">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition are ever allowed in the same fault or upgrade domain.</span></span>

<span data-ttu-id="c8b5b-162">Code:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-162">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="c8b5b-163">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c8b5b-163">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 2 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="c8b5b-164">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span><span class="sxs-lookup"><span data-stu-id="c8b5b-164">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="c8b5b-165">Sure you could!</span><span class="sxs-lookup"><span data-stu-id="c8b5b-165">Sure you could!</span></span> <span data-ttu-id="c8b5b-166">But there’s not a great reason too.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-166">But there’s not a great reason too.</span></span> <span data-ttu-id="c8b5b-167">The required, invalid, and preferred domain configurations should be avoided unless you’re actually running a cluster that spans geographic distances.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-167">The required, invalid, and preferred domain configurations should be avoided unless you’re actually running a cluster that spans geographic distances.</span></span> <span data-ttu-id="c8b5b-168">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-168">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span></span> <span data-ttu-id="c8b5b-169">Different hardware configurations should be spread across domains and those handled via normal placement constraints and node properties.</span><span class="sxs-lookup"><span data-stu-id="c8b5b-169">Different hardware configurations should be spread across domains and those handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8b5b-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8b5b-170">Next steps</span></span>
* <span data-ttu-id="c8b5b-171">For more information about the other options available for configuring services, go [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="c8b5b-171">For more information about the other options available for configuring services, go [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png



