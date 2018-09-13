---
title: Eternal orchestrations in Durable Functions - Azure
description: Learn how to implement eternal orchestrations by using the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 98504534332b6faa7a7019aea9ab7b534d4c3faa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969163"
---
# <a name="eternal-orchestrations-in-durable-functions-azure-functions"></a><span data-ttu-id="724f9-103">Eternal orchestrations in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="724f9-103">Eternal orchestrations in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="724f9-104">*Eternal orchestrations* are orchestrator functions that never end.</span><span class="sxs-lookup"><span data-stu-id="724f9-104">*Eternal orchestrations* are orchestrator functions that never end.</span></span> <span data-ttu-id="724f9-105">They are useful when you want to use [Durable Functions](durable-functions-overview.md) for aggregators and any scenario that requires an infinite loop.</span><span class="sxs-lookup"><span data-stu-id="724f9-105">They are useful when you want to use [Durable Functions](durable-functions-overview.md) for aggregators and any scenario that requires an infinite loop.</span></span>

## <a name="orchestration-history"></a><span data-ttu-id="724f9-106">Orchestration history</span><span class="sxs-lookup"><span data-stu-id="724f9-106">Orchestration history</span></span>

<span data-ttu-id="724f9-107">As explained in [Checkpointing and Replay](durable-functions-checkpointing-and-replay.md), the Durable Task Framework keeps track of the history of each function orchestration.</span><span class="sxs-lookup"><span data-stu-id="724f9-107">As explained in [Checkpointing and Replay](durable-functions-checkpointing-and-replay.md), the Durable Task Framework keeps track of the history of each function orchestration.</span></span> <span data-ttu-id="724f9-108">This history grows continuously as long as the orchestrator function continues to schedule new work.</span><span class="sxs-lookup"><span data-stu-id="724f9-108">This history grows continuously as long as the orchestrator function continues to schedule new work.</span></span> <span data-ttu-id="724f9-109">If the orchestrator function goes into an infinite loop and continuously schedules work, this history could grow critically large and cause significant performance problems.</span><span class="sxs-lookup"><span data-stu-id="724f9-109">If the orchestrator function goes into an infinite loop and continuously schedules work, this history could grow critically large and cause significant performance problems.</span></span> <span data-ttu-id="724f9-110">The *eternal orchestration* concept was designed to mitigate these kinds of problems for applications that need infinite loops.</span><span class="sxs-lookup"><span data-stu-id="724f9-110">The *eternal orchestration* concept was designed to mitigate these kinds of problems for applications that need infinite loops.</span></span>

## <a name="resetting-and-restarting"></a><span data-ttu-id="724f9-111">Resetting and restarting</span><span class="sxs-lookup"><span data-stu-id="724f9-111">Resetting and restarting</span></span>

<span data-ttu-id="724f9-112">Instead of using infinite loops, orchestrator functions reset their state by calling the [ContinueAsNew](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_ContinueAsNew_) method.</span><span class="sxs-lookup"><span data-stu-id="724f9-112">Instead of using infinite loops, orchestrator functions reset their state by calling the [ContinueAsNew](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_ContinueAsNew_) method.</span></span> <span data-ttu-id="724f9-113">This method takes a single JSON-serializable parameter, which becomes the new input for the next orchestrator function generation.</span><span class="sxs-lookup"><span data-stu-id="724f9-113">This method takes a single JSON-serializable parameter, which becomes the new input for the next orchestrator function generation.</span></span>

<span data-ttu-id="724f9-114">When `ContinueAsNew` is called, the instance enqueues a message to itself before it exits.</span><span class="sxs-lookup"><span data-stu-id="724f9-114">When `ContinueAsNew` is called, the instance enqueues a message to itself before it exits.</span></span> <span data-ttu-id="724f9-115">The message restarts the instance with the new input value.</span><span class="sxs-lookup"><span data-stu-id="724f9-115">The message restarts the instance with the new input value.</span></span> <span data-ttu-id="724f9-116">The same instance ID is kept, but the orchestrator function's history is effectively truncated.</span><span class="sxs-lookup"><span data-stu-id="724f9-116">The same instance ID is kept, but the orchestrator function's history is effectively truncated.</span></span>

