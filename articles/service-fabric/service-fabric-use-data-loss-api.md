---
title: How to Invoke Data Loss on Service Fabric Services | Microsoft Docs
description: Describes how to use the data loss api
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: ''
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 8359a03c651f6a03aa8a88e0485ceb374b742b63
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555394"
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="15601-103">How to Invoke Data Loss on Services</span><span class="sxs-lookup"><span data-stu-id="15601-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="15601-104">This document describe how to cause data loss in your services, and should be used with care.</span><span class="sxs-lookup"><span data-stu-id="15601-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="15601-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="15601-105">Introduction</span></span>
<span data-ttu-id="15601-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="15601-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="15601-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span><span class="sxs-lookup"><span data-stu-id="15601-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="15601-108">Using the Fault Injection and Analysis Service</span><span class="sxs-lookup"><span data-stu-id="15601-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="15601-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span><span class="sxs-lookup"><span data-stu-id="15601-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="15601-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="15601-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="15601-111">Please refer to the msdn documentation on each API for more information on each one.</span><span class="sxs-lookup"><span data-stu-id="15601-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="15601-112">C# API</span><span class="sxs-lookup"><span data-stu-id="15601-112">C# API</span></span> | <span data-ttu-id="15601-113">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="15601-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="15601-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="15601-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="15601-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="15601-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="15601-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="15601-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="15601-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="15601-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="15601-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="15601-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="15601-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="15601-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="15601-120">Conceptual Overview of Running a Command</span><span class="sxs-lookup"><span data-stu-id="15601-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="15601-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span><span class="sxs-lookup"><span data-stu-id="15601-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="15601-122">To start a command, call the “Start” API for the corresponding API.</span><span class="sxs-lookup"><span data-stu-id="15601-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="15601-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span><span class="sxs-lookup"><span data-stu-id="15601-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="15601-124">However, it does not indicate how far a command has run, or even if it has started yet.</span><span class="sxs-lookup"><span data-stu-id="15601-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="15601-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span><span class="sxs-lookup"><span data-stu-id="15601-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="15601-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span><span class="sxs-lookup"><span data-stu-id="15601-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="15601-127">A command runs indefinitely until:</span><span class="sxs-lookup"><span data-stu-id="15601-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="15601-128">It completes successfully.</span><span class="sxs-lookup"><span data-stu-id="15601-128">It completes successfully.</span></span>  <span data-ttu-id="15601-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span><span class="sxs-lookup"><span data-stu-id="15601-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="15601-130">It encounters a fatal error.</span><span class="sxs-lookup"><span data-stu-id="15601-130">It encounters a fatal error.</span></span>  <span data-ttu-id="15601-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span><span class="sxs-lookup"><span data-stu-id="15601-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="15601-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="15601-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="15601-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span><span class="sxs-lookup"><span data-stu-id="15601-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="15601-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span><span class="sxs-lookup"><span data-stu-id="15601-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="15601-135">Details of Running a Command</span><span class="sxs-lookup"><span data-stu-id="15601-135">Details of Running a Command</span></span>
<span data-ttu-id="15601-136">In order to start a command, call the Start API with the expected arguments.</span><span class="sxs-lookup"><span data-stu-id="15601-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="15601-137">All Start APIs have a Guid argument named operationId.</span><span class="sxs-lookup"><span data-stu-id="15601-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="15601-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span><span class="sxs-lookup"><span data-stu-id="15601-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="15601-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span><span class="sxs-lookup"><span data-stu-id="15601-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="15601-140">The operationId must be unique.</span><span class="sxs-lookup"><span data-stu-id="15601-140">The operationId must be unique.</span></span>

<span data-ttu-id="15601-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span><span class="sxs-lookup"><span data-stu-id="15601-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="15601-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span><span class="sxs-lookup"><span data-stu-id="15601-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="15601-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span><span class="sxs-lookup"><span data-stu-id="15601-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="15601-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span><span class="sxs-lookup"><span data-stu-id="15601-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="15601-145">Result.Exception will be null.</span><span class="sxs-lookup"><span data-stu-id="15601-145">Result.Exception will be null.</span></span>  <span data-ttu-id="15601-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span><span class="sxs-lookup"><span data-stu-id="15601-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="15601-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span><span class="sxs-lookup"><span data-stu-id="15601-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="15601-148">In some situations, the command may not have proceeded far enough to choose a partition.</span><span class="sxs-lookup"><span data-stu-id="15601-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="15601-149">In that case, the PartitionId will be 0.</span><span class="sxs-lookup"><span data-stu-id="15601-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="15601-150">If the state is Cancelled, Result.Exception will be null.</span><span class="sxs-lookup"><span data-stu-id="15601-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="15601-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span><span class="sxs-lookup"><span data-stu-id="15601-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="15601-152">Please also refer to the sample below.</span><span class="sxs-lookup"><span data-stu-id="15601-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="15601-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span><span class="sxs-lookup"><span data-stu-id="15601-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="15601-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span><span class="sxs-lookup"><span data-stu-id="15601-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="15601-155">History and Truncation</span><span class="sxs-lookup"><span data-stu-id="15601-155">History and Truncation</span></span>
<span data-ttu-id="15601-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span><span class="sxs-lookup"><span data-stu-id="15601-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="15601-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="15601-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
