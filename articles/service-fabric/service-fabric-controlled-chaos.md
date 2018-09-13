---
title: Induce Chaos in Service Fabric clusters | Microsoft Docs
description: Using Fault Injection and Cluster Analysis Service APIs to manage Chaos in the cluster.
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/19/2017
ms.author: motanv
ms.openlocfilehash: 79930561d5ccccbfee8d40d6eb0950dc57e5af52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550853"
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="3cdff-103">Induce controlled Chaos in Service Fabric clusters</span><span class="sxs-lookup"><span data-stu-id="3cdff-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="3cdff-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span><span class="sxs-lookup"><span data-stu-id="3cdff-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="3cdff-105">Azure Service Fabric enables developers to write reliable services on top of an unreliable infrastructure.</span><span class="sxs-lookup"><span data-stu-id="3cdff-105">Azure Service Fabric enables developers to write reliable services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="3cdff-106">To write robust services, developers need to be able to induce faults against such unreliable infrastructure to test the stability of their services.</span><span class="sxs-lookup"><span data-stu-id="3cdff-106">To write robust services, developers need to be able to induce faults against such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="3cdff-107">The Fault Injection and Cluster Analysis Service (also known as the Fault Analysis Service) gives developers the ability to induce fault actions to test services.</span><span class="sxs-lookup"><span data-stu-id="3cdff-107">The Fault Injection and Cluster Analysis Service (also known as the Fault Analysis Service) gives developers the ability to induce fault actions to test services.</span></span> <span data-ttu-id="3cdff-108">However, targeted simulated faults get you only so far.</span><span class="sxs-lookup"><span data-stu-id="3cdff-108">However, targeted simulated faults get you only so far.</span></span> <span data-ttu-id="3cdff-109">To take the testing further, you can use Chaos.</span><span class="sxs-lookup"><span data-stu-id="3cdff-109">To take the testing further, you can use Chaos.</span></span>

<span data-ttu-id="3cdff-110">Chaos simulates continuous, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="3cdff-110">Chaos simulates continuous, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="3cdff-111">After you configure Chaos with the rate and the kind of faults, you can start or stop it through either C# APIs or PowerShell to generate faults in the cluster and your service.</span><span class="sxs-lookup"><span data-stu-id="3cdff-111">After you configure Chaos with the rate and the kind of faults, you can start or stop it through either C# APIs or PowerShell to generate faults in the cluster and your service.</span></span>

<span data-ttu-id="3cdff-112">While Chaos is running, it produces different events that capture the state of the run at the moment.</span><span class="sxs-lookup"><span data-stu-id="3cdff-112">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="3cdff-113">For example, an ExecutingFaultsEvent contains all the faults that are being executed in that iteration.</span><span class="sxs-lookup"><span data-stu-id="3cdff-113">For example, an ExecutingFaultsEvent contains all the faults that are being executed in that iteration.</span></span> <span data-ttu-id="3cdff-114">A ValidationFailedEvent contains the details of a failure that was found during cluster validation.</span><span class="sxs-lookup"><span data-stu-id="3cdff-114">A ValidationFailedEvent contains the details of a failure that was found during cluster validation.</span></span> <span data-ttu-id="3cdff-115">You can invoke the GetChaosReportAsync API to get the report of Chaos runs.</span><span class="sxs-lookup"><span data-stu-id="3cdff-115">You can invoke the GetChaosReportAsync API to get the report of Chaos runs.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="3cdff-116">Faults induced in Chaos</span><span class="sxs-lookup"><span data-stu-id="3cdff-116">Faults induced in Chaos</span></span>
<span data-ttu-id="3cdff-117">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span><span class="sxs-lookup"><span data-stu-id="3cdff-117">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="3cdff-118">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span><span class="sxs-lookup"><span data-stu-id="3cdff-118">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="3cdff-119">This Chaos exercise leads to a significant improvement in the code quality of the service.</span><span class="sxs-lookup"><span data-stu-id="3cdff-119">This Chaos exercise leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="3cdff-120">Chaos induces faults from the following categories:</span><span class="sxs-lookup"><span data-stu-id="3cdff-120">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="3cdff-121">Restart a node</span><span class="sxs-lookup"><span data-stu-id="3cdff-121">Restart a node</span></span>
* <span data-ttu-id="3cdff-122">Restart a deployed code package</span><span class="sxs-lookup"><span data-stu-id="3cdff-122">Restart a deployed code package</span></span>
* <span data-ttu-id="3cdff-123">Remove a replica</span><span class="sxs-lookup"><span data-stu-id="3cdff-123">Remove a replica</span></span>
* <span data-ttu-id="3cdff-124">Restart a replica</span><span class="sxs-lookup"><span data-stu-id="3cdff-124">Restart a replica</span></span>
* <span data-ttu-id="3cdff-125">Move a primary replica (configurable)</span><span class="sxs-lookup"><span data-stu-id="3cdff-125">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="3cdff-126">Move a secondary replica (configurable)</span><span class="sxs-lookup"><span data-stu-id="3cdff-126">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="3cdff-127">Chaos runs in multiple iterations.</span><span class="sxs-lookup"><span data-stu-id="3cdff-127">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="3cdff-128">Each iteration consists of faults and cluster validation for the specified period.</span><span class="sxs-lookup"><span data-stu-id="3cdff-128">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="3cdff-129">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span><span class="sxs-lookup"><span data-stu-id="3cdff-129">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="3cdff-130">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span><span class="sxs-lookup"><span data-stu-id="3cdff-130">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span>

