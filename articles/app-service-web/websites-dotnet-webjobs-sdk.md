---
title: What is the Azure WebJobs SDK
description: An introduction to the Azure WebJobs SDK. Explains what the SDK is, typical scenarios it is useful for, and code samples.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670944"
---
# <a name="what-is-the-azure-webjobs-sdk"></a><span data-ttu-id="d1f45-104">What is the Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="d1f45-104">What is the Azure WebJobs SDK</span></span>
## <a id="overview"></a><span data-ttu-id="d1f45-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d1f45-105">Overview</span></span>
<span data-ttu-id="d1f45-106">This article explains what the WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span><span class="sxs-lookup"><span data-stu-id="d1f45-106">This article explains what the WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="d1f45-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="d1f45-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="d1f45-108">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span><span class="sxs-lookup"><span data-stu-id="d1f45-108">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="d1f45-109">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span><span class="sxs-lookup"><span data-stu-id="d1f45-109">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="d1f45-110">In addition, it's designed to be extensible.</span><span class="sxs-lookup"><span data-stu-id="d1f45-110">In addition, it's designed to be extensible.</span></span> <span data-ttu-id="d1f45-111">The [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="d1f45-111">The [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="d1f45-112">The WebJobs SDK includes the following components:</span><span class="sxs-lookup"><span data-stu-id="d1f45-112">The WebJobs SDK includes the following components:</span></span>

* <span data-ttu-id="d1f45-113">**NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="d1f45-113">**NuGet packages**.</span></span> <span data-ttu-id="d1f45-114">NuGet packages that you add to a Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span><span class="sxs-lookup"><span data-stu-id="d1f45-114">NuGet packages that you add to a Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="d1f45-115">**Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d1f45-115">**Dashboard**.</span></span> <span data-ttu-id="d1f45-116">Part of the WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="d1f45-116">Part of the WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use the NuGet packages.</span></span> <span data-ttu-id="d1f45-117">You don't have to write code to use these monitoring and diagnostics features.</span><span class="sxs-lookup"><span data-stu-id="d1f45-117">You don't have to write code to use these monitoring and diagnostics features.</span></span>

## <a id="scenarios"></a><span data-ttu-id="d1f45-118">Scenarios</span><span class="sxs-lookup"><span data-stu-id="d1f45-118">Scenarios</span></span>
<span data-ttu-id="d1f45-119">Here are some typical scenarios you can handle more easily with the Azure WebJobs SDK:</span><span class="sxs-lookup"><span data-stu-id="d1f45-119">Here are some typical scenarios you can handle more easily with the Azure WebJobs SDK:</span></span>

* <span data-ttu-id="d1f45-120">Image processing or other CPU-intensive work.</span><span class="sxs-lookup"><span data-stu-id="d1f45-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="d1f45-121">A common feature of websites is the ability to upload images or videos.</span><span class="sxs-lookup"><span data-stu-id="d1f45-121">A common feature of websites is the ability to upload images or videos.</span></span> <span data-ttu-id="d1f45-122">Often you want to manipulate the content after it's uploaded, but you don't want to make the user wait while you do that.</span><span class="sxs-lookup"><span data-stu-id="d1f45-122">Often you want to manipulate the content after it's uploaded, but you don't want to make the user wait while you do that.</span></span>
* <span data-ttu-id="d1f45-123">Queue processing.</span><span class="sxs-lookup"><span data-stu-id="d1f45-123">Queue processing.</span></span> <span data-ttu-id="d1f45-124">A common way for a web frontend to communicate with a backend service is to use queues.</span><span class="sxs-lookup"><span data-stu-id="d1f45-124">A common way for a web frontend to communicate with a backend service is to use queues.</span></span> <span data-ttu-id="d1f45-125">When the website needs to get work done, it pushes a message onto a queue.</span><span class="sxs-lookup"><span data-stu-id="d1f45-125">When the website needs to get work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="d1f45-126">A backend service pulls messages from the queue and does the work.</span><span class="sxs-lookup"><span data-stu-id="d1f45-126">A backend service pulls messages from the queue and does the work.</span></span> <span data-ttu-id="d1f45-127">You could use queues for image processing: for example, after the user uploads a number of files, put the file names in a queue message to be picked up by the backend for processing.</span><span class="sxs-lookup"><span data-stu-id="d1f45-127">You could use queues for image processing: for example, after the user uploads a number of files, put the file names in a queue message to be picked up by the backend for processing.</span></span> <span data-ttu-id="d1f45-128">Or you could use queues to improve site responsiveness.</span><span class="sxs-lookup"><span data-stu-id="d1f45-128">Or you could use queues to improve site responsiveness.</span></span> <span data-ttu-id="d1f45-129">For example, instead of writing directly to a SQL database, write to a queue, tell the user you're done, and let the backend service handle high-latency relational database work.</span><span class="sxs-lookup"><span data-stu-id="d1f45-129">For example, instead of writing directly to a SQL database, write to a queue, tell the user you're done, and let the backend service handle high-latency relational database work.</span></span> <span data-ttu-id="d1f45-130">For an example of queue processing with image process, see the [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1f45-130">For an example of queue processing with image process, see the [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="d1f45-131">RSS aggregation.</span><span class="sxs-lookup"><span data-stu-id="d1f45-131">RSS aggregation.</span></span> <span data-ttu-id="d1f45-132">If you have a site that maintains a list of RSS feeds, you could pull in all of the articles from the feeds in a background process.</span><span class="sxs-lookup"><span data-stu-id="d1f45-132">If you have a site that maintains a list of RSS feeds, you could pull in all of the articles from the feeds in a background process.</span></span>
* <span data-ttu-id="d1f45-133">File maintenance, such as aggregating or cleaning up log files.</span><span class="sxs-lookup"><span data-stu-id="d1f45-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="d1f45-134">You might have log files being created by several sites or for separate time spans which you want to combine in order to run analysis jobs on them.</span><span class="sxs-lookup"><span data-stu-id="d1f45-134">You might have log files being created by several sites or for separate time spans which you want to combine in order to run analysis jobs on them.</span></span> <span data-ttu-id="d1f45-135">Or you might want to schedule a task to run weekly to clean up old log files.</span><span class="sxs-lookup"><span data-stu-id="d1f45-135">Or you might want to schedule a task to run weekly to clean up old log files.</span></span>
* <span data-ttu-id="d1f45-136">Ingress into Azure Tables.</span><span class="sxs-lookup"><span data-stu-id="d1f45-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="d1f45-137">You might have files stored and blobs and want to parse them and store the data in tables.</span><span class="sxs-lookup"><span data-stu-id="d1f45-137">You might have files stored and blobs and want to parse them and store the data in tables.</span></span> <span data-ttu-id="d1f45-138">The ingress function could be writing lots of rows (millions in some cases), and the WebJobs SDK makes it possible to implement this functionality easily.</span><span class="sxs-lookup"><span data-stu-id="d1f45-138">The ingress function could be writing lots of rows (millions in some cases), and the WebJobs SDK makes it possible to implement this functionality easily.</span></span> <span data-ttu-id="d1f45-139">The SDK also provides real-time monitoring of progress indicators such as the number of rows written in the table.</span><span class="sxs-lookup"><span data-stu-id="d1f45-139">The SDK also provides real-time monitoring of progress indicators such as the number of rows written in the table.</span></span>
* <span data-ttu-id="d1f45-140">Other long-running tasks that you want to run in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span><span class="sxs-lookup"><span data-stu-id="d1f45-140">Other long-running tasks that you want to run in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="d1f45-141">Any tasks that you want to run on a schedule, such as performing a back-up operation every night.</span><span class="sxs-lookup"><span data-stu-id="d1f45-141">Any tasks that you want to run on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="d1f45-142">In many of these scenarios you may want to scale a web app to run on multiple VMs, which would run multiple WebJobs simultaneously.</span><span class="sxs-lookup"><span data-stu-id="d1f45-142">In many of these scenarios you may want to scale a web app to run on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="d1f45-143">In some scenarios this could result in the same data getting processed multiple times, but this is not a problem when you use the built-in queue, blob, and Service Bus triggers of the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="d1f45-143">In some scenarios this could result in the same data getting processed multiple times, but this is not a problem when you use the built-in queue, blob, and Service Bus triggers of the WebJobs SDK.</span></span> <span data-ttu-id="d1f45-144">The SDK ensures that your functions will be processed only once for each message or blob.</span><span class="sxs-lookup"><span data-stu-id="d1f45-144">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="d1f45-145">The WebJobs SDK also makes it easy to handle common error handling scenarios.</span><span class="sxs-lookup"><span data-stu-id="d1f45-145">The WebJobs SDK also makes it easy to handle common error handling scenarios.</span></span> <span data-ttu-id="d1f45-146">You can set up alerts to send notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span><span class="sxs-lookup"><span data-stu-id="d1f45-146">You can set up alerts to send notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <a id="code"></a> <span data-ttu-id="d1f45-147">Code samples</span><span class="sxs-lookup"><span data-stu-id="d1f45-147">Code samples</span></span>
<span data-ttu-id="d1f45-148">The code for handling typical tasks that work with Azure Storage is simple.</span><span class="sxs-lookup"><span data-stu-id="d1f45-148">The code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="d1f45-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates the calls to methods you write.</span><span class="sxs-lookup"><span data-stu-id="d1f45-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates the calls to methods you write.</span></span> <span data-ttu-id="d1f45-150">The WebJobs SDK framework knows when to call your methods and what parameter values to use based on the WebJobs SDK attributes you use in them.</span><span class="sxs-lookup"><span data-stu-id="d1f45-150">The WebJobs SDK framework knows when to call your methods and what parameter values to use based on the WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="d1f45-151">The SDK provides *triggers* that specify what conditions cause the function to be called, and *binders* that specify how to get information into and out of method parameters.</span><span class="sxs-lookup"><span data-stu-id="d1f45-151">The SDK provides *triggers* that specify what conditions cause the function to be called, and *binders* that specify how to get information into and out of method parameters.</span></span>

<span data-ttu-id="d1f45-152">For example, the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function to be called when a message is received on a queue, and if the message format is JSON for a byte array or a custom type, the message is automatically deserialized.</span><span class="sxs-lookup"><span data-stu-id="d1f45-152">For example, the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function to be called when a message is received on a queue, and if the message format is JSON for a byte array or a custom type, the message is automatically deserialized.</span></span> <span data-ttu-id="d1f45-153">The [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="d1f45-153">The [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="d1f45-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span><span class="sxs-lookup"><span data-stu-id="d1f45-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

<span data-ttu-id="d1f45-155">The `JobHost` object is a container for a set of background functions.</span><span class="sxs-lookup"><span data-stu-id="d1f45-155">The `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="d1f45-156">The `JobHost` object monitors the functions, watches for events that trigger them, and executes the functions when trigger events occur.</span><span class="sxs-lookup"><span data-stu-id="d1f45-156">The `JobHost` object monitors the functions, watches for events that trigger them, and executes the functions when trigger events occur.</span></span> <span data-ttu-id="d1f45-157">You call a `JobHost` method to indicate whether you want the container process to run on the current thread or a background thread.</span><span class="sxs-lookup"><span data-stu-id="d1f45-157">You call a `JobHost` method to indicate whether you want the container process to run on the current thread or a background thread.</span></span> <span data-ttu-id="d1f45-158">In the example, the `RunAndBlock` method runs the process continuously on the current thread.</span><span class="sxs-lookup"><span data-stu-id="d1f45-158">In the example, the `RunAndBlock` method runs the process continuously on the current thread.</span></span>

<span data-ttu-id="d1f45-159">Because the `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, the trigger for that function is the reception of a new queue message.</span><span class="sxs-lookup"><span data-stu-id="d1f45-159">Because the `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, the trigger for that function is the reception of a new queue message.</span></span> <span data-ttu-id="d1f45-160">The `JobHost` object watches for new queue messages on the specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="d1f45-160">The `JobHost` object watches for new queue messages on the specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="d1f45-161">The `QueueTrigger` attribute binds the `inputText` parameter to the value of the queue message.</span><span class="sxs-lookup"><span data-stu-id="d1f45-161">The `QueueTrigger` attribute binds the `inputText` parameter to the value of the queue message.</span></span> <span data-ttu-id="d1f45-162">And the `Blob` attribute binds a `TextWriter` object to a blob named "blobname" in a container named "containername".</span><span class="sxs-lookup"><span data-stu-id="d1f45-162">And the `Blob` attribute binds a `TextWriter` object to a blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="d1f45-163">The function then uses these parameters to write the value of the queue message to the blob:</span><span class="sxs-lookup"><span data-stu-id="d1f45-163">The function then uses these parameters to write the value of the queue message to the blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="d1f45-164">The trigger and binder features of the WebJobs SDK greatly simplify the code you have to write.</span><span class="sxs-lookup"><span data-stu-id="d1f45-164">The trigger and binder features of the WebJobs SDK greatly simplify the code you have to write.</span></span> <span data-ttu-id="d1f45-165">The low-level code required to process queues, blobs, or files, or to initiate scheduled tasks, is done for you by the WebJobs SDK framework.</span><span class="sxs-lookup"><span data-stu-id="d1f45-165">The low-level code required to process queues, blobs, or files, or to initiate scheduled tasks, is done for you by the WebJobs SDK framework.</span></span> <span data-ttu-id="d1f45-166">For example, the framework creates queues that don't exist yet, opens the queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes to blobs, and so on.</span><span class="sxs-lookup"><span data-stu-id="d1f45-166">For example, the framework creates queues that don't exist yet, opens the queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes to blobs, and so on.</span></span>

<span data-ttu-id="d1f45-167">The following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span><span class="sxs-lookup"><span data-stu-id="d1f45-167">The following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

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
    }
```

## <a id="schedule"></a> <span data-ttu-id="d1f45-168">Scheduling</span><span class="sxs-lookup"><span data-stu-id="d1f45-168">Scheduling</span></span>
<span data-ttu-id="d1f45-169">The `TimerTrigger` attribute gives you the ability to trigger functions to run on a schedule.</span><span class="sxs-lookup"><span data-stu-id="d1f45-169">The `TimerTrigger` attribute gives you the ability to trigger functions to run on a schedule.</span></span> <span data-ttu-id="d1f45-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using the WebJobs SDK `TimerTrigger`.</span><span class="sxs-lookup"><span data-stu-id="d1f45-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using the WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="d1f45-171">Here's a code sample.</span><span class="sxs-lookup"><span data-stu-id="d1f45-171">Here's a code sample.</span></span>

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

<span data-ttu-id="d1f45-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in the azure-webjobs-sdk-extensions repository on GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="d1f45-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in the azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="d1f45-173">Extensibility</span><span class="sxs-lookup"><span data-stu-id="d1f45-173">Extensibility</span></span>
<span data-ttu-id="d1f45-174">You're not limited to built-in functionality -- the WebJobs SDK allows you to write custom triggers and binders.</span><span class="sxs-lookup"><span data-stu-id="d1f45-174">You're not limited to built-in functionality -- the WebJobs SDK allows you to write custom triggers and binders.</span></span>  <span data-ttu-id="d1f45-175">For example, you can write triggers for cache events and periodic schedules.</span><span class="sxs-lookup"><span data-stu-id="d1f45-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="d1f45-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code to help get you started writing your own triggers and binders.</span><span class="sxs-lookup"><span data-stu-id="d1f45-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code to help get you started writing your own triggers and binders.</span></span>

## <a id="workerrole"></a><span data-ttu-id="d1f45-177">Using the WebJobs SDK outside of WebJobs</span><span class="sxs-lookup"><span data-stu-id="d1f45-177">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="d1f45-178">A program that uses the the WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have to run as a WebJob.</span><span class="sxs-lookup"><span data-stu-id="d1f45-178">A program that uses the the WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have to run as a WebJob.</span></span> <span data-ttu-id="d1f45-179">You can test the program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span><span class="sxs-lookup"><span data-stu-id="d1f45-179">You can test the program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="d1f45-180">However, the dashboard is only available as an extension for an Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="d1f45-180">However, the dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="d1f45-181">If you want to run outside of a WebJob and still use the Dashboard, you can configure a web app to use the same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span><span class="sxs-lookup"><span data-stu-id="d1f45-181">If you want to run outside of a WebJob and still use the Dashboard, you can configure a web app to use the same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="d1f45-182">You can get to the Dashboard by using the URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span><span class="sxs-lookup"><span data-stu-id="d1f45-182">You can get to the Dashboard by using the URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="d1f45-183">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that the blog post shows an old connection string name.</span><span class="sxs-lookup"><span data-stu-id="d1f45-183">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that the blog post shows an old connection string name.</span></span> 

## <a id="nostorage"></a><span data-ttu-id="d1f45-184">Dashboard features</span><span class="sxs-lookup"><span data-stu-id="d1f45-184">Dashboard features</span></span>
<span data-ttu-id="d1f45-185">The WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span><span class="sxs-lookup"><span data-stu-id="d1f45-185">The WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="d1f45-186">You can invoke functions from the Dashboard.</span><span class="sxs-lookup"><span data-stu-id="d1f45-186">You can invoke functions from the Dashboard.</span></span>
* <span data-ttu-id="d1f45-187">You can replay functions from the Dashboard.</span><span class="sxs-lookup"><span data-stu-id="d1f45-187">You can replay functions from the Dashboard.</span></span>
* <span data-ttu-id="d1f45-188">You can view logs in the Dashboard, linked to the particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked to the particular function invocation that generated them (logs written by using a `TextWriter` object that the SDK passes to the function as a parameter).</span><span class="sxs-lookup"><span data-stu-id="d1f45-188">You can view logs in the Dashboard, linked to the particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked to the particular function invocation that generated them (logs written by using a `TextWriter` object that the SDK passes to the function as a parameter).</span></span> 

<span data-ttu-id="d1f45-189">For more information, see [How to manually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span><span class="sxs-lookup"><span data-stu-id="d1f45-189">For more information, see [How to manually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <a id="nextsteps"></a><span data-ttu-id="d1f45-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1f45-190">Next steps</span></span>
<span data-ttu-id="d1f45-191">For more information about the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d1f45-191">For more information about the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="d1f45-192">For information about the latest enhancements to the WebJobs SDK, see the [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span><span class="sxs-lookup"><span data-stu-id="d1f45-192">For information about the latest enhancements to the WebJobs SDK, see the [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

