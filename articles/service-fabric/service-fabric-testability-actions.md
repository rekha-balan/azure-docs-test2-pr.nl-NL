---
title: Simulate failures in Azure microservices | Microsoft Docs
description: This article talks about the testability actions found in Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/19/2017
ms.author: motanv;heeldin
ms.openlocfilehash: e3c1091226bdc68e4e5109caa354fff9aaae8169
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556337"
---
# <a name="testability-actions"></a><span data-ttu-id="b58b6-103">Testability actions</span><span class="sxs-lookup"><span data-stu-id="b58b6-103">Testability actions</span></span>
<span data-ttu-id="b58b6-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span><span class="sxs-lookup"><span data-stu-id="b58b6-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="b58b6-105">These are exposed as testability actions.</span><span class="sxs-lookup"><span data-stu-id="b58b6-105">These are exposed as testability actions.</span></span> <span data-ttu-id="b58b6-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span><span class="sxs-lookup"><span data-stu-id="b58b6-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="b58b6-107">By combining these actions, you can write comprehensive test scenarios for your services.</span><span class="sxs-lookup"><span data-stu-id="b58b6-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="b58b6-108">Service Fabric provides some common test scenarios composed of these actions.</span><span class="sxs-lookup"><span data-stu-id="b58b6-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="b58b6-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span><span class="sxs-lookup"><span data-stu-id="b58b6-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="b58b6-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span><span class="sxs-lookup"><span data-stu-id="b58b6-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="b58b6-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="b58b6-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="b58b6-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="b58b6-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="b58b6-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span><span class="sxs-lookup"><span data-stu-id="b58b6-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="b58b6-114">Graceful vs. ungraceful fault actions</span><span class="sxs-lookup"><span data-stu-id="b58b6-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="b58b6-115">Testability actions are classified into two major buckets:</span><span class="sxs-lookup"><span data-stu-id="b58b6-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="b58b6-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span><span class="sxs-lookup"><span data-stu-id="b58b6-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="b58b6-117">In such cases of failures, the execution context of process stops abruptly.</span><span class="sxs-lookup"><span data-stu-id="b58b6-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="b58b6-118">This means no cleanup of the state can run before the application starts up again.</span><span class="sxs-lookup"><span data-stu-id="b58b6-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="b58b6-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span><span class="sxs-lookup"><span data-stu-id="b58b6-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="b58b6-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span><span class="sxs-lookup"><span data-stu-id="b58b6-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="b58b6-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span><span class="sxs-lookup"><span data-stu-id="b58b6-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="b58b6-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span><span class="sxs-lookup"><span data-stu-id="b58b6-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="b58b6-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b58b6-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="b58b6-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span><span class="sxs-lookup"><span data-stu-id="b58b6-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="b58b6-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b58b6-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="b58b6-126">This tests handling of cancellation in the RunAsync method.</span><span class="sxs-lookup"><span data-stu-id="b58b6-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="b58b6-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span><span class="sxs-lookup"><span data-stu-id="b58b6-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="b58b6-128">Testability actions list</span><span class="sxs-lookup"><span data-stu-id="b58b6-128">Testability actions list</span></span>
| <span data-ttu-id="b58b6-129">Action</span><span class="sxs-lookup"><span data-stu-id="b58b6-129">Action</span></span> | <span data-ttu-id="b58b6-130">Description</span><span class="sxs-lookup"><span data-stu-id="b58b6-130">Description</span></span> | <span data-ttu-id="b58b6-131">Managed API</span><span class="sxs-lookup"><span data-stu-id="b58b6-131">Managed API</span></span> | <span data-ttu-id="b58b6-132">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="b58b6-132">PowerShell cmdlet</span></span> | <span data-ttu-id="b58b6-133">Graceful/ungraceful faults</span><span class="sxs-lookup"><span data-stu-id="b58b6-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b58b6-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="b58b6-134">CleanTestState</span></span> |<span data-ttu-id="b58b6-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span><span class="sxs-lookup"><span data-stu-id="b58b6-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="b58b6-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-136">CleanTestStateAsync</span></span> |<span data-ttu-id="b58b6-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="b58b6-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="b58b6-138">Not applicable</span><span class="sxs-lookup"><span data-stu-id="b58b6-138">Not applicable</span></span> |
| <span data-ttu-id="b58b6-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="b58b6-139">InvokeDataLoss</span></span> |<span data-ttu-id="b58b6-140">Induces data loss into a service partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="b58b6-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="b58b6-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="b58b6-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="b58b6-143">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-143">Graceful</span></span> |
| <span data-ttu-id="b58b6-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="b58b6-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="b58b6-145">Puts a given stateful service partition into quorum loss.</span><span class="sxs-lookup"><span data-stu-id="b58b6-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="b58b6-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="b58b6-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="b58b6-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="b58b6-148">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-148">Graceful</span></span> |
| <span data-ttu-id="b58b6-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="b58b6-149">Move Primary</span></span> |<span data-ttu-id="b58b6-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span><span class="sxs-lookup"><span data-stu-id="b58b6-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="b58b6-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-151">MovePrimaryAsync</span></span> |<span data-ttu-id="b58b6-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="b58b6-153">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-153">Graceful</span></span> |
| <span data-ttu-id="b58b6-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="b58b6-154">Move Secondary</span></span> |<span data-ttu-id="b58b6-155">Moves the current secondary replica of a stateful service to a different cluster node.</span><span class="sxs-lookup"><span data-stu-id="b58b6-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="b58b6-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="b58b6-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="b58b6-158">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-158">Graceful</span></span> |
| <span data-ttu-id="b58b6-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-159">RemoveReplica</span></span> |<span data-ttu-id="b58b6-160">Simulates a replica failure by removing a replica from a cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="b58b6-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="b58b6-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="b58b6-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="b58b6-164">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-164">Graceful</span></span> |
| <span data-ttu-id="b58b6-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="b58b6-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="b58b6-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="b58b6-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span><span class="sxs-lookup"><span data-stu-id="b58b6-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="b58b6-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="b58b6-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="b58b6-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="b58b6-170">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-170">Ungraceful</span></span> |
| <span data-ttu-id="b58b6-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-171">RestartNode</span></span> |<span data-ttu-id="b58b6-172">Simulates a Service Fabric cluster node failure by restarting a node.</span><span class="sxs-lookup"><span data-stu-id="b58b6-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="b58b6-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-173">RestartNodeAsync</span></span> |<span data-ttu-id="b58b6-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="b58b6-175">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-175">Ungraceful</span></span> |
| <span data-ttu-id="b58b6-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="b58b6-176">RestartPartition</span></span> |<span data-ttu-id="b58b6-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="b58b6-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-178">RestartPartitionAsync</span></span> |<span data-ttu-id="b58b6-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="b58b6-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="b58b6-180">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-180">Graceful</span></span> |
| <span data-ttu-id="b58b6-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-181">RestartReplica</span></span> |<span data-ttu-id="b58b6-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span><span class="sxs-lookup"><span data-stu-id="b58b6-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="b58b6-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-183">RestartReplicaAsync</span></span> |<span data-ttu-id="b58b6-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="b58b6-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="b58b6-185">Graceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-185">Graceful</span></span> |
| <span data-ttu-id="b58b6-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-186">StartNode</span></span> |<span data-ttu-id="b58b6-187">Starts a node in a cluster that is already stopped.</span><span class="sxs-lookup"><span data-stu-id="b58b6-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="b58b6-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-188">StartNodeAsync</span></span> |<span data-ttu-id="b58b6-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="b58b6-190">Not applicable</span><span class="sxs-lookup"><span data-stu-id="b58b6-190">Not applicable</span></span> |
| <span data-ttu-id="b58b6-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-191">StopNode</span></span> |<span data-ttu-id="b58b6-192">Simulates a node failure by stopping a node in a cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="b58b6-193">The node will stay down until StartNode is called.</span><span class="sxs-lookup"><span data-stu-id="b58b6-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="b58b6-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-194">StopNodeAsync</span></span> |<span data-ttu-id="b58b6-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="b58b6-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="b58b6-196">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="b58b6-196">Ungraceful</span></span> |
| <span data-ttu-id="b58b6-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="b58b6-197">ValidateApplication</span></span> |<span data-ttu-id="b58b6-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span><span class="sxs-lookup"><span data-stu-id="b58b6-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="b58b6-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="b58b6-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b58b6-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="b58b6-201">Not applicable</span><span class="sxs-lookup"><span data-stu-id="b58b6-201">Not applicable</span></span> |
| <span data-ttu-id="b58b6-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="b58b6-202">ValidateService</span></span> |<span data-ttu-id="b58b6-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span><span class="sxs-lookup"><span data-stu-id="b58b6-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="b58b6-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="b58b6-204">ValidateServiceAsync</span></span> |<span data-ttu-id="b58b6-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="b58b6-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="b58b6-206">Not applicable</span><span class="sxs-lookup"><span data-stu-id="b58b6-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="b58b6-207">Running a testability action using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b58b6-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="b58b6-208">This tutorial shows you how to run a testability action by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b58b6-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="b58b6-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="b58b6-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span><span class="sxs-lookup"><span data-stu-id="b58b6-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="b58b6-211">The module is loaded automatically when you open a PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="b58b6-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="b58b6-212">Tutorial segments:</span><span class="sxs-lookup"><span data-stu-id="b58b6-212">Tutorial segments:</span></span>