<span data-ttu-id="3cdff-131">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span><span class="sxs-lookup"><span data-stu-id="3cdff-131">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="3cdff-132">Chaos induces three faults, and then validates the cluster health.</span><span class="sxs-lookup"><span data-stu-id="3cdff-132">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="3cdff-133">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span><span class="sxs-lookup"><span data-stu-id="3cdff-133">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="3cdff-134">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within a configured time), Chaos generates a ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="3cdff-134">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within a configured time), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="3cdff-135">This event indicates that something has gone wrong and might need further investigation.</span><span class="sxs-lookup"><span data-stu-id="3cdff-135">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="3cdff-136">In its current form, Chaos induces only safe faults.</span><span class="sxs-lookup"><span data-stu-id="3cdff-136">In its current form, Chaos induces only safe faults.</span></span> <span data-ttu-id="3cdff-137">This implies that, in the absence of external faults, a quorum loss or data loss never occurs.</span><span class="sxs-lookup"><span data-stu-id="3cdff-137">This implies that, in the absence of external faults, a quorum loss or data loss never occurs.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="3cdff-138">Important configuration options</span><span class="sxs-lookup"><span data-stu-id="3cdff-138">Important configuration options</span></span>
* <span data-ttu-id="3cdff-139">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span><span class="sxs-lookup"><span data-stu-id="3cdff-139">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="3cdff-140">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="3cdff-140">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>
* <span data-ttu-id="3cdff-141">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before checking on it again.</span><span class="sxs-lookup"><span data-stu-id="3cdff-141">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before checking on it again.</span></span> <span data-ttu-id="3cdff-142">This wait is to reduce the load on the cluster while it is recovering.</span><span class="sxs-lookup"><span data-stu-id="3cdff-142">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="3cdff-143">The checks performed are:</span><span class="sxs-lookup"><span data-stu-id="3cdff-143">The checks performed are:</span></span>
  * <span data-ttu-id="3cdff-144">If the cluster health is OK</span><span class="sxs-lookup"><span data-stu-id="3cdff-144">If the cluster health is OK</span></span>
  * <span data-ttu-id="3cdff-145">If the service health is OK</span><span class="sxs-lookup"><span data-stu-id="3cdff-145">If the service health is OK</span></span>
  * <span data-ttu-id="3cdff-146">If the target replica set size is achieved for the service partition</span><span class="sxs-lookup"><span data-stu-id="3cdff-146">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="3cdff-147">That no InBuild replicas exist</span><span class="sxs-lookup"><span data-stu-id="3cdff-147">That no InBuild replicas exist</span></span>
* <span data-ttu-id="3cdff-148">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span><span class="sxs-lookup"><span data-stu-id="3cdff-148">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="3cdff-149">The higher the number, the more aggressive Chaos is.</span><span class="sxs-lookup"><span data-stu-id="3cdff-149">The higher the number, the more aggressive Chaos is.</span></span> <span data-ttu-id="3cdff-150">This results in more complex failovers and transition combinations.</span><span class="sxs-lookup"><span data-stu-id="3cdff-150">This results in more complex failovers and transition combinations.</span></span> <span data-ttu-id="3cdff-151">Chaos guarantees that, in the absence of external faults, there is no quorum loss or data loss, regardless of how high a value this configuration has.</span><span class="sxs-lookup"><span data-stu-id="3cdff-151">Chaos guarantees that, in the absence of external faults, there is no quorum loss or data loss, regardless of how high a value this configuration has.</span></span>
* <span data-ttu-id="3cdff-152">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span><span class="sxs-lookup"><span data-stu-id="3cdff-152">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="3cdff-153">These faults are disabled by default.</span><span class="sxs-lookup"><span data-stu-id="3cdff-153">These faults are disabled by default.</span></span>
* <span data-ttu-id="3cdff-154">**WaitTimeBetweenIterations**: The amount of time to wait between iterations, that is, after a round of faults and corresponding validation.</span><span class="sxs-lookup"><span data-stu-id="3cdff-154">**WaitTimeBetweenIterations**: The amount of time to wait between iterations, that is, after a round of faults and corresponding validation.</span></span>
* <span data-ttu-id="3cdff-155">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in an iteration.</span><span class="sxs-lookup"><span data-stu-id="3cdff-155">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in an iteration.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="3cdff-156">How to run Chaos</span><span class="sxs-lookup"><span data-stu-id="3cdff-156">How to run Chaos</span></span>
<span data-ttu-id="3cdff-157">**C#:**</span><span class="sxs-lookup"><span data-stu-id="3cdff-157">**C#:**</span></span>

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
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

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

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.add(chaosEvent))
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
<span data-ttu-id="3cdff-158">**PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="3cdff-158">**PowerShell:**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

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
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
