---
title: HTTP APIs in Durable Functions - Azure
description: Learn how to implement HTTP APIs in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: azfuncdf
ms.openlocfilehash: 29fd4e62c13852e23e15f89ab6b4e2976fc42b25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864342"
---
# <a name="http-apis-in-durable-functions-azure-functions"></a><span data-ttu-id="7258a-103">HTTP APIs in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="7258a-103">HTTP APIs in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="7258a-104">The Durable Task extension exposes a set of HTTP APIs that can be used to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="7258a-104">The Durable Task extension exposes a set of HTTP APIs that can be used to perform the following tasks:</span></span>

* <span data-ttu-id="7258a-105">Fetch the status of an orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-105">Fetch the status of an orchestration instance.</span></span>
* <span data-ttu-id="7258a-106">Send an event to a waiting orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-106">Send an event to a waiting orchestration instance.</span></span>
* <span data-ttu-id="7258a-107">Terminate a running orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-107">Terminate a running orchestration instance.</span></span>


<span data-ttu-id="7258a-108">Each of these HTTP APIs is a webhook operation that is handled directly by the Durable Task extension.</span><span class="sxs-lookup"><span data-stu-id="7258a-108">Each of these HTTP APIs is a webhook operation that is handled directly by the Durable Task extension.</span></span> <span data-ttu-id="7258a-109">They are not specific to any function in the function app.</span><span class="sxs-lookup"><span data-stu-id="7258a-109">They are not specific to any function in the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="7258a-110">These operations can also be invoked directly using the instance management APIs on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span><span class="sxs-lookup"><span data-stu-id="7258a-110">These operations can also be invoked directly using the instance management APIs on the [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) class.</span></span> <span data-ttu-id="7258a-111">For more information, see [Instance Management](durable-functions-instance-management.md).</span><span class="sxs-lookup"><span data-stu-id="7258a-111">For more information, see [Instance Management](durable-functions-instance-management.md).</span></span>

## <a name="http-api-url-discovery"></a><span data-ttu-id="7258a-112">HTTP API URL discovery</span><span class="sxs-lookup"><span data-stu-id="7258a-112">HTTP API URL discovery</span></span>

<span data-ttu-id="7258a-113">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)  class exposes a [CreateCheckStatusResponse](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateCheckStatusResponse_) API that can be used to generate an HTTP response payload containing links to all the supported operations.</span><span class="sxs-lookup"><span data-stu-id="7258a-113">The [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)  class exposes a [CreateCheckStatusResponse](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateCheckStatusResponse_) API that can be used to generate an HTTP response payload containing links to all the supported operations.</span></span> <span data-ttu-id="7258a-114">Here is an example HTTP-trigger function that demonstrates how to use this API:</span><span class="sxs-lookup"><span data-stu-id="7258a-114">Here is an example HTTP-trigger function that demonstrates how to use this API:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/HttpStart/run.csx)]

<span data-ttu-id="7258a-115">This example function produces the following JSON response data.</span><span class="sxs-lookup"><span data-stu-id="7258a-115">This example function produces the following JSON response data.</span></span> <span data-ttu-id="7258a-116">The data type of all fields is `string`.</span><span class="sxs-lookup"><span data-stu-id="7258a-116">The data type of all fields is `string`.</span></span>

| <span data-ttu-id="7258a-117">Field</span><span class="sxs-lookup"><span data-stu-id="7258a-117">Field</span></span>             |<span data-ttu-id="7258a-118">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-118">Description</span></span>                           |
|-------------------|--------------------------------------|
| <span data-ttu-id="7258a-119">id</span><span class="sxs-lookup"><span data-stu-id="7258a-119">id</span></span>                |<span data-ttu-id="7258a-120">The ID of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-120">The ID of the orchestration instance.</span></span> |
| <span data-ttu-id="7258a-121">statusQueryGetUri</span><span class="sxs-lookup"><span data-stu-id="7258a-121">statusQueryGetUri</span></span> |<span data-ttu-id="7258a-122">The status URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-122">The status URL of the orchestration instance.</span></span> |
| <span data-ttu-id="7258a-123">sendEventPostUri</span><span class="sxs-lookup"><span data-stu-id="7258a-123">sendEventPostUri</span></span>  |<span data-ttu-id="7258a-124">The "raise event" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-124">The "raise event" URL of the orchestration instance.</span></span> |
| <span data-ttu-id="7258a-125">terminatePostUri</span><span class="sxs-lookup"><span data-stu-id="7258a-125">terminatePostUri</span></span>  |<span data-ttu-id="7258a-126">The "terminate" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-126">The "terminate" URL of the orchestration instance.</span></span> |
| <span data-ttu-id="7258a-127">rewindPostUri</span><span class="sxs-lookup"><span data-stu-id="7258a-127">rewindPostUri</span></span>     |<span data-ttu-id="7258a-128">The "rewind" URL of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-128">The "rewind" URL of the orchestration instance.</span></span> |

<span data-ttu-id="7258a-129">Here is an example response:</span><span class="sxs-lookup"><span data-stu-id="7258a-129">Here is an example response:</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 923
Content-Type: application/json; charset=utf-8
Location: https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2?taskHub=DurableFunctionsHub&connection=Storage&code=XXX

