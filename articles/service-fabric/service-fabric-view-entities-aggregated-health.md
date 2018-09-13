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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: oanapl
ms.openlocfilehash: f9f3955b4d628a9399cadaf784e4c41cc0de9901
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548800"
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="4499a-103">View Service Fabric health reports</span><span class="sxs-lookup"><span data-stu-id="4499a-103">View Service Fabric health reports</span></span>
<span data-ttu-id="4499a-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) that comprises health entities on which system components and watchdogs can report local conditions that they are monitoring.</span><span class="sxs-lookup"><span data-stu-id="4499a-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) that comprises health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="4499a-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span><span class="sxs-lookup"><span data-stu-id="4499a-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="4499a-106">Out of the box, the cluster is populated with health reports sent by the system components.</span><span class="sxs-lookup"><span data-stu-id="4499a-106">Out of the box, the cluster is populated with health reports sent by the system components.</span></span> <span data-ttu-id="4499a-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4499a-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="4499a-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span><span class="sxs-lookup"><span data-stu-id="4499a-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="4499a-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span><span class="sxs-lookup"><span data-stu-id="4499a-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="4499a-110">Health queries (through PowerShell, the API, or REST)</span><span class="sxs-lookup"><span data-stu-id="4499a-110">Health queries (through PowerShell, the API, or REST)</span></span>
* <span data-ttu-id="4499a-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, the API, or REST)</span><span class="sxs-lookup"><span data-stu-id="4499a-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, the API, or REST)</span></span>

<span data-ttu-id="4499a-112">To demonstrate these options, let's use a local cluster with five nodes.</span><span class="sxs-lookup"><span data-stu-id="4499a-112">To demonstrate these options, let's use a local cluster with five nodes.</span></span> <span data-ttu-id="4499a-113">Next to the **fabric:/System** application (which exists out of the box), some other applications are deployed.</span><span class="sxs-lookup"><span data-stu-id="4499a-113">Next to the **fabric:/System** application (which exists out of the box), some other applications are deployed.</span></span> <span data-ttu-id="4499a-114">One of these applications is **fabric:/WordCount**.</span><span class="sxs-lookup"><span data-stu-id="4499a-114">One of these applications is **fabric:/WordCount**.</span></span> <span data-ttu-id="4499a-115">This application contains a stateful service configured with seven replicas.</span><span class="sxs-lookup"><span data-stu-id="4499a-115">This application contains a stateful service configured with seven replicas.</span></span> <span data-ttu-id="4499a-116">Because there are only five nodes, the system components show a warning that the partition is below the target count.</span><span class="sxs-lookup"><span data-stu-id="4499a-116">Because there are only five nodes, the system components show a warning that the partition is below the target count.</span></span>

