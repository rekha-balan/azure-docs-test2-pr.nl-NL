---
title: Bindings for Durable Functions - Azure
description: How to use triggers and bindings for the Durable Functons extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 6a9ecbcc5161f47a192d5bf3a893a42b3ee9ce2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865208"
---
# <a name="bindings-for-durable-functions-azure-functions"></a><span data-ttu-id="71d58-103">Bindings for Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="71d58-103">Bindings for Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="71d58-104">The [Durable Functions](durable-functions-overview.md) extension introduces two new trigger bindings that control the execution of orchestrator and activity functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-104">The [Durable Functions](durable-functions-overview.md) extension introduces two new trigger bindings that control the execution of orchestrator and activity functions.</span></span> <span data-ttu-id="71d58-105">It also introduces an output binding that acts as a client for the Durable Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="71d58-105">It also introduces an output binding that acts as a client for the Durable Functions runtime.</span></span>

## <a name="orchestration-triggers"></a><span data-ttu-id="71d58-106">Orchestration triggers</span><span class="sxs-lookup"><span data-stu-id="71d58-106">Orchestration triggers</span></span>

<span data-ttu-id="71d58-107">The orchestration trigger enables you to author durable orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-107">The orchestration trigger enables you to author durable orchestrator functions.</span></span> <span data-ttu-id="71d58-108">This trigger supports starting new orchestrator function instances and resuming existing orchestrator function instances that are "awaiting" a task.</span><span class="sxs-lookup"><span data-stu-id="71d58-108">This trigger supports starting new orchestrator function instances and resuming existing orchestrator function instances that are "awaiting" a task.</span></span>

<span data-ttu-id="71d58-109">When you use the Visual Studio tools for Azure Functions, the orchestration trigger is configured using the [OrchestrationTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationTriggerAttribute.html) .NET attribute.</span><span class="sxs-lookup"><span data-stu-id="71d58-109">When you use the Visual Studio tools for Azure Functions, the orchestration trigger is configured using the [OrchestrationTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationTriggerAttribute.html) .NET attribute.</span></span>