{
    "id":"34ce9a28a6834d8492ce6a295f1a80e2",
    "statusQueryGetUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2?taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "sendEventPostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "terminatePostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/terminate?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code=XXX",
    "rewindPostUri":"https://{host}/runtime/webhooks/durabletask/instances/34ce9a28a6834d8492ce6a295f1a80e2/rewind?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code=XXX"
}
```
> [!NOTE]
> <span data-ttu-id="7258a-130">The format of the webhook URLs may differ depending on which version of the Azure Functions host you are running.</span><span class="sxs-lookup"><span data-stu-id="7258a-130">The format of the webhook URLs may differ depending on which version of the Azure Functions host you are running.</span></span> <span data-ttu-id="7258a-131">The above example is for the Azure Functions 2.0 host.</span><span class="sxs-lookup"><span data-stu-id="7258a-131">The above example is for the Azure Functions 2.0 host.</span></span>

## <a name="async-operation-tracking"></a><span data-ttu-id="7258a-132">Async operation tracking</span><span class="sxs-lookup"><span data-stu-id="7258a-132">Async operation tracking</span></span>

<span data-ttu-id="7258a-133">The HTTP response mentioned previously is designed to help implementing long-running HTTP async APIs with Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="7258a-133">The HTTP response mentioned previously is designed to help implementing long-running HTTP async APIs with Durable Functions.</span></span> <span data-ttu-id="7258a-134">This is sometimes referred to as the *Polling Consumer Pattern*.</span><span class="sxs-lookup"><span data-stu-id="7258a-134">This is sometimes referred to as the *Polling Consumer Pattern*.</span></span> <span data-ttu-id="7258a-135">The client/server flow works as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-135">The client/server flow works as follows:</span></span>

1. <span data-ttu-id="7258a-136">The client issues an HTTP request to start a long running process, such as an orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="7258a-136">The client issues an HTTP request to start a long running process, such as an orchestrator function.</span></span>
2. <span data-ttu-id="7258a-137">The target HTTP trigger returns an HTTP 202 response with a `Location` header with the `statusQueryGetUri` value.</span><span class="sxs-lookup"><span data-stu-id="7258a-137">The target HTTP trigger returns an HTTP 202 response with a `Location` header with the `statusQueryGetUri` value.</span></span>
3. <span data-ttu-id="7258a-138">The client polls the URL in the `Location` header.</span><span class="sxs-lookup"><span data-stu-id="7258a-138">The client polls the URL in the `Location` header.</span></span> <span data-ttu-id="7258a-139">It continues to see HTTP 202 responses with a `Location` header.</span><span class="sxs-lookup"><span data-stu-id="7258a-139">It continues to see HTTP 202 responses with a `Location` header.</span></span>
4. <span data-ttu-id="7258a-140">When the instance completes (or fails), the endpoint in the `Location` header returns HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="7258a-140">When the instance completes (or fails), the endpoint in the `Location` header returns HTTP 200.</span></span>

<span data-ttu-id="7258a-141">This protocol allows coordinating long-running processes with external clients or services that support polling an HTTP endpoint and following the `Location` header.</span><span class="sxs-lookup"><span data-stu-id="7258a-141">This protocol allows coordinating long-running processes with external clients or services that support polling an HTTP endpoint and following the `Location` header.</span></span> <span data-ttu-id="7258a-142">The fundamental pieces are already built into the Durable Functions HTTP APIs.</span><span class="sxs-lookup"><span data-stu-id="7258a-142">The fundamental pieces are already built into the Durable Functions HTTP APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="7258a-143">By default, all HTTP-based actions provided by [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/) support the standard asynchronous operation pattern.</span><span class="sxs-lookup"><span data-stu-id="7258a-143">By default, all HTTP-based actions provided by [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/) support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="7258a-144">This capability makes it possible to embed a long-running durable function as part of a Logic Apps workflow.</span><span class="sxs-lookup"><span data-stu-id="7258a-144">This capability makes it possible to embed a long-running durable function as part of a Logic Apps workflow.</span></span> <span data-ttu-id="7258a-145">More details on Logic Apps support for asynchronous HTTP patterns can be found in the [Azure Logic Apps workflow actions and triggers documentation](../logic-apps/logic-apps-workflow-actions-triggers.md#asynchronous-patterns).</span><span class="sxs-lookup"><span data-stu-id="7258a-145">More details on Logic Apps support for asynchronous HTTP patterns can be found in the [Azure Logic Apps workflow actions and triggers documentation](../logic-apps/logic-apps-workflow-actions-triggers.md#asynchronous-patterns).</span></span>

## <a name="http-api-reference"></a><span data-ttu-id="7258a-146">HTTP API reference</span><span class="sxs-lookup"><span data-stu-id="7258a-146">HTTP API reference</span></span>

<span data-ttu-id="7258a-147">All HTTP APIs implemented by the extension take the following parameters.</span><span class="sxs-lookup"><span data-stu-id="7258a-147">All HTTP APIs implemented by the extension take the following parameters.</span></span> <span data-ttu-id="7258a-148">The data type of all parameters is `string`.</span><span class="sxs-lookup"><span data-stu-id="7258a-148">The data type of all parameters is `string`.</span></span>

| <span data-ttu-id="7258a-149">Parameter</span><span class="sxs-lookup"><span data-stu-id="7258a-149">Parameter</span></span>  | <span data-ttu-id="7258a-150">Parameter Type</span><span class="sxs-lookup"><span data-stu-id="7258a-150">Parameter Type</span></span>  | <span data-ttu-id="7258a-151">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-151">Description</span></span> |
|------------|-----------------|-------------|
| <span data-ttu-id="7258a-152">instanceId</span><span class="sxs-lookup"><span data-stu-id="7258a-152">instanceId</span></span> | <span data-ttu-id="7258a-153">URL</span><span class="sxs-lookup"><span data-stu-id="7258a-153">URL</span></span>             | <span data-ttu-id="7258a-154">The ID of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-154">The ID of the orchestration instance.</span></span> |
| <span data-ttu-id="7258a-155">taskHub</span><span class="sxs-lookup"><span data-stu-id="7258a-155">taskHub</span></span>    | <span data-ttu-id="7258a-156">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-156">Query string</span></span>    | <span data-ttu-id="7258a-157">The name of the [task hub](durable-functions-task-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="7258a-157">The name of the [task hub](durable-functions-task-hubs.md).</span></span> <span data-ttu-id="7258a-158">If not specified, the current function app's task hub name is assumed.</span><span class="sxs-lookup"><span data-stu-id="7258a-158">If not specified, the current function app's task hub name is assumed.</span></span> |
| <span data-ttu-id="7258a-159">connection</span><span class="sxs-lookup"><span data-stu-id="7258a-159">connection</span></span> | <span data-ttu-id="7258a-160">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-160">Query string</span></span>    | <span data-ttu-id="7258a-161">The **name** of the connection string for the storage account.</span><span class="sxs-lookup"><span data-stu-id="7258a-161">The **name** of the connection string for the storage account.</span></span> <span data-ttu-id="7258a-162">If not specified, the default connection string for the function app is assumed.</span><span class="sxs-lookup"><span data-stu-id="7258a-162">If not specified, the default connection string for the function app is assumed.</span></span> |
| <span data-ttu-id="7258a-163">systemKey</span><span class="sxs-lookup"><span data-stu-id="7258a-163">systemKey</span></span>  | <span data-ttu-id="7258a-164">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-164">Query string</span></span>    | <span data-ttu-id="7258a-165">The authorization key required to invoke the API.</span><span class="sxs-lookup"><span data-stu-id="7258a-165">The authorization key required to invoke the API.</span></span> |
| <span data-ttu-id="7258a-166">showHistory</span><span class="sxs-lookup"><span data-stu-id="7258a-166">showHistory</span></span>| <span data-ttu-id="7258a-167">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-167">Query string</span></span>    | <span data-ttu-id="7258a-168">Optional parameter.</span><span class="sxs-lookup"><span data-stu-id="7258a-168">Optional parameter.</span></span> <span data-ttu-id="7258a-169">If set to `true`, the orchestration execution history will be included in the response payload.</span><span class="sxs-lookup"><span data-stu-id="7258a-169">If set to `true`, the orchestration execution history will be included in the response payload.</span></span>| 
| <span data-ttu-id="7258a-170">showHistoryOutput</span><span class="sxs-lookup"><span data-stu-id="7258a-170">showHistoryOutput</span></span>| <span data-ttu-id="7258a-171">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-171">Query string</span></span>    | <span data-ttu-id="7258a-172">Optional parameter.</span><span class="sxs-lookup"><span data-stu-id="7258a-172">Optional parameter.</span></span> <span data-ttu-id="7258a-173">If set to `true`, the activity outputs will be included in the orchestration execution history.</span><span class="sxs-lookup"><span data-stu-id="7258a-173">If set to `true`, the activity outputs will be included in the orchestration execution history.</span></span>| 

<span data-ttu-id="7258a-174">`systemKey` is an authorization key auto-generated by the Azure Functions host.</span><span class="sxs-lookup"><span data-stu-id="7258a-174">`systemKey` is an authorization key auto-generated by the Azure Functions host.</span></span> <span data-ttu-id="7258a-175">It specifically grants access to the Durable Task extension APIs and can be managed the same way as [other authorization keys](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Key-management-API).</span><span class="sxs-lookup"><span data-stu-id="7258a-175">It specifically grants access to the Durable Task extension APIs and can be managed the same way as [other authorization keys](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Key-management-API).</span></span> <span data-ttu-id="7258a-176">The simplest way to discover the `systemKey` value is by using the `CreateCheckStatusResponse` API mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="7258a-176">The simplest way to discover the `systemKey` value is by using the `CreateCheckStatusResponse` API mentioned previously.</span></span>

<span data-ttu-id="7258a-177">The next few sections cover the specific HTTP APIs supported by the extension and provide examples of how they can be used.</span><span class="sxs-lookup"><span data-stu-id="7258a-177">The next few sections cover the specific HTTP APIs supported by the extension and provide examples of how they can be used.</span></span>

### <a name="get-instance-status"></a><span data-ttu-id="7258a-178">Get instance status</span><span class="sxs-lookup"><span data-stu-id="7258a-178">Get instance status</span></span>

<span data-ttu-id="7258a-179">Gets the status of a specified orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-179">Gets the status of a specified orchestration instance.</span></span>

#### <a name="request"></a><span data-ttu-id="7258a-180">Request</span><span class="sxs-lookup"><span data-stu-id="7258a-180">Request</span></span>

<span data-ttu-id="7258a-181">For Functions 1.0, the request format is as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-181">For Functions 1.0, the request format is as follows:</span></span>

```http
GET /admin/extensions/DurableTaskExtension/instances/{instanceId}?taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-182">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span><span class="sxs-lookup"><span data-stu-id="7258a-182">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span></span>

