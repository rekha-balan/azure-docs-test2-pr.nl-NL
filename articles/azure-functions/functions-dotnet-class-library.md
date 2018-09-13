---
title: Azure Functions C# developer reference
description: Understand how to develop Azure Functions using C#.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.service: azure-functions
ms.devlang: dotnet
ms.topic: reference
ms.date: 12/12/2017
ms.author: glenga
ms.openlocfilehash: 9f538b48918bdde923c6dbf3999302e45b955035
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856228"
---
# <a name="azure-functions-c-developer-reference"></a><span data-ttu-id="23c89-104">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="23c89-104">Azure Functions C# developer reference</span></span>

<!-- When updating this article, make corresponding changes to any duplicate content in functions-reference-csharp.md -->

<span data-ttu-id="23c89-105">This article is an introduction to developing Azure Functions by using C# in .NET class libraries.</span><span class="sxs-lookup"><span data-stu-id="23c89-105">This article is an introduction to developing Azure Functions by using C# in .NET class libraries.</span></span>

<span data-ttu-id="23c89-106">Azure Functions supports C# and C# script programming languages.</span><span class="sxs-lookup"><span data-stu-id="23c89-106">Azure Functions supports C# and C# script programming languages.</span></span> <span data-ttu-id="23c89-107">If you're looking for guidance on [using C# in the Azure portal](functions-create-function-app-portal.md), see [C# script (.csx) developer reference](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="23c89-107">If you're looking for guidance on [using C# in the Azure portal](functions-create-function-app-portal.md), see [C# script (.csx) developer reference](functions-reference-csharp.md).</span></span>

<span data-ttu-id="23c89-108">This article assumes that you've already read the following articles:</span><span class="sxs-lookup"><span data-stu-id="23c89-108">This article assumes that you've already read the following articles:</span></span>

* [<span data-ttu-id="23c89-109">Azure Functions developers guide</span><span class="sxs-lookup"><span data-stu-id="23c89-109">Azure Functions developers guide</span></span>](functions-reference.md)
* [<span data-ttu-id="23c89-110">Azure Functions Visual Studio 2017 Tools</span><span class="sxs-lookup"><span data-stu-id="23c89-110">Azure Functions Visual Studio 2017 Tools</span></span>](functions-develop-vs.md)

## <a name="functions-class-library-project"></a><span data-ttu-id="23c89-111">Functions class library project</span><span class="sxs-lookup"><span data-stu-id="23c89-111">Functions class library project</span></span>

<span data-ttu-id="23c89-112">In Visual Studio, the **Azure Functions** project template creates a C# class library project that contains the following files:</span><span class="sxs-lookup"><span data-stu-id="23c89-112">In Visual Studio, the **Azure Functions** project template creates a C# class library project that contains the following files:</span></span>

