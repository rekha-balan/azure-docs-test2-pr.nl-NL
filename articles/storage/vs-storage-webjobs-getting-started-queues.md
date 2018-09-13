---
title: Getting started with queue storage and Visual Studio connected services (WebJob projects) | Microsoft Docs
description: How to get started using Azure Queue storage in a WebJob project after connecting to a storage account using Visual Studio connected services.
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 6892610b6a16b79208078b26530dfbbb67c0b304
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553234"
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="1ba17-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span><span class="sxs-lookup"><span data-stu-id="1ba17-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="1ba17-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1ba17-104">Overview</span></span>
<span data-ttu-id="1ba17-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1ba17-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="1ba17-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span><span class="sxs-lookup"><span data-stu-id="1ba17-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="1ba17-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span><span class="sxs-lookup"><span data-stu-id="1ba17-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="1ba17-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1ba17-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="1ba17-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span><span class="sxs-lookup"><span data-stu-id="1ba17-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="1ba17-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="1ba17-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="1ba17-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="1ba17-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="1ba17-112">How to trigger a function when a queue message is received</span><span class="sxs-lookup"><span data-stu-id="1ba17-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="1ba17-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span><span class="sxs-lookup"><span data-stu-id="1ba17-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="1ba17-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span><span class="sxs-lookup"><span data-stu-id="1ba17-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="1ba17-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="1ba17-116">String queue messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-116">String queue messages</span></span>
<span data-ttu-id="1ba17-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span><span class="sxs-lookup"><span data-stu-id="1ba17-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="1ba17-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="1ba17-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="1ba17-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span><span class="sxs-lookup"><span data-stu-id="1ba17-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="1ba17-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1ba17-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span><span class="sxs-lookup"><span data-stu-id="1ba17-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="1ba17-122">The SDK automatically deserializes the object.</span><span class="sxs-lookup"><span data-stu-id="1ba17-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="1ba17-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span><span class="sxs-lookup"><span data-stu-id="1ba17-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="1ba17-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span><span class="sxs-lookup"><span data-stu-id="1ba17-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="1ba17-125">Async functions</span><span class="sxs-lookup"><span data-stu-id="1ba17-125">Async functions</span></span>
<span data-ttu-id="1ba17-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="1ba17-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="1ba17-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span><span class="sxs-lookup"><span data-stu-id="1ba17-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="1ba17-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span><span class="sxs-lookup"><span data-stu-id="1ba17-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="1ba17-129">Types the QueueTrigger attribute works with</span><span class="sxs-lookup"><span data-stu-id="1ba17-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="1ba17-130">You can use **QueueTrigger** with the following types:</span><span class="sxs-lookup"><span data-stu-id="1ba17-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="1ba17-131">**string**</span><span class="sxs-lookup"><span data-stu-id="1ba17-131">**string**</span></span>
* <span data-ttu-id="1ba17-132">A POCO type serialized as JSON</span><span class="sxs-lookup"><span data-stu-id="1ba17-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="1ba17-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="1ba17-133">**byte[]**</span></span>
* <span data-ttu-id="1ba17-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="1ba17-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="1ba17-135">Polling algorithm</span><span class="sxs-lookup"><span data-stu-id="1ba17-135">Polling algorithm</span></span>
<span data-ttu-id="1ba17-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span><span class="sxs-lookup"><span data-stu-id="1ba17-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="1ba17-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span><span class="sxs-lookup"><span data-stu-id="1ba17-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="1ba17-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span><span class="sxs-lookup"><span data-stu-id="1ba17-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="1ba17-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="1ba17-140">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="1ba17-140">Multiple instances</span></span>
<span data-ttu-id="1ba17-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span><span class="sxs-lookup"><span data-stu-id="1ba17-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="1ba17-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span><span class="sxs-lookup"><span data-stu-id="1ba17-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="1ba17-143">Parallel execution</span><span class="sxs-lookup"><span data-stu-id="1ba17-143">Parallel execution</span></span>
<span data-ttu-id="1ba17-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span><span class="sxs-lookup"><span data-stu-id="1ba17-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="1ba17-145">The same is true when multiple messages are received for a single queue.</span><span class="sxs-lookup"><span data-stu-id="1ba17-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="1ba17-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span><span class="sxs-lookup"><span data-stu-id="1ba17-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="1ba17-147">[The batch size is configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="1ba17-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span><span class="sxs-lookup"><span data-stu-id="1ba17-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="1ba17-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span><span class="sxs-lookup"><span data-stu-id="1ba17-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="1ba17-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span><span class="sxs-lookup"><span data-stu-id="1ba17-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="1ba17-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span><span class="sxs-lookup"><span data-stu-id="1ba17-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="1ba17-152">Get queue or queue message metadata</span><span class="sxs-lookup"><span data-stu-id="1ba17-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="1ba17-153">You can get the following message properties by adding parameters to the method signature:</span><span class="sxs-lookup"><span data-stu-id="1ba17-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="1ba17-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="1ba17-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="1ba17-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="1ba17-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="1ba17-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="1ba17-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="1ba17-157">**string** queueTrigger (contains message text)</span><span class="sxs-lookup"><span data-stu-id="1ba17-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="1ba17-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="1ba17-158">**string** id</span></span>
* <span data-ttu-id="1ba17-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="1ba17-159">**string** popReceipt</span></span>
* <span data-ttu-id="1ba17-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="1ba17-160">**int** dequeueCount</span></span>