```http
GET /runtime/webhooks/durabletask/instances/{instanceId}?taskHub={taskHub}&connection={connection}&code={systemKey}&showHistory={showHistory}&showHistoryOutput={showHistoryOutput}
```

#### <a name="response"></a><span data-ttu-id="7258a-183">Response</span><span class="sxs-lookup"><span data-stu-id="7258a-183">Response</span></span>

<span data-ttu-id="7258a-184">Several possible status code values can be returned.</span><span class="sxs-lookup"><span data-stu-id="7258a-184">Several possible status code values can be returned.</span></span>

* <span data-ttu-id="7258a-185">**HTTP 200 (OK)**: The specified instance is in a completed state.</span><span class="sxs-lookup"><span data-stu-id="7258a-185">**HTTP 200 (OK)**: The specified instance is in a completed state.</span></span>
* <span data-ttu-id="7258a-186">**HTTP 202 (Accepted)**: The specified instance is in progress.</span><span class="sxs-lookup"><span data-stu-id="7258a-186">**HTTP 202 (Accepted)**: The specified instance is in progress.</span></span>
* <span data-ttu-id="7258a-187">**HTTP 400 (Bad Request)**: The specified instance failed or was terminated.</span><span class="sxs-lookup"><span data-stu-id="7258a-187">**HTTP 400 (Bad Request)**: The specified instance failed or was terminated.</span></span>
* <span data-ttu-id="7258a-188">**HTTP 404 (Not Found)**: The specified instance doesn't exist or has not started running.</span><span class="sxs-lookup"><span data-stu-id="7258a-188">**HTTP 404 (Not Found)**: The specified instance doesn't exist or has not started running.</span></span>
* <span data-ttu-id="7258a-189">**HTTP 500 (Internal Server Error)**: The specified instance failed with an unhandled exception.</span><span class="sxs-lookup"><span data-stu-id="7258a-189">**HTTP 500 (Internal Server Error)**: The specified instance failed with an unhandled exception.</span></span>