```xml
<Service Name="WordCountService">
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="4499a-117">Health in Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="4499a-117">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="4499a-118">Service Fabric Explorer provides a visual view of the cluster.</span><span class="sxs-lookup"><span data-stu-id="4499a-118">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="4499a-119">In the image below, you can see that:</span><span class="sxs-lookup"><span data-stu-id="4499a-119">In the image below, you can see that:</span></span>

* <span data-ttu-id="4499a-120">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span><span class="sxs-lookup"><span data-stu-id="4499a-120">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="4499a-121">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span><span class="sxs-lookup"><span data-stu-id="4499a-121">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="4499a-122">Since the service is configured with seven replicas, they can't all be placed, as there are only five nodes.</span><span class="sxs-lookup"><span data-stu-id="4499a-122">Since the service is configured with seven replicas, they can't all be placed, as there are only five nodes.</span></span> <span data-ttu-id="4499a-123">Although it's not shown here, the service partition is yellow because of the system report.</span><span class="sxs-lookup"><span data-stu-id="4499a-123">Although it's not shown here, the service partition is yellow because of the system report.</span></span> <span data-ttu-id="4499a-124">The yellow partition triggers the yellow service.</span><span class="sxs-lookup"><span data-stu-id="4499a-124">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="4499a-125">The cluster is red because of the red application.</span><span class="sxs-lookup"><span data-stu-id="4499a-125">The cluster is red because of the red application.</span></span>

<span data-ttu-id="4499a-126">The evaluation uses default policies from the cluster manifest and application manifest.</span><span class="sxs-lookup"><span data-stu-id="4499a-126">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="4499a-127">They are strict policies and do not tolerate any failure.</span><span class="sxs-lookup"><span data-stu-id="4499a-127">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="4499a-128">View of the cluster with Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="4499a-128">View of the cluster with Service Fabric Explorer:</span></span>

![View of the cluster with Service Fabric Explorer.][1]

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="4499a-130">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4499a-130">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="4499a-131">Health queries</span><span class="sxs-lookup"><span data-stu-id="4499a-131">Health queries</span></span>
<span data-ttu-id="4499a-132">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="4499a-132">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="4499a-133">They can be accessed through the API (the methods can be found on **FabricClient.HealthManager**), PowerShell cmdlets, and REST.</span><span class="sxs-lookup"><span data-stu-id="4499a-133">They can be accessed through the API (the methods can be found on **FabricClient.HealthManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="4499a-134">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), and unhealthy evaluations when the entity is not healthy.</span><span class="sxs-lookup"><span data-stu-id="4499a-134">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), and unhealthy evaluations when the entity is not healthy.</span></span>

> [!NOTE]
> <span data-ttu-id="4499a-135">A health entity is returned when it is fully populated in the health store.</span><span class="sxs-lookup"><span data-stu-id="4499a-135">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="4499a-136">The entity must be active (not deleted) and have a system report.</span><span class="sxs-lookup"><span data-stu-id="4499a-136">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="4499a-137">Its parent entities on the hierarchy chain must also have system reports.</span><span class="sxs-lookup"><span data-stu-id="4499a-137">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="4499a-138">If any of these conditions is not satisfied, the health queries return an exception that shows why the entity is not returned.</span><span class="sxs-lookup"><span data-stu-id="4499a-138">If any of these conditions is not satisfied, the health queries return an exception that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="4499a-139">The health queries must pass in the entity identifier, which depends on the entity type.</span><span class="sxs-lookup"><span data-stu-id="4499a-139">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="4499a-140">The queries accept optional health policy parameters.</span><span class="sxs-lookup"><span data-stu-id="4499a-140">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="4499a-141">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span><span class="sxs-lookup"><span data-stu-id="4499a-141">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="4499a-142">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-142">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span>

> [!NOTE]
> <span data-ttu-id="4499a-143">The output filters are applied on the server side, so the message reply size is reduced.</span><span class="sxs-lookup"><span data-stu-id="4499a-143">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="4499a-144">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span><span class="sxs-lookup"><span data-stu-id="4499a-144">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="4499a-145">An entity's health contains:</span><span class="sxs-lookup"><span data-stu-id="4499a-145">An entity's health contains:</span></span>

* <span data-ttu-id="4499a-146">The aggregated health state of the entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-146">The aggregated health state of the entity.</span></span> <span data-ttu-id="4499a-147">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-147">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="4499a-148">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="4499a-148">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="4499a-149">The health events on the entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-149">The health events on the entity.</span></span>
* <span data-ttu-id="4499a-150">The collection of health states of all children for the entities that can have children.</span><span class="sxs-lookup"><span data-stu-id="4499a-150">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="4499a-151">The health states contain entity identifiers and the aggregated health state.</span><span class="sxs-lookup"><span data-stu-id="4499a-151">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="4499a-152">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span><span class="sxs-lookup"><span data-stu-id="4499a-152">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="4499a-153">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span><span class="sxs-lookup"><span data-stu-id="4499a-153">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="4499a-154">Get cluster health</span><span class="sxs-lookup"><span data-stu-id="4499a-154">Get cluster health</span></span>
<span data-ttu-id="4499a-155">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span><span class="sxs-lookup"><span data-stu-id="4499a-155">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="4499a-156">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-156">Input:</span></span>

* <span data-ttu-id="4499a-157">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span><span class="sxs-lookup"><span data-stu-id="4499a-157">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="4499a-158">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-158">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="4499a-159">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-159">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-160">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-160">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-161">API</span><span class="sxs-lookup"><span data-stu-id="4499a-161">API</span></span>
<span data-ttu-id="4499a-162">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="4499a-162">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="4499a-163">The following call gets the cluster health:</span><span class="sxs-lookup"><span data-stu-id="4499a-163">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="4499a-164">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span><span class="sxs-lookup"><span data-stu-id="4499a-164">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="4499a-165">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span><span class="sxs-lookup"><span data-stu-id="4499a-165">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

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
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4499a-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-166">PowerShell</span></span>
<span data-ttu-id="4499a-167">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-167">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="4499a-168">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-168">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-169">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span><span class="sxs-lookup"><span data-stu-id="4499a-169">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="4499a-170">The following cmdlet gets cluster health by using default health policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-170">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="4499a-171">The aggregated health state is in warning, because the fabric:/WordCount application is in warning.</span><span class="sxs-lookup"><span data-stu-id="4499a-171">The aggregated health state is in warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="4499a-172">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span><span class="sxs-lookup"><span data-stu-id="4499a-172">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS C:\> Get-ServiceFabricClusterHealth

AggregatedHealthState   : Warning
UnhealthyEvaluations    :
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.

                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.

                              Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                              Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.

                                  Unhealthy event: SourceId='System.PLB',
                          Property='ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b', HealthState='Warning',
                          ConsiderWarningAsError=false.


NodeHealthStates        :
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok

                          NodeName              : _Node_0
                          AggregatedHealthState : Ok

                          NodeName              : _Node_1
                          AggregatedHealthState : Ok

                          NodeName              : _Node_3
                          AggregatedHealthState : Ok

                          NodeName              : _Node_4
                          AggregatedHealthState : Ok

ApplicationHealthStates :
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok

                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning

HealthEvents            : None
```

<span data-ttu-id="4499a-173">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span><span class="sxs-lookup"><span data-stu-id="4499a-173">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="4499a-174">It filters results to get only error or warning applications and nodes.</span><span class="sxs-lookup"><span data-stu-id="4499a-174">It filters results to get only error or warning applications and nodes.</span></span> <span data-ttu-id="4499a-175">As a result, no nodes are returned, as they are all healthy.</span><span class="sxs-lookup"><span data-stu-id="4499a-175">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="4499a-176">Only the fabric:/WordCount application respects the applications filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-176">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="4499a-177">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span><span class="sxs-lookup"><span data-stu-id="4499a-177">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS c:\> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error"


