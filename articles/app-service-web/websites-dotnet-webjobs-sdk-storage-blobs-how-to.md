---
title: How to use Azure blob storage with the WebJobs SDK
description: Learn how to use Azure blob storage with the WebJobs SDK. Trigger a process when a new blob appears in a container and handle 'poison blobs'.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: ''
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671293"
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="335df-104">How to use Azure blob storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="335df-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="335df-105">Overview</span><span class="sxs-lookup"><span data-stu-id="335df-105">Overview</span></span>
<span data-ttu-id="335df-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span><span class="sxs-lookup"><span data-stu-id="335df-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="335df-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="335df-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="335df-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="335df-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="335df-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="335df-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <a id="trigger"></a> <span data-ttu-id="335df-110">How to trigger a function when a blob is created or updated</span><span class="sxs-lookup"><span data-stu-id="335df-110">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="335df-111">This section shows how to use the `BlobTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="335df-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="335df-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span><span class="sxs-lookup"><span data-stu-id="335df-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="335df-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span><span class="sxs-lookup"><span data-stu-id="335df-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="335df-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span><span class="sxs-lookup"><span data-stu-id="335df-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="335df-115">Under some conditions, logs might be missed.</span><span class="sxs-lookup"><span data-stu-id="335df-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="335df-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span><span class="sxs-lookup"><span data-stu-id="335df-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="335df-117">Single placeholder for blob name with extension</span><span class="sxs-lookup"><span data-stu-id="335df-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="335df-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span><span class="sxs-lookup"><span data-stu-id="335df-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="335df-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span><span class="sxs-lookup"><span data-stu-id="335df-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="335df-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span><span class="sxs-lookup"><span data-stu-id="335df-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="335df-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span><span class="sxs-lookup"><span data-stu-id="335df-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="335df-122">This code copies only blobs that have names beginning with "original-".</span><span class="sxs-lookup"><span data-stu-id="335df-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="335df-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span><span class="sxs-lookup"><span data-stu-id="335df-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="335df-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span><span class="sxs-lookup"><span data-stu-id="335df-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="335df-125">For example, if you want to find blobs in the *images* container that have names like this:</span><span class="sxs-lookup"><span data-stu-id="335df-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="335df-126">use this for your pattern:</span><span class="sxs-lookup"><span data-stu-id="335df-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="335df-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="335df-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="335df-128">Separate blob name and extension placeholders</span><span class="sxs-lookup"><span data-stu-id="335df-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="335df-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span><span class="sxs-lookup"><span data-stu-id="335df-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="335df-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span><span class="sxs-lookup"><span data-stu-id="335df-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a id="types"></a> <span data-ttu-id="335df-131">Types that you can bind to blobs</span><span class="sxs-lookup"><span data-stu-id="335df-131">Types that you can bind to blobs</span></span>
<span data-ttu-id="335df-132">You can use the `BlobTrigger` attribute on the following types:</span><span class="sxs-lookup"><span data-stu-id="335df-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="335df-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="335df-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="335df-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span><span class="sxs-lookup"><span data-stu-id="335df-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="335df-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="335df-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <a id="string"></a> <span data-ttu-id="335df-136">Getting text blob content by binding to string</span><span class="sxs-lookup"><span data-stu-id="335df-136">Getting text blob content by binding to string</span></span>
<span data-ttu-id="335df-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span><span class="sxs-lookup"><span data-stu-id="335df-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="335df-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="335df-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="335df-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span><span class="sxs-lookup"><span data-stu-id="335df-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> <span data-ttu-id="335df-140">Getting serialized blob content by using ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="335df-140">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="335df-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span><span class="sxs-lookup"><span data-stu-id="335df-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="335df-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="335df-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="335df-143">Getting the blob path for the triggering blob</span><span class="sxs-lookup"><span data-stu-id="335df-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="335df-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span><span class="sxs-lookup"><span data-stu-id="335df-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a> <span data-ttu-id="335df-145">How to handle poison blobs</span><span class="sxs-lookup"><span data-stu-id="335df-145">How to handle poison blobs</span></span>
<span data-ttu-id="335df-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span><span class="sxs-lookup"><span data-stu-id="335df-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="335df-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span><span class="sxs-lookup"><span data-stu-id="335df-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="335df-148">By default, the SDK calls a function up to 5 times for a given blob.</span><span class="sxs-lookup"><span data-stu-id="335df-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="335df-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="335df-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="335df-150">The maximum number of retries is configurable.</span><span class="sxs-lookup"><span data-stu-id="335df-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="335df-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span><span class="sxs-lookup"><span data-stu-id="335df-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="335df-152">The queue message for poison blobs is a JSON object that contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="335df-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="335df-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="335df-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="335df-154">BlobType ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="335df-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="335df-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="335df-155">ContainerName</span></span>
* <span data-ttu-id="335df-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="335df-156">BlobName</span></span>
* <span data-ttu-id="335df-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="335df-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="335df-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span><span class="sxs-lookup"><span data-stu-id="335df-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="335df-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span><span class="sxs-lookup"><span data-stu-id="335df-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="335df-160">The SDK automatically deserializes the JSON message.</span><span class="sxs-lookup"><span data-stu-id="335df-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="335df-161">Here is the `PoisonBlobMessage` class:</span><span class="sxs-lookup"><span data-stu-id="335df-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> <span data-ttu-id="335df-162">Blob polling algorithm</span><span class="sxs-lookup"><span data-stu-id="335df-162">Blob polling algorithm</span></span>
<span data-ttu-id="335df-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span><span class="sxs-lookup"><span data-stu-id="335df-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="335df-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span><span class="sxs-lookup"><span data-stu-id="335df-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="335df-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span><span class="sxs-lookup"><span data-stu-id="335df-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="335df-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span><span class="sxs-lookup"><span data-stu-id="335df-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="335df-167">There is an exception for blobs that you create by using the `Blob` attribute.</span><span class="sxs-lookup"><span data-stu-id="335df-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="335df-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span><span class="sxs-lookup"><span data-stu-id="335df-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="335df-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span><span class="sxs-lookup"><span data-stu-id="335df-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="335df-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="335df-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <a id="receipts"></a> <span data-ttu-id="335df-171">Blob receipts</span><span class="sxs-lookup"><span data-stu-id="335df-171">Blob receipts</span></span>
<span data-ttu-id="335df-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span><span class="sxs-lookup"><span data-stu-id="335df-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="335df-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span><span class="sxs-lookup"><span data-stu-id="335df-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="335df-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span><span class="sxs-lookup"><span data-stu-id="335df-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="335df-175">A blob receipt has the following  information:</span><span class="sxs-lookup"><span data-stu-id="335df-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="335df-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="335df-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="335df-177">The container name</span><span class="sxs-lookup"><span data-stu-id="335df-177">The container name</span></span>
* <span data-ttu-id="335df-178">The blob type ("BlockBlob" or "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="335df-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="335df-179">The blob name</span><span class="sxs-lookup"><span data-stu-id="335df-179">The blob name</span></span>
* <span data-ttu-id="335df-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="335df-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="335df-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span><span class="sxs-lookup"><span data-stu-id="335df-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a id="queues"></a><span data-ttu-id="335df-182">Related topics covered by the queues article</span><span class="sxs-lookup"><span data-stu-id="335df-182">Related topics covered by the queues article</span></span>
<span data-ttu-id="335df-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="335df-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="335df-184">Related topics covered in that article include the following:</span><span class="sxs-lookup"><span data-stu-id="335df-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="335df-185">Async functions</span><span class="sxs-lookup"><span data-stu-id="335df-185">Async functions</span></span>
* <span data-ttu-id="335df-186">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="335df-186">Multiple instances</span></span>
* <span data-ttu-id="335df-187">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="335df-187">Graceful shutdown</span></span>
* <span data-ttu-id="335df-188">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="335df-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="335df-189">Set the SDK connection strings in code.</span><span class="sxs-lookup"><span data-stu-id="335df-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="335df-190">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="335df-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="335df-191">Configure `MaxDequeueCount` for poison blob handling.</span><span class="sxs-lookup"><span data-stu-id="335df-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="335df-192">Trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="335df-192">Trigger a function manually</span></span>
* <span data-ttu-id="335df-193">Write logs</span><span class="sxs-lookup"><span data-stu-id="335df-193">Write logs</span></span>

## <a id="nextsteps"></a> <span data-ttu-id="335df-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="335df-194">Next steps</span></span>
<span data-ttu-id="335df-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="335df-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="335df-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="335df-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

