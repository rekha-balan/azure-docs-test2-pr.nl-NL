---
title: Get started with the Azure WebJobs SDK
description: Introduction to the WebJobs SDK for event-driven background processing. Learn how to access data in Azure services and third-party services.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: cfowler
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/27/2018
ms.author: glenga
ms.openlocfilehash: 72f7090c285e629149519920ac82f0fe962abc48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865339"
---
# <a name="get-started-with-the-azure-webjobs-sdk-for-event-driven-background-processing"></a><span data-ttu-id="45a50-104">Get started with the Azure WebJobs SDK for event-driven background processing</span><span class="sxs-lookup"><span data-stu-id="45a50-104">Get started with the Azure WebJobs SDK for event-driven background processing</span></span>

<span data-ttu-id="45a50-105">This article shows how to create an Azure WebJobs SDK project, run it locally, and deploy it to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="45a50-105">This article shows how to create an Azure WebJobs SDK project, run it locally, and deploy it to Azure App Service.</span></span>

<span data-ttu-id="45a50-106">The instructions are for [Visual Studio 2017](https://www.visualstudio.com/vs/), but the same tasks can be accomplished with other tools, such as [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="45a50-106">The instructions are for [Visual Studio 2017](https://www.visualstudio.com/vs/), but the same tasks can be accomplished with other tools, such as [Visual Studio Code](https://code.visualstudio.com/).</span></span>

## <a name="what-is-the-azure-webjobs-sdk"></a><span data-ttu-id="45a50-107">What is the Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="45a50-107">What is the Azure WebJobs SDK</span></span>

<span data-ttu-id="45a50-108">The Azure WebJobs SDK is a framework that simplifies the task of writing background processing code that accesses data in Azure services.</span><span class="sxs-lookup"><span data-stu-id="45a50-108">The Azure WebJobs SDK is a framework that simplifies the task of writing background processing code that accesses data in Azure services.</span></span> <span data-ttu-id="45a50-109">The SDK features a declarative syntax for specifying events that should trigger a function, such as a new message added to a queue.</span><span class="sxs-lookup"><span data-stu-id="45a50-109">The SDK features a declarative syntax for specifying events that should trigger a function, such as a new message added to a queue.</span></span> <span data-ttu-id="45a50-110">Similar declarative syntax controls reading and writing data once a function has been triggered.</span><span class="sxs-lookup"><span data-stu-id="45a50-110">Similar declarative syntax controls reading and writing data once a function has been triggered.</span></span> <span data-ttu-id="45a50-111">This system of triggers and bindings takes care of most of the low-level coding tasks associated with accessing Azure and third-party services.</span><span class="sxs-lookup"><span data-stu-id="45a50-111">This system of triggers and bindings takes care of most of the low-level coding tasks associated with accessing Azure and third-party services.</span></span>

### <a name="functions-triggers-and-bindings"></a><span data-ttu-id="45a50-112">Functions, triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="45a50-112">Functions, triggers and bindings</span></span>

<span data-ttu-id="45a50-113">A WebJobs SDK project defines one or more *functions*.</span><span class="sxs-lookup"><span data-stu-id="45a50-113">A WebJobs SDK project defines one or more *functions*.</span></span> <span data-ttu-id="45a50-114">A function is a method that has a trigger attribute in its method signature.</span><span class="sxs-lookup"><span data-stu-id="45a50-114">A function is a method that has a trigger attribute in its method signature.</span></span> <span data-ttu-id="45a50-115">Triggers specify conditions for calling a function, and bindings specify what to read and write.</span><span class="sxs-lookup"><span data-stu-id="45a50-115">Triggers specify conditions for calling a function, and bindings specify what to read and write.</span></span> <span data-ttu-id="45a50-116">For example, the trigger attribute in the following function tells the runtime to call the function whenever a queue message appears in the `items` queue.</span><span class="sxs-lookup"><span data-stu-id="45a50-116">For example, the trigger attribute in the following function tells the runtime to call the function whenever a queue message appears in the `items` queue.</span></span> <span data-ttu-id="45a50-117">The `Blob` attribute tells the runtime to use the queue message to read a blob in the *workitems* container.</span><span class="sxs-lookup"><span data-stu-id="45a50-117">The `Blob` attribute tells the runtime to use the queue message to read a blob in the *workitems* container.</span></span> <span data-ttu-id="45a50-118">The content of the queue message &mdash; provided in the `queueTrigger` parameter &mdash; is the name of the blob.</span><span class="sxs-lookup"><span data-stu-id="45a50-118">The content of the queue message &mdash; provided in the `queueTrigger` parameter &mdash; is the name of the blob.</span></span>

```cs
public static void Run(
    [QueueTrigger("items")] string myQueueItem,
    [Blob("workitems/{queueTrigger}", FileAccess.Read)] Stream myBlob,
    TraceWriter log)
{
    log.Info($"BlobInput processed blob\n Name:{myQueueItem} \n Size: {myBlob.Length} bytes");
}
```

### <a name="versions-2x-and-3x"></a><span data-ttu-id="45a50-119">Versions 2.x and 3.x</span><span class="sxs-lookup"><span data-stu-id="45a50-119">Versions 2.x and 3.x</span></span>

<span data-ttu-id="45a50-120">The instructions tell how to create a WebJobs SDK version 2.x project.</span><span class="sxs-lookup"><span data-stu-id="45a50-120">The instructions tell how to create a WebJobs SDK version 2.x project.</span></span> <span data-ttu-id="45a50-121">The latest version of the WebJobs SDK is 3.x, but it is currently in preview and this article doesn't have instructions for that version yet.</span><span class="sxs-lookup"><span data-stu-id="45a50-121">The latest version of the WebJobs SDK is 3.x, but it is currently in preview and this article doesn't have instructions for that version yet.</span></span> <span data-ttu-id="45a50-122">The main change introduced by version 3.x is the use of .NET Core instead of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="45a50-122">The main change introduced by version 3.x is the use of .NET Core instead of .NET Framework.</span></span>

### <a name="azure-functions"></a><span data-ttu-id="45a50-123">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="45a50-123">Azure Functions</span></span>

<span data-ttu-id="45a50-124">[Azure Functions](../azure-functions/functions-overview.md) is based on the WebJobs SDK and is an option when you don't need to use the WebJobs SDK directly.</span><span class="sxs-lookup"><span data-stu-id="45a50-124">[Azure Functions](../azure-functions/functions-overview.md) is based on the WebJobs SDK and is an option when you don't need to use the WebJobs SDK directly.</span></span> <span data-ttu-id="45a50-125">Azure Functions 1.x uses the WebJobs SDK 2.x.</span><span class="sxs-lookup"><span data-stu-id="45a50-125">Azure Functions 1.x uses the WebJobs SDK 2.x.</span></span> <span data-ttu-id="45a50-126">For more information, see [comparison between Azure Functions and the WebJobs SDK](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md#compare-functions-and-webjobs).</span><span class="sxs-lookup"><span data-stu-id="45a50-126">For more information, see [comparison between Azure Functions and the WebJobs SDK](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md#compare-functions-and-webjobs).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45a50-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="45a50-127">Prerequisites</span></span>

<span data-ttu-id="45a50-128">This article assumes you have [an Azure account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) and experience with [apps in Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-128">This article assumes you have [an Azure account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) and experience with [apps in Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="45a50-129">To complete the steps in this article:</span><span class="sxs-lookup"><span data-stu-id="45a50-129">To complete the steps in this article:</span></span>

* <span data-ttu-id="45a50-130">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/) with the **Azure development** workload.</span><span class="sxs-lookup"><span data-stu-id="45a50-130">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/) with the **Azure development** workload.</span></span> <span data-ttu-id="45a50-131">If you already have Visual Studio but don't have that workload, add the workload by selecting **Tools > Get Tools and Features**.</span><span class="sxs-lookup"><span data-stu-id="45a50-131">If you already have Visual Studio but don't have that workload, add the workload by selecting **Tools > Get Tools and Features**.</span></span>
* <span data-ttu-id="45a50-132">[Create an App Service app](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-132">[Create an App Service app](app-service-web-get-started-dotnet-framework.md).</span></span> <span data-ttu-id="45a50-133">If you already have one that you can deploy a WebJob to, you can use that instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="45a50-133">If you already have one that you can deploy a WebJob to, you can use that instead of creating a new one.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="45a50-134">Create a project</span><span class="sxs-lookup"><span data-stu-id="45a50-134">Create a project</span></span>

1. <span data-ttu-id="45a50-135">In Visual Studio, select **File > New project**.</span><span class="sxs-lookup"><span data-stu-id="45a50-135">In Visual Studio, select **File > New project**.</span></span>

1. <span data-ttu-id="45a50-136">Select **Windows Classic Desktop > Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="45a50-136">Select **Windows Classic Desktop > Console App (.NET Framework)**.</span></span>

1. <span data-ttu-id="45a50-137">Name the project *WebJobsSDKSample*, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-137">Name the project *WebJobsSDKSample*, and then select **OK**.</span></span>

   ![New Project dialog](./media/webjobs-sdk-get-started/new-project.png)

## <a name="add-webjobs-nuget-package"></a><span data-ttu-id="45a50-139">Add WebJobs NuGet package</span><span class="sxs-lookup"><span data-stu-id="45a50-139">Add WebJobs NuGet package</span></span>

1. <span data-ttu-id="45a50-140">Install the latest stable 2.x version of the NuGet package `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="45a50-140">Install the latest stable 2.x version of the NuGet package `Microsoft.Azure.WebJobs`.</span></span>
 
   <span data-ttu-id="45a50-141">Here's the **Package Manager Console** command for version 2.2.0:</span><span class="sxs-lookup"><span data-stu-id="45a50-141">Here's the **Package Manager Console** command for version 2.2.0:</span></span>

   ```powershell
   Install-Package Microsoft.Azure.WebJobs -version 2.2.0
   ``` 

## <a name="create-the-jobhost"></a><span data-ttu-id="45a50-142">Create the JobHost</span><span class="sxs-lookup"><span data-stu-id="45a50-142">Create the JobHost</span></span>

<span data-ttu-id="45a50-143">The `JobHost` object is the runtime container for functions: it listens for triggers and calls functions.</span><span class="sxs-lookup"><span data-stu-id="45a50-143">The `JobHost` object is the runtime container for functions: it listens for triggers and calls functions.</span></span> 

1. <span data-ttu-id="45a50-144">In *Program.cs*, add a `using` statement:</span><span class="sxs-lookup"><span data-stu-id="45a50-144">In *Program.cs*, add a `using` statement:</span></span>

   ```cs
   using Microsoft.Azure.WebJobs;
   ```

1. <span data-ttu-id="45a50-145">Replace the `Main` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="45a50-145">Replace the `Main` method with the following code:</span></span>

   ```cs
   static void Main()
   {
       var config = new JobHostConfiguration();
       var host = new JobHost(config);
       host.RunAndBlock();
   }
   ```

## <a name="enable-console-logging"></a><span data-ttu-id="45a50-146">Enable console logging</span><span class="sxs-lookup"><span data-stu-id="45a50-146">Enable console logging</span></span>

<span data-ttu-id="45a50-147">There are several options for logging in WebJobs SDK project.</span><span class="sxs-lookup"><span data-stu-id="45a50-147">There are several options for logging in WebJobs SDK project.</span></span> <span data-ttu-id="45a50-148">The one we recommend is the [logging framework that was developed for ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="45a50-148">The one we recommend is the [logging framework that was developed for ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging).</span></span> <span data-ttu-id="45a50-149">This framework offers better performance and more flexibility in storage media and filtering.</span><span class="sxs-lookup"><span data-stu-id="45a50-149">This framework offers better performance and more flexibility in storage media and filtering.</span></span> 

<span data-ttu-id="45a50-150">In this section, you set up console logging that uses the new framework.</span><span class="sxs-lookup"><span data-stu-id="45a50-150">In this section, you set up console logging that uses the new framework.</span></span>

1. <span data-ttu-id="45a50-151">Install the latest stable version of the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="45a50-151">Install the latest stable version of the following NuGet packages:</span></span>

   * <span data-ttu-id="45a50-152">`Microsoft.Extensions.Logging` - The logging framework.</span><span class="sxs-lookup"><span data-stu-id="45a50-152">`Microsoft.Extensions.Logging` - The logging framework.</span></span>
   * <span data-ttu-id="45a50-153">`Microsoft.Extensions.Logging.Console` - The console *provider*.</span><span class="sxs-lookup"><span data-stu-id="45a50-153">`Microsoft.Extensions.Logging.Console` - The console *provider*.</span></span> <span data-ttu-id="45a50-154">A provider sends logs to a particular destination, in this case to the console.</span><span class="sxs-lookup"><span data-stu-id="45a50-154">A provider sends logs to a particular destination, in this case to the console.</span></span> 
 
   <span data-ttu-id="45a50-155">Here are the **Package Manager Console** commands for version 2.0.1:</span><span class="sxs-lookup"><span data-stu-id="45a50-155">Here are the **Package Manager Console** commands for version 2.0.1:</span></span>

   ```powershell
   Install-Package Microsoft.Extensions.Logging -version 2.0.1
   ``` 

   ```powershell
   Install-Package Microsoft.Extensions.Logging.Console -version 2.0.1
   ``` 

1. <span data-ttu-id="45a50-156">In *Program.cs*, add a `using` statement:</span><span class="sxs-lookup"><span data-stu-id="45a50-156">In *Program.cs*, add a `using` statement:</span></span>

   ```cs
   using Microsoft.Extensions.Logging;
   ```

1. <span data-ttu-id="45a50-157">In the `Main` method, add code to update the `JobHostConfiguration` before creating the `JobHost`:</span><span class="sxs-lookup"><span data-stu-id="45a50-157">In the `Main` method, add code to update the `JobHostConfiguration` before creating the `JobHost`:</span></span>
 
   ```
   config.DashboardConnectionString = "";
   var loggerFactory = new LoggerFactory();
   config.LoggerFactory = loggerFactory
       .AddConsole();
   ```

   <span data-ttu-id="45a50-158">This code makes the following changes:</span><span class="sxs-lookup"><span data-stu-id="45a50-158">This code makes the following changes:</span></span>

   * <span data-ttu-id="45a50-159">Disables [dashboard logging](https://github.com/Azure/azure-webjobs-sdk/wiki/Queues#logs).</span><span class="sxs-lookup"><span data-stu-id="45a50-159">Disables [dashboard logging](https://github.com/Azure/azure-webjobs-sdk/wiki/Queues#logs).</span></span> <span data-ttu-id="45a50-160">The dashboard is a legacy monitoring tool, and dashboard logging is not recommended for high-throughput production scenarios.</span><span class="sxs-lookup"><span data-stu-id="45a50-160">The dashboard is a legacy monitoring tool, and dashboard logging is not recommended for high-throughput production scenarios.</span></span>
   * <span data-ttu-id="45a50-161">Adds the console provider with default [filtering](webjobs-sdk-how-to.md#log-filtering).</span><span class="sxs-lookup"><span data-stu-id="45a50-161">Adds the console provider with default [filtering](webjobs-sdk-how-to.md#log-filtering).</span></span> 

   <span data-ttu-id="45a50-162">The `Main` method now looks like this:</span><span class="sxs-lookup"><span data-stu-id="45a50-162">The `Main` method now looks like this:</span></span>

   ```
   var config = new JobHostConfiguration();
   config.DashboardConnectionString = "";
   var loggerFactory = new LoggerFactory();
   config.LoggerFactory = loggerFactory
       .AddConsole();
   var host = new JobHost(config);
   host.RunAndBlock();
   ```
   
## <a name="create-a-function"></a><span data-ttu-id="45a50-163">Create a function</span><span class="sxs-lookup"><span data-stu-id="45a50-163">Create a function</span></span>

1. <span data-ttu-id="45a50-164">Create *Functions.cs* in the project folder, and replace the template code with this code:</span><span class="sxs-lookup"><span data-stu-id="45a50-164">Create *Functions.cs* in the project folder, and replace the template code with this code:</span></span>

   ```cs
   using Microsoft.Azure.WebJobs;
   using Microsoft.Azure.WebJobs.Host;
   using Microsoft.Extensions.Logging;

   namespace WebJobsSDKSample
   {
       public class Functions
       {
           public static void ProcessQueueMessage([QueueTrigger("queue")] string message, ILogger logger)
           {
               logger.LogInformation(message);
           }
       }
   }
   ```

   <span data-ttu-id="45a50-165">The `QueueTrigger` attribute tells the runtime to call this function when a new message is written on an Azure Storage queue called `queue`.</span><span class="sxs-lookup"><span data-stu-id="45a50-165">The `QueueTrigger` attribute tells the runtime to call this function when a new message is written on an Azure Storage queue called `queue`.</span></span> <span data-ttu-id="45a50-166">The contents of the queue message are provided to the method code in the `message` parameter.</span><span class="sxs-lookup"><span data-stu-id="45a50-166">The contents of the queue message are provided to the method code in the `message` parameter.</span></span> <span data-ttu-id="45a50-167">The body of the method is where you process the trigger data.</span><span class="sxs-lookup"><span data-stu-id="45a50-167">The body of the method is where you process the trigger data.</span></span> <span data-ttu-id="45a50-168">In this example, the code just logs the message.</span><span class="sxs-lookup"><span data-stu-id="45a50-168">In this example, the code just logs the message.</span></span>

   <span data-ttu-id="45a50-169">The `message` parameter doesn't have to be a string.</span><span class="sxs-lookup"><span data-stu-id="45a50-169">The `message` parameter doesn't have to be a string.</span></span> <span data-ttu-id="45a50-170">You can also bind to a JSON object, a byte array, or a [CloudQueueMessage](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage) object.</span><span class="sxs-lookup"><span data-stu-id="45a50-170">You can also bind to a JSON object, a byte array, or a [CloudQueueMessage](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage) object.</span></span> <span data-ttu-id="45a50-171">[See Queue trigger usage](../azure-functions/functions-bindings-storage-queue.md#trigger---usage).</span><span class="sxs-lookup"><span data-stu-id="45a50-171">[See Queue trigger usage](../azure-functions/functions-bindings-storage-queue.md#trigger---usage).</span></span> <span data-ttu-id="45a50-172">Each binding type (such as queues, blobs, or tables) has a different set of parameter types that you can bind to.</span><span class="sxs-lookup"><span data-stu-id="45a50-172">Each binding type (such as queues, blobs, or tables) has a different set of parameter types that you can bind to.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="45a50-173">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="45a50-173">Create a storage account</span></span>

<span data-ttu-id="45a50-174">The Azure Storage emulator that runs locally doesn't have all of the features that the WebJobs SDK needs.</span><span class="sxs-lookup"><span data-stu-id="45a50-174">The Azure Storage emulator that runs locally doesn't have all of the features that the WebJobs SDK needs.</span></span> <span data-ttu-id="45a50-175">So in this section you create a Storage account in Azure and configure the project to use it.</span><span class="sxs-lookup"><span data-stu-id="45a50-175">So in this section you create a Storage account in Azure and configure the project to use it.</span></span>

1. <span data-ttu-id="45a50-176">Open **Server Explorer** and sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="45a50-176">Open **Server Explorer** and sign in to Azure.</span></span> <span data-ttu-id="45a50-177">Right-click the **Azure** node, and then select **Connect to Microsoft Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="45a50-177">Right-click the **Azure** node, and then select **Connect to Microsoft Azure Subscription**.</span></span>

   ![Sign in to Azure](./media/webjobs-sdk-get-started/sign-in.png)

1. <span data-ttu-id="45a50-179">Under the **Azure** node in **Server Explorer**, right-click **Storage**, and then select **Create Storage account**.</span><span class="sxs-lookup"><span data-stu-id="45a50-179">Under the **Azure** node in **Server Explorer**, right-click **Storage**, and then select **Create Storage account**.</span></span>

   ![Create Storage account menu](./media/webjobs-sdk-get-started/create-storage-account-menu.png)

1. <span data-ttu-id="45a50-181">In the **Create Storage Account** dialog box, enter a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="45a50-181">In the **Create Storage Account** dialog box, enter a unique name for the storage account.</span></span>

1. <span data-ttu-id="45a50-182">Choose the same **Region** that you created your App Service app in, or a region close to you.</span><span class="sxs-lookup"><span data-stu-id="45a50-182">Choose the same **Region** that you created your App Service app in, or a region close to you.</span></span>

1. <span data-ttu-id="45a50-183">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="45a50-183">Select **Create**.</span></span>

   ![Create Storage account](./media/webjobs-sdk-get-started/create-storage-account.png)

1. <span data-ttu-id="45a50-185">Under the **Storage** node in **Server Explorer**, select the new Storage account.</span><span class="sxs-lookup"><span data-stu-id="45a50-185">Under the **Storage** node in **Server Explorer**, select the new Storage account.</span></span> <span data-ttu-id="45a50-186">In the **Properties** window, select the ellipsis (**...**) at the right of the **Connection String** value field.</span><span class="sxs-lookup"><span data-stu-id="45a50-186">In the **Properties** window, select the ellipsis (**...**) at the right of the **Connection String** value field.</span></span>

   ![Connection String ellipsis](./media/webjobs-sdk-get-started/conn-string-ellipsis.png)

1. <span data-ttu-id="45a50-188">Copy the connection string, and save this value somewhere that you can copy it again readily.</span><span class="sxs-lookup"><span data-stu-id="45a50-188">Copy the connection string, and save this value somewhere that you can copy it again readily.</span></span>

   ![Copy connection string](./media/webjobs-sdk-get-started/copy-key.png)

## <a name="configure-storage-for-running-locally"></a><span data-ttu-id="45a50-190">Configure storage for running locally</span><span class="sxs-lookup"><span data-stu-id="45a50-190">Configure storage for running locally</span></span>

<span data-ttu-id="45a50-191">The WebJobs SDK looks for the Storage connection string in the App Settings collection.</span><span class="sxs-lookup"><span data-stu-id="45a50-191">The WebJobs SDK looks for the Storage connection string in the App Settings collection.</span></span> <span data-ttu-id="45a50-192">When you run locally, it looks for this value in the *App.config* file or environment variables.</span><span class="sxs-lookup"><span data-stu-id="45a50-192">When you run locally, it looks for this value in the *App.config* file or environment variables.</span></span>

1. <span data-ttu-id="45a50-193">Add the following XML to the *App.config* file, immediately after the opening  `<configuration>` tag.</span><span class="sxs-lookup"><span data-stu-id="45a50-193">Add the following XML to the *App.config* file, immediately after the opening  `<configuration>` tag.</span></span>

   ```xml
   <connectionStrings>
     <add name="AzureWebJobsStorage" connectionString="{storage connection string}" />
   </connectionStrings>
   ```

1. <span data-ttu-id="45a50-194">Replace *{storage connection string}* with the connection string that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="45a50-194">Replace *{storage connection string}* with the connection string that you copied earlier.</span></span>

   <span data-ttu-id="45a50-195">Later you'll use the connection string again, when you configure the App Service app in Azure.</span><span class="sxs-lookup"><span data-stu-id="45a50-195">Later you'll use the connection string again, when you configure the App Service app in Azure.</span></span>

## <a name="test-locally"></a><span data-ttu-id="45a50-196">Test locally</span><span class="sxs-lookup"><span data-stu-id="45a50-196">Test locally</span></span>

<span data-ttu-id="45a50-197">In this section, you build and run the project locally and trigger the function by creating a queue message.</span><span class="sxs-lookup"><span data-stu-id="45a50-197">In this section, you build and run the project locally and trigger the function by creating a queue message.</span></span>

1. <span data-ttu-id="45a50-198">Press Ctrl+F5 to run the project.</span><span class="sxs-lookup"><span data-stu-id="45a50-198">Press Ctrl+F5 to run the project.</span></span>

   <span data-ttu-id="45a50-199">The console shows that the runtime found your function and is waiting for queue messages to trigger it.</span><span class="sxs-lookup"><span data-stu-id="45a50-199">The console shows that the runtime found your function and is waiting for queue messages to trigger it.</span></span>

   ```console
   Found the following functions:
   WebJobsSDKSample.Functions.ProcessQueueMessage
   info: Host.Startup[0]
         Found the following functions:
         WebJobsSDKSample.Functions.ProcessQueueMessage
   Job host started
   info: Host.Startup[0]
         Job host started
   ```

   <span data-ttu-id="45a50-200">You may see a warning message about a `ServicePointManager` setting.</span><span class="sxs-lookup"><span data-stu-id="45a50-200">You may see a warning message about a `ServicePointManager` setting.</span></span> <span data-ttu-id="45a50-201">For the testing you'll be doing with this project, you can ignore the warning.</span><span class="sxs-lookup"><span data-stu-id="45a50-201">For the testing you'll be doing with this project, you can ignore the warning.</span></span> <span data-ttu-id="45a50-202">For more information about the warning, see [How to use the WebJobs SDK](webjobs-sdk-how-to.md#jobhost-servicepointmanager-settings).</span><span class="sxs-lookup"><span data-stu-id="45a50-202">For more information about the warning, see [How to use the WebJobs SDK](webjobs-sdk-how-to.md#jobhost-servicepointmanager-settings).</span></span>

1. <span data-ttu-id="45a50-203">Close the console window.</span><span class="sxs-lookup"><span data-stu-id="45a50-203">Close the console window.</span></span>

1. <span data-ttu-id="45a50-204">In **Server Explorer**, expand the node for your new storage account, and then right-click **Queues**.</span><span class="sxs-lookup"><span data-stu-id="45a50-204">In **Server Explorer**, expand the node for your new storage account, and then right-click **Queues**.</span></span> 

1. <span data-ttu-id="45a50-205">Select **Create Queue**.</span><span class="sxs-lookup"><span data-stu-id="45a50-205">Select **Create Queue**.</span></span> 

1. <span data-ttu-id="45a50-206">Enter *queue* as the name for the queue, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-206">Enter *queue* as the name for the queue, and then select **OK**.</span></span>

   ![Create queue](./media/webjobs-sdk-get-started/create-queue.png)

1. <span data-ttu-id="45a50-208">Right-click the node for the new queue, and then select **View Queue**.</span><span class="sxs-lookup"><span data-stu-id="45a50-208">Right-click the node for the new queue, and then select **View Queue**.</span></span>

1. <span data-ttu-id="45a50-209">Select the **Add Message** icon.</span><span class="sxs-lookup"><span data-stu-id="45a50-209">Select the **Add Message** icon.</span></span>

   ![Create queue](./media/webjobs-sdk-get-started/create-queue-message.png)

1. <span data-ttu-id="45a50-211">In the **Add Message** dialog, enter *Hello World!*</span><span class="sxs-lookup"><span data-stu-id="45a50-211">In the **Add Message** dialog, enter *Hello World!*</span></span> <span data-ttu-id="45a50-212">as the **Message text**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-212">as the **Message text**, and then select **OK**.</span></span>

   ![Create queue](./media/webjobs-sdk-get-started/hello-world-text.png)

1. <span data-ttu-id="45a50-214">Run the project again.</span><span class="sxs-lookup"><span data-stu-id="45a50-214">Run the project again.</span></span>

   <span data-ttu-id="45a50-215">Because you used the `QueueTrigger` attribute in the `ProcessQueueMessage` function, the WeJobs SDK runtime listens for queue messages when it starts up.</span><span class="sxs-lookup"><span data-stu-id="45a50-215">Because you used the `QueueTrigger` attribute in the `ProcessQueueMessage` function, the WeJobs SDK runtime listens for queue messages when it starts up.</span></span> <span data-ttu-id="45a50-216">It finds a new queue message in the queue named *queue* and calls the function.</span><span class="sxs-lookup"><span data-stu-id="45a50-216">It finds a new queue message in the queue named *queue* and calls the function.</span></span>

   <span data-ttu-id="45a50-217">Due to [queue polling exponential backoff](../azure-functions/functions-bindings-storage-queue.md#trigger---polling-algorithm), it might take as long as 2 minutes for the runtime to find the message and invoke the function.</span><span class="sxs-lookup"><span data-stu-id="45a50-217">Due to [queue polling exponential backoff](../azure-functions/functions-bindings-storage-queue.md#trigger---polling-algorithm), it might take as long as 2 minutes for the runtime to find the message and invoke the function.</span></span> <span data-ttu-id="45a50-218">This wait time can be reduced by running in [development mode](webjobs-sdk-how-to.md#jobhost-development-settings).</span><span class="sxs-lookup"><span data-stu-id="45a50-218">This wait time can be reduced by running in [development mode](webjobs-sdk-how-to.md#jobhost-development-settings).</span></span>

  <span data-ttu-id="45a50-219">The console output looks like this:</span><span class="sxs-lookup"><span data-stu-id="45a50-219">The console output looks like this:</span></span>

   ```console
   Found the following functions:
   WebJobsSDKSample.Functions.ProcessQueueMessage
   info: Host.Startup[0]
         Found the following functions:
         WebJobsSDKSample.Functions.ProcessQueueMessage
   Job host started
   info: Host.Startup[0]
         Job host started
   Executing 'Functions.ProcessQueueMessage' (Reason='New queue message detected on 'queue'.', Id=ebcb275d-0d7c-4293-a1af-93e0804b9e49)
   info: Function[0]
         Hello World!
   info: Host.Results[0]
         Executed 'Functions.ProcessQueueMessage' (Succeeded, Id=ebcb275d-0d7c-4293-a1af-93e0804b9e49)
   Executed 'Functions.ProcessQueueMessage' (Succeeded, Id=ebcb275d-0d7c-4293-a1af-93e0804b9e49)
   ```

1. <span data-ttu-id="45a50-220">Close the console window.</span><span class="sxs-lookup"><span data-stu-id="45a50-220">Close the console window.</span></span>

## <a name="add-application-insights-logging"></a><span data-ttu-id="45a50-221">Add Application Insights logging</span><span class="sxs-lookup"><span data-stu-id="45a50-221">Add Application Insights logging</span></span>

<span data-ttu-id="45a50-222">When the project runs in Azure, you can't monitor function execution by viewing console output.</span><span class="sxs-lookup"><span data-stu-id="45a50-222">When the project runs in Azure, you can't monitor function execution by viewing console output.</span></span> <span data-ttu-id="45a50-223">The monitoring solution we recommend is [Application Insights](../application-insights/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-223">The monitoring solution we recommend is [Application Insights](../application-insights/app-insights-overview.md).</span></span> <span data-ttu-id="45a50-224">For more information, see [Monitor Azure Functions](../azure-functions/functions-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-224">For more information, see [Monitor Azure Functions](../azure-functions/functions-monitoring.md).</span></span>

<span data-ttu-id="45a50-225">In this section, you do the following tasks to set up Application Insights logging before you deploy to Azure:</span><span class="sxs-lookup"><span data-stu-id="45a50-225">In this section, you do the following tasks to set up Application Insights logging before you deploy to Azure:</span></span>

* <span data-ttu-id="45a50-226">Make sure you have an App Service app and an Application Insights instance to work with.</span><span class="sxs-lookup"><span data-stu-id="45a50-226">Make sure you have an App Service app and an Application Insights instance to work with.</span></span>
* <span data-ttu-id="45a50-227">Configure the App Service app to use the Application Insights instance and the storage account that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="45a50-227">Configure the App Service app to use the Application Insights instance and the storage account that you created earlier.</span></span>
* <span data-ttu-id="45a50-228">Set up the project for logging to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="45a50-228">Set up the project for logging to Application Insights.</span></span>

### <a name="create-app-service-app-and-application-insights-instance"></a><span data-ttu-id="45a50-229">Create App Service app and Application Insights instance</span><span class="sxs-lookup"><span data-stu-id="45a50-229">Create App Service app and Application Insights instance</span></span>

1. <span data-ttu-id="45a50-230">If you don't already have an App Service app that you can use, [create one](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-230">If you don't already have an App Service app that you can use, [create one](app-service-web-get-started-dotnet-framework.md).</span></span>

1. <span data-ttu-id="45a50-231">If you don't already have an Application Insights resource that you can use, [create one](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-231">If you don't already have an Application Insights resource that you can use, [create one](../application-insights/app-insights-create-new-resource.md).</span></span> <span data-ttu-id="45a50-232">Set **Application type** to **General**, and skip the sections that follow **Copy the instrumentation key**.</span><span class="sxs-lookup"><span data-stu-id="45a50-232">Set **Application type** to **General**, and skip the sections that follow **Copy the instrumentation key**.</span></span>

1. <span data-ttu-id="45a50-233">If you already have an Application Insights resource that you want to use, [copy the instrumentation key](../application-insights/app-insights-create-new-resource.md#copy-the-instrumentation-key).</span><span class="sxs-lookup"><span data-stu-id="45a50-233">If you already have an Application Insights resource that you want to use, [copy the instrumentation key](../application-insights/app-insights-create-new-resource.md#copy-the-instrumentation-key).</span></span>

### <a name="configure-app-settings"></a><span data-ttu-id="45a50-234">Configure app settings</span><span class="sxs-lookup"><span data-stu-id="45a50-234">Configure app settings</span></span> 

1. <span data-ttu-id="45a50-235">In **Server Explorer**, expand the **App Service** node under **Azure**.</span><span class="sxs-lookup"><span data-stu-id="45a50-235">In **Server Explorer**, expand the **App Service** node under **Azure**.</span></span>

1. <span data-ttu-id="45a50-236">Expand the resource group that your App Service app is in, and then right-click your App Service app.</span><span class="sxs-lookup"><span data-stu-id="45a50-236">Expand the resource group that your App Service app is in, and then right-click your App Service app.</span></span>

1. <span data-ttu-id="45a50-237">Select **View Settings**.</span><span class="sxs-lookup"><span data-stu-id="45a50-237">Select **View Settings**.</span></span>

1. <span data-ttu-id="45a50-238">In the **Connection Strings** box, add the following entry.</span><span class="sxs-lookup"><span data-stu-id="45a50-238">In the **Connection Strings** box, add the following entry.</span></span>

   |<span data-ttu-id="45a50-239">Name</span><span class="sxs-lookup"><span data-stu-id="45a50-239">Name</span></span>  |<span data-ttu-id="45a50-240">connection String</span><span class="sxs-lookup"><span data-stu-id="45a50-240">connection String</span></span>  |<span data-ttu-id="45a50-241">Database Type</span><span class="sxs-lookup"><span data-stu-id="45a50-241">Database Type</span></span>|
   |---------|---------|------|
   |<span data-ttu-id="45a50-242">AzureWebJobsStorage</span><span class="sxs-lookup"><span data-stu-id="45a50-242">AzureWebJobsStorage</span></span> | <span data-ttu-id="45a50-243">{the Storage connection string that you copied earlier}</span><span class="sxs-lookup"><span data-stu-id="45a50-243">{the Storage connection string that you copied earlier}</span></span>|<span data-ttu-id="45a50-244">Custom</span><span class="sxs-lookup"><span data-stu-id="45a50-244">Custom</span></span>|
   
1. <span data-ttu-id="45a50-245">If the **Application Settings** box doesn't have an Application Insights instrumentation key, add the one that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="45a50-245">If the **Application Settings** box doesn't have an Application Insights instrumentation key, add the one that you copied earlier.</span></span> <span data-ttu-id="45a50-246">(The instrumentation key may already be there, depending on how you created the App Service app.)</span><span class="sxs-lookup"><span data-stu-id="45a50-246">(The instrumentation key may already be there, depending on how you created the App Service app.)</span></span>

   |<span data-ttu-id="45a50-247">Name</span><span class="sxs-lookup"><span data-stu-id="45a50-247">Name</span></span>  |<span data-ttu-id="45a50-248">Value</span><span class="sxs-lookup"><span data-stu-id="45a50-248">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="45a50-249">APPINSIGHTS_INSTRUMENTATIONKEY</span><span class="sxs-lookup"><span data-stu-id="45a50-249">APPINSIGHTS_INSTRUMENTATIONKEY</span></span> | <span data-ttu-id="45a50-250">{instrumentation key}</span><span class="sxs-lookup"><span data-stu-id="45a50-250">{instrumentation key}</span></span> |

1. <span data-ttu-id="45a50-251">Replace *{instrumentation key}* with the instrumentation key from the Application Insights resource that you're using.</span><span class="sxs-lookup"><span data-stu-id="45a50-251">Replace *{instrumentation key}* with the instrumentation key from the Application Insights resource that you're using.</span></span>

1. <span data-ttu-id="45a50-252">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="45a50-252">Select **Save**.</span></span>

1. <span data-ttu-id="45a50-253">Add the following XML to the *App.config* file, immediately after the connection strings collection.</span><span class="sxs-lookup"><span data-stu-id="45a50-253">Add the following XML to the *App.config* file, immediately after the connection strings collection.</span></span>

   ```xml
   <appSettings>
     <add key="APPINSIGHTS_INSTRUMENTATIONKEY" value="{instrumentation key}" />
   </appSettings>
   ```

1. <span data-ttu-id="45a50-254">Replace *{instrumentation key}* with the instrumentation key from the Application Insights resource that you're using.</span><span class="sxs-lookup"><span data-stu-id="45a50-254">Replace *{instrumentation key}* with the instrumentation key from the Application Insights resource that you're using.</span></span>

   <span data-ttu-id="45a50-255">Adding this data to the *App.config* file enables you to test the Application Insights connection when you run the project locally.</span><span class="sxs-lookup"><span data-stu-id="45a50-255">Adding this data to the *App.config* file enables you to test the Application Insights connection when you run the project locally.</span></span> 

1. <span data-ttu-id="45a50-256">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="45a50-256">Save your changes.</span></span>

### <a name="add-application-insights-logging-provider"></a><span data-ttu-id="45a50-257">Add Application Insights logging provider</span><span class="sxs-lookup"><span data-stu-id="45a50-257">Add Application Insights logging provider</span></span>

1. <span data-ttu-id="45a50-258">Install the latest stable 2.x version of the NuGet package for the Application Insights logging provider:  `Microsoft.Azure.WebJobs.Logging.ApplicationInsights`.</span><span class="sxs-lookup"><span data-stu-id="45a50-258">Install the latest stable 2.x version of the NuGet package for the Application Insights logging provider:  `Microsoft.Azure.WebJobs.Logging.ApplicationInsights`.</span></span>

   <span data-ttu-id="45a50-259">Here's the **Package Manager Console** command for version 2.2.0:</span><span class="sxs-lookup"><span data-stu-id="45a50-259">Here's the **Package Manager Console** command for version 2.2.0:</span></span>

   ```powershell
   Install-Package Microsoft.Azure.WebJobs.Logging.ApplicationInsights -version 2.2.0
   ``` 

1. <span data-ttu-id="45a50-260">Install the latest stable 4.x version of the NuGet package for the .NET configuration manager:  `System.Configuration.ConfigurationManager`.</span><span class="sxs-lookup"><span data-stu-id="45a50-260">Install the latest stable 4.x version of the NuGet package for the .NET configuration manager:  `System.Configuration.ConfigurationManager`.</span></span>

   <span data-ttu-id="45a50-261">Here's the **Package Manager Console** command for version 4.4.1:</span><span class="sxs-lookup"><span data-stu-id="45a50-261">Here's the **Package Manager Console** command for version 4.4.1:</span></span>

   ```powershell
   Install-Package System.Configuration.ConfigurationManager -version 4.4.1
   ``` 

1. <span data-ttu-id="45a50-262">Open *Program.cs* and add a `using` statement for the configuration manager:</span><span class="sxs-lookup"><span data-stu-id="45a50-262">Open *Program.cs* and add a `using` statement for the configuration manager:</span></span>

   ```csharp
   using System.Configuration;
   ```

1. <span data-ttu-id="45a50-263">Replace the code in the `Main` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="45a50-263">Replace the code in the `Main` method with the following code:</span></span>

   ```csharp
   using (var loggerFactory = new LoggerFactory())
   {
       var config = new JobHostConfiguration();
       var instrumentationKey =
           ConfigurationManager.AppSettings["APPINSIGHTS_INSTRUMENTATIONKEY"];
       config.DashboardConnectionString = "";
       config.LoggerFactory = loggerFactory
           .AddApplicationInsights(instrumentationKey, null)
           .AddConsole();
       var host = new JobHost(config);
       host.RunAndBlock();
   }
   ```

   <span data-ttu-id="45a50-264">This code makes the following changes:</span><span class="sxs-lookup"><span data-stu-id="45a50-264">This code makes the following changes:</span></span>

   * <span data-ttu-id="45a50-265">Adds an Application Insights logging provider with default [filtering](webjobs-sdk-how-to.md#log-filtering); all Information and higher level logs will now go to both the console and Application Insights when you're running locally.</span><span class="sxs-lookup"><span data-stu-id="45a50-265">Adds an Application Insights logging provider with default [filtering](webjobs-sdk-how-to.md#log-filtering); all Information and higher level logs will now go to both the console and Application Insights when you're running locally.</span></span> 
   * <span data-ttu-id="45a50-266">Puts the `LoggerFactory` object in a `using` block to ensure that log output is flushed when the host exits.</span><span class="sxs-lookup"><span data-stu-id="45a50-266">Puts the `LoggerFactory` object in a `using` block to ensure that log output is flushed when the host exits.</span></span> 

## <a name="test-application-insights-logging"></a><span data-ttu-id="45a50-267">Test Application Insights logging</span><span class="sxs-lookup"><span data-stu-id="45a50-267">Test Application Insights logging</span></span>

<span data-ttu-id="45a50-268">In this section you run locally again to verify that logging data is now going to Application Insights as well as to the console.</span><span class="sxs-lookup"><span data-stu-id="45a50-268">In this section you run locally again to verify that logging data is now going to Application Insights as well as to the console.</span></span>

1. <span data-ttu-id="45a50-269">Use **Server Explorer** to create a queue message, the same way you did [earlier](#trigger-the-function), except enter *Hello App Insights!*</span><span class="sxs-lookup"><span data-stu-id="45a50-269">Use **Server Explorer** to create a queue message, the same way you did [earlier](#trigger-the-function), except enter *Hello App Insights!*</span></span> <span data-ttu-id="45a50-270">as the message text.</span><span class="sxs-lookup"><span data-stu-id="45a50-270">as the message text.</span></span>

1. <span data-ttu-id="45a50-271">Run the project.</span><span class="sxs-lookup"><span data-stu-id="45a50-271">Run the project.</span></span>

   <span data-ttu-id="45a50-272">The WebJobs SDK processes the queue message and you see the logs in the console window.</span><span class="sxs-lookup"><span data-stu-id="45a50-272">The WebJobs SDK processes the queue message and you see the logs in the console window.</span></span>

1. <span data-ttu-id="45a50-273">Close the console window.</span><span class="sxs-lookup"><span data-stu-id="45a50-273">Close the console window.</span></span>

1. <span data-ttu-id="45a50-274">Open the [Azure portal](https://portal.azure.com/), and go to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="45a50-274">Open the [Azure portal](https://portal.azure.com/), and go to your Application Insights resource.</span></span>

1. <span data-ttu-id="45a50-275">Select **Search**.</span><span class="sxs-lookup"><span data-stu-id="45a50-275">Select **Search**.</span></span>

   ![Select Search](./media/webjobs-sdk-get-started/select-search.png)

1. <span data-ttu-id="45a50-277">If you don't see the *Hello App Insights!*</span><span class="sxs-lookup"><span data-stu-id="45a50-277">If you don't see the *Hello App Insights!*</span></span> <span data-ttu-id="45a50-278">message, select **Refresh** periodically for several minutes.</span><span class="sxs-lookup"><span data-stu-id="45a50-278">message, select **Refresh** periodically for several minutes.</span></span> <span data-ttu-id="45a50-279">(Logs don't appear immediately because it takes a while for the Application Insights client to flush the logs it processes.)</span><span class="sxs-lookup"><span data-stu-id="45a50-279">(Logs don't appear immediately because it takes a while for the Application Insights client to flush the logs it processes.)</span></span>

   ![Logs in Application Insights](./media/webjobs-sdk-get-started/logs-in-ai.png)

1. <span data-ttu-id="45a50-281">Close the console window.</span><span class="sxs-lookup"><span data-stu-id="45a50-281">Close the console window.</span></span>

## <a name="deploy-as-a-webjob"></a><span data-ttu-id="45a50-282">Deploy as a WebJob</span><span class="sxs-lookup"><span data-stu-id="45a50-282">Deploy as a WebJob</span></span>

<span data-ttu-id="45a50-283">In this section you deploy the project as a WebJob.</span><span class="sxs-lookup"><span data-stu-id="45a50-283">In this section you deploy the project as a WebJob.</span></span> <span data-ttu-id="45a50-284">You deploy it to an App Service app that you [created earlier](#create-app-service-app-and-application-insights-instance).</span><span class="sxs-lookup"><span data-stu-id="45a50-284">You deploy it to an App Service app that you [created earlier](#create-app-service-app-and-application-insights-instance).</span></span> <span data-ttu-id="45a50-285">To test your code while it runs in Azure, you'll trigger a function invocation by creating a queue message.</span><span class="sxs-lookup"><span data-stu-id="45a50-285">To test your code while it runs in Azure, you'll trigger a function invocation by creating a queue message.</span></span>

1. <span data-ttu-id="45a50-286">In **Solution Explorer**, right-click the project, and then select **Publish as Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="45a50-286">In **Solution Explorer**, right-click the project, and then select **Publish as Azure WebJob**.</span></span>

1. <span data-ttu-id="45a50-287">In the **Add Azure WebJob** dialog, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-287">In the **Add Azure WebJob** dialog, select **OK**.</span></span>

   ![Add Azure WebJob](./media/webjobs-sdk-get-started/add-azure-webjob.png)

   <span data-ttu-id="45a50-289">Visual Studio automatically installs a NuGet package for WebJob publishing.</span><span class="sxs-lookup"><span data-stu-id="45a50-289">Visual Studio automatically installs a NuGet package for WebJob publishing.</span></span>

1. <span data-ttu-id="45a50-290">In the **Profile** step of the **Publish** wizard, select **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="45a50-290">In the **Profile** step of the **Publish** wizard, select **Microsoft Azure App Service**.</span></span>

   ![Publish dialog](./media/webjobs-sdk-get-started/publish-dialog.png)

1. <span data-ttu-id="45a50-292">In the **App Service** dialog, select **your resource group > your App Service app**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-292">In the **App Service** dialog, select **your resource group > your App Service app**, and then select **OK**.</span></span>

   ![App Service dialog](./media/webjobs-sdk-get-started/app-service-dialog.png)

1. <span data-ttu-id="45a50-294">In the **Connection** step of the wizard, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="45a50-294">In the **Connection** step of the wizard, select **Publish**.</span></span>

## <a name="trigger-the-function-in-azure"></a><span data-ttu-id="45a50-295">Trigger the function in Azure</span><span class="sxs-lookup"><span data-stu-id="45a50-295">Trigger the function in Azure</span></span>

1. <span data-ttu-id="45a50-296">Make sure you're not running locally (close the console window if it's still open).</span><span class="sxs-lookup"><span data-stu-id="45a50-296">Make sure you're not running locally (close the console window if it's still open).</span></span> <span data-ttu-id="45a50-297">Otherwise the local instance might be the first to process any queue messages you create.</span><span class="sxs-lookup"><span data-stu-id="45a50-297">Otherwise the local instance might be the first to process any queue messages you create.</span></span>

1. <span data-ttu-id="45a50-298">Use **Server Explorer** to create a queue message, the same way you did [earlier](#trigger-the-function), except enter *Hello Azure!*.</span><span class="sxs-lookup"><span data-stu-id="45a50-298">Use **Server Explorer** to create a queue message, the same way you did [earlier](#trigger-the-function), except enter *Hello Azure!*.</span></span>

1. <span data-ttu-id="45a50-299">Refresh the **Queue** page in Visual Studio, and the new message has disappeared because the function running in Azure App Service processed it.</span><span class="sxs-lookup"><span data-stu-id="45a50-299">Refresh the **Queue** page in Visual Studio, and the new message has disappeared because the function running in Azure App Service processed it.</span></span>

   > [!TIP]
   > <span data-ttu-id="45a50-300">When you're testing in Azure, use [development mode](webjobs-sdk-how-to.md#jobhost-development-settings) to ensure that a queue trigger function is invoked right away and avoid delays due to [queue polling exponential backoff](../azure-functions/functions-bindings-storage-queue.md#trigger---polling-algorithm).</span><span class="sxs-lookup"><span data-stu-id="45a50-300">When you're testing in Azure, use [development mode](webjobs-sdk-how-to.md#jobhost-development-settings) to ensure that a queue trigger function is invoked right away and avoid delays due to [queue polling exponential backoff](../azure-functions/functions-bindings-storage-queue.md#trigger---polling-algorithm).</span></span>

### <a name="view-logs-in-application-insights"></a><span data-ttu-id="45a50-301">View logs in Application Insights</span><span class="sxs-lookup"><span data-stu-id="45a50-301">View logs in Application Insights</span></span>

1. <span data-ttu-id="45a50-302">Open the [Azure portal](https://portal.azure.com/), and go to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="45a50-302">Open the [Azure portal](https://portal.azure.com/), and go to your Application Insights resource.</span></span>

1. <span data-ttu-id="45a50-303">Select **Search**.</span><span class="sxs-lookup"><span data-stu-id="45a50-303">Select **Search**.</span></span>

1. <span data-ttu-id="45a50-304">If you don't see the *Hello Azure!*</span><span class="sxs-lookup"><span data-stu-id="45a50-304">If you don't see the *Hello Azure!*</span></span> <span data-ttu-id="45a50-305">message, select **Refresh** periodically for several minutes.</span><span class="sxs-lookup"><span data-stu-id="45a50-305">message, select **Refresh** periodically for several minutes.</span></span>

   <span data-ttu-id="45a50-306">You see the logs from the function running in a WebJob, including the *Hello Azure!*</span><span class="sxs-lookup"><span data-stu-id="45a50-306">You see the logs from the function running in a WebJob, including the *Hello Azure!*</span></span> <span data-ttu-id="45a50-307">text that you entered in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="45a50-307">text that you entered in the preceding section.</span></span>

## <a name="add-an-input-binding"></a><span data-ttu-id="45a50-308">Add an input binding</span><span class="sxs-lookup"><span data-stu-id="45a50-308">Add an input binding</span></span>

<span data-ttu-id="45a50-309">Input bindings simplify code that reads data.</span><span class="sxs-lookup"><span data-stu-id="45a50-309">Input bindings simplify code that reads data.</span></span> <span data-ttu-id="45a50-310">For this example, the queue message will be a blob name and you'll use the blob name to find and read a blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="45a50-310">For this example, the queue message will be a blob name and you'll use the blob name to find and read a blob in Azure Storage.</span></span>

1. <span data-ttu-id="45a50-311">In *Functions.cs*, replace the `ProcessQueueMessage` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="45a50-311">In *Functions.cs*, replace the `ProcessQueueMessage` method with the following code:</span></span>

   ```cs
   public static void ProcessQueueMessage(
       [QueueTrigger("queue")] string message,
       [Blob("container/{queueTrigger}", FileAccess.Read)] Stream myBlob,
       ILogger logger)
   {
       logger.LogInformation($"Blob name:{message} \n Size: {myBlob.Length} bytes");
   }
   ```

   <span data-ttu-id="45a50-312">In this code, `queueTrigger` is a [binding expression](../azure-functions/functions-triggers-bindings.md#binding-expressions-and-patterns), which means it resolves to a different value at runtime.</span><span class="sxs-lookup"><span data-stu-id="45a50-312">In this code, `queueTrigger` is a [binding expression](../azure-functions/functions-triggers-bindings.md#binding-expressions-and-patterns), which means it resolves to a different value at runtime.</span></span>  <span data-ttu-id="45a50-313">At runtime it has the contents of the queue message.</span><span class="sxs-lookup"><span data-stu-id="45a50-313">At runtime it has the contents of the queue message.</span></span>

1. <span data-ttu-id="45a50-314">Add a `using`:</span><span class="sxs-lookup"><span data-stu-id="45a50-314">Add a `using`:</span></span>

   ```cs
   using System.IO;
   ```

1. <span data-ttu-id="45a50-315">Create a blob container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="45a50-315">Create a blob container in your storage account.</span></span>

   <span data-ttu-id="45a50-316">a.</span><span class="sxs-lookup"><span data-stu-id="45a50-316">a.</span></span> <span data-ttu-id="45a50-317">In **Server Explorer**, expand the node for your storage account, right-click **Blobs**, and then select **Create Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="45a50-317">In **Server Explorer**, expand the node for your storage account, right-click **Blobs**, and then select **Create Blob Container**.</span></span>

   <span data-ttu-id="45a50-318">b.</span><span class="sxs-lookup"><span data-stu-id="45a50-318">b.</span></span> <span data-ttu-id="45a50-319">In the **Create Blob Container** dialog, enter *container* as the container name, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-319">In the **Create Blob Container** dialog, enter *container* as the container name, and then click **OK**.</span></span>

1. <span data-ttu-id="45a50-320">Upload the *Program.cs* file to the blob container.</span><span class="sxs-lookup"><span data-stu-id="45a50-320">Upload the *Program.cs* file to the blob container.</span></span> <span data-ttu-id="45a50-321">(This file is used here as an example; you could upload any text file and create a queue message with the file's name.)</span><span class="sxs-lookup"><span data-stu-id="45a50-321">(This file is used here as an example; you could upload any text file and create a queue message with the file's name.)</span></span>

   <span data-ttu-id="45a50-322">a.</span><span class="sxs-lookup"><span data-stu-id="45a50-322">a.</span></span> <span data-ttu-id="45a50-323">In **Server Explorer**, double-click the node for the container you just created.</span><span class="sxs-lookup"><span data-stu-id="45a50-323">In **Server Explorer**, double-click the node for the container you just created.</span></span>

   <span data-ttu-id="45a50-324">b.</span><span class="sxs-lookup"><span data-stu-id="45a50-324">b.</span></span> <span data-ttu-id="45a50-325">In the **Container** window, select the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="45a50-325">In the **Container** window, select the **Upload** button.</span></span>

   ![Blob upload button](./media/webjobs-sdk-get-started/blob-upload-button.png)

   <span data-ttu-id="45a50-327">c.</span><span class="sxs-lookup"><span data-stu-id="45a50-327">c.</span></span> <span data-ttu-id="45a50-328">Find and select *Program.cs*, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="45a50-328">Find and select *Program.cs*, and then select **OK**.</span></span>

1. <span data-ttu-id="45a50-329">Create a queue message in the queue you created earlier, with *Program.cs* as the text of the message.</span><span class="sxs-lookup"><span data-stu-id="45a50-329">Create a queue message in the queue you created earlier, with *Program.cs* as the text of the message.</span></span>

   ![Queue message Program.cs](./media/webjobs-sdk-get-started/queue-msg-program-cs.png)

1. <span data-ttu-id="45a50-331">Run the project.</span><span class="sxs-lookup"><span data-stu-id="45a50-331">Run the project.</span></span>

   <span data-ttu-id="45a50-332">The queue message triggers the function, which then reads the blob and logs its length.</span><span class="sxs-lookup"><span data-stu-id="45a50-332">The queue message triggers the function, which then reads the blob and logs its length.</span></span> <span data-ttu-id="45a50-333">The console output looks like this:</span><span class="sxs-lookup"><span data-stu-id="45a50-333">The console output looks like this:</span></span>

   ```console
   Found the following functions:
   ConsoleApp1.Functions.ProcessQueueMessage
   Job host started
   Executing 'Functions.ProcessQueueMessage' (Reason='New queue message detected on 'queue'.', Id=5a2ac479-de13-4f41-aae9-1361f291ff88)
   Blob name:Program.cs
   Size: 532 bytes
   Executed 'Functions.ProcessQueueMessage' (Succeeded, Id=5a2ac479-de13-4f41-aae9-1361f291ff88)
   ```

## <a name="add-an-output-binding"></a><span data-ttu-id="45a50-334">Add an output binding</span><span class="sxs-lookup"><span data-stu-id="45a50-334">Add an output binding</span></span>

<span data-ttu-id="45a50-335">Output bindings simplify code that writes data.</span><span class="sxs-lookup"><span data-stu-id="45a50-335">Output bindings simplify code that writes data.</span></span> <span data-ttu-id="45a50-336">This example modifies the previous one by writing a copy of the blob instead of logging its size.</span><span class="sxs-lookup"><span data-stu-id="45a50-336">This example modifies the previous one by writing a copy of the blob instead of logging its size.</span></span>

1. <span data-ttu-id="45a50-337">Replace the `ProcessQueueMessage` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="45a50-337">Replace the `ProcessQueueMessage` method with the following code:</span></span>

   ```cs
   public static void ProcessQueueMessage(
       [QueueTrigger("queue")] string message,
       [Blob("container/{queueTrigger}", FileAccess.Read)] Stream myBlob,
       [Blob("container/copy-{queueTrigger}", FileAccess.Write)] Stream outputBlob,
       ILogger logger)
   {
       logger.LogInformation($"Blob name:{message} \n Size: {myBlob.Length} bytes");
       myBlob.CopyTo(outputBlob);
   }
   ```

1. <span data-ttu-id="45a50-338">Create another queue message with *Program.cs* as the text of the message.</span><span class="sxs-lookup"><span data-stu-id="45a50-338">Create another queue message with *Program.cs* as the text of the message.</span></span>

1. <span data-ttu-id="45a50-339">Run the project.</span><span class="sxs-lookup"><span data-stu-id="45a50-339">Run the project.</span></span>

   <span data-ttu-id="45a50-340">The queue message triggers the function, which then reads the blob, logs its length, and creates a new blob.</span><span class="sxs-lookup"><span data-stu-id="45a50-340">The queue message triggers the function, which then reads the blob, logs its length, and creates a new blob.</span></span> <span data-ttu-id="45a50-341">The console output is the same, but when you go to the blob container window and select **Refresh**, you see a new blob named *copy-Program.cs.*</span><span class="sxs-lookup"><span data-stu-id="45a50-341">The console output is the same, but when you go to the blob container window and select **Refresh**, you see a new blob named *copy-Program.cs.*</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a50-342">Next steps</span><span class="sxs-lookup"><span data-stu-id="45a50-342">Next steps</span></span>

<span data-ttu-id="45a50-343">This guide has shown how to create, run, and deploy a WebJobs SDK project.</span><span class="sxs-lookup"><span data-stu-id="45a50-343">This guide has shown how to create, run, and deploy a WebJobs SDK project.</span></span>

<span data-ttu-id="45a50-344">To show everything that goes into a WebJobs SDK project, the instructions had you create a project from scratch.</span><span class="sxs-lookup"><span data-stu-id="45a50-344">To show everything that goes into a WebJobs SDK project, the instructions had you create a project from scratch.</span></span> <span data-ttu-id="45a50-345">However, when you create your next project, consider using the **Azure WebJob** template in the **Cloud** category.</span><span class="sxs-lookup"><span data-stu-id="45a50-345">However, when you create your next project, consider using the **Azure WebJob** template in the **Cloud** category.</span></span> <span data-ttu-id="45a50-346">This template creates a project with NuGet packages and sample code already set up.</span><span class="sxs-lookup"><span data-stu-id="45a50-346">This template creates a project with NuGet packages and sample code already set up.</span></span> <span data-ttu-id="45a50-347">Note that the sample code may need to be changed to use the new logging framework.</span><span class="sxs-lookup"><span data-stu-id="45a50-347">Note that the sample code may need to be changed to use the new logging framework.</span></span>

<span data-ttu-id="45a50-348">For more information, see [How to use the WebJobs SDK](webjobs-sdk-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="45a50-348">For more information, see [How to use the WebJobs SDK](webjobs-sdk-how-to.md).</span></span>