* [<span data-ttu-id="b58b6-213">Run an action against a one-box cluster</span><span class="sxs-lookup"><span data-stu-id="b58b6-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="b58b6-214">Run an action against an Azure cluster</span><span class="sxs-lookup"><span data-stu-id="b58b6-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="b58b6-215">Run an action against a one-box cluster</span><span class="sxs-lookup"><span data-stu-id="b58b6-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="b58b6-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span><span class="sxs-lookup"><span data-stu-id="b58b6-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="b58b6-217">Let us look at the **Restart-ServiceFabricNode** action.</span><span class="sxs-lookup"><span data-stu-id="b58b6-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="b58b6-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span><span class="sxs-lookup"><span data-stu-id="b58b6-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="b58b6-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span><span class="sxs-lookup"><span data-stu-id="b58b6-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="b58b6-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span><span class="sxs-lookup"><span data-stu-id="b58b6-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="b58b6-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span><span class="sxs-lookup"><span data-stu-id="b58b6-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="b58b6-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="b58b6-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span><span class="sxs-lookup"><span data-stu-id="b58b6-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="b58b6-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span><span class="sxs-lookup"><span data-stu-id="b58b6-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="b58b6-225">It helps simulate node failures in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="b58b6-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span><span class="sxs-lookup"><span data-stu-id="b58b6-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="b58b6-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span><span class="sxs-lookup"><span data-stu-id="b58b6-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="b58b6-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span><span class="sxs-lookup"><span data-stu-id="b58b6-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="b58b6-229">Run an action against an Azure cluster</span><span class="sxs-lookup"><span data-stu-id="b58b6-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="b58b6-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="b58b6-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span><span class="sxs-lookup"><span data-stu-id="b58b6-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="b58b6-232">Running a testability action using C&#35;</span><span class="sxs-lookup"><span data-stu-id="b58b6-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="b58b6-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span><span class="sxs-lookup"><span data-stu-id="b58b6-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="b58b6-234">Then obtain the parameters needed to run the action.</span><span class="sxs-lookup"><span data-stu-id="b58b6-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="b58b6-235">Different parameters can be used to run the same action.</span><span class="sxs-lookup"><span data-stu-id="b58b6-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="b58b6-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b58b6-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="b58b6-237">Parameter explanation:</span><span class="sxs-lookup"><span data-stu-id="b58b6-237">Parameter explanation:</span></span>

* <span data-ttu-id="b58b6-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span><span class="sxs-lookup"><span data-stu-id="b58b6-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="b58b6-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span><span class="sxs-lookup"><span data-stu-id="b58b6-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="b58b6-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span><span class="sxs-lookup"><span data-stu-id="b58b6-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="b58b6-241">**CancellationToken** enables a pending call to be canceled.</span><span class="sxs-lookup"><span data-stu-id="b58b6-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="b58b6-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span><span class="sxs-lookup"><span data-stu-id="b58b6-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="b58b6-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="b58b6-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="b58b6-244">PartitionSelector and ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="b58b6-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="b58b6-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="b58b6-245">PartitionSelector</span></span>
<span data-ttu-id="b58b6-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span><span class="sxs-lookup"><span data-stu-id="b58b6-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="b58b6-247">It can be used to select a specific partition if the partition ID is known beforehand.</span><span class="sxs-lookup"><span data-stu-id="b58b6-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="b58b6-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span><span class="sxs-lookup"><span data-stu-id="b58b6-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="b58b6-249">You also have the option of selecting a random partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="b58b6-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select\* methods.</span><span class="sxs-lookup"><span data-stu-id="b58b6-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select\* methods.</span></span> <span data-ttu-id="b58b6-251">Then pass in the PartitionSelector object to the API that requires it.</span><span class="sxs-lookup"><span data-stu-id="b58b6-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="b58b6-252">If no option is selected, it defaults to a random partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-252">If no option is selected, it defaults to a random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="b58b6-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="b58b6-253">ReplicaSelector</span></span>
<span data-ttu-id="b58b6-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span><span class="sxs-lookup"><span data-stu-id="b58b6-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="b58b6-255">It can be used to select a specific replica if the replica ID is known beforehand.</span><span class="sxs-lookup"><span data-stu-id="b58b6-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="b58b6-256">In addition, you have the option of selecting a primary replica or a random secondary.</span><span class="sxs-lookup"><span data-stu-id="b58b6-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="b58b6-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span><span class="sxs-lookup"><span data-stu-id="b58b6-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="b58b6-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="b58b6-259">You can then pass it into the API that requires it.</span><span class="sxs-lookup"><span data-stu-id="b58b6-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="b58b6-260">If no option is selected, it defaults to a random replica and random partition.</span><span class="sxs-lookup"><span data-stu-id="b58b6-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="b58b6-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="b58b6-261">Next steps</span></span>
* [<span data-ttu-id="b58b6-262">Testability scenarios</span><span class="sxs-lookup"><span data-stu-id="b58b6-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="b58b6-263">How to test your service</span><span class="sxs-lookup"><span data-stu-id="b58b6-263">How to test your service</span></span>
  * [<span data-ttu-id="b58b6-264">Simulate failures during service workloads</span><span class="sxs-lookup"><span data-stu-id="b58b6-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="b58b6-265">Service-to-service communication failures</span><span class="sxs-lookup"><span data-stu-id="b58b6-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)


