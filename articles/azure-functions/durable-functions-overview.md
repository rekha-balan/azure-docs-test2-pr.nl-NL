---
title: Durable Functions Overview - Azure
description: Introduction to the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: azfuncdf
ms.openlocfilehash: 1d6160f8c66fd749942be581cb2992977da82911
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865242"
---
# <a name="durable-functions-overview"></a><span data-ttu-id="c156a-103">Durable Functions overview</span><span class="sxs-lookup"><span data-stu-id="c156a-103">Durable Functions overview</span></span>

<span data-ttu-id="c156a-104">*Durable Functions* is an extension of [Azure Functions](functions-overview.md) and [Azure WebJobs](../app-service/web-sites-create-web-jobs.md) that lets you write stateful functions in a serverless environment.</span><span class="sxs-lookup"><span data-stu-id="c156a-104">*Durable Functions* is an extension of [Azure Functions](functions-overview.md) and [Azure WebJobs](../app-service/web-sites-create-web-jobs.md) that lets you write stateful functions in a serverless environment.</span></span> <span data-ttu-id="c156a-105">The extension manages state, checkpoints, and restarts for you.</span><span class="sxs-lookup"><span data-stu-id="c156a-105">The extension manages state, checkpoints, and restarts for you.</span></span>

<span data-ttu-id="c156a-106">The extension lets you define stateful workflows in a new type of function called an [*orchestrator function*](durable-functions-types-features-overview.md#orchestrator-functions).</span><span class="sxs-lookup"><span data-stu-id="c156a-106">The extension lets you define stateful workflows in a new type of function called an [*orchestrator function*](durable-functions-types-features-overview.md#orchestrator-functions).</span></span> <span data-ttu-id="c156a-107">Here are some of the advantages of orchestrator functions:</span><span class="sxs-lookup"><span data-stu-id="c156a-107">Here are some of the advantages of orchestrator functions:</span></span>

* <span data-ttu-id="c156a-108">They define workflows in code.</span><span class="sxs-lookup"><span data-stu-id="c156a-108">They define workflows in code.</span></span> <span data-ttu-id="c156a-109">No JSON schemas or designers are needed.</span><span class="sxs-lookup"><span data-stu-id="c156a-109">No JSON schemas or designers are needed.</span></span>
* <span data-ttu-id="c156a-110">They can call other functions synchronously and asynchronously.</span><span class="sxs-lookup"><span data-stu-id="c156a-110">They can call other functions synchronously and asynchronously.</span></span> <span data-ttu-id="c156a-111">Output from called functions can be saved to local variables.</span><span class="sxs-lookup"><span data-stu-id="c156a-111">Output from called functions can be saved to local variables.</span></span>
* <span data-ttu-id="c156a-112">They automatically checkpoint their progress whenever the function awaits.</span><span class="sxs-lookup"><span data-stu-id="c156a-112">They automatically checkpoint their progress whenever the function awaits.</span></span> <span data-ttu-id="c156a-113">Local state is never lost if the process recycles or the VM reboots.</span><span class="sxs-lookup"><span data-stu-id="c156a-113">Local state is never lost if the process recycles or the VM reboots.</span></span>

> [!NOTE]
> <span data-ttu-id="c156a-114">Durable Functions is an advanced extension for Azure Functions that is not appropriate for all applications.</span><span class="sxs-lookup"><span data-stu-id="c156a-114">Durable Functions is an advanced extension for Azure Functions that is not appropriate for all applications.</span></span> <span data-ttu-id="c156a-115">The rest of this article assumes that you have a strong familiarity with [Azure Functions](functions-overview.md) concepts and the challenges involved in serverless application development.</span><span class="sxs-lookup"><span data-stu-id="c156a-115">The rest of this article assumes that you have a strong familiarity with [Azure Functions](functions-overview.md) concepts and the challenges involved in serverless application development.</span></span>

<span data-ttu-id="c156a-116">The primary use case for Durable Functions is simplifying complex, stateful coordination problems in serverless applications.</span><span class="sxs-lookup"><span data-stu-id="c156a-116">The primary use case for Durable Functions is simplifying complex, stateful coordination problems in serverless applications.</span></span> <span data-ttu-id="c156a-117">The following sections describe some typical application patterns that can benefit from Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="c156a-117">The following sections describe some typical application patterns that can benefit from Durable Functions.</span></span>

## <a name="pattern-1-function-chaining"></a><span data-ttu-id="c156a-118">Pattern #1: Function chaining</span><span class="sxs-lookup"><span data-stu-id="c156a-118">Pattern #1: Function chaining</span></span>

<span data-ttu-id="c156a-119">*Function chaining* refers to the pattern of executing a sequence of functions in a particular order.</span><span class="sxs-lookup"><span data-stu-id="c156a-119">*Function chaining* refers to the pattern of executing a sequence of functions in a particular order.</span></span> <span data-ttu-id="c156a-120">Often the output of one function needs to be applied to the input of another function.</span><span class="sxs-lookup"><span data-stu-id="c156a-120">Often the output of one function needs to be applied to the input of another function.</span></span>

![Function chaining diagram](media/durable-functions-overview/function-chaining.png)

<span data-ttu-id="c156a-122">Durable Functions allows you to implement this pattern concisely in code.</span><span class="sxs-lookup"><span data-stu-id="c156a-122">Durable Functions allows you to implement this pattern concisely in code.</span></span>

#### <a name="c-script"></a><span data-ttu-id="c156a-123">C# script</span><span class="sxs-lookup"><span data-stu-id="c156a-123">C# script</span></span>

```cs
public static async Task<object> Run(DurableOrchestrationContext ctx)
{
    try
    {
        var x = await ctx.CallActivityAsync<object>("F1");
        var y = await ctx.CallActivityAsync<object>("F2", x);
        var z = await ctx.CallActivityAsync<object>("F3", y);
        return  await ctx.CallActivityAsync<object>("F4", z);
    }
    catch (Exception)
    {
        // error handling/compensation goes here
    }
}
```
> [!NOTE]
> <span data-ttu-id="c156a-124">There are subtle differences while writing a precompiled durable function in C# vs the C# script sample shown before.</span><span class="sxs-lookup"><span data-stu-id="c156a-124">There are subtle differences while writing a precompiled durable function in C# vs the C# script sample shown before.</span></span> <span data-ttu-id="c156a-125">A C# precompiled function would require durable parameters to be decorated with respective attributes.</span><span class="sxs-lookup"><span data-stu-id="c156a-125">A C# precompiled function would require durable parameters to be decorated with respective attributes.</span></span> <span data-ttu-id="c156a-126">An example is `[OrchestrationTrigger]` attribute for `DurableOrchestrationContext` parameter.</span><span class="sxs-lookup"><span data-stu-id="c156a-126">An example is `[OrchestrationTrigger]` attribute for `DurableOrchestrationContext` parameter.</span></span> <span data-ttu-id="c156a-127">If the parameters are not properly decorated, the runtime would not be able to inject the variables to the function and would give error.</span><span class="sxs-lookup"><span data-stu-id="c156a-127">If the parameters are not properly decorated, the runtime would not be able to inject the variables to the function and would give error.</span></span> <span data-ttu-id="c156a-128">Please visit [sample](https://github.com/Azure/azure-functions-durable-extension/blob/master/samples) for more examples.</span><span class="sxs-lookup"><span data-stu-id="c156a-128">Please visit [sample](https://github.com/Azure/azure-functions-durable-extension/blob/master/samples) for more examples.</span></span>

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="c156a-129">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="c156a-129">JavaScript (Functions v2 only)</span></span>

```js
const df = require("durable-functions");

module.exports = df(function*(ctx) {
    const x = yield ctx.df.callActivityAsync("F1");
    const y = yield ctx.df.callActivityAsync("F2", x);
    const z = yield ctx.df.callActivityAsync("F3", y);
    return yield ctx.df.callActivityAsync("F4", z);
});
```

<span data-ttu-id="c156a-130">The values "F1", "F2", "F3", and "F4" are the names of other functions in the function app.</span><span class="sxs-lookup"><span data-stu-id="c156a-130">The values "F1", "F2", "F3", and "F4" are the names of other functions in the function app.</span></span> <span data-ttu-id="c156a-131">Control flow is implemented using normal imperative coding constructs.</span><span class="sxs-lookup"><span data-stu-id="c156a-131">Control flow is implemented using normal imperative coding constructs.</span></span> <span data-ttu-id="c156a-132">That is, code executes top-down and can involve existing language control flow semantics, like conditionals, and loops.</span><span class="sxs-lookup"><span data-stu-id="c156a-132">That is, code executes top-down and can involve existing language control flow semantics, like conditionals, and loops.</span></span>  <span data-ttu-id="c156a-133">Error handling logic can be included in try/catch/finally blocks.</span><span class="sxs-lookup"><span data-stu-id="c156a-133">Error handling logic can be included in try/catch/finally blocks.</span></span>

<span data-ttu-id="c156a-134">The `ctx` parameter ([DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html)) provides methods for invoking other functions by name, passing parameters, and returning function output.</span><span class="sxs-lookup"><span data-stu-id="c156a-134">The `ctx` parameter ([DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html)) provides methods for invoking other functions by name, passing parameters, and returning function output.</span></span> <span data-ttu-id="c156a-135">Each time the code calls `await`, the Durable Functions framework *checkpoints* the progress of the current function instance.</span><span class="sxs-lookup"><span data-stu-id="c156a-135">Each time the code calls `await`, the Durable Functions framework *checkpoints* the progress of the current function instance.</span></span> <span data-ttu-id="c156a-136">If the process or VM recycles midway through the execution, the function instance resumes from the previous `await` call.</span><span class="sxs-lookup"><span data-stu-id="c156a-136">If the process or VM recycles midway through the execution, the function instance resumes from the previous `await` call.</span></span> <span data-ttu-id="c156a-137">More on this restart behavior later.</span><span class="sxs-lookup"><span data-stu-id="c156a-137">More on this restart behavior later.</span></span>

## <a name="pattern-2-fan-outfan-in"></a><span data-ttu-id="c156a-138">Pattern #2: Fan-out/fan-in</span><span class="sxs-lookup"><span data-stu-id="c156a-138">Pattern #2: Fan-out/fan-in</span></span>

<span data-ttu-id="c156a-139">*Fan-out/fan-in* refers to the pattern of executing multiple functions in parallel, and then waiting for all to finish.</span><span class="sxs-lookup"><span data-stu-id="c156a-139">*Fan-out/fan-in* refers to the pattern of executing multiple functions in parallel, and then waiting for all to finish.</span></span>  <span data-ttu-id="c156a-140">Often some aggregation work is done on results returned from the functions.</span><span class="sxs-lookup"><span data-stu-id="c156a-140">Often some aggregation work is done on results returned from the functions.</span></span>

![Fan-out/fan-in diagram](media/durable-functions-overview/fan-out-fan-in.png)

<span data-ttu-id="c156a-142">With normal functions, fanning out can be done by having the function send multiple messages to a queue.</span><span class="sxs-lookup"><span data-stu-id="c156a-142">With normal functions, fanning out can be done by having the function send multiple messages to a queue.</span></span> <span data-ttu-id="c156a-143">However, fanning back in is much more challenging.</span><span class="sxs-lookup"><span data-stu-id="c156a-143">However, fanning back in is much more challenging.</span></span> <span data-ttu-id="c156a-144">You'd have to write code to track when the queue-triggered functions end and store function outputs.</span><span class="sxs-lookup"><span data-stu-id="c156a-144">You'd have to write code to track when the queue-triggered functions end and store function outputs.</span></span> <span data-ttu-id="c156a-145">The Durable Functions extension handles this pattern with relatively simple code.</span><span class="sxs-lookup"><span data-stu-id="c156a-145">The Durable Functions extension handles this pattern with relatively simple code.</span></span>

#### <a name="c-script"></a><span data-ttu-id="c156a-146">C# script</span><span class="sxs-lookup"><span data-stu-id="c156a-146">C# script</span></span>

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    var parallelTasks = new List<Task<int>>();
 
    // get a list of N work items to process in parallel
    object[] workBatch = await ctx.CallActivityAsync<object[]>("F1");
    for (int i = 0; i < workBatch.Length; i++)
    {
        Task<int> task = ctx.CallActivityAsync<int>("F2", workBatch[i]);
        parallelTasks.Add(task);
    }
 
    await Task.WhenAll(parallelTasks);
 
    // aggregate all N outputs and send result to F3
    int sum = parallelTasks.Sum(t => t.Result);
    await ctx.CallActivityAsync("F3", sum);
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="c156a-147">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="c156a-147">JavaScript (Functions v2 only)</span></span>

```js
const df = require("durable-functions");

module.exports = df(function*(ctx) {
    const parallelTasks = [];

    // get a list of N work items to process in parallel
    const workBatch = yield ctx.df.callActivityAsync("F1");
    for (let i = 0; i < workBatch.length; i++) {
        parallelTasks.push(ctx.df.callActivityAsync("F2", workBatch[i]));
    }

    yield ctx.df.task.all(parallelTasks);

    // aggregate all N outputs and send result to F3
    const sum = parallelTasks.reduce((prev, curr) => prev + curr, 0);
    yield ctx.df.callActivityAsync("F3", sum);
});
```

<span data-ttu-id="c156a-148">The fan-out work is distributed to multiple instances of function `F2`, and the work is tracked by using a dynamic list of tasks.</span><span class="sxs-lookup"><span data-stu-id="c156a-148">The fan-out work is distributed to multiple instances of function `F2`, and the work is tracked by using a dynamic list of tasks.</span></span> <span data-ttu-id="c156a-149">The .NET `Task.WhenAll` API is called to wait for all of the called functions to finish.</span><span class="sxs-lookup"><span data-stu-id="c156a-149">The .NET `Task.WhenAll` API is called to wait for all of the called functions to finish.</span></span> <span data-ttu-id="c156a-150">Then the `F2`function outputs are aggregated from the dynamic task list and passed on to the `F3` function.</span><span class="sxs-lookup"><span data-stu-id="c156a-150">Then the `F2`function outputs are aggregated from the dynamic task list and passed on to the `F3` function.</span></span>

<span data-ttu-id="c156a-151">The automatic checkpointing that happens at the `await` call on `Task.WhenAll` ensures that any crash or reboot midway through does not require a restart of any already completed tasks.</span><span class="sxs-lookup"><span data-stu-id="c156a-151">The automatic checkpointing that happens at the `await` call on `Task.WhenAll` ensures that any crash or reboot midway through does not require a restart of any already completed tasks.</span></span>

## <a name="pattern-3-async-http-apis"></a><span data-ttu-id="c156a-152">Pattern #3: Async HTTP APIs</span><span class="sxs-lookup"><span data-stu-id="c156a-152">Pattern #3: Async HTTP APIs</span></span>

<span data-ttu-id="c156a-153">The third pattern is all about the problem of coordinating the state of long-running operations with external clients.</span><span class="sxs-lookup"><span data-stu-id="c156a-153">The third pattern is all about the problem of coordinating the state of long-running operations with external clients.</span></span> <span data-ttu-id="c156a-154">A common way to implement this pattern is by having the long-running action triggered by an HTTP call, and then redirecting the client to a status endpoint that they can poll to learn when the operation completes.</span><span class="sxs-lookup"><span data-stu-id="c156a-154">A common way to implement this pattern is by having the long-running action triggered by an HTTP call, and then redirecting the client to a status endpoint that they can poll to learn when the operation completes.</span></span>

![HTTP API diagram](media/durable-functions-overview/async-http-api.png)

<span data-ttu-id="c156a-156">Durable Functions provides built-in APIs that simplify the code you write for interacting with long-running function executions.</span><span class="sxs-lookup"><span data-stu-id="c156a-156">Durable Functions provides built-in APIs that simplify the code you write for interacting with long-running function executions.</span></span> <span data-ttu-id="c156a-157">The [samples](durable-functions-install.md) show a simple REST command that can be used to start new orchestrator function instances.</span><span class="sxs-lookup"><span data-stu-id="c156a-157">The [samples](durable-functions-install.md) show a simple REST command that can be used to start new orchestrator function instances.</span></span> <span data-ttu-id="c156a-158">Once an instance is started, the extension exposes webhook HTTP APIs that query the orchestrator function status.</span><span class="sxs-lookup"><span data-stu-id="c156a-158">Once an instance is started, the extension exposes webhook HTTP APIs that query the orchestrator function status.</span></span> <span data-ttu-id="c156a-159">The following example shows the REST commands to start an orchestrator and to query its status.</span><span class="sxs-lookup"><span data-stu-id="c156a-159">The following example shows the REST commands to start an orchestrator and to query its status.</span></span> <span data-ttu-id="c156a-160">For clarity, some details are omitted from the example.</span><span class="sxs-lookup"><span data-stu-id="c156a-160">For clarity, some details are omitted from the example.</span></span>

```
> curl -X POST https://myfunc.azurewebsites.net/orchestrators/DoWork -H "Content-Length: 0" -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec

{"id":"b79baf67f717453ca9e86c5da21e03ec", ...}

> curl https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec

{"runtimeStatus":"Running","lastUpdatedTime":"2017-03-16T21:20:47Z", ...}

> curl https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 200 OK
Content-Length: 175
Content-Type: application/json

{"runtimeStatus":"Completed","lastUpdatedTime":"2017-03-16T21:20:57Z", ...}
```

<span data-ttu-id="c156a-161">Because the state is managed by the Durable Functions runtime, you don't have to implement your own status tracking mechanism.</span><span class="sxs-lookup"><span data-stu-id="c156a-161">Because the state is managed by the Durable Functions runtime, you don't have to implement your own status tracking mechanism.</span></span>

<span data-ttu-id="c156a-162">Even though the Durable Functions extension has built-in webhooks for managing long-running orchestrations, you can implement this pattern yourself using your own function triggers (such as HTTP, queue, or Event Hub) and the `orchestrationClient` binding.</span><span class="sxs-lookup"><span data-stu-id="c156a-162">Even though the Durable Functions extension has built-in webhooks for managing long-running orchestrations, you can implement this pattern yourself using your own function triggers (such as HTTP, queue, or Event Hub) and the `orchestrationClient` binding.</span></span> <span data-ttu-id="c156a-163">For example, you could use a queue message to trigger termination.</span><span class="sxs-lookup"><span data-stu-id="c156a-163">For example, you could use a queue message to trigger termination.</span></span>  <span data-ttu-id="c156a-164">Or you could use an HTTP trigger protected by an Azure Active Directory authentication policy instead of the built-in webhooks that use a generated key for authentication.</span><span class="sxs-lookup"><span data-stu-id="c156a-164">Or you could use an HTTP trigger protected by an Azure Active Directory authentication policy instead of the built-in webhooks that use a generated key for authentication.</span></span> 

```cs
// HTTP-triggered function to start a new orchestrator function instance.
public static async Task<HttpResponseMessage> Run(
    HttpRequestMessage req,
    DurableOrchestrationClient starter,
    string functionName,
    TraceWriter log)
{
    // Function name comes from the request URL.
    // Function input comes from the request content.
    dynamic eventData = await req.Content.ReadAsAsync<object>();
    string instanceId = await starter.StartNewAsync(functionName, eventData);
    
    log.Info($"Started orchestration with ID = '{instanceId}'.");
    
    return starter.CreateCheckStatusResponse(req, instanceId);
}
```

<span data-ttu-id="c156a-165">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) `starter` parameter is a value from the `orchestrationClient` output binding, which is part of the Durable Functions extension.</span><span class="sxs-lookup"><span data-stu-id="c156a-165">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) `starter` parameter is a value from the `orchestrationClient` output binding, which is part of the Durable Functions extension.</span></span> <span data-ttu-id="c156a-166">It provides methods for starting, sending events to, terminating, and querying for new or existing orchestrator function instances.</span><span class="sxs-lookup"><span data-stu-id="c156a-166">It provides methods for starting, sending events to, terminating, and querying for new or existing orchestrator function instances.</span></span> <span data-ttu-id="c156a-167">In the previous example, an HTTP triggered-function takes in a `functionName` value from the incoming URL and passes that value to [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_).</span><span class="sxs-lookup"><span data-stu-id="c156a-167">In the previous example, an HTTP triggered-function takes in a `functionName` value from the incoming URL and passes that value to [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_).</span></span> <span data-ttu-id="c156a-168">This binding API then returns a response that contains a `Location` header and additional information about the instance that can later be used to look up the status of the started instance or terminate it.</span><span class="sxs-lookup"><span data-stu-id="c156a-168">This binding API then returns a response that contains a `Location` header and additional information about the instance that can later be used to look up the status of the started instance or terminate it.</span></span>

