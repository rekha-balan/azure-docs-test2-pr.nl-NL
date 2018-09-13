---
title: Manage instances in Durable Functions - Azure
description: Learn how to manage instances in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 08/31/2018
ms.author: azfuncdf
ms.openlocfilehash: 70ea13c1badf79c86bed53a34d9036706dbbac6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857762"
---
# <a name="manage-instances-in-durable-functions-azure-functions"></a><span data-ttu-id="7fcb1-103">Manage instances in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="7fcb1-103">Manage instances in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="7fcb1-104">[Durable Functions](durable-functions-overview.md) orchestration instances can be started, terminated, queried, and sent notification events.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-104">[Durable Functions](durable-functions-overview.md) orchestration instances can be started, terminated, queried, and sent notification events.</span></span> <span data-ttu-id="7fcb1-105">All instance management is done using the [orchestration client binding](durable-functions-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-105">All instance management is done using the [orchestration client binding](durable-functions-bindings.md).</span></span> <span data-ttu-id="7fcb1-106">This article goes into the details of each instance management operation.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-106">This article goes into the details of each instance management operation.</span></span>

## <a name="starting-instances"></a><span data-ttu-id="7fcb1-107">Starting instances</span><span class="sxs-lookup"><span data-stu-id="7fcb1-107">Starting instances</span></span>

<span data-ttu-id="7fcb1-108">The [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) method on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) starts a new instance of an orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-108">The [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) method on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) starts a new instance of an orchestrator function.</span></span> <span data-ttu-id="7fcb1-109">Instances of this class can be acquired using the `orchestrationClient` binding.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-109">Instances of this class can be acquired using the `orchestrationClient` binding.</span></span> <span data-ttu-id="7fcb1-110">Internally, this method enqueues a message into the control queue, which then triggers the start of a function with the specified name that uses the `orchestrationTrigger` trigger binding.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-110">Internally, this method enqueues a message into the control queue, which then triggers the start of a function with the specified name that uses the `orchestrationTrigger` trigger binding.</span></span> 

<span data-ttu-id="7fcb1-111">The task completes when the orchestration process is started.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-111">The task completes when the orchestration process is started.</span></span> <span data-ttu-id="7fcb1-112">The orchestration process should start within 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-112">The orchestration process should start within 30 seconds.</span></span> <span data-ttu-id="7fcb1-113">If it takes longer, a `TimeoutException` is thrown.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-113">If it takes longer, a `TimeoutException` is thrown.</span></span> 

<span data-ttu-id="7fcb1-114">The parameters to [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) are as follows:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-114">The parameters to [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) are as follows:</span></span>

* <span data-ttu-id="7fcb1-115">**Name**: The name of the orchestrator function to schedule.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-115">**Name**: The name of the orchestrator function to schedule.</span></span>
* <span data-ttu-id="7fcb1-116">**Input**: Any JSON-serializable data that should be passed as the input to the orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-116">**Input**: Any JSON-serializable data that should be passed as the input to the orchestrator function.</span></span>
* <span data-ttu-id="7fcb1-117">**InstanceId**: (Optional) The unique ID of the instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-117">**InstanceId**: (Optional) The unique ID of the instance.</span></span> <span data-ttu-id="7fcb1-118">If not specified, a random instance ID will be generated.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-118">If not specified, a random instance ID will be generated.</span></span>

<span data-ttu-id="7fcb1-119">Here is a simple C# example:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-119">Here is a simple C# example:</span></span>

```csharp
[FunctionName("HelloWorldManualStart")]
public static async Task Run(
    [ManualTrigger] string input,
    [OrchestrationClient] DurableOrchestrationClient starter,
    TraceWriter log)
{
    string instanceId = await starter.StartNewAsync("HelloWorld", input);
    log.Info($"Started orchestration with ID = '{instanceId}'.");
}
```

<span data-ttu-id="7fcb1-120">For non-.NET languages, the function output binding can be used to start new instances as well.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-120">For non-.NET languages, the function output binding can be used to start new instances as well.</span></span> <span data-ttu-id="7fcb1-121">In this case, any JSON-serializable object that has the above three parameters as fields can be used.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-121">In this case, any JSON-serializable object that has the above three parameters as fields can be used.</span></span> <span data-ttu-id="7fcb1-122">For example, consider the following JavaScript function:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-122">For example, consider the following JavaScript function:</span></span>