<span data-ttu-id="1ba17-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span><span class="sxs-lookup"><span data-stu-id="1ba17-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="1ba17-162">The following example writes all of this metadata to an INFO application log.</span><span class="sxs-lookup"><span data-stu-id="1ba17-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="1ba17-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span><span class="sxs-lookup"><span data-stu-id="1ba17-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="1ba17-164">Here is a sample log written by the sample code:</span><span class="sxs-lookup"><span data-stu-id="1ba17-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="1ba17-165">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="1ba17-165">Graceful shutdown</span></span>
<span data-ttu-id="1ba17-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span><span class="sxs-lookup"><span data-stu-id="1ba17-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="1ba17-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span><span class="sxs-lookup"><span data-stu-id="1ba17-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="1ba17-168">The following example shows how to check for impending WebJob termination in a function.</span><span class="sxs-lookup"><span data-stu-id="1ba17-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="1ba17-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span><span class="sxs-lookup"><span data-stu-id="1ba17-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="1ba17-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="1ba17-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="1ba17-171">How to create a queue message while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="1ba17-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="1ba17-172">To write a function that creates a new queue message, use the **Queue** attribute.</span><span class="sxs-lookup"><span data-stu-id="1ba17-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="1ba17-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="1ba17-174">String queue messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-174">String queue messages</span></span>
<span data-ttu-id="1ba17-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="1ba17-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="1ba17-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span><span class="sxs-lookup"><span data-stu-id="1ba17-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="1ba17-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1ba17-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span><span class="sxs-lookup"><span data-stu-id="1ba17-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="1ba17-179">The SDK automatically serializes the object to JSON.</span><span class="sxs-lookup"><span data-stu-id="1ba17-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="1ba17-180">A queue message is always created, even if the object is null.</span><span class="sxs-lookup"><span data-stu-id="1ba17-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="1ba17-181">Create multiple messages or in async functions</span><span class="sxs-lookup"><span data-stu-id="1ba17-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="1ba17-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="1ba17-183">Each queue message is created immediately when the **Add** method is called.</span><span class="sxs-lookup"><span data-stu-id="1ba17-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="1ba17-184">Types that the Queue attribute works with</span><span class="sxs-lookup"><span data-stu-id="1ba17-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="1ba17-185">You can use the **Queue** attribute on the following parameter types:</span><span class="sxs-lookup"><span data-stu-id="1ba17-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="1ba17-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span><span class="sxs-lookup"><span data-stu-id="1ba17-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="1ba17-187">**out byte[]** (works like **string**)</span><span class="sxs-lookup"><span data-stu-id="1ba17-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="1ba17-188">**out CloudQueueMessage** (works like **string**)</span><span class="sxs-lookup"><span data-stu-id="1ba17-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="1ba17-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span><span class="sxs-lookup"><span data-stu-id="1ba17-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="1ba17-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="1ba17-190">**ICollector**</span></span>
* <span data-ttu-id="1ba17-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="1ba17-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="1ba17-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span><span class="sxs-lookup"><span data-stu-id="1ba17-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="1ba17-193">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="1ba17-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="1ba17-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span><span class="sxs-lookup"><span data-stu-id="1ba17-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="1ba17-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span><span class="sxs-lookup"><span data-stu-id="1ba17-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="1ba17-196">The output queue name is set by code in the body of the function.</span><span class="sxs-lookup"><span data-stu-id="1ba17-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="1ba17-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span><span class="sxs-lookup"><span data-stu-id="1ba17-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="1ba17-198">How to read and write blobs and tables while processing a queue message</span><span class="sxs-lookup"><span data-stu-id="1ba17-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="1ba17-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span><span class="sxs-lookup"><span data-stu-id="1ba17-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="1ba17-200">The samples in this section apply to blobs.</span><span class="sxs-lookup"><span data-stu-id="1ba17-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="1ba17-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="1ba17-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="1ba17-202">String queue messages triggering blob operations</span><span class="sxs-lookup"><span data-stu-id="1ba17-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="1ba17-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span><span class="sxs-lookup"><span data-stu-id="1ba17-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="1ba17-204">The following example uses **Stream** objects to read and write blobs.</span><span class="sxs-lookup"><span data-stu-id="1ba17-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="1ba17-205">The queue message is the name of a blob located in the textblobs container.</span><span class="sxs-lookup"><span data-stu-id="1ba17-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="1ba17-206">A copy of the blob with "-new" appended to the name is created in the same container.</span><span class="sxs-lookup"><span data-stu-id="1ba17-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="1ba17-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span><span class="sxs-lookup"><span data-stu-id="1ba17-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="1ba17-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="1ba17-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="1ba17-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span><span class="sxs-lookup"><span data-stu-id="1ba17-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="1ba17-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span><span class="sxs-lookup"><span data-stu-id="1ba17-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="1ba17-211">The queue message is the name of the blob.</span><span class="sxs-lookup"><span data-stu-id="1ba17-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="1ba17-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1ba17-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span><span class="sxs-lookup"><span data-stu-id="1ba17-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="1ba17-214">You can also use queue metadata property names as placeholders.</span><span class="sxs-lookup"><span data-stu-id="1ba17-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="1ba17-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="1ba17-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="1ba17-216">The following example copies a blob to a new blob with a different extension.</span><span class="sxs-lookup"><span data-stu-id="1ba17-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="1ba17-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span><span class="sxs-lookup"><span data-stu-id="1ba17-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="1ba17-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span><span class="sxs-lookup"><span data-stu-id="1ba17-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="1ba17-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span><span class="sxs-lookup"><span data-stu-id="1ba17-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="1ba17-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span><span class="sxs-lookup"><span data-stu-id="1ba17-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="1ba17-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="1ba17-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="1ba17-222">Types you can use the Blob attribute with</span><span class="sxs-lookup"><span data-stu-id="1ba17-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="1ba17-223">The **Blob** attribute can be used with the following types:</span><span class="sxs-lookup"><span data-stu-id="1ba17-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="1ba17-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span><span class="sxs-lookup"><span data-stu-id="1ba17-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="1ba17-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="1ba17-225">**TextReader**</span></span>
* <span data-ttu-id="1ba17-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="1ba17-226">**TextWriter**</span></span>
* <span data-ttu-id="1ba17-227">**string** (read)</span><span class="sxs-lookup"><span data-stu-id="1ba17-227">**string** (read)</span></span>
* <span data-ttu-id="1ba17-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span><span class="sxs-lookup"><span data-stu-id="1ba17-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="1ba17-229">POCO (read)</span><span class="sxs-lookup"><span data-stu-id="1ba17-229">POCO (read)</span></span>
* <span data-ttu-id="1ba17-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span><span class="sxs-lookup"><span data-stu-id="1ba17-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="1ba17-231">**CloudBlobStream** (write)</span><span class="sxs-lookup"><span data-stu-id="1ba17-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="1ba17-232">**ICloudBlob** (read or write)</span><span class="sxs-lookup"><span data-stu-id="1ba17-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="1ba17-233">**CloudBlockBlob** (read or write)</span><span class="sxs-lookup"><span data-stu-id="1ba17-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="1ba17-234">**CloudPageBlob** (read or write)</span><span class="sxs-lookup"><span data-stu-id="1ba17-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="1ba17-235">How to handle poison messages</span><span class="sxs-lookup"><span data-stu-id="1ba17-235">How to handle poison messages</span></span>
<span data-ttu-id="1ba17-236">Messages whose content causes a function to fail are called *poison messages*.</span><span class="sxs-lookup"><span data-stu-id="1ba17-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="1ba17-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span><span class="sxs-lookup"><span data-stu-id="1ba17-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="1ba17-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span><span class="sxs-lookup"><span data-stu-id="1ba17-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="1ba17-239">Automatic poison message handling</span><span class="sxs-lookup"><span data-stu-id="1ba17-239">Automatic poison message handling</span></span>
<span data-ttu-id="1ba17-240">The SDK will call a function up to 5 times to process a queue message.</span><span class="sxs-lookup"><span data-stu-id="1ba17-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="1ba17-241">If the fifth try fails, the message is moved to a poison queue.</span><span class="sxs-lookup"><span data-stu-id="1ba17-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="1ba17-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="1ba17-243">The poison queue is named *{originalqueuename}*-poison.</span><span class="sxs-lookup"><span data-stu-id="1ba17-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="1ba17-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span><span class="sxs-lookup"><span data-stu-id="1ba17-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="1ba17-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="1ba17-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="1ba17-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span><span class="sxs-lookup"><span data-stu-id="1ba17-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="1ba17-247">The **ProcessPoisonMessage** then logs the poison message.</span><span class="sxs-lookup"><span data-stu-id="1ba17-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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