<span data-ttu-id="71d58-110">When you write orchestrator functions in scripting languages (for example, in the Azure portal), the orchestration trigger is defined by the following JSON object in the `bindings` array of the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="71d58-110">When you write orchestrator functions in scripting languages (for example, in the Azure portal), the orchestration trigger is defined by the following JSON object in the `bindings` array of the *function.json* file:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "orchestration": "<Optional - name of the orchestration>",
    "type": "orchestrationTrigger",
    "direction": "in"
}
```

* <span data-ttu-id="71d58-111">`orchestration` is the name of the orchestration.</span><span class="sxs-lookup"><span data-stu-id="71d58-111">`orchestration` is the name of the orchestration.</span></span> <span data-ttu-id="71d58-112">This is the value that clients must use when they want to start new instances of this orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="71d58-112">This is the value that clients must use when they want to start new instances of this orchestrator function.</span></span> <span data-ttu-id="71d58-113">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="71d58-113">This property is optional.</span></span> <span data-ttu-id="71d58-114">If not specified, the name of the function is used.</span><span class="sxs-lookup"><span data-stu-id="71d58-114">If not specified, the name of the function is used.</span></span>

<span data-ttu-id="71d58-115">Internally this trigger binding polls a series of queues in the default storage account for the function app.</span><span class="sxs-lookup"><span data-stu-id="71d58-115">Internally this trigger binding polls a series of queues in the default storage account for the function app.</span></span> <span data-ttu-id="71d58-116">These queues are internal implementation details of the extension, which is why they are not explicitly configured in the binding properties.</span><span class="sxs-lookup"><span data-stu-id="71d58-116">These queues are internal implementation details of the extension, which is why they are not explicitly configured in the binding properties.</span></span>

### <a name="trigger-behavior"></a><span data-ttu-id="71d58-117">Trigger behavior</span><span class="sxs-lookup"><span data-stu-id="71d58-117">Trigger behavior</span></span>

<span data-ttu-id="71d58-118">Here are some notes about the orchestration trigger:</span><span class="sxs-lookup"><span data-stu-id="71d58-118">Here are some notes about the orchestration trigger:</span></span>

* <span data-ttu-id="71d58-119">**Single-threading** - A single dispatcher thread is used for all orchestrator function execution on a single host instance.</span><span class="sxs-lookup"><span data-stu-id="71d58-119">**Single-threading** - A single dispatcher thread is used for all orchestrator function execution on a single host instance.</span></span> <span data-ttu-id="71d58-120">For this reason, it is important to ensure that orchestrator function code is efficient and doesn't perform any I/O.</span><span class="sxs-lookup"><span data-stu-id="71d58-120">For this reason, it is important to ensure that orchestrator function code is efficient and doesn't perform any I/O.</span></span> <span data-ttu-id="71d58-121">It is also important to ensure that this thread does not do any async work except when awaiting on Durable Functions-specific task types.</span><span class="sxs-lookup"><span data-stu-id="71d58-121">It is also important to ensure that this thread does not do any async work except when awaiting on Durable Functions-specific task types.</span></span>
* <span data-ttu-id="71d58-122">**Poison-message handling** - There is no poison message support in orchestration triggers.</span><span class="sxs-lookup"><span data-stu-id="71d58-122">**Poison-message handling** - There is no poison message support in orchestration triggers.</span></span>
* <span data-ttu-id="71d58-123">**Message visibility** - Orchestration trigger messages are dequeued and kept invisible for a configurable duration.</span><span class="sxs-lookup"><span data-stu-id="71d58-123">**Message visibility** - Orchestration trigger messages are dequeued and kept invisible for a configurable duration.</span></span> <span data-ttu-id="71d58-124">The visibility of these messages is renewed automatically as long as the function app is running and healthy.</span><span class="sxs-lookup"><span data-stu-id="71d58-124">The visibility of these messages is renewed automatically as long as the function app is running and healthy.</span></span>
* <span data-ttu-id="71d58-125">**Return values** - Return values are serialized to JSON and persisted to the orchestration history table in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="71d58-125">**Return values** - Return values are serialized to JSON and persisted to the orchestration history table in Azure Table storage.</span></span> <span data-ttu-id="71d58-126">These return values can be queried by the orchestration client binding, described later.</span><span class="sxs-lookup"><span data-stu-id="71d58-126">These return values can be queried by the orchestration client binding, described later.</span></span>

> [!WARNING]
> <span data-ttu-id="71d58-127">Orchestrator functions should never use any input or output bindings other than the orchestration trigger binding.</span><span class="sxs-lookup"><span data-stu-id="71d58-127">Orchestrator functions should never use any input or output bindings other than the orchestration trigger binding.</span></span> <span data-ttu-id="71d58-128">Doing so has the potential to cause problems with the Durable Task extension because those bindings may not obey the single-threading and I/O rules.</span><span class="sxs-lookup"><span data-stu-id="71d58-128">Doing so has the potential to cause problems with the Durable Task extension because those bindings may not obey the single-threading and I/O rules.</span></span>

### <a name="trigger-usage"></a><span data-ttu-id="71d58-129">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="71d58-129">Trigger usage</span></span>

<span data-ttu-id="71d58-130">The orchestration trigger binding supports both inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="71d58-130">The orchestration trigger binding supports both inputs and outputs.</span></span> <span data-ttu-id="71d58-131">Here are some things to know about input and output handling:</span><span class="sxs-lookup"><span data-stu-id="71d58-131">Here are some things to know about input and output handling:</span></span>

* <span data-ttu-id="71d58-132">**inputs** - Orchestration functions support only [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html) as a parameter type.</span><span class="sxs-lookup"><span data-stu-id="71d58-132">**inputs** - Orchestration functions support only [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html) as a parameter type.</span></span> <span data-ttu-id="71d58-133">Deserialization of inputs directly in the function signature is not supported.</span><span class="sxs-lookup"><span data-stu-id="71d58-133">Deserialization of inputs directly in the function signature is not supported.</span></span> <span data-ttu-id="71d58-134">Code must use the [GetInput\<T>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_GetInput__1) method to fetch orchestrator function inputs.</span><span class="sxs-lookup"><span data-stu-id="71d58-134">Code must use the [GetInput\<T>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_GetInput__1) method to fetch orchestrator function inputs.</span></span> <span data-ttu-id="71d58-135">These inputs must be JSON-serializable types.</span><span class="sxs-lookup"><span data-stu-id="71d58-135">These inputs must be JSON-serializable types.</span></span>
* <span data-ttu-id="71d58-136">**outputs** - Orchestration triggers support output values as well as inputs.</span><span class="sxs-lookup"><span data-stu-id="71d58-136">**outputs** - Orchestration triggers support output values as well as inputs.</span></span> <span data-ttu-id="71d58-137">The return value of the function is used to assign the output value and must be JSON-serializable.</span><span class="sxs-lookup"><span data-stu-id="71d58-137">The return value of the function is used to assign the output value and must be JSON-serializable.</span></span> <span data-ttu-id="71d58-138">If a function returns `Task` or `void`, a `null` value will be saved as the output.</span><span class="sxs-lookup"><span data-stu-id="71d58-138">If a function returns `Task` or `void`, a `null` value will be saved as the output.</span></span>

### <a name="trigger-sample"></a><span data-ttu-id="71d58-139">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="71d58-139">Trigger sample</span></span>

<span data-ttu-id="71d58-140">The following is an example of what the simplest "Hello World" orchestrator function might look like:</span><span class="sxs-lookup"><span data-stu-id="71d58-140">The following is an example of what the simplest "Hello World" orchestrator function might look like:</span></span>

#### <a name="c"></a><span data-ttu-id="71d58-141">C#</span><span class="sxs-lookup"><span data-stu-id="71d58-141">C#</span></span>

```csharp
[FunctionName("HelloWorld")]
public static string Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    string name = context.GetInput<string>();
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="71d58-142">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="71d58-142">JavaScript (Functions v2 only)</span></span>

