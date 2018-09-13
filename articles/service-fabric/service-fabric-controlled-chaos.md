---
title: Induce Chaos in Service Fabric clusters | Microsoft Docs
description: Using Fault Injection and Cluster Analysis Service APIs to manage Chaos in the cluster.
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/05/2018
ms.author: motanv
ms.openlocfilehash: dc846bbd3c140c54221af04c931495c3fe97a674
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830440"
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="7e561-103">Induce controlled Chaos in Service Fabric clusters</span><span class="sxs-lookup"><span data-stu-id="7e561-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="7e561-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span><span class="sxs-lookup"><span data-stu-id="7e561-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="7e561-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span><span class="sxs-lookup"><span data-stu-id="7e561-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="7e561-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span><span class="sxs-lookup"><span data-stu-id="7e561-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="7e561-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span><span class="sxs-lookup"><span data-stu-id="7e561-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="7e561-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span><span class="sxs-lookup"><span data-stu-id="7e561-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="7e561-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span><span class="sxs-lookup"><span data-stu-id="7e561-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="7e561-110">For an unbiased testing, you can use Chaos.</span><span class="sxs-lookup"><span data-stu-id="7e561-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="7e561-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="7e561-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="7e561-112">A graceful fault consists of a set of Service Fabric API calls, for example, restart replica fault is a graceful fault because this is a close followed by an open on a replica.</span><span class="sxs-lookup"><span data-stu-id="7e561-112">A graceful fault consists of a set of Service Fabric API calls, for example, restart replica fault is a graceful fault because this is a close followed by an open on a replica.</span></span> <span data-ttu-id="7e561-113">Remove replica, move primary replica, and move secondary replica are the other graceful faults exercised by Chaos.</span><span class="sxs-lookup"><span data-stu-id="7e561-113">Remove replica, move primary replica, and move secondary replica are the other graceful faults exercised by Chaos.</span></span> <span data-ttu-id="7e561-114">Ungraceful faults are process exits, like restart node and restart code package.</span><span class="sxs-lookup"><span data-stu-id="7e561-114">Ungraceful faults are process exits, like restart node and restart code package.</span></span> 