## <a name="pattern-4-monitoring"></a><span data-ttu-id="c156a-169">Pattern #4: Monitoring</span><span class="sxs-lookup"><span data-stu-id="c156a-169">Pattern #4: Monitoring</span></span>

<span data-ttu-id="c156a-170">The monitor pattern refers to a flexible *recurring* process in a workflow - for example, polling until certain conditions are met.</span><span class="sxs-lookup"><span data-stu-id="c156a-170">The monitor pattern refers to a flexible *recurring* process in a workflow - for example, polling until certain conditions are met.</span></span> <span data-ttu-id="c156a-171">A regular timer-trigger can address a simple scenario, such as a periodic cleanup job, but its interval is static and managing instance lifetimes becomes complex.</span><span class="sxs-lookup"><span data-stu-id="c156a-171">A regular timer-trigger can address a simple scenario, such as a periodic cleanup job, but its interval is static and managing instance lifetimes becomes complex.</span></span> <span data-ttu-id="c156a-172">Durable Functions enables flexible recurrence intervals, task lifetime management, and the ability to create multiple monitor processes from a single orchestration.</span><span class="sxs-lookup"><span data-stu-id="c156a-172">Durable Functions enables flexible recurrence intervals, task lifetime management, and the ability to create multiple monitor processes from a single orchestration.</span></span>