```javascript
const df = require("durable-functions");

module.exports = df(function*(context) {
    const name = context.df.getInput();
    return `Hello ${name}!`;
});
```

> [!NOTE]
> <span data-ttu-id="71d58-143">JavaScript orchestrators should use `return`.</span><span class="sxs-lookup"><span data-stu-id="71d58-143">JavaScript orchestrators should use `return`.</span></span> <span data-ttu-id="71d58-144">The `durable-functions` library takes care of calling the `context.done` method.</span><span class="sxs-lookup"><span data-stu-id="71d58-144">The `durable-functions` library takes care of calling the `context.done` method.</span></span>

<span data-ttu-id="71d58-145">Most orchestrator functions call activity functions, so here is a "Hello World" example that demonstrates how to call an activity function:</span><span class="sxs-lookup"><span data-stu-id="71d58-145">Most orchestrator functions call activity functions, so here is a "Hello World" example that demonstrates how to call an activity function:</span></span>

#### <a name="c"></a><span data-ttu-id="71d58-146">C#</span><span class="sxs-lookup"><span data-stu-id="71d58-146">C#</span></span>

```csharp
[FunctionName("HelloWorld")]
public static async Task<string> Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    string name = context.GetInput<string>();
    string result = await context.CallActivityAsync<string>("SayHello", name);
    return result;
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="71d58-147">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="71d58-147">JavaScript (Functions v2 only)</span></span>

```javascript
const df = require("durable-functions");

module.exports = df(function*(context) {
    const name = context.df.getInput();
    const result = yield context.df.callActivityAsync("SayHello", name);
    return result;
});
```

## <a name="activity-triggers"></a><span data-ttu-id="71d58-148">Activity triggers</span><span class="sxs-lookup"><span data-stu-id="71d58-148">Activity triggers</span></span>

<span data-ttu-id="71d58-149">The activity trigger enables you to author functions that are called by orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-149">The activity trigger enables you to author functions that are called by orchestrator functions.</span></span>

<span data-ttu-id="71d58-150">If you're using Visual Studio, the activity trigger is configured using the [ActivityTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.ActivityTriggerAttribute.html) .NET attribute.</span><span class="sxs-lookup"><span data-stu-id="71d58-150">If you're using Visual Studio, the activity trigger is configured using the [ActivityTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.ActivityTriggerAttribute.html) .NET attribute.</span></span> 

<span data-ttu-id="71d58-151">If you're using the Azure portal for development, the activity trigger is defined by the following JSON object in the `bindings` array of *function.json*:</span><span class="sxs-lookup"><span data-stu-id="71d58-151">If you're using the Azure portal for development, the activity trigger is defined by the following JSON object in the `bindings` array of *function.json*:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "activity": "<Optional - name of the activity>",
    "type": "activityTrigger",
    "direction": "in"
}
```

