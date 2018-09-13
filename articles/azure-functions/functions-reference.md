---
title: Guidance for developing Azure Functions | Microsoft Docs
description: Learn the Azure Functions concepts and techniques that you need to develop functions in Azure, across all programming languages and bindings.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: developer guide, azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/23/2017
ms.author: chrande
ms.openlocfilehash: adb70fc58321c11c0b57efc9810a44d0ab2c8a20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661214"
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="0c108-104">Azure Functions developers guide</span><span class="sxs-lookup"><span data-stu-id="0c108-104">Azure Functions developers guide</span></span>
<span data-ttu-id="0c108-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of the language or binding you use.</span><span class="sxs-lookup"><span data-stu-id="0c108-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of the language or binding you use.</span></span> <span data-ttu-id="0c108-106">Before you jump into learning details specific to a given language or binding, be sure to read through this overview that applies to all of them.</span><span class="sxs-lookup"><span data-stu-id="0c108-106">Before you jump into learning details specific to a given language or binding, be sure to read through this overview that applies to all of them.</span></span>

<span data-ttu-id="0c108-107">This article assumes that you've already read the [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and the JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0c108-107">This article assumes that you've already read the [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and the JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="0c108-108">Azure Functions is based on the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="0c108-108">Azure Functions is based on the WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="0c108-109">Function code</span><span class="sxs-lookup"><span data-stu-id="0c108-109">Function code</span></span>
<span data-ttu-id="0c108-110">A *function* is the primary concept in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0c108-110">A *function* is the primary concept in Azure Functions.</span></span> <span data-ttu-id="0c108-111">You write code for a function in a language of your choice and save the code and configuration files in the same folder.</span><span class="sxs-lookup"><span data-stu-id="0c108-111">You write code for a function in a language of your choice and save the code and configuration files in the same folder.</span></span> <span data-ttu-id="0c108-112">The configuration is named `function.json`, which contains JSON configuration data.</span><span class="sxs-lookup"><span data-stu-id="0c108-112">The configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="0c108-113">Various languages are supported, and each one has a slightly different experience optimized to work best for that language.</span><span class="sxs-lookup"><span data-stu-id="0c108-113">Various languages are supported, and each one has a slightly different experience optimized to work best for that language.</span></span> 

<span data-ttu-id="0c108-114">The function.json file defines the function bindings and other configuration settings.</span><span class="sxs-lookup"><span data-stu-id="0c108-114">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="0c108-115">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span><span class="sxs-lookup"><span data-stu-id="0c108-115">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="0c108-116">The following is an example function.json file.</span><span class="sxs-lookup"><span data-stu-id="0c108-116">The following is an example function.json file.</span></span>

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

<span data-ttu-id="0c108-117">Set the `disabled` property to `true` to prevent the function from being executed.</span><span class="sxs-lookup"><span data-stu-id="0c108-117">Set the `disabled` property to `true` to prevent the function from being executed.</span></span>

<span data-ttu-id="0c108-118">The `bindings` property is where you configure both triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="0c108-118">The `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="0c108-119">Each binding shares a few common settings and some settings, which are specific to a particular type of binding.</span><span class="sxs-lookup"><span data-stu-id="0c108-119">Each binding shares a few common settings and some settings, which are specific to a particular type of binding.</span></span> <span data-ttu-id="0c108-120">Every binding requires the following settings:</span><span class="sxs-lookup"><span data-stu-id="0c108-120">Every binding requires the following settings:</span></span>

| <span data-ttu-id="0c108-121">Property</span><span class="sxs-lookup"><span data-stu-id="0c108-121">Property</span></span> | <span data-ttu-id="0c108-122">Values/Types</span><span class="sxs-lookup"><span data-stu-id="0c108-122">Values/Types</span></span> | <span data-ttu-id="0c108-123">Comments</span><span class="sxs-lookup"><span data-stu-id="0c108-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="0c108-124">string</span><span class="sxs-lookup"><span data-stu-id="0c108-124">string</span></span> |<span data-ttu-id="0c108-125">Binding type.</span><span class="sxs-lookup"><span data-stu-id="0c108-125">Binding type.</span></span> <span data-ttu-id="0c108-126">For example, `queueTrigger`.</span><span class="sxs-lookup"><span data-stu-id="0c108-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="0c108-127">'in', 'out'</span><span class="sxs-lookup"><span data-stu-id="0c108-127">'in', 'out'</span></span> |<span data-ttu-id="0c108-128">Indicates whether the binding is for receiving data into the function or sending data from the function.</span><span class="sxs-lookup"><span data-stu-id="0c108-128">Indicates whether the binding is for receiving data into the function or sending data from the function.</span></span> |
| `name` |<span data-ttu-id="0c108-129">string</span><span class="sxs-lookup"><span data-stu-id="0c108-129">string</span></span> |<span data-ttu-id="0c108-130">The name that is used for the bound data in the function.</span><span class="sxs-lookup"><span data-stu-id="0c108-130">The name that is used for the bound data in the function.</span></span> <span data-ttu-id="0c108-131">For C#, this is an argument name; for JavaScript, it's the key in a key/value list.</span><span class="sxs-lookup"><span data-stu-id="0c108-131">For C#, this is an argument name; for JavaScript, it's the key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="0c108-132">Function app</span><span class="sxs-lookup"><span data-stu-id="0c108-132">Function app</span></span>
<span data-ttu-id="0c108-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c108-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="0c108-134">All of the functions in a function app share the same pricing plan, continuous deployment and runtime version.</span><span class="sxs-lookup"><span data-stu-id="0c108-134">All of the functions in a function app share the same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="0c108-135">Functions written in multiple languages can all share the same function app.</span><span class="sxs-lookup"><span data-stu-id="0c108-135">Functions written in multiple languages can all share the same function app.</span></span> <span data-ttu-id="0c108-136">Think of a function app as a way to organize and collectively manage your functions.</span><span class="sxs-lookup"><span data-stu-id="0c108-136">Think of a function app as a way to organize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="0c108-137">Runtime (script host and web host)</span><span class="sxs-lookup"><span data-stu-id="0c108-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="0c108-138">The runtime, or script host, is the underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span><span class="sxs-lookup"><span data-stu-id="0c108-138">The runtime, or script host, is the underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="0c108-139">To facilitate HTTP triggers, there is also a web host that is designed to sit in front of the script host in production scenarios.</span><span class="sxs-lookup"><span data-stu-id="0c108-139">To facilitate HTTP triggers, there is also a web host that is designed to sit in front of the script host in production scenarios.</span></span> <span data-ttu-id="0c108-140">Having two hosts helps to isolate the script host from the front end traffic managed by the web host.</span><span class="sxs-lookup"><span data-stu-id="0c108-140">Having two hosts helps to isolate the script host from the front end traffic managed by the web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="0c108-141">Folder Structure</span><span class="sxs-lookup"><span data-stu-id="0c108-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="0c108-142">When setting-up a project for deploying functions to a function app in Azure App Service, you can treat this folder structure as your site code.</span><span class="sxs-lookup"><span data-stu-id="0c108-142">When setting-up a project for deploying functions to a function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="0c108-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span><span class="sxs-lookup"><span data-stu-id="0c108-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="0c108-144">Make sure to deploy your `host.json` file and function folders directly to the `wwwroot` folder.</span><span class="sxs-lookup"><span data-stu-id="0c108-144">Make sure to deploy your `host.json` file and function folders directly to the `wwwroot` folder.</span></span> <span data-ttu-id="0c108-145">Do not include the `wwwroot` folder in your deployments.</span><span class="sxs-lookup"><span data-stu-id="0c108-145">Do not include the `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="0c108-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span><span class="sxs-lookup"><span data-stu-id="0c108-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <a id="fileupdate"></a> <span data-ttu-id="0c108-147">How to update function app files</span><span class="sxs-lookup"><span data-stu-id="0c108-147">How to update function app files</span></span>
<span data-ttu-id="0c108-148">The function editor built into the Azure portal lets you update the *function.json* file and the code file for a function.</span><span class="sxs-lookup"><span data-stu-id="0c108-148">The function editor built into the Azure portal lets you update the *function.json* file and the code file for a function.</span></span> <span data-ttu-id="0c108-149">To upload or update other files such as *package.json* or *project.json* or dependencies, you have to use other deployment methods.</span><span class="sxs-lookup"><span data-stu-id="0c108-149">To upload or update other files such as *package.json* or *project.json* or dependencies, you have to use other deployment methods.</span></span>

<span data-ttu-id="0c108-150">Function apps are built on App Service, so all the [deployment options available to standard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span><span class="sxs-lookup"><span data-stu-id="0c108-150">Function apps are built on App Service, so all the [deployment options available to standard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="0c108-151">Here are some methods you can use to upload or update function app files.</span><span class="sxs-lookup"><span data-stu-id="0c108-151">Here are some methods you can use to upload or update function app files.</span></span> 

#### <a name="to-use-app-service-editor"></a><span data-ttu-id="0c108-152">To use App Service Editor</span><span class="sxs-lookup"><span data-stu-id="0c108-152">To use App Service Editor</span></span>
1. <span data-ttu-id="0c108-153">In the Azure Functions portal, click **Function app settings**.</span><span class="sxs-lookup"><span data-stu-id="0c108-153">In the Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="0c108-154">In the **Advanced Settings** section, click **Go to App Service Settings**.</span><span class="sxs-lookup"><span data-stu-id="0c108-154">In the **Advanced Settings** section, click **Go to App Service Settings**.</span></span>
3. <span data-ttu-id="0c108-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span><span class="sxs-lookup"><span data-stu-id="0c108-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="0c108-156">click **Go**.</span><span class="sxs-lookup"><span data-stu-id="0c108-156">click **Go**.</span></span>
   
   <span data-ttu-id="0c108-157">After App Service Editor loads, you'll see the *host.json* file and function folders under *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="0c108-157">After App Service Editor loads, you'll see the *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="0c108-158">Open files to edit them, or drag and drop from your development machine to upload files.</span><span class="sxs-lookup"><span data-stu-id="0c108-158">Open files to edit them, or drag and drop from your development machine to upload files.</span></span>

#### <a name="to-use-the-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="0c108-159">To use the function app's SCM (Kudu) endpoint</span><span class="sxs-lookup"><span data-stu-id="0c108-159">To use the function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="0c108-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0c108-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="0c108-161">Click **Debug Console > CMD**.</span><span class="sxs-lookup"><span data-stu-id="0c108-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="0c108-162">Navigate to `D:\home\site\wwwroot\` to update *host.json* or `D:\home\site\wwwroot\<function_name>` to update a function's files.</span><span class="sxs-lookup"><span data-stu-id="0c108-162">Navigate to `D:\home\site\wwwroot\` to update *host.json* or `D:\home\site\wwwroot\<function_name>` to update a function's files.</span></span>
4. <span data-ttu-id="0c108-163">Drag-and-drop a file you want to upload into the appropriate folder in the file grid.</span><span class="sxs-lookup"><span data-stu-id="0c108-163">Drag-and-drop a file you want to upload into the appropriate folder in the file grid.</span></span> <span data-ttu-id="0c108-164">There are two areas in the file grid where you can drop a file.</span><span class="sxs-lookup"><span data-stu-id="0c108-164">There are two areas in the file grid where you can drop a file.</span></span> <span data-ttu-id="0c108-165">For *.zip* files, a box appears with the label "Drag here to upload and unzip."</span><span class="sxs-lookup"><span data-stu-id="0c108-165">For *.zip* files, a box appears with the label "Drag here to upload and unzip."</span></span> <span data-ttu-id="0c108-166">For other file types, drop in the file grid but outside the "unzip" box.</span><span class="sxs-lookup"><span data-stu-id="0c108-166">For other file types, drop in the file grid but outside the "unzip" box.</span></span>

#### <a name="to-use-ftp"></a><span data-ttu-id="0c108-167">To use FTP</span><span class="sxs-lookup"><span data-stu-id="0c108-167">To use FTP</span></span>
1. <span data-ttu-id="0c108-168">Follow the instructions [here](../app-service-web/web-sites-deploy.md#ftp) to get FTP configured.</span><span class="sxs-lookup"><span data-stu-id="0c108-168">Follow the instructions [here](../app-service-web/web-sites-deploy.md#ftp) to get FTP configured.</span></span>
2. <span data-ttu-id="0c108-169">When you're connected to the function app site, copy an updated *host.json* file to `/site/wwwroot` or copy function files to `/site/wwwroot/<function_name>`.</span><span class="sxs-lookup"><span data-stu-id="0c108-169">When you're connected to the function app site, copy an updated *host.json* file to `/site/wwwroot` or copy function files to `/site/wwwroot/<function_name>`.</span></span>

#### <a name="to-use-continuous-deployment"></a><span data-ttu-id="0c108-170">To use continuous deployment</span><span class="sxs-lookup"><span data-stu-id="0c108-170">To use continuous deployment</span></span>
<span data-ttu-id="0c108-171">Follow the instructions in the topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0c108-171">Follow the instructions in the topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="0c108-172">Parallel execution</span><span class="sxs-lookup"><span data-stu-id="0c108-172">Parallel execution</span></span>
<span data-ttu-id="0c108-173">When multiple triggering events occur faster than a single-threaded function runtime can process them, the runtime may invoke the function multiple times in parallel.</span><span class="sxs-lookup"><span data-stu-id="0c108-173">When multiple triggering events occur faster than a single-threaded function runtime can process them, the runtime may invoke the function multiple times in parallel.</span></span>  <span data-ttu-id="0c108-174">If a function app is using the [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), the function app could scale out automatically.</span><span class="sxs-lookup"><span data-stu-id="0c108-174">If a function app is using the [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), the function app could scale out automatically.</span></span>  <span data-ttu-id="0c108-175">Each instance of the function app, whether the app runs on the Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span><span class="sxs-lookup"><span data-stu-id="0c108-175">Each instance of the function app, whether the app runs on the Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="0c108-176">The maximum number of concurrent function invocations in each function app instance varies based on the type of trigger being used as well as the resources used by other functions within the function app.</span><span class="sxs-lookup"><span data-stu-id="0c108-176">The maximum number of concurrent function invocations in each function app instance varies based on the type of trigger being used as well as the resources used by other functions within the function app.</span></span>

## <a name="azure-functions-pulse"></a><span data-ttu-id="0c108-177">Azure Functions Pulse</span><span class="sxs-lookup"><span data-stu-id="0c108-177">Azure Functions Pulse</span></span>
<span data-ttu-id="0c108-178">Pulse is a live event stream that shows how often your function runs, as well as successes and failures.</span><span class="sxs-lookup"><span data-stu-id="0c108-178">Pulse is a live event stream that shows how often your function runs, as well as successes and failures.</span></span> <span data-ttu-id="0c108-179">You can also monitor your average execution time.</span><span class="sxs-lookup"><span data-stu-id="0c108-179">You can also monitor your average execution time.</span></span> <span data-ttu-id="0c108-180">We’ll be adding more features and customization to it over time.</span><span class="sxs-lookup"><span data-stu-id="0c108-180">We’ll be adding more features and customization to it over time.</span></span> <span data-ttu-id="0c108-181">You can access the **Pulse** page from the **Monitoring** tab.</span><span class="sxs-lookup"><span data-stu-id="0c108-181">You can access the **Pulse** page from the **Monitoring** tab.</span></span>

## <a name="repositories"></a><span data-ttu-id="0c108-182">Repositories</span><span class="sxs-lookup"><span data-stu-id="0c108-182">Repositories</span></span>
<span data-ttu-id="0c108-183">The code for Azure Functions is open source and stored in GitHub repositories:</span><span class="sxs-lookup"><span data-stu-id="0c108-183">The code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="0c108-184">Azure Functions runtime</span><span class="sxs-lookup"><span data-stu-id="0c108-184">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="0c108-185">Azure Functions portal</span><span class="sxs-lookup"><span data-stu-id="0c108-185">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="0c108-186">Azure Functions templates</span><span class="sxs-lookup"><span data-stu-id="0c108-186">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="0c108-187">Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="0c108-187">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="0c108-188">Azure WebJobs SDK Extensions</span><span class="sxs-lookup"><span data-stu-id="0c108-188">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="0c108-189">Bindings</span><span class="sxs-lookup"><span data-stu-id="0c108-189">Bindings</span></span>
<span data-ttu-id="0c108-190">Here is a table of all supported bindings.</span><span class="sxs-lookup"><span data-stu-id="0c108-190">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="0c108-191">Reporting Issues</span><span class="sxs-lookup"><span data-stu-id="0c108-191">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="0c108-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c108-192">Next steps</span></span>
<span data-ttu-id="0c108-193">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="0c108-193">For more information, see the following resources:</span></span>

* [<span data-ttu-id="0c108-194">Best Practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0c108-194">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="0c108-195">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="0c108-195">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="0c108-196">Azure Functions F# developer reference</span><span class="sxs-lookup"><span data-stu-id="0c108-196">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="0c108-197">Azure Functions NodeJS developer reference</span><span class="sxs-lookup"><span data-stu-id="0c108-197">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="0c108-198">Azure Functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="0c108-198">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="0c108-199">[Azure Functions: The Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on the Azure App Service team blog.</span><span class="sxs-lookup"><span data-stu-id="0c108-199">[Azure Functions: The Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on the Azure App Service team blog.</span></span> <span data-ttu-id="0c108-200">A history of how Azure Functions was developed.</span><span class="sxs-lookup"><span data-stu-id="0c108-200">A history of how Azure Functions was developed.</span></span>

