---
title: Best Practices for Azure Functions | Microsoft Docs
description: Learn best practices and patterns for Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, patterns, best practice, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53dcaea155471d47eb61317c52d38524c05e4600
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551143"
---
# <a name="tips-for-improving-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="ae602-104">Tips for improving the performance and reliability of Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ae602-104">Tips for improving the performance and reliability of Azure Functions</span></span>

##<a name="overview"></a><span data-ttu-id="ae602-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ae602-105">Overview</span></span>

<span data-ttu-id="ae602-106">This article provides a collection of best practices for you to consider when implementing function apps.</span><span class="sxs-lookup"><span data-stu-id="ae602-106">This article provides a collection of best practices for you to consider when implementing function apps.</span></span> <span data-ttu-id="ae602-107">Keep in mind that your function app is an app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ae602-107">Keep in mind that your function app is an app in Azure App Service.</span></span> <span data-ttu-id="ae602-108">So App Service best practices also apply.</span><span class="sxs-lookup"><span data-stu-id="ae602-108">So App Service best practices also apply.</span></span>


## <a name="avoid-large-long-running-functions"></a><span data-ttu-id="ae602-109">Avoid large long running functions</span><span class="sxs-lookup"><span data-stu-id="ae602-109">Avoid large long running functions</span></span>

<span data-ttu-id="ae602-110">Large, long-running functions can cause unexpected timeout issues.</span><span class="sxs-lookup"><span data-stu-id="ae602-110">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="ae602-111">A function can be large because of many Node.js dependencies.</span><span class="sxs-lookup"><span data-stu-id="ae602-111">A function can be large because of many Node.js dependencies.</span></span> <span data-ttu-id="ae602-112">Importing these dependencies can cause increased load times resulting in unexpected timeouts.</span><span class="sxs-lookup"><span data-stu-id="ae602-112">Importing these dependencies can cause increased load times resulting in unexpected timeouts.</span></span> <span data-ttu-id="ae602-113">Node.js dependencies could be explicitly loaded by multiple `require()` statements in your code.</span><span class="sxs-lookup"><span data-stu-id="ae602-113">Node.js dependencies could be explicitly loaded by multiple `require()` statements in your code.</span></span> <span data-ttu-id="ae602-114">Dependencies could also be implicit, based on a single module loaded by your code that has its own internal dependencies.</span><span class="sxs-lookup"><span data-stu-id="ae602-114">Dependencies could also be implicit, based on a single module loaded by your code that has its own internal dependencies.</span></span>  

<span data-ttu-id="ae602-115">Whenever possible, refactor large functions into smaller function sets that work together and return fast responses.</span><span class="sxs-lookup"><span data-stu-id="ae602-115">Whenever possible, refactor large functions into smaller function sets that work together and return fast responses.</span></span> <span data-ttu-id="ae602-116">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit.</span><span class="sxs-lookup"><span data-stu-id="ae602-116">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit.</span></span> <span data-ttu-id="ae602-117">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span><span class="sxs-lookup"><span data-stu-id="ae602-117">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="ae602-118">This approach allows you to defer the actual work and return an immediate response.</span><span class="sxs-lookup"><span data-stu-id="ae602-118">This approach allows you to defer the actual work and return an immediate response.</span></span> <span data-ttu-id="ae602-119">It is common for webhooks to require an immediate response.</span><span class="sxs-lookup"><span data-stu-id="ae602-119">It is common for webhooks to require an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="ae602-120">Cross function communication.</span><span class="sxs-lookup"><span data-stu-id="ae602-120">Cross function communication.</span></span>

<span data-ttu-id="ae602-121">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span><span class="sxs-lookup"><span data-stu-id="ae602-121">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="ae602-122">The main reason is storage queues are cheaper and much easier to provision.</span><span class="sxs-lookup"><span data-stu-id="ae602-122">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="ae602-123">Individual messages in a storage queue are limited in size to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ae602-123">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="ae602-124">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span><span class="sxs-lookup"><span data-stu-id="ae602-124">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="ae602-125">Service Bus topics are useful if you require message filtering before processing.</span><span class="sxs-lookup"><span data-stu-id="ae602-125">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="ae602-126">Event hubs are useful to support high volume communications.</span><span class="sxs-lookup"><span data-stu-id="ae602-126">Event hubs are useful to support high volume communications.</span></span>



## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="ae602-127">Write functions to be stateless</span><span class="sxs-lookup"><span data-stu-id="ae602-127">Write functions to be stateless</span></span> 

<span data-ttu-id="ae602-128">Functions should be stateless and idempotent if possible.</span><span class="sxs-lookup"><span data-stu-id="ae602-128">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="ae602-129">Associate any required state information with your data.</span><span class="sxs-lookup"><span data-stu-id="ae602-129">Associate any required state information with your data.</span></span> <span data-ttu-id="ae602-130">For example, an order being processed would likely have an associated `state` member.</span><span class="sxs-lookup"><span data-stu-id="ae602-130">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="ae602-131">A function could process an order based on that state while the function itself remains stateless.</span><span class="sxs-lookup"><span data-stu-id="ae602-131">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="ae602-132">Idempotent functions are especially recommended with timer triggers.</span><span class="sxs-lookup"><span data-stu-id="ae602-132">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="ae602-133">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span><span class="sxs-lookup"><span data-stu-id="ae602-133">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="ae602-134">The function can exit when there is no work for a particular day.</span><span class="sxs-lookup"><span data-stu-id="ae602-134">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="ae602-135">Also if a previous run failed to complete, the next run should pick up where it left off.</span><span class="sxs-lookup"><span data-stu-id="ae602-135">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="ae602-136">Write defensive functions.</span><span class="sxs-lookup"><span data-stu-id="ae602-136">Write defensive functions.</span></span>

