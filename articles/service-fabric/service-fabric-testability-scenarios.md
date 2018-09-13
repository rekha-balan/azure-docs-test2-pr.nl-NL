---
title: Create chaos and failover tests for Azure Service Fabric | Microsoft Docs
description: Using the Service Fabric chaos test and failover test scenarios to induce faults and verify the reliability of your services.
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 7cb911e50a87e0997982688c8127f01ea0588575
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805615"
---
# <a name="testability-scenarios"></a><span data-ttu-id="ca5ca-103">Testability scenarios</span><span class="sxs-lookup"><span data-stu-id="ca5ca-103">Testability scenarios</span></span>
<span data-ttu-id="ca5ca-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="ca5ca-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="ca5ca-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="ca5ca-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="ca5ca-108">However, targeted simulated faults will get you only so far.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="ca5ca-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="ca5ca-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="ca5ca-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="ca5ca-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="ca5ca-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="ca5ca-114">Chaos test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-114">Chaos test</span></span>
<span data-ttu-id="ca5ca-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="ca5ca-116">The scenario compresses faults generally seen in months or years to a few hours.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="ca5ca-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="ca5ca-118">This leads to a significant improvement in the code quality of the service.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="ca5ca-119">Faults simulated in the chaos test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="ca5ca-120">Restart a node</span><span class="sxs-lookup"><span data-stu-id="ca5ca-120">Restart a node</span></span>
* <span data-ttu-id="ca5ca-121">Restart a deployed code package</span><span class="sxs-lookup"><span data-stu-id="ca5ca-121">Restart a deployed code package</span></span>
* <span data-ttu-id="ca5ca-122">Remove a replica</span><span class="sxs-lookup"><span data-stu-id="ca5ca-122">Remove a replica</span></span>
* <span data-ttu-id="ca5ca-123">Restart a replica</span><span class="sxs-lookup"><span data-stu-id="ca5ca-123">Restart a replica</span></span>
* <span data-ttu-id="ca5ca-124">Move a primary replica (optional)</span><span class="sxs-lookup"><span data-stu-id="ca5ca-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="ca5ca-125">Move a secondary replica (optional)</span><span class="sxs-lookup"><span data-stu-id="ca5ca-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="ca5ca-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="ca5ca-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="ca5ca-128">The scenario fails when you hit a single failure in cluster validation.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="ca5ca-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="ca5ca-130">The test will induce three faults, and then validate the cluster health.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="ca5ca-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="ca5ca-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="ca5ca-133">This exception indicates that something has gone wrong and needs further investigation.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="ca5ca-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="ca5ca-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="ca5ca-136">Important configuration options</span><span class="sxs-lookup"><span data-stu-id="ca5ca-136">Important configuration options</span></span>
* <span data-ttu-id="ca5ca-137">**TimeToRun**: Total time that the test will run before finishing with success.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="ca5ca-138">The test can finish earlier in lieu of a validation failure.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="ca5ca-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="ca5ca-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="ca5ca-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="ca5ca-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="ca5ca-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="ca5ca-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="ca5ca-145">These faults are disabled by default.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="ca5ca-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="ca5ca-147">How to run the chaos test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-147">How to run the chaos test</span></span>
<span data-ttu-id="ca5ca-148">C# sample</span><span class="sxs-lookup"><span data-stu-id="ca5ca-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="ca5ca-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca5ca-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="ca5ca-150">Failover test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-150">Failover test</span></span>
<span data-ttu-id="ca5ca-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="ca5ca-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="ca5ca-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="ca5ca-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="ca5ca-155">A failure in service validation indicates an issue that needs further investigation.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="ca5ca-156">Faults simulated in the failover test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="ca5ca-157">Restart a deployed code package where the partition is hosted</span><span class="sxs-lookup"><span data-stu-id="ca5ca-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="ca5ca-158">Remove a primary/secondary replica or stateless instance</span><span class="sxs-lookup"><span data-stu-id="ca5ca-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="ca5ca-159">Restart a primary secondary replica (if a persisted service)</span><span class="sxs-lookup"><span data-stu-id="ca5ca-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="ca5ca-160">Move a primary replica</span><span class="sxs-lookup"><span data-stu-id="ca5ca-160">Move a primary replica</span></span>
* <span data-ttu-id="ca5ca-161">Move a secondary replica</span><span class="sxs-lookup"><span data-stu-id="ca5ca-161">Move a secondary replica</span></span>
* <span data-ttu-id="ca5ca-162">Restart the partition</span><span class="sxs-lookup"><span data-stu-id="ca5ca-162">Restart the partition</span></span>

<span data-ttu-id="ca5ca-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="ca5ca-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="ca5ca-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="ca5ca-166">The test induces only safe faults.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-166">The test induces only safe faults.</span></span> <span data-ttu-id="ca5ca-167">This means that in absence of external failures, a quorum or data loss will not occur.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="ca5ca-168">Important configuration options</span><span class="sxs-lookup"><span data-stu-id="ca5ca-168">Important configuration options</span></span>
* <span data-ttu-id="ca5ca-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="ca5ca-170">**TimeToRun**: Total time that the test will run before finishing.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="ca5ca-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="ca5ca-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="ca5ca-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span><span class="sxs-lookup"><span data-stu-id="ca5ca-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="ca5ca-174">How to run the failover test</span><span class="sxs-lookup"><span data-stu-id="ca5ca-174">How to run the failover test</span></span>
<span data-ttu-id="ca5ca-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="ca5ca-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="ca5ca-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ca5ca-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
