---
title: Overview of function types and features for Durable Functions  - Azure
description: Learn the types of functions and roles that allow for function-to-function communication as part of a durable function orchestration.
services: functions
author: jeffhollan
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 07/04/2018
ms.author: azfuncdf
ms.openlocfilehash: 24889765369a2af7d87ddb0fdc8f7c9f91ac66fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968134"
---
# <a name="overview-of-function-types-and-features-for-durable-functions-azure-functions"></a><span data-ttu-id="876b2-103">Overview of function types and features for Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="876b2-103">Overview of function types and features for Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="876b2-104">Azure Durable Functions provides stateful orchestration of function execution.</span><span class="sxs-lookup"><span data-stu-id="876b2-104">Azure Durable Functions provides stateful orchestration of function execution.</span></span>  <span data-ttu-id="876b2-105">A durable function is a solution made up of different Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="876b2-105">A durable function is a solution made up of different Azure Functions.</span></span>  <span data-ttu-id="876b2-106">Each of these functions can play different roles as part of an orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-106">Each of these functions can play different roles as part of an orchestration.</span></span>  <span data-ttu-id="876b2-107">The following document provides an overview of the types of functions involved in a durable function orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-107">The following document provides an overview of the types of functions involved in a durable function orchestration.</span></span>  <span data-ttu-id="876b2-108">It also includes some common patterns in connecting functions together.</span><span class="sxs-lookup"><span data-stu-id="876b2-108">It also includes some common patterns in connecting functions together.</span></span>  

![Types of durable functions][1]  

## <a name="types-of-functions"></a><span data-ttu-id="876b2-110">Types of functions</span><span class="sxs-lookup"><span data-stu-id="876b2-110">Types of functions</span></span>

### <a name="activity-functions"></a><span data-ttu-id="876b2-111">Activity functions</span><span class="sxs-lookup"><span data-stu-id="876b2-111">Activity functions</span></span>

<span data-ttu-id="876b2-112">Activity functions are the basic unit of work in a durable orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-112">Activity functions are the basic unit of work in a durable orchestration.</span></span>  <span data-ttu-id="876b2-113">Activity functions are the functions and tasks being orchestrated in the process.</span><span class="sxs-lookup"><span data-stu-id="876b2-113">Activity functions are the functions and tasks being orchestrated in the process.</span></span>  <span data-ttu-id="876b2-114">For example, you may create a durable function to process an order - check the inventory, charge the customer, and create a shipment.</span><span class="sxs-lookup"><span data-stu-id="876b2-114">For example, you may create a durable function to process an order - check the inventory, charge the customer, and create a shipment.</span></span>  <span data-ttu-id="876b2-115">Each one of those tasks would be an activity function.</span><span class="sxs-lookup"><span data-stu-id="876b2-115">Each one of those tasks would be an activity function.</span></span>  <span data-ttu-id="876b2-116">Activity functions don't have any restrictions in the type of work you can do in them.</span><span class="sxs-lookup"><span data-stu-id="876b2-116">Activity functions don't have any restrictions in the type of work you can do in them.</span></span>  <span data-ttu-id="876b2-117">They can be written in any language supported by Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="876b2-117">They can be written in any language supported by Azure Functions.</span></span>  <span data-ttu-id="876b2-118">The durable task framework guarantees that each called activity function will be executed at least once during an orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-118">The durable task framework guarantees that each called activity function will be executed at least once during an orchestration.</span></span>

