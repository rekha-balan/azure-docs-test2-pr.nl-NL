---
title: Get started with blob storage and Visual Studio connected services (WebJob projects) | Microsoft Docs
description: How to get started using Blob storage in a WebJob project after connecting to an Azure storage using Visual Studio connected services.
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 7fec890590302a99bbc96f46f24ae440c041580c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563288"
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="6fbf0-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span><span class="sxs-lookup"><span data-stu-id="6fbf0-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6fbf0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6fbf0-104">Overview</span></span>
<span data-ttu-id="6fbf0-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="6fbf0-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="6fbf0-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="6fbf0-108">How to trigger a function when a blob is created or updated</span><span class="sxs-lookup"><span data-stu-id="6fbf0-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="6fbf0-109">This section shows how to use the **BlobTrigger** attribute.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="6fbf0-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="6fbf0-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="6fbf0-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="6fbf0-113">Single placeholder for blob name with extension</span><span class="sxs-lookup"><span data-stu-id="6fbf0-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="6fbf0-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6fbf0-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="6fbf0-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="6fbf0-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6fbf0-118">This code copies only blobs that have names beginning with "original-".</span><span class="sxs-lookup"><span data-stu-id="6fbf0-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="6fbf0-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="6fbf0-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="6fbf0-121">For example, if you want to find blobs in the *images* container that have names like this:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="6fbf0-122">use this for your pattern:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="6fbf0-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="6fbf0-124">Separate blob name and extension placeholders</span><span class="sxs-lookup"><span data-stu-id="6fbf0-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="6fbf0-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="6fbf0-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="6fbf0-127">Types that you can bind to blobs</span><span class="sxs-lookup"><span data-stu-id="6fbf0-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="6fbf0-128">You can use the **BlobTrigger** attribute on the following types:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="6fbf0-129">**string**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-129">**string**</span></span>
* <span data-ttu-id="6fbf0-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-130">**TextReader**</span></span>
* <span data-ttu-id="6fbf0-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-131">**Stream**</span></span>
* <span data-ttu-id="6fbf0-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-132">**ICloudBlob**</span></span>
* <span data-ttu-id="6fbf0-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="6fbf0-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="6fbf0-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="6fbf0-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="6fbf0-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="6fbf0-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="6fbf0-137">Getting text blob content by binding to string</span><span class="sxs-lookup"><span data-stu-id="6fbf0-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="6fbf0-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="6fbf0-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="6fbf0-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="6fbf0-141">Getting serialized blob content by using ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="6fbf0-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="6fbf0-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="6fbf0-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="6fbf0-144">How to handle poison blobs</span><span class="sxs-lookup"><span data-stu-id="6fbf0-144">How to handle poison blobs</span></span>
<span data-ttu-id="6fbf0-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="6fbf0-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="6fbf0-147">By default, the SDK calls a function up to 5 times for a given blob.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="6fbf0-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="6fbf0-149">The maximum number of retries is configurable.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="6fbf0-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="6fbf0-151">The queue message for poison blobs is a JSON object that contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="6fbf0-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="6fbf0-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="6fbf0-153">BlobType ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6fbf0-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6fbf0-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="6fbf0-154">ContainerName</span></span>
* <span data-ttu-id="6fbf0-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="6fbf0-155">BlobName</span></span>
* <span data-ttu-id="6fbf0-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6fbf0-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6fbf0-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="6fbf0-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="6fbf0-159">The SDK automatically deserializes the JSON message.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="6fbf0-160">Here is the **PoisonBlobMessage** class:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="6fbf0-161">Blob polling algorithm</span><span class="sxs-lookup"><span data-stu-id="6fbf0-161">Blob polling algorithm</span></span>
<span data-ttu-id="6fbf0-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="6fbf0-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="6fbf0-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="6fbf0-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="6fbf0-166">There is an exception for blobs that you create by using the **Blob** attribute.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="6fbf0-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="6fbf0-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="6fbf0-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="6fbf0-170">Blob receipts</span><span class="sxs-lookup"><span data-stu-id="6fbf0-170">Blob receipts</span></span>
<span data-ttu-id="6fbf0-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="6fbf0-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="6fbf0-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="6fbf0-174">A blob receipt has the following  information:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="6fbf0-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="6fbf0-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="6fbf0-176">The container name</span><span class="sxs-lookup"><span data-stu-id="6fbf0-176">The container name</span></span>
* <span data-ttu-id="6fbf0-177">The blob type ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6fbf0-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6fbf0-178">The blob name</span><span class="sxs-lookup"><span data-stu-id="6fbf0-178">The blob name</span></span>
* <span data-ttu-id="6fbf0-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6fbf0-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6fbf0-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="6fbf0-181">Related topics covered by the queues article</span><span class="sxs-lookup"><span data-stu-id="6fbf0-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="6fbf0-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6fbf0-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="6fbf0-183">Related topics covered in that article include the following:</span><span class="sxs-lookup"><span data-stu-id="6fbf0-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="6fbf0-184">Async functions</span><span class="sxs-lookup"><span data-stu-id="6fbf0-184">Async functions</span></span>
* <span data-ttu-id="6fbf0-185">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="6fbf0-185">Multiple instances</span></span>
* <span data-ttu-id="6fbf0-186">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="6fbf0-186">Graceful shutdown</span></span>
* <span data-ttu-id="6fbf0-187">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="6fbf0-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="6fbf0-188">Set the SDK connection strings in code.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="6fbf0-189">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="6fbf0-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6fbf0-190">Configure **MaxDequeueCount** for poison blob handling.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="6fbf0-191">Trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="6fbf0-191">Trigger a function manually</span></span>
* <span data-ttu-id="6fbf0-192">Write logs</span><span class="sxs-lookup"><span data-stu-id="6fbf0-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fbf0-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="6fbf0-193">Next steps</span></span>
<span data-ttu-id="6fbf0-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="6fbf0-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="6fbf0-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6fbf0-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