AggregatedHealthState   : Error
UnhealthyEvaluations    :
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.

                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.

                              Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                              Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                  Unhealthy event: SourceId='System.PLB',
                          Property='ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b', HealthState='Warning',
                          ConsiderWarningAsError=true.


NodeHealthStates        : None
ApplicationHealthStates :
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error

HealthEvents            : None

```

### <a name="rest"></a><span data-ttu-id="4499a-178">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-178">REST</span></span>
<span data-ttu-id="4499a-179">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-179">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="4499a-180">Get node health</span><span class="sxs-lookup"><span data-stu-id="4499a-180">Get node health</span></span>
<span data-ttu-id="4499a-181">Returns the health of a node entity and contains the health events reported on the node.</span><span class="sxs-lookup"><span data-stu-id="4499a-181">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="4499a-182">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-182">Input:</span></span>

* <span data-ttu-id="4499a-183">[Required] The node name that identifies the node.</span><span class="sxs-lookup"><span data-stu-id="4499a-183">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="4499a-184">[Optional] The cluster health policy settings used to evaluate health.</span><span class="sxs-lookup"><span data-stu-id="4499a-184">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="4499a-185">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-185">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-186">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-186">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-187">API</span><span class="sxs-lookup"><span data-stu-id="4499a-187">API</span></span>
<span data-ttu-id="4499a-188">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-188">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4499a-189">The following code gets the node health for the specified node name:</span><span class="sxs-lookup"><span data-stu-id="4499a-189">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="4499a-190">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="4499a-190">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4499a-191">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-191">PowerShell</span></span>
<span data-ttu-id="4499a-192">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-192">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="4499a-193">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-193">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>
<span data-ttu-id="4499a-194">The following cmdlet gets the node health by using default health policies:</span><span class="sxs-lookup"><span data-stu-id="4499a-194">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 6
                        SentAt                : 3/22/2016 7:47:56 PM
                        ReceivedAt            : 3/22/2016 7:48:19 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:48:19 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="4499a-195">The following cmdlet gets the health of all nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="4499a-195">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_2                     Ok
_Node_0                     Ok
_Node_1                     Ok
_Node_3                     Ok
_Node_4                     Ok
```

### <a name="rest"></a><span data-ttu-id="4499a-196">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-196">REST</span></span>
<span data-ttu-id="4499a-197">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-197">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="4499a-198">Get application health</span><span class="sxs-lookup"><span data-stu-id="4499a-198">Get application health</span></span>
<span data-ttu-id="4499a-199">Returns the health of an application entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-199">Returns the health of an application entity.</span></span> <span data-ttu-id="4499a-200">It contains the health states of the deployed application and service children.</span><span class="sxs-lookup"><span data-stu-id="4499a-200">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="4499a-201">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-201">Input:</span></span>

* <span data-ttu-id="4499a-202">[Required] The application name (URI) that identifies the application.</span><span class="sxs-lookup"><span data-stu-id="4499a-202">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="4499a-203">[Optional] The application health policy used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-203">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="4499a-204">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-204">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-205">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-205">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-206">API</span><span class="sxs-lookup"><span data-stu-id="4499a-206">API</span></span>
<span data-ttu-id="4499a-207">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-207">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4499a-208">The following code gets the application health for the specified application name (URI):</span><span class="sxs-lookup"><span data-stu-id="4499a-208">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="4499a-209">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4499a-209">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="4499a-210">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-210">PowerShell</span></span>
<span data-ttu-id="4499a-211">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-211">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth).</span></span> <span data-ttu-id="4499a-212">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-212">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-213">The following cmdlet returns the health of the **fabric:/WordCount** application:</span><span class="sxs-lookup"><span data-stu-id="4499a-213">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS c:\>
PS C:\WINDOWS\system32>  Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            :
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.

                                      Unhealthy event: SourceId='System.PLB',
                                  Property='ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b', HealthState='Warning',
                                  ConsiderWarningAsError=false.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Ok
                                  SequenceNumber        : 131031545225930951
                                  SentAt                : 3/22/2016 9:08:42 PM
                                  ReceivedAt            : 3/22/2016 9:08:42 PM
                                  TTL                   : Infinite
                                  Description           : Availability checked successfully, latency ok
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 8:55:39 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="4499a-214">The following PowerShell cmdlet passes in custom policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-214">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="4499a-215">It also filters children and events.</span><span class="sxs-lookup"><span data-stu-id="4499a-215">It also filters children and events.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy event: SourceId='System.PLB',
                                  Property='ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b', HealthState='Warning',
                                  ConsiderWarningAsError=true.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="4499a-216">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-216">REST</span></span>
<span data-ttu-id="4499a-217">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-217">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="4499a-218">Get service health</span><span class="sxs-lookup"><span data-stu-id="4499a-218">Get service health</span></span>
<span data-ttu-id="4499a-219">Returns the health of a service entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-219">Returns the health of a service entity.</span></span> <span data-ttu-id="4499a-220">It contains the partition health states.</span><span class="sxs-lookup"><span data-stu-id="4499a-220">It contains the partition health states.</span></span> <span data-ttu-id="4499a-221">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-221">Input:</span></span>

