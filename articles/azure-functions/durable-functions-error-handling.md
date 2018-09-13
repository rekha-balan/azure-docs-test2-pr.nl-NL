---
title: Handling errors in Durable Functions - Azure
description: Learn how to handle errors in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/05/2018
ms.author: azfuncdf
ms.openlocfilehash: 6bf9eb2cd2ebdf5f6d53e00923146bab49a142bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855879"
---
# <a name="handling-errors-in-durable-functions-azure-functions"></a><span data-ttu-id="0aa06-103">Handling errors in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="0aa06-103">Handling errors in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="0aa06-104">Durable Function orchestrations are implemented in code and can use the error-handling capabilities of the programming language.</span><span class="sxs-lookup"><span data-stu-id="0aa06-104">Durable Function orchestrations are implemented in code and can use the error-handling capabilities of the programming language.</span></span> <span data-ttu-id="0aa06-105">With this in mind, there really aren't any new concepts you need to learn about when incorporating error handling and compensation into your orchestrations.</span><span class="sxs-lookup"><span data-stu-id="0aa06-105">With this in mind, there really aren't any new concepts you need to learn about when incorporating error handling and compensation into your orchestrations.</span></span> <span data-ttu-id="0aa06-106">However, there are a few behaviors that you should be aware of.</span><span class="sxs-lookup"><span data-stu-id="0aa06-106">However, there are a few behaviors that you should be aware of.</span></span>

## <a name="errors-in-activity-functions"></a><span data-ttu-id="0aa06-107">Errors in activity functions</span><span class="sxs-lookup"><span data-stu-id="0aa06-107">Errors in activity functions</span></span>

<span data-ttu-id="0aa06-108">Any exception that is thrown in an activity function is marshalled back to the orchestrator function and thrown as a `FunctionFailedException`.</span><span class="sxs-lookup"><span data-stu-id="0aa06-108">Any exception that is thrown in an activity function is marshalled back to the orchestrator function and thrown as a `FunctionFailedException`.</span></span> <span data-ttu-id="0aa06-109">You can write error handling and compensation code that suits your needs in the orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="0aa06-109">You can write error handling and compensation code that suits your needs in the orchestrator function.</span></span>

<span data-ttu-id="0aa06-110">For example, consider the following orchestrator function that transfers funds from one account to another:</span><span class="sxs-lookup"><span data-stu-id="0aa06-110">For example, consider the following orchestrator function that transfers funds from one account to another:</span></span>

```csharp
#r "Microsoft.Azure.WebJobs.Extensions.DurableTask"

public static async Task Run(DurableOrchestrationContext context)
{
    var transferDetails = ctx.GetInput<TransferOperation>();

    await context.CallActivityAsync("DebitAccount",
        new
        { 
            Account = transferDetails.SourceAccount,
            Amount = transferDetails.Amount
        });

    try
    {
        await context.CallActivityAsync("CreditAccount",         
            new
            { 
                Account = transferDetails.DestinationAccount,
                Amount = transferDetails.Amount
            });
    }
    catch (Exception)
    {
        // Refund the source account.
        // Another try/catch could be used here based on the needs of the application.
        await context.CallActivityAsync("CreditAccount",         
            new
            { 
                Account = transferDetails.SourceAccount,
                Amount = transferDetails.Amount
            });
    }
}
```

<span data-ttu-id="0aa06-111">If the call to the **CreditAccount** function fails for the destination account, the orchestrator function compensates for this by crediting the funds back to the source account.</span><span class="sxs-lookup"><span data-stu-id="0aa06-111">If the call to the **CreditAccount** function fails for the destination account, the orchestrator function compensates for this by crediting the funds back to the source account.</span></span>

## <a name="automatic-retry-on-failure"></a><span data-ttu-id="0aa06-112">Automatic retry on failure</span><span class="sxs-lookup"><span data-stu-id="0aa06-112">Automatic retry on failure</span></span>

<span data-ttu-id="0aa06-113">When you call activity functions or sub-orchestration functions, you can specify an automatic retry policy.</span><span class="sxs-lookup"><span data-stu-id="0aa06-113">When you call activity functions or sub-orchestration functions, you can specify an automatic retry policy.</span></span> <span data-ttu-id="0aa06-114">The following example attempts to call a function up to three times and waits 5 seconds between each retry:</span><span class="sxs-lookup"><span data-stu-id="0aa06-114">The following example attempts to call a function up to three times and waits 5 seconds between each retry:</span></span>

```csharp
public static async Task Run(DurableOrchestrationContext context)
{
    var retryOptions = new RetryOptions(
        firstRetryInterval: TimeSpan.FromSeconds(5),
        maxNumberOfAttempts: 3);

    await ctx.CallActivityWithRetryAsync("FlakyFunction", retryOptions, null);
    
    // ...
}
```

