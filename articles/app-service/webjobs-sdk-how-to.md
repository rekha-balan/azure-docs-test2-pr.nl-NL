---
title: How to use the Azure WebJobs SDK
description: Learn more about how to write code for the WebJobs SDK. Create  event-driven background processing jobs that access data in Azure services and third-party services.
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
ms.openlocfilehash: 3e06dc82baed4043ce490769aa0ec84ab3de8c24
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856909"
---
# <a name="how-to-use-the-azure-webjobs-sdk-for-event-driven-background-processing"></a><span data-ttu-id="5befe-104">How to use the Azure WebJobs SDK for event-driven background processing</span><span class="sxs-lookup"><span data-stu-id="5befe-104">How to use the Azure WebJobs SDK for event-driven background processing</span></span>

<span data-ttu-id="5befe-105">This article provides guidance on how to write code for [the Azure WebJobs SDK](webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5befe-105">This article provides guidance on how to write code for [the Azure WebJobs SDK](webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="5befe-106">The documentation applies to versions 2.x and 3.x except where noted otherwise.</span><span class="sxs-lookup"><span data-stu-id="5befe-106">The documentation applies to versions 2.x and 3.x except where noted otherwise.</span></span> <span data-ttu-id="5befe-107">The main change introduced by 3.x is the use of .NET Core instead of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5befe-107">The main change introduced by 3.x is the use of .NET Core instead of .NET Framework.</span></span>

>[!NOTE]
> <span data-ttu-id="5befe-108">[Azure Functions](../azure-functions/functions-overview.md) is built on the WebJobs SDK, and this article links to Azure Functions documentation for some topics.</span><span class="sxs-lookup"><span data-stu-id="5befe-108">[Azure Functions](../azure-functions/functions-overview.md) is built on the WebJobs SDK, and this article links to Azure Functions documentation for some topics.</span></span> <span data-ttu-id="5befe-109">Note the following differences between Functions and the WebJobs SDK:</span><span class="sxs-lookup"><span data-stu-id="5befe-109">Note the following differences between Functions and the WebJobs SDK:</span></span>
> * <span data-ttu-id="5befe-110">Azure Functions version 1.x corresponds to WebJobs SDK version 2.x, and Azure Functions 2.x corresponds to WebJobs SDK 3.x.</span><span class="sxs-lookup"><span data-stu-id="5befe-110">Azure Functions version 1.x corresponds to WebJobs SDK version 2.x, and Azure Functions 2.x corresponds to WebJobs SDK 3.x.</span></span> <span data-ttu-id="5befe-111">Source code repositories follow the WebJobs SDK numbering, and many have v2.x branches, with the master branch currently having 3.x code.</span><span class="sxs-lookup"><span data-stu-id="5befe-111">Source code repositories follow the WebJobs SDK numbering, and many have v2.x branches, with the master branch currently having 3.x code.</span></span>
> * <span data-ttu-id="5befe-112">Sample code for Azure Functions C# class libraries is like WebJobs SDK code except you don't need a `FunctionName` attribute in a WebJobs SDK project.</span><span class="sxs-lookup"><span data-stu-id="5befe-112">Sample code for Azure Functions C# class libraries is like WebJobs SDK code except you don't need a `FunctionName` attribute in a WebJobs SDK project.</span></span>
> * <span data-ttu-id="5befe-113">Some binding types are only supported in Functions, such as HTTP, webhook, and Event Grid (which is based on HTTP).</span><span class="sxs-lookup"><span data-stu-id="5befe-113">Some binding types are only supported in Functions, such as HTTP, webhook, and Event Grid (which is based on HTTP).</span></span> 
> 
> <span data-ttu-id="5befe-114">For more information, see [Compare the WebJobs SDK and Azure Functions](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md#compare-functions-and-webjobs).</span><span class="sxs-lookup"><span data-stu-id="5befe-114">For more information, see [Compare the WebJobs SDK and Azure Functions](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md#compare-functions-and-webjobs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5befe-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5befe-115">Prerequisites</span></span>

<span data-ttu-id="5befe-116">This article assumes you have read [Get started with the WebJobs SDK](webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5befe-116">This article assumes you have read [Get started with the WebJobs SDK](webjobs-sdk-get-started.md).</span></span>

## <a name="jobhost"></a><span data-ttu-id="5befe-117">JobHost</span><span class="sxs-lookup"><span data-stu-id="5befe-117">JobHost</span></span>

<span data-ttu-id="5befe-118">The `JobHost` object is the runtime container for functions: it listens for triggers and calls functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-118">The `JobHost` object is the runtime container for functions: it listens for triggers and calls functions.</span></span> <span data-ttu-id="5befe-119">You create the `JobHost` in your code and write code to customize its behavior.</span><span class="sxs-lookup"><span data-stu-id="5befe-119">You create the `JobHost` in your code and write code to customize its behavior.</span></span>

<span data-ttu-id="5befe-120">This is a key difference between using the WebJobs SDK directly and using it indirectly by using Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-120">This is a key difference between using the WebJobs SDK directly and using it indirectly by using Azure Functions.</span></span> <span data-ttu-id="5befe-121">In Azure Functions, the service controls the `JobHost`, and you can't customize it by writing code.</span><span class="sxs-lookup"><span data-stu-id="5befe-121">In Azure Functions, the service controls the `JobHost`, and you can't customize it by writing code.</span></span> <span data-ttu-id="5befe-122">Azure Functions lets you customize host behavior through settings in the *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="5befe-122">Azure Functions lets you customize host behavior through settings in the *host.json* file.</span></span> <span data-ttu-id="5befe-123">Those settings are strings, not code, which limits the kinds of customizations you can do.</span><span class="sxs-lookup"><span data-stu-id="5befe-123">Those settings are strings, not code, which limits the kinds of customizations you can do.</span></span>

### <a name="jobhost-connection-strings"></a><span data-ttu-id="5befe-124">JobHost connection strings</span><span class="sxs-lookup"><span data-stu-id="5befe-124">JobHost connection strings</span></span>

<span data-ttu-id="5befe-125">The WebJobs SDK looks for Storage and Service Bus connection strings in  *local.settings.json* when you run locally, or in the WebJob's environment when you run in Azure.</span><span class="sxs-lookup"><span data-stu-id="5befe-125">The WebJobs SDK looks for Storage and Service Bus connection strings in  *local.settings.json* when you run locally, or in the WebJob's environment when you run in Azure.</span></span> <span data-ttu-id="5befe-126">If you want to use your own names for these connection strings, or store them elsewhere, you can set them in code, as shown here:</span><span class="sxs-lookup"><span data-stu-id="5befe-126">If you want to use your own names for these connection strings, or store them elsewhere, you can set them in code, as shown here:</span></span>

```cs
static void Main(string[] args)
{
    var _storageConn = ConfigurationManager
        .ConnectionStrings["MyStorageConnection"].ConnectionString;

    var _dashboardConn = ConfigurationManager
        .ConnectionStrings["MyDashboardConnection"].ConnectionString;

    JobHostConfiguration config = new JobHostConfiguration();
    config.StorageConnectionString = _storageConn;
    config.DashboardConnectionString = _dashboardConn;
    JobHost host = new JobHost(config);
    host.RunAndBlock();
}
```

### <a name="jobhost-development-settings"></a><span data-ttu-id="5befe-127">JobHost development settings</span><span class="sxs-lookup"><span data-stu-id="5befe-127">JobHost development settings</span></span>

<span data-ttu-id="5befe-128">The `JobHostConfiguration` class has a `UseDevelopmentSettings` method that you can call to make local development more efficient.</span><span class="sxs-lookup"><span data-stu-id="5befe-128">The `JobHostConfiguration` class has a `UseDevelopmentSettings` method that you can call to make local development more efficient.</span></span> <span data-ttu-id="5befe-129">Here are some of the settings that this method changes:</span><span class="sxs-lookup"><span data-stu-id="5befe-129">Here are some of the settings that this method changes:</span></span>

| <span data-ttu-id="5befe-130">Property</span><span class="sxs-lookup"><span data-stu-id="5befe-130">Property</span></span> | <span data-ttu-id="5befe-131">Development setting</span><span class="sxs-lookup"><span data-stu-id="5befe-131">Development setting</span></span> |
| ------------- | ------------- |
| `Tracing.ConsoleLevel` | <span data-ttu-id="5befe-132">`TraceLevel.Verbose` to maximize log output.</span><span class="sxs-lookup"><span data-stu-id="5befe-132">`TraceLevel.Verbose` to maximize log output.</span></span> |
| `Queues.MaxPollingInterval`  | <span data-ttu-id="5befe-133">A low value to ensure queue methods are triggered immediately.</span><span class="sxs-lookup"><span data-stu-id="5befe-133">A low value to ensure queue methods are triggered immediately.</span></span>  |
| `Singleton.ListenerLockPeriod` | <span data-ttu-id="5befe-134">15 seconds to aid in rapid iterative development.</span><span class="sxs-lookup"><span data-stu-id="5befe-134">15 seconds to aid in rapid iterative development.</span></span> |

<span data-ttu-id="5befe-135">The following example shows how to use development settings.</span><span class="sxs-lookup"><span data-stu-id="5befe-135">The following example shows how to use development settings.</span></span> <span data-ttu-id="5befe-136">To make `config.IsDevelopment` return `true` when running locally, set a local environment variable named `AzureWebJobsEnv` with value `Development`.</span><span class="sxs-lookup"><span data-stu-id="5befe-136">To make `config.IsDevelopment` return `true` when running locally, set a local environment variable named `AzureWebJobsEnv` with value `Development`.</span></span>

```cs
static void Main()
{
    config = new JobHostConfiguration();

    if (config.IsDevelopment)
    {
        config.UseDevelopmentSettings();
    }

    var host = new JobHost(config);
    host.RunAndBlock();
}
```

### <a name="jobhost-servicepointmanager-settings"></a><span data-ttu-id="5befe-137">JobHost ServicePointManager settings</span><span class="sxs-lookup"><span data-stu-id="5befe-137">JobHost ServicePointManager settings</span></span>

<span data-ttu-id="5befe-138">The .NET Framework contains an API called [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) that controls the number of concurrent connections to a host.</span><span class="sxs-lookup"><span data-stu-id="5befe-138">The .NET Framework contains an API called [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) that controls the number of concurrent connections to a host.</span></span> <span data-ttu-id="5befe-139">We recommend that you increase this value from the default of 2 before starting your WebJobs host.</span><span class="sxs-lookup"><span data-stu-id="5befe-139">We recommend that you increase this value from the default of 2 before starting your WebJobs host.</span></span>

<span data-ttu-id="5befe-140">All outgoing HTTP requests that you make from a function by using `HttpClient` flow through the `ServicePointManager`.</span><span class="sxs-lookup"><span data-stu-id="5befe-140">All outgoing HTTP requests that you make from a function by using `HttpClient` flow through the `ServicePointManager`.</span></span> <span data-ttu-id="5befe-141">Once you hit the `DefaultConnectionLimit`, the `ServicePointManager` starts queueing requests before sending them.</span><span class="sxs-lookup"><span data-stu-id="5befe-141">Once you hit the `DefaultConnectionLimit`, the `ServicePointManager` starts queueing requests before sending them.</span></span> <span data-ttu-id="5befe-142">Suppose your `DefaultConnectionLimit` is set to 2 and your code makes 1,000 HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="5befe-142">Suppose your `DefaultConnectionLimit` is set to 2 and your code makes 1,000 HTTP requests.</span></span> <span data-ttu-id="5befe-143">Initially, only 2 requests are actually allowed through to the OS.</span><span class="sxs-lookup"><span data-stu-id="5befe-143">Initially, only 2 requests are actually allowed through to the OS.</span></span> <span data-ttu-id="5befe-144">The other 998 are queued until there’s room for them.</span><span class="sxs-lookup"><span data-stu-id="5befe-144">The other 998 are queued until there’s room for them.</span></span> <span data-ttu-id="5befe-145">That means your `HttpClient` may time out, because it *thinks* it’s made the request, but the request was never sent by the OS to the destination server.</span><span class="sxs-lookup"><span data-stu-id="5befe-145">That means your `HttpClient` may time out, because it *thinks* it’s made the request, but the request was never sent by the OS to the destination server.</span></span> <span data-ttu-id="5befe-146">So you might see behavior that doesn't seem to make sense: your local `HttpClient` is taking 10 seconds to complete a request, but your service is returning every request in 200 ms.</span><span class="sxs-lookup"><span data-stu-id="5befe-146">So you might see behavior that doesn't seem to make sense: your local `HttpClient` is taking 10 seconds to complete a request, but your service is returning every request in 200 ms.</span></span> 

<span data-ttu-id="5befe-147">The default value for ASP.NET applications is `Int32.MaxValue`, and that's likely to work well for WebJobs running in a Basic or higher App Service plan.</span><span class="sxs-lookup"><span data-stu-id="5befe-147">The default value for ASP.NET applications is `Int32.MaxValue`, and that's likely to work well for WebJobs running in a Basic or higher App Service plan.</span></span> <span data-ttu-id="5befe-148">WebJobs typically need the Always On setting, and that's supported only by Basic and higher App Service plans.</span><span class="sxs-lookup"><span data-stu-id="5befe-148">WebJobs typically need the Always On setting, and that's supported only by Basic and higher App Service plans.</span></span> 

<span data-ttu-id="5befe-149">If your WebJob is running in a Free or Shared App Service Plan, your application is restricted by the App Service sandbox, which currently has a [connection limit of 300](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#per-sandbox-per-appper-site-numerical-limits).</span><span class="sxs-lookup"><span data-stu-id="5befe-149">If your WebJob is running in a Free or Shared App Service Plan, your application is restricted by the App Service sandbox, which currently has a [connection limit of 300](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#per-sandbox-per-appper-site-numerical-limits).</span></span> <span data-ttu-id="5befe-150">With an unbound connection limit in `ServicePointManager`, it's more likely that the sandbox connection threshold will be reached and the site shut down.</span><span class="sxs-lookup"><span data-stu-id="5befe-150">With an unbound connection limit in `ServicePointManager`, it's more likely that the sandbox connection threshold will be reached and the site shut down.</span></span> <span data-ttu-id="5befe-151">In that case, setting `DefaultConnectionLimit` to something lower, like 50 or 100, can prevent this from happening and still allow for sufficient throughput.</span><span class="sxs-lookup"><span data-stu-id="5befe-151">In that case, setting `DefaultConnectionLimit` to something lower, like 50 or 100, can prevent this from happening and still allow for sufficient throughput.</span></span>

<span data-ttu-id="5befe-152">The setting must be configured before any HTTP requests are made.</span><span class="sxs-lookup"><span data-stu-id="5befe-152">The setting must be configured before any HTTP requests are made.</span></span> <span data-ttu-id="5befe-153">For this reason, the WebJobs host shouldn't try to adjust the setting automatically; there may be HTTP requests that occur before the host starts and this can lead to unexpected behavior.</span><span class="sxs-lookup"><span data-stu-id="5befe-153">For this reason, the WebJobs host shouldn't try to adjust the setting automatically; there may be HTTP requests that occur before the host starts and this can lead to unexpected behavior.</span></span> <span data-ttu-id="5befe-154">The best approach is to set the value immediately in your `Main` method before initializing the `JobHost`, as shown in the following example</span><span class="sxs-lookup"><span data-stu-id="5befe-154">The best approach is to set the value immediately in your `Main` method before initializing the `JobHost`, as shown in the following example</span></span>

```csharp
static void Main(string[] args)
{
    // Set this immediately so that it is used by all requests.
    ServicePointManager.DefaultConnectionLimit = Int32.MaxValue;

    var host = new JobHost();
    host.RunAndBlock();
}
```

## <a name="triggers"></a><span data-ttu-id="5befe-155">Triggers</span><span class="sxs-lookup"><span data-stu-id="5befe-155">Triggers</span></span>

<span data-ttu-id="5befe-156">Functions must be public methods and must have one trigger attribute or the [NoAutomaticTrigger](#manual-trigger) attribute.</span><span class="sxs-lookup"><span data-stu-id="5befe-156">Functions must be public methods and must have one trigger attribute or the [NoAutomaticTrigger](#manual-trigger) attribute.</span></span>

### <a name="automatic-trigger"></a><span data-ttu-id="5befe-157">Automatic trigger</span><span class="sxs-lookup"><span data-stu-id="5befe-157">Automatic trigger</span></span>

<span data-ttu-id="5befe-158">Automatic triggers call a function in response to an event.</span><span class="sxs-lookup"><span data-stu-id="5befe-158">Automatic triggers call a function in response to an event.</span></span> <span data-ttu-id="5befe-159">For an example, see the queue trigger in the [Get started article](webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5befe-159">For an example, see the queue trigger in the [Get started article](webjobs-sdk-get-started.md).</span></span>

### <a name="manual-trigger"></a><span data-ttu-id="5befe-160">Manual trigger</span><span class="sxs-lookup"><span data-stu-id="5befe-160">Manual trigger</span></span>

<span data-ttu-id="5befe-161">To trigger a function manually, use the `NoAutomaticTrigger` attribute, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5befe-161">To trigger a function manually, use the `NoAutomaticTrigger` attribute, as shown in the following example:</span></span>

```cs
static void Main(string[] args)
{
    JobHost host = new JobHost();
    host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
}
```

```cs
[NoAutomaticTrigger]
public static void CreateQueueMessage(
    TextWriter logger,
    string value,
    [Queue("outputqueue")] out string message)
{
    message = value;
    logger.WriteLine("Creating queue message: ", message);
}
```

## <a name="input-and-output-bindings"></a><span data-ttu-id="5befe-162">Input and output bindings</span><span class="sxs-lookup"><span data-stu-id="5befe-162">Input and output bindings</span></span>

<span data-ttu-id="5befe-163">Input bindings provide a declarative way to make data from Azure or third-party services available to your code.</span><span class="sxs-lookup"><span data-stu-id="5befe-163">Input bindings provide a declarative way to make data from Azure or third-party services available to your code.</span></span> <span data-ttu-id="5befe-164">Output bindings provide a way to update data.</span><span class="sxs-lookup"><span data-stu-id="5befe-164">Output bindings provide a way to update data.</span></span> <span data-ttu-id="5befe-165">The [Get started article](webjobs-sdk-get-started.md) shows an example of each.</span><span class="sxs-lookup"><span data-stu-id="5befe-165">The [Get started article](webjobs-sdk-get-started.md) shows an example of each.</span></span>

<span data-ttu-id="5befe-166">You can use a method return value for an output binding, by applying the attribute to the method return value.</span><span class="sxs-lookup"><span data-stu-id="5befe-166">You can use a method return value for an output binding, by applying the attribute to the method return value.</span></span> <span data-ttu-id="5befe-167">See the example in the Azure Functions [Triggers and bindings](../azure-functions/functions-triggers-bindings.md#using-the-function-return-value) article.</span><span class="sxs-lookup"><span data-stu-id="5befe-167">See the example in the Azure Functions [Triggers and bindings](../azure-functions/functions-triggers-bindings.md#using-the-function-return-value) article.</span></span>

## <a name="binding-types"></a><span data-ttu-id="5befe-168">Binding types</span><span class="sxs-lookup"><span data-stu-id="5befe-168">Binding types</span></span>

<span data-ttu-id="5befe-169">The following trigger and binding types are included in the `Microsoft.Azure.WebJobs` package:</span><span class="sxs-lookup"><span data-stu-id="5befe-169">The following trigger and binding types are included in the `Microsoft.Azure.WebJobs` package:</span></span>

* <span data-ttu-id="5befe-170">Blob storage</span><span class="sxs-lookup"><span data-stu-id="5befe-170">Blob storage</span></span>
* <span data-ttu-id="5befe-171">Queue storage</span><span class="sxs-lookup"><span data-stu-id="5befe-171">Queue storage</span></span>
* <span data-ttu-id="5befe-172">Table storage</span><span class="sxs-lookup"><span data-stu-id="5befe-172">Table storage</span></span>

<span data-ttu-id="5befe-173">To use other trigger and binding types, install the NuGet package that contains them and call a `Use<binding>` method on the `JobHostConfiguration` object.</span><span class="sxs-lookup"><span data-stu-id="5befe-173">To use other trigger and binding types, install the NuGet package that contains them and call a `Use<binding>` method on the `JobHostConfiguration` object.</span></span> <span data-ttu-id="5befe-174">For example, if you want to use a Timer trigger, install `Microsoft.Azure.WebJobs.Extensions` and call `UseTimers` in the `Main` method, as in this example:</span><span class="sxs-lookup"><span data-stu-id="5befe-174">For example, if you want to use a Timer trigger, install `Microsoft.Azure.WebJobs.Extensions` and call `UseTimers` in the `Main` method, as in this example:</span></span>

```cs
static void Main()
{
    config = new JobHostConfiguration();
    config.UseTimers();
    var host = new JobHost(config);
    host.RunAndBlock();
}
```

<span data-ttu-id="5befe-175">You can find the package to install for a particular binding type in the **Packages** section of that binding type's [reference article](#binding-reference-information) for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-175">You can find the package to install for a particular binding type in the **Packages** section of that binding type's [reference article](#binding-reference-information) for Azure Functions.</span></span> <span data-ttu-id="5befe-176">An exception is the Files trigger and binding (for the local file system), which is not supported by Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-176">An exception is the Files trigger and binding (for the local file system), which is not supported by Azure Functions.</span></span> <span data-ttu-id="5befe-177">to use the Files binding, install `Microsoft.Azure.WebJobs.Extensions` and call `UseFiles`.</span><span class="sxs-lookup"><span data-stu-id="5befe-177">to use the Files binding, install `Microsoft.Azure.WebJobs.Extensions` and call `UseFiles`.</span></span>

### <a name="usecore"></a><span data-ttu-id="5befe-178">UseCore</span><span class="sxs-lookup"><span data-stu-id="5befe-178">UseCore</span></span>

<span data-ttu-id="5befe-179">The `Microsoft.Azure.WebJobs.Extensions` package mentioned earlier also provides a special binding type that you can register by calling the `UseCore` method.</span><span class="sxs-lookup"><span data-stu-id="5befe-179">The `Microsoft.Azure.WebJobs.Extensions` package mentioned earlier also provides a special binding type that you can register by calling the `UseCore` method.</span></span> <span data-ttu-id="5befe-180">This binding lets you define an [ExecutionContext](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Core/ExecutionContext.cs) parameter in your function signature.</span><span class="sxs-lookup"><span data-stu-id="5befe-180">This binding lets you define an [ExecutionContext](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Core/ExecutionContext.cs) parameter in your function signature.</span></span> <span data-ttu-id="5befe-181">The context object gives you access to the invocation ID, which you can use to correlate all logs produced by a given function invocation.</span><span class="sxs-lookup"><span data-stu-id="5befe-181">The context object gives you access to the invocation ID, which you can use to correlate all logs produced by a given function invocation.</span></span> <span data-ttu-id="5befe-182">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="5befe-182">Here's an example:</span></span>

```cs
class Program
{
    static void Main()
    {
        config = new JobHostConfiguration();
        config.UseCore();
        var host = new JobHost(config);
        host.RunAndBlock();
    }
}
public class Functions
{
    public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        ExecutionContext executionContext,
        ILogger logger)
    {
        logger.LogInformation($"{message}\n{executionContext.InvocationId}");
    }
}
```

## <a name="binding-configuration"></a><span data-ttu-id="5befe-183">Binding configuration</span><span class="sxs-lookup"><span data-stu-id="5befe-183">Binding configuration</span></span>

<span data-ttu-id="5befe-184">Many trigger and binding types let you configure their behavior by setting properties in a configuration object that you pass in to the `JobHost`.</span><span class="sxs-lookup"><span data-stu-id="5befe-184">Many trigger and binding types let you configure their behavior by setting properties in a configuration object that you pass in to the `JobHost`.</span></span>

### <a name="queue-trigger-configuration"></a><span data-ttu-id="5befe-185">Queue trigger configuration</span><span class="sxs-lookup"><span data-stu-id="5befe-185">Queue trigger configuration</span></span>

<span data-ttu-id="5befe-186">The settings you can configure for the Storage queue trigger are explained in the Azure Functions [host.json reference](../azure-functions/functions-host-json.md#queues).</span><span class="sxs-lookup"><span data-stu-id="5befe-186">The settings you can configure for the Storage queue trigger are explained in the Azure Functions [host.json reference](../azure-functions/functions-host-json.md#queues).</span></span> <span data-ttu-id="5befe-187">How to set them in a WebJobs SDK project is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5befe-187">How to set them in a WebJobs SDK project is shown in the following example:</span></span>

```cs
static void Main(string[] args)
{
    JobHostConfiguration config = new JobHostConfiguration();
    config.Queues.BatchSize = 8;
    config.Queues.NewBatchThreshold = 4;
    config.Queues.MaxDequeueCount = 4;
    config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
    JobHost host = new JobHost(config);
    host.RunAndBlock();
}
```

### <a name="configuration-for-other-bindings"></a><span data-ttu-id="5befe-188">Configuration for other bindings</span><span class="sxs-lookup"><span data-stu-id="5befe-188">Configuration for other bindings</span></span>

<span data-ttu-id="5befe-189">Some trigger and binding types define their own custom configuration type.</span><span class="sxs-lookup"><span data-stu-id="5befe-189">Some trigger and binding types define their own custom configuration type.</span></span> <span data-ttu-id="5befe-190">For example, the File trigger lets you specify the root path to monitor:</span><span class="sxs-lookup"><span data-stu-id="5befe-190">For example, the File trigger lets you specify the root path to monitor:</span></span>

```cs
static void Main()
{
    config = new JobHostConfiguration();
    var filesConfig = new FilesConfiguration
    {
        RootPath = @"c:\data\import"
    };
    config.UseFiles(filesConfig);
    var host = new JobHost(config);
    host.RunAndBlock();
}
```

## <a name="binding-expressions"></a><span data-ttu-id="5befe-191">Binding expressions</span><span class="sxs-lookup"><span data-stu-id="5befe-191">Binding expressions</span></span>

<span data-ttu-id="5befe-192">In attribute constructor parameters, you can use expressions that resolve to values from various sources.</span><span class="sxs-lookup"><span data-stu-id="5befe-192">In attribute constructor parameters, you can use expressions that resolve to values from various sources.</span></span> <span data-ttu-id="5befe-193">For example, in the following code, the path for the `BlobTrigger` attribute creates an expression named `filename`.</span><span class="sxs-lookup"><span data-stu-id="5befe-193">For example, in the following code, the path for the `BlobTrigger` attribute creates an expression named `filename`.</span></span> <span data-ttu-id="5befe-194">When used for the output binding, `filename` resolves to the name of the triggering blob.</span><span class="sxs-lookup"><span data-stu-id="5befe-194">When used for the output binding, `filename` resolves to the name of the triggering blob.</span></span>
 
```cs
public static void CreateThumbnail(
    [BlobTrigger("sample-images/{filename}")] Stream image,
    [Blob("sample-images-sm/{filename}", FileAccess.Write)] Stream imageSmall,
    string filename,
    ILogger logger)
{
    logger.Info($"Blob trigger processing: {filename}");
    // ...
}
```

<span data-ttu-id="5befe-195">For more information about binding expressions, see [Binding expressions and patterns](../azure-functions/functions-triggers-bindings.md#binding-expressions-and-patterns) in the Azure Functions documentation.</span><span class="sxs-lookup"><span data-stu-id="5befe-195">For more information about binding expressions, see [Binding expressions and patterns](../azure-functions/functions-triggers-bindings.md#binding-expressions-and-patterns) in the Azure Functions documentation.</span></span>

### <a name="custom-binding-expressions"></a><span data-ttu-id="5befe-196">Custom binding expressions</span><span class="sxs-lookup"><span data-stu-id="5befe-196">Custom binding expressions</span></span>

<span data-ttu-id="5befe-197">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span><span class="sxs-lookup"><span data-stu-id="5befe-197">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="5befe-198">For example, you might want to specify the queue name for the `QueueTrigger` attribute in a configuration file or environment variable.</span><span class="sxs-lookup"><span data-stu-id="5befe-198">For example, you might want to specify the queue name for the `QueueTrigger` attribute in a configuration file or environment variable.</span></span>

<span data-ttu-id="5befe-199">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` object.</span><span class="sxs-lookup"><span data-stu-id="5befe-199">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` object.</span></span> <span data-ttu-id="5befe-200">You include placeholders in trigger or binding attribute constructor parameters, and your `NameResolver` code provides the actual values to be used in place of those placeholders.</span><span class="sxs-lookup"><span data-stu-id="5befe-200">You include placeholders in trigger or binding attribute constructor parameters, and your `NameResolver` code provides the actual values to be used in place of those placeholders.</span></span> <span data-ttu-id="5befe-201">The placeholders are identified by surrounding them with percent (%) signs, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5befe-201">The placeholders are identified by surrounding them with percent (%) signs, as shown in the following example:</span></span>
 
```cs
public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
{
    Console.WriteLine(logMessage);
}
```

<span data-ttu-id="5befe-202">This code lets you use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span><span class="sxs-lookup"><span data-stu-id="5befe-202">This code lets you use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="5befe-203">Instead of a hard-coded queue name, you specify the name of an entry in the `appSettings` collection.</span><span class="sxs-lookup"><span data-stu-id="5befe-203">Instead of a hard-coded queue name, you specify the name of an entry in the `appSettings` collection.</span></span> 

<span data-ttu-id="5befe-204">There is a default NameResolver that takes effect if you don't provide a custom one.</span><span class="sxs-lookup"><span data-stu-id="5befe-204">There is a default NameResolver that takes effect if you don't provide a custom one.</span></span> <span data-ttu-id="5befe-205">The default gets values from app settings or environment variables.</span><span class="sxs-lookup"><span data-stu-id="5befe-205">The default gets values from app settings or environment variables.</span></span>

<span data-ttu-id="5befe-206">Your `NameResolver` class gets the queue name from `appSettings` as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5befe-206">Your `NameResolver` class gets the queue name from `appSettings` as shown in the following example:</span></span>

```cs
public class CustomNameResolver : INameResolver
{
    public string Resolve(string name)
    {
        return ConfigurationManager.AppSettings[name].ToString();
    }
}
```

<span data-ttu-id="5befe-207">Pass your `NameResolver` class in to the `JobHost` object as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5befe-207">Pass your `NameResolver` class in to the `JobHost` object as shown in the following example:</span></span>

```cs
 static void Main(string[] args)
{
    JobHostConfiguration config = new JobHostConfiguration();
    config.NameResolver = new CustomNameResolver();
    JobHost host = new JobHost(config);
    host.RunAndBlock();
}
```

<span data-ttu-id="5befe-208">Azure Functions implements `INameResolver` to get values from app settings, as shown in the example.</span><span class="sxs-lookup"><span data-stu-id="5befe-208">Azure Functions implements `INameResolver` to get values from app settings, as shown in the example.</span></span> <span data-ttu-id="5befe-209">When you use the WebJobs SDK directly, you can write a custom implementation that gets placeholder replacement values from whatever source you prefer.</span><span class="sxs-lookup"><span data-stu-id="5befe-209">When you use the WebJobs SDK directly, you can write a custom implementation that gets placeholder replacement values from whatever source you prefer.</span></span> 

## <a name="binding-at-runtime"></a><span data-ttu-id="5befe-210">Binding at runtime</span><span class="sxs-lookup"><span data-stu-id="5befe-210">Binding at runtime</span></span>

<span data-ttu-id="5befe-211">If you need to do some work in your function before using a binding attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="5befe-211">If you need to do some work in your function before using a binding attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="5befe-212">The following example takes an input queue message and creates a new message with the same content in an output queue.</span><span class="sxs-lookup"><span data-stu-id="5befe-212">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="5befe-213">The output queue name is set by code in the body of the function.</span><span class="sxs-lookup"><span data-stu-id="5befe-213">The output queue name is set by code in the body of the function.</span></span>

```cs
public static void CreateQueueMessage(
    [QueueTrigger("inputqueue")] string queueMessage,
    IBinder binder)
{
    string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
    QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
    CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
    outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
}
```

<span data-ttu-id="5befe-214">For more information, see [Binding at runtime](../azure-functions/functions-dotnet-class-library.md#binding-at-runtime) in the Azure Functions documentation.</span><span class="sxs-lookup"><span data-stu-id="5befe-214">For more information, see [Binding at runtime](../azure-functions/functions-dotnet-class-library.md#binding-at-runtime) in the Azure Functions documentation.</span></span>

## <a name="binding-reference-information"></a><span data-ttu-id="5befe-215">Binding reference information</span><span class="sxs-lookup"><span data-stu-id="5befe-215">Binding reference information</span></span>

<span data-ttu-id="5befe-216">Reference information about each binding type is provided in the Azure Functions documentation.</span><span class="sxs-lookup"><span data-stu-id="5befe-216">Reference information about each binding type is provided in the Azure Functions documentation.</span></span> <span data-ttu-id="5befe-217">Using Storage queue as an example, you'll find the following information in each binding reference article:</span><span class="sxs-lookup"><span data-stu-id="5befe-217">Using Storage queue as an example, you'll find the following information in each binding reference article:</span></span>

* <span data-ttu-id="5befe-218">[Packages](../azure-functions/functions-bindings-storage-queue.md#packages---functions-1x) - What package to install in order to include support for the binding in a WebJobs SDK project.</span><span class="sxs-lookup"><span data-stu-id="5befe-218">[Packages](../azure-functions/functions-bindings-storage-queue.md#packages---functions-1x) - What package to install in order to include support for the binding in a WebJobs SDK project.</span></span>
* <span data-ttu-id="5befe-219">[Examples](../azure-functions/functions-bindings-storage-queue.md#trigger---example) - The C# class library example applies to the WebJobs SDK; just omit the `FunctionName` attribute.</span><span class="sxs-lookup"><span data-stu-id="5befe-219">[Examples](../azure-functions/functions-bindings-storage-queue.md#trigger---example) - The C# class library example applies to the WebJobs SDK; just omit the `FunctionName` attribute.</span></span>
* <span data-ttu-id="5befe-220">[Attributes](../azure-functions/functions-bindings-storage-queue.md#trigger---attributes) - The attributes to use for the binding type.</span><span class="sxs-lookup"><span data-stu-id="5befe-220">[Attributes](../azure-functions/functions-bindings-storage-queue.md#trigger---attributes) - The attributes to use for the binding type.</span></span>
* <span data-ttu-id="5befe-221">[Configuration](../azure-functions/functions-bindings-storage-queue.md#trigger---configuration) - Explanations of the attribute properties and constructor parameters.</span><span class="sxs-lookup"><span data-stu-id="5befe-221">[Configuration](../azure-functions/functions-bindings-storage-queue.md#trigger---configuration) - Explanations of the attribute properties and constructor parameters.</span></span>
* <span data-ttu-id="5befe-222">[Usage](../azure-functions/functions-bindings-storage-queue.md#trigger---usage) - What types you can bind to and information about how the binding works.</span><span class="sxs-lookup"><span data-stu-id="5befe-222">[Usage](../azure-functions/functions-bindings-storage-queue.md#trigger---usage) - What types you can bind to and information about how the binding works.</span></span> <span data-ttu-id="5befe-223">For example: polling algorithm, poison queue processing.</span><span class="sxs-lookup"><span data-stu-id="5befe-223">For example: polling algorithm, poison queue processing.</span></span>
  
<span data-ttu-id="5befe-224">For a list of binding reference articles, see **Supported bindings** in the [Triggers and bindings](../azure-functions/functions-triggers-bindings.md#supported-bindings) article for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-224">For a list of binding reference articles, see **Supported bindings** in the [Triggers and bindings](../azure-functions/functions-triggers-bindings.md#supported-bindings) article for Azure Functions.</span></span> <span data-ttu-id="5befe-225">In that list, the HTTP, webhook, and Event Grid bindings are supported only by Azure Functions, not by the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="5befe-225">In that list, the HTTP, webhook, and Event Grid bindings are supported only by Azure Functions, not by the WebJobs SDK.</span></span>

## <a name="disable-attribute"></a><span data-ttu-id="5befe-226">Disable attribute</span><span class="sxs-lookup"><span data-stu-id="5befe-226">Disable attribute</span></span> 

<span data-ttu-id="5befe-227">The [Disable](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/DisableAttribute.cs) attribute lets you control whether a function can be triggered.</span><span class="sxs-lookup"><span data-stu-id="5befe-227">The [Disable](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/DisableAttribute.cs) attribute lets you control whether a function can be triggered.</span></span> 

<span data-ttu-id="5befe-228">In the following example, if the app setting `Disable_TestJob` has a value of "1" or "True" (case insensitive), the function will not run.</span><span class="sxs-lookup"><span data-stu-id="5befe-228">In the following example, if the app setting `Disable_TestJob` has a value of "1" or "True" (case insensitive), the function will not run.</span></span> <span data-ttu-id="5befe-229">In that case, the runtime creates a log message *Function 'Functions.TestJob' is disabled*.</span><span class="sxs-lookup"><span data-stu-id="5befe-229">In that case, the runtime creates a log message *Function 'Functions.TestJob' is disabled*.</span></span>

```cs
[Disable("Disable_TestJob")]
public static void TestJob([QueueTrigger("testqueue2")] string message)
{
    Console.WriteLine("Function with Disable attribute executed!");
}
```

<span data-ttu-id="5befe-230">When you change app setting values in the Azure portal, it causes the WebJob to be restarted, picking up the new setting.</span><span class="sxs-lookup"><span data-stu-id="5befe-230">When you change app setting values in the Azure portal, it causes the WebJob to be restarted, picking up the new setting.</span></span>

<span data-ttu-id="5befe-231">The attribute can be declared at the parameter, method, or class level.</span><span class="sxs-lookup"><span data-stu-id="5befe-231">The attribute can be declared at the parameter, method, or class level.</span></span> <span data-ttu-id="5befe-232">The setting name can also contain binding expressions.</span><span class="sxs-lookup"><span data-stu-id="5befe-232">The setting name can also contain binding expressions.</span></span>

## <a name="timeout-attribute"></a><span data-ttu-id="5befe-233">Timeout attribute</span><span class="sxs-lookup"><span data-stu-id="5befe-233">Timeout attribute</span></span>

<span data-ttu-id="5befe-234">The [Timeout](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TimeoutAttribute.cs) attribute causes a function to be canceled if it doesn't complete within a specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="5befe-234">The [Timeout](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TimeoutAttribute.cs) attribute causes a function to be canceled if it doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="5befe-235">In the following example, the function would run for one day without the timeout.</span><span class="sxs-lookup"><span data-stu-id="5befe-235">In the following example, the function would run for one day without the timeout.</span></span> <span data-ttu-id="5befe-236">With the timeout, the function is canceled after 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="5befe-236">With the timeout, the function is canceled after 15 seconds.</span></span>

```cs
[Timeout("00:00:15")]
public static async Task TimeoutJob(
    [QueueTrigger("testqueue2")] string message,
    CancellationToken token,
    TextWriter log)
{
    await log.WriteLineAsync("Job starting");
    await Task.Delay(TimeSpan.FromDays(1), token);
    await log.WriteLineAsync("Job completed");
}
```

<span data-ttu-id="5befe-237">You can apply the Timeout attribute at class or method level, and you can specify a global timeout by using `JobHostConfiguration.FunctionTimeout`.</span><span class="sxs-lookup"><span data-stu-id="5befe-237">You can apply the Timeout attribute at class or method level, and you can specify a global timeout by using `JobHostConfiguration.FunctionTimeout`.</span></span> <span data-ttu-id="5befe-238">Class or method level timeouts override the global timeout.</span><span class="sxs-lookup"><span data-stu-id="5befe-238">Class or method level timeouts override the global timeout.</span></span>

## <a name="singleton-attribute"></a><span data-ttu-id="5befe-239">Singleton attribute</span><span class="sxs-lookup"><span data-stu-id="5befe-239">Singleton attribute</span></span>

<span data-ttu-id="5befe-240">Use the [Singleton](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/SingletonAttribute.cs) attribute to ensure that only one instance of a function runs even when there are multiple instances of the host web app.</span><span class="sxs-lookup"><span data-stu-id="5befe-240">Use the [Singleton](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/SingletonAttribute.cs) attribute to ensure that only one instance of a function runs even when there are multiple instances of the host web app.</span></span> <span data-ttu-id="5befe-241">It does this by implementing [distributed locking](#viewing-lease-blobs).</span><span class="sxs-lookup"><span data-stu-id="5befe-241">It does this by implementing [distributed locking](#viewing-lease-blobs).</span></span>

<span data-ttu-id="5befe-242">In the following example, only a single instance of the `ProcessImage` function runs at any given time:</span><span class="sxs-lookup"><span data-stu-id="5befe-242">In the following example, only a single instance of the `ProcessImage` function runs at any given time:</span></span>

```cs
[Singleton]
public static async Task ProcessImage([BlobTrigger("images")] Stream image)
{
     // Process the image
}
```

### <a name="singletonmodelistener"></a><span data-ttu-id="5befe-243">SingletonMode.Listener</span><span class="sxs-lookup"><span data-stu-id="5befe-243">SingletonMode.Listener</span></span>

<span data-ttu-id="5befe-244">Some triggers have built-in support for concurrency management:</span><span class="sxs-lookup"><span data-stu-id="5befe-244">Some triggers have built-in support for concurrency management:</span></span>

* <span data-ttu-id="5befe-245">**QueueTrigger** - Set `JobHostConfiguration.Queues.BatchSize` to 1.</span><span class="sxs-lookup"><span data-stu-id="5befe-245">**QueueTrigger** - Set `JobHostConfiguration.Queues.BatchSize` to 1.</span></span>
* <span data-ttu-id="5befe-246">**ServiceBusTrigger** - Set `ServiceBusConfiguration.MessageOptions.MaxConcurrentCalls` to 1.</span><span class="sxs-lookup"><span data-stu-id="5befe-246">**ServiceBusTrigger** - Set `ServiceBusConfiguration.MessageOptions.MaxConcurrentCalls` to 1.</span></span>
* <span data-ttu-id="5befe-247">**FileTrigger** - Set `FileProcessor.MaxDegreeOfParallelism` to 1.</span><span class="sxs-lookup"><span data-stu-id="5befe-247">**FileTrigger** - Set `FileProcessor.MaxDegreeOfParallelism` to 1.</span></span>

<span data-ttu-id="5befe-248">You can use these settings to ensure that your function runs as a singleton on a single instance.</span><span class="sxs-lookup"><span data-stu-id="5befe-248">You can use these settings to ensure that your function runs as a singleton on a single instance.</span></span> <span data-ttu-id="5befe-249">To ensure only a single instance of the function is running when the web app scales out to multiple instances, apply a listener level Singleton lock on the function (`[Singleton(Mode = SingletonMode.Listener)]`).</span><span class="sxs-lookup"><span data-stu-id="5befe-249">To ensure only a single instance of the function is running when the web app scales out to multiple instances, apply a listener level Singleton lock on the function (`[Singleton(Mode = SingletonMode.Listener)]`).</span></span> <span data-ttu-id="5befe-250">Listener locks are acquired on startup of the JobHost.</span><span class="sxs-lookup"><span data-stu-id="5befe-250">Listener locks are acquired on startup of the JobHost.</span></span> <span data-ttu-id="5befe-251">If three scaled-out instances all start at the same time, only one of the instances acquires the lock and only one listener starts.</span><span class="sxs-lookup"><span data-stu-id="5befe-251">If three scaled-out instances all start at the same time, only one of the instances acquires the lock and only one listener starts.</span></span>

### <a name="scope-values"></a><span data-ttu-id="5befe-252">Scope Values</span><span class="sxs-lookup"><span data-stu-id="5befe-252">Scope Values</span></span>

<span data-ttu-id="5befe-253">You can specify a **scope expression/value** on the Singleton which will ensure that all executions of the function at that scope will be serialized.</span><span class="sxs-lookup"><span data-stu-id="5befe-253">You can specify a **scope expression/value** on the Singleton which will ensure that all executions of the function at that scope will be serialized.</span></span> <span data-ttu-id="5befe-254">Implementing more granular locking in this way can allow for some level of parallelism for your function, while serializing other invocations as dictated by your requirements.</span><span class="sxs-lookup"><span data-stu-id="5befe-254">Implementing more granular locking in this way can allow for some level of parallelism for your function, while serializing other invocations as dictated by your requirements.</span></span> <span data-ttu-id="5befe-255">For example, in the following example the scope expression binds to the `Region` value of the incoming message.</span><span class="sxs-lookup"><span data-stu-id="5befe-255">For example, in the following example the scope expression binds to the `Region` value of the incoming message.</span></span> <span data-ttu-id="5befe-256">If the queue contains 3 messages in Regions "East", "East", and "West" respectively, then the messages that have region "East" will be executed serially while the message with region "West" will be executed in parallel with those.</span><span class="sxs-lookup"><span data-stu-id="5befe-256">If the queue contains 3 messages in Regions "East", "East", and "West" respectively, then the messages that have region "East" will be executed serially while the message with region "West" will be executed in parallel with those.</span></span>

```csharp
[Singleton("{Region}")]
public static async Task ProcessWorkItem([QueueTrigger("workitems")] WorkItem workItem)
{
     // Process the work item
}

public class WorkItem
{
     public int ID { get; set; }
     public string Region { get; set; }
     public int Category { get; set; }
     public string Description { get; set; }
}
```

### <a name="singletonscopehost"></a><span data-ttu-id="5befe-257">SingletonScope.Host</span><span class="sxs-lookup"><span data-stu-id="5befe-257">SingletonScope.Host</span></span>

<span data-ttu-id="5befe-258">The default scope for a lock is `SingletonScope.Function` meaning the lock scope (the blob lease path) is tied to the fully qualified function name.</span><span class="sxs-lookup"><span data-stu-id="5befe-258">The default scope for a lock is `SingletonScope.Function` meaning the lock scope (the blob lease path) is tied to the fully qualified function name.</span></span> <span data-ttu-id="5befe-259">To lock across functions, specify `SingletonScope.Host` and use a scope ID name that is the same across all of the functions that you don't want to run simultaneously.</span><span class="sxs-lookup"><span data-stu-id="5befe-259">To lock across functions, specify `SingletonScope.Host` and use a scope ID name that is the same across all of the functions that you don't want to run simultaneously.</span></span> <span data-ttu-id="5befe-260">In the following example, only one instance of `AddItem` or `RemoveItem` runs at a time:</span><span class="sxs-lookup"><span data-stu-id="5befe-260">In the following example, only one instance of `AddItem` or `RemoveItem` runs at a time:</span></span>

```charp
[Singleton("ItemsLock", SingletonScope.Host)]
public static void AddItem([QueueTrigger("add-item")] string message)
{
     // Perform the add operation
}

[Singleton("ItemsLock", SingletonScope.Host)]
public static void RemoveItem([QueueTrigger("remove-item")] string message)
{
     // Perform the remove operation
}
```

### <a name="viewing-lease-blobs"></a><span data-ttu-id="5befe-261">Viewing lease blobs</span><span class="sxs-lookup"><span data-stu-id="5befe-261">Viewing lease blobs</span></span>

<span data-ttu-id="5befe-262">The WebJobs SDK uses [Azure blob leases](../storage/common/storage-concurrency.md#pessimistic-concurrency-for-blobs) under the covers to implement distributed locking.</span><span class="sxs-lookup"><span data-stu-id="5befe-262">The WebJobs SDK uses [Azure blob leases](../storage/common/storage-concurrency.md#pessimistic-concurrency-for-blobs) under the covers to implement distributed locking.</span></span> <span data-ttu-id="5befe-263">The lease blobs used by Singleton can be found in the `azure-webjobs-host` container in the `AzureWebJobsStorage` storage account under path "locks".</span><span class="sxs-lookup"><span data-stu-id="5befe-263">The lease blobs used by Singleton can be found in the `azure-webjobs-host` container in the `AzureWebJobsStorage` storage account under path "locks".</span></span> <span data-ttu-id="5befe-264">For example, the lease blob path for the first `ProcessImage` example shown earlier might be `locks/061851c758f04938a4426aa9ab3869c0/WebJobs.Functions.ProcessImage`.</span><span class="sxs-lookup"><span data-stu-id="5befe-264">For example, the lease blob path for the first `ProcessImage` example shown earlier might be `locks/061851c758f04938a4426aa9ab3869c0/WebJobs.Functions.ProcessImage`.</span></span> <span data-ttu-id="5befe-265">All paths include the JobHost ID, in this case 061851c758f04938a4426aa9ab3869c0.</span><span class="sxs-lookup"><span data-stu-id="5befe-265">All paths include the JobHost ID, in this case 061851c758f04938a4426aa9ab3869c0.</span></span>

## <a name="async-functions"></a><span data-ttu-id="5befe-266">Async functions</span><span class="sxs-lookup"><span data-stu-id="5befe-266">Async functions</span></span>

<span data-ttu-id="5befe-267">For information about how to code async functions, see the Azure Functions documentation on [Async Functions](../azure-functions/functions-dotnet-class-library.md#async).</span><span class="sxs-lookup"><span data-stu-id="5befe-267">For information about how to code async functions, see the Azure Functions documentation on [Async Functions](../azure-functions/functions-dotnet-class-library.md#async).</span></span>

## <a name="cancellation-tokens"></a><span data-ttu-id="5befe-268">Cancellation tokens</span><span class="sxs-lookup"><span data-stu-id="5befe-268">Cancellation tokens</span></span>

<span data-ttu-id="5befe-269">For information about how to handle cancellation tokens, see the Azure Functions documentation on [cancellation tokens and graceful shutdown](../azure-functions/functions-dotnet-class-library.md#cancellation-tokens).</span><span class="sxs-lookup"><span data-stu-id="5befe-269">For information about how to handle cancellation tokens, see the Azure Functions documentation on [cancellation tokens and graceful shutdown](../azure-functions/functions-dotnet-class-library.md#cancellation-tokens).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="5befe-270">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="5befe-270">Multiple instances</span></span>

<span data-ttu-id="5befe-271">If your web app runs on multiple instances, a continuous WebJob runs on each instance, listening for triggers and calling functions.</span><span class="sxs-lookup"><span data-stu-id="5befe-271">If your web app runs on multiple instances, a continuous WebJob runs on each instance, listening for triggers and calling functions.</span></span> <span data-ttu-id="5befe-272">The various trigger bindings are designed to efficiently share work collaboratively across instances, so that scaling out to more instances allows you to handle more load.</span><span class="sxs-lookup"><span data-stu-id="5befe-272">The various trigger bindings are designed to efficiently share work collaboratively across instances, so that scaling out to more instances allows you to handle more load.</span></span>

<span data-ttu-id="5befe-273">The queue and blob triggers automatically prevent a function from processing a queue message or blob more than once; functions do not have to be idempotent.</span><span class="sxs-lookup"><span data-stu-id="5befe-273">The queue and blob triggers automatically prevent a function from processing a queue message or blob more than once; functions do not have to be idempotent.</span></span>

<span data-ttu-id="5befe-274">The timer trigger automatically ensures that only one instance of the timer runs, so you don't get more than one function instance running at a given scheduled time.</span><span class="sxs-lookup"><span data-stu-id="5befe-274">The timer trigger automatically ensures that only one instance of the timer runs, so you don't get more than one function instance running at a given scheduled time.</span></span>

<span data-ttu-id="5befe-275">If you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the [Singleton](#singleton) attribute.</span><span class="sxs-lookup"><span data-stu-id="5befe-275">If you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the [Singleton](#singleton) attribute.</span></span>
    
## <a name="filters"></a><span data-ttu-id="5befe-276">Filters</span><span class="sxs-lookup"><span data-stu-id="5befe-276">Filters</span></span> 

<span data-ttu-id="5befe-277">Function Filters (preview) provide a way to customize the WebJobs execution pipeline with your own logic.</span><span class="sxs-lookup"><span data-stu-id="5befe-277">Function Filters (preview) provide a way to customize the WebJobs execution pipeline with your own logic.</span></span> <span data-ttu-id="5befe-278">Filters are similar to [ASP.NET Core Filters](https://docs.microsoft.com/aspnet/core/mvc/controllers/filters).</span><span class="sxs-lookup"><span data-stu-id="5befe-278">Filters are similar to [ASP.NET Core Filters](https://docs.microsoft.com/aspnet/core/mvc/controllers/filters).</span></span> <span data-ttu-id="5befe-279">They can be implemented as declarative attributes that are applied to your functions or classes.</span><span class="sxs-lookup"><span data-stu-id="5befe-279">They can be implemented as declarative attributes that are applied to your functions or classes.</span></span> <span data-ttu-id="5befe-280">For more information, see [Function Filters](https://github.com/Azure/azure-webjobs-sdk/wiki/Function-Filters).</span><span class="sxs-lookup"><span data-stu-id="5befe-280">For more information, see [Function Filters](https://github.com/Azure/azure-webjobs-sdk/wiki/Function-Filters).</span></span>

## <a name="logging-and-monitoring"></a><span data-ttu-id="5befe-281">Logging and monitoring</span><span class="sxs-lookup"><span data-stu-id="5befe-281">Logging and monitoring</span></span>

<span data-ttu-id="5befe-282">We recommend the logging framework that was developed for ASP.NET, and the [Get started](webjobs-sdk-get-started.md) article shows how to use it.</span><span class="sxs-lookup"><span data-stu-id="5befe-282">We recommend the logging framework that was developed for ASP.NET, and the [Get started](webjobs-sdk-get-started.md) article shows how to use it.</span></span> 

### <a name="log-filtering"></a><span data-ttu-id="5befe-283">Log filtering</span><span class="sxs-lookup"><span data-stu-id="5befe-283">Log filtering</span></span>

<span data-ttu-id="5befe-284">Every log created by an `ILogger` instance has an associated `Category` and `Level`.</span><span class="sxs-lookup"><span data-stu-id="5befe-284">Every log created by an `ILogger` instance has an associated `Category` and `Level`.</span></span> <span data-ttu-id="5befe-285">[LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel#Microsoft_Extensions_Logging_LogLevel) is an enumeration, and the integer code indicates relative importance:</span><span class="sxs-lookup"><span data-stu-id="5befe-285">[LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel#Microsoft_Extensions_Logging_LogLevel) is an enumeration, and the integer code indicates relative importance:</span></span>

|<span data-ttu-id="5befe-286">LogLevel</span><span class="sxs-lookup"><span data-stu-id="5befe-286">LogLevel</span></span>    |<span data-ttu-id="5befe-287">Code</span><span class="sxs-lookup"><span data-stu-id="5befe-287">Code</span></span>|
|------------|---|
|<span data-ttu-id="5befe-288">Trace</span><span class="sxs-lookup"><span data-stu-id="5befe-288">Trace</span></span>       | <span data-ttu-id="5befe-289">0</span><span class="sxs-lookup"><span data-stu-id="5befe-289">0</span></span> |
|<span data-ttu-id="5befe-290">Debug</span><span class="sxs-lookup"><span data-stu-id="5befe-290">Debug</span></span>       | <span data-ttu-id="5befe-291">1</span><span class="sxs-lookup"><span data-stu-id="5befe-291">1</span></span> |
|<span data-ttu-id="5befe-292">Information</span><span class="sxs-lookup"><span data-stu-id="5befe-292">Information</span></span> | <span data-ttu-id="5befe-293">2</span><span class="sxs-lookup"><span data-stu-id="5befe-293">2</span></span> |
|<span data-ttu-id="5befe-294">Warning</span><span class="sxs-lookup"><span data-stu-id="5befe-294">Warning</span></span>     | <span data-ttu-id="5befe-295">3</span><span class="sxs-lookup"><span data-stu-id="5befe-295">3</span></span> |
|<span data-ttu-id="5befe-296">Error</span><span class="sxs-lookup"><span data-stu-id="5befe-296">Error</span></span>       | <span data-ttu-id="5befe-297">4</span><span class="sxs-lookup"><span data-stu-id="5befe-297">4</span></span> |
|<span data-ttu-id="5befe-298">Critical</span><span class="sxs-lookup"><span data-stu-id="5befe-298">Critical</span></span>    | <span data-ttu-id="5befe-299">5</span><span class="sxs-lookup"><span data-stu-id="5befe-299">5</span></span> |
|<span data-ttu-id="5befe-300">None</span><span class="sxs-lookup"><span data-stu-id="5befe-300">None</span></span>        | <span data-ttu-id="5befe-301">6</span><span class="sxs-lookup"><span data-stu-id="5befe-301">6</span></span> |

<span data-ttu-id="5befe-302">Each category can be independently filtered to a particular [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel).</span><span class="sxs-lookup"><span data-stu-id="5befe-302">Each category can be independently filtered to a particular [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="5befe-303">For example, you might want to see all logs for blob trigger processing but only `Error` and higher for everything else.</span><span class="sxs-lookup"><span data-stu-id="5befe-303">For example, you might want to see all logs for blob trigger processing but only `Error` and higher for everything else.</span></span>

<span data-ttu-id="5befe-304">To make it easier to specify filtering rules, the WebJobs SDK provides the `LogCategoryFilter` that can be passed into many of the existing logging providers, including Application Insights and Console.</span><span class="sxs-lookup"><span data-stu-id="5befe-304">To make it easier to specify filtering rules, the WebJobs SDK provides the `LogCategoryFilter` that can be passed into many of the existing logging providers, including Application Insights and Console.</span></span>

<span data-ttu-id="5befe-305">The `LogCategoryFilter` has a `Default` property with an initial value of `Information`, meaning that any messages with levels of `Information`, `Warning`, `Error`, or `Critical` are logged, but any messages with levels of `Debug` or `Trace` are filtered away.</span><span class="sxs-lookup"><span data-stu-id="5befe-305">The `LogCategoryFilter` has a `Default` property with an initial value of `Information`, meaning that any messages with levels of `Information`, `Warning`, `Error`, or `Critical` are logged, but any messages with levels of `Debug` or `Trace` are filtered away.</span></span>

<span data-ttu-id="5befe-306">The `CategoryLevels` property allows you to specify log levels for specific categories so you can fine-tune the logging output.</span><span class="sxs-lookup"><span data-stu-id="5befe-306">The `CategoryLevels` property allows you to specify log levels for specific categories so you can fine-tune the logging output.</span></span> <span data-ttu-id="5befe-307">If no match is found within the `CategoryLevels` dictionary, the filter falls back to the `Default` value when deciding whether to filter the message.</span><span class="sxs-lookup"><span data-stu-id="5befe-307">If no match is found within the `CategoryLevels` dictionary, the filter falls back to the `Default` value when deciding whether to filter the message.</span></span>

<span data-ttu-id="5befe-308">The following example constructs a filter that by default filters all logs at the `Warning` level.</span><span class="sxs-lookup"><span data-stu-id="5befe-308">The following example constructs a filter that by default filters all logs at the `Warning` level.</span></span> <span data-ttu-id="5befe-309">Categories of `Function` or `Host.Results` are filtered at the `Error` level.</span><span class="sxs-lookup"><span data-stu-id="5befe-309">Categories of `Function` or `Host.Results` are filtered at the `Error` level.</span></span> <span data-ttu-id="5befe-310">The `LogCategoryFilter` compares the current category to all registered `CategoryLevels` and chooses the longest match.</span><span class="sxs-lookup"><span data-stu-id="5befe-310">The `LogCategoryFilter` compares the current category to all registered `CategoryLevels` and chooses the longest match.</span></span> <span data-ttu-id="5befe-311">This means that the `Debug` level registered for `Host.Triggers` will match `Host.Triggers.Queue` or `Host.Triggers.Blob`.</span><span class="sxs-lookup"><span data-stu-id="5befe-311">This means that the `Debug` level registered for `Host.Triggers` will match `Host.Triggers.Queue` or `Host.Triggers.Blob`.</span></span> <span data-ttu-id="5befe-312">This allows you to control broader categories without needing to add each one.</span><span class="sxs-lookup"><span data-stu-id="5befe-312">This allows you to control broader categories without needing to add each one.</span></span>

```csharp
var filter = new LogCategoryFilter();
filter.DefaultLevel = LogLevel.Warning;
filter.CategoryLevels[LogCategories.Function] = LogLevel.Error;
filter.CategoryLevels[LogCategories.Results] = LogLevel.Error;
filter.CategoryLevels["Host.Triggers"] = LogLevel.Debug;

config.LoggerFactory = new LoggerFactory()
    .AddApplicationInsights(instrumentationKey, filter.Filter)
    .AddConsole(filter.Filter);
```

### <a name="custom-telemetry-for-application-insights"></a><span data-ttu-id="5befe-313">Custom telemetry for Application Insights</span><span class="sxs-lookup"><span data-stu-id="5befe-313">Custom telemetry for Application Insights</span></span>

<span data-ttu-id="5befe-314">Internally, the `TelemetryClient` created by the Application Insights provider for the WebJobs SDK uses the [ServerTelemetryChannel](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/ServerTelemetryChannel/ServerTelemetryChannel.cs).</span><span class="sxs-lookup"><span data-stu-id="5befe-314">Internally, the `TelemetryClient` created by the Application Insights provider for the WebJobs SDK uses the [ServerTelemetryChannel](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/ServerTelemetryChannel/ServerTelemetryChannel.cs).</span></span> <span data-ttu-id="5befe-315">When the Application Insights endpoint is unavailable or throttling incoming requests, this channel [saves requests in the web app's file system and resubmits them later](http://apmtips.com/blog/2015/09/03/more-telemetry-channels).</span><span class="sxs-lookup"><span data-stu-id="5befe-315">When the Application Insights endpoint is unavailable or throttling incoming requests, this channel [saves requests in the web app's file system and resubmits them later](http://apmtips.com/blog/2015/09/03/more-telemetry-channels).</span></span>

<span data-ttu-id="5befe-316">The `TelemetryClient` is created by a class that implements `ITelemetryClientFactory`.</span><span class="sxs-lookup"><span data-stu-id="5befe-316">The `TelemetryClient` is created by a class that implements `ITelemetryClientFactory`.</span></span> <span data-ttu-id="5befe-317">By default, this is the [DefaultTelemetryClientFactory](https://github.com/Azure/azure-webjobs-sdk/blob/dev/src/Microsoft.Azure.WebJobs.Logging.ApplicationInsights/DefaultTelemetryClientFactory.cs).</span><span class="sxs-lookup"><span data-stu-id="5befe-317">By default, this is the [DefaultTelemetryClientFactory](https://github.com/Azure/azure-webjobs-sdk/blob/dev/src/Microsoft.Azure.WebJobs.Logging.ApplicationInsights/DefaultTelemetryClientFactory.cs).</span></span>

<span data-ttu-id="5befe-318">If you want to modify any part of the Application Insights pipeline, you can supply your own `ITelemetryClientFactory`, and the host will use your class to construct a `TelemetryClient`.</span><span class="sxs-lookup"><span data-stu-id="5befe-318">If you want to modify any part of the Application Insights pipeline, you can supply your own `ITelemetryClientFactory`, and the host will use your class to construct a `TelemetryClient`.</span></span> <span data-ttu-id="5befe-319">For example, this code overrides the `DefaultTelemetryClientFactory` to modify a property of the `ServerTelemetryChannel`:</span><span class="sxs-lookup"><span data-stu-id="5befe-319">For example, this code overrides the `DefaultTelemetryClientFactory` to modify a property of the `ServerTelemetryChannel`:</span></span>

```csharp
private class CustomTelemetryClientFactory : DefaultTelemetryClientFactory
{
    public CustomTelemetryClientFactory(string instrumentationKey, Func<string, LogLevel, bool> filter)
        : base(instrumentationKey, new SamplingPercentageEstimatorSettings(), filter)
    {
    }

    protected override ITelemetryChannel CreateTelemetryChannel()
    {
        ServerTelemetryChannel channel = new ServerTelemetryChannel();

        // change the default from 30 seconds to 15 seconds
        channel.MaxTelemetryBufferDelay = TimeSpan.FromSeconds(15);

        return channel;
    }
}
```

<span data-ttu-id="5befe-320">The SamplingPercentageEstimatorSettings object configures [adaptive sampling](https://docs.microsoft.com/azure/application-insights/app-insights-sampling#adaptive-sampling-at-your-web-server).</span><span class="sxs-lookup"><span data-stu-id="5befe-320">The SamplingPercentageEstimatorSettings object configures [adaptive sampling](https://docs.microsoft.com/azure/application-insights/app-insights-sampling#adaptive-sampling-at-your-web-server).</span></span> <span data-ttu-id="5befe-321">This means that in certain high-volume scenarios, App Insights sends a selected subset of telemetry data to the server.</span><span class="sxs-lookup"><span data-stu-id="5befe-321">This means that in certain high-volume scenarios, App Insights sends a selected subset of telemetry data to the server.</span></span>

<span data-ttu-id="5befe-322">Once you've created the telemetry factory, you pass it in to the Application Insights logging provider:</span><span class="sxs-lookup"><span data-stu-id="5befe-322">Once you've created the telemetry factory, you pass it in to the Application Insights logging provider:</span></span>

```csharp
var clientFactory = new CustomTelemetryClientFactory(instrumentationKey, filter.Filter);

config.LoggerFactory = new LoggerFactory()
    .AddApplicationInsights(clientFactory);
```

## <a id="nextsteps"></a> <span data-ttu-id="5befe-323">Next steps</span><span class="sxs-lookup"><span data-stu-id="5befe-323">Next steps</span></span>

<span data-ttu-id="5befe-324">This guide has provided code snippets that demonstrate how to handle common scenarios for working with the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="5befe-324">This guide has provided code snippets that demonstrate how to handle common scenarios for working with the WebJobs SDK.</span></span> <span data-ttu-id="5befe-325">For complete samples, see [azure-webjobs-sdk-samples](https://github.com/Azure/azure-webjobs-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="5befe-325">For complete samples, see [azure-webjobs-sdk-samples](https://github.com/Azure/azure-webjobs-sdk-samples).</span></span>