<span data-ttu-id="7258a-190">The response payload for the **HTTP 200** and **HTTP 202** cases is a JSON object with the following fields:</span><span class="sxs-lookup"><span data-stu-id="7258a-190">The response payload for the **HTTP 200** and **HTTP 202** cases is a JSON object with the following fields:</span></span>

| <span data-ttu-id="7258a-191">Field</span><span class="sxs-lookup"><span data-stu-id="7258a-191">Field</span></span>           | <span data-ttu-id="7258a-192">Data type</span><span class="sxs-lookup"><span data-stu-id="7258a-192">Data type</span></span> | <span data-ttu-id="7258a-193">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-193">Description</span></span> |
|-----------------|-----------|-------------|
| <span data-ttu-id="7258a-194">runtimeStatus</span><span class="sxs-lookup"><span data-stu-id="7258a-194">runtimeStatus</span></span>   | <span data-ttu-id="7258a-195">string</span><span class="sxs-lookup"><span data-stu-id="7258a-195">string</span></span>    | <span data-ttu-id="7258a-196">The runtime status of the instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-196">The runtime status of the instance.</span></span> <span data-ttu-id="7258a-197">Values include *Running*, *Pending*, *Failed*, *Canceled*, *Terminated*, *Completed*.</span><span class="sxs-lookup"><span data-stu-id="7258a-197">Values include *Running*, *Pending*, *Failed*, *Canceled*, *Terminated*, *Completed*.</span></span> |
| <span data-ttu-id="7258a-198">input</span><span class="sxs-lookup"><span data-stu-id="7258a-198">input</span></span>           | <span data-ttu-id="7258a-199">JSON</span><span class="sxs-lookup"><span data-stu-id="7258a-199">JSON</span></span>      | <span data-ttu-id="7258a-200">The JSON data used to initialize the instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-200">The JSON data used to initialize the instance.</span></span> |
| <span data-ttu-id="7258a-201">customStatus</span><span class="sxs-lookup"><span data-stu-id="7258a-201">customStatus</span></span>    | <span data-ttu-id="7258a-202">JSON</span><span class="sxs-lookup"><span data-stu-id="7258a-202">JSON</span></span>      | <span data-ttu-id="7258a-203">The JSON data used for custom orchestration status.</span><span class="sxs-lookup"><span data-stu-id="7258a-203">The JSON data used for custom orchestration status.</span></span> <span data-ttu-id="7258a-204">This field is `null` if not set.</span><span class="sxs-lookup"><span data-stu-id="7258a-204">This field is `null` if not set.</span></span> |
| <span data-ttu-id="7258a-205">output</span><span class="sxs-lookup"><span data-stu-id="7258a-205">output</span></span>          | <span data-ttu-id="7258a-206">JSON</span><span class="sxs-lookup"><span data-stu-id="7258a-206">JSON</span></span>      | <span data-ttu-id="7258a-207">The JSON output of the instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-207">The JSON output of the instance.</span></span> <span data-ttu-id="7258a-208">This field is `null` if the instance is not in a completed state.</span><span class="sxs-lookup"><span data-stu-id="7258a-208">This field is `null` if the instance is not in a completed state.</span></span> |
| <span data-ttu-id="7258a-209">createdTime</span><span class="sxs-lookup"><span data-stu-id="7258a-209">createdTime</span></span>     | <span data-ttu-id="7258a-210">string</span><span class="sxs-lookup"><span data-stu-id="7258a-210">string</span></span>    | <span data-ttu-id="7258a-211">The time at which the instance was created.</span><span class="sxs-lookup"><span data-stu-id="7258a-211">The time at which the instance was created.</span></span> <span data-ttu-id="7258a-212">Uses ISO 8601 extended notation.</span><span class="sxs-lookup"><span data-stu-id="7258a-212">Uses ISO 8601 extended notation.</span></span> |
| <span data-ttu-id="7258a-213">lastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="7258a-213">lastUpdatedTime</span></span> | <span data-ttu-id="7258a-214">string</span><span class="sxs-lookup"><span data-stu-id="7258a-214">string</span></span>    | <span data-ttu-id="7258a-215">The time at which the instance last persisted.</span><span class="sxs-lookup"><span data-stu-id="7258a-215">The time at which the instance last persisted.</span></span> <span data-ttu-id="7258a-216">Uses ISO 8601 extended notation.</span><span class="sxs-lookup"><span data-stu-id="7258a-216">Uses ISO 8601 extended notation.</span></span> |
| <span data-ttu-id="7258a-217">historyEvents</span><span class="sxs-lookup"><span data-stu-id="7258a-217">historyEvents</span></span>   | <span data-ttu-id="7258a-218">JSON</span><span class="sxs-lookup"><span data-stu-id="7258a-218">JSON</span></span>      | <span data-ttu-id="7258a-219">A JSON array containing the orchestration execution history.</span><span class="sxs-lookup"><span data-stu-id="7258a-219">A JSON array containing the orchestration execution history.</span></span> <span data-ttu-id="7258a-220">This field is `null` unless the `showHistory` query string parameter is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="7258a-220">This field is `null` unless the `showHistory` query string parameter is set to `true`.</span></span>  | 

