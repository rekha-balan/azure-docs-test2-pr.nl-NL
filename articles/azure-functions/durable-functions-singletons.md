---
title: Singletons for Durable Functions - Azure
description: How to use singletons in the Durable Functons extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 8177fb6e8dea83ab2b8b12183cdcca6e43f92ade
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868000"
---
# <a name="singleton-orchestrators-in-durable-functions-azure-functions"></a><span data-ttu-id="893fe-103">Singleton orchestrators in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="893fe-103">Singleton orchestrators in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="893fe-104">For background jobs or actor-style orchestrations, you often need to ensure that only one instance of a particular orchestrator runs at a time.</span><span class="sxs-lookup"><span data-stu-id="893fe-104">For background jobs or actor-style orchestrations, you often need to ensure that only one instance of a particular orchestrator runs at a time.</span></span> <span data-ttu-id="893fe-105">This can be done in [Durable Functions](durable-functions-overview.md) by assigning a specific instance ID to an orchestrator when creating it.</span><span class="sxs-lookup"><span data-stu-id="893fe-105">This can be done in [Durable Functions](durable-functions-overview.md) by assigning a specific instance ID to an orchestrator when creating it.</span></span>

## <a name="singleton-example"></a><span data-ttu-id="893fe-106">Singleton example</span><span class="sxs-lookup"><span data-stu-id="893fe-106">Singleton example</span></span>

<span data-ttu-id="893fe-107">The following C# example shows an HTTP-trigger function that creates a singleton background job orchestration.</span><span class="sxs-lookup"><span data-stu-id="893fe-107">The following C# example shows an HTTP-trigger function that creates a singleton background job orchestration.</span></span> <span data-ttu-id="893fe-108">The code ensures that only one instance exists for a specified instance ID.</span><span class="sxs-lookup"><span data-stu-id="893fe-108">The code ensures that only one instance exists for a specified instance ID.</span></span>

```cs
[FunctionName("HttpStartSingle")]
public static async Task<HttpResponseMessage> RunSingle(
    [HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}/{instanceId}")] HttpRequestMessage req,
    [OrchestrationClient] DurableOrchestrationClient starter,
    string functionName,
    string instanceId,
    TraceWriter log)
{
    // Check if an instance with the specified ID already exists.
    var existingInstance = await starter.GetStatusAsync(instanceId);
    if (existingInstance == null)
    {
        // An instance with the specified ID doesn't exist, create one.
        dynamic eventData = await req.Content.ReadAsAsync<object>();
        await starter.StartNewAsync(functionName, instanceId, eventData);
        log.Info($"Started orchestration with ID = '{instanceId}'.");
        return starter.CreateCheckStatusResponse(req, instanceId);
    }
    else
    {
        // An instance with the specified ID exists, don't create one.
        return req.CreateErrorResponse(
            HttpStatusCode.Conflict,
            $"An instance with ID '{instanceId}' already exists.");
    }
}
```

<span data-ttu-id="893fe-109">By default, instance IDs are randomly generated GUIDs.</span><span class="sxs-lookup"><span data-stu-id="893fe-109">By default, instance IDs are randomly generated GUIDs.</span></span> <span data-ttu-id="893fe-110">But in this case, the instance ID is passed in route data from the URL.</span><span class="sxs-lookup"><span data-stu-id="893fe-110">But in this case, the instance ID is passed in route data from the URL.</span></span> <span data-ttu-id="893fe-111">The code calls [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_GetStatusAsync_) to check if an instance having the specified ID is already running.</span><span class="sxs-lookup"><span data-stu-id="893fe-111">The code calls [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_GetStatusAsync_) to check if an instance having the specified ID is already running.</span></span> <span data-ttu-id="893fe-112">If not, an instance is created with that ID.</span><span class="sxs-lookup"><span data-stu-id="893fe-112">If not, an instance is created with that ID.</span></span>

> [!NOTE]
> <span data-ttu-id="893fe-113">There is a potential race condition in this sample.</span><span class="sxs-lookup"><span data-stu-id="893fe-113">There is a potential race condition in this sample.</span></span> <span data-ttu-id="893fe-114">If two instances of **HttpStartSingle** execute concurrently, the result could be two different created instances of the singleton, one which overwrites the other.</span><span class="sxs-lookup"><span data-stu-id="893fe-114">If two instances of **HttpStartSingle** execute concurrently, the result could be two different created instances of the singleton, one which overwrites the other.</span></span> <span data-ttu-id="893fe-115">Depending on your requirements, this may have undesirable side effects.</span><span class="sxs-lookup"><span data-stu-id="893fe-115">Depending on your requirements, this may have undesirable side effects.</span></span> <span data-ttu-id="893fe-116">For this reason, it is important to ensure that no two requests can execute this trigger function concurrently.</span><span class="sxs-lookup"><span data-stu-id="893fe-116">For this reason, it is important to ensure that no two requests can execute this trigger function concurrently.</span></span>

<span data-ttu-id="893fe-117">The implementation details of the orchestrator function do not actually matter.</span><span class="sxs-lookup"><span data-stu-id="893fe-117">The implementation details of the orchestrator function do not actually matter.</span></span> <span data-ttu-id="893fe-118">It could be a regular orchestrator function that starts and completes, or it could be one that runs forever (that is, an [Eternal Orchestration](durable-functions-eternal-orchestrations.md)).</span><span class="sxs-lookup"><span data-stu-id="893fe-118">It could be a regular orchestrator function that starts and completes, or it could be one that runs forever (that is, an [Eternal Orchestration](durable-functions-eternal-orchestrations.md)).</span></span> <span data-ttu-id="893fe-119">The important point is that there is only ever one instance running at a time.</span><span class="sxs-lookup"><span data-stu-id="893fe-119">The important point is that there is only ever one instance running at a time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="893fe-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="893fe-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="893fe-121">Learn how to call sub-orchestrations</span><span class="sxs-lookup"><span data-stu-id="893fe-121">Learn how to call sub-orchestrations</span></span>](durable-functions-sub-orchestrations.md)
