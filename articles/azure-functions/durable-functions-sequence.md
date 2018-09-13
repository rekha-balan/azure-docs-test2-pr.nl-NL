---
title: Function chaining in Durable Functions - Azure
description: Learn how to run a Durable Functions sample that executes a sequence of functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: azfuncdf
ms.openlocfilehash: c84977dacddcf9ccca7fde735ad4acb8a1523fa9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870949"
---
# <a name="function-chaining-in-durable-functions---hello-sequence-sample"></a><span data-ttu-id="55ca0-103">Function chaining in Durable Functions - Hello sequence sample</span><span class="sxs-lookup"><span data-stu-id="55ca0-103">Function chaining in Durable Functions - Hello sequence sample</span></span>

<span data-ttu-id="55ca0-104">Function chaining refers to the pattern of executing a sequence of functions in a particular order.</span><span class="sxs-lookup"><span data-stu-id="55ca0-104">Function chaining refers to the pattern of executing a sequence of functions in a particular order.</span></span> <span data-ttu-id="55ca0-105">Often the output of one function needs to be applied to the input of another function.</span><span class="sxs-lookup"><span data-stu-id="55ca0-105">Often the output of one function needs to be applied to the input of another function.</span></span> <span data-ttu-id="55ca0-106">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement function chaining.</span><span class="sxs-lookup"><span data-stu-id="55ca0-106">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement function chaining.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55ca0-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="55ca0-107">Prerequisites</span></span>

* <span data-ttu-id="55ca0-108">[Install Durable Functions](durable-functions-install.md).</span><span class="sxs-lookup"><span data-stu-id="55ca0-108">[Install Durable Functions](durable-functions-install.md).</span></span>

## <a name="the-functions"></a><span data-ttu-id="55ca0-109">The functions</span><span class="sxs-lookup"><span data-stu-id="55ca0-109">The functions</span></span>

<span data-ttu-id="55ca0-110">This article explains the following functions in the sample app:</span><span class="sxs-lookup"><span data-stu-id="55ca0-110">This article explains the following functions in the sample app:</span></span>

* <span data-ttu-id="55ca0-111">`E1_HelloSequence`: An orchestrator function that calls `E1_SayHello` multiple times in a sequence.</span><span class="sxs-lookup"><span data-stu-id="55ca0-111">`E1_HelloSequence`: An orchestrator function that calls `E1_SayHello` multiple times in a sequence.</span></span> <span data-ttu-id="55ca0-112">It stores the outputs from the `E1_SayHello` calls and records the results.</span><span class="sxs-lookup"><span data-stu-id="55ca0-112">It stores the outputs from the `E1_SayHello` calls and records the results.</span></span>
* <span data-ttu-id="55ca0-113">`E1_SayHello`: An activity function that prepends a string with "Hello".</span><span class="sxs-lookup"><span data-stu-id="55ca0-113">`E1_SayHello`: An activity function that prepends a string with "Hello".</span></span>

<span data-ttu-id="55ca0-114">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="55ca0-114">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span></span> <span data-ttu-id="55ca0-115">The code for Visual Studio development is shown at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="55ca0-115">The code for Visual Studio development is shown at the end of the article.</span></span>

> [!NOTE]
> <span data-ttu-id="55ca0-116">Durable Functions is available in JavaScript in the v2 Functions runtime only.</span><span class="sxs-lookup"><span data-stu-id="55ca0-116">Durable Functions is available in JavaScript in the v2 Functions runtime only.</span></span>

## <a name="e1hellosequence"></a><span data-ttu-id="55ca0-117">E1_HelloSequence</span><span class="sxs-lookup"><span data-stu-id="55ca0-117">E1_HelloSequence</span></span>
### <a name="functionjson-file"></a><span data-ttu-id="55ca0-118">function.json file</span><span class="sxs-lookup"><span data-stu-id="55ca0-118">function.json file</span></span>