<span data-ttu-id="ae602-137">Assume your function could encounter an exception at any time.</span><span class="sxs-lookup"><span data-stu-id="ae602-137">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="ae602-138">Design your functions with the ability to continue from a previous fail point during the next execution.</span><span class="sxs-lookup"><span data-stu-id="ae602-138">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="ae602-139">Consider a scenario that requires the following actions:</span><span class="sxs-lookup"><span data-stu-id="ae602-139">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="ae602-140">Query for 10,000 rows in a db.</span><span class="sxs-lookup"><span data-stu-id="ae602-140">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="ae602-141">Create a queue message for each of those rows to process further down the line.</span><span class="sxs-lookup"><span data-stu-id="ae602-141">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="ae602-142">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span><span class="sxs-lookup"><span data-stu-id="ae602-142">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="ae602-143">You need to design your functions to be prepared for it.</span><span class="sxs-lookup"><span data-stu-id="ae602-143">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="ae602-144">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span><span class="sxs-lookup"><span data-stu-id="ae602-144">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="ae602-145">Track items in a set that you’ve completed.</span><span class="sxs-lookup"><span data-stu-id="ae602-145">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="ae602-146">Otherwise, you might insert them again next time.</span><span class="sxs-lookup"><span data-stu-id="ae602-146">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="ae602-147">This can have a serious impact on your work flow.</span><span class="sxs-lookup"><span data-stu-id="ae602-147">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="ae602-148">If a queue item was already processed, allow your function to be a no-op.</span><span class="sxs-lookup"><span data-stu-id="ae602-148">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="ae602-149">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span><span class="sxs-lookup"><span data-stu-id="ae602-149">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="ae602-150">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="ae602-150">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="ae602-151">Don't mix test and production code in the same function app.</span><span class="sxs-lookup"><span data-stu-id="ae602-151">Don't mix test and production code in the same function app.</span></span>

<span data-ttu-id="ae602-152">Functions within a function app share resources.</span><span class="sxs-lookup"><span data-stu-id="ae602-152">Functions within a function app share resources.</span></span> <span data-ttu-id="ae602-153">For example, memory is shared.</span><span class="sxs-lookup"><span data-stu-id="ae602-153">For example, memory is shared.</span></span> <span data-ttu-id="ae602-154">If you're using a function app in production, don't add test-related functions and resources to it.</span><span class="sxs-lookup"><span data-stu-id="ae602-154">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="ae602-155">It can cause unexpected overhead during production code execution.</span><span class="sxs-lookup"><span data-stu-id="ae602-155">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="ae602-156">Be careful what you load in your production function apps.</span><span class="sxs-lookup"><span data-stu-id="ae602-156">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="ae602-157">Memory is averaged across each function in the app.</span><span class="sxs-lookup"><span data-stu-id="ae602-157">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="ae602-158">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span><span class="sxs-lookup"><span data-stu-id="ae602-158">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="ae602-159">Reference the assembly with a statement similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ae602-159">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="ae602-160">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span><span class="sxs-lookup"><span data-stu-id="ae602-160">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="ae602-161">Don't use verbose logging in production code.</span><span class="sxs-lookup"><span data-stu-id="ae602-161">Don't use verbose logging in production code.</span></span> <span data-ttu-id="ae602-162">It has a negative performance impact.</span><span class="sxs-lookup"><span data-stu-id="ae602-162">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-taskresult"></a><span data-ttu-id="ae602-163">Use async code but avoid Task.Result</span><span class="sxs-lookup"><span data-stu-id="ae602-163">Use async code but avoid Task.Result</span></span>

<span data-ttu-id="ae602-164">Asynchronous programming is a recommended best practice.</span><span class="sxs-lookup"><span data-stu-id="ae602-164">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="ae602-165">However, always avoid referencing the `Task.Result` property.</span><span class="sxs-lookup"><span data-stu-id="ae602-165">However, always avoid referencing the `Task.Result` property.</span></span> <span data-ttu-id="ae602-166">This approach essentially does a busy-wait on a lock of another thread.</span><span class="sxs-lookup"><span data-stu-id="ae602-166">This approach essentially does a busy-wait on a lock of another thread.</span></span> <span data-ttu-id="ae602-167">Holding a lock creates the potential for deadlocks.</span><span class="sxs-lookup"><span data-stu-id="ae602-167">Holding a lock creates the potential for deadlocks.</span></span>




## <a name="next-steps"></a><span data-ttu-id="ae602-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae602-168">Next steps</span></span>
<span data-ttu-id="ae602-169">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="ae602-169">For more information, see the following resources:</span></span>

* [<span data-ttu-id="ae602-170">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="ae602-170">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="ae602-171">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="ae602-171">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="ae602-172">Azure Functions F# developer reference</span><span class="sxs-lookup"><span data-stu-id="ae602-172">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="ae602-173">Azure Functions NodeJS developer reference</span><span class="sxs-lookup"><span data-stu-id="ae602-173">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="ae602-174">Patterns and Practices HTTP Performance Optimizations</span><span class="sxs-lookup"><span data-stu-id="ae602-174">Patterns and Practices HTTP Performance Optimizations</span></span>](https://github.com/mspnp/performance-optimization/blob/master/ImproperInstantiation/docs/ImproperInstantiation.md)