* <span data-ttu-id="4499a-222">[Required] The service name (URI) that identifies the service.</span><span class="sxs-lookup"><span data-stu-id="4499a-222">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="4499a-223">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="4499a-223">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4499a-224">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-224">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-225">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-225">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-226">API</span><span class="sxs-lookup"><span data-stu-id="4499a-226">API</span></span>
<span data-ttu-id="4499a-227">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-227">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4499a-228">The following example gets the health of a service with specified service name (URI):</span><span class="sxs-lookup"><span data-stu-id="4499a-228">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="4499a-229">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="4499a-229">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4499a-230">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-230">PowerShell</span></span>
<span data-ttu-id="4499a-231">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-231">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="4499a-232">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-232">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-233">The following cmdlet gets the service health by using default health policies:</span><span class="sxs-lookup"><span data-stu-id="4499a-233">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB',
                        Property='ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b', HealthState='Warning',
                        ConsiderWarningAsError=false.

PartitionHealthStates :
                        PartitionId           : a1f83a35-d6bf-4d39-b90d-28d15f39599b
                        AggregatedHealthState : Warning

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 10
                        SentAt                : 3/22/2016 7:56:53 PM
                        ReceivedAt            : 3/22/2016 7:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_a1f83a35-d6bf-4d39-b90d-28d15f39599b
                        HealthState           : Warning
                        SequenceNumber        : 131031547693687021
                        SentAt                : 3/22/2016 9:12:49 PM
                        ReceivedAt            : 3/22/2016 9:12:49 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        fabric:/WordCount/WordCountService Secondary Partition a1f83a35-d6bf-4d39-b90d-28d15f39599b could not be placed, possibly,
                        due to the following constraints and properties:  
                        Placement Constraint: N/A
                        Depended Service: N/A

                        Constraint Elimination Sequence:
                        ReplicaExclusionStatic eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        ReplicaExclusionDynamic eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.

                        Nodes Eliminated By Constraints:

                        ReplicaExclusionStatic:
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status:
                        None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status:
                        None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status:
                        None/None
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status:
                        None/None

                        ReplicaExclusionDynamic:
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status:
                        None/None


                        RemoveWhenExpired     : True
                        IsExpired             : False
