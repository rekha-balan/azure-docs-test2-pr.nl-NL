---
title: Fan-out/fan-in scenarios in Durable Functions - Azure
description: Learn how to implement a fan-out-fan-in scenario in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 03/19/2018
ms.author: azfuncdf
ms.openlocfilehash: eec75ad9cf0f568e674b2a4f12d962982f84294f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866472"
---
# <a name="fan-outfan-in-scenario-in-durable-functions---cloud-backup-example"></a><span data-ttu-id="aab7a-103">Fan-out/fan-in scenario in Durable Functions - Cloud backup example</span><span class="sxs-lookup"><span data-stu-id="aab7a-103">Fan-out/fan-in scenario in Durable Functions - Cloud backup example</span></span>

<span data-ttu-id="aab7a-104">*Fan-out/fan-in* refers to the pattern of executing multiple functions concurrently and then performing some aggregation on the results.</span><span class="sxs-lookup"><span data-stu-id="aab7a-104">*Fan-out/fan-in* refers to the pattern of executing multiple functions concurrently and then performing some aggregation on the results.</span></span> <span data-ttu-id="aab7a-105">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement a fan-in/fan-out scenario.</span><span class="sxs-lookup"><span data-stu-id="aab7a-105">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement a fan-in/fan-out scenario.</span></span> <span data-ttu-id="aab7a-106">The sample is a durable function that backs up all or some of an app's site content into Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aab7a-106">The sample is a durable function that backs up all or some of an app's site content into Azure Storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aab7a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aab7a-107">Prerequisites</span></span>

* <span data-ttu-id="aab7a-108">[Install Durable Functions](durable-functions-install.md).</span><span class="sxs-lookup"><span data-stu-id="aab7a-108">[Install Durable Functions](durable-functions-install.md).</span></span>
* <span data-ttu-id="aab7a-109">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aab7a-109">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="aab7a-110">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="aab7a-110">Scenario overview</span></span>

<span data-ttu-id="aab7a-111">In this sample, the functions upload all files under a specified directory recursively into blob storage.</span><span class="sxs-lookup"><span data-stu-id="aab7a-111">In this sample, the functions upload all files under a specified directory recursively into blob storage.</span></span> <span data-ttu-id="aab7a-112">They also count the total number of bytes that were uploaded.</span><span class="sxs-lookup"><span data-stu-id="aab7a-112">They also count the total number of bytes that were uploaded.</span></span>

<span data-ttu-id="aab7a-113">It's possible to write a single function that takes care of everything.</span><span class="sxs-lookup"><span data-stu-id="aab7a-113">It's possible to write a single function that takes care of everything.</span></span> <span data-ttu-id="aab7a-114">The main problem you would run into is **scalability**.</span><span class="sxs-lookup"><span data-stu-id="aab7a-114">The main problem you would run into is **scalability**.</span></span> <span data-ttu-id="aab7a-115">A single function execution can only run on a single VM, so the throughput will be limited by the throughput of that single VM.</span><span class="sxs-lookup"><span data-stu-id="aab7a-115">A single function execution can only run on a single VM, so the throughput will be limited by the throughput of that single VM.</span></span> <span data-ttu-id="aab7a-116">Another problem is **reliability**.</span><span class="sxs-lookup"><span data-stu-id="aab7a-116">Another problem is **reliability**.</span></span> <span data-ttu-id="aab7a-117">If there's a failure midway through, or if the entire process takes more than 5 minutes, the backup could fail in a partially-completed state.</span><span class="sxs-lookup"><span data-stu-id="aab7a-117">If there's a failure midway through, or if the entire process takes more than 5 minutes, the backup could fail in a partially-completed state.</span></span> <span data-ttu-id="aab7a-118">It would then need to be restarted.</span><span class="sxs-lookup"><span data-stu-id="aab7a-118">It would then need to be restarted.</span></span>

