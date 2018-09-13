---
title: Versioning in Durable Functions - Azure
description: Learn how to implement versioning in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 9d628f48f4958e4e763ed0064462a5fb2ed398bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869307"
---
# <a name="versioning-in-durable-functions-azure-functions"></a><span data-ttu-id="46d7c-103">Versioning in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="46d7c-103">Versioning in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="46d7c-104">It is inevitable that functions will be added, removed, and changed over the lifetime of an application.</span><span class="sxs-lookup"><span data-stu-id="46d7c-104">It is inevitable that functions will be added, removed, and changed over the lifetime of an application.</span></span> <span data-ttu-id="46d7c-105">[Durable Functions](durable-functions-overview.md) allows chaining functions together in ways that weren't previously possible, and this chaining affects how you can handle versioning.</span><span class="sxs-lookup"><span data-stu-id="46d7c-105">[Durable Functions](durable-functions-overview.md) allows chaining functions together in ways that weren't previously possible, and this chaining affects how you can handle versioning.</span></span>

## <a name="how-to-handle-breaking-changes"></a><span data-ttu-id="46d7c-106">How to handle breaking changes</span><span class="sxs-lookup"><span data-stu-id="46d7c-106">How to handle breaking changes</span></span>

<span data-ttu-id="46d7c-107">There are several examples of breaking changes to be aware of.</span><span class="sxs-lookup"><span data-stu-id="46d7c-107">There are several examples of breaking changes to be aware of.</span></span> <span data-ttu-id="46d7c-108">This article discusses the most common ones.</span><span class="sxs-lookup"><span data-stu-id="46d7c-108">This article discusses the most common ones.</span></span> <span data-ttu-id="46d7c-109">The main theme behind all of them is that both new and existing function orchestrations are impacted by changes to function code.</span><span class="sxs-lookup"><span data-stu-id="46d7c-109">The main theme behind all of them is that both new and existing function orchestrations are impacted by changes to function code.</span></span>

### <a name="changing-activity-function-signatures"></a><span data-ttu-id="46d7c-110">Changing activity function signatures</span><span class="sxs-lookup"><span data-stu-id="46d7c-110">Changing activity function signatures</span></span>

<span data-ttu-id="46d7c-111">A signature change refers to a change in the name, input, or output of a function.</span><span class="sxs-lookup"><span data-stu-id="46d7c-111">A signature change refers to a change in the name, input, or output of a function.</span></span> <span data-ttu-id="46d7c-112">If this kind of change is made to an activity function, it could break the orchestrator function that depends on it.</span><span class="sxs-lookup"><span data-stu-id="46d7c-112">If this kind of change is made to an activity function, it could break the orchestrator function that depends on it.</span></span> <span data-ttu-id="46d7c-113">If you update the orchestrator function to accommodate this change, you could break existing in-flight instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-113">If you update the orchestrator function to accommodate this change, you could break existing in-flight instances.</span></span>

<span data-ttu-id="46d7c-114">As an example, suppose we have the following function.</span><span class="sxs-lookup"><span data-stu-id="46d7c-114">As an example, suppose we have the following function.</span></span>

```csharp
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    bool result = await context.CallActivityAsync<bool>("Foo");
    await context.CallActivityAsync("Bar", result);
}
```

<span data-ttu-id="46d7c-115">This simplistic function takes the results of **Foo** and passes it to **Bar**.</span><span class="sxs-lookup"><span data-stu-id="46d7c-115">This simplistic function takes the results of **Foo** and passes it to **Bar**.</span></span> <span data-ttu-id="46d7c-116">Let's assume we need to change the return value of **Foo** from `bool` to `int` to support a wider variety of result values.</span><span class="sxs-lookup"><span data-stu-id="46d7c-116">Let's assume we need to change the return value of **Foo** from `bool` to `int` to support a wider variety of result values.</span></span> <span data-ttu-id="46d7c-117">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="46d7c-117">The result looks like this:</span></span>

```csharp
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    int result = await context.CallActivityAsync<int>("Foo");
    await context.CallActivityAsync("Bar", result);
}
```