<span data-ttu-id="55ca0-119">If you use Visual Studio Code or the Azure portal for development, here's the content of the *function.json* file for the orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="55ca0-119">If you use Visual Studio Code or the Azure portal for development, here's the content of the *function.json* file for the orchestrator function.</span></span> <span data-ttu-id="55ca0-120">Most orchestrator *function.json* files look almost exactly like this.</span><span class="sxs-lookup"><span data-stu-id="55ca0-120">Most orchestrator *function.json* files look almost exactly like this.</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/function.json)]

<span data-ttu-id="55ca0-121">The important thing is the `orchestrationTrigger` binding type.</span><span class="sxs-lookup"><span data-stu-id="55ca0-121">The important thing is the `orchestrationTrigger` binding type.</span></span> <span data-ttu-id="55ca0-122">All orchestrator functions must use this trigger type.</span><span class="sxs-lookup"><span data-stu-id="55ca0-122">All orchestrator functions must use this trigger type.</span></span>

> [!WARNING]
> <span data-ttu-id="55ca0-123">To abide by the "no I/O" rule of orchestrator functions, don't use any input or output bindings when using the `orchestrationTrigger` trigger binding.</span><span class="sxs-lookup"><span data-stu-id="55ca0-123">To abide by the "no I/O" rule of orchestrator functions, don't use any input or output bindings when using the `orchestrationTrigger` trigger binding.</span></span>  <span data-ttu-id="55ca0-124">If other input or output bindings are needed, they should instead be used in the context of `activityTrigger` functions, which are called by the orchestrator.</span><span class="sxs-lookup"><span data-stu-id="55ca0-124">If other input or output bindings are needed, they should instead be used in the context of `activityTrigger` functions, which are called by the orchestrator.</span></span>

### <a name="c-script-visual-studio-code-and-azure-portal-sample-code"></a><span data-ttu-id="55ca0-125">C# script (Visual Studio Code and Azure portal sample code)</span><span class="sxs-lookup"><span data-stu-id="55ca0-125">C# script (Visual Studio Code and Azure portal sample code)</span></span> 

<span data-ttu-id="55ca0-126">Here is the source code:</span><span class="sxs-lookup"><span data-stu-id="55ca0-126">Here is the source code:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/run.csx)]

<span data-ttu-id="55ca0-127">All C# orchestration functions must have a parameter of type `DurableOrchestrationContext`, which exists in the `Microsoft.Azure.WebJobs.Extensions.DurableTask` assembly.</span><span class="sxs-lookup"><span data-stu-id="55ca0-127">All C# orchestration functions must have a parameter of type `DurableOrchestrationContext`, which exists in the `Microsoft.Azure.WebJobs.Extensions.DurableTask` assembly.</span></span> <span data-ttu-id="55ca0-128">If you're using C# script, the assembly can be referenced using the `#r` notation.</span><span class="sxs-lookup"><span data-stu-id="55ca0-128">If you're using C# script, the assembly can be referenced using the `#r` notation.</span></span> <span data-ttu-id="55ca0-129">This context object lets you call other *activity* functions and pass input parameters using its [CallActivityAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_) method.</span><span class="sxs-lookup"><span data-stu-id="55ca0-129">This context object lets you call other *activity* functions and pass input parameters using its [CallActivityAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_) method.</span></span>

<span data-ttu-id="55ca0-130">The code calls `E1_SayHello` three times in sequence with different parameter values.</span><span class="sxs-lookup"><span data-stu-id="55ca0-130">The code calls `E1_SayHello` three times in sequence with different parameter values.</span></span> <span data-ttu-id="55ca0-131">The return value of each call is added to the `outputs` list, which is returned at the end of the function.</span><span class="sxs-lookup"><span data-stu-id="55ca0-131">The return value of each call is added to the `outputs` list, which is returned at the end of the function.</span></span>

### <a name="javascript"></a><span data-ttu-id="55ca0-132">Javascript</span><span class="sxs-lookup"><span data-stu-id="55ca0-132">Javascript</span></span>

<span data-ttu-id="55ca0-133">Here is the source code:</span><span class="sxs-lookup"><span data-stu-id="55ca0-133">Here is the source code:</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E1_HelloSequence/index.js)]