<span data-ttu-id="aab7a-119">A more robust approach would be to write two regular functions: one would enumerate the files and add the file names to a queue, and another would read from the queue and upload the files to blob storage.</span><span class="sxs-lookup"><span data-stu-id="aab7a-119">A more robust approach would be to write two regular functions: one would enumerate the files and add the file names to a queue, and another would read from the queue and upload the files to blob storage.</span></span> <span data-ttu-id="aab7a-120">This is better in terms of throughput and reliability, but it requires you to provision and manage a queue.</span><span class="sxs-lookup"><span data-stu-id="aab7a-120">This is better in terms of throughput and reliability, but it requires you to provision and manage a queue.</span></span> <span data-ttu-id="aab7a-121">More importantly, significant complexity is introduced in terms of **state management** and **coordination** if you want to do anything more, like report the total number of bytes uploaded.</span><span class="sxs-lookup"><span data-stu-id="aab7a-121">More importantly, significant complexity is introduced in terms of **state management** and **coordination** if you want to do anything more, like report the total number of bytes uploaded.</span></span>

<span data-ttu-id="aab7a-122">A Durable Functions approach gives you all of the mentioned benefits with very low overhead.</span><span class="sxs-lookup"><span data-stu-id="aab7a-122">A Durable Functions approach gives you all of the mentioned benefits with very low overhead.</span></span>

## <a name="the-functions"></a><span data-ttu-id="aab7a-123">The functions</span><span class="sxs-lookup"><span data-stu-id="aab7a-123">The functions</span></span>

<span data-ttu-id="aab7a-124">This article explains the following functions in the sample app:</span><span class="sxs-lookup"><span data-stu-id="aab7a-124">This article explains the following functions in the sample app:</span></span>

* `E2_BackupSiteContent`
* `E2_GetFileList`
* `E2_CopyFileToBlob`

<span data-ttu-id="aab7a-125">The following sections explain the configuration and code that are used for C# scripting.</span><span class="sxs-lookup"><span data-stu-id="aab7a-125">The following sections explain the configuration and code that are used for C# scripting.</span></span> <span data-ttu-id="aab7a-126">The code for Visual Studio development is shown at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="aab7a-126">The code for Visual Studio development is shown at the end of the article.</span></span>

## <a name="the-cloud-backup-orchestration-visual-studio-code-and-azure-portal-sample-code"></a><span data-ttu-id="aab7a-127">The cloud backup orchestration (Visual Studio Code and Azure portal sample code)</span><span class="sxs-lookup"><span data-stu-id="aab7a-127">The cloud backup orchestration (Visual Studio Code and Azure portal sample code)</span></span>

<span data-ttu-id="aab7a-128">The `E2_BackupSiteContent` function uses the standard *function.json* for orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="aab7a-128">The `E2_BackupSiteContent` function uses the standard *function.json* for orchestrator functions.</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E2_BackupSiteContent/function.json)]

<span data-ttu-id="aab7a-129">Here is the code that implements the orchestrator function:</span><span class="sxs-lookup"><span data-stu-id="aab7a-129">Here is the code that implements the orchestrator function:</span></span>

### <a name="c"></a><span data-ttu-id="aab7a-130">C#</span><span class="sxs-lookup"><span data-stu-id="aab7a-130">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E2_BackupSiteContent/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="aab7a-131">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="aab7a-131">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E2_BackupSiteContent/index.js)]

<span data-ttu-id="aab7a-132">This orchestrator function essentially does the following:</span><span class="sxs-lookup"><span data-stu-id="aab7a-132">This orchestrator function essentially does the following:</span></span>