<span data-ttu-id="c156a-173">An example would be reversing the earlier async HTTP API scenario.</span><span class="sxs-lookup"><span data-stu-id="c156a-173">An example would be reversing the earlier async HTTP API scenario.</span></span> <span data-ttu-id="c156a-174">Instead of exposing an endpoint for an external client to monitor a long-running operation, the long-running monitor consumes an external endpoint, waiting for some state change.</span><span class="sxs-lookup"><span data-stu-id="c156a-174">Instead of exposing an endpoint for an external client to monitor a long-running operation, the long-running monitor consumes an external endpoint, waiting for some state change.</span></span>

![Monitor diagram](media/durable-functions-overview/monitor.png)

<span data-ttu-id="c156a-176">Using Durable Functions, multiple monitors that observe arbitrary endpoints can be created in a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="c156a-176">Using Durable Functions, multiple monitors that observe arbitrary endpoints can be created in a few lines of code.</span></span> <span data-ttu-id="c156a-177">The monitors can end execution when some condition is met, or be terminated by the [DurableOrchestrationClient](durable-functions-instance-management.md), and their wait interval can be changed based on some condition (i.e. exponential backoff.) The following code implements a basic monitor.</span><span class="sxs-lookup"><span data-stu-id="c156a-177">The monitors can end execution when some condition is met, or be terminated by the [DurableOrchestrationClient](durable-functions-instance-management.md), and their wait interval can be changed based on some condition (i.e. exponential backoff.) The following code implements a basic monitor.</span></span>

