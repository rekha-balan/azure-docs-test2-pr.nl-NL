---
title: How to use Azure queue storage with the WebJobs SDK
description: Learn how to use Azure queue storage with the WebJobs SDK. Create and delete queues; insert, peek, get, and delete queue messages, and more.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 73056751ac4cced5ea691977b5ea6483d2b63802
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552391"
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="94273-104">How to use Azure queue storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="94273-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="94273-105">Overview</span><span class="sxs-lookup"><span data-stu-id="94273-105">Overview</span></span>
<span data-ttu-id="94273-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span><span class="sxs-lookup"><span data-stu-id="94273-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="94273-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="94273-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="94273-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span><span class="sxs-lookup"><span data-stu-id="94273-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="94273-109">The guide includes the following topics:</span><span class="sxs-lookup"><span data-stu-id="94273-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="94273-110">How to trigger a function when a queue message is received</span><span class="sxs-lookup"><span data-stu-id="94273-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="94273-111">String queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-111">String queue messages</span></span>
  * <span data-ttu-id="94273-112">POCO queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-112">POCO queue messages</span></span>
  * <span data-ttu-id="94273-113">Async functions</span><span class="sxs-lookup"><span data-stu-id="94273-113">Async functions</span></span>
  * <span data-ttu-id="94273-114">Types the QueueTrigger attribute works with</span><span class="sxs-lookup"><span data-stu-id="94273-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="94273-115">Polling algorithm</span><span class="sxs-lookup"><span data-stu-id="94273-115">Polling algorithm</span></span>
  * <span data-ttu-id="94273-116">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="94273-116">Multiple instances</span></span>
  * <span data-ttu-id="94273-117">Parallel execution</span><span class="sxs-lookup"><span data-stu-id="94273-117">Parallel execution</span></span>
  * <span data-ttu-id="94273-118">Get queue or queue message metadata</span><span class="sxs-lookup"><span data-stu-id="94273-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="94273-119">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="94273-119">Graceful shutdown</span></span>