1. <span data-ttu-id="aab7a-133">Takes a `rootDirectory` value as an input parameter.</span><span class="sxs-lookup"><span data-stu-id="aab7a-133">Takes a `rootDirectory` value as an input parameter.</span></span>
2. <span data-ttu-id="aab7a-134">Calls a function to get a recursive list of files under `rootDirectory`.</span><span class="sxs-lookup"><span data-stu-id="aab7a-134">Calls a function to get a recursive list of files under `rootDirectory`.</span></span>
3. <span data-ttu-id="aab7a-135">Makes multiple parallel function calls to upload each file into Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="aab7a-135">Makes multiple parallel function calls to upload each file into Azure Blob Storage.</span></span>
4. <span data-ttu-id="aab7a-136">Waits for all uploads to complete.</span><span class="sxs-lookup"><span data-stu-id="aab7a-136">Waits for all uploads to complete.</span></span>
5. <span data-ttu-id="aab7a-137">Returns the sum total bytes that were uploaded to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="aab7a-137">Returns the sum total bytes that were uploaded to Azure Blob Storage.</span></span>

<span data-ttu-id="aab7a-138">Notice the `await Task.WhenAll(tasks);` (C#) and `yield context.df.Task.all(tasks);` (JS) line.</span><span class="sxs-lookup"><span data-stu-id="aab7a-138">Notice the `await Task.WhenAll(tasks);` (C#) and `yield context.df.Task.all(tasks);` (JS) line.</span></span> <span data-ttu-id="aab7a-139">All the calls to the `E2_CopyFileToBlob` function were *not* awaited.</span><span class="sxs-lookup"><span data-stu-id="aab7a-139">All the calls to the `E2_CopyFileToBlob` function were *not* awaited.</span></span> <span data-ttu-id="aab7a-140">This is intentional to allow them to run in parallel.</span><span class="sxs-lookup"><span data-stu-id="aab7a-140">This is intentional to allow them to run in parallel.</span></span> <span data-ttu-id="aab7a-141">When we pass this array of tasks to `Task.WhenAll`, we get back a task that won't complete *until all the copy operations have completed*.</span><span class="sxs-lookup"><span data-stu-id="aab7a-141">When we pass this array of tasks to `Task.WhenAll`, we get back a task that won't complete *until all the copy operations have completed*.</span></span> <span data-ttu-id="aab7a-142">If you're familiar with the Task Parallel Library (TPL) in .NET, then this is not new to you.</span><span class="sxs-lookup"><span data-stu-id="aab7a-142">If you're familiar with the Task Parallel Library (TPL) in .NET, then this is not new to you.</span></span> <span data-ttu-id="aab7a-143">The difference is that these tasks could be running on multiple VMs concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.</span><span class="sxs-lookup"><span data-stu-id="aab7a-143">The difference is that these tasks could be running on multiple VMs concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.</span></span>

<span data-ttu-id="aab7a-144">Tasks are very similar to the JavaScript concept of promises.</span><span class="sxs-lookup"><span data-stu-id="aab7a-144">Tasks are very similar to the JavaScript concept of promises.</span></span> <span data-ttu-id="aab7a-145">However, `Promise.all` has some differences from `Task.WhenAll`.</span><span class="sxs-lookup"><span data-stu-id="aab7a-145">However, `Promise.all` has some differences from `Task.WhenAll`.</span></span> <span data-ttu-id="aab7a-146">The concept of `Task.WhenAll` has been ported over as part of the `durable-functions` JavaScript module and is exclusive to it.</span><span class="sxs-lookup"><span data-stu-id="aab7a-146">The concept of `Task.WhenAll` has been ported over as part of the `durable-functions` JavaScript module and is exclusive to it.</span></span>

<span data-ttu-id="aab7a-147">After awaiting from `Task.WhenAll` (or yielding from `context.df.Task.all`), we know that all function calls have completed and have returned values back to us.</span><span class="sxs-lookup"><span data-stu-id="aab7a-147">After awaiting from `Task.WhenAll` (or yielding from `context.df.Task.all`), we know that all function calls have completed and have returned values back to us.</span></span> <span data-ttu-id="aab7a-148">Each call to `E2_CopyFileToBlob` returns the number of bytes uploaded, so calculating the sum total byte count is a matter of adding all those return values together.</span><span class="sxs-lookup"><span data-stu-id="aab7a-148">Each call to `E2_CopyFileToBlob` returns the number of bytes uploaded, so calculating the sum total byte count is a matter of adding all those return values together.</span></span>

## <a name="helper-activity-functions"></a><span data-ttu-id="aab7a-149">Helper activity functions</span><span class="sxs-lookup"><span data-stu-id="aab7a-149">Helper activity functions</span></span>

<span data-ttu-id="aab7a-150">The helper activity functions, as with other samples, are just regular functions that use the `activityTrigger` trigger binding.</span><span class="sxs-lookup"><span data-stu-id="aab7a-150">The helper activity functions, as with other samples, are just regular functions that use the `activityTrigger` trigger binding.</span></span> <span data-ttu-id="aab7a-151">For example, the *function.json* file for `E2_GetFileList` looks like the following:</span><span class="sxs-lookup"><span data-stu-id="aab7a-151">For example, the *function.json* file for `E2_GetFileList` looks like the following:</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E2_GetFileList/function.json)]