```

### <a name="rest"></a><span data-ttu-id="4499a-234">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-234">REST</span></span>
<span data-ttu-id="4499a-235">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-235">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="4499a-236">Get partition health</span><span class="sxs-lookup"><span data-stu-id="4499a-236">Get partition health</span></span>
<span data-ttu-id="4499a-237">Returns the health of a partition entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-237">Returns the health of a partition entity.</span></span> <span data-ttu-id="4499a-238">It contains the replica health states.</span><span class="sxs-lookup"><span data-stu-id="4499a-238">It contains the replica health states.</span></span> <span data-ttu-id="4499a-239">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-239">Input:</span></span>

* <span data-ttu-id="4499a-240">[Required] The partition ID (GUID) that identifies the partition.</span><span class="sxs-lookup"><span data-stu-id="4499a-240">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="4499a-241">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="4499a-241">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4499a-242">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-242">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-243">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-243">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-244">API</span><span class="sxs-lookup"><span data-stu-id="4499a-244">API</span></span>
<span data-ttu-id="4499a-245">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-245">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4499a-246">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4499a-246">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="4499a-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-247">PowerShell</span></span>
<span data-ttu-id="4499a-248">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-248">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="4499a-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-250">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service:</span><span class="sxs-lookup"><span data-stu-id="4499a-250">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth


PartitionId           : a1f83a35-d6bf-4d39-b90d-28d15f39599b
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 131031502143040223
                        AggregatedHealthState : Ok

                        ReplicaId             : 131031502346844060
                        AggregatedHealthState : Ok

                        ReplicaId             : 131031502346844059
                        AggregatedHealthState : Ok

                        ReplicaId             : 131031502346844061
                        AggregatedHealthState : Ok

                        ReplicaId             : 131031502346844058
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 76
                        SentAt                : 3/22/2016 7:57:26 PM
                        ReceivedAt            : 3/22/2016 7:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 3/22/2016 7:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4499a-251">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-251">REST</span></span>
<span data-ttu-id="4499a-252">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-252">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="4499a-253">Get replica health</span><span class="sxs-lookup"><span data-stu-id="4499a-253">Get replica health</span></span>
<span data-ttu-id="4499a-254">Returns the health of a stateful service replica or a stateless service instance.</span><span class="sxs-lookup"><span data-stu-id="4499a-254">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="4499a-255">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-255">Input:</span></span>

* <span data-ttu-id="4499a-256">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span><span class="sxs-lookup"><span data-stu-id="4499a-256">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="4499a-257">[Optional] The application health policy parameters used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-257">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="4499a-258">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-258">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-259">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-259">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-260">API</span><span class="sxs-lookup"><span data-stu-id="4499a-260">API</span></span>
<span data-ttu-id="4499a-261">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-261">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4499a-262">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4499a-262">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="4499a-263">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-263">PowerShell</span></span>
<span data-ttu-id="4499a-264">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-264">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="4499a-265">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-265">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-266">The following cmdlet gets the health of the primary replica for all partitions of the service:</span><span class="sxs-lookup"><span data-stu-id="4499a-266">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : a1f83a35-d6bf-4d39-b90d-28d15f39599b
ReplicaId             : 131031502143040223
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131031502145556748
                        SentAt                : 3/22/2016 7:56:54 PM
                        ReceivedAt            : 3/22/2016 7:57:12 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:57:12 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4499a-267">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-267">REST</span></span>
<span data-ttu-id="4499a-268">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-268">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="4499a-269">Get deployed application health</span><span class="sxs-lookup"><span data-stu-id="4499a-269">Get deployed application health</span></span>
<span data-ttu-id="4499a-270">Returns the health of an application deployed on a node entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-270">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="4499a-271">It contains the deployed service package health states.</span><span class="sxs-lookup"><span data-stu-id="4499a-271">It contains the deployed service package health states.</span></span> <span data-ttu-id="4499a-272">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-272">Input:</span></span>

* <span data-ttu-id="4499a-273">[Required] The application name (URI) and node name (string) that identify the deployed application.</span><span class="sxs-lookup"><span data-stu-id="4499a-273">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="4499a-274">[Optional] The application health policy used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-274">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="4499a-275">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-275">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-276">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-276">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-277">API</span><span class="sxs-lookup"><span data-stu-id="4499a-277">API</span></span>
<span data-ttu-id="4499a-278">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-278">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4499a-279">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4499a-279">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="4499a-280">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-280">PowerShell</span></span>
<span data-ttu-id="4499a-281">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-281">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth).</span></span> <span data-ttu-id="4499a-282">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-282">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span> <span data-ttu-id="4499a-283">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth) and look at the deployed application children.</span><span class="sxs-lookup"><span data-stu-id="4499a-283">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth) and look at the deployed application children.</span></span>

<span data-ttu-id="4499a-284">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="4499a-284">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_2


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_2
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates :
                                     ServiceManifestName   : WordCountServicePkg
                                     NodeName              : _Node_2
                                     AggregatedHealthState : Ok

                                     ServiceManifestName   : WordCountWebServicePkg
                                     NodeName              : _Node_2
                                     AggregatedHealthState : Ok

HealthEvents                       :
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131031502143710698
                                     SentAt                : 3/22/2016 7:56:54 PM
                                     ReceivedAt            : 3/22/2016 7:57:12 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 3/22/2016 7:57:12 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4499a-285">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-285">REST</span></span>
<span data-ttu-id="4499a-286">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-286">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="4499a-287">Get deployed service package health</span><span class="sxs-lookup"><span data-stu-id="4499a-287">Get deployed service package health</span></span>
<span data-ttu-id="4499a-288">Returns the health of a deployed service package entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-288">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="4499a-289">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-289">Input:</span></span>

* <span data-ttu-id="4499a-290">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span><span class="sxs-lookup"><span data-stu-id="4499a-290">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="4499a-291">[Optional] The application health policy used to override the application manifest policy.</span><span class="sxs-lookup"><span data-stu-id="4499a-291">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4499a-292">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span><span class="sxs-lookup"><span data-stu-id="4499a-292">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4499a-293">All events are used to evaluate the entity aggregated health, regardless of the filter.</span><span class="sxs-lookup"><span data-stu-id="4499a-293">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-294">API</span><span class="sxs-lookup"><span data-stu-id="4499a-294">API</span></span>
<span data-ttu-id="4499a-295">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4499a-295">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4499a-296">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4499a-296">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="4499a-297">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-297">PowerShell</span></span>
<span data-ttu-id="4499a-298">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="4499a-298">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="4499a-299">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-299">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span> <span data-ttu-id="4499a-300">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth) and look at the deployed applications.</span><span class="sxs-lookup"><span data-stu-id="4499a-300">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricapplicationhealth) and look at the deployed applications.</span></span> <span data-ttu-id="4499a-301">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth) output.</span><span class="sxs-lookup"><span data-stu-id="4499a-301">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth) output.</span></span>

<span data-ttu-id="4499a-302">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="4499a-302">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="4499a-303">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span><span class="sxs-lookup"><span data-stu-id="4499a-303">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName       : fabric:/WordCount
ServiceManifestName   : WordCountServicePkg
NodeName              : _Node_2
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.Hosting
                        Property              : Activation
                        HealthState           : Ok
                        SequenceNumber        : 131031502301306211
                        SentAt                : 3/22/2016 7:57:10 PM
                        ReceivedAt            : 3/22/2016 7:57:12 PM
                        TTL                   : Infinite
                        Description           : The ServicePackage was activated successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:57:12 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.Hosting
                        Property              : CodePackageActivation:Code:EntryPoint
                        HealthState           : Ok
                        SequenceNumber        : 131031502301568982
                        SentAt                : 3/22/2016 7:57:10 PM
                        ReceivedAt            : 3/22/2016 7:57:12 PM
                        TTL                   : Infinite
                        Description           : The CodePackage was activated successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:57:12 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.Hosting
                        Property              : ServiceTypeRegistration:WordCountServiceType
                        HealthState           : Ok
                        SequenceNumber        : 131031502314788519
                        SentAt                : 3/22/2016 7:57:11 PM
                        ReceivedAt            : 3/22/2016 7:57:12 PM
                        TTL                   : Infinite
                        Description           : The ServiceType was registered successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 3/22/2016 7:57:12 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4499a-304">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-304">REST</span></span>
<span data-ttu-id="4499a-305">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-305">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="4499a-306">Health chunk queries</span><span class="sxs-lookup"><span data-stu-id="4499a-306">Health chunk queries</span></span>
<span data-ttu-id="4499a-307">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-307">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="4499a-308">It supports advanced filters that allow much flexibility to express which specific children to be returned, identified by their unique identifier or other group identifier and/or health state.</span><span class="sxs-lookup"><span data-stu-id="4499a-308">It supports advanced filters that allow much flexibility to express which specific children to be returned, identified by their unique identifier or other group identifier and/or health state.</span></span> <span data-ttu-id="4499a-309">By default, no children are included, as opposed to health commands that always include first-level children.</span><span class="sxs-lookup"><span data-stu-id="4499a-309">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="4499a-310">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-310">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="4499a-311">To get the children of the children, you must call additional health APIs for each entity of interest.</span><span class="sxs-lookup"><span data-stu-id="4499a-311">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="4499a-312">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-312">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="4499a-313">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span><span class="sxs-lookup"><span data-stu-id="4499a-313">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="4499a-314">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span><span class="sxs-lookup"><span data-stu-id="4499a-314">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="4499a-315">You can express complex health query such as:</span><span class="sxs-lookup"><span data-stu-id="4499a-315">You can express complex health query such as:</span></span>

* <span data-ttu-id="4499a-316">Return only applications at error, and for those applications include all services at warning|error.</span><span class="sxs-lookup"><span data-stu-id="4499a-316">Return only applications at error, and for those applications include all services at warning|error.</span></span> <span data-ttu-id="4499a-317">For returned services, include all partitions.</span><span class="sxs-lookup"><span data-stu-id="4499a-317">For returned services, include all partitions.</span></span>
* <span data-ttu-id="4499a-318">Return only the health of 4 applications, specified by their names.</span><span class="sxs-lookup"><span data-stu-id="4499a-318">Return only the health of 4 applications, specified by their names.</span></span>
* <span data-ttu-id="4499a-319">Return only the health of applications of a desired application type.</span><span class="sxs-lookup"><span data-stu-id="4499a-319">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="4499a-320">Return all deployed entities on a node.</span><span class="sxs-lookup"><span data-stu-id="4499a-320">Return all deployed entities on a node.</span></span> <span data-ttu-id="4499a-321">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span><span class="sxs-lookup"><span data-stu-id="4499a-321">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="4499a-322">Return all replicas at error.</span><span class="sxs-lookup"><span data-stu-id="4499a-322">Return all replicas at error.</span></span> <span data-ttu-id="4499a-323">Returns all applications, services, partitions, and only replicas at error.</span><span class="sxs-lookup"><span data-stu-id="4499a-323">Returns all applications, services, partitions, and only replicas at error.</span></span>
* <span data-ttu-id="4499a-324">Return all applications.</span><span class="sxs-lookup"><span data-stu-id="4499a-324">Return all applications.</span></span> <span data-ttu-id="4499a-325">For a specified service, include all partitions.</span><span class="sxs-lookup"><span data-stu-id="4499a-325">For a specified service, include all partitions.</span></span>

<span data-ttu-id="4499a-326">Currently, the health chunk query is exposed only for the cluster entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-326">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="4499a-327">It returns a cluster health chunk, which contains:</span><span class="sxs-lookup"><span data-stu-id="4499a-327">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="4499a-328">The cluster aggregated health state.</span><span class="sxs-lookup"><span data-stu-id="4499a-328">The cluster aggregated health state.</span></span>
* <span data-ttu-id="4499a-329">The health state chunk list of nodes that respect input filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-329">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="4499a-330">The health state chunk list of applications that respect input filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-330">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="4499a-331">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-331">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="4499a-332">Same for the children of services and deployed applications.</span><span class="sxs-lookup"><span data-stu-id="4499a-332">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="4499a-333">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span><span class="sxs-lookup"><span data-stu-id="4499a-333">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="4499a-334">Cluster health chunk query</span><span class="sxs-lookup"><span data-stu-id="4499a-334">Cluster health chunk query</span></span>
<span data-ttu-id="4499a-335">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span><span class="sxs-lookup"><span data-stu-id="4499a-335">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="4499a-336">Input:</span><span class="sxs-lookup"><span data-stu-id="4499a-336">Input:</span></span>

* <span data-ttu-id="4499a-337">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span><span class="sxs-lookup"><span data-stu-id="4499a-337">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="4499a-338">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span><span class="sxs-lookup"><span data-stu-id="4499a-338">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="4499a-339">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span><span class="sxs-lookup"><span data-stu-id="4499a-339">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="4499a-340">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span><span class="sxs-lookup"><span data-stu-id="4499a-340">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="4499a-341">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span><span class="sxs-lookup"><span data-stu-id="4499a-341">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="4499a-342">If empty, the children are not returned by default.</span><span class="sxs-lookup"><span data-stu-id="4499a-342">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="4499a-343">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="4499a-343">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="4499a-344">The application filters can recursively specify advanced filters for children.</span><span class="sxs-lookup"><span data-stu-id="4499a-344">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="4499a-345">The chunk result includes the children that respect the filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-345">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="4499a-346">Currently, the chunk query does not return unhealthy evaluations or entity events.</span><span class="sxs-lookup"><span data-stu-id="4499a-346">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="4499a-347">That extra information can be obtained using the existing cluster health query.</span><span class="sxs-lookup"><span data-stu-id="4499a-347">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="4499a-348">API</span><span class="sxs-lookup"><span data-stu-id="4499a-348">API</span></span>
<span data-ttu-id="4499a-349">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="4499a-349">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="4499a-350">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-350">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="4499a-351">The following code gets cluster health chunk with advanced filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-351">The following code gets cluster health chunk with advanced filters.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="4499a-352">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4499a-352">PowerShell</span></span>
<span data-ttu-id="4499a-353">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="4499a-353">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="4499a-354">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4499a-354">First, connect to the cluster by using the [Connect-ServiceFabricCluster](https://docs.microsoft.com/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet.</span></span>

<span data-ttu-id="4499a-355">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span><span class="sxs-lookup"><span data-stu-id="4499a-355">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS C:\> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters

HealthState                  : Error
NodeHealthStateChunks        :
                               TotalCount            : 1

                               NodeName              : _Node_1
                               HealthState           : Ok

ApplicationHealthStateChunks : None
```