```js
module.exports = function (context, input) {
    var id = generateSomeUniqueId();
    context.bindings.starter = [{
        FunctionName: "HelloWorld",
        Input: input,
        InstanceId: id
    }];

    context.done(null);
};
```

> [!NOTE]
> <span data-ttu-id="7fcb1-123">We recommend that you use a random identifier for the instance ID.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-123">We recommend that you use a random identifier for the instance ID.</span></span> <span data-ttu-id="7fcb1-124">This will help ensure an equal load distribution when scaling orchestrator functions across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-124">This will help ensure an equal load distribution when scaling orchestrator functions across multiple VMs.</span></span> <span data-ttu-id="7fcb1-125">The proper time to use non-random instance IDs is when the ID must come from an external source or when implementing the [singleton orchestrator](durable-functions-singletons.md) pattern.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-125">The proper time to use non-random instance IDs is when the ID must come from an external source or when implementing the [singleton orchestrator](durable-functions-singletons.md) pattern.</span></span>

## <a name="querying-instances"></a><span data-ttu-id="7fcb1-126">Querying instances</span><span class="sxs-lookup"><span data-stu-id="7fcb1-126">Querying instances</span></span>

<span data-ttu-id="7fcb1-127">The [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_) method on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class queries the status of an orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-127">The [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_) method on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class queries the status of an orchestration instance.</span></span> <span data-ttu-id="7fcb1-128">It takes an `instanceId` (required), `showHistory` (optional), and `showHistoryOutput` (optional) as parameters.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-128">It takes an `instanceId` (required), `showHistory` (optional), and `showHistoryOutput` (optional) as parameters.</span></span> <span data-ttu-id="7fcb1-129">If `showHistory` is set to `true`, the response will contain the execution history.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-129">If `showHistory` is set to `true`, the response will contain the execution history.</span></span> <span data-ttu-id="7fcb1-130">If `showHistoryOutput` is set to `true` as well, the execution history will contain activity outputs.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-130">If `showHistoryOutput` is set to `true` as well, the execution history will contain activity outputs.</span></span> <span data-ttu-id="7fcb1-131">The method returns an object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-131">The method returns an object with the following properties:</span></span>

* <span data-ttu-id="7fcb1-132">**Name**: The name of the orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-132">**Name**: The name of the orchestrator function.</span></span>
* <span data-ttu-id="7fcb1-133">**InstanceId**: The instance ID of the orchestration (should be the same as the `instanceId` input).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-133">**InstanceId**: The instance ID of the orchestration (should be the same as the `instanceId` input).</span></span>
* <span data-ttu-id="7fcb1-134">**CreatedTime**: The time at which the orchestrator function started running.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-134">**CreatedTime**: The time at which the orchestrator function started running.</span></span>
* <span data-ttu-id="7fcb1-135">**LastUpdatedTime**: The time at which the orchestration last checkpointed.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-135">**LastUpdatedTime**: The time at which the orchestration last checkpointed.</span></span>
* <span data-ttu-id="7fcb1-136">**Input**: The input of the function as a JSON value.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-136">**Input**: The input of the function as a JSON value.</span></span>
* <span data-ttu-id="7fcb1-137">**CustomStatus**: Custom orchestration status in JSON format.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-137">**CustomStatus**: Custom orchestration status in JSON format.</span></span> 
* <span data-ttu-id="7fcb1-138">**Output**: The output of the function as a JSON value (if the function has completed).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-138">**Output**: The output of the function as a JSON value (if the function has completed).</span></span> <span data-ttu-id="7fcb1-139">If the orchestrator function failed, this property will include the failure details.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-139">If the orchestrator function failed, this property will include the failure details.</span></span> <span data-ttu-id="7fcb1-140">If the orchestrator function was terminated, this property will include the provided reason for the termination (if any).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-140">If the orchestrator function was terminated, this property will include the provided reason for the termination (if any).</span></span>
* <span data-ttu-id="7fcb1-141">**RuntimeStatus**: One of the following values:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-141">**RuntimeStatus**: One of the following values:</span></span>
    * <span data-ttu-id="7fcb1-142">**Pending**: The instance has been scheduled but has not yet started running.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-142">**Pending**: The instance has been scheduled but has not yet started running.</span></span>
    * <span data-ttu-id="7fcb1-143">**Running**: The instance has started running.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-143">**Running**: The instance has started running.</span></span>
    * <span data-ttu-id="7fcb1-144">**Completed**: The instance has completed normally.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-144">**Completed**: The instance has completed normally.</span></span>
    * <span data-ttu-id="7fcb1-145">**ContinuedAsNew**: The instance has restarted itself with a new history.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-145">**ContinuedAsNew**: The instance has restarted itself with a new history.</span></span> <span data-ttu-id="7fcb1-146">This is a transient state.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-146">This is a transient state.</span></span>
    * <span data-ttu-id="7fcb1-147">**Failed**: The instance failed with an error.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-147">**Failed**: The instance failed with an error.</span></span>
    * <span data-ttu-id="7fcb1-148">**Terminated**: The instance was abruptly terminated.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-148">**Terminated**: The instance was abruptly terminated.</span></span>
