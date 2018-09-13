---
title: Azure Functions developer reference | Microsoft Docs
description: Understand how to develop Azure Functions using C#.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/04/2017
ms.author: chrande
ms.openlocfilehash: 76b43c78341abb638e2ede97f68c05ee6df0700f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549553"
---
# <a name="azure-functions-c-developer-reference"></a><span data-ttu-id="3650d-104">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="3650d-104">Azure Functions C# developer reference</span></span>
> [!div class="op_single_selector"]
> * [C# script](functions-reference-csharp.md)
> * [F# script](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

<span data-ttu-id="3650d-108">The C# experience for Azure Functions is based on the Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="3650d-108">The C# experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="3650d-109">Data flows into your C# function via method arguments.</span><span class="sxs-lookup"><span data-stu-id="3650d-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="3650d-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span><span class="sxs-lookup"><span data-stu-id="3650d-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="3650d-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3650d-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="3650d-112">How .csx works</span><span class="sxs-lookup"><span data-stu-id="3650d-112">How .csx works</span></span>
<span data-ttu-id="3650d-113">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span><span class="sxs-lookup"><span data-stu-id="3650d-113">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="3650d-114">For Azure Functions, you just include any assembly references and namespaces you need up top, as usual, and instead of wrapping everything in a namespace and class, you can just define your `Run` method.</span><span class="sxs-lookup"><span data-stu-id="3650d-114">For Azure Functions, you just include any assembly references and namespaces you need up top, as usual, and instead of wrapping everything in a namespace and class, you can just define your `Run` method.</span></span> <span data-ttu-id="3650d-115">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span><span class="sxs-lookup"><span data-stu-id="3650d-115">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="3650d-116">Binding to arguments</span><span class="sxs-lookup"><span data-stu-id="3650d-116">Binding to arguments</span></span>
<span data-ttu-id="3650d-117">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span><span class="sxs-lookup"><span data-stu-id="3650d-117">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="3650d-118">Each binding has its own supported types which is documented per binding; for instance, a blob trigger can support a string, a POCO, or several other types.</span><span class="sxs-lookup"><span data-stu-id="3650d-118">Each binding has its own supported types which is documented per binding; for instance, a blob trigger can support a string, a POCO, or several other types.</span></span> <span data-ttu-id="3650d-119">You can use the type which best suits your need.</span><span class="sxs-lookup"><span data-stu-id="3650d-119">You can use the type which best suits your need.</span></span> <span data-ttu-id="3650d-120">A POCO object must have a getter and setter defined for each property.</span><span class="sxs-lookup"><span data-stu-id="3650d-120">A POCO object must have a getter and setter defined for each property.</span></span> 

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

> [!TIP]
>
> If you plan to use the HTTP or WebHook bindings, we suggest reading this best practices document on [HTTPClient](https://github.com/mspnp/performance-optimization/blob/master/ImproperInstantiation/docs/ImproperInstantiation.md).
>

## <a name="logging"></a><span data-ttu-id="3650d-122">Logging</span><span class="sxs-lookup"><span data-stu-id="3650d-122">Logging</span></span>
<span data-ttu-id="3650d-123">To log output to your streaming logs in C#, you can include a `TraceWriter` typed argument.</span><span class="sxs-lookup"><span data-stu-id="3650d-123">To log output to your streaming logs in C#, you can include a `TraceWriter` typed argument.</span></span> <span data-ttu-id="3650d-124">We recommend that you name it `log`.</span><span class="sxs-lookup"><span data-stu-id="3650d-124">We recommend that you name it `log`.</span></span> <span data-ttu-id="3650d-125">We recommend you avoid `Console.Write` in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3650d-125">We recommend you avoid `Console.Write` in Azure Functions.</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="3650d-126">Async</span><span class="sxs-lookup"><span data-stu-id="3650d-126">Async</span></span>
<span data-ttu-id="3650d-127">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span><span class="sxs-lookup"><span data-stu-id="3650d-127">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName, 
        Stream blobInput,
        Stream blobOutput)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="cancellation-token"></a><span data-ttu-id="3650d-128">Cancellation Token</span><span class="sxs-lookup"><span data-stu-id="3650d-128">Cancellation Token</span></span>
<span data-ttu-id="3650d-129">In certain cases, you may have operations which are sensitive to being shut down.</span><span class="sxs-lookup"><span data-stu-id="3650d-129">In certain cases, you may have operations which are sensitive to being shut down.</span></span> <span data-ttu-id="3650d-130">While it's always best to write code which can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span><span class="sxs-lookup"><span data-stu-id="3650d-130">While it's always best to write code which can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="3650d-131">A `CancellationToken` will be provided if a host shutdown is triggered.</span><span class="sxs-lookup"><span data-stu-id="3650d-131">A `CancellationToken` will be provided if a host shutdown is triggered.</span></span> 

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName, 
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="3650d-132">Importing namespaces</span><span class="sxs-lookup"><span data-stu-id="3650d-132">Importing namespaces</span></span>
<span data-ttu-id="3650d-133">If you need to import namespaces, you can do so as usual, with the `using` clause.</span><span class="sxs-lookup"><span data-stu-id="3650d-133">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="3650d-134">The following namespaces are automatically imported and are therefore optional:</span><span class="sxs-lookup"><span data-stu-id="3650d-134">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="3650d-135">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="3650d-135">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="3650d-136">Referencing External Assemblies</span><span class="sxs-lookup"><span data-stu-id="3650d-136">Referencing External Assemblies</span></span>
<span data-ttu-id="3650d-137">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span><span class="sxs-lookup"><span data-stu-id="3650d-137">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="3650d-138">The following assemblies are automatically added by the Azure Functions hosting environment:</span><span class="sxs-lookup"><span data-stu-id="3650d-138">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="3650d-139">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="3650d-139">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="3650d-140">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="3650d-140">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="3650d-141">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="3650d-141">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

<span data-ttu-id="3650d-142">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="3650d-142">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="3650d-143">For information on how to upload files to your function folder, see the following section on package management.</span><span class="sxs-lookup"><span data-stu-id="3650d-143">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="package-management"></a><span data-ttu-id="3650d-144">Package management</span><span class="sxs-lookup"><span data-stu-id="3650d-144">Package management</span></span>
<span data-ttu-id="3650d-145">To use NuGet packages in a C# function, upload a *project.json* file to the the function's folder in the function app's file system.</span><span class="sxs-lookup"><span data-stu-id="3650d-145">To use NuGet packages in a C# function, upload a *project.json* file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="3650d-146">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="3650d-146">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="3650d-147">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span><span class="sxs-lookup"><span data-stu-id="3650d-147">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="3650d-148">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span><span class="sxs-lookup"><span data-stu-id="3650d-148">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="3650d-149">You don't need to add `#r "AssemblyName"` directives.</span><span class="sxs-lookup"><span data-stu-id="3650d-149">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="3650d-150">Just add the required `using` statements to your *run.csx* file to use the types defined in the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="3650d-150">Just add the required `using` statements to your *run.csx* file to use the types defined in the NuGet packages.</span></span>

<span data-ttu-id="3650d-151">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="3650d-151">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="3650d-152">If the date and time stamps of the files do not match, a NuGet restore runs and NuGet downloads updated packages.</span><span class="sxs-lookup"><span data-stu-id="3650d-152">If the date and time stamps of the files do not match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="3650d-153">However, if the date and time stamps of the files match, NuGet does not perform a restore.</span><span class="sxs-lookup"><span data-stu-id="3650d-153">However, if the date and time stamps of the files match, NuGet does not perform a restore.</span></span> <span data-ttu-id="3650d-154">Therefore, `project.lock.json` should not be deployed as this causes NuGet to skip the restore, and the function will not have the required packages.</span><span class="sxs-lookup"><span data-stu-id="3650d-154">Therefore, `project.lock.json` should not be deployed as this causes NuGet to skip the restore, and the function will not have the required packages.</span></span> <span data-ttu-id="3650d-155">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span><span class="sxs-lookup"><span data-stu-id="3650d-155">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

### <a name="how-to-upload-a-projectjson-file"></a><span data-ttu-id="3650d-156">How to upload a project.json file</span><span class="sxs-lookup"><span data-stu-id="3650d-156">How to upload a project.json file</span></span>
1. <span data-ttu-id="3650d-157">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3650d-157">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> 
   
    <span data-ttu-id="3650d-158">This also gives access to the streaming logs where package installation output will be displayed.</span><span class="sxs-lookup"><span data-stu-id="3650d-158">This also gives access to the streaming logs where package installation output will be displayed.</span></span> 
2. <span data-ttu-id="3650d-159">To upload a project.json file, use one of the methods described in the **How to update function app files** section of the [Azure Functions developer reference topic](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="3650d-159">To upload a project.json file, use one of the methods described in the **How to update function app files** section of the [Azure Functions developer reference topic](functions-reference.md#fileupdate).</span></span> 
3. <span data-ttu-id="3650d-160">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span><span class="sxs-lookup"><span data-stu-id="3650d-160">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="3650d-161">Environment variables</span><span class="sxs-lookup"><span data-stu-id="3650d-161">Environment variables</span></span>
<span data-ttu-id="3650d-162">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span><span class="sxs-lookup"><span data-stu-id="3650d-162">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="3650d-163">Reusing .csx code</span><span class="sxs-lookup"><span data-stu-id="3650d-163">Reusing .csx code</span></span>
<span data-ttu-id="3650d-164">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="3650d-164">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="3650d-165">To do that, use `#load` directives in your *run.csx* file.</span><span class="sxs-lookup"><span data-stu-id="3650d-165">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="3650d-166">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span><span class="sxs-lookup"><span data-stu-id="3650d-166">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span> 

<span data-ttu-id="3650d-167">Example *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="3650d-167">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}"); 
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="3650d-168">Example *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="3650d-168">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext); 
}
```

<span data-ttu-id="3650d-169">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span><span class="sxs-lookup"><span data-stu-id="3650d-169">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="3650d-170">In the following simplified example, a HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span><span class="sxs-lookup"><span data-stu-id="3650d-170">In the following simplified example, a HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="3650d-171">Example *run.csx* for HTTP trigger:</span><span class="sxs-lookup"><span data-stu-id="3650d-171">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="3650d-172">Example *run.csx* for queue trigger:</span><span class="sxs-lookup"><span data-stu-id="3650d-172">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="3650d-173">Example *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="3650d-173">Example *order.csx*:</span></span> 

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

<span data-ttu-id="3650d-174">You can use a relative path with the `#load` directive:</span><span class="sxs-lookup"><span data-stu-id="3650d-174">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="3650d-175">`#load "mylogger.csx"` loads a file located in the function folder.</span><span class="sxs-lookup"><span data-stu-id="3650d-175">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="3650d-176">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span><span class="sxs-lookup"><span data-stu-id="3650d-176">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="3650d-177">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="3650d-177">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="3650d-178">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span><span class="sxs-lookup"><span data-stu-id="3650d-178">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span> 

## <a name="versioning"></a><span data-ttu-id="3650d-179">Versioning</span><span class="sxs-lookup"><span data-stu-id="3650d-179">Versioning</span></span>

<span data-ttu-id="3650d-180">The Functions runtime runs as a site extension to your Function App.</span><span class="sxs-lookup"><span data-stu-id="3650d-180">The Functions runtime runs as a site extension to your Function App.</span></span> <span data-ttu-id="3650d-181">Site extensions are extensibility points that enable you to add features to an Azure App Service, Website, or Function App.</span><span class="sxs-lookup"><span data-stu-id="3650d-181">Site extensions are extensibility points that enable you to add features to an Azure App Service, Website, or Function App.</span></span> <span data-ttu-id="3650d-182">`Kudu` and `Monaco` are two examples of site extensions, and you may create and use custom extensions as well.</span><span class="sxs-lookup"><span data-stu-id="3650d-182">`Kudu` and `Monaco` are two examples of site extensions, and you may create and use custom extensions as well.</span></span> <span data-ttu-id="3650d-183">You can configure the version of the extensions using the `FUNCTIONS_EXTENSION_VERSION` app setting.</span><span class="sxs-lookup"><span data-stu-id="3650d-183">You can configure the version of the extensions using the `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span>

<span data-ttu-id="3650d-184">The `FUNCTIONS_EXTENSION_VERSION` only sets the major version of the runtime.</span><span class="sxs-lookup"><span data-stu-id="3650d-184">The `FUNCTIONS_EXTENSION_VERSION` only sets the major version of the runtime.</span></span> <span data-ttu-id="3650d-185">For example, the value "~1" indicates that your Function App will use 1 as its major version.</span><span class="sxs-lookup"><span data-stu-id="3650d-185">For example, the value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="3650d-186">Function Apps are upgraded to each new minor version as they are released.</span><span class="sxs-lookup"><span data-stu-id="3650d-186">Function Apps are upgraded to each new minor version as they are released.</span></span> <span data-ttu-id="3650d-187">This allows you manage when to upgrade to versions to avoid breaking changes.</span><span class="sxs-lookup"><span data-stu-id="3650d-187">This allows you manage when to upgrade to versions to avoid breaking changes.</span></span>

<span data-ttu-id="3650d-188">Additionally, you may want to upgrade the runtime before it becomes the default version in the portal.</span><span class="sxs-lookup"><span data-stu-id="3650d-188">Additionally, you may want to upgrade the runtime before it becomes the default version in the portal.</span></span> <span data-ttu-id="3650d-189">Don't worry though, you can roll back at any time by reverting the `FUNCTIONS_EXTENSION_VERSION` setting to its old value.</span><span class="sxs-lookup"><span data-stu-id="3650d-189">Don't worry though, you can roll back at any time by reverting the `FUNCTIONS_EXTENSION_VERSION` setting to its old value.</span></span>

<span data-ttu-id="3650d-190">*To determine your Azure Function App's runtime version:*</span><span class="sxs-lookup"><span data-stu-id="3650d-190">*To determine your Azure Function App's runtime version:*</span></span>

<span data-ttu-id="3650d-191">Locate the `applicationhost.config` file located in the `D:\local\Config` folder in Kudu.</span><span class="sxs-lookup"><span data-stu-id="3650d-191">Locate the `applicationhost.config` file located in the `D:\local\Config` folder in Kudu.</span></span> <span data-ttu-id="3650d-192">The `virtualDirectory` entry reveals the exact Functions runtime version:</span><span class="sxs-lookup"><span data-stu-id="3650d-192">The `virtualDirectory` entry reveals the exact Functions runtime version:</span></span> 

```xml
<virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Functions\0.8.10564" />
```
<span data-ttu-id="3650d-193">You may use this value to set a specific major and minor runtime version of your Function App.</span><span class="sxs-lookup"><span data-stu-id="3650d-193">You may use this value to set a specific major and minor runtime version of your Function App.</span></span> <span data-ttu-id="3650d-194">Whenever you change the version of a Function App you must restart it.</span><span class="sxs-lookup"><span data-stu-id="3650d-194">Whenever you change the version of a Function App you must restart it.</span></span>

## <a name="advanced-binding-at-runtime-imperative-binding"></a><span data-ttu-id="3650d-195">Advanced binding at runtime (imperative binding)</span><span class="sxs-lookup"><span data-stu-id="3650d-195">Advanced binding at runtime (imperative binding)</span></span>

<span data-ttu-id="3650d-196">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="3650d-196">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="3650d-197">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span><span class="sxs-lookup"><span data-stu-id="3650d-197">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="3650d-198">With this patttern, you can bind to any number of supported input and output binding on-the-fly in your function code.</span><span class="sxs-lookup"><span data-stu-id="3650d-198">With this patttern, you can bind to any number of supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="3650d-199">Define an imperative binding as follows:</span><span class="sxs-lookup"><span data-stu-id="3650d-199">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="3650d-200">**Do not** include an entry in *function.json* for your desired imperative bindings.</span><span class="sxs-lookup"><span data-stu-id="3650d-200">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="3650d-201">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="3650d-201">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span> 
- <span data-ttu-id="3650d-202">Use the following C# pattern to perform the data binding.</span><span class="sxs-lookup"><span data-stu-id="3650d-202">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="3650d-203">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span><span class="sxs-lookup"><span data-stu-id="3650d-203">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="3650d-204">`T` also cannot be an `out` parameter type (such as `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="3650d-204">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="3650d-205">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span><span class="sxs-lookup"><span data-stu-id="3650d-205">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>
    
<span data-ttu-id="3650d-206">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#storage-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span><span class="sxs-lookup"><span data-stu-id="3650d-206">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#storage-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="3650d-207">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span><span class="sxs-lookup"><span data-stu-id="3650d-207">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="3650d-208">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="3650d-208">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="3650d-209">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="3650d-209">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="3650d-210">For example,</span><span class="sxs-lookup"><span data-stu-id="3650d-210">For example,</span></span>

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

<span data-ttu-id="3650d-211">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span><span class="sxs-lookup"><span data-stu-id="3650d-211">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span> 

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="3650d-212">Binding</span><span class="sxs-lookup"><span data-stu-id="3650d-212">Binding</span></span> | <span data-ttu-id="3650d-213">Attribute</span><span class="sxs-lookup"><span data-stu-id="3650d-213">Attribute</span></span> | <span data-ttu-id="3650d-214">Add reference</span><span class="sxs-lookup"><span data-stu-id="3650d-214">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="3650d-215">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3650d-215">DocumentDB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="3650d-216">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3650d-216">Event Hubs</span></span> | <span data-ttu-id="3650d-217">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="3650d-217">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="3650d-218">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3650d-218">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="3650d-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="3650d-219">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="3650d-220">Service Bus</span><span class="sxs-lookup"><span data-stu-id="3650d-220">Service Bus</span></span> | <span data-ttu-id="3650d-221">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="3650d-221">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="3650d-222">Storage queue</span><span class="sxs-lookup"><span data-stu-id="3650d-222">Storage queue</span></span> | <span data-ttu-id="3650d-223">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="3650d-223">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="3650d-224">Storage blob</span><span class="sxs-lookup"><span data-stu-id="3650d-224">Storage blob</span></span> | <span data-ttu-id="3650d-225">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="3650d-225">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="3650d-226">Storage table</span><span class="sxs-lookup"><span data-stu-id="3650d-226">Storage table</span></span> | <span data-ttu-id="3650d-227">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="3650d-227">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="3650d-228">Twilio</span><span class="sxs-lookup"><span data-stu-id="3650d-228">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="3650d-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="3650d-229">Next steps</span></span>
<span data-ttu-id="3650d-230">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="3650d-230">For more information, see the following resources:</span></span>

* [<span data-ttu-id="3650d-231">Best Practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3650d-231">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="3650d-232">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="3650d-232">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="3650d-233">Azure Functions F# developer reference</span><span class="sxs-lookup"><span data-stu-id="3650d-233">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="3650d-234">Azure Functions NodeJS developer reference</span><span class="sxs-lookup"><span data-stu-id="3650d-234">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="3650d-235">Azure Functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="3650d-235">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

