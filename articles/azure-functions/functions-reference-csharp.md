---
title: Azure Functions C# script developer reference
description: Understand how to develop Azure Functions using C# script.
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
ms.openlocfilehash: 3bdb5bc2aa47a51cc95a4274fbf20ba5d0515130
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782592"
---
# <a name="azure-functions-c-script-csx-developer-reference"></a><span data-ttu-id="a8a56-104">Azure Functions C# script (.csx) developer reference</span><span class="sxs-lookup"><span data-stu-id="a8a56-104">Azure Functions C# script (.csx) developer reference</span></span>

<!-- When updating this article, make corresponding changes to any duplicate content in functions-dotnet-class-library.md -->

<span data-ttu-id="a8a56-105">This article is an introduction to developing Azure Functions by using C# script (*.csx*).</span><span class="sxs-lookup"><span data-stu-id="a8a56-105">This article is an introduction to developing Azure Functions by using C# script (*.csx*).</span></span>

<span data-ttu-id="a8a56-106">Azure Functions supports C# and C# script programming languages.</span><span class="sxs-lookup"><span data-stu-id="a8a56-106">Azure Functions supports C# and C# script programming languages.</span></span> <span data-ttu-id="a8a56-107">If you're looking for guidance on [using C# in a Visual Studio class library project](functions-develop-vs.md), see [C# developer reference](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="a8a56-107">If you're looking for guidance on [using C# in a Visual Studio class library project](functions-develop-vs.md), see [C# developer reference](functions-dotnet-class-library.md).</span></span>

<span data-ttu-id="a8a56-108">This article assumes that you've already read the [Azure Functions developers guide](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a8a56-108">This article assumes that you've already read the [Azure Functions developers guide](functions-reference.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="a8a56-109">How .csx works</span><span class="sxs-lookup"><span data-stu-id="a8a56-109">How .csx works</span></span>

<span data-ttu-id="a8a56-110">The C# script experience for Azure Functions is based on the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki/Introduction).</span><span class="sxs-lookup"><span data-stu-id="a8a56-110">The C# script experience for Azure Functions is based on the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki/Introduction).</span></span> <span data-ttu-id="a8a56-111">Data flows into your C# function via method arguments.</span><span class="sxs-lookup"><span data-stu-id="a8a56-111">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="a8a56-112">Argument names are specified in a `function.json` file, and there are predefined names for accessing things like the function logger and cancellation tokens.</span><span class="sxs-lookup"><span data-stu-id="a8a56-112">Argument names are specified in a `function.json` file, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="a8a56-113">The *.csx* format allows you to write less "boilerplate" and focus on writing just a C# function.</span><span class="sxs-lookup"><span data-stu-id="a8a56-113">The *.csx* format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="a8a56-114">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span><span class="sxs-lookup"><span data-stu-id="a8a56-114">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="a8a56-115">Include any assembly references and namespaces at the beginning of the file as usual.</span><span class="sxs-lookup"><span data-stu-id="a8a56-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span>

<span data-ttu-id="a8a56-116">A function app's *.csx* files are compiled when an instance is initialized.</span><span class="sxs-lookup"><span data-stu-id="a8a56-116">A function app's *.csx* files are compiled when an instance is initialized.</span></span> <span data-ttu-id="a8a56-117">This compilation step means things like cold start may take longer for C# script functions compared to C# class libraries.</span><span class="sxs-lookup"><span data-stu-id="a8a56-117">This compilation step means things like cold start may take longer for C# script functions compared to C# class libraries.</span></span> <span data-ttu-id="a8a56-118">This compilation step is also why C# script functions are editable in the Azure Portal, while C# class libraries are not.</span><span class="sxs-lookup"><span data-stu-id="a8a56-118">This compilation step is also why C# script functions are editable in the Azure Portal, while C# class libraries are not.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="a8a56-119">Binding to arguments</span><span class="sxs-lookup"><span data-stu-id="a8a56-119">Binding to arguments</span></span>

<span data-ttu-id="a8a56-120">Input or output data is bound to a C# script function parameter via the `name` property in the *function.json* configuration file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-120">Input or output data is bound to a C# script function parameter via the `name` property in the *function.json* configuration file.</span></span> <span data-ttu-id="a8a56-121">The following example shows a *function.json* file  and *run.csx* file for a queue-triggered function.</span><span class="sxs-lookup"><span data-stu-id="a8a56-121">The following example shows a *function.json* file  and *run.csx* file for a queue-triggered function.</span></span> <span data-ttu-id="a8a56-122">The parameter that receives data from the queue message is named `myQueueItem` because that's the value of the `name` property.</span><span class="sxs-lookup"><span data-stu-id="a8a56-122">The parameter that receives data from the queue message is named `myQueueItem` because that's the value of the `name` property.</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionAppSetting"
        }
    ]
}
```

```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}");
}
```

<span data-ttu-id="a8a56-123">The `#r` statement is explained [later in this article](#referencing-external-assemblies).</span><span class="sxs-lookup"><span data-stu-id="a8a56-123">The `#r` statement is explained [later in this article](#referencing-external-assemblies).</span></span>