* <span data-ttu-id="7fcb1-149">**History**: The execution history of the orchestration.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-149">**History**: The execution history of the orchestration.</span></span> <span data-ttu-id="7fcb1-150">This field is only populated if `showHistory` is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-150">This field is only populated if `showHistory` is set to `true`.</span></span>
    
<span data-ttu-id="7fcb1-151">This method returns `null` if the instance either doesn't exist or has not yet started running.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-151">This method returns `null` if the instance either doesn't exist or has not yet started running.</span></span>

```csharp
[FunctionName("GetStatus")]
public static async Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    var status = await client.GetStatusAsync(instanceId);
    // do something based on the current status.
}
```
## <a name="querying-all-instances"></a><span data-ttu-id="7fcb1-152">Querying all instances</span><span class="sxs-lookup"><span data-stu-id="7fcb1-152">Querying all instances</span></span>

<span data-ttu-id="7fcb1-153">You can use the `GetStatusAsync` method to query the statuses of all orchestration instances.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-153">You can use the `GetStatusAsync` method to query the statuses of all orchestration instances.</span></span> <span data-ttu-id="7fcb1-154">It doesn't take any parameters, or you can pass a `CancellationToken` object in case you want to cancel it.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-154">It doesn't take any parameters, or you can pass a `CancellationToken` object in case you want to cancel it.</span></span> <span data-ttu-id="7fcb1-155">The method returns objects with the same properties as the `GetStatusAsync` method with parameters, except it doesn't return history.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-155">The method returns objects with the same properties as the `GetStatusAsync` method with parameters, except it doesn't return history.</span></span> 

```csharp
[FunctionName("GetAllStatus")]
public static async Task Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")]HttpRequestMessage req,
    [OrchestrationClient] DurableOrchestrationClient client,
    TraceWriter log)
{
    IList<DurableOrchestrationStatus> instances = await starter.GetStatusAsync(); // You can pass CancellationToken as a parameter.
    foreach (var instance in instances)
    {
        log.Info(JsonConvert.SerializeObject(instance));
    };
}
```

## <a name="terminating-instances"></a><span data-ttu-id="7fcb1-156">Terminating instances</span><span class="sxs-lookup"><span data-stu-id="7fcb1-156">Terminating instances</span></span>