<span data-ttu-id="0aa06-115">The `CallActivityWithRetryAsync` API takes a `RetryOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="0aa06-115">The `CallActivityWithRetryAsync` API takes a `RetryOptions` parameter.</span></span> <span data-ttu-id="0aa06-116">Suborchestration calls using the `CallSubOrchestratorWithRetryAsync` API can use these same retry policies.</span><span class="sxs-lookup"><span data-stu-id="0aa06-116">Suborchestration calls using the `CallSubOrchestratorWithRetryAsync` API can use these same retry policies.</span></span>

<span data-ttu-id="0aa06-117">There are several options for customizing the automatic retry policy.</span><span class="sxs-lookup"><span data-stu-id="0aa06-117">There are several options for customizing the automatic retry policy.</span></span> <span data-ttu-id="0aa06-118">They include the following:</span><span class="sxs-lookup"><span data-stu-id="0aa06-118">They include the following:</span></span>

* <span data-ttu-id="0aa06-119">**Max number of attempts**: The maximum number of retry attempts.</span><span class="sxs-lookup"><span data-stu-id="0aa06-119">**Max number of attempts**: The maximum number of retry attempts.</span></span>
* <span data-ttu-id="0aa06-120">**First retry interval**: The amount of time to wait before the first retry attempt.</span><span class="sxs-lookup"><span data-stu-id="0aa06-120">**First retry interval**: The amount of time to wait before the first retry attempt.</span></span>
* <span data-ttu-id="0aa06-121">**Backoff coefficient**: The coefficient used to determine rate of increase of backoff.</span><span class="sxs-lookup"><span data-stu-id="0aa06-121">**Backoff coefficient**: The coefficient used to determine rate of increase of backoff.</span></span> <span data-ttu-id="0aa06-122">Defaults to 1.</span><span class="sxs-lookup"><span data-stu-id="0aa06-122">Defaults to 1.</span></span>
* <span data-ttu-id="0aa06-123">**Max retry interval**: The maximum amount of time to wait in between retry attempts.</span><span class="sxs-lookup"><span data-stu-id="0aa06-123">**Max retry interval**: The maximum amount of time to wait in between retry attempts.</span></span>
* <span data-ttu-id="0aa06-124">**Retry timeout**: The maximum amount of time to spend doing retries.</span><span class="sxs-lookup"><span data-stu-id="0aa06-124">**Retry timeout**: The maximum amount of time to spend doing retries.</span></span> <span data-ttu-id="0aa06-125">The default behavior is to retry indefinitely.</span><span class="sxs-lookup"><span data-stu-id="0aa06-125">The default behavior is to retry indefinitely.</span></span>
* <span data-ttu-id="0aa06-126">**Handle**: A user-defined callback can be specified which determines whether or not a function call should be retried.</span><span class="sxs-lookup"><span data-stu-id="0aa06-126">**Handle**: A user-defined callback can be specified which determines whether or not a function call should be retried.</span></span>

## <a name="function-timeouts"></a><span data-ttu-id="0aa06-127">Function timeouts</span><span class="sxs-lookup"><span data-stu-id="0aa06-127">Function timeouts</span></span>

<span data-ttu-id="0aa06-128">You might want to abandon a function call within an orchestrator function if it is taking too long to complete.</span><span class="sxs-lookup"><span data-stu-id="0aa06-128">You might want to abandon a function call within an orchestrator function if it is taking too long to complete.</span></span> <span data-ttu-id="0aa06-129">The proper way to do this today is by creating a [durable timer](durable-functions-timers.md) using `context.CreateTimer` in conjunction with `Task.WhenAny`, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="0aa06-129">The proper way to do this today is by creating a [durable timer](durable-functions-timers.md) using `context.CreateTimer` in conjunction with `Task.WhenAny`, as in the following example:</span></span>

```csharp
public static async Task<bool> Run(DurableOrchestrationContext context)
{
    TimeSpan timeout = TimeSpan.FromSeconds(30);
    DateTime deadline = context.CurrentUtcDateTime.Add(timeout);

    using (var cts = new CancellationTokenSource())
    {
        Task activityTask = context.CallActivityAsync("FlakyFunction");
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

> [!NOTE]
> <span data-ttu-id="0aa06-130">This mechanism does not actually terminate in-progress activity function execution.</span><span class="sxs-lookup"><span data-stu-id="0aa06-130">This mechanism does not actually terminate in-progress activity function execution.</span></span> <span data-ttu-id="0aa06-131">Rather, it simply allows the orchestrator function to ignore the result and move on.</span><span class="sxs-lookup"><span data-stu-id="0aa06-131">Rather, it simply allows the orchestrator function to ignore the result and move on.</span></span> <span data-ttu-id="0aa06-132">For more information, see the [Timers](durable-functions-timers.md#usage-for-timeout) documentation.</span><span class="sxs-lookup"><span data-stu-id="0aa06-132">For more information, see the [Timers](durable-functions-timers.md#usage-for-timeout) documentation.</span></span>

## <a name="unhandled-exceptions"></a><span data-ttu-id="0aa06-133">Unhandled exceptions</span><span class="sxs-lookup"><span data-stu-id="0aa06-133">Unhandled exceptions</span></span>

<span data-ttu-id="0aa06-134">If an orchestrator function fails with an unhandled exception, the details of the exception are logged and the instance completes with a `Failed` status.</span><span class="sxs-lookup"><span data-stu-id="0aa06-134">If an orchestrator function fails with an unhandled exception, the details of the exception are logged and the instance completes with a `Failed` status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aa06-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="0aa06-135">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0aa06-136">Learn how to diagnose problems</span><span class="sxs-lookup"><span data-stu-id="0aa06-136">Learn how to diagnose problems</span></span>](durable-functions-diagnostics.md)