<span data-ttu-id="7258a-221">Here is an example response payload including the orchestration execution history and activity outputs (formatted for readability):</span><span class="sxs-lookup"><span data-stu-id="7258a-221">Here is an example response payload including the orchestration execution history and activity outputs (formatted for readability):</span></span>

```json
{
  "createdTime": "2018-02-28T05:18:49Z",
  "historyEvents": [
      {
          "EventType": "ExecutionStarted",
          "FunctionName": "E1_HelloSequence",
          "Timestamp": "2018-02-28T05:18:49.3452372Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello Tokyo!",
          "ScheduledTime": "2018-02-28T05:18:51.3939873Z",
          "Timestamp": "2018-02-28T05:18:52.2895622Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello Seattle!",
          "ScheduledTime": "2018-02-28T05:18:52.8755705Z",
          "Timestamp": "2018-02-28T05:18:53.1765771Z"
      },
      {
          "EventType": "TaskCompleted",
          "FunctionName": "E1_SayHello",
          "Result": "Hello London!",
          "ScheduledTime": "2018-02-28T05:18:53.5170791Z",
          "Timestamp": "2018-02-28T05:18:53.891081Z"
      },
      {
          "EventType": "ExecutionCompleted",
          "OrchestrationStatus": "Completed",
          "Result": [
              "Hello Tokyo!",
              "Hello Seattle!",
              "Hello London!"
          ],
          "Timestamp": "2018-02-28T05:18:54.3660895Z"
      }
  ],
  "input": null,
  "customStatus": { "nextActions": ["A", "B", "C"], "foo": 2 },
  "lastUpdatedTime": "2018-02-28T05:18:54Z",
  "output": [
      "Hello Tokyo!",
      "Hello Seattle!",
      "Hello London!"
  ],
  "runtimeStatus": "Completed"
}
```

<span data-ttu-id="7258a-222">The **HTTP 202** response also includes a **Location** response header that references the same URL as the `statusQueryGetUri` field mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="7258a-222">The **HTTP 202** response also includes a **Location** response header that references the same URL as the `statusQueryGetUri` field mentioned previously.</span></span>

### <a name="get-all-instances-status"></a><span data-ttu-id="7258a-223">Get all instances status</span><span class="sxs-lookup"><span data-stu-id="7258a-223">Get all instances status</span></span>

<span data-ttu-id="7258a-224">You can also query all instances status.</span><span class="sxs-lookup"><span data-stu-id="7258a-224">You can also query all instances status.</span></span> <span data-ttu-id="7258a-225">Remove the `instanceId` from the 'Get instance status' request.</span><span class="sxs-lookup"><span data-stu-id="7258a-225">Remove the `instanceId` from the 'Get instance status' request.</span></span> <span data-ttu-id="7258a-226">The parameters are the same as the 'Get instance status.'</span><span class="sxs-lookup"><span data-stu-id="7258a-226">The parameters are the same as the 'Get instance status.'</span></span> 

#### <a name="request"></a><span data-ttu-id="7258a-227">Request</span><span class="sxs-lookup"><span data-stu-id="7258a-227">Request</span></span>

<span data-ttu-id="7258a-228">For Functions 1.0, the request format is as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-228">For Functions 1.0, the request format is as follows:</span></span>