<span data-ttu-id="55ca0-134">All JavaScript orchestration functions must include the `durable-functions` module.</span><span class="sxs-lookup"><span data-stu-id="55ca0-134">All JavaScript orchestration functions must include the `durable-functions` module.</span></span> <span data-ttu-id="55ca0-135">This is a JavaScript library that translates the orchestration function's actions into Durable's execution protocol for out-of-proc languages.</span><span class="sxs-lookup"><span data-stu-id="55ca0-135">This is a JavaScript library that translates the orchestration function's actions into Durable's execution protocol for out-of-proc languages.</span></span> <span data-ttu-id="55ca0-136">There are three significant differences between an orchestration function and other JavaScript functions:</span><span class="sxs-lookup"><span data-stu-id="55ca0-136">There are three significant differences between an orchestration function and other JavaScript functions:</span></span>

1. <span data-ttu-id="55ca0-137">The function is a [generator function.](https://docs.microsoft.com/scripting/javascript/advanced/iterators-and-generators-javascript)</span><span class="sxs-lookup"><span data-stu-id="55ca0-137">The function is a [generator function.](https://docs.microsoft.com/scripting/javascript/advanced/iterators-and-generators-javascript)</span></span>
2. <span data-ttu-id="55ca0-138">The function is wrapped in a call to the `durable-functions` module (here `df`).</span><span class="sxs-lookup"><span data-stu-id="55ca0-138">The function is wrapped in a call to the `durable-functions` module (here `df`).</span></span>
3. <span data-ttu-id="55ca0-139">The function ends by calling `return`, not `context.done`.</span><span class="sxs-lookup"><span data-stu-id="55ca0-139">The function ends by calling `return`, not `context.done`.</span></span>

<span data-ttu-id="55ca0-140">The `context` object contains a `df` object lets you call other *activity* functions and pass input parameters using its `callActivityAsync` method.</span><span class="sxs-lookup"><span data-stu-id="55ca0-140">The `context` object contains a `df` object lets you call other *activity* functions and pass input parameters using its `callActivityAsync` method.</span></span> <span data-ttu-id="55ca0-141">The code calls `E1_SayHello` three times in sequence with different parameter values, using `yield` to indicate the execution should wait on the async activity function calls to be returned.</span><span class="sxs-lookup"><span data-stu-id="55ca0-141">The code calls `E1_SayHello` three times in sequence with different parameter values, using `yield` to indicate the execution should wait on the async activity function calls to be returned.</span></span> <span data-ttu-id="55ca0-142">The return value of each call is added to the `outputs` list, which is returned at the end of the function.</span><span class="sxs-lookup"><span data-stu-id="55ca0-142">The return value of each call is added to the `outputs` list, which is returned at the end of the function.</span></span>

## <a name="e1sayhello"></a><span data-ttu-id="55ca0-143">E1_SayHello</span><span class="sxs-lookup"><span data-stu-id="55ca0-143">E1_SayHello</span></span>
### <a name="functionjson-file"></a><span data-ttu-id="55ca0-144">function.json file</span><span class="sxs-lookup"><span data-stu-id="55ca0-144">function.json file</span></span>

<span data-ttu-id="55ca0-145">The *function.json* file for the activity function `E1_SayHello` is similar to that of `E1_HelloSequence` except that it uses an `activityTrigger` binding type instead of an `orchestrationTrigger` binding type.</span><span class="sxs-lookup"><span data-stu-id="55ca0-145">The *function.json* file for the activity function `E1_SayHello` is similar to that of `E1_HelloSequence` except that it uses an `activityTrigger` binding type instead of an `orchestrationTrigger` binding type.</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_SayHello/function.json)]

> [!NOTE]
> <span data-ttu-id="55ca0-146">Any function called by an orchestration function must use the `activityTrigger` binding.</span><span class="sxs-lookup"><span data-stu-id="55ca0-146">Any function called by an orchestration function must use the `activityTrigger` binding.</span></span>

<span data-ttu-id="55ca0-147">The implementation of `E1_SayHello` is a relatively trivial string formatting operation.</span><span class="sxs-lookup"><span data-stu-id="55ca0-147">The implementation of `E1_SayHello` is a relatively trivial string formatting operation.</span></span>