<span data-ttu-id="4499a-356">The following cmdlet gets cluster chunk with application filters.</span><span class="sxs-lookup"><span data-stu-id="4499a-356">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
$errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
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

                                       PartitionId           : a1f83a35-d6bf-4d39-b90d-28d15f39599b
                                       HealthState           : Error
                                       ReplicaHealthStateChunks :
                                           TotalCount            : 5

                                           ReplicaOrInstanceId   : 131031502143040223
                                           HealthState           : Ok

                                           ReplicaOrInstanceId   : 131031502346844060
                                           HealthState           : Ok

                                           ReplicaOrInstanceId   : 131031502346844059
                                           HealthState           : Ok

                                           ReplicaOrInstanceId   : 131031502346844061
                                           HealthState           : Ok

                                           ReplicaOrInstanceId   : 131031502346844058
                                           HealthState           : Error
```

<span data-ttu-id="4499a-357">The following cmdlet returns all deployed entities on a node.</span><span class="sxs-lookup"><span data-stu-id="4499a-357">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
$errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
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
                                       HealthState           : Ok



                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks :
                                   TotalCount            : 1

                                   NodeName              : _Node_2
                                   HealthState           : Ok
                                   DeployedServicePackageHealthStateChunks :
                                       TotalCount            : 2

                                       ServiceManifestName   : WordCountServicePkg
                                       HealthState           : Ok

                                       ServiceManifestName   : WordCountWebServicePkg
                                       HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="4499a-358">REST</span><span class="sxs-lookup"><span data-stu-id="4499a-358">REST</span></span>
<span data-ttu-id="4499a-359">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span><span class="sxs-lookup"><span data-stu-id="4499a-359">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="4499a-360">General queries</span><span class="sxs-lookup"><span data-stu-id="4499a-360">General queries</span></span>
<span data-ttu-id="4499a-361">General queries return a list of Service Fabric entities of a specified type.</span><span class="sxs-lookup"><span data-stu-id="4499a-361">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="4499a-362">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span><span class="sxs-lookup"><span data-stu-id="4499a-362">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="4499a-363">These queries aggregate subqueries from multiple components.</span><span class="sxs-lookup"><span data-stu-id="4499a-363">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="4499a-364">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span><span class="sxs-lookup"><span data-stu-id="4499a-364">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="4499a-365">General queries return the aggregated health state of the entity and do not contain rich health data.</span><span class="sxs-lookup"><span data-stu-id="4499a-365">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="4499a-366">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span><span class="sxs-lookup"><span data-stu-id="4499a-366">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="4499a-367">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-367">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="4499a-368">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span><span class="sxs-lookup"><span data-stu-id="4499a-368">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="4499a-369">Follow up with a health query for the entity.</span><span class="sxs-lookup"><span data-stu-id="4499a-369">Follow up with a health query for the entity.</span></span> <span data-ttu-id="4499a-370">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span><span class="sxs-lookup"><span data-stu-id="4499a-370">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="4499a-371">It may also give you more details from the health store about why the entity is not exposed.</span><span class="sxs-lookup"><span data-stu-id="4499a-371">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="4499a-372">The queries that contain **HealthState** for entities are:</span><span class="sxs-lookup"><span data-stu-id="4499a-372">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="4499a-373">Node list: Returns the list nodes in the cluster (paged).</span><span class="sxs-lookup"><span data-stu-id="4499a-373">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="4499a-374">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-374">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="4499a-375">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4499a-375">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="4499a-376">Application list: Returns the list of applications in the cluster (paged).</span><span class="sxs-lookup"><span data-stu-id="4499a-376">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="4499a-377">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-377">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="4499a-378">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4499a-378">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="4499a-379">Service list: Returns the list of services in an application (paged).</span><span class="sxs-lookup"><span data-stu-id="4499a-379">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="4499a-380">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-380">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="4499a-381">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="4499a-381">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="4499a-382">Partition list: Returns the list of partitions in a service (paged).</span><span class="sxs-lookup"><span data-stu-id="4499a-382">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="4499a-383">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-383">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="4499a-384">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="4499a-384">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="4499a-385">Replica list: Returns the list of replicas in a partition (paged).</span><span class="sxs-lookup"><span data-stu-id="4499a-385">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="4499a-386">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-386">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="4499a-387">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4499a-387">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="4499a-388">Deployed application list: Returns the list of deployed applications on a node.</span><span class="sxs-lookup"><span data-stu-id="4499a-388">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="4499a-389">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-389">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="4499a-390">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="4499a-390">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="4499a-391">Deployed service package list: Returns the list of service packages in a deployed application.</span><span class="sxs-lookup"><span data-stu-id="4499a-391">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="4499a-392">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="4499a-392">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="4499a-393">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="4499a-393">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="4499a-394">Some of the queries return paged results.</span><span class="sxs-lookup"><span data-stu-id="4499a-394">Some of the queries return paged results.</span></span> <span data-ttu-id="4499a-395">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="4499a-395">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="4499a-396">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span><span class="sxs-lookup"><span data-stu-id="4499a-396">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="4499a-397">You should continue to call the same query and pass in the continuation token from the previous query to get next results.</span><span class="sxs-lookup"><span data-stu-id="4499a-397">You should continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="4499a-398">Examples</span><span class="sxs-lookup"><span data-stu-id="4499a-398">Examples</span></span>
<span data-ttu-id="4499a-399">The following code gets the unhealthy applications in the cluster:</span><span class="sxs-lookup"><span data-stu-id="4499a-399">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="4499a-400">The following cmdlet gets the application details for the fabric:/WordCount application.</span><span class="sxs-lookup"><span data-stu-id="4499a-400">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="4499a-401">Notice that health state is at warning.</span><span class="sxs-lookup"><span data-stu-id="4499a-401">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="4499a-402">The following cmdlet gets the services with a health state of warning:</span><span class="sxs-lookup"><span data-stu-id="4499a-402">The following cmdlet gets the services with a health state of warning:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Warning"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Warning
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="4499a-403">Cluster and application upgrades</span><span class="sxs-lookup"><span data-stu-id="4499a-403">Cluster and application upgrades</span></span>
<span data-ttu-id="4499a-404">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span><span class="sxs-lookup"><span data-stu-id="4499a-404">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="4499a-405">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span><span class="sxs-lookup"><span data-stu-id="4499a-405">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="4499a-406">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span><span class="sxs-lookup"><span data-stu-id="4499a-406">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="4499a-407">During a *cluster* upgrade, you can get the cluster upgrade status.</span><span class="sxs-lookup"><span data-stu-id="4499a-407">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="4499a-408">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4499a-408">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="4499a-409">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span><span class="sxs-lookup"><span data-stu-id="4499a-409">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="4499a-410">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span><span class="sxs-lookup"><span data-stu-id="4499a-410">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="4499a-411">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span><span class="sxs-lookup"><span data-stu-id="4499a-411">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="4499a-412">The following shows the application upgrade status for a modified fabric:/WordCount application.</span><span class="sxs-lookup"><span data-stu-id="4499a-412">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="4499a-413">A watchdog reported an error on one of its replicas.</span><span class="sxs-lookup"><span data-stu-id="4499a-413">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="4499a-414">The upgrade is rolling back because the health checks are not respected.</span><span class="sxs-lookup"><span data-stu-id="4499a-414">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2015 5:23:26 PM
FailureTimestampUtc           : 4/21/2015 5:23:37 PM
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

<span data-ttu-id="4499a-415">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="4499a-415">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="4499a-416">Use health evaluations to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="4499a-416">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="4499a-417">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span><span class="sxs-lookup"><span data-stu-id="4499a-417">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="4499a-418">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span><span class="sxs-lookup"><span data-stu-id="4499a-418">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="4499a-419">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span><span class="sxs-lookup"><span data-stu-id="4499a-419">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

> [!NOTE]
> <span data-ttu-id="4499a-420">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span><span class="sxs-lookup"><span data-stu-id="4499a-420">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="4499a-421">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span><span class="sxs-lookup"><span data-stu-id="4499a-421">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="4499a-422">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4499a-422">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4499a-423">Next steps</span><span class="sxs-lookup"><span data-stu-id="4499a-423">Next steps</span></span>
[<span data-ttu-id="4499a-424">Use system health reports to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="4499a-424">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="4499a-425">Add custom Service Fabric health reports</span><span class="sxs-lookup"><span data-stu-id="4499a-425">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="4499a-426">How to report and check service health</span><span class="sxs-lookup"><span data-stu-id="4499a-426">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="4499a-427">Monitor and diagnose services locally</span><span class="sxs-lookup"><span data-stu-id="4499a-427">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="4499a-428">Service Fabric application upgrade</span><span class="sxs-lookup"><span data-stu-id="4499a-428">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