<span data-ttu-id="46d7c-118">This change works fine for all new instances of the orchestrator function but breaks any in-flight instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-118">This change works fine for all new instances of the orchestrator function but breaks any in-flight instances.</span></span> <span data-ttu-id="46d7c-119">For example, consider the case where an orchestration instance calls **Foo**, gets back a boolean value and then checkpoints.</span><span class="sxs-lookup"><span data-stu-id="46d7c-119">For example, consider the case where an orchestration instance calls **Foo**, gets back a boolean value and then checkpoints.</span></span> <span data-ttu-id="46d7c-120">If the signature change is deployed at this point, the checkpointed instance will fail immediately when it resumes and replays the call to `context.CallActivityAsync<int>("Foo")`.</span><span class="sxs-lookup"><span data-stu-id="46d7c-120">If the signature change is deployed at this point, the checkpointed instance will fail immediately when it resumes and replays the call to `context.CallActivityAsync<int>("Foo")`.</span></span> <span data-ttu-id="46d7c-121">This is because the result in the history table is `bool` but the new code tries to deserialize it into `int`.</span><span class="sxs-lookup"><span data-stu-id="46d7c-121">This is because the result in the history table is `bool` but the new code tries to deserialize it into `int`.</span></span>

<span data-ttu-id="46d7c-122">This is just one of many different ways that a signature change can break existing instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-122">This is just one of many different ways that a signature change can break existing instances.</span></span> <span data-ttu-id="46d7c-123">In general, if an orchestrator needs to change the way it calls a function, then the change is likely to be problematic.</span><span class="sxs-lookup"><span data-stu-id="46d7c-123">In general, if an orchestrator needs to change the way it calls a function, then the change is likely to be problematic.</span></span>

### <a name="changing-orchestrator-logic"></a><span data-ttu-id="46d7c-124">Changing orchestrator logic</span><span class="sxs-lookup"><span data-stu-id="46d7c-124">Changing orchestrator logic</span></span>

<span data-ttu-id="46d7c-125">The other class of versioning problems come from changing the orchestrator function code in a way that confuses the replay logic for in-flight instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-125">The other class of versioning problems come from changing the orchestrator function code in a way that confuses the replay logic for in-flight instances.</span></span>

<span data-ttu-id="46d7c-126">Consider the following orchestrator function:</span><span class="sxs-lookup"><span data-stu-id="46d7c-126">Consider the following orchestrator function:</span></span>

```csharp
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    bool result = await context.CallActivityAsync<bool>("Foo");
    await context.CallActivityAsync("Bar", result);
}
```

<span data-ttu-id="46d7c-127">Now let's assume you want to make a seemingly innocent change to add another function call.</span><span class="sxs-lookup"><span data-stu-id="46d7c-127">Now let's assume you want to make a seemingly innocent change to add another function call.</span></span>

```csharp
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    bool result = await context.CallActivityAsync<bool>("Foo");
    if (result)
    {
        await context.CallActivityAsync("SendNotification");
    }

    await context.CallActivityAsync("Bar", result);
}
```

<span data-ttu-id="46d7c-128">This change adds a new function call to **SendNotification** between **Foo** and **Bar**.</span><span class="sxs-lookup"><span data-stu-id="46d7c-128">This change adds a new function call to **SendNotification** between **Foo** and **Bar**.</span></span> <span data-ttu-id="46d7c-129">There are no signature changes.</span><span class="sxs-lookup"><span data-stu-id="46d7c-129">There are no signature changes.</span></span> <span data-ttu-id="46d7c-130">The problem arises when an existing instance resumes from the call to **Bar**.</span><span class="sxs-lookup"><span data-stu-id="46d7c-130">The problem arises when an existing instance resumes from the call to **Bar**.</span></span> <span data-ttu-id="46d7c-131">During replay, if the original call to **Foo** returned `true`, then the orchestrator replay will call into **SendNotification** which is not in its execution history.</span><span class="sxs-lookup"><span data-stu-id="46d7c-131">During replay, if the original call to **Foo** returned `true`, then the orchestrator replay will call into **SendNotification** which is not in its execution history.</span></span> <span data-ttu-id="46d7c-132">As a result, the Durable Task Framework fails with a `NonDeterministicOrchestrationException` because it encountered a call to **SendNotification** when it expected to see a call to **Bar**.</span><span class="sxs-lookup"><span data-stu-id="46d7c-132">As a result, the Durable Task Framework fails with a `NonDeterministicOrchestrationException` because it encountered a call to **SendNotification** when it expected to see a call to **Bar**.</span></span>

## <a name="mitigation-strategies"></a><span data-ttu-id="46d7c-133">Mitigation strategies</span><span class="sxs-lookup"><span data-stu-id="46d7c-133">Mitigation strategies</span></span>