```http
GET /admin/extensions/DurableTaskExtension/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-229">The Functions 2.0 format has all the same parameters but a slightly different URL prefix:</span><span class="sxs-lookup"><span data-stu-id="7258a-229">The Functions 2.0 format has all the same parameters but a slightly different URL prefix:</span></span> 

```http
GET /runtime/webhooks/durabletask/instances/?taskHub={taskHub}&connection={connection}&code={systemKey}
```

#### <a name="response"></a><span data-ttu-id="7258a-230">Response</span><span class="sxs-lookup"><span data-stu-id="7258a-230">Response</span></span>

<span data-ttu-id="7258a-231">Here is an example of response payloads including the orchestration status (formatted for readability):</span><span class="sxs-lookup"><span data-stu-id="7258a-231">Here is an example of response payloads including the orchestration status (formatted for readability):</span></span>

```json
[
    {
        "instanceId": "7af46ff000564c65aafbfe99d07c32a5",
        "runtimeStatus": "Completed",
        "input": null,
        "customStatus": null,
        "output": [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ],
        "createdTime": "2018-06-04T10:46:39Z",
        "lastUpdatedTime": "2018-06-04T10:46:47Z"
    },
    {
        "instanceId": "80eb7dd5c22f4eeba9f42b062794321e",
        "runtimeStatus": "Running",
        "input": null,
        "customStatus": null,
        "output": null,
        "createdTime": "2018-06-04T15:18:28Z",
        "lastUpdatedTime": "2018-06-04T15:18:38Z"
    },
    {
        "instanceId": "9124518926db408ab8dfe84822aba2b1",
        "runtimeStatus": "Completed",
        "input": null,
        "customStatus": null,
        "output": [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ],
        "createdTime": "2018-06-04T10:46:54Z",
        "lastUpdatedTime": "2018-06-04T10:47:03Z"
    },
    {
        "instanceId": "d100b90b903c4009ba1a90868331b11b",
        "runtimeStatus": "Pending",
        "input": null,
        "customStatus": null,
        "output": null,
        "createdTime": "2018-06-04T15:18:39Z",
        "lastUpdatedTime": "2018-06-04T15:18:39Z"
    }
]
```

> [!NOTE]
> <span data-ttu-id="7258a-232">This operation can be very expensive in terms of Azure Storage I/O if there are a lot of rows in the Instances table.</span><span class="sxs-lookup"><span data-stu-id="7258a-232">This operation can be very expensive in terms of Azure Storage I/O if there are a lot of rows in the Instances table.</span></span> <span data-ttu-id="7258a-233">More details on Instance table can be found in the [Performance and scale in Durable Functions (Azure Functions)](https://docs.microsoft.com/en-us/azure/azure-functions/durable-functions-perf-and-scale#instances-table) documentation.</span><span class="sxs-lookup"><span data-stu-id="7258a-233">More details on Instance table can be found in the [Performance and scale in Durable Functions (Azure Functions)](https://docs.microsoft.com/en-us/azure/azure-functions/durable-functions-perf-and-scale#instances-table) documentation.</span></span>
> 

### <a name="raise-event"></a><span data-ttu-id="7258a-234">Raise event</span><span class="sxs-lookup"><span data-stu-id="7258a-234">Raise event</span></span>

<span data-ttu-id="7258a-235">Sends an event notification message to a running orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-235">Sends an event notification message to a running orchestration instance.</span></span>

#### <a name="request"></a><span data-ttu-id="7258a-236">Request</span><span class="sxs-lookup"><span data-stu-id="7258a-236">Request</span></span>

<span data-ttu-id="7258a-237">For Functions 1.0, the request format is as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-237">For Functions 1.0, the request format is as follows:</span></span>

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-238">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span><span class="sxs-lookup"><span data-stu-id="7258a-238">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span></span>

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-239">Request parameters for this API include the default set mentioned previously as well as the following unique parameters:</span><span class="sxs-lookup"><span data-stu-id="7258a-239">Request parameters for this API include the default set mentioned previously as well as the following unique parameters:</span></span>

| <span data-ttu-id="7258a-240">Field</span><span class="sxs-lookup"><span data-stu-id="7258a-240">Field</span></span>       | <span data-ttu-id="7258a-241">Parameter type</span><span class="sxs-lookup"><span data-stu-id="7258a-241">Parameter type</span></span>  | <span data-ttu-id="7258a-242">Data tType</span><span class="sxs-lookup"><span data-stu-id="7258a-242">Data tType</span></span> | <span data-ttu-id="7258a-243">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-243">Description</span></span> |
|-------------|-----------------|-----------|-------------|
| <span data-ttu-id="7258a-244">eventName</span><span class="sxs-lookup"><span data-stu-id="7258a-244">eventName</span></span>   | <span data-ttu-id="7258a-245">URL</span><span class="sxs-lookup"><span data-stu-id="7258a-245">URL</span></span>             | <span data-ttu-id="7258a-246">string</span><span class="sxs-lookup"><span data-stu-id="7258a-246">string</span></span>    | <span data-ttu-id="7258a-247">The name of the event that the target orchestration instance is waiting on.</span><span class="sxs-lookup"><span data-stu-id="7258a-247">The name of the event that the target orchestration instance is waiting on.</span></span> |
| <span data-ttu-id="7258a-248">{content}</span><span class="sxs-lookup"><span data-stu-id="7258a-248">{content}</span></span>   | <span data-ttu-id="7258a-249">Request content</span><span class="sxs-lookup"><span data-stu-id="7258a-249">Request content</span></span> | <span data-ttu-id="7258a-250">JSON</span><span class="sxs-lookup"><span data-stu-id="7258a-250">JSON</span></span>      | <span data-ttu-id="7258a-251">The JSON-formatted event payload.</span><span class="sxs-lookup"><span data-stu-id="7258a-251">The JSON-formatted event payload.</span></span> |

#### <a name="response"></a><span data-ttu-id="7258a-252">Response</span><span class="sxs-lookup"><span data-stu-id="7258a-252">Response</span></span>

<span data-ttu-id="7258a-253">Several possible status code values can be returned.</span><span class="sxs-lookup"><span data-stu-id="7258a-253">Several possible status code values can be returned.</span></span>

* <span data-ttu-id="7258a-254">**HTTP 202 (Accepted)**: The raised event was accepted for processing.</span><span class="sxs-lookup"><span data-stu-id="7258a-254">**HTTP 202 (Accepted)**: The raised event was accepted for processing.</span></span>
* <span data-ttu-id="7258a-255">**HTTP 400 (Bad request)**: The request content was not of type `application/json` or was not valid JSON.</span><span class="sxs-lookup"><span data-stu-id="7258a-255">**HTTP 400 (Bad request)**: The request content was not of type `application/json` or was not valid JSON.</span></span>
* <span data-ttu-id="7258a-256">**HTTP 404 (Not Found)**: The specified instance was not found.</span><span class="sxs-lookup"><span data-stu-id="7258a-256">**HTTP 404 (Not Found)**: The specified instance was not found.</span></span>
* <span data-ttu-id="7258a-257">**HTTP 410 (Gone)**: The specified instance has completed or failed and cannot process any raised events.</span><span class="sxs-lookup"><span data-stu-id="7258a-257">**HTTP 410 (Gone)**: The specified instance has completed or failed and cannot process any raised events.</span></span>

<span data-ttu-id="7258a-258">Here is an example request that sends the JSON string `"incr"` to an instance waiting for an event named **operation**:</span><span class="sxs-lookup"><span data-stu-id="7258a-258">Here is an example request that sends the JSON string `"incr"` to an instance waiting for an event named **operation**:</span></span>

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/raiseEvent/operation?taskHub=DurableFunctionsHub&connection=Storage&code=XXX
Content-Type: application/json
Content-Length: 6

"incr"
```