#### <a name="c-script"></a><span data-ttu-id="c156a-178">C# script</span><span class="sxs-lookup"><span data-stu-id="c156a-178">C# script</span></span>

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    int jobId = ctx.GetInput<int>();
    int pollingInterval = GetPollingInterval();
    DateTime expiryTime = GetExpiryTime();
    
    while (ctx.CurrentUtcDateTime < expiryTime) 
    {
        var jobStatus = await ctx.CallActivityAsync<string>("GetJobStatus", jobId);
        if (jobStatus == "Completed")
        {
            // Perform action when condition met
            await ctx.CallActivityAsync("SendAlert", machineId);
            break;
        }

        // Orchestration will sleep until this time
        var nextCheck = ctx.CurrentUtcDateTime.AddSeconds(pollingInterval);
        await ctx.CreateTimer(nextCheck, CancellationToken.None);
    }

    // Perform further work here, or let the orchestration end
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="c156a-179">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="c156a-179">JavaScript (Functions v2 only)</span></span>

```js
const df = require("durable-functions");
const df = require("moment");

module.exports = df(function*(ctx) {
    const jobId = ctx.df.getInput();
    const pollingInternal = getPollingInterval();
    const expiryTime = getExpiryTime();

    while (moment.utc(ctx.df.currentUtcDateTime).isBefore(expiryTime)) {
        const jobStatus = yield ctx.df.callActivityAsync("GetJobStatus", jobId);
        if (jobStatus === "Completed") {
            // Perform action when condition met
            yield ctx.df.callActivityAsync("SendAlert", machineId);
            break;
        }

        // Orchestration will sleep until this time
        const nextCheck = moment.utc(ctx.df.currentUtcDateTime).add(pollingInterval, 's');
        yield ctx.df.createTimer(nextCheck.toDate());
    }

    // Perform further work here, or let the orchestration end
});
```