### <a name="c"></a><span data-ttu-id="55ca0-148">C#</span><span class="sxs-lookup"><span data-stu-id="55ca0-148">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_SayHello/run.csx)]

<span data-ttu-id="55ca0-149">This function has a parameter of type [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html), which it uses to get the input that was passed to it by the orchestrator function's call to [`CallActivityAsync<T>`](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_).</span><span class="sxs-lookup"><span data-stu-id="55ca0-149">This function has a parameter of type [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html), which it uses to get the input that was passed to it by the orchestrator function's call to [`CallActivityAsync<T>`](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_).</span></span>

### <a name="javascript"></a><span data-ttu-id="55ca0-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="55ca0-150">JavaScript</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E1_SayHello/index.js)]

<span data-ttu-id="55ca0-151">Unlike a JavaScript orchestration function, a JavaScript activity function needs no special setup.</span><span class="sxs-lookup"><span data-stu-id="55ca0-151">Unlike a JavaScript orchestration function, a JavaScript activity function needs no special setup.</span></span> <span data-ttu-id="55ca0-152">The input passed to it by the orchestrator function is located on the `context.bindings` object under the name of the `activitytrigger` binding - in this case, `context.bindings.name`.</span><span class="sxs-lookup"><span data-stu-id="55ca0-152">The input passed to it by the orchestrator function is located on the `context.bindings` object under the name of the `activitytrigger` binding - in this case, `context.bindings.name`.</span></span> <span data-ttu-id="55ca0-153">The binding name can be set as a parameter of the exported function and accessed directly, which is what the sample code does.</span><span class="sxs-lookup"><span data-stu-id="55ca0-153">The binding name can be set as a parameter of the exported function and accessed directly, which is what the sample code does.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="55ca0-154">Run the sample</span><span class="sxs-lookup"><span data-stu-id="55ca0-154">Run the sample</span></span>

<span data-ttu-id="55ca0-155">To execute the `E1_HelloSequence` orchestration, send the following HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="55ca0-155">To execute the `E1_HelloSequence` orchestration, send the following HTTP POST request.</span></span>

```
POST http://{host}/orchestrators/E1_HelloSequence
```

> [!NOTE]
> <span data-ttu-id="55ca0-156">The previous HTTP snippet assumes there is an entry in the `host.json` file which removes the default `api/` prefix from all HTTP trigger functions URLs.</span><span class="sxs-lookup"><span data-stu-id="55ca0-156">The previous HTTP snippet assumes there is an entry in the `host.json` file which removes the default `api/` prefix from all HTTP trigger functions URLs.</span></span> <span data-ttu-id="55ca0-157">You can find the markup for this configuration in the `host.json` file in the samples.</span><span class="sxs-lookup"><span data-stu-id="55ca0-157">You can find the markup for this configuration in the `host.json` file in the samples.</span></span>

<span data-ttu-id="55ca0-158">For example, if you're running the sample in a function app named "myfunctionapp", replace "{host}" with "myfunctionapp.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="55ca0-158">For example, if you're running the sample in a function app named "myfunctionapp", replace "{host}" with "myfunctionapp.azurewebsites.net".</span></span>

<span data-ttu-id="55ca0-159">The result is an HTTP 202 response, like this (trimmed for brevity):</span><span class="sxs-lookup"><span data-stu-id="55ca0-159">The result is an HTTP 202 response, like this (trimmed for brevity):</span></span>

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

(...trimmed...)
```

<span data-ttu-id="55ca0-160">At this point, the orchestration is queued up and begins to run immediately.</span><span class="sxs-lookup"><span data-stu-id="55ca0-160">At this point, the orchestration is queued up and begins to run immediately.</span></span> <span data-ttu-id="55ca0-161">The URL in the `Location` header can be used to check the status of the execution.</span><span class="sxs-lookup"><span data-stu-id="55ca0-161">The URL in the `Location` header can be used to check the status of the execution.</span></span>

```
GET http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```

<span data-ttu-id="55ca0-162">The result is the status of the orchestration.</span><span class="sxs-lookup"><span data-stu-id="55ca0-162">The result is the status of the orchestration.</span></span> <span data-ttu-id="55ca0-163">It runs and completes quickly, so you see it in the *Completed* state with a response that looks like this (trimmed for brevity):</span><span class="sxs-lookup"><span data-stu-id="55ca0-163">It runs and completes quickly, so you see it in the *Completed* state with a response that looks like this (trimmed for brevity):</span></span>

```
HTTP/1.1 200 OK
Content-Length: 179
Content-Type: application/json; charset=utf-8