* <span data-ttu-id="23c89-113">[host.json](functions-host-json.md) - stores configuration settings that affect all functions in the project when running locally or in Azure.</span><span class="sxs-lookup"><span data-stu-id="23c89-113">[host.json](functions-host-json.md) - stores configuration settings that affect all functions in the project when running locally or in Azure.</span></span>
* <span data-ttu-id="23c89-114">[local.settings.json](functions-run-local.md#local-settings-file) - stores app settings and connection strings that are used when running locally.</span><span class="sxs-lookup"><span data-stu-id="23c89-114">[local.settings.json](functions-run-local.md#local-settings-file) - stores app settings and connection strings that are used when running locally.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23c89-115">The build process creates a *function.json* file for each function.</span><span class="sxs-lookup"><span data-stu-id="23c89-115">The build process creates a *function.json* file for each function.</span></span> <span data-ttu-id="23c89-116">This *function.json* file is not meant to be edited directly.</span><span class="sxs-lookup"><span data-stu-id="23c89-116">This *function.json* file is not meant to be edited directly.</span></span> <span data-ttu-id="23c89-117">You can't change binding configuration or disable the function by editing this file.</span><span class="sxs-lookup"><span data-stu-id="23c89-117">You can't change binding configuration or disable the function by editing this file.</span></span> <span data-ttu-id="23c89-118">To disable a function, use the [Disable](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/DisableAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="23c89-118">To disable a function, use the [Disable](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/DisableAttribute.cs) attribute.</span></span> <span data-ttu-id="23c89-119">For example, add a Boolean app setting MY_TIMER_DISABLED, and apply `[Disable("MY_TIMER_DISABLED")]` to your function.</span><span class="sxs-lookup"><span data-stu-id="23c89-119">For example, add a Boolean app setting MY_TIMER_DISABLED, and apply `[Disable("MY_TIMER_DISABLED")]` to your function.</span></span> <span data-ttu-id="23c89-120">You can then enable and disable it by changing the app setting.</span><span class="sxs-lookup"><span data-stu-id="23c89-120">You can then enable and disable it by changing the app setting.</span></span>

## <a name="methods-recognized-as-functions"></a><span data-ttu-id="23c89-121">Methods recognized as functions</span><span class="sxs-lookup"><span data-stu-id="23c89-121">Methods recognized as functions</span></span>

<span data-ttu-id="23c89-122">In a class library, a function is a static method with a `FunctionName` and a trigger attribute, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="23c89-122">In a class library, a function is a static method with a `FunctionName` and a trigger attribute, as shown in the following example:</span></span>

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

<span data-ttu-id="23c89-123">The `FunctionName` attribute marks the method as a function entry point.</span><span class="sxs-lookup"><span data-stu-id="23c89-123">The `FunctionName` attribute marks the method as a function entry point.</span></span> <span data-ttu-id="23c89-124">The name must be unique within a project, start with a letter and only contain letters, numbers, `_` and `-`, up to 127 characters in length.</span><span class="sxs-lookup"><span data-stu-id="23c89-124">The name must be unique within a project, start with a letter and only contain letters, numbers, `_` and `-`, up to 127 characters in length.</span></span> <span data-ttu-id="23c89-125">Project templates often create a method named `Run`, but the method name can be any valid C# method name.</span><span class="sxs-lookup"><span data-stu-id="23c89-125">Project templates often create a method named `Run`, but the method name can be any valid C# method name.</span></span>

<span data-ttu-id="23c89-126">The trigger attribute specifies the trigger type and binds input data to a method parameter.</span><span class="sxs-lookup"><span data-stu-id="23c89-126">The trigger attribute specifies the trigger type and binds input data to a method parameter.</span></span> <span data-ttu-id="23c89-127">The example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem` parameter.</span><span class="sxs-lookup"><span data-stu-id="23c89-127">The example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem` parameter.</span></span>

## <a name="method-signature-parameters"></a><span data-ttu-id="23c89-128">Method signature parameters</span><span class="sxs-lookup"><span data-stu-id="23c89-128">Method signature parameters</span></span>

<span data-ttu-id="23c89-129">The method signature may contain parameters other than the one used with the trigger attribute.</span><span class="sxs-lookup"><span data-stu-id="23c89-129">The method signature may contain parameters other than the one used with the trigger attribute.</span></span> <span data-ttu-id="23c89-130">Here are some of the additional parameters that you can include:</span><span class="sxs-lookup"><span data-stu-id="23c89-130">Here are some of the additional parameters that you can include:</span></span>

* <span data-ttu-id="23c89-131">[Input and output bindings](functions-triggers-bindings.md) marked as such by decorating them with attributes.</span><span class="sxs-lookup"><span data-stu-id="23c89-131">[Input and output bindings](functions-triggers-bindings.md) marked as such by decorating them with attributes.</span></span>  
* <span data-ttu-id="23c89-132">An `ILogger` or `TraceWriter` parameter for [logging](#logging).</span><span class="sxs-lookup"><span data-stu-id="23c89-132">An `ILogger` or `TraceWriter` parameter for [logging](#logging).</span></span>
* <span data-ttu-id="23c89-133">A `CancellationToken` parameter for [graceful shutdown](#cancellation-tokens).</span><span class="sxs-lookup"><span data-stu-id="23c89-133">A `CancellationToken` parameter for [graceful shutdown](#cancellation-tokens).</span></span>
* <span data-ttu-id="23c89-134">[Binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns) parameters to get trigger metadata.</span><span class="sxs-lookup"><span data-stu-id="23c89-134">[Binding expressions](functions-triggers-bindings.md#binding-expressions-and-patterns) parameters to get trigger metadata.</span></span>

<span data-ttu-id="23c89-135">The order of parameters in the function signature does not matter.</span><span class="sxs-lookup"><span data-stu-id="23c89-135">The order of parameters in the function signature does not matter.</span></span> <span data-ttu-id="23c89-136">For example, you can put trigger parameters before or after other bindings, and you can put the logger parameter before or after trigger or binding parameters.</span><span class="sxs-lookup"><span data-stu-id="23c89-136">For example, you can put trigger parameters before or after other bindings, and you can put the logger parameter before or after trigger or binding parameters.</span></span>

### <a name="output-binding-example"></a><span data-ttu-id="23c89-137">Output binding example</span><span class="sxs-lookup"><span data-stu-id="23c89-137">Output binding example</span></span>

<span data-ttu-id="23c89-138">The following example modifies the preceding one by adding an output queue binding.</span><span class="sxs-lookup"><span data-stu-id="23c89-138">The following example modifies the preceding one by adding an output queue binding.</span></span> <span data-ttu-id="23c89-139">The function writes the queue message that triggers the function to a new queue message in a different queue.</span><span class="sxs-lookup"><span data-stu-id="23c89-139">The function writes the queue message that triggers the function to a new queue message in a different queue.</span></span>

```csharp
public static class SimpleExampleWithOutput
{
    [FunctionName("CopyQueueMessage")]
    public static void Run(
        [QueueTrigger("myqueue-items-source")] string myQueueItem, 
        [Queue("myqueue-items-destination")] out string myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"CopyQueueMessage function processed: {myQueueItem}");
        myQueueItemCopy = myQueueItem;
    }
}
```

<span data-ttu-id="23c89-140">The binding reference articles ([Storage queues](functions-bindings-storage-queue.md), for example) explain which parameter types you can use with trigger, input, or output binding attributes.</span><span class="sxs-lookup"><span data-stu-id="23c89-140">The binding reference articles ([Storage queues](functions-bindings-storage-queue.md), for example) explain which parameter types you can use with trigger, input, or output binding attributes.</span></span>

### <a name="binding-expressions-example"></a><span data-ttu-id="23c89-141">Binding expressions example</span><span class="sxs-lookup"><span data-stu-id="23c89-141">Binding expressions example</span></span>

<span data-ttu-id="23c89-142">The following code gets the name of the queue to monitor from an app setting, and it gets the queue message creation time in the `insertionTime` parameter.</span><span class="sxs-lookup"><span data-stu-id="23c89-142">The following code gets the name of the queue to monitor from an app setting, and it gets the queue message creation time in the `insertionTime` parameter.</span></span>

```csharp
public static class BindingExpressionsExample
{
    [FunctionName("LogQueueMessage")]
    public static void Run(
        [QueueTrigger("%queueappsetting%")] string myQueueItem,
        DateTimeOffset insertionTime,
        TraceWriter log)
    {
        log.Info($"Message content: {myQueueItem}");
        log.Info($"Created at: {insertionTime}");
    }
}
```

## <a name="autogenerated-functionjson"></a><span data-ttu-id="23c89-143">Autogenerated function.json</span><span class="sxs-lookup"><span data-stu-id="23c89-143">Autogenerated function.json</span></span>

<span data-ttu-id="23c89-144">The build process creates a *function.json* file in a function folder in the build folder.</span><span class="sxs-lookup"><span data-stu-id="23c89-144">The build process creates a *function.json* file in a function folder in the build folder.</span></span> <span data-ttu-id="23c89-145">As noted earlier, this file is not meant to be edited directly.</span><span class="sxs-lookup"><span data-stu-id="23c89-145">As noted earlier, this file is not meant to be edited directly.</span></span> <span data-ttu-id="23c89-146">You can't change binding configuration or disable the function by editing this file.</span><span class="sxs-lookup"><span data-stu-id="23c89-146">You can't change binding configuration or disable the function by editing this file.</span></span> 

<span data-ttu-id="23c89-147">The purpose of this file is to provide information to the scale controller to use for [scaling decisions on the consumption plan](functions-scale.md#how-the-consumption-plan-works).</span><span class="sxs-lookup"><span data-stu-id="23c89-147">The purpose of this file is to provide information to the scale controller to use for [scaling decisions on the consumption plan](functions-scale.md#how-the-consumption-plan-works).</span></span> <span data-ttu-id="23c89-148">For this reason, the file only has trigger info, not input or output bindings.</span><span class="sxs-lookup"><span data-stu-id="23c89-148">For this reason, the file only has trigger info, not input or output bindings.</span></span>

<span data-ttu-id="23c89-149">The generated *function.json* file includes a `configurationSource` property that tells the runtime to use .NET attributes for bindings, rather than *function.json* configuration.</span><span class="sxs-lookup"><span data-stu-id="23c89-149">The generated *function.json* file includes a `configurationSource` property that tells the runtime to use .NET attributes for bindings, rather than *function.json* configuration.</span></span> <span data-ttu-id="23c89-150">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="23c89-150">Here's an example:</span></span>

```json
{
  "generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
  "configurationSource": "attributes",
  "bindings": [
    {
      "type": "queueTrigger",
      "queueName": "%input-queue-name%",
      "name": "myQueueItem"
    }
  ],
  "disabled": false,
  "scriptFile": "..\\bin\\FunctionApp1.dll",
  "entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```

## <a name="microsoftnetsdkfunctions"></a><span data-ttu-id="23c89-151">Microsoft.NET.Sdk.Functions</span><span class="sxs-lookup"><span data-stu-id="23c89-151">Microsoft.NET.Sdk.Functions</span></span>

<span data-ttu-id="23c89-152">The *function.json* file generation is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="23c89-152">The *function.json* file generation is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> 

<span data-ttu-id="23c89-153">The same package is used for both version 1.x and 2.x of the Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="23c89-153">The same package is used for both version 1.x and 2.x of the Functions runtime.</span></span> <span data-ttu-id="23c89-154">The target framework is what differentiates a 1.x project from a 2.x project.</span><span class="sxs-lookup"><span data-stu-id="23c89-154">The target framework is what differentiates a 1.x project from a 2.x project.</span></span> <span data-ttu-id="23c89-155">Here are the relevant parts of *.csproj* files, showing different target frameworks and the same `Sdk` package:</span><span class="sxs-lookup"><span data-stu-id="23c89-155">Here are the relevant parts of *.csproj* files, showing different target frameworks and the same `Sdk` package:</span></span>

<span data-ttu-id="23c89-156">**Functions 1.x**</span><span class="sxs-lookup"><span data-stu-id="23c89-156">**Functions 1.x**</span></span>

```xml
<PropertyGroup>
  <TargetFramework>net461</TargetFramework>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Sdk.Functions" Version="1.0.8" />
</ItemGroup>
```

<span data-ttu-id="23c89-157">**Functions 2.x**</span><span class="sxs-lookup"><span data-stu-id="23c89-157">**Functions 2.x**</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netstandard2.0</TargetFramework>
  <AzureFunctionsVersion>v2</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Sdk.Functions" Version="1.0.8" />
</ItemGroup>
```

<span data-ttu-id="23c89-158">Among the `Sdk` package dependencies are triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="23c89-158">Among the `Sdk` package dependencies are triggers and bindings.</span></span> <span data-ttu-id="23c89-159">A 1.x project refers to 1.x triggers and bindings because those target the .NET Framework, while 2.x triggers and bindings target .NET Core.</span><span class="sxs-lookup"><span data-stu-id="23c89-159">A 1.x project refers to 1.x triggers and bindings because those target the .NET Framework, while 2.x triggers and bindings target .NET Core.</span></span>

<span data-ttu-id="23c89-160">The `Sdk` package also depends on [Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json), and indirectly on [WindowsAzure.Storage](http://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="23c89-160">The `Sdk` package also depends on [Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json), and indirectly on [WindowsAzure.Storage](http://www.nuget.org/packages/WindowsAzure.Storage).</span></span> <span data-ttu-id="23c89-161">These dependencies make sure that your project uses the versions of those packages that work with the Functions runtime version that the project targets.</span><span class="sxs-lookup"><span data-stu-id="23c89-161">These dependencies make sure that your project uses the versions of those packages that work with the Functions runtime version that the project targets.</span></span> <span data-ttu-id="23c89-162">For example, `Newtonsoft.Json` has version 11 for .NET Framework 4.6.1, but the Functions runtime that targets .NET Framework 4.6.1 is only compatible with `Newtonsoft.Json` 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="23c89-162">For example, `Newtonsoft.Json` has version 11 for .NET Framework 4.6.1, but the Functions runtime that targets .NET Framework 4.6.1 is only compatible with `Newtonsoft.Json` 9.0.1.</span></span> <span data-ttu-id="23c89-163">So your function code in that project also has to use `Newtonsoft.Json` 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="23c89-163">So your function code in that project also has to use `Newtonsoft.Json` 9.0.1.</span></span>

<span data-ttu-id="23c89-164">The source code for `Microsoft.NET.Sdk.Functions` is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="23c89-164">The source code for `Microsoft.NET.Sdk.Functions` is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="runtime-version"></a><span data-ttu-id="23c89-165">Runtime version</span><span class="sxs-lookup"><span data-stu-id="23c89-165">Runtime version</span></span>

<span data-ttu-id="23c89-166">Visual Studio uses the [Azure Functions Core Tools](functions-run-local.md#install-the-azure-functions-core-tools) to run Functions projects.</span><span class="sxs-lookup"><span data-stu-id="23c89-166">Visual Studio uses the [Azure Functions Core Tools](functions-run-local.md#install-the-azure-functions-core-tools) to run Functions projects.</span></span> <span data-ttu-id="23c89-167">The Core Tools is a command-line interface for the Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="23c89-167">The Core Tools is a command-line interface for the Functions runtime.</span></span>

<span data-ttu-id="23c89-168">If you install the Core Tools by using npm, that doesn't affect the Core Tools version used by Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23c89-168">If you install the Core Tools by using npm, that doesn't affect the Core Tools version used by Visual Studio.</span></span> <span data-ttu-id="23c89-169">For the Functions runtime version 1.x, Visual Studio stores Core Tools versions in *%USERPROFILE%\AppData\Local\Azure.Functions.Cli* and uses the latest version stored there.</span><span class="sxs-lookup"><span data-stu-id="23c89-169">For the Functions runtime version 1.x, Visual Studio stores Core Tools versions in *%USERPROFILE%\AppData\Local\Azure.Functions.Cli* and uses the latest version stored there.</span></span> <span data-ttu-id="23c89-170">For Functions 2.x, the Core Tools are included in the **Azure Functions and Web Jobs Tools** extension.</span><span class="sxs-lookup"><span data-stu-id="23c89-170">For Functions 2.x, the Core Tools are included in the **Azure Functions and Web Jobs Tools** extension.</span></span> <span data-ttu-id="23c89-171">For both 1.x and 2.x, you can see what version is being used in the console output when you run a Functions project:</span><span class="sxs-lookup"><span data-stu-id="23c89-171">For both 1.x and 2.x, you can see what version is being used in the console output when you run a Functions project:</span></span>

```terminal
[3/1/2018 9:59:53 AM] Starting Host (HostId=contoso2-1518597420, Version=2.0.11353.0, ProcessId=22020, Debug=False, Attempt=0, FunctionsExtensionVersion=)
```

## <a name="supported-types-for-bindings"></a><span data-ttu-id="23c89-172">Supported types for bindings</span><span class="sxs-lookup"><span data-stu-id="23c89-172">Supported types for bindings</span></span>

<span data-ttu-id="23c89-173">Each binding has its own supported types; for instance, a blob trigger attribute can be applied to a string parameter, a POCO parameter, a `CloudBlockBlob` parameter, or any of several other supported types.</span><span class="sxs-lookup"><span data-stu-id="23c89-173">Each binding has its own supported types; for instance, a blob trigger attribute can be applied to a string parameter, a POCO parameter, a `CloudBlockBlob` parameter, or any of several other supported types.</span></span> <span data-ttu-id="23c89-174">The [binding reference article for blob bindings](functions-bindings-storage-blob.md#trigger---usage) lists all supported parameter types.</span><span class="sxs-lookup"><span data-stu-id="23c89-174">The [binding reference article for blob bindings](functions-bindings-storage-blob.md#trigger---usage) lists all supported parameter types.</span></span> <span data-ttu-id="23c89-175">For more information, see [Triggers and bindings](functions-triggers-bindings.md) and the [binding reference docs for each binding type](functions-triggers-bindings.md#next-steps).</span><span class="sxs-lookup"><span data-stu-id="23c89-175">For more information, see [Triggers and bindings](functions-triggers-bindings.md) and the [binding reference docs for each binding type](functions-triggers-bindings.md#next-steps).</span></span>

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="binding-to-method-return-value"></a><span data-ttu-id="23c89-176">Binding to method return value</span><span class="sxs-lookup"><span data-stu-id="23c89-176">Binding to method return value</span></span>

<span data-ttu-id="23c89-177">You can use a method return value for an output binding, by applying the attribute to the method return value.</span><span class="sxs-lookup"><span data-stu-id="23c89-177">You can use a method return value for an output binding, by applying the attribute to the method return value.</span></span> <span data-ttu-id="23c89-178">For examples, see [Triggers and bindings](functions-triggers-bindings.md#using-the-function-return-value).</span><span class="sxs-lookup"><span data-stu-id="23c89-178">For examples, see [Triggers and bindings](functions-triggers-bindings.md#using-the-function-return-value).</span></span> 

<span data-ttu-id="23c89-179">Use the return value only if a successful function execution always results in a return value to pass to the output binding.</span><span class="sxs-lookup"><span data-stu-id="23c89-179">Use the return value only if a successful function execution always results in a return value to pass to the output binding.</span></span> <span data-ttu-id="23c89-180">Otherwise, use `ICollector` or `IAsyncCollector`, as shown in the following section.</span><span class="sxs-lookup"><span data-stu-id="23c89-180">Otherwise, use `ICollector` or `IAsyncCollector`, as shown in the following section.</span></span>

## <a name="writing-multiple-output-values"></a><span data-ttu-id="23c89-181">Writing multiple output values</span><span class="sxs-lookup"><span data-stu-id="23c89-181">Writing multiple output values</span></span>

<span data-ttu-id="23c89-182">To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span><span class="sxs-lookup"><span data-stu-id="23c89-182">To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="23c89-183">These types are write-only collections that are written to the output binding when the method completes.</span><span class="sxs-lookup"><span data-stu-id="23c89-183">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="23c89-184">This example writes multiple queue messages into the same queue using `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="23c89-184">This example writes multiple queue messages into the same queue using `ICollector`:</span></span>

```csharp
public static class ICollectorExample
{
    [FunctionName("CopyQueueMessageICollector")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-3")] string myQueueItem,
        [Queue("myqueue-items-destination")] ICollector<string> myDestinationQueue,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        myDestinationQueue.Add($"Copy 1: {myQueueItem}");
        myDestinationQueue.Add($"Copy 2: {myQueueItem}");
    }
}
```

## <a name="logging"></a><span data-ttu-id="23c89-185">Logging</span><span class="sxs-lookup"><span data-stu-id="23c89-185">Logging</span></span>

<span data-ttu-id="23c89-186">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="23c89-186">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="23c89-187">We recommend that you name it `log`.</span><span class="sxs-lookup"><span data-stu-id="23c89-187">We recommend that you name it `log`.</span></span> <span data-ttu-id="23c89-188">Avoid using `Console.Write` in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="23c89-188">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="23c89-189">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="23c89-189">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="23c89-190">The log level for `TraceWriter` can be configured in [host.json](functions-host-json.md).</span><span class="sxs-lookup"><span data-stu-id="23c89-190">The log level for `TraceWriter` can be configured in [host.json](functions-host-json.md).</span></span>

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

> [!NOTE]
> <span data-ttu-id="23c89-191">For information about a newer logging framework that you can use instead of `TraceWriter`, see [Write logs in C# functions](functions-monitoring.md#write-logs-in-c-functions) in the **Monitor Azure Functions** article.</span><span class="sxs-lookup"><span data-stu-id="23c89-191">For information about a newer logging framework that you can use instead of `TraceWriter`, see [Write logs in C# functions](functions-monitoring.md#write-logs-in-c-functions) in the **Monitor Azure Functions** article.</span></span>

## <a name="async"></a><span data-ttu-id="23c89-192">Async</span><span class="sxs-lookup"><span data-stu-id="23c89-192">Async</span></span>

<span data-ttu-id="23c89-193">To make a function [asynchronous](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/), use the `async` keyword and return a `Task` object.</span><span class="sxs-lookup"><span data-stu-id="23c89-193">To make a function [asynchronous](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/), use the `async` keyword and return a `Task` object.</span></span>

```csharp
public static class AsyncExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token,
        TraceWriter log)
    {
        log.Info($"BlobCopy function processed.");
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

<span data-ttu-id="23c89-194">You can't use `out` parameters in async functions.</span><span class="sxs-lookup"><span data-stu-id="23c89-194">You can't use `out` parameters in async functions.</span></span> <span data-ttu-id="23c89-195">For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.</span><span class="sxs-lookup"><span data-stu-id="23c89-195">For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.</span></span>

## <a name="cancellation-tokens"></a><span data-ttu-id="23c89-196">Cancellation tokens</span><span class="sxs-lookup"><span data-stu-id="23c89-196">Cancellation tokens</span></span>

<span data-ttu-id="23c89-197">A function can accept a [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) parameter, which enables the operating system to notify your code when the function is about to be terminated.</span><span class="sxs-lookup"><span data-stu-id="23c89-197">A function can accept a [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) parameter, which enables the operating system to notify your code when the function is about to be terminated.</span></span> <span data-ttu-id="23c89-198">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span><span class="sxs-lookup"><span data-stu-id="23c89-198">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="23c89-199">The following example shows how to check for impending function termination.</span><span class="sxs-lookup"><span data-stu-id="23c89-199">The following example shows how to check for impending function termination.</span></span>

```csharp
public static class CancellationTokenExample
{
    public static void Run(
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
            Thread.Sleep(5000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }
}
```

## <a name="environment-variables"></a><span data-ttu-id="23c89-200">Environment variables</span><span class="sxs-lookup"><span data-stu-id="23c89-200">Environment variables</span></span>

<span data-ttu-id="23c89-201">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span><span class="sxs-lookup"><span data-stu-id="23c89-201">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

```csharp
public static class EnvironmentVariablesExample
{
    [FunctionName("GetEnvironmentVariables")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
    {
        log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
        log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
        log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
    }

    public static string GetEnvironmentVariable(string name)
    {
        return name + ": " +
            System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
    }
}
```

<span data-ttu-id="23c89-202">App settings can be read from environment variables both when developing locally and when running in Azure.</span><span class="sxs-lookup"><span data-stu-id="23c89-202">App settings can be read from environment variables both when developing locally and when running in Azure.</span></span> <span data-ttu-id="23c89-203">When developing locally, app settings come from the `Values` collection in the *local.settings.json* file.</span><span class="sxs-lookup"><span data-stu-id="23c89-203">When developing locally, app settings come from the `Values` collection in the *local.settings.json* file.</span></span> <span data-ttu-id="23c89-204">In both environments, local and Azure, `GetEnvironmentVariable("<app setting name>")` retrieves the value of the named app setting.</span><span class="sxs-lookup"><span data-stu-id="23c89-204">In both environments, local and Azure, `GetEnvironmentVariable("<app setting name>")` retrieves the value of the named app setting.</span></span> <span data-ttu-id="23c89-205">For instance, when you're running locally, "My Site Name" would be returned if your *local.settings.json* file contains `{ "Values": { "WEBSITE_SITE_NAME": "My Site Name" } }`.</span><span class="sxs-lookup"><span data-stu-id="23c89-205">For instance, when you're running locally, "My Site Name" would be returned if your *local.settings.json* file contains `{ "Values": { "WEBSITE_SITE_NAME": "My Site Name" } }`.</span></span>

<span data-ttu-id="23c89-206">The [System.Configuration.ConfigurationManager.AppSettings](https://docs.microsoft.com/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable` as shown here.</span><span class="sxs-lookup"><span data-stu-id="23c89-206">The [System.Configuration.ConfigurationManager.AppSettings](https://docs.microsoft.com/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable` as shown here.</span></span>

## <a name="binding-at-runtime"></a><span data-ttu-id="23c89-207">Binding at runtime</span><span class="sxs-lookup"><span data-stu-id="23c89-207">Binding at runtime</span></span>

<span data-ttu-id="23c89-208">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in attributes.</span><span class="sxs-lookup"><span data-stu-id="23c89-208">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in attributes.</span></span> <span data-ttu-id="23c89-209">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span><span class="sxs-lookup"><span data-stu-id="23c89-209">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="23c89-210">With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.</span><span class="sxs-lookup"><span data-stu-id="23c89-210">With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.</span></span>

<span data-ttu-id="23c89-211">Define an imperative binding as follows:</span><span class="sxs-lookup"><span data-stu-id="23c89-211">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="23c89-212">**Do not** include an attribute in the function signature for your desired imperative bindings.</span><span class="sxs-lookup"><span data-stu-id="23c89-212">**Do not** include an attribute in the function signature for your desired imperative bindings.</span></span>
- <span data-ttu-id="23c89-213">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="23c89-213">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="23c89-214">Use the following C# pattern to perform the data binding.</span><span class="sxs-lookup"><span data-stu-id="23c89-214">Use the following C# pattern to perform the data binding.</span></span>

  ```cs
  using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
  {
      ...
  }
  ```

  <span data-ttu-id="23c89-215">`BindingTypeAttribute` is the .NET attribute that defines your binding, and `T` is an input or output type that's supported by that binding type.</span><span class="sxs-lookup"><span data-stu-id="23c89-215">`BindingTypeAttribute` is the .NET attribute that defines your binding, and `T` is an input or output type that's supported by that binding type.</span></span> <span data-ttu-id="23c89-216">`T` cannot be an `out` parameter type (such as `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="23c89-216">`T` cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="23c89-217">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) with imperative binding.</span><span class="sxs-lookup"><span data-stu-id="23c89-217">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) with imperative binding.</span></span>

### <a name="single-attribute-example"></a><span data-ttu-id="23c89-218">Single attribute example</span><span class="sxs-lookup"><span data-stu-id="23c89-218">Single attribute example</span></span>

<span data-ttu-id="23c89-219">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#output) with blob path that's defined at run time, then writes a string to the blob.</span><span class="sxs-lookup"><span data-stu-id="23c89-219">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#output) with blob path that's defined at run time, then writes a string to the blob.</span></span>

```cs
public static class IBinderExample
{
    [FunctionName("CreateBlobUsingBinder")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-4")] string myQueueItem,
        IBinder binder,
        TraceWriter log)
    {
        log.Info($"CreateBlobUsingBinder function processed: {myQueueItem}");
        using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
                    $"samples-output/{myQueueItem}", FileAccess.Write)))
        {
            writer.Write("Hello World!");
        };
    }
}
```

<span data-ttu-id="23c89-220">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span><span class="sxs-lookup"><span data-stu-id="23c89-220">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>

### <a name="multiple-attribute-example"></a><span data-ttu-id="23c89-221">Multiple attribute example</span><span class="sxs-lookup"><span data-stu-id="23c89-221">Multiple attribute example</span></span>

<span data-ttu-id="23c89-222">The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="23c89-222">The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="23c89-223">You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="23c89-223">You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="23c89-224">Use a `Binder` parameter, not `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="23c89-224">Use a `Binder` parameter, not `IBinder`.</span></span>  <span data-ttu-id="23c89-225">For example:</span><span class="sxs-lookup"><span data-stu-id="23c89-225">For example:</span></span>

```cs
public static class IBinderExampleMultipleAttributes
{
    [FunctionName("CreateBlobInDifferentStorageAccount")]
    public async static Task RunAsync(
            [QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
            Binder binder,
            TraceWriter log)
    {
        log.Info($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
        var attributes = new Attribute[]
        {
        new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
        new StorageAccountAttribute("MyStorageAccount")
        };
        using (var writer = await binder.BindAsync<TextWriter>(attributes))
        {
            await writer.WriteAsync("Hello World!!");
        }
    }
}
```

## <a name="triggers-and-bindings"></a><span data-ttu-id="23c89-226">Triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="23c89-226">Triggers and bindings</span></span> 

[!INCLUDE [Supported triggers and bindings](../../includes/functions-bindings.md)]

## <a name="next-steps"></a><span data-ttu-id="23c89-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="23c89-227">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="23c89-228">Learn more about triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="23c89-228">Learn more about triggers and bindings</span></span>](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="23c89-229">Learn more about best practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="23c89-229">Learn more about best practices for Azure Functions</span></span>](functions-best-practices.md)