<span data-ttu-id="7258a-259">The responses for this API do not contain any content.</span><span class="sxs-lookup"><span data-stu-id="7258a-259">The responses for this API do not contain any content.</span></span>

### <a name="terminate-instance"></a><span data-ttu-id="7258a-260">Terminate instance</span><span class="sxs-lookup"><span data-stu-id="7258a-260">Terminate instance</span></span>

<span data-ttu-id="7258a-261">Terminates a running orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-261">Terminates a running orchestration instance.</span></span>

#### <a name="request"></a><span data-ttu-id="7258a-262">Request</span><span class="sxs-lookup"><span data-stu-id="7258a-262">Request</span></span>

<span data-ttu-id="7258a-263">For Functions 1.0, the request format is as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-263">For Functions 1.0, the request format is as follows:</span></span>

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/terminate?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-264">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span><span class="sxs-lookup"><span data-stu-id="7258a-264">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span></span>

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/terminate?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-265">Request parameters for this API include the default set mentioned previously as well as the following unique parameter.</span><span class="sxs-lookup"><span data-stu-id="7258a-265">Request parameters for this API include the default set mentioned previously as well as the following unique parameter.</span></span>

| <span data-ttu-id="7258a-266">Field</span><span class="sxs-lookup"><span data-stu-id="7258a-266">Field</span></span>       | <span data-ttu-id="7258a-267">Parameter Type</span><span class="sxs-lookup"><span data-stu-id="7258a-267">Parameter Type</span></span>  | <span data-ttu-id="7258a-268">Data Type</span><span class="sxs-lookup"><span data-stu-id="7258a-268">Data Type</span></span> | <span data-ttu-id="7258a-269">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-269">Description</span></span> |
|-------------|-----------------|-----------|-------------|
| <span data-ttu-id="7258a-270">reason</span><span class="sxs-lookup"><span data-stu-id="7258a-270">reason</span></span>      | <span data-ttu-id="7258a-271">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-271">Query string</span></span>    | <span data-ttu-id="7258a-272">string</span><span class="sxs-lookup"><span data-stu-id="7258a-272">string</span></span>    | <span data-ttu-id="7258a-273">Optional.</span><span class="sxs-lookup"><span data-stu-id="7258a-273">Optional.</span></span> <span data-ttu-id="7258a-274">The reason for terminating the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-274">The reason for terminating the orchestration instance.</span></span> |

#### <a name="response"></a><span data-ttu-id="7258a-275">Response</span><span class="sxs-lookup"><span data-stu-id="7258a-275">Response</span></span>

<span data-ttu-id="7258a-276">Several possible status code values can be returned.</span><span class="sxs-lookup"><span data-stu-id="7258a-276">Several possible status code values can be returned.</span></span>

* <span data-ttu-id="7258a-277">**HTTP 202 (Accepted)**: The terminate request was accepted for processing.</span><span class="sxs-lookup"><span data-stu-id="7258a-277">**HTTP 202 (Accepted)**: The terminate request was accepted for processing.</span></span>
* <span data-ttu-id="7258a-278">**HTTP 404 (Not Found)**: The specified instance was not found.</span><span class="sxs-lookup"><span data-stu-id="7258a-278">**HTTP 404 (Not Found)**: The specified instance was not found.</span></span>
* <span data-ttu-id="7258a-279">**HTTP 410 (Gone)**: The specified instance has completed or failed.</span><span class="sxs-lookup"><span data-stu-id="7258a-279">**HTTP 410 (Gone)**: The specified instance has completed or failed.</span></span>