<span data-ttu-id="aab7a-152">And here is the implementation:</span><span class="sxs-lookup"><span data-stu-id="aab7a-152">And here is the implementation:</span></span>

### <a name="c"></a><span data-ttu-id="aab7a-153">C#</span><span class="sxs-lookup"><span data-stu-id="aab7a-153">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E2_GetFileList/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="aab7a-154">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="aab7a-154">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E2_GetFileList/index.js)]

<span data-ttu-id="aab7a-155">The JavaScript implementation of `E2_GetFileList` uses the `readdirp` module to recursively read the directory structure.</span><span class="sxs-lookup"><span data-stu-id="aab7a-155">The JavaScript implementation of `E2_GetFileList` uses the `readdirp` module to recursively read the directory structure.</span></span>

> [!NOTE]
> <span data-ttu-id="aab7a-156">You might be wondering why you couldn't just put this code directly into the orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="aab7a-156">You might be wondering why you couldn't just put this code directly into the orchestrator function.</span></span> <span data-ttu-id="aab7a-157">You could, but this would break one of the fundamental rules of orchestrator functions, which is that they should never do I/O, including local file system access.</span><span class="sxs-lookup"><span data-stu-id="aab7a-157">You could, but this would break one of the fundamental rules of orchestrator functions, which is that they should never do I/O, including local file system access.</span></span>

<span data-ttu-id="aab7a-158">The *function.json* file for `E2_CopyFileToBlob` is similarly simple:</span><span class="sxs-lookup"><span data-stu-id="aab7a-158">The *function.json* file for `E2_CopyFileToBlob` is similarly simple:</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E2_CopyFileToBlob/function.json)]

<span data-ttu-id="aab7a-159">The C# implementation is also pretty straightforward.</span><span class="sxs-lookup"><span data-stu-id="aab7a-159">The C# implementation is also pretty straightforward.</span></span> <span data-ttu-id="aab7a-160">It happens to use some advanced features of Azure Functions bindings (that is, the use of the `Binder` parameter), but you don't need to worry about those details for the purpose of this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aab7a-160">It happens to use some advanced features of Azure Functions bindings (that is, the use of the `Binder` parameter), but you don't need to worry about those details for the purpose of this walkthrough.</span></span>

### <a name="c"></a><span data-ttu-id="aab7a-161">C#</span><span class="sxs-lookup"><span data-stu-id="aab7a-161">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E2_CopyFileToBlob/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="aab7a-162">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="aab7a-162">JavaScript (Functions v2 only)</span></span>

