---
title: How to run durable functions as WebJobs - Azure
description: Learn how to code and configure Durable Functions to run in WebJobs by using the WebJobs SDK.
services: functions
author: ggailey777
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/25/2018
ms.author: azfuncdf
ms.openlocfilehash: 83650649e891b752b81ca40eeec68d14447b37ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869488"
---
# <a name="how-to-run-durable-functions-as-webjobs"></a><span data-ttu-id="462c3-103">How to run durable functions as WebJobs</span><span class="sxs-lookup"><span data-stu-id="462c3-103">How to run durable functions as WebJobs</span></span>

<span data-ttu-id="462c3-104">[Azure Functions](functions-overview.md) and the [Durable Functions](durable-functions-overview.md) extension are built on the [WebJobs SDK](../app-service/web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="462c3-104">[Azure Functions](functions-overview.md) and the [Durable Functions](durable-functions-overview.md) extension are built on the [WebJobs SDK](../app-service/web-sites-create-web-jobs.md).</span></span> <span data-ttu-id="462c3-105">The `JobHost` in the WebJobs SDK is the runtime in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="462c3-105">The `JobHost` in the WebJobs SDK is the runtime in Azure Functions.</span></span> <span data-ttu-id="462c3-106">If you need to control `JobHost` behavior in ways not possible in Azure Functions, you can develop and run durable functions by using the WebJobs SDK yourself.</span><span class="sxs-lookup"><span data-stu-id="462c3-106">If you need to control `JobHost` behavior in ways not possible in Azure Functions, you can develop and run durable functions by using the WebJobs SDK yourself.</span></span> <span data-ttu-id="462c3-107">You can then run your durable functions in an Azure WebJob or anywhere a console application runs.</span><span class="sxs-lookup"><span data-stu-id="462c3-107">You can then run your durable functions in an Azure WebJob or anywhere a console application runs.</span></span>

<span data-ttu-id="462c3-108">The chaining Durable Functions sample is available in a WebJobs SDK version: download or clone the [Durable Functions repository](https://github.com/azure/azure-functions-durable-extension/) and navigate to the *samples\\webjobssdk\\chaining* folder.</span><span class="sxs-lookup"><span data-stu-id="462c3-108">The chaining Durable Functions sample is available in a WebJobs SDK version: download or clone the [Durable Functions repository](https://github.com/azure/azure-functions-durable-extension/) and navigate to the *samples\\webjobssdk\\chaining* folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="462c3-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="462c3-109">Prerequisites</span></span>

<span data-ttu-id="462c3-110">This article assumes you're familiar with the basics of the WebJobs SDK, C# class library development for Azure Functions, and Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="462c3-110">This article assumes you're familiar with the basics of the WebJobs SDK, C# class library development for Azure Functions, and Durable Functions.</span></span> <span data-ttu-id="462c3-111">If you need an introduction to these topics, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="462c3-111">If you need an introduction to these topics, see the following resources:</span></span>

* [<span data-ttu-id="462c3-112">Get started with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="462c3-112">Get started with the WebJobs SDK</span></span>](../app-service/webjobs-sdk-get-started.md)
* [<span data-ttu-id="462c3-113">Create your first function using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="462c3-113">Create your first function using Visual Studio</span></span>](functions-create-your-first-function-visual-studio.md)
* [<span data-ttu-id="462c3-114">Durable Functions</span><span class="sxs-lookup"><span data-stu-id="462c3-114">Durable Functions</span></span>](durable-functions-sequence.md)

<span data-ttu-id="462c3-115">To complete the steps in this article:</span><span class="sxs-lookup"><span data-stu-id="462c3-115">To complete the steps in this article:</span></span>

* <span data-ttu-id="462c3-116">[Install Visual Studio 2017 version 15.6 or later](https://docs.microsoft.com/visualstudio/install/) with the **Azure development** workload.</span><span class="sxs-lookup"><span data-stu-id="462c3-116">[Install Visual Studio 2017 version 15.6 or later](https://docs.microsoft.com/visualstudio/install/) with the **Azure development** workload.</span></span>

  <span data-ttu-id="462c3-117">If you already have Visual Studio but don't have that workload, add the workload by selecting **Tools > Get Tools and Features**.</span><span class="sxs-lookup"><span data-stu-id="462c3-117">If you already have Visual Studio but don't have that workload, add the workload by selecting **Tools > Get Tools and Features**.</span></span> 

  <span data-ttu-id="462c3-118">(You can use [Visual Studio Code](https://code.visualstudio.com/) instead, but some of the instructions are specific to Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="462c3-118">(You can use [Visual Studio Code](https://code.visualstudio.com/) instead, but some of the instructions are specific to Visual Studio.)</span></span>

* <span data-ttu-id="462c3-119">Install and run [Azure Storage Emulator](../storage/common/storage-use-emulator.md) version 5.2 or later.</span><span class="sxs-lookup"><span data-stu-id="462c3-119">Install and run [Azure Storage Emulator](../storage/common/storage-use-emulator.md) version 5.2 or later.</span></span> <span data-ttu-id="462c3-120">An alternative is to update the *App.config* file with an Azure Storage connection string.</span><span class="sxs-lookup"><span data-stu-id="462c3-120">An alternative is to update the *App.config* file with an Azure Storage connection string.</span></span>

## <a name="webjobs-sdk-versions"></a><span data-ttu-id="462c3-121">WebJobs SDK versions</span><span class="sxs-lookup"><span data-stu-id="462c3-121">WebJobs SDK versions</span></span>

<span data-ttu-id="462c3-122">This article explains how to develop a WebJobs SDK 2.x project (equivalent to Azure Functions version 1.x).</span><span class="sxs-lookup"><span data-stu-id="462c3-122">This article explains how to develop a WebJobs SDK 2.x project (equivalent to Azure Functions version 1.x).</span></span> <span data-ttu-id="462c3-123">For information about version 3.x, see [WebJobs SDK 3.x](#webjobs-sdk-3x) later in this article.</span><span class="sxs-lookup"><span data-stu-id="462c3-123">For information about version 3.x, see [WebJobs SDK 3.x](#webjobs-sdk-3x) later in this article.</span></span> 

## <a name="create-console-app"></a><span data-ttu-id="462c3-124">Create console app</span><span class="sxs-lookup"><span data-stu-id="462c3-124">Create console app</span></span>

<span data-ttu-id="462c3-125">A WebJobs SDK project is just a console app project with the appropriate NuGet packages installed.</span><span class="sxs-lookup"><span data-stu-id="462c3-125">A WebJobs SDK project is just a console app project with the appropriate NuGet packages installed.</span></span>

<span data-ttu-id="462c3-126">In the Visual Studio **New Project** dialog, select **Windows Classic Desktop > Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="462c3-126">In the Visual Studio **New Project** dialog, select **Windows Classic Desktop > Console App (.NET Framework)**.</span></span> <span data-ttu-id="462c3-127">In the project file, the `TargetFrameworkVersion` should be `v4.6.1`.</span><span class="sxs-lookup"><span data-stu-id="462c3-127">In the project file, the `TargetFrameworkVersion` should be `v4.6.1`.</span></span>

<span data-ttu-id="462c3-128">Visual Studio also has a WebJob project template, which you can use by selecting **Cloud > Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="462c3-128">Visual Studio also has a WebJob project template, which you can use by selecting **Cloud > Azure WebJob (.NET Framework)**.</span></span> <span data-ttu-id="462c3-129">This template installs many packages, some of which you might not need.</span><span class="sxs-lookup"><span data-stu-id="462c3-129">This template installs many packages, some of which you might not need.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="462c3-130">Install NuGet packages</span><span class="sxs-lookup"><span data-stu-id="462c3-130">Install NuGet packages</span></span>

<span data-ttu-id="462c3-131">You need NuGet packages for the WebJobs SDK, core bindings, the logging framework, and the Durable Task extension.</span><span class="sxs-lookup"><span data-stu-id="462c3-131">You need NuGet packages for the WebJobs SDK, core bindings, the logging framework, and the Durable Task extension.</span></span> <span data-ttu-id="462c3-132">Here are **Package Manager Console** commands for those packages, with latest stable version numbers as of the date this article was written:</span><span class="sxs-lookup"><span data-stu-id="462c3-132">Here are **Package Manager Console** commands for those packages, with latest stable version numbers as of the date this article was written:</span></span>

```powershell
Install-Package Microsoft.Azure.WebJobs.Extensions -version 2.2.0
Install-Package Microsoft.Extensions.Logging -version 2.0.1
Install-Package Microsoft.Azure.WebJobs.Extensions.DurableTask -version 1.4.0
```

<span data-ttu-id="462c3-133">You also need logging providers.</span><span class="sxs-lookup"><span data-stu-id="462c3-133">You also need logging providers.</span></span> <span data-ttu-id="462c3-134">The following commands install the Application Insights provider and the `ConfigurationManager`.</span><span class="sxs-lookup"><span data-stu-id="462c3-134">The following commands install the Application Insights provider and the `ConfigurationManager`.</span></span> <span data-ttu-id="462c3-135">The `ConfigurationManager` lets you get the Application Insights instrumentation key from app settings.</span><span class="sxs-lookup"><span data-stu-id="462c3-135">The `ConfigurationManager` lets you get the Application Insights instrumentation key from app settings.</span></span>

```powershell
Install-Package Microsoft.Azure.WebJobs.Logging.ApplicationInsights -version 2.2.0
Install-Package System.Configuration.ConfigurationManager -version 4.4.1
```

<span data-ttu-id="462c3-136">The following command installs the console provider:</span><span class="sxs-lookup"><span data-stu-id="462c3-136">The following command installs the console provider:</span></span>

```powershell
Install-Package Microsoft.Extensions.Logging.Console -version 2.0.1
```

## <a name="jobhost-code"></a><span data-ttu-id="462c3-137">JobHost code</span><span class="sxs-lookup"><span data-stu-id="462c3-137">JobHost code</span></span>

<span data-ttu-id="462c3-138">To use the Durable Functions extension, call `UseDurableTask` on the `JobHostConfiguration` object in your `Main` method:</span><span class="sxs-lookup"><span data-stu-id="462c3-138">To use the Durable Functions extension, call `UseDurableTask` on the `JobHostConfiguration` object in your `Main` method:</span></span>

```cs
var config = new JobHostConfiguration();
config.UseDurableTask(new DurableTaskExtension
{
    HubName = "MyTaskHub",
};
```

<span data-ttu-id="462c3-139">For a list of properties that you can set in the `DurableTaskExtension` object, see [host.json](functions-host-json.md#durabletask).</span><span class="sxs-lookup"><span data-stu-id="462c3-139">For a list of properties that you can set in the `DurableTaskExtension` object, see [host.json](functions-host-json.md#durabletask).</span></span>

<span data-ttu-id="462c3-140">The `Main` method is also the place to set up logging providers.</span><span class="sxs-lookup"><span data-stu-id="462c3-140">The `Main` method is also the place to set up logging providers.</span></span> <span data-ttu-id="462c3-141">The following example configures console and Application Insights providers.</span><span class="sxs-lookup"><span data-stu-id="462c3-141">The following example configures console and Application Insights providers.</span></span>

```cs
static void Main(string[] args)
{
    using (var loggerFactory = new LoggerFactory())
    {
        var config = new JobHostConfiguration();

        config.DashboardConnectionString = "";

        var instrumentationKey =
            ConfigurationManager.AppSettings["APPINSIGHTS_INSTRUMENTATIONKEY"];

        config.LoggerFactory = loggerFactory
            .AddApplicationInsights(instrumentationKey, null)
            .AddConsole();

        config.UseTimers();
        config.UseDurableTask(new DurableTaskExtension
        {
            HubName = "MyTaskHub",
        });
        var host = new JobHost(config);
        host.RunAndBlock();
    }
}
```

## <a name="functions"></a><span data-ttu-id="462c3-142">Functions</span><span class="sxs-lookup"><span data-stu-id="462c3-142">Functions</span></span>

<span data-ttu-id="462c3-143">There are a few differences in the code you write for WebJobs SDK functions compared to what you write for the Azure Functions service.</span><span class="sxs-lookup"><span data-stu-id="462c3-143">There are a few differences in the code you write for WebJobs SDK functions compared to what you write for the Azure Functions service.</span></span>

<span data-ttu-id="462c3-144">The WebJobs SDK doesn't support the following Azure Functions features:</span><span class="sxs-lookup"><span data-stu-id="462c3-144">The WebJobs SDK doesn't support the following Azure Functions features:</span></span>

* [<span data-ttu-id="462c3-145">FunctionName attribute</span><span class="sxs-lookup"><span data-stu-id="462c3-145">FunctionName attribute</span></span>](#functionname-attribute)
* [<span data-ttu-id="462c3-146">HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="462c3-146">HTTP trigger</span></span>](#http-trigger)
* [<span data-ttu-id="462c3-147">Durable Functions HTTP management API</span><span class="sxs-lookup"><span data-stu-id="462c3-147">Durable Functions HTTP management API</span></span>](#http-management-api)

### <a name="functionname-attribute"></a><span data-ttu-id="462c3-148">FunctionName attribute</span><span class="sxs-lookup"><span data-stu-id="462c3-148">FunctionName attribute</span></span>

<span data-ttu-id="462c3-149">In a WebJobs SDK project, the method name of a function is the function name.</span><span class="sxs-lookup"><span data-stu-id="462c3-149">In a WebJobs SDK project, the method name of a function is the function name.</span></span> <span data-ttu-id="462c3-150">The `FunctionName` attribute is used only in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="462c3-150">The `FunctionName` attribute is used only in Azure Functions.</span></span>

### <a name="http-trigger"></a><span data-ttu-id="462c3-151">HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="462c3-151">HTTP trigger</span></span>

<span data-ttu-id="462c3-152">The WebJobs SDK does not have an HTTP trigger.</span><span class="sxs-lookup"><span data-stu-id="462c3-152">The WebJobs SDK does not have an HTTP trigger.</span></span> <span data-ttu-id="462c3-153">The sample project's orchestration client uses a timer trigger:</span><span class="sxs-lookup"><span data-stu-id="462c3-153">The sample project's orchestration client uses a timer trigger:</span></span>

```cs
public static async Task CronJob(
    [TimerTrigger("0 */2 * * * *")] TimerInfo timer,
    [OrchestrationClient] DurableOrchestrationClient client,
    ILogger logger)
{
  ...
}
```

### <a name="http-management-api"></a><span data-ttu-id="462c3-154">HTTP management API</span><span class="sxs-lookup"><span data-stu-id="462c3-154">HTTP management API</span></span>

<span data-ttu-id="462c3-155">Because it has no HTTP trigger, the WebJobs SDK has no [HTTP management API](durable-functions-http-api.md).</span><span class="sxs-lookup"><span data-stu-id="462c3-155">Because it has no HTTP trigger, the WebJobs SDK has no [HTTP management API](durable-functions-http-api.md).</span></span>

<span data-ttu-id="462c3-156">In a WebJobs SDK project, you can call methods on the orchestration client object instead of sending HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="462c3-156">In a WebJobs SDK project, you can call methods on the orchestration client object instead of sending HTTP requests.</span></span> <span data-ttu-id="462c3-157">The following methods correspond to the three tasks you can do with the HTTP management API:</span><span class="sxs-lookup"><span data-stu-id="462c3-157">The following methods correspond to the three tasks you can do with the HTTP management API:</span></span>

* `GetStatusAsync`
* `RaiseEventAsync`
* `TerminateAsync`

<span data-ttu-id="462c3-158">The orchestration client function in the sample project starts the orchestrator function and then goes into a loop that calls `GetStatusAsync` every 2 seconds:</span><span class="sxs-lookup"><span data-stu-id="462c3-158">The orchestration client function in the sample project starts the orchestrator function and then goes into a loop that calls `GetStatusAsync` every 2 seconds:</span></span>

```cs
string instanceId = await client.StartNewAsync(nameof(HelloSequence), input: null);
logger.LogInformation($"Started new instance with ID = {instanceId}.");

DurableOrchestrationStatus status;
while (true)
{
    status = await client.GetStatusAsync(instanceId);
    logger.LogInformation($"Status: {status.RuntimeStatus}, Last update: {status.LastUpdatedTime}.");

    if (status.RuntimeStatus == OrchestrationRuntimeStatus.Completed ||
        status.RuntimeStatus == OrchestrationRuntimeStatus.Failed ||
        status.RuntimeStatus == OrchestrationRuntimeStatus.Terminated)
    {
        break;
    }

    await Task.Delay(TimeSpan.FromSeconds(2));
}
```

## <a name="run-the-sample"></a><span data-ttu-id="462c3-159">Run the sample</span><span class="sxs-lookup"><span data-stu-id="462c3-159">Run the sample</span></span>

<span data-ttu-id="462c3-160">This section provides an overview of how to run the [sample project](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/webjobssdk/chaining).</span><span class="sxs-lookup"><span data-stu-id="462c3-160">This section provides an overview of how to run the [sample project](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/webjobssdk/chaining).</span></span> <span data-ttu-id="462c3-161">For detailed instructions that explain how to run a WebJobs SDK project locally and deploy it to an Azure WebJob, see [Get started with the WebJobs SDK](../app-service/webjobs-sdk-get-started.md#deploy-as-a-webjob).</span><span class="sxs-lookup"><span data-stu-id="462c3-161">For detailed instructions that explain how to run a WebJobs SDK project locally and deploy it to an Azure WebJob, see [Get started with the WebJobs SDK](../app-service/webjobs-sdk-get-started.md#deploy-as-a-webjob).</span></span>

### <a name="run-locally"></a><span data-ttu-id="462c3-162">Run locally</span><span class="sxs-lookup"><span data-stu-id="462c3-162">Run locally</span></span>

1. <span data-ttu-id="462c3-163">Make sure the Storage emulator is running (see [Prerequisites](#prerequisites)).</span><span class="sxs-lookup"><span data-stu-id="462c3-163">Make sure the Storage emulator is running (see [Prerequisites](#prerequisites)).</span></span>

1. <span data-ttu-id="462c3-164">If you want to see logs in Application Insights when you run locally:</span><span class="sxs-lookup"><span data-stu-id="462c3-164">If you want to see logs in Application Insights when you run locally:</span></span>

  <span data-ttu-id="462c3-165">a.</span><span class="sxs-lookup"><span data-stu-id="462c3-165">a.</span></span> <span data-ttu-id="462c3-166">Create an Application Insights resource, app type **General**.</span><span class="sxs-lookup"><span data-stu-id="462c3-166">Create an Application Insights resource, app type **General**.</span></span>

  <span data-ttu-id="462c3-167">b.</span><span class="sxs-lookup"><span data-stu-id="462c3-167">b.</span></span> <span data-ttu-id="462c3-168">Save the instrumentation key in the *App.config* file.</span><span class="sxs-lookup"><span data-stu-id="462c3-168">Save the instrumentation key in the *App.config* file.</span></span>

1. <span data-ttu-id="462c3-169">Run the project.</span><span class="sxs-lookup"><span data-stu-id="462c3-169">Run the project.</span></span>

### <a name="run-in-azure"></a><span data-ttu-id="462c3-170">Run in Azure</span><span class="sxs-lookup"><span data-stu-id="462c3-170">Run in Azure</span></span>

1. <span data-ttu-id="462c3-171">Create a web app and a storage account.</span><span class="sxs-lookup"><span data-stu-id="462c3-171">Create a web app and a storage account.</span></span>

1. <span data-ttu-id="462c3-172">In the web app, save the Storage connection string in an app setting named AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="462c3-172">In the web app, save the Storage connection string in an app setting named AzureWebJobsStorage.</span></span>

1. <span data-ttu-id="462c3-173">Create an Application Insights resource, app type **General**.</span><span class="sxs-lookup"><span data-stu-id="462c3-173">Create an Application Insights resource, app type **General**.</span></span>

1. <span data-ttu-id="462c3-174">Save the instrumentation key in an app setting named APPINSIGHTS_INSTRUMENTATIONKEY.</span><span class="sxs-lookup"><span data-stu-id="462c3-174">Save the instrumentation key in an app setting named APPINSIGHTS_INSTRUMENTATIONKEY.</span></span>

1. <span data-ttu-id="462c3-175">Deploy as a WebJob.</span><span class="sxs-lookup"><span data-stu-id="462c3-175">Deploy as a WebJob.</span></span>

## <a name="webjobs-sdk-3x"></a><span data-ttu-id="462c3-176">WebJobs SDK 3.x</span><span class="sxs-lookup"><span data-stu-id="462c3-176">WebJobs SDK 3.x</span></span>

<span data-ttu-id="462c3-177">The main change introduced by 3.x is the use of .NET Core instead of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="462c3-177">The main change introduced by 3.x is the use of .NET Core instead of .NET Framework.</span></span> <span data-ttu-id="462c3-178">To create a 3.x project the instructions are the same, with these exceptions:</span><span class="sxs-lookup"><span data-stu-id="462c3-178">To create a 3.x project the instructions are the same, with these exceptions:</span></span>

1. <span data-ttu-id="462c3-179">Create a .NET Core console app.</span><span class="sxs-lookup"><span data-stu-id="462c3-179">Create a .NET Core console app.</span></span> <span data-ttu-id="462c3-180">In the Visual Studio **New Project** dialog, select  **.NET Core > Console App (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="462c3-180">In the Visual Studio **New Project** dialog, select  **.NET Core > Console App (.NET Core)**.</span></span> <span data-ttu-id="462c3-181">The project file specifies that `TargetFramework` is `netcoreapp2.0`.</span><span class="sxs-lookup"><span data-stu-id="462c3-181">The project file specifies that `TargetFramework` is `netcoreapp2.0`.</span></span>

1. <span data-ttu-id="462c3-182">Choose the prerelease version 3.x of the following packages:</span><span class="sxs-lookup"><span data-stu-id="462c3-182">Choose the prerelease version 3.x of the following packages:</span></span>

  * `Microsoft.Azure.WebJobs.Extensions`
  * `Microsoft.Azure.WebJobs.Logging.ApplicationInsights`

1. <span data-ttu-id="462c3-183">Change `Main` method code to get the Storage connection string and the Application Insights instrumentation key from an *appsettings.json* file, using the .NET Core configuration framework.</span><span class="sxs-lookup"><span data-stu-id="462c3-183">Change `Main` method code to get the Storage connection string and the Application Insights instrumentation key from an *appsettings.json* file, using the .NET Core configuration framework.</span></span>  <span data-ttu-id="462c3-184">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="462c3-184">Here's an example:</span></span>

   ```cs
   static void Main(string[] args)
   {
       var builder = new ConfigurationBuilder()
           .SetBasePath(Directory.GetCurrentDirectory())
           .AddJsonFile("appsettings.json");

       var appSettingsConfig = builder.Build();

       using (var loggerFactory = new LoggerFactory())
       {
           var config = new JobHostConfiguration();

           config.DashboardConnectionString = "";
           config.StorageConnectionString = 
               appSettingsConfig.GetConnectionString("AzureWebJobsStorage");
           var instrumentationKey =
               appSettingsConfig["APPINSIGHTS_INSTRUMENTATIONKEY"];

           config.LoggerFactory = loggerFactory
               .AddApplicationInsights(instrumentationKey, null)
               .AddConsole();

           config.UseTimers();
           config.UseDurableTask(new DurableTaskExtension
           {
               HubName = "MyTaskHub",
           });
           var host = new JobHost(config);
           host.RunAndBlock();
       }
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="462c3-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="462c3-185">Next steps</span></span>

<span data-ttu-id="462c3-186">To learn more about the WebJobs SDK, see [How to use the WebJobs SDK](../app-service/webjobs-sdk-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="462c3-186">To learn more about the WebJobs SDK, see [How to use the WebJobs SDK](../app-service/webjobs-sdk-how-to.md).</span></span>