* <span data-ttu-id="71d58-152">`activity` is the name of the activity.</span><span class="sxs-lookup"><span data-stu-id="71d58-152">`activity` is the name of the activity.</span></span> <span data-ttu-id="71d58-153">This is the value that orchestrator functions use to invoke this activity function.</span><span class="sxs-lookup"><span data-stu-id="71d58-153">This is the value that orchestrator functions use to invoke this activity function.</span></span> <span data-ttu-id="71d58-154">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="71d58-154">This property is optional.</span></span> <span data-ttu-id="71d58-155">If not specified, the name of the function is used.</span><span class="sxs-lookup"><span data-stu-id="71d58-155">If not specified, the name of the function is used.</span></span>

<span data-ttu-id="71d58-156">Internally this trigger binding polls a queue in the default storage account for the function app.</span><span class="sxs-lookup"><span data-stu-id="71d58-156">Internally this trigger binding polls a queue in the default storage account for the function app.</span></span> <span data-ttu-id="71d58-157">This queue is an internal implementation detail of the extension, which is why it is not explicitly configured in the binding properties.</span><span class="sxs-lookup"><span data-stu-id="71d58-157">This queue is an internal implementation detail of the extension, which is why it is not explicitly configured in the binding properties.</span></span>

### <a name="trigger-behavior"></a><span data-ttu-id="71d58-158">Trigger behavior</span><span class="sxs-lookup"><span data-stu-id="71d58-158">Trigger behavior</span></span>

<span data-ttu-id="71d58-159">Here are some notes about the activity trigger:</span><span class="sxs-lookup"><span data-stu-id="71d58-159">Here are some notes about the activity trigger:</span></span>

* <span data-ttu-id="71d58-160">**Threading** - Unlike the orchestration trigger, activity triggers don't have any restrictions around threading or I/O.</span><span class="sxs-lookup"><span data-stu-id="71d58-160">**Threading** - Unlike the orchestration trigger, activity triggers don't have any restrictions around threading or I/O.</span></span> <span data-ttu-id="71d58-161">They can be treated like regular functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-161">They can be treated like regular functions.</span></span>
* <span data-ttu-id="71d58-162">**Poising-message handling** - There is no poison message support in activity triggers.</span><span class="sxs-lookup"><span data-stu-id="71d58-162">**Poising-message handling** - There is no poison message support in activity triggers.</span></span>
* <span data-ttu-id="71d58-163">**Message visibility** - Activity trigger messages are dequeued and kept invisible for a configurable duration.</span><span class="sxs-lookup"><span data-stu-id="71d58-163">**Message visibility** - Activity trigger messages are dequeued and kept invisible for a configurable duration.</span></span> <span data-ttu-id="71d58-164">The visibility of these messages is renewed automatically as long as the function app is running and healthy.</span><span class="sxs-lookup"><span data-stu-id="71d58-164">The visibility of these messages is renewed automatically as long as the function app is running and healthy.</span></span>
* <span data-ttu-id="71d58-165">**Return values** - Return values are serialized to JSON and persisted to the orchestration history table in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="71d58-165">**Return values** - Return values are serialized to JSON and persisted to the orchestration history table in Azure Table storage.</span></span>

> [!WARNING]
> <span data-ttu-id="71d58-166">The storage backend for activity functions is an implementation detail and user code should not interact with these storage entities directly.</span><span class="sxs-lookup"><span data-stu-id="71d58-166">The storage backend for activity functions is an implementation detail and user code should not interact with these storage entities directly.</span></span>