<span data-ttu-id="aab7a-163">The JavaScript implementation does not have access to the `Binder` feature of Azure Functions, so the [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) takes its place.</span><span class="sxs-lookup"><span data-stu-id="aab7a-163">The JavaScript implementation does not have access to the `Binder` feature of Azure Functions, so the [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) takes its place.</span></span> <span data-ttu-id="aab7a-164">Note that the SDK requires an `AZURE_STORAGE_CONNECTION_STRING` app setting.</span><span class="sxs-lookup"><span data-stu-id="aab7a-164">Note that the SDK requires an `AZURE_STORAGE_CONNECTION_STRING` app setting.</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E2_CopyFileToBlob/index.js)]

<span data-ttu-id="aab7a-165">The implementation loads the file from disk and asynchronously streams the contents into a blob of the same name in the "backups" container.</span><span class="sxs-lookup"><span data-stu-id="aab7a-165">The implementation loads the file from disk and asynchronously streams the contents into a blob of the same name in the "backups" container.</span></span> <span data-ttu-id="aab7a-166">The return value is the number of bytes copied to storage, that is then used by the orchestrator function to compute the aggregate sum.</span><span class="sxs-lookup"><span data-stu-id="aab7a-166">The return value is the number of bytes copied to storage, that is then used by the orchestrator function to compute the aggregate sum.</span></span>

> [!NOTE]
> <span data-ttu-id="aab7a-167">This is a perfect example of moving I/O operations into an `activityTrigger` function.</span><span class="sxs-lookup"><span data-stu-id="aab7a-167">This is a perfect example of moving I/O operations into an `activityTrigger` function.</span></span> <span data-ttu-id="aab7a-168">Not only can the work be distributed across many different VMs, but you also get the benefits of checkpointing the progress.</span><span class="sxs-lookup"><span data-stu-id="aab7a-168">Not only can the work be distributed across many different VMs, but you also get the benefits of checkpointing the progress.</span></span> <span data-ttu-id="aab7a-169">If the host process gets terminated for any reason, you know which uploads have already completed.</span><span class="sxs-lookup"><span data-stu-id="aab7a-169">If the host process gets terminated for any reason, you know which uploads have already completed.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="aab7a-170">Run the sample</span><span class="sxs-lookup"><span data-stu-id="aab7a-170">Run the sample</span></span>

<span data-ttu-id="aab7a-171">You can start the orchestration by sending the following HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="aab7a-171">You can start the orchestration by sending the following HTTP POST request.</span></span>

```
POST http://{host}/orchestrators/E2_BackupSiteContent
Content-Type: application/json
Content-Length: 20

"D:\\home\\LogFiles"
```

> [!NOTE]
> <span data-ttu-id="aab7a-172">The `HttpStart` function that you are invoking only works with JSON-formatted content.</span><span class="sxs-lookup"><span data-stu-id="aab7a-172">The `HttpStart` function that you are invoking only works with JSON-formatted content.</span></span> <span data-ttu-id="aab7a-173">For this reason, the `Content-Type: application/json` header is required and the directory path is encoded as a JSON string.</span><span class="sxs-lookup"><span data-stu-id="aab7a-173">For this reason, the `Content-Type: application/json` header is required and the directory path is encoded as a JSON string.</span></span>

<span data-ttu-id="aab7a-174">This HTTP request triggers the `E2_BackupSiteContent` orchestrator and passes the string `D:\home\LogFiles` as a parameter.</span><span class="sxs-lookup"><span data-stu-id="aab7a-174">This HTTP request triggers the `E2_BackupSiteContent` orchestrator and passes the string `D:\home\LogFiles` as a parameter.</span></span> <span data-ttu-id="aab7a-175">The response provides a link to get the status of the backup operation:</span><span class="sxs-lookup"><span data-stu-id="aab7a-175">The response provides a link to get the status of the backup operation:</span></span>

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