<span data-ttu-id="46d7c-134">Here are some of the strategies for dealing with versioning challenges:</span><span class="sxs-lookup"><span data-stu-id="46d7c-134">Here are some of the strategies for dealing with versioning challenges:</span></span>

* <span data-ttu-id="46d7c-135">Do nothing</span><span class="sxs-lookup"><span data-stu-id="46d7c-135">Do nothing</span></span>
* <span data-ttu-id="46d7c-136">Stop all in-flight instances</span><span class="sxs-lookup"><span data-stu-id="46d7c-136">Stop all in-flight instances</span></span>
* <span data-ttu-id="46d7c-137">Side-by-side deployments</span><span class="sxs-lookup"><span data-stu-id="46d7c-137">Side-by-side deployments</span></span>

### <a name="do-nothing"></a><span data-ttu-id="46d7c-138">Do nothing</span><span class="sxs-lookup"><span data-stu-id="46d7c-138">Do nothing</span></span>

<span data-ttu-id="46d7c-139">The easiest way to handle a breaking change is to let in-flight orchestration instances fail.</span><span class="sxs-lookup"><span data-stu-id="46d7c-139">The easiest way to handle a breaking change is to let in-flight orchestration instances fail.</span></span> <span data-ttu-id="46d7c-140">New instances successfully run the changed code.</span><span class="sxs-lookup"><span data-stu-id="46d7c-140">New instances successfully run the changed code.</span></span>

<span data-ttu-id="46d7c-141">Whether this is a problem depends on the importance of your in-flight instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-141">Whether this is a problem depends on the importance of your in-flight instances.</span></span> <span data-ttu-id="46d7c-142">If you are in active development and don't care about in-flight instances, this might be good enough.</span><span class="sxs-lookup"><span data-stu-id="46d7c-142">If you are in active development and don't care about in-flight instances, this might be good enough.</span></span> <span data-ttu-id="46d7c-143">However, you will need to deal with exceptions and errors in your diagnostics pipeline.</span><span class="sxs-lookup"><span data-stu-id="46d7c-143">However, you will need to deal with exceptions and errors in your diagnostics pipeline.</span></span> <span data-ttu-id="46d7c-144">If you want to avoid those things, consider the other versioning options.</span><span class="sxs-lookup"><span data-stu-id="46d7c-144">If you want to avoid those things, consider the other versioning options.</span></span>

### <a name="stop-all-in-flight-instances"></a><span data-ttu-id="46d7c-145">Stop all in-flight instances</span><span class="sxs-lookup"><span data-stu-id="46d7c-145">Stop all in-flight instances</span></span>

<span data-ttu-id="46d7c-146">Another option is to stop all in-flight instances.</span><span class="sxs-lookup"><span data-stu-id="46d7c-146">Another option is to stop all in-flight instances.</span></span> <span data-ttu-id="46d7c-147">This can be done by clearing the contents of the internal **control-queue** and **workitem-queue** queues.</span><span class="sxs-lookup"><span data-stu-id="46d7c-147">This can be done by clearing the contents of the internal **control-queue** and **workitem-queue** queues.</span></span> <span data-ttu-id="46d7c-148">The instances will be forever stuck where they are, but they will not clutter your telemetry with failure messages.</span><span class="sxs-lookup"><span data-stu-id="46d7c-148">The instances will be forever stuck where they are, but they will not clutter your telemetry with failure messages.</span></span> <span data-ttu-id="46d7c-149">This is ideal in rapid prototype development.</span><span class="sxs-lookup"><span data-stu-id="46d7c-149">This is ideal in rapid prototype development.</span></span>

> [!WARNING]
> <span data-ttu-id="46d7c-150">The details of these queues may change over time, so don't rely on this technique for production workloads.</span><span class="sxs-lookup"><span data-stu-id="46d7c-150">The details of these queues may change over time, so don't rely on this technique for production workloads.</span></span>

### <a name="side-by-side-deployments"></a><span data-ttu-id="46d7c-151">Side-by-side deployments</span><span class="sxs-lookup"><span data-stu-id="46d7c-151">Side-by-side deployments</span></span>

<span data-ttu-id="46d7c-152">The most fail-proof way to ensure that breaking changes are deployed safely is by deploying them side-by-side with your older versions.</span><span class="sxs-lookup"><span data-stu-id="46d7c-152">The most fail-proof way to ensure that breaking changes are deployed safely is by deploying them side-by-side with your older versions.</span></span> <span data-ttu-id="46d7c-153">This can be done using any of the following techniques:</span><span class="sxs-lookup"><span data-stu-id="46d7c-153">This can be done using any of the following techniques:</span></span>