<span data-ttu-id="7e561-115">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C#, Powershell, or REST API to start generating faults in the cluster and in your services.</span><span class="sxs-lookup"><span data-stu-id="7e561-115">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C#, Powershell, or REST API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="7e561-116">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C#, Powershell, or REST) to stop it at any time.</span><span class="sxs-lookup"><span data-stu-id="7e561-116">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C#, Powershell, or REST) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="7e561-117">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span><span class="sxs-lookup"><span data-stu-id="7e561-117">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="7e561-118">While Chaos is running, it produces different events that capture the state of the run at the moment.</span><span class="sxs-lookup"><span data-stu-id="7e561-118">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="7e561-119">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span><span class="sxs-lookup"><span data-stu-id="7e561-119">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="7e561-120">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span><span class="sxs-lookup"><span data-stu-id="7e561-120">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="7e561-121">You can invoke the GetChaosReport API (C#, Powershell, or REST) to get the report of Chaos runs.</span><span class="sxs-lookup"><span data-stu-id="7e561-121">You can invoke the GetChaosReport API (C#, Powershell, or REST) to get the report of Chaos runs.</span></span> <span data-ttu-id="7e561-122">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span><span class="sxs-lookup"><span data-stu-id="7e561-122">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="7e561-123">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span><span class="sxs-lookup"><span data-stu-id="7e561-123">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="7e561-124">Faults induced in Chaos</span><span class="sxs-lookup"><span data-stu-id="7e561-124">Faults induced in Chaos</span></span>
<span data-ttu-id="7e561-125">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span><span class="sxs-lookup"><span data-stu-id="7e561-125">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="7e561-126">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span><span class="sxs-lookup"><span data-stu-id="7e561-126">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="7e561-127">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span><span class="sxs-lookup"><span data-stu-id="7e561-127">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="7e561-128">Chaos induces faults from the following categories:</span><span class="sxs-lookup"><span data-stu-id="7e561-128">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="7e561-129">Restart a node</span><span class="sxs-lookup"><span data-stu-id="7e561-129">Restart a node</span></span>
* <span data-ttu-id="7e561-130">Restart a deployed code package</span><span class="sxs-lookup"><span data-stu-id="7e561-130">Restart a deployed code package</span></span>
* <span data-ttu-id="7e561-131">Remove a replica</span><span class="sxs-lookup"><span data-stu-id="7e561-131">Remove a replica</span></span>
* <span data-ttu-id="7e561-132">Restart a replica</span><span class="sxs-lookup"><span data-stu-id="7e561-132">Restart a replica</span></span>
* <span data-ttu-id="7e561-133">Move a primary replica (configurable)</span><span class="sxs-lookup"><span data-stu-id="7e561-133">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="7e561-134">Move a secondary replica (configurable)</span><span class="sxs-lookup"><span data-stu-id="7e561-134">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="7e561-135">Chaos runs in multiple iterations.</span><span class="sxs-lookup"><span data-stu-id="7e561-135">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="7e561-136">Each iteration consists of faults and cluster validation for the specified period.</span><span class="sxs-lookup"><span data-stu-id="7e561-136">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="7e561-137">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="7e561-137">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="7e561-138">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span><span class="sxs-lookup"><span data-stu-id="7e561-138">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="7e561-139">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span><span class="sxs-lookup"><span data-stu-id="7e561-139">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="7e561-140">Chaos induces three faults, and then validates the cluster health.</span><span class="sxs-lookup"><span data-stu-id="7e561-140">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="7e561-141">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span><span class="sxs-lookup"><span data-stu-id="7e561-141">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="7e561-142">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize or it does not become healthy within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="7e561-142">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize or it does not become healthy within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="7e561-143">This event indicates that something has gone wrong and might need further investigation.</span><span class="sxs-lookup"><span data-stu-id="7e561-143">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="7e561-144">To get which faults Chaos induced, you can use GetChaosReport API (powershell, C#, or REST).</span><span class="sxs-lookup"><span data-stu-id="7e561-144">To get which faults Chaos induced, you can use GetChaosReport API (powershell, C#, or REST).</span></span> <span data-ttu-id="7e561-145">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span><span class="sxs-lookup"><span data-stu-id="7e561-145">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="7e561-146">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span><span class="sxs-lookup"><span data-stu-id="7e561-146">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="7e561-147">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span><span class="sxs-lookup"><span data-stu-id="7e561-147">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="7e561-148">Important configuration options</span><span class="sxs-lookup"><span data-stu-id="7e561-148">Important configuration options</span></span>
* <span data-ttu-id="7e561-149">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span><span class="sxs-lookup"><span data-stu-id="7e561-149">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="7e561-150">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="7e561-150">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="7e561-151">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="7e561-151">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="7e561-152">This wait is to reduce the load on the cluster while it is recovering.</span><span class="sxs-lookup"><span data-stu-id="7e561-152">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="7e561-153">The checks performed are:</span><span class="sxs-lookup"><span data-stu-id="7e561-153">The checks performed are:</span></span>
  * <span data-ttu-id="7e561-154">If the cluster health is OK</span><span class="sxs-lookup"><span data-stu-id="7e561-154">If the cluster health is OK</span></span>
  * <span data-ttu-id="7e561-155">If the service health is OK</span><span class="sxs-lookup"><span data-stu-id="7e561-155">If the service health is OK</span></span>
  * <span data-ttu-id="7e561-156">If the target replica set size is achieved for the service partition</span><span class="sxs-lookup"><span data-stu-id="7e561-156">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="7e561-157">That no InBuild replicas exist</span><span class="sxs-lookup"><span data-stu-id="7e561-157">That no InBuild replicas exist</span></span>
* <span data-ttu-id="7e561-158">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span><span class="sxs-lookup"><span data-stu-id="7e561-158">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="7e561-159">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span><span class="sxs-lookup"><span data-stu-id="7e561-159">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="7e561-160">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span><span class="sxs-lookup"><span data-stu-id="7e561-160">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="7e561-161">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span><span class="sxs-lookup"><span data-stu-id="7e561-161">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="7e561-162">These faults are enabled by default.</span><span class="sxs-lookup"><span data-stu-id="7e561-162">These faults are enabled by default.</span></span>
* <span data-ttu-id="7e561-163">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span><span class="sxs-lookup"><span data-stu-id="7e561-163">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="7e561-164">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span><span class="sxs-lookup"><span data-stu-id="7e561-164">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="7e561-165">The higher the value, the lower is the average fault injection rate.</span><span class="sxs-lookup"><span data-stu-id="7e561-165">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="7e561-166">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span><span class="sxs-lookup"><span data-stu-id="7e561-166">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="7e561-167">The higher the value, the lower the concurrency of (or the overlap between) faults.</span><span class="sxs-lookup"><span data-stu-id="7e561-167">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="7e561-168">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span><span class="sxs-lookup"><span data-stu-id="7e561-168">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="7e561-169">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span><span class="sxs-lookup"><span data-stu-id="7e561-169">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="7e561-170">**Context**: A collection of (string, string) type key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="7e561-170">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="7e561-171">The map can be used to record information about the Chaos run.</span><span class="sxs-lookup"><span data-stu-id="7e561-171">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="7e561-172">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span><span class="sxs-lookup"><span data-stu-id="7e561-172">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="7e561-173">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span><span class="sxs-lookup"><span data-stu-id="7e561-173">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>
* <span data-ttu-id="7e561-174">**ChaosTargetFilter**: This filter can be used to target Chaos faults only to certain node types or only to certain application instances.</span><span class="sxs-lookup"><span data-stu-id="7e561-174">**ChaosTargetFilter**: This filter can be used to target Chaos faults only to certain node types or only to certain application instances.</span></span> <span data-ttu-id="7e561-175">If ChaosTargetFilter is not used, Chaos faults all cluster entities.</span><span class="sxs-lookup"><span data-stu-id="7e561-175">If ChaosTargetFilter is not used, Chaos faults all cluster entities.</span></span> <span data-ttu-id="7e561-176">If ChaosTargetFilter is used, Chaos faults only the entities that meet the ChaosTargetFilter specification.</span><span class="sxs-lookup"><span data-stu-id="7e561-176">If ChaosTargetFilter is used, Chaos faults only the entities that meet the ChaosTargetFilter specification.</span></span> <span data-ttu-id="7e561-177">NodeTypeInclusionList and ApplicationInclusionList allow union semantics only.</span><span class="sxs-lookup"><span data-stu-id="7e561-177">NodeTypeInclusionList and ApplicationInclusionList allow union semantics only.</span></span> <span data-ttu-id="7e561-178">In other words, it is not possible to specify an intersection of NodeTypeInclusionList and ApplicationInclusionList.</span><span class="sxs-lookup"><span data-stu-id="7e561-178">In other words, it is not possible to specify an intersection of NodeTypeInclusionList and ApplicationInclusionList.</span></span> <span data-ttu-id="7e561-179">For example, it is not possible to specify "fault this application only when it is on that node type."</span><span class="sxs-lookup"><span data-stu-id="7e561-179">For example, it is not possible to specify "fault this application only when it is on that node type."</span></span> <span data-ttu-id="7e561-180">Once an entity is included in either NodeTypeInclusionList or ApplicationInclusionList, that entity cannot be excluded using ChaosTargetFilter.</span><span class="sxs-lookup"><span data-stu-id="7e561-180">Once an entity is included in either NodeTypeInclusionList or ApplicationInclusionList, that entity cannot be excluded using ChaosTargetFilter.</span></span> <span data-ttu-id="7e561-181">Even if applicationX does not appear in ApplicationInclusionList, in some Chaos iteration applicationX can be faulted because it happens to be on a node of nodeTypeY that is included in NodeTypeInclusionList.</span><span class="sxs-lookup"><span data-stu-id="7e561-181">Even if applicationX does not appear in ApplicationInclusionList, in some Chaos iteration applicationX can be faulted because it happens to be on a node of nodeTypeY that is included in NodeTypeInclusionList.</span></span> <span data-ttu-id="7e561-182">If both NodeTypeInclusionList and ApplicationInclusionList are null or empty, an ArgumentException is thrown.</span><span class="sxs-lookup"><span data-stu-id="7e561-182">If both NodeTypeInclusionList and ApplicationInclusionList are null or empty, an ArgumentException is thrown.</span></span>
    * <span data-ttu-id="7e561-183">**NodeTypeInclusionList**: A list of node types to include in Chaos faults.</span><span class="sxs-lookup"><span data-stu-id="7e561-183">**NodeTypeInclusionList**: A list of node types to include in Chaos faults.</span></span> <span data-ttu-id="7e561-184">All types of faults (restart node, restart codepackage, remove replica, restart replica, move primary, and move secondary) are enabled for the nodes of these node types.</span><span class="sxs-lookup"><span data-stu-id="7e561-184">All types of faults (restart node, restart codepackage, remove replica, restart replica, move primary, and move secondary) are enabled for the nodes of these node types.</span></span> <span data-ttu-id="7e561-185">If a nodetype (say NodeTypeX) does not appear in the NodeTypeInclusionList, then node level faults (like NodeRestart) will never be enabled for the nodes of NodeTypeX, but code package and replica faults can still be enabled for NodeTypeX if an application in the ApplicationInclusionList happens to reside on a node of NodeTypeX.</span><span class="sxs-lookup"><span data-stu-id="7e561-185">If a nodetype (say NodeTypeX) does not appear in the NodeTypeInclusionList, then node level faults (like NodeRestart) will never be enabled for the nodes of NodeTypeX, but code package and replica faults can still be enabled for NodeTypeX if an application in the ApplicationInclusionList happens to reside on a node of NodeTypeX.</span></span> <span data-ttu-id="7e561-186">At most 100 node type names can be included in this list, to increase this number, a config upgrade is required for MaxNumberOfNodeTypesInChaosTargetFilter configuration.</span><span class="sxs-lookup"><span data-stu-id="7e561-186">At most 100 node type names can be included in this list, to increase this number, a config upgrade is required for MaxNumberOfNodeTypesInChaosTargetFilter configuration.</span></span>
    * <span data-ttu-id="7e561-187">**ApplicationInclusionList**: A list of application URIs to include in Chaos faults.</span><span class="sxs-lookup"><span data-stu-id="7e561-187">**ApplicationInclusionList**: A list of application URIs to include in Chaos faults.</span></span> <span data-ttu-id="7e561-188">All replicas belonging to services of these applications are amenable to replica faults (restart replica, remove replica, move primary, and move secondary) by Chaos.</span><span class="sxs-lookup"><span data-stu-id="7e561-188">All replicas belonging to services of these applications are amenable to replica faults (restart replica, remove replica, move primary, and move secondary) by Chaos.</span></span> <span data-ttu-id="7e561-189">Chaos may restart a code package only if the code package hosts replicas of these applications only.</span><span class="sxs-lookup"><span data-stu-id="7e561-189">Chaos may restart a code package only if the code package hosts replicas of these applications only.</span></span> <span data-ttu-id="7e561-190">If an application does not appear in this list, it can still be faulted in some Chaos iteration if the application ends up on a node of a node type that is incuded in NodeTypeInclusionList.</span><span class="sxs-lookup"><span data-stu-id="7e561-190">If an application does not appear in this list, it can still be faulted in some Chaos iteration if the application ends up on a node of a node type that is incuded in NodeTypeInclusionList.</span></span> <span data-ttu-id="7e561-191">However if applicationX is tied to nodeTypeY through placement constraints and applicationX is absent from ApplicationInclusionList and nodeTypeY is absent from NodeTypeInclusionList, then applicationX will never be faulted.</span><span class="sxs-lookup"><span data-stu-id="7e561-191">However if applicationX is tied to nodeTypeY through placement constraints and applicationX is absent from ApplicationInclusionList and nodeTypeY is absent from NodeTypeInclusionList, then applicationX will never be faulted.</span></span> <span data-ttu-id="7e561-192">At most 1000 application names can be included in this list, to increase this number, a config upgrade is required for MaxNumberOfApplicationsInChaosTargetFilter configuration.</span><span class="sxs-lookup"><span data-stu-id="7e561-192">At most 1000 application names can be included in this list, to increase this number, a config upgrade is required for MaxNumberOfApplicationsInChaosTargetFilter configuration.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="7e561-193">How to run Chaos</span><span class="sxs-lookup"><span data-stu-id="7e561-193">How to run Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }
        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;

            // The maximum amount of time to wait for all cluster entities to become stable and healthy. 
            // Chaos executes in iterations and at the start of each iteration it validates the health of cluster entities. 
            // During validation if a cluster entity is not stable and healthy within MaxClusterStabilizationTimeoutInSeconds, Chaos generates a validation failed event.
            var maxClusterStabilizationTimeout = TimeSpan.FromSeconds(30.0);

            var timeToRun = TimeSpan.FromMinutes(60.0);

            // MaxConcurrentFaults is the maximum number of concurrent faults induced per iteration. 
            // Chaos executes in iterations and two consecutive iterations are separated by a validation phase. 
            // The higher the concurrency, the more aggressive the injection of faults -- inducing more complex series of states to uncover bugs. 
            // The recommendation is to start with a value of 2 or 3 and to exercise caution while moving up.
            var maxConcurrentFaults = 3;

            // Describes a map, which is a collection of (string, string) type key-value pairs. The map can be used to record information about
            // the Chaos run. There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.
            // This map is set by the starter of the Chaos run to optionally store the context about the specific run.
            var startContext = new Dictionary<string, string>{{"ReasonForStart", "Testing"}};

            // Time-separation (in seconds) between two consecutive iterations of Chaos. The larger the value, the lower the fault injection rate.
            var waitTimeBetweenIterations = TimeSpan.FromSeconds(10);

            // Wait time (in seconds) between consecutive faults within a single iteration. 
            // The larger the value, the lower the overlapping between faults and the simpler the sequence of state transitions that the cluster goes through. 
            // The recommendation is to start with a value between 1 and 5 and exercise caution while moving up.
            var waitTimeBetweenFaults = TimeSpan.Zero;

            // Passed-in cluster health policy is used to validate health of the cluster in between Chaos iterations. 
            var clusterHealthPolicy = new ClusterHealthPolicy
            {
                ConsiderWarningAsError = false,
                MaxPercentUnhealthyApplications = 100,
                MaxPercentUnhealthyNodes = 100
            };

            // All types of faults, restart node, restart code package, restart replica, move primary replica, and move secondary replica will happen
            // for nodes of type 'FrontEndType'
            var nodetypeInclusionList = new List<string> { "FrontEndType"};

            // In addition to the faults included by nodetypeInclusionList, 
            // restart code package, restart replica, move primary replica, move secondary replica faults will happen for 'fabric:/TestApp2'
            // even if a replica or code package from 'fabric:/TestApp2' is residing on a node which is not of type included in nodeypeInclusionList.
            var applicationInclusionList = new List<string> { "fabric:/TestApp2" };

            // List of cluster entities to target for Chaos faults.
            var chaosTargetFilter = new ChaosTargetFilter
            {
                NodeTypeInclusionList = nodetypeInclusionList,
                ApplicationInclusionList = applicationInclusionList
            };

            var parameters = new ChaosParameters(
                maxClusterStabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun,
                startContext,
                waitTimeBetweenIterations,
                waitTimeBetweenFaults,
                clusterHealthPolicy) {ChaosTargetFilter = chaosTargetFilter};

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            string continuationToken = null;

            while (true)
            {
                ChaosReport report;
                try
                {
                    report = string.IsNullOrEmpty(continuationToken)
                        ? client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult()
                        : client.TestManager.GetChaosReportAsync(continuationToken).GetAwaiter().GetResult();
                }
                catch (Exception e)
                {
                    if (e is FabricTransientException)
                    {
                        Console.WriteLine("A transient exception happened: '{0}'", e);
                    }
                    else if(e is TimeoutException)
                    {
                        Console.WriteLine("A timeout exception happened: '{0}'", e);
                    }
                    else
                    {
                        throw;
                    }

                    Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
                    continue;
                }

                continuationToken = report.ContinuationToken;

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit the loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$clusterConnectionString = "localhost:19000"
$timeToRunMinute = 60

# The maximum amount of time to wait for all cluster entities to become stable and healthy. 
# Chaos executes in iterations and at the start of each iteration it validates the health of cluster entities. 
# During validation if a cluster entity is not stable and healthy within MaxClusterStabilizationTimeoutInSeconds, Chaos generates a validation failed event.
$maxClusterStabilizationTimeSecs = 30

# MaxConcurrentFaults is the maximum number of concurrent faults induced per iteration. 
# Chaos executes in iterations and two consecutive iterations are separated by a validation phase. 
# The higher the concurrency, the more aggressive the injection of faults -- inducing more complex series of states to uncover bugs. 
# The recommendation is to start with a value of 2 or 3 and to exercise caution while moving up.
$maxConcurrentFaults = 3

# Time-separation (in seconds) between two consecutive iterations of Chaos. The larger the value, the lower the fault injection rate.
$waitTimeBetweenIterationsSec = 10

# Wait time (in seconds) between consecutive faults within a single iteration. 
# The larger the value, the lower the overlapping between faults and the simpler the sequence of state transitions that the cluster goes through. 
# The recommendation is to start with a value between 1 and 5 and exercise caution while moving up.
$waitTimeBetweenFaultsSec = 0

# Passed-in cluster health policy is used to validate health of the cluster in between Chaos iterations. 
$clusterHealthPolicy = new-object -TypeName System.Fabric.Health.ClusterHealthPolicy
$clusterHealthPolicy.MaxPercentUnhealthyNodes = 100
$clusterHealthPolicy.MaxPercentUnhealthyApplications = 100
$clusterHealthPolicy.ConsiderWarningAsError = $False

# Describes a map, which is a collection of (string, string) type key-value pairs. The map can be used to record information about
# the Chaos run. There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.
# This map is set by the starter of the Chaos run to optionally store the context about the specific run.
$context = @{"ReasonForStart" = "Testing"}

#List of cluster entities to target for Chaos faults.
$chaosTargetFilter = new-object -TypeName System.Fabric.Chaos.DataStructures.ChaosTargetFilter
$chaosTargetFilter.NodeTypeInclusionList = new-object -TypeName "System.Collections.Generic.List[String]"

# All types of faults, restart node, restart code package, restart replica, move primary replica, and move secondary replica will happen
# for nodes of type 'FrontEndType'
$chaosTargetFilter.NodeTypeInclusionList.AddRange( [string[]]@("FrontEndType") )
$chaosTargetFilter.ApplicationInclusionList = new-object -TypeName "System.Collections.Generic.List[String]"

# In addition to the faults included by nodetypeInclusionList, 
# restart code package, restart replica, move primary replica, move secondary replica faults will happen for 'fabric:/TestApp2'
# even if a replica or code package from 'fabric:/TestApp2' is residing on a node which is not of type included in nodeypeInclusionList.
$chaosTargetFilter.ApplicationInclusionList.Add("fabric:/TestApp2")

Connect-ServiceFabricCluster $clusterConnectionString

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRunMinute -MaxConcurrentFaults $maxConcurrentFaults -MaxClusterStabilizationTimeoutSec $maxClusterStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ClusterHealthPolicy $clusterHealthPolicy -ChaosTargetFilter $chaosTargetFilter

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                Write-Host $e
                # When Chaos stops, a StoppedEvent is created.
                # If a StoppedEvent is found, exit the loop.
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    return
                }
            }
        }
    }

    Start-Sleep -Seconds 1
}
```