<span data-ttu-id="7258a-280">Here is an example request that terminates a running instance and specifies a reason of **buggy**:</span><span class="sxs-lookup"><span data-stu-id="7258a-280">Here is an example request that terminates a running instance and specifies a reason of **buggy**:</span></span>

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/terminate?reason=buggy&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```

<span data-ttu-id="7258a-281">The responses for this API do not contain any content.</span><span class="sxs-lookup"><span data-stu-id="7258a-281">The responses for this API do not contain any content.</span></span>

## <a name="rewind-instance-preview"></a><span data-ttu-id="7258a-282">Rewind instance (preview)</span><span class="sxs-lookup"><span data-stu-id="7258a-282">Rewind instance (preview)</span></span>

<span data-ttu-id="7258a-283">Restores a failed orchestration instance into a running state by replaying the most recent failed operations.</span><span class="sxs-lookup"><span data-stu-id="7258a-283">Restores a failed orchestration instance into a running state by replaying the most recent failed operations.</span></span>

#### <a name="request"></a><span data-ttu-id="7258a-284">Request</span><span class="sxs-lookup"><span data-stu-id="7258a-284">Request</span></span>

<span data-ttu-id="7258a-285">For Functions 1.0, the request format is as follows:</span><span class="sxs-lookup"><span data-stu-id="7258a-285">For Functions 1.0, the request format is as follows:</span></span>

```http
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/rewind?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-286">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span><span class="sxs-lookup"><span data-stu-id="7258a-286">The Functions 2.0 format has all the same parameters but has a slightly different URL prefix:</span></span>

```http
POST /runtime/webhooks/durabletask/instances/{instanceId}/rewind?reason={reason}&taskHub={taskHub}&connection={connection}&code={systemKey}
```

<span data-ttu-id="7258a-287">Request parameters for this API include the default set mentioned previously as well as the following unique parameter.</span><span class="sxs-lookup"><span data-stu-id="7258a-287">Request parameters for this API include the default set mentioned previously as well as the following unique parameter.</span></span>

| <span data-ttu-id="7258a-288">Field</span><span class="sxs-lookup"><span data-stu-id="7258a-288">Field</span></span>       | <span data-ttu-id="7258a-289">Parameter Type</span><span class="sxs-lookup"><span data-stu-id="7258a-289">Parameter Type</span></span>  | <span data-ttu-id="7258a-290">Data Type</span><span class="sxs-lookup"><span data-stu-id="7258a-290">Data Type</span></span> | <span data-ttu-id="7258a-291">Description</span><span class="sxs-lookup"><span data-stu-id="7258a-291">Description</span></span> |
|-------------|-----------------|-----------|-------------|
| <span data-ttu-id="7258a-292">reason</span><span class="sxs-lookup"><span data-stu-id="7258a-292">reason</span></span>      | <span data-ttu-id="7258a-293">Query string</span><span class="sxs-lookup"><span data-stu-id="7258a-293">Query string</span></span>    | <span data-ttu-id="7258a-294">string</span><span class="sxs-lookup"><span data-stu-id="7258a-294">string</span></span>    | <span data-ttu-id="7258a-295">Optional.</span><span class="sxs-lookup"><span data-stu-id="7258a-295">Optional.</span></span> <span data-ttu-id="7258a-296">The reason for rewinding the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="7258a-296">The reason for rewinding the orchestration instance.</span></span> |

#### <a name="response"></a><span data-ttu-id="7258a-297">Response</span><span class="sxs-lookup"><span data-stu-id="7258a-297">Response</span></span>

<span data-ttu-id="7258a-298">Several possible status code values can be returned.</span><span class="sxs-lookup"><span data-stu-id="7258a-298">Several possible status code values can be returned.</span></span>

* <span data-ttu-id="7258a-299">**HTTP 202 (Accepted)**: The rewind request was accepted for processing.</span><span class="sxs-lookup"><span data-stu-id="7258a-299">**HTTP 202 (Accepted)**: The rewind request was accepted for processing.</span></span>
* <span data-ttu-id="7258a-300">**HTTP 404 (Not Found)**: The specified instance was not found.</span><span class="sxs-lookup"><span data-stu-id="7258a-300">**HTTP 404 (Not Found)**: The specified instance was not found.</span></span>
* <span data-ttu-id="7258a-301">**HTTP 410 (Gone)**: The specified instance has completed or was terminated.</span><span class="sxs-lookup"><span data-stu-id="7258a-301">**HTTP 410 (Gone)**: The specified instance has completed or was terminated.</span></span>

<span data-ttu-id="7258a-302">Here is an example request that rewinds a failed instance and specifies a reason of **fixed**:</span><span class="sxs-lookup"><span data-stu-id="7258a-302">Here is an example request that rewinds a failed instance and specifies a reason of **fixed**:</span></span>

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/rewind?reason=fixed&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```

<span data-ttu-id="7258a-303">The responses for this API do not contain any content.</span><span class="sxs-lookup"><span data-stu-id="7258a-303">The responses for this API do not contain any content.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7258a-304">Next steps</span><span class="sxs-lookup"><span data-stu-id="7258a-304">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7258a-305">Learn how to handle errors</span><span class="sxs-lookup"><span data-stu-id="7258a-305">Learn how to handle errors</span></span>](durable-functions-error-handling.md)