* <span data-ttu-id="46d7c-154">Deploy all the updates as entirely new functions (new names).</span><span class="sxs-lookup"><span data-stu-id="46d7c-154">Deploy all the updates as entirely new functions (new names).</span></span>
* <span data-ttu-id="46d7c-155">Deploy all the updates as a new function app with a different storage account.</span><span class="sxs-lookup"><span data-stu-id="46d7c-155">Deploy all the updates as a new function app with a different storage account.</span></span>
* <span data-ttu-id="46d7c-156">Deploy a new copy of the function app but with an updated `TaskHub` name.</span><span class="sxs-lookup"><span data-stu-id="46d7c-156">Deploy a new copy of the function app but with an updated `TaskHub` name.</span></span> <span data-ttu-id="46d7c-157">This is the recommended technique.</span><span class="sxs-lookup"><span data-stu-id="46d7c-157">This is the recommended technique.</span></span>

### <a name="how-to-change-task-hub-name"></a><span data-ttu-id="46d7c-158">How to change task hub name</span><span class="sxs-lookup"><span data-stu-id="46d7c-158">How to change task hub name</span></span>

<span data-ttu-id="46d7c-159">The task hub can be configured in the *host.json* file as follows:</span><span class="sxs-lookup"><span data-stu-id="46d7c-159">The task hub can be configured in the *host.json* file as follows:</span></span>

```json
{
    "durableTask": {
        "HubName": "MyTaskHubV2"
    }
}
```

<span data-ttu-id="46d7c-160">The default value is `DurableFunctionsHub`.</span><span class="sxs-lookup"><span data-stu-id="46d7c-160">The default value is `DurableFunctionsHub`.</span></span>

<span data-ttu-id="46d7c-161">All Azure Storage entities are named based on the `HubName` configuration value.</span><span class="sxs-lookup"><span data-stu-id="46d7c-161">All Azure Storage entities are named based on the `HubName` configuration value.</span></span> <span data-ttu-id="46d7c-162">By giving the task hub a new name, you ensure that separate queues and history table are created for the new version of your application.</span><span class="sxs-lookup"><span data-stu-id="46d7c-162">By giving the task hub a new name, you ensure that separate queues and history table are created for the new version of your application.</span></span>

<span data-ttu-id="46d7c-163">We recommend that you deploy the new version of the function app to a new [Deployment Slot](https://blogs.msdn.microsoft.com/appserviceteam/2017/06/13/deployment-slots-preview-for-azure-functions/).</span><span class="sxs-lookup"><span data-stu-id="46d7c-163">We recommend that you deploy the new version of the function app to a new [Deployment Slot](https://blogs.msdn.microsoft.com/appserviceteam/2017/06/13/deployment-slots-preview-for-azure-functions/).</span></span> <span data-ttu-id="46d7c-164">Deployment slots allow you to run multiple copies of your function app side-by-side with only one of them as the active *production* slot.</span><span class="sxs-lookup"><span data-stu-id="46d7c-164">Deployment slots allow you to run multiple copies of your function app side-by-side with only one of them as the active *production* slot.</span></span> <span data-ttu-id="46d7c-165">When you are ready to expose the new orchestration logic to your existing infrastructure, it can be as simple as swapping the new version into the production slot.</span><span class="sxs-lookup"><span data-stu-id="46d7c-165">When you are ready to expose the new orchestration logic to your existing infrastructure, it can be as simple as swapping the new version into the production slot.</span></span>

> [!NOTE]
> <span data-ttu-id="46d7c-166">This strategy works best when you use HTTP and webhook triggers for orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="46d7c-166">This strategy works best when you use HTTP and webhook triggers for orchestrator functions.</span></span> <span data-ttu-id="46d7c-167">For non-HTTP triggers, such as queues or Event Hubs, the trigger definition should derive from an app setting that gets updated as part of the swap operation.</span><span class="sxs-lookup"><span data-stu-id="46d7c-167">For non-HTTP triggers, such as queues or Event Hubs, the trigger definition should derive from an app setting that gets updated as part of the swap operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d7c-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="46d7c-168">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46d7c-169">Learn how to handle performance and scale issues</span><span class="sxs-lookup"><span data-stu-id="46d7c-169">Learn how to handle performance and scale issues</span></span>](durable-functions-perf-and-scale.md)
