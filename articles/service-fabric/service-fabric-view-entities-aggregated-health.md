---
title: How to view Azure Service Fabric entities' aggregated health | Microsoft Docs
description: Describes how to query, view, and evaluate Azure Service Fabric entities' aggregated health, through health queries and general queries.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: ''
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 2/28/2018
ms.author: oanapl
ms.openlocfilehash: 393e072fd50aacbab578a7a7244b4ce6b8ab7949
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781253"
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="2fd45-103">View Service Fabric health reports</span><span class="sxs-lookup"><span data-stu-id="2fd45-103">View Service Fabric health reports</span></span>
<span data-ttu-id="2fd45-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span><span class="sxs-lookup"><span data-stu-id="2fd45-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="2fd45-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="2fd45-106">The cluster is automatically populated with health reports sent by the system components.</span><span class="sxs-lookup"><span data-stu-id="2fd45-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="2fd45-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="2fd45-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="2fd45-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span><span class="sxs-lookup"><span data-stu-id="2fd45-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="2fd45-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span><span class="sxs-lookup"><span data-stu-id="2fd45-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="2fd45-110">Health queries (through PowerShell, API, or REST)</span><span class="sxs-lookup"><span data-stu-id="2fd45-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="2fd45-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span><span class="sxs-lookup"><span data-stu-id="2fd45-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="2fd45-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="2fd45-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="2fd45-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="2fd45-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="2fd45-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span><span class="sxs-lookup"><span data-stu-id="2fd45-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="2fd45-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span><span class="sxs-lookup"><span data-stu-id="2fd45-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="2fd45-116">Health in Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="2fd45-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="2fd45-117">Service Fabric Explorer provides a visual view of the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd45-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="2fd45-118">In the image below, you can see that:</span><span class="sxs-lookup"><span data-stu-id="2fd45-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="2fd45-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span><span class="sxs-lookup"><span data-stu-id="2fd45-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="2fd45-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span><span class="sxs-lookup"><span data-stu-id="2fd45-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="2fd45-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span><span class="sxs-lookup"><span data-stu-id="2fd45-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="2fd45-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="2fd45-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="2fd45-123">The yellow partition triggers the yellow service.</span><span class="sxs-lookup"><span data-stu-id="2fd45-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="2fd45-124">The cluster is red because of the red application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="2fd45-125">The evaluation uses default policies from the cluster manifest and application manifest.</span><span class="sxs-lookup"><span data-stu-id="2fd45-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="2fd45-126">They are strict policies and do not tolerate any failure.</span><span class="sxs-lookup"><span data-stu-id="2fd45-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="2fd45-127">View of the cluster with Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="2fd45-127">View of the cluster with Service Fabric Explorer:</span></span>