<span data-ttu-id="7fcb1-157">A running orchestration instance can be terminated using the [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-157">A running orchestration instance can be terminated using the [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span></span> <span data-ttu-id="7fcb1-158">The two parameters are an `instanceId` and a `reason` string, which will be written to logs and to the instance status.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-158">The two parameters are an `instanceId` and a `reason` string, which will be written to logs and to the instance status.</span></span> <span data-ttu-id="7fcb1-159">A terminated instance will stop running as soon as it reaches the next `await` point, or it will terminate immediately if it is already on an `await`.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-159">A terminated instance will stop running as soon as it reaches the next `await` point, or it will terminate immediately if it is already on an `await`.</span></span> 

```csharp
[FunctionName("TerminateInstance")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    string reason = "It was time to be done.";
    return client.TerminateAsync(instanceId, reason);
}
```

> [!NOTE]
> <span data-ttu-id="7fcb1-160">Instance termination does not currently propagate.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-160">Instance termination does not currently propagate.</span></span> <span data-ttu-id="7fcb1-161">Activity functions and sub-orchestrations will run to completion regardless of whether the orchestration instance that called them has been terminated.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-161">Activity functions and sub-orchestrations will run to completion regardless of whether the orchestration instance that called them has been terminated.</span></span>

## <a name="sending-events-to-instances"></a><span data-ttu-id="7fcb1-162">Sending events to instances</span><span class="sxs-lookup"><span data-stu-id="7fcb1-162">Sending events to instances</span></span>

<span data-ttu-id="7fcb1-163">Event notifications can be sent to running instances using the [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-163">Event notifications can be sent to running instances using the [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span></span> <span data-ttu-id="7fcb1-164">Instances that can handle these events are those that are awaiting a call to [WaitForExternalEvent](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_WaitForExternalEvent_).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-164">Instances that can handle these events are those that are awaiting a call to [WaitForExternalEvent](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_WaitForExternalEvent_).</span></span> 

<span data-ttu-id="7fcb1-165">The parameters to [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) are as follows:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-165">The parameters to [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) are as follows:</span></span>

* <span data-ttu-id="7fcb1-166">**InstanceId**: The unique ID of the instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-166">**InstanceId**: The unique ID of the instance.</span></span>
* <span data-ttu-id="7fcb1-167">**EventName**: The name of the event to send.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-167">**EventName**: The name of the event to send.</span></span>
* <span data-ttu-id="7fcb1-168">**EventData**: A JSON-serializable payload to send to the instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-168">**EventData**: A JSON-serializable payload to send to the instance.</span></span>

```csharp
[FunctionName("RaiseEvent")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    int[] eventData = new int[] { 1, 2, 3 };
    return client.RaiseEventAsync(instanceId, "MyEvent", eventData);
}
```

> [!WARNING]
> <span data-ttu-id="7fcb1-169">If there is no orchestration instance with the specified *instance ID* or if the instance is not waiting on the specified *event name*, the event message is discarded.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-169">If there is no orchestration instance with the specified *instance ID* or if the instance is not waiting on the specified *event name*, the event message is discarded.</span></span> <span data-ttu-id="7fcb1-170">For more information about this behavior, see the [GitHub issue](https://github.com/Azure/azure-functions-durable-extension/issues/29).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-170">For more information about this behavior, see the [GitHub issue](https://github.com/Azure/azure-functions-durable-extension/issues/29).</span></span>

## <a name="wait-for-orchestration-completion"></a><span data-ttu-id="7fcb1-171">Wait for orchestration completion</span><span class="sxs-lookup"><span data-stu-id="7fcb1-171">Wait for orchestration completion</span></span>

<span data-ttu-id="7fcb1-172">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class exposes a [WaitForCompletionOrCreateCheckStatusResponseAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_WaitForCompletionOrCreateCheckStatusResponseAsync_) API that can be used to get synchronously the actual output from an orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-172">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class exposes a [WaitForCompletionOrCreateCheckStatusResponseAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_WaitForCompletionOrCreateCheckStatusResponseAsync_) API that can be used to get synchronously the actual output from an orchestration instance.</span></span> <span data-ttu-id="7fcb1-173">The method uses default value of 10 seconds for `timeout` and 1 second for `retryInterval` when they are not set.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-173">The method uses default value of 10 seconds for `timeout` and 1 second for `retryInterval` when they are not set.</span></span>  

<span data-ttu-id="7fcb1-174">Here is an example HTTP-trigger function that demonstrates how to use this API:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-174">Here is an example HTTP-trigger function that demonstrates how to use this API:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HttpSyncStart.cs)]

<span data-ttu-id="7fcb1-175">The function can be called with the following line using 2-seconds timeout and 0.5-second retry interval:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-175">The function can be called with the following line using 2-seconds timeout and 0.5-second retry interval:</span></span>

```bash
    http POST http://localhost:7071/orchestrators/E1_HelloSequence/wait?timeout=2&retryInterval=0.5
```

<span data-ttu-id="7fcb1-176">Depending on the time required to get the response from the orchestration instance there are two cases:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-176">Depending on the time required to get the response from the orchestration instance there are two cases:</span></span>

1. <span data-ttu-id="7fcb1-177">The orchestration instances complete within the defined timeout (in this case 2 seconds), the response is the actual orchestration instance output delivered synchronously:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-177">The orchestration instances complete within the defined timeout (in this case 2 seconds), the response is the actual orchestration instance output delivered synchronously:</span></span>

    ```http
        HTTP/1.1 200 OK
        Content-Type: application/json; charset=utf-8
        Date: Thu, 14 Dec 2017 06:14:29 GMT
        Server: Microsoft-HTTPAPI/2.0
        Transfer-Encoding: chunked

        [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ]
    ```

2. <span data-ttu-id="7fcb1-178">The orchestration instances cannot complete within the defined timeout (in this case 2 seconds), the response is the default one described in **HTTP API URL discovery**:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-178">The orchestration instances cannot complete within the defined timeout (in this case 2 seconds), the response is the default one described in **HTTP API URL discovery**:</span></span>

    ```http
        HTTP/1.1 202 Accepted
        Content-Type: application/json; charset=utf-8
        Date: Thu, 14 Dec 2017 06:13:51 GMT
        Location: http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}
        Retry-After: 10
        Server: Microsoft-HTTPAPI/2.0
        Transfer-Encoding: chunked

        {
            "id": "d3b72dddefce4e758d92f4d411567177",
            "sendEventPostUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/raiseEvent/{eventName}?taskHub={taskHub}&connection={connection}&code={systemKey}",
            "statusQueryGetUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}",
            "terminatePostUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/terminate?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}",
            "rewindPostUri": "https://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/rewind?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}"
        }
    ```

> [!NOTE]
> <span data-ttu-id="7fcb1-179">The format of the webhook URLs may differ depending on which version of the Azure Functions host you are running.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-179">The format of the webhook URLs may differ depending on which version of the Azure Functions host you are running.</span></span> <span data-ttu-id="7fcb1-180">The preceding example is for the Azure Functions 2.0 host.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-180">The preceding example is for the Azure Functions 2.0 host.</span></span>

## <a name="retrieving-http-management-webhook-urls"></a><span data-ttu-id="7fcb1-181">Retrieving HTTP Management Webhook URLs</span><span class="sxs-lookup"><span data-stu-id="7fcb1-181">Retrieving HTTP Management Webhook URLs</span></span>

<span data-ttu-id="7fcb1-182">External systems can communicate with Durable Functions via the webhook URLs that are part of the default response described in [HTTP API URL discovery](durable-functions-http-api.md).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-182">External systems can communicate with Durable Functions via the webhook URLs that are part of the default response described in [HTTP API URL discovery](durable-functions-http-api.md).</span></span> <span data-ttu-id="7fcb1-183">However, the webhook URLs also can be accessed programmatically in the orchestration client or in an activity function via the [CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-183">However, the webhook URLs also can be accessed programmatically in the orchestration client or in an activity function via the [CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_) method of the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span></span> 

<span data-ttu-id="7fcb1-184">[CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_) has one parameter:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-184">[CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_) has one parameter:</span></span>

* <span data-ttu-id="7fcb1-185">**instanceId**: The unique ID of the instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-185">**instanceId**: The unique ID of the instance.</span></span>

<span data-ttu-id="7fcb1-186">The method returns an instance of the [HttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.Extensions.DurableTask.HttpManagementPayload.html#Microsoft_Azure_WebJobs_Extensions_DurableTask_HttpManagementPayload_) with the following string properties:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-186">The method returns an instance of the [HttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.Extensions.DurableTask.HttpManagementPayload.html#Microsoft_Azure_WebJobs_Extensions_DurableTask_HttpManagementPayload_) with the following string properties:</span></span>

* <span data-ttu-id="7fcb1-187">**Id**: The instance ID of the orchestration (should be the same as the `InstanceId` input).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-187">**Id**: The instance ID of the orchestration (should be the same as the `InstanceId` input).</span></span>
* <span data-ttu-id="7fcb1-188">**StatusQueryGetUri**: The status URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-188">**StatusQueryGetUri**: The status URL of the orchestration instance.</span></span>
* <span data-ttu-id="7fcb1-189">**SendEventPostUri**: The "raise event" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-189">**SendEventPostUri**: The "raise event" URL of the orchestration instance.</span></span>
* <span data-ttu-id="7fcb1-190">**TerminatePostUri**: The "terminate" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-190">**TerminatePostUri**: The "terminate" URL of the orchestration instance.</span></span>
* <span data-ttu-id="7fcb1-191">**RewindPostUri**: The "rewind" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-191">**RewindPostUri**: The "rewind" URL of the orchestration instance.</span></span>

<span data-ttu-id="7fcb1-192">Activity functions can send an instance of [HttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.Extensions.DurableTask.HttpManagementPayload.html#Microsoft_Azure_WebJobs_Extensions_DurableTask_HttpManagementPayload_) to external systems to monitor or raise events to an orchestration:</span><span class="sxs-lookup"><span data-stu-id="7fcb1-192">Activity functions can send an instance of [HttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.Extensions.DurableTask.HttpManagementPayload.html#Microsoft_Azure_WebJobs_Extensions_DurableTask_HttpManagementPayload_) to external systems to monitor or raise events to an orchestration:</span></span>

```csharp
[FunctionName("SendInstanceInfo")]
public static void SendInstanceInfo(
    [ActivityTrigger] DurableActivityContext ctx,
    [OrchestrationClient] DurableOrchestrationClient client,
    [DocumentDB(
        databaseName: "MonitorDB",
        collectionName: "HttpManagementPayloads",
        ConnectionStringSetting = "CosmosDBConnection")]out dynamic document)
{
    HttpManagementPayload payload = client.CreateHttpManagementPayload(ctx.InstanceId);

    // send the payload to Cosmos DB
    document = new { Payload = payload, id = ctx.InstanceId };
}
```

## <a name="rewinding-instances-preview"></a><span data-ttu-id="7fcb1-193">Rewinding instances (preview)</span><span class="sxs-lookup"><span data-stu-id="7fcb1-193">Rewinding instances (preview)</span></span>

<span data-ttu-id="7fcb1-194">A failed orchestration instance can be *rewound* into a previously healthy state using the [RewindAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RewindAsync_System_String_System_String_) API.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-194">A failed orchestration instance can be *rewound* into a previously healthy state using the [RewindAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RewindAsync_System_String_System_String_) API.</span></span> <span data-ttu-id="7fcb1-195">It works by putting the orchestration back into the *Running* state and re-running the activity and/or sub-orchestration execution failures that caused the orchestration failure.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-195">It works by putting the orchestration back into the *Running* state and re-running the activity and/or sub-orchestration execution failures that caused the orchestration failure.</span></span>

> [!NOTE]
> <span data-ttu-id="7fcb1-196">This API is not intended to be a replacement for proper error handling and retry policies.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-196">This API is not intended to be a replacement for proper error handling and retry policies.</span></span> <span data-ttu-id="7fcb1-197">Rather, it is intended to be used only in cases where orchestration instances fail for unexpected reasons.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-197">Rather, it is intended to be used only in cases where orchestration instances fail for unexpected reasons.</span></span> <span data-ttu-id="7fcb1-198">For more details on error handling and retry policies, please see the [Error handling](durable-functions-error-handling.md) topic.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-198">For more details on error handling and retry policies, please see the [Error handling](durable-functions-error-handling.md) topic.</span></span>

<span data-ttu-id="7fcb1-199">One example use case for *rewind* is a workflow involving a series of [human approvals](durable-functions-overview.md#pattern-5-human-interaction).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-199">One example use case for *rewind* is a workflow involving a series of [human approvals](durable-functions-overview.md#pattern-5-human-interaction).</span></span> <span data-ttu-id="7fcb1-200">Suppose there are a series of activity functions that notify someone that their approval is needed and wait out the real-time response.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-200">Suppose there are a series of activity functions that notify someone that their approval is needed and wait out the real-time response.</span></span> <span data-ttu-id="7fcb1-201">After all of the approval activities have received responses or timed out, another activity fails due to an application misconfiguration (e.g. an invalid database connection string).</span><span class="sxs-lookup"><span data-stu-id="7fcb1-201">After all of the approval activities have received responses or timed out, another activity fails due to an application misconfiguration (e.g. an invalid database connection string).</span></span> <span data-ttu-id="7fcb1-202">The result is an orchestration failure deep into the workflow.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-202">The result is an orchestration failure deep into the workflow.</span></span> <span data-ttu-id="7fcb1-203">With the `RewindAsync` API, an application administrator can fix the configuration error and *rewind* the failed orchestration back to the state immediately before the failure.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-203">With the `RewindAsync` API, an application administrator can fix the configuration error and *rewind* the failed orchestration back to the state immediately before the failure.</span></span> <span data-ttu-id="7fcb1-204">None of the human-interaction steps need to be re-approved and the orchestration can now complete successfully.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-204">None of the human-interaction steps need to be re-approved and the orchestration can now complete successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="7fcb1-205">The *rewind* feature does not support rewinding orchestration instances that use durable timers.</span><span class="sxs-lookup"><span data-stu-id="7fcb1-205">The *rewind* feature does not support rewinding orchestration instances that use durable timers.</span></span>

```csharp
[FunctionName("RewindInstance")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    string reason = "Orchestrator failed and needs to be revived.";
    return client.RewindAsync(instanceId, reason);
}
```

## <a name="next-steps"></a><span data-ttu-id="7fcb1-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fcb1-206">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fcb1-207">Learn how to use the HTTP APIs for instance management</span><span class="sxs-lookup"><span data-stu-id="7fcb1-207">Learn how to use the HTTP APIs for instance management</span></span>](durable-functions-http-api.md)