<span data-ttu-id="876b2-119">An activity function must be triggered by an [activity trigger](durable-functions-bindings.md#activity-triggers).</span><span class="sxs-lookup"><span data-stu-id="876b2-119">An activity function must be triggered by an [activity trigger](durable-functions-bindings.md#activity-triggers).</span></span>  <span data-ttu-id="876b2-120">This function will receive a [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) as a parameter.</span><span class="sxs-lookup"><span data-stu-id="876b2-120">This function will receive a [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) as a parameter.</span></span> <span data-ttu-id="876b2-121">You can also bind the trigger to any other object to pass in inputs to the function.</span><span class="sxs-lookup"><span data-stu-id="876b2-121">You can also bind the trigger to any other object to pass in inputs to the function.</span></span>  <span data-ttu-id="876b2-122">Your activity function can also return values back to the orchestrator.</span><span class="sxs-lookup"><span data-stu-id="876b2-122">Your activity function can also return values back to the orchestrator.</span></span>  <span data-ttu-id="876b2-123">If sending or returning many values from an activity function, you can [leverage tuples or arrays](durable-functions-bindings.md#passing-multiple-parameters).</span><span class="sxs-lookup"><span data-stu-id="876b2-123">If sending or returning many values from an activity function, you can [leverage tuples or arrays](durable-functions-bindings.md#passing-multiple-parameters).</span></span>  <span data-ttu-id="876b2-124">Activity functions can only be triggered from an orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="876b2-124">Activity functions can only be triggered from an orchestration instance.</span></span>  <span data-ttu-id="876b2-125">While some code may be shared between an activity function and another function (like an HTTP triggered function), each function can only have one trigger.</span><span class="sxs-lookup"><span data-stu-id="876b2-125">While some code may be shared between an activity function and another function (like an HTTP triggered function), each function can only have one trigger.</span></span>

<span data-ttu-id="876b2-126">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#activity-triggers).</span><span class="sxs-lookup"><span data-stu-id="876b2-126">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#activity-triggers).</span></span>

### <a name="orchestrator-functions"></a><span data-ttu-id="876b2-127">Orchestrator functions</span><span class="sxs-lookup"><span data-stu-id="876b2-127">Orchestrator functions</span></span>

<span data-ttu-id="876b2-128">Orchestrator functions are the heart of a durable function.</span><span class="sxs-lookup"><span data-stu-id="876b2-128">Orchestrator functions are the heart of a durable function.</span></span>  <span data-ttu-id="876b2-129">Orchestrator functions describe the way and order actions are executed.</span><span class="sxs-lookup"><span data-stu-id="876b2-129">Orchestrator functions describe the way and order actions are executed.</span></span>  <span data-ttu-id="876b2-130">Orchestrator functions describe the orchestration in code (C# or JavaScript) as shown in the [durable functions overview](durable-functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="876b2-130">Orchestrator functions describe the orchestration in code (C# or JavaScript) as shown in the [durable functions overview](durable-functions-overview.md).</span></span>  <span data-ttu-id="876b2-131">An orchestration can have many different types of actions, like [activity Functions](#activity-functions), [sub-orchestrations](#sub-orchestrations), [waiting for external events](#external-events), and [timers](#durable-timers).</span><span class="sxs-lookup"><span data-stu-id="876b2-131">An orchestration can have many different types of actions, like [activity Functions](#activity-functions), [sub-orchestrations](#sub-orchestrations), [waiting for external events](#external-events), and [timers](#durable-timers).</span></span>  

<span data-ttu-id="876b2-132">An orchestrator function must be triggered by an [orchestration trigger](durable-functions-bindings.md#orchestration-triggers).</span><span class="sxs-lookup"><span data-stu-id="876b2-132">An orchestrator function must be triggered by an [orchestration trigger](durable-functions-bindings.md#orchestration-triggers).</span></span>

<span data-ttu-id="876b2-133">An orchestrator is started by an [orchestrator client](#client-functions) which could itself be triggered from any source (HTTP, queues, event streams).</span><span class="sxs-lookup"><span data-stu-id="876b2-133">An orchestrator is started by an [orchestrator client](#client-functions) which could itself be triggered from any source (HTTP, queues, event streams).</span></span>  <span data-ttu-id="876b2-134">Each instance of an orchestration has an instance identifier, which can be auto-generated (recommended) or user-generated.</span><span class="sxs-lookup"><span data-stu-id="876b2-134">Each instance of an orchestration has an instance identifier, which can be auto-generated (recommended) or user-generated.</span></span>  <span data-ttu-id="876b2-135">This identifier can be used to [manage instances](durable-functions-instance-management.md) of the orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-135">This identifier can be used to [manage instances](durable-functions-instance-management.md) of the orchestration.</span></span>

<span data-ttu-id="876b2-136">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#orchestration-triggers).</span><span class="sxs-lookup"><span data-stu-id="876b2-136">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#orchestration-triggers).</span></span>

### <a name="client-functions"></a><span data-ttu-id="876b2-137">Client functions</span><span class="sxs-lookup"><span data-stu-id="876b2-137">Client functions</span></span>

<span data-ttu-id="876b2-138">Client functions are the triggered functions that will create new instances of an orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-138">Client functions are the triggered functions that will create new instances of an orchestration.</span></span>  <span data-ttu-id="876b2-139">They are the entry point for creating an instance of a durable orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-139">They are the entry point for creating an instance of a durable orchestration.</span></span>  <span data-ttu-id="876b2-140">Client functions can be triggered by any trigger (HTTP, queues, event streams, etc.) and written in any language supported by the app.</span><span class="sxs-lookup"><span data-stu-id="876b2-140">Client functions can be triggered by any trigger (HTTP, queues, event streams, etc.) and written in any language supported by the app.</span></span>  <span data-ttu-id="876b2-141">In addition to the trigger, client functions have an [orchestration client](durable-functions-bindings.md#orchestration-client) binding that allows them to create and manage durable orchestrations.</span><span class="sxs-lookup"><span data-stu-id="876b2-141">In addition to the trigger, client functions have an [orchestration client](durable-functions-bindings.md#orchestration-client) binding that allows them to create and manage durable orchestrations.</span></span>  <span data-ttu-id="876b2-142">The most basic example of a client function is an HTTP triggered function that starts an orchestrator function and returns a check status response as [shown in this following example](durable-functions-http-api.md#http-api-url-discovery).</span><span class="sxs-lookup"><span data-stu-id="876b2-142">The most basic example of a client function is an HTTP triggered function that starts an orchestrator function and returns a check status response as [shown in this following example](durable-functions-http-api.md#http-api-url-discovery).</span></span>

<span data-ttu-id="876b2-143">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#orchestration-client).</span><span class="sxs-lookup"><span data-stu-id="876b2-143">More information and examples can be found in the [Durable Functions binding article](durable-functions-bindings.md#orchestration-client).</span></span>

## <a name="features-and-patterns"></a><span data-ttu-id="876b2-144">Features and patterns</span><span class="sxs-lookup"><span data-stu-id="876b2-144">Features and patterns</span></span>

### <a name="sub-orchestrations"></a><span data-ttu-id="876b2-145">Sub-orchestrations</span><span class="sxs-lookup"><span data-stu-id="876b2-145">Sub-orchestrations</span></span>

<span data-ttu-id="876b2-146">In addition to calling activity functions, orchestrator functions can call other orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="876b2-146">In addition to calling activity functions, orchestrator functions can call other orchestrator functions.</span></span> <span data-ttu-id="876b2-147">For example, you can build a larger orchestration out of a library of orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="876b2-147">For example, you can build a larger orchestration out of a library of orchestrator functions.</span></span> <span data-ttu-id="876b2-148">Or you can run multiple instances of an orchestrator function in parallel.</span><span class="sxs-lookup"><span data-stu-id="876b2-148">Or you can run multiple instances of an orchestrator function in parallel.</span></span>

<span data-ttu-id="876b2-149">More information and examples can be found in the [sub-orchestration article](durable-functions-sub-orchestrations.md).</span><span class="sxs-lookup"><span data-stu-id="876b2-149">More information and examples can be found in the [sub-orchestration article](durable-functions-sub-orchestrations.md).</span></span>

### <a name="durable-timers"></a><span data-ttu-id="876b2-150">Durable timers</span><span class="sxs-lookup"><span data-stu-id="876b2-150">Durable timers</span></span>

<span data-ttu-id="876b2-151">[Durable Functions](durable-functions-overview.md) provides *durable timers* for use in orchestrator functions to implement delays or to set up timeouts on async actions.</span><span class="sxs-lookup"><span data-stu-id="876b2-151">[Durable Functions](durable-functions-overview.md) provides *durable timers* for use in orchestrator functions to implement delays or to set up timeouts on async actions.</span></span> <span data-ttu-id="876b2-152">Durable timers should be used in orchestrator functions instead of `Thread.Sleep` and `Task.Delay` (C#), or `setTimeout()` and `setInterval()` (JavaScript).</span><span class="sxs-lookup"><span data-stu-id="876b2-152">Durable timers should be used in orchestrator functions instead of `Thread.Sleep` and `Task.Delay` (C#), or `setTimeout()` and `setInterval()` (JavaScript).</span></span>

<span data-ttu-id="876b2-153">More information and examples of durable timers can be found in the [durable timers article](durable-functions-timers.md)</span><span class="sxs-lookup"><span data-stu-id="876b2-153">More information and examples of durable timers can be found in the [durable timers article](durable-functions-timers.md)</span></span>

### <a name="external-events"></a><span data-ttu-id="876b2-154">External events</span><span class="sxs-lookup"><span data-stu-id="876b2-154">External events</span></span>

<span data-ttu-id="876b2-155">Orchestrator functions can wait for external events to update an orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="876b2-155">Orchestrator functions can wait for external events to update an orchestration instance.</span></span> <span data-ttu-id="876b2-156">This feature of Durable Functions is often useful for handling human interaction or other external callbacks.</span><span class="sxs-lookup"><span data-stu-id="876b2-156">This feature of Durable Functions is often useful for handling human interaction or other external callbacks.</span></span>

<span data-ttu-id="876b2-157">More information and examples can be found in the [external events article](durable-functions-external-events.md).</span><span class="sxs-lookup"><span data-stu-id="876b2-157">More information and examples can be found in the [external events article](durable-functions-external-events.md).</span></span>

### <a name="error-handling"></a><span data-ttu-id="876b2-158">Error handling</span><span class="sxs-lookup"><span data-stu-id="876b2-158">Error handling</span></span>

<span data-ttu-id="876b2-159">Durable Function orchestrations are implemented in code and can use the error-handling features of the programming language.</span><span class="sxs-lookup"><span data-stu-id="876b2-159">Durable Function orchestrations are implemented in code and can use the error-handling features of the programming language.</span></span>  <span data-ttu-id="876b2-160">This means patterns like "try/catch" will work in your orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-160">This means patterns like "try/catch" will work in your orchestration.</span></span>  <span data-ttu-id="876b2-161">Durable functions also come with some built-in retry policies.</span><span class="sxs-lookup"><span data-stu-id="876b2-161">Durable functions also come with some built-in retry policies.</span></span>  <span data-ttu-id="876b2-162">An action can delay and retry activities automatically on exceptions.</span><span class="sxs-lookup"><span data-stu-id="876b2-162">An action can delay and retry activities automatically on exceptions.</span></span>  <span data-ttu-id="876b2-163">Retries allow you to handle transient exceptions without having to abandon the orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-163">Retries allow you to handle transient exceptions without having to abandon the orchestration.</span></span>

<span data-ttu-id="876b2-164">More information and examples can be found in the [error handling article](durable-functions-error-handling.md).</span><span class="sxs-lookup"><span data-stu-id="876b2-164">More information and examples can be found in the [error handling article](durable-functions-error-handling.md).</span></span>

### <a name="cross-function-app-communication"></a><span data-ttu-id="876b2-165">Cross-function app communication</span><span class="sxs-lookup"><span data-stu-id="876b2-165">Cross-function app communication</span></span>

<span data-ttu-id="876b2-166">While a durable orchestration generally lives within a context of a single function app, there are patterns to enable you to coordinate orchestrations across many function apps.</span><span class="sxs-lookup"><span data-stu-id="876b2-166">While a durable orchestration generally lives within a context of a single function app, there are patterns to enable you to coordinate orchestrations across many function apps.</span></span>  <span data-ttu-id="876b2-167">Even though cross-app communication may be happening over HTTP, using the durable framework for each activity means you can still maintain a durable process across two apps.</span><span class="sxs-lookup"><span data-stu-id="876b2-167">Even though cross-app communication may be happening over HTTP, using the durable framework for each activity means you can still maintain a durable process across two apps.</span></span>

<span data-ttu-id="876b2-168">An example of a cross-function app orchestration in C# is provided below.</span><span class="sxs-lookup"><span data-stu-id="876b2-168">An example of a cross-function app orchestration in C# is provided below.</span></span>  <span data-ttu-id="876b2-169">One activity will start the external orchestration.</span><span class="sxs-lookup"><span data-stu-id="876b2-169">One activity will start the external orchestration.</span></span> <span data-ttu-id="876b2-170">Another activity will then retrieve and return the status.</span><span class="sxs-lookup"><span data-stu-id="876b2-170">Another activity will then retrieve and return the status.</span></span>  <span data-ttu-id="876b2-171">The orchestrator will wait for the status to be complete before continuing.</span><span class="sxs-lookup"><span data-stu-id="876b2-171">The orchestrator will wait for the status to be complete before continuing.</span></span>

```csharp
[FunctionName("OrchestratorA")]
public static async Task RunRemoteOrchestrator(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    // Do some work...

    // Call a remote orchestration
    string statusUrl = await context.CallActivityAsync<string>(
        "StartRemoteOrchestration", "OrchestratorB");

    // Wait for the remote orchestration to complete
    while (true)
    {
        bool isComplete = await context.CallActivityAsync<bool>("CheckIsComplete", statusUrl);
        if (isComplete)
        {
            break;
        }

        await context.CreateTimer(context.CurrentUtcDateTime.AddMinutes(1), CancellationToken.None);
    }

    // B is done. Now go do more work...
}

[FunctionName("StartRemoteOrchestration")]
public static async Task<string> StartRemoteOrchestration([ActivityTrigger] string orchestratorName)
{
    using (var response = await HttpClient.PostAsync(
        $"https://appB.azurewebsites.net/orchestrations/{orchestratorName}",
        new StringContent("")))
    {
        string statusUrl = await response.Content.ReadAsAsync<string>();
        return statusUrl;
    }
}

[FunctionName("CheckIsComplete")]
public static async Task<bool> CheckIsComplete([ActivityTrigger] string statusUrl)
{
    using (var response = await HttpClient.GetAsync(statusUrl))
    {
        // 200 = Complete, 202 = Running
        return response.StatusCode == HttpStatusCode.OK;
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="876b2-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="876b2-172">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="876b2-173">Continue reading Durable Functions documentation</span><span class="sxs-lookup"><span data-stu-id="876b2-173">Continue reading Durable Functions documentation</span></span>](durable-functions-bindings.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="876b2-174">Install the Durable Functions extension and samples</span><span class="sxs-lookup"><span data-stu-id="876b2-174">Install the Durable Functions extension and samples</span></span>](durable-functions-install.md)

<!-- Media references -->
[1]: media/durable-functions-types-features-overview/durable-concepts.png