![View of the cluster with Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="2fd45-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2fd45-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="2fd45-130">Health queries</span><span class="sxs-lookup"><span data-stu-id="2fd45-130">Health queries</span></span>
<span data-ttu-id="2fd45-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="2fd45-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="2fd45-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span><span class="sxs-lookup"><span data-stu-id="2fd45-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="2fd45-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span><span class="sxs-lookup"><span data-stu-id="2fd45-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="2fd45-134">A health entity is returned when it is fully populated in the health store.</span><span class="sxs-lookup"><span data-stu-id="2fd45-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="2fd45-135">The entity must be active (not deleted) and have a system report.</span><span class="sxs-lookup"><span data-stu-id="2fd45-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="2fd45-136">Its parent entities on the hierarchy chain must also have system reports.</span><span class="sxs-lookup"><span data-stu-id="2fd45-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="2fd45-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span><span class="sxs-lookup"><span data-stu-id="2fd45-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="2fd45-138">The health queries must pass in the entity identifier, which depends on the entity type.</span><span class="sxs-lookup"><span data-stu-id="2fd45-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="2fd45-139">The queries accept optional health policy parameters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="2fd45-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span><span class="sxs-lookup"><span data-stu-id="2fd45-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="2fd45-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span><span class="sxs-lookup"><span data-stu-id="2fd45-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="2fd45-142">The default health policies do not tolerate any failures.</span><span class="sxs-lookup"><span data-stu-id="2fd45-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="2fd45-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="2fd45-144">Another filter allows excluding the children statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd45-145">The output filters are applied on the server side, so the message reply size is reduced.</span><span class="sxs-lookup"><span data-stu-id="2fd45-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="2fd45-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span><span class="sxs-lookup"><span data-stu-id="2fd45-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="2fd45-147">An entity's health contains:</span><span class="sxs-lookup"><span data-stu-id="2fd45-147">An entity's health contains:</span></span>

* <span data-ttu-id="2fd45-148">The aggregated health state of the entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="2fd45-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="2fd45-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="2fd45-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="2fd45-151">The health events on the entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-151">The health events on the entity.</span></span>
* <span data-ttu-id="2fd45-152">The collection of health states of all children for the entities that can have children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="2fd45-153">The health states contain entity identifiers and the aggregated health state.</span><span class="sxs-lookup"><span data-stu-id="2fd45-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="2fd45-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span><span class="sxs-lookup"><span data-stu-id="2fd45-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="2fd45-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="2fd45-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span><span class="sxs-lookup"><span data-stu-id="2fd45-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="2fd45-157">For example, a watchdog reported an error against a replica.</span><span class="sxs-lookup"><span data-stu-id="2fd45-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="2fd45-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span><span class="sxs-lookup"><span data-stu-id="2fd45-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="2fd45-159">The health statistics for all children types of the entities that have children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="2fd45-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd45-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="2fd45-161">Service health shows the total number of partitions and replicas under the specified service.</span><span class="sxs-lookup"><span data-stu-id="2fd45-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="2fd45-162">Get cluster health</span><span class="sxs-lookup"><span data-stu-id="2fd45-162">Get cluster health</span></span>
<span data-ttu-id="2fd45-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span><span class="sxs-lookup"><span data-stu-id="2fd45-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="2fd45-164">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-164">Input:</span></span>

* <span data-ttu-id="2fd45-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span><span class="sxs-lookup"><span data-stu-id="2fd45-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="2fd45-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="2fd45-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="2fd45-169">[Optional] Filter to exclude health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="2fd45-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="2fd45-171">Only applicable when the health statistics are not excluded.</span><span class="sxs-lookup"><span data-stu-id="2fd45-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="2fd45-172">By default, the health statistics include only statistics for user applications and not the System application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-173">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-173">API</span></span>
<span data-ttu-id="2fd45-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="2fd45-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="2fd45-175">The following call gets the cluster health:</span><span class="sxs-lookup"><span data-stu-id="2fd45-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="2fd45-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span><span class="sxs-lookup"><span data-stu-id="2fd45-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="2fd45-177">It specifies that the health statistics include the fabric:/System statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="2fd45-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span><span class="sxs-lookup"><span data-stu-id="2fd45-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-179">PowerShell</span></span>
<span data-ttu-id="2fd45-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="2fd45-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span><span class="sxs-lookup"><span data-stu-id="2fd45-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="2fd45-183">The following cmdlet gets cluster health by using default health policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="2fd45-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span><span class="sxs-lookup"><span data-stu-id="2fd45-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="2fd45-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span><span class="sxs-lookup"><span data-stu-id="2fd45-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="2fd45-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="2fd45-187">It filters results to get only applications and nodes in error or warning.</span><span class="sxs-lookup"><span data-stu-id="2fd45-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="2fd45-188">As a result, no nodes are returned, as they are all healthy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="2fd45-189">Only the fabric:/WordCount application respects the applications filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="2fd45-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd45-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="2fd45-191">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-191">REST</span></span>
<span data-ttu-id="2fd45-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="2fd45-193">Get node health</span><span class="sxs-lookup"><span data-stu-id="2fd45-193">Get node health</span></span>
<span data-ttu-id="2fd45-194">Returns the health of a node entity and contains the health events reported on the node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="2fd45-195">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-195">Input:</span></span>

* <span data-ttu-id="2fd45-196">[Required] The node name that identifies the node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="2fd45-197">[Optional] The cluster health policy settings used to evaluate health.</span><span class="sxs-lookup"><span data-stu-id="2fd45-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="2fd45-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-200">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-200">API</span></span>
<span data-ttu-id="2fd45-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="2fd45-202">The following code gets the node health for the specified node name:</span><span class="sxs-lookup"><span data-stu-id="2fd45-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="2fd45-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="2fd45-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-204">PowerShell</span></span>
<span data-ttu-id="2fd45-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="2fd45-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="2fd45-207">The following cmdlet gets the node health by using default health policies:</span><span class="sxs-lookup"><span data-stu-id="2fd45-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="2fd45-208">The following cmdlet gets the health of all nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="2fd45-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="2fd45-209">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-209">REST</span></span>
<span data-ttu-id="2fd45-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="2fd45-211">Get application health</span><span class="sxs-lookup"><span data-stu-id="2fd45-211">Get application health</span></span>
<span data-ttu-id="2fd45-212">Returns the health of an application entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-212">Returns the health of an application entity.</span></span> <span data-ttu-id="2fd45-213">It contains the health states of the deployed application and service children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="2fd45-214">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-214">Input:</span></span>

* <span data-ttu-id="2fd45-215">[Required] The application name (URI) that identifies the application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="2fd45-216">[Optional] The application health policy used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="2fd45-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="2fd45-219">[Optional] Filter to exclude the health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="2fd45-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span><span class="sxs-lookup"><span data-stu-id="2fd45-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-221">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-221">API</span></span>
<span data-ttu-id="2fd45-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="2fd45-223">The following code gets the application health for the specified application name (URI):</span><span class="sxs-lookup"><span data-stu-id="2fd45-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="2fd45-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="2fd45-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-225">PowerShell</span></span>
<span data-ttu-id="2fd45-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2fd45-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="2fd45-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span><span class="sxs-lookup"><span data-stu-id="2fd45-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="2fd45-229">The following PowerShell cmdlet passes in custom policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="2fd45-230">It also filters children and events.</span><span class="sxs-lookup"><span data-stu-id="2fd45-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="2fd45-231">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-231">REST</span></span>
<span data-ttu-id="2fd45-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="2fd45-233">Get service health</span><span class="sxs-lookup"><span data-stu-id="2fd45-233">Get service health</span></span>
<span data-ttu-id="2fd45-234">Returns the health of a service entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-234">Returns the health of a service entity.</span></span> <span data-ttu-id="2fd45-235">It contains the partition health states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-235">It contains the partition health states.</span></span> <span data-ttu-id="2fd45-236">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-236">Input:</span></span>

* <span data-ttu-id="2fd45-237">[Required] The service name (URI) that identifies the service.</span><span class="sxs-lookup"><span data-stu-id="2fd45-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="2fd45-238">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="2fd45-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="2fd45-241">[Optional] Filter to exclude health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="2fd45-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span><span class="sxs-lookup"><span data-stu-id="2fd45-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-243">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-243">API</span></span>
<span data-ttu-id="2fd45-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="2fd45-245">The following example gets the health of a service with specified service name (URI):</span><span class="sxs-lookup"><span data-stu-id="2fd45-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="2fd45-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="2fd45-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-247">PowerShell</span></span>
<span data-ttu-id="2fd45-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="2fd45-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-250">The following cmdlet gets the service health by using default health policies:</span><span class="sxs-lookup"><span data-stu-id="2fd45-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="2fd45-251">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-251">REST</span></span>
<span data-ttu-id="2fd45-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="2fd45-253">Get partition health</span><span class="sxs-lookup"><span data-stu-id="2fd45-253">Get partition health</span></span>
<span data-ttu-id="2fd45-254">Returns the health of a partition entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="2fd45-255">It contains the replica health states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-255">It contains the replica health states.</span></span> <span data-ttu-id="2fd45-256">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-256">Input:</span></span>

* <span data-ttu-id="2fd45-257">[Required] The partition ID (GUID) that identifies the partition.</span><span class="sxs-lookup"><span data-stu-id="2fd45-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="2fd45-258">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="2fd45-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="2fd45-261">[Optional] Filter to exclude health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="2fd45-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-263">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-263">API</span></span>
<span data-ttu-id="2fd45-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="2fd45-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="2fd45-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-266">PowerShell</span></span>
<span data-ttu-id="2fd45-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="2fd45-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span><span class="sxs-lookup"><span data-stu-id="2fd45-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="2fd45-270">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-270">REST</span></span>
<span data-ttu-id="2fd45-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="2fd45-272">Get replica health</span><span class="sxs-lookup"><span data-stu-id="2fd45-272">Get replica health</span></span>
<span data-ttu-id="2fd45-273">Returns the health of a stateful service replica or a stateless service instance.</span><span class="sxs-lookup"><span data-stu-id="2fd45-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="2fd45-274">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-274">Input:</span></span>

* <span data-ttu-id="2fd45-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span><span class="sxs-lookup"><span data-stu-id="2fd45-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="2fd45-276">[Optional] The application health policy parameters used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="2fd45-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-279">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-279">API</span></span>
<span data-ttu-id="2fd45-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="2fd45-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="2fd45-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-282">PowerShell</span></span>
<span data-ttu-id="2fd45-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="2fd45-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span><span class="sxs-lookup"><span data-stu-id="2fd45-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="2fd45-286">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-286">REST</span></span>
<span data-ttu-id="2fd45-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="2fd45-288">Get deployed application health</span><span class="sxs-lookup"><span data-stu-id="2fd45-288">Get deployed application health</span></span>
<span data-ttu-id="2fd45-289">Returns the health of an application deployed on a node entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="2fd45-290">It contains the deployed service package health states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="2fd45-291">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-291">Input:</span></span>

* <span data-ttu-id="2fd45-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="2fd45-293">[Optional] The application health policy used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="2fd45-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="2fd45-296">[Optional] Filter to exclude health statistics.</span><span class="sxs-lookup"><span data-stu-id="2fd45-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="2fd45-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-298">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-298">API</span></span>
<span data-ttu-id="2fd45-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="2fd45-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="2fd45-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="2fd45-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-301">PowerShell</span></span>
<span data-ttu-id="2fd45-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2fd45-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="2fd45-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="2fd45-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="2fd45-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="2fd45-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="2fd45-306">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-306">REST</span></span>
<span data-ttu-id="2fd45-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="2fd45-308">Get deployed service package health</span><span class="sxs-lookup"><span data-stu-id="2fd45-308">Get deployed service package health</span></span>
<span data-ttu-id="2fd45-309">Returns the health of a deployed service package entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="2fd45-310">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-310">Input:</span></span>

* <span data-ttu-id="2fd45-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span><span class="sxs-lookup"><span data-stu-id="2fd45-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="2fd45-312">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="2fd45-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="2fd45-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="2fd45-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="2fd45-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-315">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-315">API</span></span>
<span data-ttu-id="2fd45-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="2fd45-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="2fd45-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="2fd45-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="2fd45-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-318">PowerShell</span></span>
<span data-ttu-id="2fd45-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="2fd45-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="2fd45-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="2fd45-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span><span class="sxs-lookup"><span data-stu-id="2fd45-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="2fd45-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span><span class="sxs-lookup"><span data-stu-id="2fd45-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="2fd45-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="2fd45-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="2fd45-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span><span class="sxs-lookup"><span data-stu-id="2fd45-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="2fd45-325">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-325">REST</span></span>
<span data-ttu-id="2fd45-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="2fd45-327">Health chunk queries</span><span class="sxs-lookup"><span data-stu-id="2fd45-327">Health chunk queries</span></span>
<span data-ttu-id="2fd45-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="2fd45-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span><span class="sxs-lookup"><span data-stu-id="2fd45-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="2fd45-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span><span class="sxs-lookup"><span data-stu-id="2fd45-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="2fd45-331">By default, no children are included, as opposed to health commands that always include first-level children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="2fd45-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="2fd45-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span><span class="sxs-lookup"><span data-stu-id="2fd45-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="2fd45-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="2fd45-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span><span class="sxs-lookup"><span data-stu-id="2fd45-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="2fd45-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span><span class="sxs-lookup"><span data-stu-id="2fd45-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="2fd45-337">You can express complex health query such as:</span><span class="sxs-lookup"><span data-stu-id="2fd45-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="2fd45-338">Return only applications in error, and for those applications include all services in warning or error.</span><span class="sxs-lookup"><span data-stu-id="2fd45-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="2fd45-339">For returned services, include all partitions.</span><span class="sxs-lookup"><span data-stu-id="2fd45-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="2fd45-340">Return only the health of four applications, specified by their names.</span><span class="sxs-lookup"><span data-stu-id="2fd45-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="2fd45-341">Return only the health of applications of a desired application type.</span><span class="sxs-lookup"><span data-stu-id="2fd45-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="2fd45-342">Return all deployed entities on a node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="2fd45-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="2fd45-344">Return all replicas in error.</span><span class="sxs-lookup"><span data-stu-id="2fd45-344">Return all replicas in error.</span></span> <span data-ttu-id="2fd45-345">Returns all applications, services, partitions, and only replicas in error.</span><span class="sxs-lookup"><span data-stu-id="2fd45-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="2fd45-346">Return all applications.</span><span class="sxs-lookup"><span data-stu-id="2fd45-346">Return all applications.</span></span> <span data-ttu-id="2fd45-347">For a specified service, include all partitions.</span><span class="sxs-lookup"><span data-stu-id="2fd45-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="2fd45-348">Currently, the health chunk query is exposed only for the cluster entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="2fd45-349">It returns a cluster health chunk, which contains:</span><span class="sxs-lookup"><span data-stu-id="2fd45-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="2fd45-350">The cluster aggregated health state.</span><span class="sxs-lookup"><span data-stu-id="2fd45-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="2fd45-351">The health state chunk list of nodes that respect input filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="2fd45-352">The health state chunk list of applications that respect input filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="2fd45-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="2fd45-354">Same for the children of services and deployed applications.</span><span class="sxs-lookup"><span data-stu-id="2fd45-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="2fd45-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span><span class="sxs-lookup"><span data-stu-id="2fd45-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="2fd45-356">Cluster health chunk query</span><span class="sxs-lookup"><span data-stu-id="2fd45-356">Cluster health chunk query</span></span>
<span data-ttu-id="2fd45-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="2fd45-358">Input:</span><span class="sxs-lookup"><span data-stu-id="2fd45-358">Input:</span></span>

* <span data-ttu-id="2fd45-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span><span class="sxs-lookup"><span data-stu-id="2fd45-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="2fd45-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="2fd45-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="2fd45-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span><span class="sxs-lookup"><span data-stu-id="2fd45-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="2fd45-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span><span class="sxs-lookup"><span data-stu-id="2fd45-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="2fd45-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span><span class="sxs-lookup"><span data-stu-id="2fd45-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="2fd45-364">If empty, the children are not returned by default.</span><span class="sxs-lookup"><span data-stu-id="2fd45-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="2fd45-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="2fd45-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="2fd45-366">The application filters can recursively specify advanced filters for children.</span><span class="sxs-lookup"><span data-stu-id="2fd45-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="2fd45-367">The chunk result includes the children that respect the filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="2fd45-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span><span class="sxs-lookup"><span data-stu-id="2fd45-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="2fd45-369">That extra information can be obtained using the existing cluster health query.</span><span class="sxs-lookup"><span data-stu-id="2fd45-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="2fd45-370">API</span><span class="sxs-lookup"><span data-stu-id="2fd45-370">API</span></span>
<span data-ttu-id="2fd45-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="2fd45-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="2fd45-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="2fd45-373">The following code gets cluster health chunk with advanced filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="2fd45-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd45-374">PowerShell</span></span>
<span data-ttu-id="2fd45-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="2fd45-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="2fd45-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd45-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="2fd45-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span><span class="sxs-lookup"><span data-stu-id="2fd45-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="2fd45-378">The following cmdlet gets cluster chunk with application filters.</span><span class="sxs-lookup"><span data-stu-id="2fd45-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="2fd45-379">The following cmdlet returns all deployed entities on a node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="2fd45-380">REST</span><span class="sxs-lookup"><span data-stu-id="2fd45-380">REST</span></span>
<span data-ttu-id="2fd45-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span><span class="sxs-lookup"><span data-stu-id="2fd45-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="2fd45-382">General queries</span><span class="sxs-lookup"><span data-stu-id="2fd45-382">General queries</span></span>
<span data-ttu-id="2fd45-383">General queries return a list of Service Fabric entities of a specified type.</span><span class="sxs-lookup"><span data-stu-id="2fd45-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="2fd45-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span><span class="sxs-lookup"><span data-stu-id="2fd45-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="2fd45-385">These queries aggregate subqueries from multiple components.</span><span class="sxs-lookup"><span data-stu-id="2fd45-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="2fd45-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span><span class="sxs-lookup"><span data-stu-id="2fd45-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="2fd45-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span><span class="sxs-lookup"><span data-stu-id="2fd45-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="2fd45-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span><span class="sxs-lookup"><span data-stu-id="2fd45-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="2fd45-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="2fd45-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span><span class="sxs-lookup"><span data-stu-id="2fd45-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="2fd45-391">Follow up with a health query for the entity.</span><span class="sxs-lookup"><span data-stu-id="2fd45-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="2fd45-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span><span class="sxs-lookup"><span data-stu-id="2fd45-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="2fd45-393">It may also give you more details from the health store about why the entity is not exposed.</span><span class="sxs-lookup"><span data-stu-id="2fd45-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="2fd45-394">The queries that contain **HealthState** for entities are:</span><span class="sxs-lookup"><span data-stu-id="2fd45-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="2fd45-395">Node list: Returns the list nodes in the cluster (paged).</span><span class="sxs-lookup"><span data-stu-id="2fd45-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="2fd45-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="2fd45-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="2fd45-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="2fd45-398">Application list: Returns the list of applications in the cluster (paged).</span><span class="sxs-lookup"><span data-stu-id="2fd45-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="2fd45-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="2fd45-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="2fd45-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="2fd45-401">Service list: Returns the list of services in an application (paged).</span><span class="sxs-lookup"><span data-stu-id="2fd45-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="2fd45-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="2fd45-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="2fd45-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="2fd45-404">Partition list: Returns the list of partitions in a service (paged).</span><span class="sxs-lookup"><span data-stu-id="2fd45-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="2fd45-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="2fd45-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="2fd45-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="2fd45-407">Replica list: Returns the list of replicas in a partition (paged).</span><span class="sxs-lookup"><span data-stu-id="2fd45-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="2fd45-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="2fd45-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="2fd45-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="2fd45-410">Deployed application list: Returns the list of deployed applications on a node.</span><span class="sxs-lookup"><span data-stu-id="2fd45-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="2fd45-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="2fd45-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="2fd45-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="2fd45-413">Deployed service package list: Returns the list of service packages in a deployed application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="2fd45-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="2fd45-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="2fd45-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="2fd45-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="2fd45-416">Some of the queries return paged results.</span><span class="sxs-lookup"><span data-stu-id="2fd45-416">Some of the queries return paged results.</span></span> <span data-ttu-id="2fd45-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="2fd45-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="2fd45-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span><span class="sxs-lookup"><span data-stu-id="2fd45-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="2fd45-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span><span class="sxs-lookup"><span data-stu-id="2fd45-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="2fd45-420">Examples</span><span class="sxs-lookup"><span data-stu-id="2fd45-420">Examples</span></span>
<span data-ttu-id="2fd45-421">The following code gets the unhealthy applications in the cluster:</span><span class="sxs-lookup"><span data-stu-id="2fd45-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="2fd45-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="2fd45-423">Notice that health state is at warning.</span><span class="sxs-lookup"><span data-stu-id="2fd45-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="2fd45-424">The following cmdlet gets the services with a health state of error:</span><span class="sxs-lookup"><span data-stu-id="2fd45-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="2fd45-425">Cluster and application upgrades</span><span class="sxs-lookup"><span data-stu-id="2fd45-425">Cluster and application upgrades</span></span>
<span data-ttu-id="2fd45-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span><span class="sxs-lookup"><span data-stu-id="2fd45-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="2fd45-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span><span class="sxs-lookup"><span data-stu-id="2fd45-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="2fd45-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span><span class="sxs-lookup"><span data-stu-id="2fd45-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="2fd45-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span><span class="sxs-lookup"><span data-stu-id="2fd45-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="2fd45-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd45-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="2fd45-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span><span class="sxs-lookup"><span data-stu-id="2fd45-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="2fd45-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span><span class="sxs-lookup"><span data-stu-id="2fd45-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="2fd45-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span><span class="sxs-lookup"><span data-stu-id="2fd45-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="2fd45-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span><span class="sxs-lookup"><span data-stu-id="2fd45-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="2fd45-435">A watchdog reported an error on one of its replicas.</span><span class="sxs-lookup"><span data-stu-id="2fd45-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="2fd45-436">The upgrade is rolling back because the health checks are not respected.</span><span class="sxs-lookup"><span data-stu-id="2fd45-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="2fd45-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="2fd45-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="2fd45-438">Use health evaluations to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="2fd45-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="2fd45-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span><span class="sxs-lookup"><span data-stu-id="2fd45-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="2fd45-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span><span class="sxs-lookup"><span data-stu-id="2fd45-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="2fd45-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span><span class="sxs-lookup"><span data-stu-id="2fd45-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="2fd45-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span><span class="sxs-lookup"><span data-stu-id="2fd45-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="2fd45-443">The following Powershell cmdlet shows the unhealthy evaluations:</span><span class="sxs-lookup"><span data-stu-id="2fd45-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="2fd45-444">You can look at the replica to get more information:</span><span class="sxs-lookup"><span data-stu-id="2fd45-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="2fd45-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span><span class="sxs-lookup"><span data-stu-id="2fd45-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="2fd45-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span><span class="sxs-lookup"><span data-stu-id="2fd45-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="2fd45-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd45-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2fd45-448">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fd45-448">Next steps</span></span>
[<span data-ttu-id="2fd45-449">Use system health reports to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="2fd45-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="2fd45-450">Add custom Service Fabric health reports</span><span class="sxs-lookup"><span data-stu-id="2fd45-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="2fd45-451">How to report and check service health</span><span class="sxs-lookup"><span data-stu-id="2fd45-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="2fd45-452">Monitor and diagnose services locally</span><span class="sxs-lookup"><span data-stu-id="2fd45-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="2fd45-453">Service Fabric application upgrade</span><span class="sxs-lookup"><span data-stu-id="2fd45-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
