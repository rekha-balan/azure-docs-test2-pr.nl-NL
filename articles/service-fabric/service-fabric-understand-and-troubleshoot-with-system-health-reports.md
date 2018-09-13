---
title: Troubleshoot with system health reports | Microsoft Docs
description: Describes the health reports sent by Azure Service Fabric components and their usage for troubleshooting cluster or application issues.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: ''
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: oanapl
ms.openlocfilehash: 43f2e2e868b15b8cbfa5323e0e277184806559d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555894"
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="cc40b-103">Use system health reports to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="cc40b-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="cc40b-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span><span class="sxs-lookup"><span data-stu-id="cc40b-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="cc40b-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span><span class="sxs-lookup"><span data-stu-id="cc40b-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="cc40b-106">It also organizes them in a hierarchy that captures entity interactions.</span><span class="sxs-lookup"><span data-stu-id="cc40b-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="cc40b-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc40b-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="cc40b-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span><span class="sxs-lookup"><span data-stu-id="cc40b-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="cc40b-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span><span class="sxs-lookup"><span data-stu-id="cc40b-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="cc40b-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span><span class="sxs-lookup"><span data-stu-id="cc40b-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="cc40b-111">User services can enrich the health data with information specific to their logic.</span><span class="sxs-lookup"><span data-stu-id="cc40b-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="cc40b-112">Watchdogs health reports are visible only *after* the system components create an entity.</span><span class="sxs-lookup"><span data-stu-id="cc40b-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="cc40b-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span><span class="sxs-lookup"><span data-stu-id="cc40b-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="cc40b-114">The same is true when a new instance of the entity is created (for example, a new service replica instance is created).</span><span class="sxs-lookup"><span data-stu-id="cc40b-114">The same is true when a new instance of the entity is created (for example, a new service replica instance is created).</span></span> <span data-ttu-id="cc40b-115">All reports associated with the old instance are deleted and cleaned up from the store.</span><span class="sxs-lookup"><span data-stu-id="cc40b-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="cc40b-116">The system component reports are identified by the source, which starts with the "**System.**"</span><span class="sxs-lookup"><span data-stu-id="cc40b-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="cc40b-117">prefix.</span><span class="sxs-lookup"><span data-stu-id="cc40b-117">prefix.</span></span> <span data-ttu-id="cc40b-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span><span class="sxs-lookup"><span data-stu-id="cc40b-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="cc40b-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span><span class="sxs-lookup"><span data-stu-id="cc40b-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="cc40b-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span><span class="sxs-lookup"><span data-stu-id="cc40b-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="cc40b-121">Cluster system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-121">Cluster system health reports</span></span>
<span data-ttu-id="cc40b-122">The cluster health entity is created automatically in the health store.</span><span class="sxs-lookup"><span data-stu-id="cc40b-122">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="cc40b-123">If everything works properly, it doesn't have a system report.</span><span class="sxs-lookup"><span data-stu-id="cc40b-123">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="cc40b-124">Neighborhood loss</span><span class="sxs-lookup"><span data-stu-id="cc40b-124">Neighborhood loss</span></span>
<span data-ttu-id="cc40b-125">**System.Federation** reports an error when it detects a neighborhood loss.</span><span class="sxs-lookup"><span data-stu-id="cc40b-125">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="cc40b-126">The report is from individual nodes, and the node ID is included in the property name.</span><span class="sxs-lookup"><span data-stu-id="cc40b-126">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="cc40b-127">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span><span class="sxs-lookup"><span data-stu-id="cc40b-127">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="cc40b-128">If more neighborhoods are lost, there are more events.</span><span class="sxs-lookup"><span data-stu-id="cc40b-128">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="cc40b-129">The report specifies the global lease timeout as the time to live.</span><span class="sxs-lookup"><span data-stu-id="cc40b-129">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="cc40b-130">The report is resent every half of the TTL duration for as long as the condition remains active.</span><span class="sxs-lookup"><span data-stu-id="cc40b-130">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="cc40b-131">The event is automatically removed when it expires.</span><span class="sxs-lookup"><span data-stu-id="cc40b-131">The event is automatically removed when it expires.</span></span> <span data-ttu-id="cc40b-132">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span><span class="sxs-lookup"><span data-stu-id="cc40b-132">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="cc40b-133">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="cc40b-133">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="cc40b-134">**Property**: Starts with **Neighborhood** and includes node information</span><span class="sxs-lookup"><span data-stu-id="cc40b-134">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="cc40b-135">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span><span class="sxs-lookup"><span data-stu-id="cc40b-135">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="cc40b-136">Node system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-136">Node system health reports</span></span>
<span data-ttu-id="cc40b-137">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="cc40b-137">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="cc40b-138">Each node should have one report from System.FM showing its state.</span><span class="sxs-lookup"><span data-stu-id="cc40b-138">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="cc40b-139">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="cc40b-139">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="cc40b-140">Node up/down</span><span class="sxs-lookup"><span data-stu-id="cc40b-140">Node up/down</span></span>
<span data-ttu-id="cc40b-141">System.FM reports as OK when the node joins the ring (it's up and running).</span><span class="sxs-lookup"><span data-stu-id="cc40b-141">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="cc40b-142">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span><span class="sxs-lookup"><span data-stu-id="cc40b-142">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="cc40b-143">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span><span class="sxs-lookup"><span data-stu-id="cc40b-143">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="cc40b-144">It considers the node a virtual parent of all deployed entities.</span><span class="sxs-lookup"><span data-stu-id="cc40b-144">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="cc40b-145">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span><span class="sxs-lookup"><span data-stu-id="cc40b-145">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="cc40b-146">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-146">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="cc40b-147">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="cc40b-147">**SourceId**: System.FM</span></span>
* <span data-ttu-id="cc40b-148">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-148">**Property**: State</span></span>
* <span data-ttu-id="cc40b-149">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span><span class="sxs-lookup"><span data-stu-id="cc40b-149">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="cc40b-150">In this case, the health state should be switched back to OK.</span><span class="sxs-lookup"><span data-stu-id="cc40b-150">In this case, the health state should be switched back to OK.</span></span> <span data-ttu-id="cc40b-151">If the node doesn't come back or it fails, the problem needs more investigation.</span><span class="sxs-lookup"><span data-stu-id="cc40b-151">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="cc40b-152">The following example shows the System.FM event with a health state of OK for node up:</span><span class="sxs-lookup"><span data-stu-id="cc40b-152">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 2
                        SentAt                : 4/24/2015 5:27:33 PM
                        ReceivedAt            : 4/24/2015 5:28:50 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 5:28:50 PM

```


### <a name="certificate-expiration"></a><span data-ttu-id="cc40b-153">Certificate expiration</span><span class="sxs-lookup"><span data-stu-id="cc40b-153">Certificate expiration</span></span>
<span data-ttu-id="cc40b-154">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span><span class="sxs-lookup"><span data-stu-id="cc40b-154">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="cc40b-155">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="cc40b-155">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="cc40b-156">When the expiration is at least two weeks away, the report health state is OK.</span><span class="sxs-lookup"><span data-stu-id="cc40b-156">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="cc40b-157">When the expiration is within two weeks, the report type is a warning.</span><span class="sxs-lookup"><span data-stu-id="cc40b-157">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="cc40b-158">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span><span class="sxs-lookup"><span data-stu-id="cc40b-158">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="cc40b-159">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="cc40b-159">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="cc40b-160">**Property**: Starts with **Certificate** and contains more information about the certificate type</span><span class="sxs-lookup"><span data-stu-id="cc40b-160">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="cc40b-161">**Next steps**: Update the certificates if they are near expiration.</span><span class="sxs-lookup"><span data-stu-id="cc40b-161">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="cc40b-162">Load capacity violation</span><span class="sxs-lookup"><span data-stu-id="cc40b-162">Load capacity violation</span></span>
<span data-ttu-id="cc40b-163">The Service Fabric Load Balancer reports a warning if it detects a node capacity violation.</span><span class="sxs-lookup"><span data-stu-id="cc40b-163">The Service Fabric Load Balancer reports a warning if it detects a node capacity violation.</span></span>

* <span data-ttu-id="cc40b-164">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="cc40b-164">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="cc40b-165">**Property**: Starts with **Capacity**</span><span class="sxs-lookup"><span data-stu-id="cc40b-165">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="cc40b-166">**Next steps**: Check provided metrics and view the current capacity on the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-166">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="cc40b-167">Application system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-167">Application system health reports</span></span>
<span data-ttu-id="cc40b-168">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span><span class="sxs-lookup"><span data-stu-id="cc40b-168">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="cc40b-169">State</span><span class="sxs-lookup"><span data-stu-id="cc40b-169">State</span></span>
<span data-ttu-id="cc40b-170">System.CM reports as OK when the application has been created or updated.</span><span class="sxs-lookup"><span data-stu-id="cc40b-170">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="cc40b-171">It informs the health store when the application has been deleted, so that it can be removed from store.</span><span class="sxs-lookup"><span data-stu-id="cc40b-171">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="cc40b-172">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="cc40b-172">**SourceId**: System.CM</span></span>
* <span data-ttu-id="cc40b-173">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-173">**Property**: State</span></span>
* <span data-ttu-id="cc40b-174">**Next steps**: If the application has been created, it should include the Cluster Manager health report.</span><span class="sxs-lookup"><span data-stu-id="cc40b-174">**Next steps**: If the application has been created, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="cc40b-175">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet \*\*Get-ServiceFabricApplication -ApplicationName \*applicationName\*\*\*).</span><span class="sxs-lookup"><span data-stu-id="cc40b-175">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet \*\*Get-ServiceFabricApplication -ApplicationName \*applicationName\*\*\*).</span></span>

<span data-ttu-id="cc40b-176">The following example shows the state event on the **fabric:/WordCount** application:</span><span class="sxs-lookup"><span data-stu-id="cc40b-176">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 82
                                  SentAt                : 4/24/2015 6:12:51 PM
                                  ReceivedAt            : 4/24/2015 6:12:51 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : ->Ok = 4/24/2015 6:12:51 PM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="cc40b-177">Service system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-177">Service system health reports</span></span>
<span data-ttu-id="cc40b-178">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span><span class="sxs-lookup"><span data-stu-id="cc40b-178">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="cc40b-179">State</span><span class="sxs-lookup"><span data-stu-id="cc40b-179">State</span></span>
<span data-ttu-id="cc40b-180">System.FM reports as OK when the service has been created.</span><span class="sxs-lookup"><span data-stu-id="cc40b-180">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="cc40b-181">It deletes the entity from the health store when the service has been deleted.</span><span class="sxs-lookup"><span data-stu-id="cc40b-181">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="cc40b-182">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="cc40b-182">**SourceId**: System.FM</span></span>
* <span data-ttu-id="cc40b-183">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-183">**Property**: State</span></span>

<span data-ttu-id="cc40b-184">The following example shows the state event on the service **fabric:/WordCount/WordCountService**:</span><span class="sxs-lookup"><span data-stu-id="cc40b-184">The following example shows the state event on the service **fabric:/WordCount/WordCountService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountService

ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Ok
PartitionHealthStates :
                        PartitionId           : 875a1caa-d79f-43bd-ac9d-43ee89a9891c
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 4/24/2015 6:12:51 PM
                        ReceivedAt            : 4/24/2015 6:13:01 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:13:01 PM
```

### <a name="unplaced-replicas-violation"></a><span data-ttu-id="cc40b-185">Unplaced replicas violation</span><span class="sxs-lookup"><span data-stu-id="cc40b-185">Unplaced replicas violation</span></span>
<span data-ttu-id="cc40b-186">**System.PLB** reports a warning if it cannot find a placement for one or more service replicas.</span><span class="sxs-lookup"><span data-stu-id="cc40b-186">**System.PLB** reports a warning if it cannot find a placement for one or more service replicas.</span></span> <span data-ttu-id="cc40b-187">The report is removed when it expires.</span><span class="sxs-lookup"><span data-stu-id="cc40b-187">The report is removed when it expires.</span></span>

* <span data-ttu-id="cc40b-188">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="cc40b-188">**SourceId**: System.FM</span></span>
* <span data-ttu-id="cc40b-189">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-189">**Property**: State</span></span>
* <span data-ttu-id="cc40b-190">**Next steps**: Check the service constraints and the current state of the placement.</span><span class="sxs-lookup"><span data-stu-id="cc40b-190">**Next steps**: Check the service constraints and the current state of the placement.</span></span>

<span data-ttu-id="cc40b-191">The following example shows a violation for a service configured with 7 target replicas in a cluster with 5 nodes:</span><span class="sxs-lookup"><span data-stu-id="cc40b-191">The following example shows a violation for a service configured with 7 target replicas in a cluster with 5 nodes:</span></span>

```xml
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountService


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
                        SequenceNumber        : 131032232425505477
                        SentAt                : 3/23/2016 4:14:02 PM
                        ReceivedAt            : 3/23/2016 4:14:03 PM
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
                        Transitions           : Error->Warning = 3/22/2016 7:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="partition-system-health-reports"></a><span data-ttu-id="cc40b-192">Partition system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-192">Partition system health reports</span></span>
<span data-ttu-id="cc40b-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span><span class="sxs-lookup"><span data-stu-id="cc40b-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="cc40b-194">State</span><span class="sxs-lookup"><span data-stu-id="cc40b-194">State</span></span>
<span data-ttu-id="cc40b-195">System.FM reports as OK when the partition has been created and is healthy.</span><span class="sxs-lookup"><span data-stu-id="cc40b-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="cc40b-196">It deletes the entity from the health store when the partition is deleted.</span><span class="sxs-lookup"><span data-stu-id="cc40b-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="cc40b-197">If the partition is below the minimum replica count, it reports an error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="cc40b-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span><span class="sxs-lookup"><span data-stu-id="cc40b-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="cc40b-199">If the partition is in quorum loss, System.FM reports an error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="cc40b-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span><span class="sxs-lookup"><span data-stu-id="cc40b-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="cc40b-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span><span class="sxs-lookup"><span data-stu-id="cc40b-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="cc40b-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span><span class="sxs-lookup"><span data-stu-id="cc40b-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="cc40b-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="cc40b-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="cc40b-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-204">**Property**: State</span></span>
* <span data-ttu-id="cc40b-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span><span class="sxs-lookup"><span data-stu-id="cc40b-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="cc40b-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span><span class="sxs-lookup"><span data-stu-id="cc40b-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="cc40b-207">The following example shows a healthy partition:</span><span class="sxs-lookup"><span data-stu-id="cc40b-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/StatelessPiApplication/StatelessPiService | Get-ServiceFabricPartitionHealth
PartitionId           : 29da484c-2c08-40c5-b5d9-03774af9a9bf
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 38
                        SentAt                : 4/24/2015 6:33:10 PM
                        ReceivedAt            : 4/24/2015 6:33:31 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:33:31 PM
```

<span data-ttu-id="cc40b-208">The following example shows the health of a partition that is below target replica count.</span><span class="sxs-lookup"><span data-stu-id="cc40b-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="cc40b-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is two and **TargetReplicaSetSize** is seven.</span><span class="sxs-lookup"><span data-stu-id="cc40b-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is two and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="cc40b-210">Then get the number of nodes in the cluster: five.</span><span class="sxs-lookup"><span data-stu-id="cc40b-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="cc40b-211">So in this case, two replicas can't be placed.</span><span class="sxs-lookup"><span data-stu-id="cc40b-211">So in this case, two replicas can't be placed.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : 875a1caa-d79f-43bd-ac9d-43ee89a9891c
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   : None
HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 37
                        SentAt                : 4/24/2015 6:13:12 PM
                        ReceivedAt            : 4/24/2015 6:13:31 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 4/24/2015 6:13:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService

PartitionId            : 875a1caa-d79f-43bd-ac9d-43ee89a9891c
PartitionKind          : Int64Range
PartitionLowKey        : 1
PartitionHighKey       : 26
PartitionStatus        : Ready
LastQuorumLossDuration : 00:00:00
MinReplicaSetSize      : 2
TargetReplicaSetSize   : 7
HealthState            : Warning
DataLossNumber         : 130743727710830900
ConfigurationNumber    : 8589934592


PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="cc40b-212">Replica constraint violation</span><span class="sxs-lookup"><span data-stu-id="cc40b-212">Replica constraint violation</span></span>
<span data-ttu-id="cc40b-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place replicas of the partition.</span><span class="sxs-lookup"><span data-stu-id="cc40b-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place replicas of the partition.</span></span>

* <span data-ttu-id="cc40b-214">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="cc40b-214">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="cc40b-215">**Property**: Starts with **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="cc40b-215">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="cc40b-216">Replica system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-216">Replica system health reports</span></span>
<span data-ttu-id="cc40b-217">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span><span class="sxs-lookup"><span data-stu-id="cc40b-217">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="cc40b-218">State</span><span class="sxs-lookup"><span data-stu-id="cc40b-218">State</span></span>
<span data-ttu-id="cc40b-219">**System.RA** reports as OK when the replica has been created.</span><span class="sxs-lookup"><span data-stu-id="cc40b-219">**System.RA** reports as OK when the replica has been created.</span></span>

* <span data-ttu-id="cc40b-220">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="cc40b-220">**SourceId**: System.RA</span></span>
* <span data-ttu-id="cc40b-221">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="cc40b-221">**Property**: State</span></span>

<span data-ttu-id="cc40b-222">The following example shows a healthy replica:</span><span class="sxs-lookup"><span data-stu-id="cc40b-222">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth
PartitionId           : 875a1caa-d79f-43bd-ac9d-43ee89a9891c
ReplicaId             : 130743727717237310
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743727718018580
                        SentAt                : 4/24/2015 6:12:51 PM
                        ReceivedAt            : 4/24/2015 6:13:02 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:13:02 PM
```

### <a name="replica-open-status"></a><span data-ttu-id="cc40b-223">Replica open status</span><span class="sxs-lookup"><span data-stu-id="cc40b-223">Replica open status</span></span>
<span data-ttu-id="cc40b-224">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span><span class="sxs-lookup"><span data-stu-id="cc40b-224">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="cc40b-225">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span><span class="sxs-lookup"><span data-stu-id="cc40b-225">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="cc40b-226">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span><span class="sxs-lookup"><span data-stu-id="cc40b-226">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="cc40b-227">The time measured includes the time taken for the replicator open and the service open.</span><span class="sxs-lookup"><span data-stu-id="cc40b-227">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="cc40b-228">The property changes to OK if the open completes.</span><span class="sxs-lookup"><span data-stu-id="cc40b-228">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="cc40b-229">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="cc40b-229">**SourceId**: System.RA</span></span>
* <span data-ttu-id="cc40b-230">**Property**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="cc40b-230">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="cc40b-231">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span><span class="sxs-lookup"><span data-stu-id="cc40b-231">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="cc40b-232">Slow service API call</span><span class="sxs-lookup"><span data-stu-id="cc40b-232">Slow service API call</span></span>
<span data-ttu-id="cc40b-233">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span><span class="sxs-lookup"><span data-stu-id="cc40b-233">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="cc40b-234">The warning is cleared when the call completes.</span><span class="sxs-lookup"><span data-stu-id="cc40b-234">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="cc40b-235">**SourceId**: System.RAP or System.Replicator</span><span class="sxs-lookup"><span data-stu-id="cc40b-235">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="cc40b-236">**Property**: The name of the slow API.</span><span class="sxs-lookup"><span data-stu-id="cc40b-236">**Property**: The name of the slow API.</span></span> <span data-ttu-id="cc40b-237">The description provides more details about the time the API has been pending.</span><span class="sxs-lookup"><span data-stu-id="cc40b-237">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="cc40b-238">**Next steps**: Investigate why the call takes longer than expected.</span><span class="sxs-lookup"><span data-stu-id="cc40b-238">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="cc40b-239">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span><span class="sxs-lookup"><span data-stu-id="cc40b-239">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="cc40b-240">One of the replicas has a warning health state, so you get its health.</span><span class="sxs-lookup"><span data-stu-id="cc40b-240">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="cc40b-241">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span><span class="sxs-lookup"><span data-stu-id="cc40b-241">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="cc40b-242">After this information is received, the next step is to look at the service code and investigate there.</span><span class="sxs-lookup"><span data-stu-id="cc40b-242">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="cc40b-243">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span><span class="sxs-lookup"><span data-stu-id="cc40b-243">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="cc40b-244">The replicas are recycling, so you may not see any replicas in the warning state.</span><span class="sxs-lookup"><span data-stu-id="cc40b-244">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="cc40b-245">You can retry getting the health state and look for any differences in the replica ID.</span><span class="sxs-lookup"><span data-stu-id="cc40b-245">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="cc40b-246">In certain cases, the retries can give you clues.</span><span class="sxs-lookup"><span data-stu-id="cc40b-246">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 2
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="cc40b-247">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span><span class="sxs-lookup"><span data-stu-id="cc40b-247">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Visual Studio 2015 diagnostic events: RunAsync failure in fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="cc40b-249">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="cc40b-249">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="cc40b-250">Replication queue full</span><span class="sxs-lookup"><span data-stu-id="cc40b-250">Replication queue full</span></span>
<span data-ttu-id="cc40b-251">**System.Replicator** reports a warning if the replication queue is full.</span><span class="sxs-lookup"><span data-stu-id="cc40b-251">**System.Replicator** reports a warning if the replication queue is full.</span></span> <span data-ttu-id="cc40b-252">On the primary, this usually happens because one or more secondary replicas are slow to acknowledge operations.</span><span class="sxs-lookup"><span data-stu-id="cc40b-252">On the primary, this usually happens because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="cc40b-253">On the secondary, this usually happens when the service is slow to apply the operations.</span><span class="sxs-lookup"><span data-stu-id="cc40b-253">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="cc40b-254">The warning is cleared when the queue is no longer full.</span><span class="sxs-lookup"><span data-stu-id="cc40b-254">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="cc40b-255">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="cc40b-255">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="cc40b-256">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span><span class="sxs-lookup"><span data-stu-id="cc40b-256">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="cc40b-257">Slow Naming operations</span><span class="sxs-lookup"><span data-stu-id="cc40b-257">Slow Naming operations</span></span>
<span data-ttu-id="cc40b-258">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span><span class="sxs-lookup"><span data-stu-id="cc40b-258">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="cc40b-259">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="cc40b-259">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="cc40b-260">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="cc40b-260">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="cc40b-261">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span><span class="sxs-lookup"><span data-stu-id="cc40b-261">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="cc40b-262">It is a Service Fabric partitioned persisted service.</span><span class="sxs-lookup"><span data-stu-id="cc40b-262">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="cc40b-263">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span><span class="sxs-lookup"><span data-stu-id="cc40b-263">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="cc40b-264">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span><span class="sxs-lookup"><span data-stu-id="cc40b-264">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="cc40b-265">Read more about [Naming service](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="cc40b-265">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="cc40b-266">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span><span class="sxs-lookup"><span data-stu-id="cc40b-266">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="cc40b-267">If the operation completes successfully, the Warning is cleared.</span><span class="sxs-lookup"><span data-stu-id="cc40b-267">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="cc40b-268">If the operation completes with an error, the health report includes details about the error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-268">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="cc40b-269">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="cc40b-269">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="cc40b-270">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span><span class="sxs-lookup"><span data-stu-id="cc40b-270">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="cc40b-271">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="cc40b-271">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="cc40b-272">AO points to the role of the Naming partition for this name and operation.</span><span class="sxs-lookup"><span data-stu-id="cc40b-272">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="cc40b-273">**Next steps**: Check why the Naming operation fails.</span><span class="sxs-lookup"><span data-stu-id="cc40b-273">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="cc40b-274">Each operation can have different root causes.</span><span class="sxs-lookup"><span data-stu-id="cc40b-274">Each operation can have different root causes.</span></span> <span data-ttu-id="cc40b-275">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span><span class="sxs-lookup"><span data-stu-id="cc40b-275">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="cc40b-276">The following example shows a create service operation.</span><span class="sxs-lookup"><span data-stu-id="cc40b-276">The following example shows a create service operation.</span></span> <span data-ttu-id="cc40b-277">The operation took longer than the configured duration.</span><span class="sxs-lookup"><span data-stu-id="cc40b-277">The operation took longer than the configured duration.</span></span> <span data-ttu-id="cc40b-278">AO retries and sends work to NO.</span><span class="sxs-lookup"><span data-stu-id="cc40b-278">AO retries and sends work to NO.</span></span> <span data-ttu-id="cc40b-279">NO completed the last operation with Timeout.</span><span class="sxs-lookup"><span data-stu-id="cc40b-279">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="cc40b-280">In this case, the same replica is primary for both the AO and NO roles.</span><span class="sxs-lookup"><span data-stu-id="cc40b-280">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="cc40b-281">DeployedApplication system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-281">DeployedApplication system health reports</span></span>
<span data-ttu-id="cc40b-282">**System.Hosting** is the authority on deployed entities.</span><span class="sxs-lookup"><span data-stu-id="cc40b-282">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="cc40b-283">Activation</span><span class="sxs-lookup"><span data-stu-id="cc40b-283">Activation</span></span>
<span data-ttu-id="cc40b-284">System.Hosting reports as OK when an application has been successfully activated on the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-284">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="cc40b-285">Otherwise, it reports an error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-285">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="cc40b-286">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-286">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-287">**Property**: Activation, including the rollout version</span><span class="sxs-lookup"><span data-stu-id="cc40b-287">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="cc40b-288">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span><span class="sxs-lookup"><span data-stu-id="cc40b-288">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="cc40b-289">The following example shows successful activation:</span><span class="sxs-lookup"><span data-stu-id="cc40b-289">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName Node.1 -ApplicationName fabric:/WordCount

ApplicationName                    : fabric:/WordCount
NodeName                           : Node.1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates :
                                     ServiceManifestName   : WordCountServicePkg
                                     NodeName              : Node.1
                                     AggregatedHealthState : Ok

HealthEvents                       :
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 130743727751144415
                                     SentAt                : 4/24/2015 6:12:55 PM
                                     ReceivedAt            : 4/24/2015 6:13:03 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : ->Ok = 4/24/2015 6:13:03 PM
```

### <a name="download"></a><span data-ttu-id="cc40b-290">Download</span><span class="sxs-lookup"><span data-stu-id="cc40b-290">Download</span></span>
<span data-ttu-id="cc40b-291">**System.Hosting** reports an error if the application package download fails.</span><span class="sxs-lookup"><span data-stu-id="cc40b-291">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="cc40b-292">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-292">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-293">**Property**: **Download:\*RolloutVersion**\*</span><span class="sxs-lookup"><span data-stu-id="cc40b-293">**Property**: **Download:\*RolloutVersion**\*</span></span>
* <span data-ttu-id="cc40b-294">**Next steps**: Investigate why the download failed on the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-294">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="cc40b-295">DeployedServicePackage system health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-295">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="cc40b-296">**System.Hosting** is the authority on deployed entities.</span><span class="sxs-lookup"><span data-stu-id="cc40b-296">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="cc40b-297">Service package activation</span><span class="sxs-lookup"><span data-stu-id="cc40b-297">Service package activation</span></span>
<span data-ttu-id="cc40b-298">System.Hosting reports as OK if the service package activation on the node is successful.</span><span class="sxs-lookup"><span data-stu-id="cc40b-298">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="cc40b-299">Otherwise, it reports an error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-299">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="cc40b-300">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-300">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-301">**Property**: Activation</span><span class="sxs-lookup"><span data-stu-id="cc40b-301">**Property**: Activation</span></span>
* <span data-ttu-id="cc40b-302">**Next steps**: Investigate why the activation failed.</span><span class="sxs-lookup"><span data-stu-id="cc40b-302">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="cc40b-303">Code package activation</span><span class="sxs-lookup"><span data-stu-id="cc40b-303">Code package activation</span></span>
<span data-ttu-id="cc40b-304">**System.Hosting** reports as OK for each code package if the activation is successful.</span><span class="sxs-lookup"><span data-stu-id="cc40b-304">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="cc40b-305">If the activation fails, it reports a warning as configured.</span><span class="sxs-lookup"><span data-stu-id="cc40b-305">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="cc40b-306">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span><span class="sxs-lookup"><span data-stu-id="cc40b-306">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="cc40b-307">If a service package contains multiple code packages, an activation report is generated for each one.</span><span class="sxs-lookup"><span data-stu-id="cc40b-307">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="cc40b-308">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-308">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-309">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:\*SetupEntryPoint/EntryPoint**\* (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="cc40b-309">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:\*SetupEntryPoint/EntryPoint**\* (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="cc40b-310">Service type registration</span><span class="sxs-lookup"><span data-stu-id="cc40b-310">Service type registration</span></span>
<span data-ttu-id="cc40b-311">**System.Hosting** reports as OK if the service type has been registered successfully.</span><span class="sxs-lookup"><span data-stu-id="cc40b-311">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="cc40b-312">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="cc40b-312">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="cc40b-313">If the service type is unregistered from the node, this is because the run time has been closed.</span><span class="sxs-lookup"><span data-stu-id="cc40b-313">If the service type is unregistered from the node, this is because the run time has been closed.</span></span> <span data-ttu-id="cc40b-314">Hosting reports a warning.</span><span class="sxs-lookup"><span data-stu-id="cc40b-314">Hosting reports a warning.</span></span>

* <span data-ttu-id="cc40b-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="cc40b-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="cc40b-317">The following example shows a healthy deployed service package:</span><span class="sxs-lookup"><span data-stu-id="cc40b-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName Node.1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName       : fabric:/WordCount
ServiceManifestName   : WordCountServicePkg
NodeName              : Node.1
AggregatedHealthState : Ok
HealthEvents          :
                        SourceId              : System.Hosting
                        Property              : Activation
                        HealthState           : Ok
                        SequenceNumber        : 130743727751456915
                        SentAt                : 4/24/2015 6:12:55 PM
                        ReceivedAt            : 4/24/2015 6:13:03 PM
                        TTL                   : Infinite
                        Description           : The ServicePackage was activated successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:13:03 PM

                        SourceId              : System.Hosting
                        Property              : CodePackageActivation:Code:EntryPoint
                        HealthState           : Ok
                        SequenceNumber        : 130743727751613185
                        SentAt                : 4/24/2015 6:12:55 PM
                        ReceivedAt            : 4/24/2015 6:13:03 PM
                        TTL                   : Infinite
                        Description           : The CodePackage was activated successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:13:03 PM

                        SourceId              : System.Hosting
                        Property              : ServiceTypeRegistration:WordCountServiceType
                        HealthState           : Ok
                        SequenceNumber        : 130743727753644473
                        SentAt                : 4/24/2015 6:12:55 PM
                        ReceivedAt            : 4/24/2015 6:13:03 PM
                        TTL                   : Infinite
                        Description           : The ServiceType was registered successfully.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 6:13:03 PM
```

### <a name="download"></a><span data-ttu-id="cc40b-318">Download</span><span class="sxs-lookup"><span data-stu-id="cc40b-318">Download</span></span>
<span data-ttu-id="cc40b-319">**System.Hosting** reports an error if the service package download fails.</span><span class="sxs-lookup"><span data-stu-id="cc40b-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="cc40b-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-321">**Property**: **Download:\*RolloutVersion**\*</span><span class="sxs-lookup"><span data-stu-id="cc40b-321">**Property**: **Download:\*RolloutVersion**\*</span></span>
* <span data-ttu-id="cc40b-322">**Next steps**: Investigate why the download failed on the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="cc40b-323">Upgrade validation</span><span class="sxs-lookup"><span data-stu-id="cc40b-323">Upgrade validation</span></span>
<span data-ttu-id="cc40b-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span><span class="sxs-lookup"><span data-stu-id="cc40b-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="cc40b-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="cc40b-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="cc40b-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span><span class="sxs-lookup"><span data-stu-id="cc40b-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="cc40b-327">**Description**: Points to the error encountered</span><span class="sxs-lookup"><span data-stu-id="cc40b-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc40b-328">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc40b-328">Next steps</span></span>
[<span data-ttu-id="cc40b-329">View Service Fabric health reports</span><span class="sxs-lookup"><span data-stu-id="cc40b-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="cc40b-330">How to report and check service health</span><span class="sxs-lookup"><span data-stu-id="cc40b-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="cc40b-331">Monitor and diagnose services locally</span><span class="sxs-lookup"><span data-stu-id="cc40b-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="cc40b-332">Service Fabric application upgrade</span><span class="sxs-lookup"><span data-stu-id="cc40b-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)