<span data-ttu-id="c156a-180">When a request is received, a new orchestration instance is created for that job ID.</span><span class="sxs-lookup"><span data-stu-id="c156a-180">When a request is received, a new orchestration instance is created for that job ID.</span></span> <span data-ttu-id="c156a-181">The instance polls a status until a condition is met and the loop is exited.</span><span class="sxs-lookup"><span data-stu-id="c156a-181">The instance polls a status until a condition is met and the loop is exited.</span></span> <span data-ttu-id="c156a-182">A durable timer is used to control the polling interval.</span><span class="sxs-lookup"><span data-stu-id="c156a-182">A durable timer is used to control the polling interval.</span></span> <span data-ttu-id="c156a-183">Further work can then be performed, or the orchestration can end.</span><span class="sxs-lookup"><span data-stu-id="c156a-183">Further work can then be performed, or the orchestration can end.</span></span> <span data-ttu-id="c156a-184">When the `ctx.CurrentUtcDateTime` exceeds the `expiryTime`, the monitor ends.</span><span class="sxs-lookup"><span data-stu-id="c156a-184">When the `ctx.CurrentUtcDateTime` exceeds the `expiryTime`, the monitor ends.</span></span>

## <a name="pattern-5-human-interaction"></a><span data-ttu-id="c156a-185">Pattern #5: Human interaction</span><span class="sxs-lookup"><span data-stu-id="c156a-185">Pattern #5: Human interaction</span></span>

<span data-ttu-id="c156a-186">Many processes involve some kind of human interaction.</span><span class="sxs-lookup"><span data-stu-id="c156a-186">Many processes involve some kind of human interaction.</span></span> <span data-ttu-id="c156a-187">The tricky thing about involving humans in an automated process is that people are not always as highly available and responsive as cloud services.</span><span class="sxs-lookup"><span data-stu-id="c156a-187">The tricky thing about involving humans in an automated process is that people are not always as highly available and responsive as cloud services.</span></span> <span data-ttu-id="c156a-188">Automated processes must allow for this, and they often do so by using timeouts and compensation logic.</span><span class="sxs-lookup"><span data-stu-id="c156a-188">Automated processes must allow for this, and they often do so by using timeouts and compensation logic.</span></span>

<span data-ttu-id="c156a-189">One example of a business process that involves human interaction is an approval process.</span><span class="sxs-lookup"><span data-stu-id="c156a-189">One example of a business process that involves human interaction is an approval process.</span></span> <span data-ttu-id="c156a-190">For example, approval from a manager might be required for an expense report that exceeds a certain amount.</span><span class="sxs-lookup"><span data-stu-id="c156a-190">For example, approval from a manager might be required for an expense report that exceeds a certain amount.</span></span> <span data-ttu-id="c156a-191">If the manager does not approve within 72 hours (maybe they went on vacation), an escalation process kicks in to get the approval from someone else (perhaps the manager's manager).</span><span class="sxs-lookup"><span data-stu-id="c156a-191">If the manager does not approve within 72 hours (maybe they went on vacation), an escalation process kicks in to get the approval from someone else (perhaps the manager's manager).</span></span>

![Human interaction diagram](media/durable-functions-overview/approval.png)

<span data-ttu-id="c156a-193">This pattern can be implemented using an orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="c156a-193">This pattern can be implemented using an orchestrator function.</span></span> <span data-ttu-id="c156a-194">The orchestrator would use a [durable timer](durable-functions-timers.md) to request approval and escalate in case of timeout.</span><span class="sxs-lookup"><span data-stu-id="c156a-194">The orchestrator would use a [durable timer](durable-functions-timers.md) to request approval and escalate in case of timeout.</span></span> <span data-ttu-id="c156a-195">It would wait for an [external event](durable-functions-external-events.md), which would be the notification generated by some human interaction.</span><span class="sxs-lookup"><span data-stu-id="c156a-195">It would wait for an [external event](durable-functions-external-events.md), which would be the notification generated by some human interaction.</span></span>

#### <a name="c-script"></a><span data-ttu-id="c156a-196">C# script</span><span class="sxs-lookup"><span data-stu-id="c156a-196">C# script</span></span>

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    await ctx.CallActivityAsync("RequestApproval");
    using (var timeoutCts = new CancellationTokenSource())
    {
        DateTime dueTime = ctx.CurrentUtcDateTime.AddHours(72);
        Task durableTimeout = ctx.CreateTimer(dueTime, timeoutCts.Token);

        Task<bool> approvalEvent = ctx.WaitForExternalEvent<bool>("ApprovalEvent");
        if (approvalEvent == await Task.WhenAny(approvalEvent, durableTimeout))
        {
            timeoutCts.Cancel();
            await ctx.CallActivityAsync("ProcessApproval", approvalEvent.Result);
        }
        else
        {
            await ctx.CallActivityAsync("Escalate");
        }
    }
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="c156a-197">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="c156a-197">JavaScript (Functions v2 only)</span></span>

```js
const df = require("durable-functions");
const df = require('moment');

module.exports = df(function*(ctx) {
    yield ctx.df.callActivityAsync("RequestApproval");

    const dueTime = moment.utc(ctx.df.currentUtcDateTime).add(72, 'h');
    const durableTimeout = ctx.df.createTimer(dueTime.toDate());

    const approvalEvent = ctx.df.waitForExternalEvent("ApprovalEvent");
    if (approvalEvent === yield ctx.df.Task.any([approvalEvent, durableTimeout])) {
        durableTimeout.cancel();
        yield ctx.df.callActivityAsync("ProcessApproval", approvalEvent.result);
    } else {
        yield ctx.df.callActivityAsync("Escalate");
    }
});
```

<span data-ttu-id="c156a-198">The durable timer is created by calling `ctx.CreateTimer`.</span><span class="sxs-lookup"><span data-stu-id="c156a-198">The durable timer is created by calling `ctx.CreateTimer`.</span></span> <span data-ttu-id="c156a-199">The notification is received by `ctx.WaitForExternalEvent`.</span><span class="sxs-lookup"><span data-stu-id="c156a-199">The notification is received by `ctx.WaitForExternalEvent`.</span></span> <span data-ttu-id="c156a-200">And `Task.WhenAny` is called to decide whether to escalate (timeout happens first) or process approval (approval is received before timeout).</span><span class="sxs-lookup"><span data-stu-id="c156a-200">And `Task.WhenAny` is called to decide whether to escalate (timeout happens first) or process approval (approval is received before timeout).</span></span>

