---
title: Timers in Durable Functions - Azure
description: Learn how to implement durable timers in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/30/2018
ms.author: azfuncdf
ms.openlocfilehash: ff530d1af9a64383568aa53d3f53c59781d868a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867356"
---
# <a name="timers-in-durable-functions-azure-functions"></a><span data-ttu-id="13105-103">Timers in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="13105-103">Timers in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="13105-104">[Durable Functions](durable-functions-overview.md) provides *durable timers* for use in orchestrator functions to implement delays or to set up timeouts on async actions.</span><span class="sxs-lookup"><span data-stu-id="13105-104">[Durable Functions](durable-functions-overview.md) provides *durable timers* for use in orchestrator functions to implement delays or to set up timeouts on async actions.</span></span> <span data-ttu-id="13105-105">Durable timers should be used in orchestrator functions instead of `Thread.Sleep` and `Task.Delay` (C#), or `setTimeout()` and `setInterval()` (JavaScript).</span><span class="sxs-lookup"><span data-stu-id="13105-105">Durable timers should be used in orchestrator functions instead of `Thread.Sleep` and `Task.Delay` (C#), or `setTimeout()` and `setInterval()` (JavaScript).</span></span>

<span data-ttu-id="13105-106">You create a durable timer by calling the [CreateTimer](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CreateTimer_) method in [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html).</span><span class="sxs-lookup"><span data-stu-id="13105-106">You create a durable timer by calling the [CreateTimer](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CreateTimer_) method in [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html).</span></span> <span data-ttu-id="13105-107">The method returns a task that resumes on a specified date and time.</span><span class="sxs-lookup"><span data-stu-id="13105-107">The method returns a task that resumes on a specified date and time.</span></span>

## <a name="timer-limitations"></a><span data-ttu-id="13105-108">Timer limitations</span><span class="sxs-lookup"><span data-stu-id="13105-108">Timer limitations</span></span>

<span data-ttu-id="13105-109">When you create a timer that expires at 4:30 pm, the underlying Durable Task Framework enqueues a message which becomes visible only at 4:30 pm.</span><span class="sxs-lookup"><span data-stu-id="13105-109">When you create a timer that expires at 4:30 pm, the underlying Durable Task Framework enqueues a message which becomes visible only at 4:30 pm.</span></span> <span data-ttu-id="13105-110">When running in the Azure Functions consumption plan, the newly visible timer message will ensure that the function app gets activated on an appropriate VM.</span><span class="sxs-lookup"><span data-stu-id="13105-110">When running in the Azure Functions consumption plan, the newly visible timer message will ensure that the function app gets activated on an appropriate VM.</span></span>