> [!NOTE]
> <span data-ttu-id="724f9-117">The Durable Task Framework maintains the same instance ID but internally creates a new *execution ID* for the orchestrator function that gets reset by `ContinueAsNew`.</span><span class="sxs-lookup"><span data-stu-id="724f9-117">The Durable Task Framework maintains the same instance ID but internally creates a new *execution ID* for the orchestrator function that gets reset by `ContinueAsNew`.</span></span> <span data-ttu-id="724f9-118">This execution ID is generally not exposed externally, but it may be useful to know about when debugging orchestration execution.</span><span class="sxs-lookup"><span data-stu-id="724f9-118">This execution ID is generally not exposed externally, but it may be useful to know about when debugging orchestration execution.</span></span>

> [!NOTE]
> <span data-ttu-id="724f9-119">The `ContinueAsNew` method is not yet available in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="724f9-119">The `ContinueAsNew` method is not yet available in JavaScript.</span></span>

## <a name="periodic-work-example"></a><span data-ttu-id="724f9-120">Periodic work example</span><span class="sxs-lookup"><span data-stu-id="724f9-120">Periodic work example</span></span>

<span data-ttu-id="724f9-121">One use case for eternal orchestrations is code that needs to do periodic work indefinitely.</span><span class="sxs-lookup"><span data-stu-id="724f9-121">One use case for eternal orchestrations is code that needs to do periodic work indefinitely.</span></span>

```csharp
[FunctionName("Periodic_Cleanup_Loop")]
public static async Task Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    await context.CallActivityAsync("DoCleanup");

    // sleep for one hour between cleanups
    DateTime nextCleanup = context.CurrentUtcDateTime.AddHours(1);
    await context.CreateTimer(nextCleanup, CancellationToken.None);

    context.ContinueAsNew(null);
}
```

<span data-ttu-id="724f9-122">The difference between this example and a timer-triggered function is that cleanup trigger times here are not based on a schedule.</span><span class="sxs-lookup"><span data-stu-id="724f9-122">The difference between this example and a timer-triggered function is that cleanup trigger times here are not based on a schedule.</span></span> <span data-ttu-id="724f9-123">For example, a CRON schedule that executes a function every hour will execute it at 1:00, 2:00, 3:00 etc. and could potentially run into overlap issues.</span><span class="sxs-lookup"><span data-stu-id="724f9-123">For example, a CRON schedule that executes a function every hour will execute it at 1:00, 2:00, 3:00 etc. and could potentially run into overlap issues.</span></span> <span data-ttu-id="724f9-124">In this example, however, if the cleanup takes 30 minutes, then it will be scheduled at 1:00, 2:30, 4:00, etc. and there is no chance of overlap.</span><span class="sxs-lookup"><span data-stu-id="724f9-124">In this example, however, if the cleanup takes 30 minutes, then it will be scheduled at 1:00, 2:30, 4:00, etc. and there is no chance of overlap.</span></span>

## <a name="exit-from-an-eternal-orchestration"></a><span data-ttu-id="724f9-125">Exit from an eternal orchestration</span><span class="sxs-lookup"><span data-stu-id="724f9-125">Exit from an eternal orchestration</span></span>

<span data-ttu-id="724f9-126">If an orchestrator function needs to eventually complete, then all you need to do is *not* call `ContinueAsNew` and let the function exit.</span><span class="sxs-lookup"><span data-stu-id="724f9-126">If an orchestrator function needs to eventually complete, then all you need to do is *not* call `ContinueAsNew` and let the function exit.</span></span>

<span data-ttu-id="724f9-127">If an orchestrator function is in an infinite loop and needs to be stopped, use the [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) method to stop it.</span><span class="sxs-lookup"><span data-stu-id="724f9-127">If an orchestrator function is in an infinite loop and needs to be stopped, use the [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) method to stop it.</span></span> <span data-ttu-id="724f9-128">For more information, see [Instance Management](durable-functions-instance-management.md).</span><span class="sxs-lookup"><span data-stu-id="724f9-128">For more information, see [Instance Management](durable-functions-instance-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="724f9-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="724f9-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="724f9-130">Learn how to implement singleton orchestrations</span><span class="sxs-lookup"><span data-stu-id="724f9-130">Learn how to implement singleton orchestrations</span></span>](durable-functions-singletons.md)