{"runtimeStatus":"Completed","input":null,"output":["Hello Tokyo!","Hello Seattle!","Hello London!"],"createdTime":"2017-06-29T05:24:57Z","lastUpdatedTime":"2017-06-29T05:24:59Z"}
```

<span data-ttu-id="55ca0-164">As you can see, the `runtimeStatus` of the instance is *Completed* and the `output` contains the JSON-serialized result of the orchestrator function execution.</span><span class="sxs-lookup"><span data-stu-id="55ca0-164">As you can see, the `runtimeStatus` of the instance is *Completed* and the `output` contains the JSON-serialized result of the orchestrator function execution.</span></span>

> [!NOTE]
> <span data-ttu-id="55ca0-165">The HTTP POST endpoint that started the orchestrator function is implemented in the sample app as an HTTP trigger function named "HttpStart".</span><span class="sxs-lookup"><span data-stu-id="55ca0-165">The HTTP POST endpoint that started the orchestrator function is implemented in the sample app as an HTTP trigger function named "HttpStart".</span></span> <span data-ttu-id="55ca0-166">You can implement similar starter logic for other trigger types, like `queueTrigger`, `eventHubTrigger`, or `timerTrigger`.</span><span class="sxs-lookup"><span data-stu-id="55ca0-166">You can implement similar starter logic for other trigger types, like `queueTrigger`, `eventHubTrigger`, or `timerTrigger`.</span></span>

<span data-ttu-id="55ca0-167">Look at the function execution logs.</span><span class="sxs-lookup"><span data-stu-id="55ca0-167">Look at the function execution logs.</span></span> <span data-ttu-id="55ca0-168">The `E1_HelloSequence` function started and completed multiple times due to the replay behavior described in the [overview](durable-functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55ca0-168">The `E1_HelloSequence` function started and completed multiple times due to the replay behavior described in the [overview](durable-functions-overview.md).</span></span> <span data-ttu-id="55ca0-169">On the other hand, there were only three executions of `E1_SayHello` since those function executions do not get replayed.</span><span class="sxs-lookup"><span data-stu-id="55ca0-169">On the other hand, there were only three executions of `E1_SayHello` since those function executions do not get replayed.</span></span>

## <a name="visual-studio-sample-code"></a><span data-ttu-id="55ca0-170">Visual Studio sample code</span><span class="sxs-lookup"><span data-stu-id="55ca0-170">Visual Studio sample code</span></span>

<span data-ttu-id="55ca0-171">Here is the orchestration as a single C# file in a Visual Studio project:</span><span class="sxs-lookup"><span data-stu-id="55ca0-171">Here is the orchestration as a single C# file in a Visual Studio project:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HelloSequence.cs)]

## <a name="next-steps"></a><span data-ttu-id="55ca0-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="55ca0-172">Next steps</span></span>

<span data-ttu-id="55ca0-173">This sample has demonstrated a simple function-chaining orchestration.</span><span class="sxs-lookup"><span data-stu-id="55ca0-173">This sample has demonstrated a simple function-chaining orchestration.</span></span> <span data-ttu-id="55ca0-174">The next sample shows how to implement the  fan-out/fan-in pattern.</span><span class="sxs-lookup"><span data-stu-id="55ca0-174">The next sample shows how to implement the  fan-out/fan-in pattern.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="55ca0-175">Run the Fan-out/fan-in sample</span><span class="sxs-lookup"><span data-stu-id="55ca0-175">Run the Fan-out/fan-in sample</span></span>](durable-functions-cloud-backup.md)