<span data-ttu-id="c156a-201">An external client can deliver the event notification to a waiting orchestrator function using either the [built-in HTTP APIs](durable-functions-http-api.md#raise-event) or by using [DurableOrchestrationClient.RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_System_String_System_String_System_Object_) API from another function:</span><span class="sxs-lookup"><span data-stu-id="c156a-201">An external client can deliver the event notification to a waiting orchestrator function using either the [built-in HTTP APIs](durable-functions-http-api.md#raise-event) or by using [DurableOrchestrationClient.RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_System_String_System_String_System_Object_) API from another function:</span></span>

```csharp
public static async Task Run(string instanceId, DurableOrchestrationClient client)
{
    bool isApproved = true;
    await client.RaiseEventAsync(instanceId, "ApprovalEvent", isApproved);
}
```

## <a name="the-technology"></a><span data-ttu-id="c156a-202">The technology</span><span class="sxs-lookup"><span data-stu-id="c156a-202">The technology</span></span>

<span data-ttu-id="c156a-203">Behind the scenes, the Durable Functions extension is built on top of the [Durable Task Framework](https://github.com/Azure/durabletask), an open-source library on GitHub for building durable task orchestrations.</span><span class="sxs-lookup"><span data-stu-id="c156a-203">Behind the scenes, the Durable Functions extension is built on top of the [Durable Task Framework](https://github.com/Azure/durabletask), an open-source library on GitHub for building durable task orchestrations.</span></span> <span data-ttu-id="c156a-204">Much like how Azure Functions is the serverless evolution of Azure WebJobs, Durable Functions is the serverless evolution of the Durable Task Framework.</span><span class="sxs-lookup"><span data-stu-id="c156a-204">Much like how Azure Functions is the serverless evolution of Azure WebJobs, Durable Functions is the serverless evolution of the Durable Task Framework.</span></span> <span data-ttu-id="c156a-205">The Durable Task Framework is used heavily within Microsoft and outside as well to automate mission-critical processes.</span><span class="sxs-lookup"><span data-stu-id="c156a-205">The Durable Task Framework is used heavily within Microsoft and outside as well to automate mission-critical processes.</span></span> <span data-ttu-id="c156a-206">It's a natural fit for the serverless Azure Functions environment.</span><span class="sxs-lookup"><span data-stu-id="c156a-206">It's a natural fit for the serverless Azure Functions environment.</span></span>

### <a name="event-sourcing-checkpointing-and-replay"></a><span data-ttu-id="c156a-207">Event sourcing, checkpointing, and replay</span><span class="sxs-lookup"><span data-stu-id="c156a-207">Event sourcing, checkpointing, and replay</span></span>

<span data-ttu-id="c156a-208">Orchestrator functions reliably maintain their execution state using a design pattern known as [Event Sourcing](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing).</span><span class="sxs-lookup"><span data-stu-id="c156a-208">Orchestrator functions reliably maintain their execution state using a design pattern known as [Event Sourcing](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing).</span></span> <span data-ttu-id="c156a-209">Instead of directly storing the *current* state of an orchestration, the durable extension uses an append-only store to record the *full series of actions* taken by the function orchestration.</span><span class="sxs-lookup"><span data-stu-id="c156a-209">Instead of directly storing the *current* state of an orchestration, the durable extension uses an append-only store to record the *full series of actions* taken by the function orchestration.</span></span> <span data-ttu-id="c156a-210">This has many benefits, including improving performance, scalability, and responsiveness compared to "dumping" the full runtime state.</span><span class="sxs-lookup"><span data-stu-id="c156a-210">This has many benefits, including improving performance, scalability, and responsiveness compared to "dumping" the full runtime state.</span></span> <span data-ttu-id="c156a-211">Other benefits include providing eventual consistency for transactional data and maintaining full audit trails and history.</span><span class="sxs-lookup"><span data-stu-id="c156a-211">Other benefits include providing eventual consistency for transactional data and maintaining full audit trails and history.</span></span> <span data-ttu-id="c156a-212">The audit trails themselves enable reliable compensating actions.</span><span class="sxs-lookup"><span data-stu-id="c156a-212">The audit trails themselves enable reliable compensating actions.</span></span>

<span data-ttu-id="c156a-213">The use of Event Sourcing by this extension is transparent.</span><span class="sxs-lookup"><span data-stu-id="c156a-213">The use of Event Sourcing by this extension is transparent.</span></span> <span data-ttu-id="c156a-214">Under the covers, the `await` operator in an orchestrator function yields control of the orchestrator thread back to the Durable Task Framework dispatcher.</span><span class="sxs-lookup"><span data-stu-id="c156a-214">Under the covers, the `await` operator in an orchestrator function yields control of the orchestrator thread back to the Durable Task Framework dispatcher.</span></span> <span data-ttu-id="c156a-215">The dispatcher then commits any new actions that the orchestrator function scheduled (such as calling one or more child functions or scheduling a durable timer) to storage.</span><span class="sxs-lookup"><span data-stu-id="c156a-215">The dispatcher then commits any new actions that the orchestrator function scheduled (such as calling one or more child functions or scheduling a durable timer) to storage.</span></span> <span data-ttu-id="c156a-216">This transparent commit action appends to the *execution history* of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="c156a-216">This transparent commit action appends to the *execution history* of the orchestration instance.</span></span> <span data-ttu-id="c156a-217">The history is stored in a storage table.</span><span class="sxs-lookup"><span data-stu-id="c156a-217">The history is stored in a storage table.</span></span> <span data-ttu-id="c156a-218">The commit action then adds messages to a queue to schedule the actual work.</span><span class="sxs-lookup"><span data-stu-id="c156a-218">The commit action then adds messages to a queue to schedule the actual work.</span></span> <span data-ttu-id="c156a-219">At this point, the orchestrator function can be unloaded from memory.</span><span class="sxs-lookup"><span data-stu-id="c156a-219">At this point, the orchestrator function can be unloaded from memory.</span></span> <span data-ttu-id="c156a-220">Billing for it stops if you're using the Azure Functions Consumption Plan.</span><span class="sxs-lookup"><span data-stu-id="c156a-220">Billing for it stops if you're using the Azure Functions Consumption Plan.</span></span>  <span data-ttu-id="c156a-221">When there is more work to do, the function is restarted and its state is reconstructed.</span><span class="sxs-lookup"><span data-stu-id="c156a-221">When there is more work to do, the function is restarted and its state is reconstructed.</span></span>

<span data-ttu-id="c156a-222">Once an orchestration function is given more work to do (for example, a response message is received or a durable timer expires), the orchestrator wakes up again and re-executes the entire function from the start in order to rebuild the local state.</span><span class="sxs-lookup"><span data-stu-id="c156a-222">Once an orchestration function is given more work to do (for example, a response message is received or a durable timer expires), the orchestrator wakes up again and re-executes the entire function from the start in order to rebuild the local state.</span></span> <span data-ttu-id="c156a-223">If during this replay the code tries to call a function (or do any other async work), the Durable Task Framework consults with the *execution history* of the current orchestration.</span><span class="sxs-lookup"><span data-stu-id="c156a-223">If during this replay the code tries to call a function (or do any other async work), the Durable Task Framework consults with the *execution history* of the current orchestration.</span></span> <span data-ttu-id="c156a-224">If it finds that the [activity function](durable-functions-types-features-overview.md#activity-functions) has already executed and yielded some result, it replays that function's result, and the orchestrator code continues running.</span><span class="sxs-lookup"><span data-stu-id="c156a-224">If it finds that the [activity function](durable-functions-types-features-overview.md#activity-functions) has already executed and yielded some result, it replays that function's result, and the orchestrator code continues running.</span></span> <span data-ttu-id="c156a-225">This continues happening until the function code gets to a point where either it is finished or it has scheduled new async work.</span><span class="sxs-lookup"><span data-stu-id="c156a-225">This continues happening until the function code gets to a point where either it is finished or it has scheduled new async work.</span></span>

### <a name="orchestrator-code-constraints"></a><span data-ttu-id="c156a-226">Orchestrator code constraints</span><span class="sxs-lookup"><span data-stu-id="c156a-226">Orchestrator code constraints</span></span>

<span data-ttu-id="c156a-227">The replay behavior creates constraints on the type of code that can be written in an orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="c156a-227">The replay behavior creates constraints on the type of code that can be written in an orchestrator function.</span></span> <span data-ttu-id="c156a-228">For example, orchestrator code must be deterministic, as it will be replayed multiple times and must produce the same result each time.</span><span class="sxs-lookup"><span data-stu-id="c156a-228">For example, orchestrator code must be deterministic, as it will be replayed multiple times and must produce the same result each time.</span></span> <span data-ttu-id="c156a-229">The complete list of constraints can be found in the [Orchestrator code constraints](durable-functions-checkpointing-and-replay.md#orchestrator-code-constraints) section of the **Checkpointing and restart** article.</span><span class="sxs-lookup"><span data-stu-id="c156a-229">The complete list of constraints can be found in the [Orchestrator code constraints](durable-functions-checkpointing-and-replay.md#orchestrator-code-constraints) section of the **Checkpointing and restart** article.</span></span>

## <a name="language-support"></a><span data-ttu-id="c156a-230">Language support</span><span class="sxs-lookup"><span data-stu-id="c156a-230">Language support</span></span>

<span data-ttu-id="c156a-231">Currently C# (Functions v1 and v2), F# and JavaScript (Functions v2 only) are the only supported languages for Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="c156a-231">Currently C# (Functions v1 and v2), F# and JavaScript (Functions v2 only) are the only supported languages for Durable Functions.</span></span> <span data-ttu-id="c156a-232">This includes orchestrator functions and activity functions.</span><span class="sxs-lookup"><span data-stu-id="c156a-232">This includes orchestrator functions and activity functions.</span></span> <span data-ttu-id="c156a-233">In the future, we will add support for all languages that Azure Functions supports.</span><span class="sxs-lookup"><span data-stu-id="c156a-233">In the future, we will add support for all languages that Azure Functions supports.</span></span> <span data-ttu-id="c156a-234">See the Azure Functions [GitHub repository issues list](https://github.com/Azure/azure-functions-durable-extension/issues) to see the latest status of our additional language support work.</span><span class="sxs-lookup"><span data-stu-id="c156a-234">See the Azure Functions [GitHub repository issues list](https://github.com/Azure/azure-functions-durable-extension/issues) to see the latest status of our additional language support work.</span></span>

## <a name="monitoring-and-diagnostics"></a><span data-ttu-id="c156a-235">Monitoring and diagnostics</span><span class="sxs-lookup"><span data-stu-id="c156a-235">Monitoring and diagnostics</span></span>

<span data-ttu-id="c156a-236">The Durable Functions extension automatically emits structured tracking data to [Application Insights](functions-monitoring.md) when the function app is configured with an Application Insights instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="c156a-236">The Durable Functions extension automatically emits structured tracking data to [Application Insights](functions-monitoring.md) when the function app is configured with an Application Insights instrumentation key.</span></span> <span data-ttu-id="c156a-237">This tracking data can be used to monitor the behavior and progress of your orchestrations.</span><span class="sxs-lookup"><span data-stu-id="c156a-237">This tracking data can be used to monitor the behavior and progress of your orchestrations.</span></span>

<span data-ttu-id="c156a-238">Here is an example of what the Durable Functions tracking events look like in the Application Insights portal using [Application Insights Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics):</span><span class="sxs-lookup"><span data-stu-id="c156a-238">Here is an example of what the Durable Functions tracking events look like in the Application Insights portal using [Application Insights Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics):</span></span>

![App Insights query results](media/durable-functions-overview/app-insights-1.png)

<span data-ttu-id="c156a-240">There is a lot of useful structured data packed into the `customDimensions` field in each log entry.</span><span class="sxs-lookup"><span data-stu-id="c156a-240">There is a lot of useful structured data packed into the `customDimensions` field in each log entry.</span></span> <span data-ttu-id="c156a-241">Here is an example of one such entry fully expanded.</span><span class="sxs-lookup"><span data-stu-id="c156a-241">Here is an example of one such entry fully expanded.</span></span>

![customDimensions field in App Insights query](media/durable-functions-overview/app-insights-2.png)

<span data-ttu-id="c156a-243">Because of the replay behavior of the Durable Task Framework dispatcher, you can expect to see redundant log entries for replayed actions.</span><span class="sxs-lookup"><span data-stu-id="c156a-243">Because of the replay behavior of the Durable Task Framework dispatcher, you can expect to see redundant log entries for replayed actions.</span></span> <span data-ttu-id="c156a-244">This can be useful to understand the replay behavior of the core engine.</span><span class="sxs-lookup"><span data-stu-id="c156a-244">This can be useful to understand the replay behavior of the core engine.</span></span> <span data-ttu-id="c156a-245">The [Diagnostics](durable-functions-diagnostics.md) article shows sample queries that filter out replay logs so you can see just the "real-time" logs.</span><span class="sxs-lookup"><span data-stu-id="c156a-245">The [Diagnostics](durable-functions-diagnostics.md) article shows sample queries that filter out replay logs so you can see just the "real-time" logs.</span></span>

## <a name="storage-and-scalability"></a><span data-ttu-id="c156a-246">Storage and scalability</span><span class="sxs-lookup"><span data-stu-id="c156a-246">Storage and scalability</span></span>

<span data-ttu-id="c156a-247">The Durable Functions extension uses Azure Storage queues, tables, and blobs to persist execution history state and trigger function execution.</span><span class="sxs-lookup"><span data-stu-id="c156a-247">The Durable Functions extension uses Azure Storage queues, tables, and blobs to persist execution history state and trigger function execution.</span></span> <span data-ttu-id="c156a-248">The default storage account for the function app can be used, or you can configure a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="c156a-248">The default storage account for the function app can be used, or you can configure a separate storage account.</span></span> <span data-ttu-id="c156a-249">You might want a separate account due to storage throughput limits.</span><span class="sxs-lookup"><span data-stu-id="c156a-249">You might want a separate account due to storage throughput limits.</span></span> <span data-ttu-id="c156a-250">The orchestrator code you write does not need to (and should not) interact with the entities in these storage accounts.</span><span class="sxs-lookup"><span data-stu-id="c156a-250">The orchestrator code you write does not need to (and should not) interact with the entities in these storage accounts.</span></span> <span data-ttu-id="c156a-251">The entities are managed directly by the Durable Task Framework as an implementation detail.</span><span class="sxs-lookup"><span data-stu-id="c156a-251">The entities are managed directly by the Durable Task Framework as an implementation detail.</span></span>

<span data-ttu-id="c156a-252">Orchestrator functions schedule activity functions and receive their responses via internal queue messages.</span><span class="sxs-lookup"><span data-stu-id="c156a-252">Orchestrator functions schedule activity functions and receive their responses via internal queue messages.</span></span> <span data-ttu-id="c156a-253">When a function app runs in the Azure Functions Consumption plan, these queues are monitored by the [Azure Functions Scale Controller](functions-scale.md#how-the-consumption-plan-works) and new compute instances are added as needed.</span><span class="sxs-lookup"><span data-stu-id="c156a-253">When a function app runs in the Azure Functions Consumption plan, these queues are monitored by the [Azure Functions Scale Controller](functions-scale.md#how-the-consumption-plan-works) and new compute instances are added as needed.</span></span> <span data-ttu-id="c156a-254">When scaled out to multiple VMs, an orchestrator function may run on one VM while activity functions it calls run on several different VMs.</span><span class="sxs-lookup"><span data-stu-id="c156a-254">When scaled out to multiple VMs, an orchestrator function may run on one VM while activity functions it calls run on several different VMs.</span></span> <span data-ttu-id="c156a-255">You can find more details on the scale behavior of Durable Functions in [Performance and scale](durable-functions-perf-and-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c156a-255">You can find more details on the scale behavior of Durable Functions in [Performance and scale](durable-functions-perf-and-scale.md).</span></span>

<span data-ttu-id="c156a-256">Table storage is used to store the execution history for orchestrator accounts.</span><span class="sxs-lookup"><span data-stu-id="c156a-256">Table storage is used to store the execution history for orchestrator accounts.</span></span> <span data-ttu-id="c156a-257">Whenever an instance rehydrates on a particular VM, it fetches its execution history from table storage so that it can rebuild its local state.</span><span class="sxs-lookup"><span data-stu-id="c156a-257">Whenever an instance rehydrates on a particular VM, it fetches its execution history from table storage so that it can rebuild its local state.</span></span> <span data-ttu-id="c156a-258">One of the convenient things about having the history available in Table storage is that you can take a look and see the history of your orchestrations using tools such as [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span><span class="sxs-lookup"><span data-stu-id="c156a-258">One of the convenient things about having the history available in Table storage is that you can take a look and see the history of your orchestrations using tools such as [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span></span>

<span data-ttu-id="c156a-259">Storage blobs are used primarily as a leasing mechanism to coordinate the scale-out of orchestration instances across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="c156a-259">Storage blobs are used primarily as a leasing mechanism to coordinate the scale-out of orchestration instances across multiple VMs.</span></span> <span data-ttu-id="c156a-260">They are also used to hold data for large messages which cannot be stored directly in tables or queues.</span><span class="sxs-lookup"><span data-stu-id="c156a-260">They are also used to hold data for large messages which cannot be stored directly in tables or queues.</span></span>

![Azure Storage Explorer screen shot](media/durable-functions-overview/storage-explorer.png)

> [!WARNING]
> <span data-ttu-id="c156a-262">While it's easy and convenient to see execution history in table storage, avoid taking any dependency on this table.</span><span class="sxs-lookup"><span data-stu-id="c156a-262">While it's easy and convenient to see execution history in table storage, avoid taking any dependency on this table.</span></span> <span data-ttu-id="c156a-263">It may change as the Durable Functions extension evolves.</span><span class="sxs-lookup"><span data-stu-id="c156a-263">It may change as the Durable Functions extension evolves.</span></span>

## <a name="known-issues-and-faq"></a><span data-ttu-id="c156a-264">Known issues and FAQ</span><span class="sxs-lookup"><span data-stu-id="c156a-264">Known issues and FAQ</span></span>

<span data-ttu-id="c156a-265">All known issues should be tracked in the [GitHub issues](https://github.com/Azure/azure-functions-durable-extension/issues) list.</span><span class="sxs-lookup"><span data-stu-id="c156a-265">All known issues should be tracked in the [GitHub issues](https://github.com/Azure/azure-functions-durable-extension/issues) list.</span></span> <span data-ttu-id="c156a-266">If you run into a problem and can't find the issue in GitHub, open a new issue and include a detailed description of the problem.</span><span class="sxs-lookup"><span data-stu-id="c156a-266">If you run into a problem and can't find the issue in GitHub, open a new issue and include a detailed description of the problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c156a-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="c156a-267">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c156a-268">Continue reading Durable Functions documentation</span><span class="sxs-lookup"><span data-stu-id="c156a-268">Continue reading Durable Functions documentation</span></span>](durable-functions-types-features-overview.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c156a-269">Install the Durable Functions extension and samples</span><span class="sxs-lookup"><span data-stu-id="c156a-269">Install the Durable Functions extension and samples</span></span>](durable-functions-install.md)