## <a name="supported-types-for-bindings"></a><span data-ttu-id="a8a56-124">Supported types for bindings</span><span class="sxs-lookup"><span data-stu-id="a8a56-124">Supported types for bindings</span></span>

<span data-ttu-id="a8a56-125">Each binding has its own supported types; for instance, a blob trigger can be used with a string parameter, a POCO parameter, a `CloudBlockBlob` parameter, or any of several other supported types.</span><span class="sxs-lookup"><span data-stu-id="a8a56-125">Each binding has its own supported types; for instance, a blob trigger can be used with a string parameter, a POCO parameter, a `CloudBlockBlob` parameter, or any of several other supported types.</span></span> <span data-ttu-id="a8a56-126">The [binding reference article for blob bindings](functions-bindings-storage-blob.md#trigger---usage) lists all supported parameter types for blob triggers.</span><span class="sxs-lookup"><span data-stu-id="a8a56-126">The [binding reference article for blob bindings](functions-bindings-storage-blob.md#trigger---usage) lists all supported parameter types for blob triggers.</span></span> <span data-ttu-id="a8a56-127">For more information, see [Triggers and bindings](functions-triggers-bindings.md) and the [binding reference docs for each binding type](functions-triggers-bindings.md#next-steps).</span><span class="sxs-lookup"><span data-stu-id="a8a56-127">For more information, see [Triggers and bindings](functions-triggers-bindings.md) and the [binding reference docs for each binding type](functions-triggers-bindings.md#next-steps).</span></span>

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="referencing-custom-classes"></a><span data-ttu-id="a8a56-128">Referencing custom classes</span><span class="sxs-lookup"><span data-stu-id="a8a56-128">Referencing custom classes</span></span>

<span data-ttu-id="a8a56-129">If you need to use a custom Plain Old CLR Object (POCO) class, you can include the class definition inside the same file or put it in a separate file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-129">If you need to use a custom Plain Old CLR Object (POCO) class, you can include the class definition inside the same file or put it in a separate file.</span></span>

<span data-ttu-id="a8a56-130">The following example shows a *run.csx* example that includes a POCO class definition.</span><span class="sxs-lookup"><span data-stu-id="a8a56-130">The following example shows a *run.csx* example that includes a POCO class definition.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

<span data-ttu-id="a8a56-131">A POCO class must have a getter and setter defined for each property.</span><span class="sxs-lookup"><span data-stu-id="a8a56-131">A POCO class must have a getter and setter defined for each property.</span></span>

## <a name="reusing-csx-code"></a><span data-ttu-id="a8a56-132">Reusing .csx code</span><span class="sxs-lookup"><span data-stu-id="a8a56-132">Reusing .csx code</span></span>

<span data-ttu-id="a8a56-133">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-133">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="a8a56-134">To do that, use `#load` directives in your *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-134">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="a8a56-135">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span><span class="sxs-lookup"><span data-stu-id="a8a56-135">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="a8a56-136">Example *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="a8a56-136">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="a8a56-137">Example *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="a8a56-137">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="a8a56-138">Using a shared *.csx* file is a common pattern when you want to strongly type the data passed between functions by using a POCO object.</span><span class="sxs-lookup"><span data-stu-id="a8a56-138">Using a shared *.csx* file is a common pattern when you want to strongly type the data passed between functions by using a POCO object.</span></span> <span data-ttu-id="a8a56-139">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span><span class="sxs-lookup"><span data-stu-id="a8a56-139">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="a8a56-140">Example *run.csx* for HTTP trigger:</span><span class="sxs-lookup"><span data-stu-id="a8a56-140">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="a8a56-141">Example *run.csx* for queue trigger:</span><span class="sxs-lookup"><span data-stu-id="a8a56-141">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="a8a56-142">Example *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="a8a56-142">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="a8a56-143">You can use a relative path with the `#load` directive:</span><span class="sxs-lookup"><span data-stu-id="a8a56-143">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="a8a56-144">`#load "mylogger.csx"` loads a file located in the function folder.</span><span class="sxs-lookup"><span data-stu-id="a8a56-144">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="a8a56-145">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span><span class="sxs-lookup"><span data-stu-id="a8a56-145">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="a8a56-146">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="a8a56-146">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="a8a56-147">The `#load` directive works only with *.csx* files, not with *.cs* files.</span><span class="sxs-lookup"><span data-stu-id="a8a56-147">The `#load` directive works only with *.csx* files, not with *.cs* files.</span></span>

## <a name="binding-to-method-return-value"></a><span data-ttu-id="a8a56-148">Binding to method return value</span><span class="sxs-lookup"><span data-stu-id="a8a56-148">Binding to method return value</span></span>

<span data-ttu-id="a8a56-149">You can use a method return value for an output binding, by using the name `$return` in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="a8a56-149">You can use a method return value for an output binding, by using the name `$return` in *function.json*.</span></span> <span data-ttu-id="a8a56-150">For examples, see [Triggers and bindings](functions-triggers-bindings.md#using-the-function-return-value).</span><span class="sxs-lookup"><span data-stu-id="a8a56-150">For examples, see [Triggers and bindings](functions-triggers-bindings.md#using-the-function-return-value).</span></span>

<span data-ttu-id="a8a56-151">Use the return value only if a successful function execution always results in a return value to pass to the output binding.</span><span class="sxs-lookup"><span data-stu-id="a8a56-151">Use the return value only if a successful function execution always results in a return value to pass to the output binding.</span></span> <span data-ttu-id="a8a56-152">Otherwise, use `ICollector` or `IAsyncCollector`, as shown in the following section.</span><span class="sxs-lookup"><span data-stu-id="a8a56-152">Otherwise, use `ICollector` or `IAsyncCollector`, as shown in the following section.</span></span>

## <a name="writing-multiple-output-values"></a><span data-ttu-id="a8a56-153">Writing multiple output values</span><span class="sxs-lookup"><span data-stu-id="a8a56-153">Writing multiple output values</span></span>

<span data-ttu-id="a8a56-154">To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span><span class="sxs-lookup"><span data-stu-id="a8a56-154">To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="a8a56-155">These types are write-only collections that are written to the output binding when the method completes.</span><span class="sxs-lookup"><span data-stu-id="a8a56-155">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="a8a56-156">This example writes multiple queue messages into the same queue using `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="a8a56-156">This example writes multiple queue messages into the same queue using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueue, TraceWriter log)
{
    myQueue.Add("Hello");
    myQueue.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="a8a56-157">Logging</span><span class="sxs-lookup"><span data-stu-id="a8a56-157">Logging</span></span>

<span data-ttu-id="a8a56-158">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-158">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="a8a56-159">We recommend that you name it `log`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-159">We recommend that you name it `log`.</span></span> <span data-ttu-id="a8a56-160">Avoid using `Console.Write` in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a8a56-160">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="a8a56-161">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="a8a56-161">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="a8a56-162">The log level for `TraceWriter` can be configured in [host.json](functions-host-json.md).</span><span class="sxs-lookup"><span data-stu-id="a8a56-162">The log level for `TraceWriter` can be configured in [host.json](functions-host-json.md).</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

> [!NOTE]
> <span data-ttu-id="a8a56-163">For information about a newer logging framework that you can use instead of `TraceWriter`, see [Write logs in C# functions](functions-monitoring.md#write-logs-in-c-functions) in the **Monitor Azure Functions** article.</span><span class="sxs-lookup"><span data-stu-id="a8a56-163">For information about a newer logging framework that you can use instead of `TraceWriter`, see [Write logs in C# functions](functions-monitoring.md#write-logs-in-c-functions) in the **Monitor Azure Functions** article.</span></span>

## <a name="async"></a><span data-ttu-id="a8a56-164">Async</span><span class="sxs-lookup"><span data-stu-id="a8a56-164">Async</span></span>

<span data-ttu-id="a8a56-165">To make a function [asynchronous](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/), use the `async` keyword and return a `Task` object.</span><span class="sxs-lookup"><span data-stu-id="a8a56-165">To make a function [asynchronous](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/), use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096);
}
```

<span data-ttu-id="a8a56-166">You can't use `out` parameters in async functions.</span><span class="sxs-lookup"><span data-stu-id="a8a56-166">You can't use `out` parameters in async functions.</span></span> <span data-ttu-id="a8a56-167">For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.</span><span class="sxs-lookup"><span data-stu-id="a8a56-167">For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.</span></span>

## <a name="cancellation-tokens"></a><span data-ttu-id="a8a56-168">Cancellation tokens</span><span class="sxs-lookup"><span data-stu-id="a8a56-168">Cancellation tokens</span></span>

<span data-ttu-id="a8a56-169">A function can accept a [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) parameter, which enables the operating system to notify your code when the function is about to be terminated.</span><span class="sxs-lookup"><span data-stu-id="a8a56-169">A function can accept a [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) parameter, which enables the operating system to notify your code when the function is about to be terminated.</span></span> <span data-ttu-id="a8a56-170">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span><span class="sxs-lookup"><span data-stu-id="a8a56-170">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="a8a56-171">The following example shows how to check for impending function termination.</span><span class="sxs-lookup"><span data-stu-id="a8a56-171">The following example shows how to check for impending function termination.</span></span>

```csharp
using System;
using System.IO;
using System.Threading;

public static void Run(
    string inputText,
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
```

## <a name="importing-namespaces"></a><span data-ttu-id="a8a56-172">Importing namespaces</span><span class="sxs-lookup"><span data-stu-id="a8a56-172">Importing namespaces</span></span>

<span data-ttu-id="a8a56-173">If you need to import namespaces, you can do so as usual, with the `using` clause.</span><span class="sxs-lookup"><span data-stu-id="a8a56-173">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="a8a56-174">The following namespaces are automatically imported and are therefore optional:</span><span class="sxs-lookup"><span data-stu-id="a8a56-174">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="a8a56-175">Referencing external assemblies</span><span class="sxs-lookup"><span data-stu-id="a8a56-175">Referencing external assemblies</span></span>

<span data-ttu-id="a8a56-176">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span><span class="sxs-lookup"><span data-stu-id="a8a56-176">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="a8a56-177">The following assemblies are automatically added by the Azure Functions hosting environment:</span><span class="sxs-lookup"><span data-stu-id="a8a56-177">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="a8a56-178">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="a8a56-178">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="a8a56-179">Referencing custom assemblies</span><span class="sxs-lookup"><span data-stu-id="a8a56-179">Referencing custom assemblies</span></span>

<span data-ttu-id="a8a56-180">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span><span class="sxs-lookup"><span data-stu-id="a8a56-180">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="a8a56-181">Shared assemblies are shared across all functions within a function app.</span><span class="sxs-lookup"><span data-stu-id="a8a56-181">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="a8a56-182">To reference a custom assembly, upload the assembly to a folder named `bin` in your [function app root folder](functions-reference.md#folder-structure) (wwwroot).</span><span class="sxs-lookup"><span data-stu-id="a8a56-182">To reference a custom assembly, upload the assembly to a folder named `bin` in your [function app root folder](functions-reference.md#folder-structure) (wwwroot).</span></span> 
- <span data-ttu-id="a8a56-183">Private assemblies are part of a given function's context, and support side-loading of different versions.</span><span class="sxs-lookup"><span data-stu-id="a8a56-183">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="a8a56-184">Private assemblies should be uploaded in a `bin` folder in the function directory.</span><span class="sxs-lookup"><span data-stu-id="a8a56-184">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="a8a56-185">Reference the assemblies using the file name, such as `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-185">Reference the assemblies using the file name, such as `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="a8a56-186">For information on how to upload files to your function folder, see the section on [package management](#using-nuget-packages).</span><span class="sxs-lookup"><span data-stu-id="a8a56-186">For information on how to upload files to your function folder, see the section on [package management](#using-nuget-packages).</span></span>

### <a name="watched-directories"></a><span data-ttu-id="a8a56-187">Watched directories</span><span class="sxs-lookup"><span data-stu-id="a8a56-187">Watched directories</span></span>

<span data-ttu-id="a8a56-188">The directory that contains the function script file is automatically watched for changes to assemblies.</span><span class="sxs-lookup"><span data-stu-id="a8a56-188">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="a8a56-189">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host.json](functions-host-json.md).</span><span class="sxs-lookup"><span data-stu-id="a8a56-189">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host.json](functions-host-json.md).</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="a8a56-190">Using NuGet packages</span><span class="sxs-lookup"><span data-stu-id="a8a56-190">Using NuGet packages</span></span>

<span data-ttu-id="a8a56-191">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span><span class="sxs-lookup"><span data-stu-id="a8a56-191">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="a8a56-192">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="a8a56-192">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="a8a56-193">In Azure Functions 1.x, only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span><span class="sxs-lookup"><span data-stu-id="a8a56-193">In Azure Functions 1.x, only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="a8a56-194">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span><span class="sxs-lookup"><span data-stu-id="a8a56-194">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="a8a56-195">You don't need to add `#r "AssemblyName"` directives.</span><span class="sxs-lookup"><span data-stu-id="a8a56-195">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="a8a56-196">To use the types defined in the NuGet packages; just add the required `using` statements to your *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-196">To use the types defined in the NuGet packages; just add the required `using` statements to your *run.csx* file.</span></span> 

<span data-ttu-id="a8a56-197">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-197">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="a8a56-198">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span><span class="sxs-lookup"><span data-stu-id="a8a56-198">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="a8a56-199">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span><span class="sxs-lookup"><span data-stu-id="a8a56-199">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="a8a56-200">Therefore, `project.lock.json` should not be deployed, as it causes NuGet to skip package restore.</span><span class="sxs-lookup"><span data-stu-id="a8a56-200">Therefore, `project.lock.json` should not be deployed, as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="a8a56-201">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span><span class="sxs-lookup"><span data-stu-id="a8a56-201">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="a8a56-202">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span><span class="sxs-lookup"><span data-stu-id="a8a56-202">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="a8a56-203">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="a8a56-203">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="a8a56-204">Using a project.json file</span><span class="sxs-lookup"><span data-stu-id="a8a56-204">Using a project.json file</span></span>

1. <span data-ttu-id="a8a56-205">Open the function in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8a56-205">Open the function in the Azure portal.</span></span> <span data-ttu-id="a8a56-206">The logs tab displays the package installation output.</span><span class="sxs-lookup"><span data-stu-id="a8a56-206">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="a8a56-207">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span><span class="sxs-lookup"><span data-stu-id="a8a56-207">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="a8a56-208">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span><span class="sxs-lookup"><span data-stu-id="a8a56-208">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="a8a56-209">Environment variables</span><span class="sxs-lookup"><span data-stu-id="a8a56-209">Environment variables</span></span>

<span data-ttu-id="a8a56-210">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span><span class="sxs-lookup"><span data-stu-id="a8a56-210">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
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
```

<span data-ttu-id="a8a56-211">The [System.Configuration.ConfigurationManager.AppSettings](https://docs.microsoft.com/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable` as shown here.</span><span class="sxs-lookup"><span data-stu-id="a8a56-211">The [System.Configuration.ConfigurationManager.AppSettings](https://docs.microsoft.com/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable` as shown here.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime"></a><span data-ttu-id="a8a56-212">Binding at runtime</span><span class="sxs-lookup"><span data-stu-id="a8a56-212">Binding at runtime</span></span>

<span data-ttu-id="a8a56-213">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="a8a56-213">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="a8a56-214">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span><span class="sxs-lookup"><span data-stu-id="a8a56-214">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="a8a56-215">With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.</span><span class="sxs-lookup"><span data-stu-id="a8a56-215">With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.</span></span>

<span data-ttu-id="a8a56-216">Define an imperative binding as follows:</span><span class="sxs-lookup"><span data-stu-id="a8a56-216">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="a8a56-217">**Do not** include an entry in *function.json* for your desired imperative bindings.</span><span class="sxs-lookup"><span data-stu-id="a8a56-217">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="a8a56-218">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="a8a56-218">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="a8a56-219">Use the following C# pattern to perform the data binding.</span><span class="sxs-lookup"><span data-stu-id="a8a56-219">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="a8a56-220">`BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is an input or output type that's supported by that binding type.</span><span class="sxs-lookup"><span data-stu-id="a8a56-220">`BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is an input or output type that's supported by that binding type.</span></span> <span data-ttu-id="a8a56-221">`T` cannot be an `out` parameter type (such as `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="a8a56-221">`T` cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="a8a56-222">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-222">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

### <a name="single-attribute-example"></a><span data-ttu-id="a8a56-223">Single attribute example</span><span class="sxs-lookup"><span data-stu-id="a8a56-223">Single attribute example</span></span>

<span data-ttu-id="a8a56-224">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#output) with blob path that's defined at run time, then writes a string to the blob.</span><span class="sxs-lookup"><span data-stu-id="a8a56-224">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#output) with blob path that's defined at run time, then writes a string to the blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="a8a56-225">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span><span class="sxs-lookup"><span data-stu-id="a8a56-225">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>

### <a name="multiple-attribute-example"></a><span data-ttu-id="a8a56-226">Multiple attribute example</span><span class="sxs-lookup"><span data-stu-id="a8a56-226">Multiple attribute example</span></span>

<span data-ttu-id="a8a56-227">The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="a8a56-227">The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="a8a56-228">You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-228">You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="a8a56-229">Use a `Binder` parameter, not `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="a8a56-229">Use a `Binder` parameter, not `IBinder`.</span></span>  <span data-ttu-id="a8a56-230">For example:</span><span class="sxs-lookup"><span data-stu-id="a8a56-230">For example:</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="a8a56-231">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span><span class="sxs-lookup"><span data-stu-id="a8a56-231">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="a8a56-232">Binding</span><span class="sxs-lookup"><span data-stu-id="a8a56-232">Binding</span></span> | <span data-ttu-id="a8a56-233">Attribute</span><span class="sxs-lookup"><span data-stu-id="a8a56-233">Attribute</span></span> | <span data-ttu-id="a8a56-234">Add reference</span><span class="sxs-lookup"><span data-stu-id="a8a56-234">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="a8a56-235">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a8a56-235">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.CosmosDB"` |
| <span data-ttu-id="a8a56-236">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a8a56-236">Event Hubs</span></span> | <span data-ttu-id="a8a56-237">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a8a56-237">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="a8a56-238">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="a8a56-238">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="a8a56-239">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="a8a56-239">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="a8a56-240">Service Bus</span><span class="sxs-lookup"><span data-stu-id="a8a56-240">Service Bus</span></span> | <span data-ttu-id="a8a56-241">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a8a56-241">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="a8a56-242">Storage queue</span><span class="sxs-lookup"><span data-stu-id="a8a56-242">Storage queue</span></span> | <span data-ttu-id="a8a56-243">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a8a56-243">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a8a56-244">Storage blob</span><span class="sxs-lookup"><span data-stu-id="a8a56-244">Storage blob</span></span> | <span data-ttu-id="a8a56-245">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a8a56-245">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a8a56-246">Storage table</span><span class="sxs-lookup"><span data-stu-id="a8a56-246">Storage table</span></span> | <span data-ttu-id="a8a56-247">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a8a56-247">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a8a56-248">Twilio</span><span class="sxs-lookup"><span data-stu-id="a8a56-248">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |

## <a name="next-steps"></a><span data-ttu-id="a8a56-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8a56-249">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8a56-250">Learn more about triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="a8a56-250">Learn more about triggers and bindings</span></span>](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8a56-251">Learn more about best practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a8a56-251">Learn more about best practices for Azure Functions</span></span>](functions-best-practices.md)