(...trimmed...)
```

<span data-ttu-id="aab7a-176">Depending on how many log files you have in your function app, this operation could take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="aab7a-176">Depending on how many log files you have in your function app, this operation could take several minutes to complete.</span></span> <span data-ttu-id="aab7a-177">You can get the latest status by querying the URL in the `Location` header of the previous HTTP 202 response.</span><span class="sxs-lookup"><span data-stu-id="aab7a-177">You can get the latest status by querying the URL in the `Location` header of the previous HTTP 202 response.</span></span>

```
GET http://{host}/admin/extensions/DurableTaskExtension/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```

```
HTTP/1.1 202 Accepted
Content-Length: 148
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

{"runtimeStatus":"Running","input":"D:\\home\\LogFiles","output":null,"createdTime":"2017-06-29T18:50:55Z","lastUpdatedTime":"2017-06-29T18:51:16Z"}
```

<span data-ttu-id="aab7a-178">In this case, the function is still running.</span><span class="sxs-lookup"><span data-stu-id="aab7a-178">In this case, the function is still running.</span></span> <span data-ttu-id="aab7a-179">You are able to see the input that was saved into the orchestrator state and the last updated time.</span><span class="sxs-lookup"><span data-stu-id="aab7a-179">You are able to see the input that was saved into the orchestrator state and the last updated time.</span></span> <span data-ttu-id="aab7a-180">You can continue to use the `Location` header values to poll for completion.</span><span class="sxs-lookup"><span data-stu-id="aab7a-180">You can continue to use the `Location` header values to poll for completion.</span></span> <span data-ttu-id="aab7a-181">When the status is "Completed", you see an HTTP response value similar to the following:</span><span class="sxs-lookup"><span data-stu-id="aab7a-181">When the status is "Completed", you see an HTTP response value similar to the following:</span></span>

```
HTTP/1.1 200 OK
Content-Length: 152
Content-Type: application/json; charset=utf-8

{"runtimeStatus":"Completed","input":"D:\\home\\LogFiles","output":452071,"createdTime":"2017-06-29T18:50:55Z","lastUpdatedTime":"2017-06-29T18:51:26Z"}
```

<span data-ttu-id="aab7a-182">Now you can see that the orchestration is complete and approximately how much time it took to complete.</span><span class="sxs-lookup"><span data-stu-id="aab7a-182">Now you can see that the orchestration is complete and approximately how much time it took to complete.</span></span> <span data-ttu-id="aab7a-183">You also see a value for the `output` field, which indicates that around 450 KB of logs were uploaded.</span><span class="sxs-lookup"><span data-stu-id="aab7a-183">You also see a value for the `output` field, which indicates that around 450 KB of logs were uploaded.</span></span>

## <a name="visual-studio-sample-code"></a><span data-ttu-id="aab7a-184">Visual Studio sample code</span><span class="sxs-lookup"><span data-stu-id="aab7a-184">Visual Studio sample code</span></span>

<span data-ttu-id="aab7a-185">Here is the orchestration as a single C# file in a Visual Studio project:</span><span class="sxs-lookup"><span data-stu-id="aab7a-185">Here is the orchestration as a single C# file in a Visual Studio project:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/BackupSiteContent.cs)]

## <a name="next-steps"></a><span data-ttu-id="aab7a-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="aab7a-186">Next steps</span></span>

<span data-ttu-id="aab7a-187">This sample has shown how to implement the fan-out/fan-in pattern.</span><span class="sxs-lookup"><span data-stu-id="aab7a-187">This sample has shown how to implement the fan-out/fan-in pattern.</span></span> <span data-ttu-id="aab7a-188">The next sample shows how to implement the monitor pattern using [durable timers](durable-functions-timers.md).</span><span class="sxs-lookup"><span data-stu-id="aab7a-188">The next sample shows how to implement the monitor pattern using [durable timers](durable-functions-timers.md).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aab7a-189">Run the monitor sample</span><span class="sxs-lookup"><span data-stu-id="aab7a-189">Run the monitor sample</span></span>](durable-functions-monitor.md)