* [<span data-ttu-id="94273-120">How to create a queue message while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="94273-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="94273-121">String queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-121">String queue messages</span></span>
  * <span data-ttu-id="94273-122">POCO queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-122">POCO queue messages</span></span>
  * <span data-ttu-id="94273-123">Create multiple messages or in async functions</span><span class="sxs-lookup"><span data-stu-id="94273-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="94273-124">Types the Queue attribute works with</span><span class="sxs-lookup"><span data-stu-id="94273-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="94273-125">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="94273-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="94273-126">How to read and write blobs while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="94273-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="94273-127">String queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-127">String queue messages</span></span>
  * <span data-ttu-id="94273-128">POCO queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-128">POCO queue messages</span></span>
  * <span data-ttu-id="94273-129">Types the Blob attribute works with</span><span class="sxs-lookup"><span data-stu-id="94273-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="94273-130">How to handle poison messages</span><span class="sxs-lookup"><span data-stu-id="94273-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="94273-131">Automatic poison message handling</span><span class="sxs-lookup"><span data-stu-id="94273-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="94273-132">Manual poison message handling</span><span class="sxs-lookup"><span data-stu-id="94273-132">Manual poison message handling</span></span>
* [<span data-ttu-id="94273-133">How to set configuration options</span><span class="sxs-lookup"><span data-stu-id="94273-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="94273-134">Set SDK connection strings in code</span><span class="sxs-lookup"><span data-stu-id="94273-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="94273-135">Configure QueueTrigger settings</span><span class="sxs-lookup"><span data-stu-id="94273-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="94273-136">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="94273-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="94273-137">How to trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="94273-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="94273-138">How to write logs</span><span class="sxs-lookup"><span data-stu-id="94273-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="94273-139">How to handle errors and configure timeouts</span><span class="sxs-lookup"><span data-stu-id="94273-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="94273-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="94273-140">Next steps</span></span>](#nextsteps)

## <a id="trigger"></a> <span data-ttu-id="94273-141">How to trigger a function when a queue message is received</span><span class="sxs-lookup"><span data-stu-id="94273-141">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="94273-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="94273-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="94273-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span><span class="sxs-lookup"><span data-stu-id="94273-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="94273-144">You can also [set the queue name dynamically](#config).</span><span class="sxs-lookup"><span data-stu-id="94273-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="94273-145">String queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-145">String queue messages</span></span>
<span data-ttu-id="94273-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span><span class="sxs-lookup"><span data-stu-id="94273-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="94273-147">The function [writes a log message to the Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="94273-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="94273-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span><span class="sxs-lookup"><span data-stu-id="94273-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="94273-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="94273-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span><span class="sxs-lookup"><span data-stu-id="94273-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="94273-151">The SDK automatically deserializes the object.</span><span class="sxs-lookup"><span data-stu-id="94273-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="94273-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span><span class="sxs-lookup"><span data-stu-id="94273-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="94273-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span><span class="sxs-lookup"><span data-stu-id="94273-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="94273-154">Async functions</span><span class="sxs-lookup"><span data-stu-id="94273-154">Async functions</span></span>
<span data-ttu-id="94273-155">The following async function [writes a log to the Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="94273-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="94273-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span><span class="sxs-lookup"><span data-stu-id="94273-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="94273-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span><span class="sxs-lookup"><span data-stu-id="94273-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a> <span data-ttu-id="94273-158">Types the QueueTrigger attribute works with</span><span class="sxs-lookup"><span data-stu-id="94273-158">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="94273-159">You can use `QueueTrigger` with the following types:</span><span class="sxs-lookup"><span data-stu-id="94273-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="94273-160">A POCO type serialized as JSON</span><span class="sxs-lookup"><span data-stu-id="94273-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a> <span data-ttu-id="94273-161">Polling algorithm</span><span class="sxs-lookup"><span data-stu-id="94273-161">Polling algorithm</span></span>
<span data-ttu-id="94273-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span><span class="sxs-lookup"><span data-stu-id="94273-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="94273-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span><span class="sxs-lookup"><span data-stu-id="94273-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="94273-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span><span class="sxs-lookup"><span data-stu-id="94273-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="94273-165">[The maximum wait time is configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="94273-165">[The maximum wait time is configurable](#config).</span></span>

### <a id="instances"></a> <span data-ttu-id="94273-166">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="94273-166">Multiple instances</span></span>
<span data-ttu-id="94273-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span><span class="sxs-lookup"><span data-stu-id="94273-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="94273-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span><span class="sxs-lookup"><span data-stu-id="94273-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="94273-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span><span class="sxs-lookup"><span data-stu-id="94273-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <a id="parallel"></a> <span data-ttu-id="94273-170">Parallel execution</span><span class="sxs-lookup"><span data-stu-id="94273-170">Parallel execution</span></span>
<span data-ttu-id="94273-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span><span class="sxs-lookup"><span data-stu-id="94273-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="94273-172">The same is true when multiple messages are received for a single queue.</span><span class="sxs-lookup"><span data-stu-id="94273-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="94273-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span><span class="sxs-lookup"><span data-stu-id="94273-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="94273-174">[The batch size is configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="94273-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="94273-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span><span class="sxs-lookup"><span data-stu-id="94273-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="94273-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span><span class="sxs-lookup"><span data-stu-id="94273-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="94273-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="94273-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="94273-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span><span class="sxs-lookup"><span data-stu-id="94273-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="94273-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="94273-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <a id="queuemetadata"></a><span data-ttu-id="94273-180">Get queue or queue message metadata</span><span class="sxs-lookup"><span data-stu-id="94273-180">Get queue or queue message metadata</span></span>
<span data-ttu-id="94273-181">You can get the following message properties by adding parameters to the method signature:</span><span class="sxs-lookup"><span data-stu-id="94273-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="94273-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="94273-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="94273-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="94273-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="94273-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="94273-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="94273-185">`string` queueTrigger (contains message text)</span><span class="sxs-lookup"><span data-stu-id="94273-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="94273-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="94273-186">`string` id</span></span>
* <span data-ttu-id="94273-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="94273-187">`string` popReceipt</span></span>
* <span data-ttu-id="94273-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="94273-188">`int` dequeueCount</span></span>

<span data-ttu-id="94273-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="94273-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="94273-190">The following example writes all of this metadata to an INFO application log.</span><span class="sxs-lookup"><span data-stu-id="94273-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="94273-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span><span class="sxs-lookup"><span data-stu-id="94273-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="94273-192">Here is a sample log written by the sample code:</span><span class="sxs-lookup"><span data-stu-id="94273-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a><span data-ttu-id="94273-193">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="94273-193">Graceful shutdown</span></span>
<span data-ttu-id="94273-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span><span class="sxs-lookup"><span data-stu-id="94273-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="94273-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span><span class="sxs-lookup"><span data-stu-id="94273-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="94273-196">The following example shows how to check for impending WebJob termination in a function.</span><span class="sxs-lookup"><span data-stu-id="94273-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="94273-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span><span class="sxs-lookup"><span data-stu-id="94273-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="94273-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="94273-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a id="createqueue"></a> <span data-ttu-id="94273-199">How to create a queue message while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="94273-199">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="94273-200">To write a function that creates a new queue message, use the `Queue` attribute.</span><span class="sxs-lookup"><span data-stu-id="94273-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="94273-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span><span class="sxs-lookup"><span data-stu-id="94273-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="94273-202">String queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-202">String queue messages</span></span>
<span data-ttu-id="94273-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="94273-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="94273-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span><span class="sxs-lookup"><span data-stu-id="94273-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="94273-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="94273-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span><span class="sxs-lookup"><span data-stu-id="94273-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="94273-207">The SDK automatically serializes the object to JSON.</span><span class="sxs-lookup"><span data-stu-id="94273-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="94273-208">A queue message is always created, even if the object is null.</span><span class="sxs-lookup"><span data-stu-id="94273-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="94273-209">Create multiple messages or in async functions</span><span class="sxs-lookup"><span data-stu-id="94273-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="94273-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="94273-211">Each queue message is created immediately when the `Add` method is called.</span><span class="sxs-lookup"><span data-stu-id="94273-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="94273-212">Types that the Queue attribute works with</span><span class="sxs-lookup"><span data-stu-id="94273-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="94273-213">You can use the `Queue` attribute on the following parameter types:</span><span class="sxs-lookup"><span data-stu-id="94273-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="94273-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span><span class="sxs-lookup"><span data-stu-id="94273-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="94273-215">`out byte[]` (works like `string`)</span><span class="sxs-lookup"><span data-stu-id="94273-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="94273-216">`out CloudQueueMessage` (works like `string`)</span><span class="sxs-lookup"><span data-stu-id="94273-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="94273-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span><span class="sxs-lookup"><span data-stu-id="94273-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="94273-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span><span class="sxs-lookup"><span data-stu-id="94273-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <a id="ibinder"></a><span data-ttu-id="94273-219">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="94273-219">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="94273-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="94273-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="94273-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span><span class="sxs-lookup"><span data-stu-id="94273-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="94273-222">The output queue name is set by code in the body of the function.</span><span class="sxs-lookup"><span data-stu-id="94273-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="94273-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span><span class="sxs-lookup"><span data-stu-id="94273-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <a id="blobs"></a> <span data-ttu-id="94273-224">How to read and write blobs and tables while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="94273-224">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="94273-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span><span class="sxs-lookup"><span data-stu-id="94273-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="94273-226">The samples in this section apply to blobs.</span><span class="sxs-lookup"><span data-stu-id="94273-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="94273-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="94273-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="94273-228">String queue messages triggering blob operations</span><span class="sxs-lookup"><span data-stu-id="94273-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="94273-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span><span class="sxs-lookup"><span data-stu-id="94273-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="94273-230">The following example uses `Stream` objects to read and write blobs.</span><span class="sxs-lookup"><span data-stu-id="94273-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="94273-231">The queue message is the name of a blob located in the textblobs container.</span><span class="sxs-lookup"><span data-stu-id="94273-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="94273-232">A copy of the blob with "-new" appended to the name is created in the same container.</span><span class="sxs-lookup"><span data-stu-id="94273-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="94273-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span><span class="sxs-lookup"><span data-stu-id="94273-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="94273-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="94273-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="94273-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span><span class="sxs-lookup"><span data-stu-id="94273-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="94273-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span><span class="sxs-lookup"><span data-stu-id="94273-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="94273-237">The queue message is the name of the blob.</span><span class="sxs-lookup"><span data-stu-id="94273-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a> <span data-ttu-id="94273-238">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="94273-238">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="94273-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="94273-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="94273-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span><span class="sxs-lookup"><span data-stu-id="94273-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="94273-241">The following example copies a blob to a new blob with a different extension.</span><span class="sxs-lookup"><span data-stu-id="94273-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="94273-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span><span class="sxs-lookup"><span data-stu-id="94273-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="94273-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span><span class="sxs-lookup"><span data-stu-id="94273-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="94273-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span><span class="sxs-lookup"><span data-stu-id="94273-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="94273-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span><span class="sxs-lookup"><span data-stu-id="94273-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="94273-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="94273-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <a id="blobattributetypes"></a> <span data-ttu-id="94273-247">Types you can use the Blob attribute with</span><span class="sxs-lookup"><span data-stu-id="94273-247">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="94273-248">The `Blob` attribute can be used with the following types:</span><span class="sxs-lookup"><span data-stu-id="94273-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="94273-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span><span class="sxs-lookup"><span data-stu-id="94273-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="94273-250">`string` (read)</span><span class="sxs-lookup"><span data-stu-id="94273-250">`string` (read)</span></span>
* <span data-ttu-id="94273-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span><span class="sxs-lookup"><span data-stu-id="94273-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="94273-252">POCO (read)</span><span class="sxs-lookup"><span data-stu-id="94273-252">POCO (read)</span></span>
* <span data-ttu-id="94273-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span><span class="sxs-lookup"><span data-stu-id="94273-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="94273-254">`CloudBlobStream` (write)</span><span class="sxs-lookup"><span data-stu-id="94273-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="94273-255">`ICloudBlob` (read or write)</span><span class="sxs-lookup"><span data-stu-id="94273-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="94273-256">`CloudBlockBlob` (read or write)</span><span class="sxs-lookup"><span data-stu-id="94273-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="94273-257">`CloudPageBlob` (read or write)</span><span class="sxs-lookup"><span data-stu-id="94273-257">`CloudPageBlob` (read or write)</span></span>

## <a id="poison"></a> <span data-ttu-id="94273-258">How to handle poison messages</span><span class="sxs-lookup"><span data-stu-id="94273-258">How to handle poison messages</span></span>
<span data-ttu-id="94273-259">Messages whose content causes a function to fail are called *poison messages*.</span><span class="sxs-lookup"><span data-stu-id="94273-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="94273-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span><span class="sxs-lookup"><span data-stu-id="94273-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="94273-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span><span class="sxs-lookup"><span data-stu-id="94273-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="94273-262">Automatic poison message handling</span><span class="sxs-lookup"><span data-stu-id="94273-262">Automatic poison message handling</span></span>
<span data-ttu-id="94273-263">The SDK will call a function up to 5 times to process a queue message.</span><span class="sxs-lookup"><span data-stu-id="94273-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="94273-264">If the fifth try fails, the message is moved to a poison queue.</span><span class="sxs-lookup"><span data-stu-id="94273-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="94273-265">[The maximum number of retries is configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="94273-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="94273-266">The poison queue is named *{originalqueuename}*-poison.</span><span class="sxs-lookup"><span data-stu-id="94273-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="94273-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span><span class="sxs-lookup"><span data-stu-id="94273-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="94273-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="94273-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="94273-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span><span class="sxs-lookup"><span data-stu-id="94273-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="94273-270">The `ProcessPoisonMessage` then logs the poison message.</span><span class="sxs-lookup"><span data-stu-id="94273-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="94273-271">The following illustration shows console output from these functions when a poison message is processed.</span><span class="sxs-lookup"><span data-stu-id="94273-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Console output for poison message handling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="94273-273">Manual poison message handling</span><span class="sxs-lookup"><span data-stu-id="94273-273">Manual poison message handling</span></span>
<span data-ttu-id="94273-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span><span class="sxs-lookup"><span data-stu-id="94273-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="94273-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a> <span data-ttu-id="94273-276">How to set configuration options</span><span class="sxs-lookup"><span data-stu-id="94273-276">How to set configuration options</span></span>
<span data-ttu-id="94273-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span><span class="sxs-lookup"><span data-stu-id="94273-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="94273-278">Set the SDK connection strings in code.</span><span class="sxs-lookup"><span data-stu-id="94273-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="94273-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span><span class="sxs-lookup"><span data-stu-id="94273-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="94273-280">Get queue names from configuration.</span><span class="sxs-lookup"><span data-stu-id="94273-280">Get queue names from configuration.</span></span>

### <a id="setconnstr"></a><span data-ttu-id="94273-281">Set SDK connection strings in code</span><span class="sxs-lookup"><span data-stu-id="94273-281">Set SDK connection strings in code</span></span>
<span data-ttu-id="94273-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="configqueue"></a><span data-ttu-id="94273-283">Configure QueueTrigger  settings</span><span class="sxs-lookup"><span data-stu-id="94273-283">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="94273-284">You can configure the following settings that apply to the queue message processing:</span><span class="sxs-lookup"><span data-stu-id="94273-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="94273-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span><span class="sxs-lookup"><span data-stu-id="94273-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="94273-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span><span class="sxs-lookup"><span data-stu-id="94273-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="94273-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span><span class="sxs-lookup"><span data-stu-id="94273-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="94273-288">The following example shows how to configure these settings:</span><span class="sxs-lookup"><span data-stu-id="94273-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a><span data-ttu-id="94273-289">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="94273-289">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="94273-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span><span class="sxs-lookup"><span data-stu-id="94273-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="94273-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span><span class="sxs-lookup"><span data-stu-id="94273-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="94273-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span><span class="sxs-lookup"><span data-stu-id="94273-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="94273-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span><span class="sxs-lookup"><span data-stu-id="94273-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="94273-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span><span class="sxs-lookup"><span data-stu-id="94273-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="94273-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span><span class="sxs-lookup"><span data-stu-id="94273-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="94273-296">If the `appSettings` key is logqueue, your function could look like the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="94273-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="94273-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="94273-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="94273-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span><span class="sxs-lookup"><span data-stu-id="94273-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="94273-300">You can't change blob container name while the job is running.</span><span class="sxs-lookup"><span data-stu-id="94273-300">You can't change blob container name while the job is running.</span></span>

## <a id="manual"></a><span data-ttu-id="94273-301">How to trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="94273-301">How to trigger a function manually</span></span>
<span data-ttu-id="94273-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a id="logs"></a><span data-ttu-id="94273-303">How to write logs</span><span class="sxs-lookup"><span data-stu-id="94273-303">How to write logs</span></span>
<span data-ttu-id="94273-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span><span class="sxs-lookup"><span data-stu-id="94273-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logs in WebJob page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logs in function invocation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="94273-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span><span class="sxs-lookup"><span data-stu-id="94273-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="94273-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span><span class="sxs-lookup"><span data-stu-id="94273-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="94273-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span><span class="sxs-lookup"><span data-stu-id="94273-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="94273-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span><span class="sxs-lookup"><span data-stu-id="94273-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="94273-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span><span class="sxs-lookup"><span data-stu-id="94273-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="94273-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span><span class="sxs-lookup"><span data-stu-id="94273-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="94273-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="94273-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="94273-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span><span class="sxs-lookup"><span data-stu-id="94273-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="94273-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span><span class="sxs-lookup"><span data-stu-id="94273-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="94273-316">Disable dashboard logging for high throughput scenarios.</span><span class="sxs-lookup"><span data-stu-id="94273-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="94273-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span><span class="sxs-lookup"><span data-stu-id="94273-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="94273-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="94273-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="94273-319">The following example shows several ways to write logs:</span><span class="sxs-lookup"><span data-stu-id="94273-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="94273-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span><span class="sxs-lookup"><span data-stu-id="94273-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Click function invocation link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logs in function invocation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="94273-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span><span class="sxs-lookup"><span data-stu-id="94273-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Click Toggle Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="94273-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span><span class="sxs-lookup"><span data-stu-id="94273-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="94273-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="94273-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="94273-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span><span class="sxs-lookup"><span data-stu-id="94273-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Info log in table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Error log in table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="94273-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="94273-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <a id="errors"></a><span data-ttu-id="94273-331">How to handle errors and configure timeouts</span><span class="sxs-lookup"><span data-stu-id="94273-331">How to handle errors and configure timeouts</span></span>
<span data-ttu-id="94273-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="94273-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="94273-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="94273-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="94273-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="94273-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="94273-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span><span class="sxs-lookup"><span data-stu-id="94273-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="94273-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="94273-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <a id="nextsteps"></a> <span data-ttu-id="94273-337">Next steps</span><span class="sxs-lookup"><span data-stu-id="94273-337">Next steps</span></span>
<span data-ttu-id="94273-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span><span class="sxs-lookup"><span data-stu-id="94273-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="94273-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="94273-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>