> [!NOTE]
> * <span data-ttu-id="13105-111">Durable timers cannot last longer than 7 days due to limitations in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="13105-111">Durable timers cannot last longer than 7 days due to limitations in Azure Storage.</span></span> <span data-ttu-id="13105-112">We are working on a [feature request to extend timers beyond 7 days](https://github.com/Azure/azure-functions-durable-extension/issues/14).</span><span class="sxs-lookup"><span data-stu-id="13105-112">We are working on a [feature request to extend timers beyond 7 days](https://github.com/Azure/azure-functions-durable-extension/issues/14).</span></span>
> * <span data-ttu-id="13105-113">Always use [CurrentUtcDateTime](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CurrentUtcDateTime) instead of `DateTime.UtcNow` as shown in the examples below when computing a relative deadline of a durable timer.</span><span class="sxs-lookup"><span data-stu-id="13105-113">Always use [CurrentUtcDateTime](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CurrentUtcDateTime) instead of `DateTime.UtcNow` as shown in the examples below when computing a relative deadline of a durable timer.</span></span>

## <a name="usage-for-delay"></a><span data-ttu-id="13105-114">Usage for delay</span><span class="sxs-lookup"><span data-stu-id="13105-114">Usage for delay</span></span>

<span data-ttu-id="13105-115">The following example illustrates how to use durable timers for delaying execution.</span><span class="sxs-lookup"><span data-stu-id="13105-115">The following example illustrates how to use durable timers for delaying execution.</span></span> <span data-ttu-id="13105-116">The example is issuing a billing notification every day for ten days.</span><span class="sxs-lookup"><span data-stu-id="13105-116">The example is issuing a billing notification every day for ten days.</span></span>

#### <a name="c"></a><span data-ttu-id="13105-117">C#</span><span class="sxs-lookup"><span data-stu-id="13105-117">C#</span></span>

```csharp
[FunctionName("BillingIssuer")]
public static async Task Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    for (int i = 0; i < 10; i++)
    {
        DateTime deadline = context.CurrentUtcDateTime.Add(TimeSpan.FromDays(1));
        await context.CreateTimer(deadline, CancellationToken.None);
        await context.CallActivityAsync("SendBillingEvent");
    }
}
```

#### <a name="javascript"></a><span data-ttu-id="13105-118">JavaScript</span><span class="sxs-lookup"><span data-stu-id="13105-118">JavaScript</span></span>

```js
const df = require("durable-functions");
const moment = require("moment-js");

module.exports = df(function*(context) {
    for (let i = 0; i < 10; i++) {
        const dayOfMonth = context.df.currentUtcDateTime.getDate();
        const deadline = moment.utc(context.df.currentUtcDateTime).add(1, 'd');
        yield context.df.createTimer(deadline.toDate());
        yield context.df.callActivityAsync("SendBillingEvent");
    }
});
```

> [!WARNING]
> <span data-ttu-id="13105-119">Avoid infinite loops in orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="13105-119">Avoid infinite loops in orchestrator functions.</span></span> <span data-ttu-id="13105-120">For information about how to safely and efficiently implement infinite loop scenarios, see [Eternal Orchestrations](durable-functions-eternal-orchestrations.md).</span><span class="sxs-lookup"><span data-stu-id="13105-120">For information about how to safely and efficiently implement infinite loop scenarios, see [Eternal Orchestrations](durable-functions-eternal-orchestrations.md).</span></span> 

## <a name="usage-for-timeout"></a><span data-ttu-id="13105-121">Usage for timeout</span><span class="sxs-lookup"><span data-stu-id="13105-121">Usage for timeout</span></span>

<span data-ttu-id="13105-122">This example illustrates how to use durable timers to implement timeouts.</span><span class="sxs-lookup"><span data-stu-id="13105-122">This example illustrates how to use durable timers to implement timeouts.</span></span>

#### <a name="c"></a><span data-ttu-id="13105-123">C#</span><span class="sxs-lookup"><span data-stu-id="13105-123">C#</span></span>

```csharp
[FunctionName("TryGetQuote")]
public static async Task<bool> Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    TimeSpan timeout = TimeSpan.FromSeconds(30);
    DateTime deadline = context.CurrentUtcDateTime.Add(timeout);

    using (var cts = new CancellationTokenSource())
    {
        Task activityTask = context.CallActivityAsync("GetQuote");
        Task timeoutTask = context.CreateTimer(deadline, cts.Token);

        Task winner = await Task.WhenAny(activityTask, timeoutTask);
        if (winner == activityTask)
        {
            // success case
            cts.Cancel();
            return true;
        }
        else
        {
            // timeout case
            return false;
        }
    }
}
```

#### <a name="javascript"></a><span data-ttu-id="13105-124">JavaScript</span><span class="sxs-lookup"><span data-stu-id="13105-124">JavaScript</span></span>

```js
const df = require("durable-functions");
const moment = require("moment-js");

module.exports = df(function*(context) {
    const deadline = moment.utc(context.df.currentUtcDateTime).add(30, 's');

    const activityTask = context.df.callActivityAsync("GetQuote");
    const timeoutTask = context.df.createTimer(deadline);

    const winner = yield context.df.Task.any([activityTask, timeoutTask]);
    if (winner === activityTask) {
        // success case
        timeoutTask.cancel();
        return true;
    }
    else
    {
        // timeout case
        return false;
    }
});
```

> [!WARNING]
> <span data-ttu-id="13105-125">Use a `CancellationTokenSource` to cancel a durable timer (C#) or call `cancel()` on the returned `TimerTask` (JavaScript) if your code will not wait for it to complete.</span><span class="sxs-lookup"><span data-stu-id="13105-125">Use a `CancellationTokenSource` to cancel a durable timer (C#) or call `cancel()` on the returned `TimerTask` (JavaScript) if your code will not wait for it to complete.</span></span> <span data-ttu-id="13105-126">The Durable Task Framework will not change an orchestration's status to "completed" until all outstanding tasks are completed or cancelled.</span><span class="sxs-lookup"><span data-stu-id="13105-126">The Durable Task Framework will not change an orchestration's status to "completed" until all outstanding tasks are completed or cancelled.</span></span>

<span data-ttu-id="13105-127">This mechanism does not actually terminate in-progress activity function execution.</span><span class="sxs-lookup"><span data-stu-id="13105-127">This mechanism does not actually terminate in-progress activity function execution.</span></span> <span data-ttu-id="13105-128">Rather, it simply allows the orchestrator function to ignore the result and move on.</span><span class="sxs-lookup"><span data-stu-id="13105-128">Rather, it simply allows the orchestrator function to ignore the result and move on.</span></span> <span data-ttu-id="13105-129">If your function app uses the Consumption plan, you will still be billed for any time and memory consumed by the abandoned activity function.</span><span class="sxs-lookup"><span data-stu-id="13105-129">If your function app uses the Consumption plan, you will still be billed for any time and memory consumed by the abandoned activity function.</span></span> <span data-ttu-id="13105-130">By default, functions running in the Consumption plan have a timeout of five minutes.</span><span class="sxs-lookup"><span data-stu-id="13105-130">By default, functions running in the Consumption plan have a timeout of five minutes.</span></span> <span data-ttu-id="13105-131">If this limit is exceeded, the Azure Functions host is recycled to stop all execution and prevent a runaway billing situation.</span><span class="sxs-lookup"><span data-stu-id="13105-131">If this limit is exceeded, the Azure Functions host is recycled to stop all execution and prevent a runaway billing situation.</span></span> <span data-ttu-id="13105-132">The [function timeout is configurable](functions-host-json.md#functiontimeout).</span><span class="sxs-lookup"><span data-stu-id="13105-132">The [function timeout is configurable](functions-host-json.md#functiontimeout).</span></span>

<span data-ttu-id="13105-133">For a more in-depth example of how to implement timeouts in orchestrator functions, see the [Human Interaction & Timeouts - Phone Verification](durable-functions-phone-verification.md) walkthrough.</span><span class="sxs-lookup"><span data-stu-id="13105-133">For a more in-depth example of how to implement timeouts in orchestrator functions, see the [Human Interaction & Timeouts - Phone Verification](durable-functions-phone-verification.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13105-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="13105-134">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="13105-135">Learn how to raise and handle external events</span><span class="sxs-lookup"><span data-stu-id="13105-135">Learn how to raise and handle external events</span></span>](durable-functions-external-events.md)