<span data-ttu-id="1ba17-248">The following illustration shows console output from these functions when a poison message is processed.</span><span class="sxs-lookup"><span data-stu-id="1ba17-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Console output for poison message handling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="1ba17-250">Manual poison message handling</span><span class="sxs-lookup"><span data-stu-id="1ba17-250">Manual poison message handling</span></span>
<span data-ttu-id="1ba17-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span><span class="sxs-lookup"><span data-stu-id="1ba17-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="1ba17-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="1ba17-253">How to set configuration options</span><span class="sxs-lookup"><span data-stu-id="1ba17-253">How to set configuration options</span></span>
<span data-ttu-id="1ba17-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span><span class="sxs-lookup"><span data-stu-id="1ba17-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="1ba17-255">Set the SDK connection strings in code.</span><span class="sxs-lookup"><span data-stu-id="1ba17-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="1ba17-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span><span class="sxs-lookup"><span data-stu-id="1ba17-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="1ba17-257">Get queue names from configuration.</span><span class="sxs-lookup"><span data-stu-id="1ba17-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="1ba17-258">Set SDK connection strings in code</span><span class="sxs-lookup"><span data-stu-id="1ba17-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="1ba17-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="1ba17-260">Configure QueueTrigger  settings</span><span class="sxs-lookup"><span data-stu-id="1ba17-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="1ba17-261">You can configure the following settings that apply to the queue message processing:</span><span class="sxs-lookup"><span data-stu-id="1ba17-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="1ba17-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span><span class="sxs-lookup"><span data-stu-id="1ba17-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="1ba17-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span><span class="sxs-lookup"><span data-stu-id="1ba17-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="1ba17-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span><span class="sxs-lookup"><span data-stu-id="1ba17-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="1ba17-265">The following example shows how to configure these settings:</span><span class="sxs-lookup"><span data-stu-id="1ba17-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="1ba17-266">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="1ba17-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="1ba17-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span><span class="sxs-lookup"><span data-stu-id="1ba17-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="1ba17-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span><span class="sxs-lookup"><span data-stu-id="1ba17-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="1ba17-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span><span class="sxs-lookup"><span data-stu-id="1ba17-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="1ba17-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span><span class="sxs-lookup"><span data-stu-id="1ba17-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="1ba17-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span><span class="sxs-lookup"><span data-stu-id="1ba17-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="1ba17-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span><span class="sxs-lookup"><span data-stu-id="1ba17-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="1ba17-273">If the **appSettings** key is logqueue, your function could look like the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="1ba17-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1ba17-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="1ba17-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="1ba17-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span><span class="sxs-lookup"><span data-stu-id="1ba17-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="1ba17-277">You can't change blob container name while the job is running.</span><span class="sxs-lookup"><span data-stu-id="1ba17-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="1ba17-278">How to trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="1ba17-278">How to trigger a function manually</span></span>
<span data-ttu-id="1ba17-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1ba17-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="1ba17-280">How to write logs</span><span class="sxs-lookup"><span data-stu-id="1ba17-280">How to write logs</span></span>
<span data-ttu-id="1ba17-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span><span class="sxs-lookup"><span data-stu-id="1ba17-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logs in WebJob page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logs in function invocation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="1ba17-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span><span class="sxs-lookup"><span data-stu-id="1ba17-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="1ba17-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span><span class="sxs-lookup"><span data-stu-id="1ba17-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="1ba17-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span><span class="sxs-lookup"><span data-stu-id="1ba17-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="1ba17-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span><span class="sxs-lookup"><span data-stu-id="1ba17-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="1ba17-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span><span class="sxs-lookup"><span data-stu-id="1ba17-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="1ba17-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span><span class="sxs-lookup"><span data-stu-id="1ba17-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="1ba17-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="1ba17-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="1ba17-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span><span class="sxs-lookup"><span data-stu-id="1ba17-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="1ba17-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span><span class="sxs-lookup"><span data-stu-id="1ba17-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="1ba17-293">You can disable logging by setting the Dashboard connection string to null.</span><span class="sxs-lookup"><span data-stu-id="1ba17-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="1ba17-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="1ba17-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="1ba17-295">The following example shows several ways to write logs:</span><span class="sxs-lookup"><span data-stu-id="1ba17-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="1ba17-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span><span class="sxs-lookup"><span data-stu-id="1ba17-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Invocation link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logs in function invocation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="1ba17-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span><span class="sxs-lookup"><span data-stu-id="1ba17-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Toggle output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="1ba17-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span><span class="sxs-lookup"><span data-stu-id="1ba17-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="1ba17-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="1ba17-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="1ba17-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span><span class="sxs-lookup"><span data-stu-id="1ba17-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Info log in table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Error log in table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="1ba17-306">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ba17-306">Next steps</span></span>
<span data-ttu-id="1ba17-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span><span class="sxs-lookup"><span data-stu-id="1ba17-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="1ba17-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="1ba17-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>