### <a name="trigger-usage"></a><span data-ttu-id="71d58-167">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="71d58-167">Trigger usage</span></span>

<span data-ttu-id="71d58-168">The activity trigger binding supports both inputs and outputs, just like the orchestration trigger.</span><span class="sxs-lookup"><span data-stu-id="71d58-168">The activity trigger binding supports both inputs and outputs, just like the orchestration trigger.</span></span> <span data-ttu-id="71d58-169">Here are some things to know about input and output handling:</span><span class="sxs-lookup"><span data-stu-id="71d58-169">Here are some things to know about input and output handling:</span></span>

* <span data-ttu-id="71d58-170">**inputs** - Activity functions natively use [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) as a parameter type.</span><span class="sxs-lookup"><span data-stu-id="71d58-170">**inputs** - Activity functions natively use [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) as a parameter type.</span></span> <span data-ttu-id="71d58-171">Alternatively, an activity function can be declared with any parameter type that is JSON-serializable.</span><span class="sxs-lookup"><span data-stu-id="71d58-171">Alternatively, an activity function can be declared with any parameter type that is JSON-serializable.</span></span> <span data-ttu-id="71d58-172">When you use `DurableActivityContext`, you can call [GetInput\<T>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html#Microsoft_Azure_WebJobs_DurableActivityContext_GetInput__1) to fetch and deserialize the activity function input.</span><span class="sxs-lookup"><span data-stu-id="71d58-172">When you use `DurableActivityContext`, you can call [GetInput\<T>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html#Microsoft_Azure_WebJobs_DurableActivityContext_GetInput__1) to fetch and deserialize the activity function input.</span></span>
* <span data-ttu-id="71d58-173">**outputs** - Activity functions support output values as well as inputs.</span><span class="sxs-lookup"><span data-stu-id="71d58-173">**outputs** - Activity functions support output values as well as inputs.</span></span> <span data-ttu-id="71d58-174">The return value of the function is used to assign the output value and must be JSON-serializable.</span><span class="sxs-lookup"><span data-stu-id="71d58-174">The return value of the function is used to assign the output value and must be JSON-serializable.</span></span> <span data-ttu-id="71d58-175">If a function returns `Task` or `void`, a `null` value will be saved as the output.</span><span class="sxs-lookup"><span data-stu-id="71d58-175">If a function returns `Task` or `void`, a `null` value will be saved as the output.</span></span>
* <span data-ttu-id="71d58-176">**metadata** - Activity functions can bind to a `string instanceId` parameter to get the instance ID of the parent orchestration.</span><span class="sxs-lookup"><span data-stu-id="71d58-176">**metadata** - Activity functions can bind to a `string instanceId` parameter to get the instance ID of the parent orchestration.</span></span>

### <a name="trigger-sample"></a><span data-ttu-id="71d58-177">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="71d58-177">Trigger sample</span></span>

<span data-ttu-id="71d58-178">The following is an example of what a simple "Hello World" activity function might look like:</span><span class="sxs-lookup"><span data-stu-id="71d58-178">The following is an example of what a simple "Hello World" activity function might look like:</span></span>

#### <a name="c"></a><span data-ttu-id="71d58-179">C#</span><span class="sxs-lookup"><span data-stu-id="71d58-179">C#</span></span>

```csharp
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] DurableActivityContext helloContext)
{
    string name = helloContext.GetInput<string>();
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="71d58-180">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="71d58-180">JavaScript (Functions v2 only)</span></span>

```javascript
module.exports = function(context) {
    context.done(null, `Hello ${context.bindings.name}!`);
};
```

<span data-ttu-id="71d58-181">The default parameter type for the `ActivityTriggerAttribute` binding is `DurableActivityContext`.</span><span class="sxs-lookup"><span data-stu-id="71d58-181">The default parameter type for the `ActivityTriggerAttribute` binding is `DurableActivityContext`.</span></span> <span data-ttu-id="71d58-182">However, activity triggers also support binding directly to JSON-serializeable types (including primitive types), so the same function could be simplified as follows:</span><span class="sxs-lookup"><span data-stu-id="71d58-182">However, activity triggers also support binding directly to JSON-serializeable types (including primitive types), so the same function could be simplified as follows:</span></span>

#### <a name="c"></a><span data-ttu-id="71d58-183">C#</span><span class="sxs-lookup"><span data-stu-id="71d58-183">C#</span></span>

```csharp
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] string name)
{
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="71d58-184">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="71d58-184">JavaScript (Functions v2 only)</span></span>

```javascript
module.exports = function(context, name) {
    context.done(null, `Hello ${name}!`);
};
```

### <a name="passing-multiple-parameters"></a><span data-ttu-id="71d58-185">Passing multiple parameters</span><span class="sxs-lookup"><span data-stu-id="71d58-185">Passing multiple parameters</span></span> 

<span data-ttu-id="71d58-186">It is not possible to pass multiple parameters to an activity function directly.</span><span class="sxs-lookup"><span data-stu-id="71d58-186">It is not possible to pass multiple parameters to an activity function directly.</span></span> <span data-ttu-id="71d58-187">The recommendation in this case is to pass in an array of objects or to use [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) objects.</span><span class="sxs-lookup"><span data-stu-id="71d58-187">The recommendation in this case is to pass in an array of objects or to use [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) objects.</span></span>

<span data-ttu-id="71d58-188">The following sample is using new features of [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) added with [C# 7](https://docs.microsoft.com/dotnet/csharp/whats-new/csharp-7#tuples):</span><span class="sxs-lookup"><span data-stu-id="71d58-188">The following sample is using new features of [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) added with [C# 7](https://docs.microsoft.com/dotnet/csharp/whats-new/csharp-7#tuples):</span></span>

```csharp
[FunctionName("GetCourseRecommendations")]
public static async Task<dynamic> RunOrchestrator(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    string major = "ComputerScience";
    int universityYear = context.GetInput<int>();

    dynamic courseRecommendations = await context.CallActivityAsync<dynamic>("CourseRecommendations", (major, universityYear));
    return courseRecommendations;
}

[FunctionName("CourseRecommendations")]
public static async Task<dynamic> Mapper([ActivityTrigger] DurableActivityContext inputs)
{
    // parse input for student's major and year in university 
    (string Major, int UniversityYear) studentInfo = inputs.GetInput<(string, int)>();

    // retrieve and return course recommendations by major and university year
    return new {
        major = studentInfo.Major,
        universityYear = studentInfo.UniversityYear,
        recommendedCourses = new []
        {
            "Introduction to .NET Programming",
            "Introduction to Linux",
            "Becoming an Entrepreneur"
        }
    };
}
```

## <a name="orchestration-client"></a><span data-ttu-id="71d58-189">Orchestration client</span><span class="sxs-lookup"><span data-stu-id="71d58-189">Orchestration client</span></span>

<span data-ttu-id="71d58-190">The orchestration client binding enables you to write functions which interact with orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-190">The orchestration client binding enables you to write functions which interact with orchestrator functions.</span></span> <span data-ttu-id="71d58-191">For example, you can act on orchestration instances in the following ways:</span><span class="sxs-lookup"><span data-stu-id="71d58-191">For example, you can act on orchestration instances in the following ways:</span></span>
* <span data-ttu-id="71d58-192">Start them.</span><span class="sxs-lookup"><span data-stu-id="71d58-192">Start them.</span></span>
* <span data-ttu-id="71d58-193">Query their status.</span><span class="sxs-lookup"><span data-stu-id="71d58-193">Query their status.</span></span>
* <span data-ttu-id="71d58-194">Terminate them.</span><span class="sxs-lookup"><span data-stu-id="71d58-194">Terminate them.</span></span>
* <span data-ttu-id="71d58-195">Send events to them while they're running.</span><span class="sxs-lookup"><span data-stu-id="71d58-195">Send events to them while they're running.</span></span>

<span data-ttu-id="71d58-196">If you're using Visual Studio, you can bind to the orchestration client by using the [OrchestrationClientAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationClientAttribute.html) .NET attribute.</span><span class="sxs-lookup"><span data-stu-id="71d58-196">If you're using Visual Studio, you can bind to the orchestration client by using the [OrchestrationClientAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationClientAttribute.html) .NET attribute.</span></span>

<span data-ttu-id="71d58-197">If you're using scripting languages (e.g. *.csx* files) for development, the orchestration trigger is defined by the following JSON object in the `bindings` array of *function.json*:</span><span class="sxs-lookup"><span data-stu-id="71d58-197">If you're using scripting languages (e.g. *.csx* files) for development, the orchestration trigger is defined by the following JSON object in the `bindings` array of *function.json*:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "taskHub": "<Optional - name of the task hub>",
    "connectionName": "<Optional - name of the connection string app setting>",
    "type": "orchestrationClient",
    "direction": "out"
}
```

* <span data-ttu-id="71d58-198">`taskHub` - Used in scenarios where multiple function apps share the same storage account but need to be isolated from each other.</span><span class="sxs-lookup"><span data-stu-id="71d58-198">`taskHub` - Used in scenarios where multiple function apps share the same storage account but need to be isolated from each other.</span></span> <span data-ttu-id="71d58-199">If not specified, the default value from `host.json` is used.</span><span class="sxs-lookup"><span data-stu-id="71d58-199">If not specified, the default value from `host.json` is used.</span></span> <span data-ttu-id="71d58-200">This value must match the value used by the target orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-200">This value must match the value used by the target orchestrator functions.</span></span>
* <span data-ttu-id="71d58-201">`connectionName` - The name of an app setting that contains a storage account connection string.</span><span class="sxs-lookup"><span data-stu-id="71d58-201">`connectionName` - The name of an app setting that contains a storage account connection string.</span></span> <span data-ttu-id="71d58-202">The storage account represented by this connection string must be the same one used by the target orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-202">The storage account represented by this connection string must be the same one used by the target orchestrator functions.</span></span> <span data-ttu-id="71d58-203">If not specified, the default storage account connection string for the function app is used.</span><span class="sxs-lookup"><span data-stu-id="71d58-203">If not specified, the default storage account connection string for the function app is used.</span></span>

> [!NOTE]
> <span data-ttu-id="71d58-204">In most cases, we recommend that you omit these properties and rely on the default behavior.</span><span class="sxs-lookup"><span data-stu-id="71d58-204">In most cases, we recommend that you omit these properties and rely on the default behavior.</span></span>

### <a name="client-usage"></a><span data-ttu-id="71d58-205">Client usage</span><span class="sxs-lookup"><span data-stu-id="71d58-205">Client usage</span></span>

<span data-ttu-id="71d58-206">In C# functions, you typically bind to `DurableOrchestrationClient`, which gives you full access to all client APIs supported by Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="71d58-206">In C# functions, you typically bind to `DurableOrchestrationClient`, which gives you full access to all client APIs supported by Durable Functions.</span></span> <span data-ttu-id="71d58-207">APIs on the client object include:</span><span class="sxs-lookup"><span data-stu-id="71d58-207">APIs on the client object include:</span></span>

* [<span data-ttu-id="71d58-208">StartNewAsync</span><span class="sxs-lookup"><span data-stu-id="71d58-208">StartNewAsync</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_)
* [<span data-ttu-id="71d58-209">GetStatusAsync</span><span class="sxs-lookup"><span data-stu-id="71d58-209">GetStatusAsync</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_)
* [<span data-ttu-id="71d58-210">TerminateAsync</span><span class="sxs-lookup"><span data-stu-id="71d58-210">TerminateAsync</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_)
* [<span data-ttu-id="71d58-211">RaiseEventAsync</span><span class="sxs-lookup"><span data-stu-id="71d58-211">RaiseEventAsync</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_)

<span data-ttu-id="71d58-212">Alternatively, you can bind to `IAsyncCollector<T>` where `T` is [StartOrchestrationArgs](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.StartOrchestrationArgs.html) or `JObject`.</span><span class="sxs-lookup"><span data-stu-id="71d58-212">Alternatively, you can bind to `IAsyncCollector<T>` where `T` is [StartOrchestrationArgs](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.StartOrchestrationArgs.html) or `JObject`.</span></span>

<span data-ttu-id="71d58-213">See the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) API documentation for additional details on these operations.</span><span class="sxs-lookup"><span data-stu-id="71d58-213">See the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) API documentation for additional details on these operations.</span></span>

### <a name="client-sample-visual-studio-development"></a><span data-ttu-id="71d58-214">Client sample (Visual Studio development)</span><span class="sxs-lookup"><span data-stu-id="71d58-214">Client sample (Visual Studio development)</span></span>

<span data-ttu-id="71d58-215">Here is an example queue-triggered function that starts a "HelloWorld" orchestration.</span><span class="sxs-lookup"><span data-stu-id="71d58-215">Here is an example queue-triggered function that starts a "HelloWorld" orchestration.</span></span>

```csharp
[FunctionName("QueueStart")]
public static Task Run(
    [QueueTrigger("durable-function-trigger")] string input,
    [OrchestrationClient] DurableOrchestrationClient starter)
{
    // Orchestration input comes from the queue message content.
    return starter.StartNewAsync("HelloWorld", input);
}
```

### <a name="client-sample-not-visual-studio"></a><span data-ttu-id="71d58-216">Client sample (not Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="71d58-216">Client sample (not Visual Studio)</span></span>

<span data-ttu-id="71d58-217">If you're not using Visual Studio for development, you can create the following *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="71d58-217">If you're not using Visual Studio for development, you can create the following *function.json* file.</span></span> <span data-ttu-id="71d58-218">This example shows how to configure a queue-triggered function that uses the durable orchestration client binding:</span><span class="sxs-lookup"><span data-stu-id="71d58-218">This example shows how to configure a queue-triggered function that uses the durable orchestration client binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "queueTrigger",
      "queueName": "durable-function-trigger",
      "direction": "in"
    },
    {
      "name": "starter",
      "type": "orchestrationClient",
      "direction": "out"
    }
  ],
  "disabled": false
} 
```

<span data-ttu-id="71d58-219">Following are language-specific samples that start new orchestrator function instances.</span><span class="sxs-lookup"><span data-stu-id="71d58-219">Following are language-specific samples that start new orchestrator function instances.</span></span>

#### <a name="c-sample"></a><span data-ttu-id="71d58-220">C# Sample</span><span class="sxs-lookup"><span data-stu-id="71d58-220">C# Sample</span></span>

<span data-ttu-id="71d58-221">The following sample shows how to use the durable orchestration client binding to start a new function instance from a C# script function:</span><span class="sxs-lookup"><span data-stu-id="71d58-221">The following sample shows how to use the durable orchestration client binding to start a new function instance from a C# script function:</span></span>

```csharp
#r "Microsoft.Azure.WebJobs.Extensions.DurableTask"

public static Task<string> Run(string input, DurableOrchestrationClient starter)
{
    return starter.StartNewAsync("HelloWorld", input);
}
```

#### <a name="javascript-sample"></a><span data-ttu-id="71d58-222">JavaScript Sample</span><span class="sxs-lookup"><span data-stu-id="71d58-222">JavaScript Sample</span></span>

<span data-ttu-id="71d58-223">The following sample shows how to use the durable orchestration client binding to start a new function instance from a JavaScript function:</span><span class="sxs-lookup"><span data-stu-id="71d58-223">The following sample shows how to use the durable orchestration client binding to start a new function instance from a JavaScript function:</span></span>

```js
module.exports = function (context, input) {
    var id = generateSomeUniqueId();
    context.bindings.starter = [{
        FunctionName: "HelloWorld",
        Input: input,
        InstanceId: id
    }];

    context.done(null, id);
};
```

<span data-ttu-id="71d58-224">More details on starting instances can be found in [Instance management](durable-functions-instance-management.md).</span><span class="sxs-lookup"><span data-stu-id="71d58-224">More details on starting instances can be found in [Instance management](durable-functions-instance-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71d58-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="71d58-225">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71d58-226">Learn about checkpointing and replay behaviors</span><span class="sxs-lookup"><span data-stu-id="71d58-226">Learn about checkpointing and replay behaviors</span></span>](durable-functions-checkpointing-and-replay.md)

