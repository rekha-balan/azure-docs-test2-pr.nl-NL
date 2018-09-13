---
title: Mobile Apps bindings for Azure Functions
description: Understand how to use Azure Mobile Apps bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: d43032f854aa37f150945c25515c03ec97277b41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810302"
---
# <a name="mobile-apps-bindings-for-azure-functions"></a><span data-ttu-id="439a5-104">Mobile Apps bindings for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="439a5-104">Mobile Apps bindings for Azure Functions</span></span> 

<span data-ttu-id="439a5-105">This article explains how to work with [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="439a5-105">This article explains how to work with [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="439a5-106">Azure Functions supports input and output bindings for Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="439a5-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="439a5-107">The Mobile Apps bindings let you read and update data tables in mobile apps.</span><span class="sxs-lookup"><span data-stu-id="439a5-107">The Mobile Apps bindings let you read and update data tables in mobile apps.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="439a5-108">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="439a5-108">Packages - Functions 1.x</span></span>

<span data-ttu-id="439a5-109">Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x.</span><span class="sxs-lookup"><span data-stu-id="439a5-109">Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x.</span></span> <span data-ttu-id="439a5-110">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="439a5-110">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="439a5-111">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="439a5-111">Packages - Functions 2.x</span></span>

<span data-ttu-id="439a5-112">Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="439a5-112">Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 3.x.</span></span> <span data-ttu-id="439a5-113">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="439a5-113">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="input"></a><span data-ttu-id="439a5-114">Input</span><span class="sxs-lookup"><span data-stu-id="439a5-114">Input</span></span>

<span data-ttu-id="439a5-115">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span><span class="sxs-lookup"><span data-stu-id="439a5-115">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="439a5-116">In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span><span class="sxs-lookup"><span data-stu-id="439a5-116">In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

## <a name="input---example"></a><span data-ttu-id="439a5-117">Input - example</span><span class="sxs-lookup"><span data-stu-id="439a5-117">Input - example</span></span>

<span data-ttu-id="439a5-118">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="439a5-118">See the language-specific example:</span></span>

* [<span data-ttu-id="439a5-119">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="439a5-119">C# script (.csx)</span></span>](#input---c-script-example)
* [<span data-ttu-id="439a5-120">JavaScript</span><span class="sxs-lookup"><span data-stu-id="439a5-120">JavaScript</span></span>](#input---javascript-example)

### <a name="input---c-script-example"></a><span data-ttu-id="439a5-121">Input - C# script example</span><span class="sxs-lookup"><span data-stu-id="439a5-121">Input - C# script example</span></span>

<span data-ttu-id="439a5-122">The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-122">The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="439a5-123">The function is triggered by a queue message that has a record identifier.</span><span class="sxs-lookup"><span data-stu-id="439a5-123">The function is triggered by a queue message that has a record identifier.</span></span> <span data-ttu-id="439a5-124">The function reads the specified record and modifies its `Text` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-124">The function reads the specified record and modifies its `Text` property.</span></span>

<span data-ttu-id="439a5-125">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="439a5-125">Here's the binding data in the *function.json* file:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```
<span data-ttu-id="439a5-126">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="439a5-126">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="439a5-127">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="439a5-127">Here's the C# script code:</span></span>

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

### <a name="input---javascript"></a><span data-ttu-id="439a5-128">Input - JavaScript</span><span class="sxs-lookup"><span data-stu-id="439a5-128">Input - JavaScript</span></span>

<span data-ttu-id="439a5-129">The following example shows a Mobile Apps input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-129">The following example shows a Mobile Apps input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="439a5-130">The function is triggered by a queue message that has a record identifier.</span><span class="sxs-lookup"><span data-stu-id="439a5-130">The function is triggered by a queue message that has a record identifier.</span></span> <span data-ttu-id="439a5-131">The function reads the specified record and modifies its `Text` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-131">The function reads the specified record and modifies its `Text` property.</span></span>

<span data-ttu-id="439a5-132">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="439a5-132">Here's the binding data in the *function.json* file:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```
<span data-ttu-id="439a5-133">The [configuration](#input---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="439a5-133">The [configuration](#input---configuration) section explains these properties.</span></span>

<span data-ttu-id="439a5-134">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="439a5-134">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

## <a name="input---attributes"></a><span data-ttu-id="439a5-135">Input - attributes</span><span class="sxs-lookup"><span data-stu-id="439a5-135">Input - attributes</span></span>

<span data-ttu-id="439a5-136">In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="439a5-136">In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.</span></span>

<span data-ttu-id="439a5-137">For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).</span><span class="sxs-lookup"><span data-stu-id="439a5-137">For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).</span></span>

## <a name="input---configuration"></a><span data-ttu-id="439a5-138">Input - configuration</span><span class="sxs-lookup"><span data-stu-id="439a5-138">Input - configuration</span></span>

<span data-ttu-id="439a5-139">The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.</span><span class="sxs-lookup"><span data-stu-id="439a5-139">The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.</span></span>

|<span data-ttu-id="439a5-140">function.json property</span><span class="sxs-lookup"><span data-stu-id="439a5-140">function.json property</span></span> | <span data-ttu-id="439a5-141">Attribute property</span><span class="sxs-lookup"><span data-stu-id="439a5-141">Attribute property</span></span> |<span data-ttu-id="439a5-142">Description</span><span class="sxs-lookup"><span data-stu-id="439a5-142">Description</span></span>|
|---------|---------|----------------------|
| <span data-ttu-id="439a5-143">**type**</span><span class="sxs-lookup"><span data-stu-id="439a5-143">**type**</span></span>|| <span data-ttu-id="439a5-144">Must be set to "mobileTable"</span><span class="sxs-lookup"><span data-stu-id="439a5-144">Must be set to "mobileTable"</span></span>|
| <span data-ttu-id="439a5-145">**direction**</span><span class="sxs-lookup"><span data-stu-id="439a5-145">**direction**</span></span>||<span data-ttu-id="439a5-146">Must be set to "in"</span><span class="sxs-lookup"><span data-stu-id="439a5-146">Must be set to "in"</span></span>|
| <span data-ttu-id="439a5-147">**name**</span><span class="sxs-lookup"><span data-stu-id="439a5-147">**name**</span></span>|| <span data-ttu-id="439a5-148">Name of input parameter in function signature.</span><span class="sxs-lookup"><span data-stu-id="439a5-148">Name of input parameter in function signature.</span></span>|
|<span data-ttu-id="439a5-149">**tableName**</span><span class="sxs-lookup"><span data-stu-id="439a5-149">**tableName**</span></span> |<span data-ttu-id="439a5-150">**TableName**</span><span class="sxs-lookup"><span data-stu-id="439a5-150">**TableName**</span></span>|<span data-ttu-id="439a5-151">Name of the mobile app's data table</span><span class="sxs-lookup"><span data-stu-id="439a5-151">Name of the mobile app's data table</span></span>|
| <span data-ttu-id="439a5-152">**id**</span><span class="sxs-lookup"><span data-stu-id="439a5-152">**id**</span></span>| <span data-ttu-id="439a5-153">**Id**</span><span class="sxs-lookup"><span data-stu-id="439a5-153">**Id**</span></span> | <span data-ttu-id="439a5-154">The identifier of the record to retrieve.</span><span class="sxs-lookup"><span data-stu-id="439a5-154">The identifier of the record to retrieve.</span></span> <span data-ttu-id="439a5-155">Can be static or based on the trigger that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="439a5-155">Can be static or based on the trigger that invokes the function.</span></span> <span data-ttu-id="439a5-156">For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span><span class="sxs-lookup"><span data-stu-id="439a5-156">For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>|
|<span data-ttu-id="439a5-157">**connection**</span><span class="sxs-lookup"><span data-stu-id="439a5-157">**connection**</span></span>|<span data-ttu-id="439a5-158">**Connection**</span><span class="sxs-lookup"><span data-stu-id="439a5-158">**Connection**</span></span>|<span data-ttu-id="439a5-159">The name of an app setting that has the mobile app's URL.</span><span class="sxs-lookup"><span data-stu-id="439a5-159">The name of an app setting that has the mobile app's URL.</span></span> <span data-ttu-id="439a5-160">The function uses this URL to construct the required REST operations against your mobile app.</span><span class="sxs-lookup"><span data-stu-id="439a5-160">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="439a5-161">Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-161">Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding.</span></span> <span data-ttu-id="439a5-162">The URL looks like `http://<appname>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="439a5-162">The URL looks like `http://<appname>.azurewebsites.net`.</span></span>
|<span data-ttu-id="439a5-163">**apiKey**</span><span class="sxs-lookup"><span data-stu-id="439a5-163">**apiKey**</span></span>|<span data-ttu-id="439a5-164">**ApiKey**</span><span class="sxs-lookup"><span data-stu-id="439a5-164">**ApiKey**</span></span>|<span data-ttu-id="439a5-165">The name of an app setting that has your mobile app's API key.</span><span class="sxs-lookup"><span data-stu-id="439a5-165">The name of an app setting that has your mobile app's API key.</span></span> <span data-ttu-id="439a5-166">Provide the API key if you [implement an API key in your Node.js mobile app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="439a5-166">Provide the API key if you [implement an API key in your Node.js mobile app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="439a5-167">To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span><span class="sxs-lookup"><span data-stu-id="439a5-167">To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

> [!IMPORTANT]
> <span data-ttu-id="439a5-168">Don't share the API key with your mobile app clients.</span><span class="sxs-lookup"><span data-stu-id="439a5-168">Don't share the API key with your mobile app clients.</span></span> <span data-ttu-id="439a5-169">It should only be distributed securely to service-side clients, like Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="439a5-169">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> <span data-ttu-id="439a5-170">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span><span class="sxs-lookup"><span data-stu-id="439a5-170">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="439a5-171">This safeguards your sensitive information.</span><span class="sxs-lookup"><span data-stu-id="439a5-171">This safeguards your sensitive information.</span></span>

## <a name="input---usage"></a><span data-ttu-id="439a5-172">Input - usage</span><span class="sxs-lookup"><span data-stu-id="439a5-172">Input - usage</span></span>

<span data-ttu-id="439a5-173">In C# functions, when the record with the specified ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter.</span><span class="sxs-lookup"><span data-stu-id="439a5-173">In C# functions, when the record with the specified ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter.</span></span> <span data-ttu-id="439a5-174">When the record is not found, the parameter value is `null`.</span><span class="sxs-lookup"><span data-stu-id="439a5-174">When the record is not found, the parameter value is `null`.</span></span> 

<span data-ttu-id="439a5-175">In JavaScript functions, the record is passed into the `context.bindings.<name>` object.</span><span class="sxs-lookup"><span data-stu-id="439a5-175">In JavaScript functions, the record is passed into the `context.bindings.<name>` object.</span></span> <span data-ttu-id="439a5-176">When the record is not found, the parameter value is `null`.</span><span class="sxs-lookup"><span data-stu-id="439a5-176">When the record is not found, the parameter value is `null`.</span></span> 

<span data-ttu-id="439a5-177">In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully.</span><span class="sxs-lookup"><span data-stu-id="439a5-177">In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully.</span></span> <span data-ttu-id="439a5-178">You can't modify a record in JavaScript functions.</span><span class="sxs-lookup"><span data-stu-id="439a5-178">You can't modify a record in JavaScript functions.</span></span>

## <a name="output"></a><span data-ttu-id="439a5-179">Output</span><span class="sxs-lookup"><span data-stu-id="439a5-179">Output</span></span>

<span data-ttu-id="439a5-180">Use the Mobile Apps output binding to write a new record to a Mobile Apps table.</span><span class="sxs-lookup"><span data-stu-id="439a5-180">Use the Mobile Apps output binding to write a new record to a Mobile Apps table.</span></span>  

## <a name="output---example"></a><span data-ttu-id="439a5-181">Output - example</span><span class="sxs-lookup"><span data-stu-id="439a5-181">Output - example</span></span>

<span data-ttu-id="439a5-182">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="439a5-182">See the language-specific example:</span></span>

* [<span data-ttu-id="439a5-183">C#</span><span class="sxs-lookup"><span data-stu-id="439a5-183">C#</span></span>](#output---c-example)
* [<span data-ttu-id="439a5-184">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="439a5-184">C# script (.csx)</span></span>](#output---c-script-example)
* [<span data-ttu-id="439a5-185">JavaScript</span><span class="sxs-lookup"><span data-stu-id="439a5-185">JavaScript</span></span>](#output---javascript-example)

### <a name="output---c-example"></a><span data-ttu-id="439a5-186">Output - C# example</span><span class="sxs-lookup"><span data-stu-id="439a5-186">Output - C# example</span></span>

<span data-ttu-id="439a5-187">The following example shows a [C# function](functions-dotnet-class-library.md) that is triggered by a queue message and creates a record in a mobile app table.</span><span class="sxs-lookup"><span data-stu-id="439a5-187">The following example shows a [C# function](functions-dotnet-class-library.md) that is triggered by a queue message and creates a record in a mobile app table.</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
    TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

### <a name="output---c-script-example"></a><span data-ttu-id="439a5-188">Output - C# script example</span><span class="sxs-lookup"><span data-stu-id="439a5-188">Output - C# script example</span></span>

<span data-ttu-id="439a5-189">The following example shows a Mobile Apps output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-189">The following example shows a Mobile Apps output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="439a5-190">The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-190">The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.</span></span>

<span data-ttu-id="439a5-191">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="439a5-191">Here's the binding data in the *function.json* file:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="439a5-192">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="439a5-192">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="439a5-193">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="439a5-193">Here's the C# script code:</span></span>

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

### <a name="output---javascript-example"></a><span data-ttu-id="439a5-194">Output - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="439a5-194">Output - JavaScript example</span></span>

<span data-ttu-id="439a5-195">The following example shows a Mobile Apps output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-195">The following example shows a Mobile Apps output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="439a5-196">The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-196">The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.</span></span>

<span data-ttu-id="439a5-197">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="439a5-197">Here's the binding data in the *function.json* file:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="439a5-198">The [configuration](#output---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="439a5-198">The [configuration](#output---configuration) section explains these properties.</span></span>

<span data-ttu-id="439a5-199">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="439a5-199">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="output---attributes"></a><span data-ttu-id="439a5-200">Output - attributes</span><span class="sxs-lookup"><span data-stu-id="439a5-200">Output - attributes</span></span>

<span data-ttu-id="439a5-201">In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="439a5-201">In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.</span></span>

<span data-ttu-id="439a5-202">For information about attribute properties that you can configure, see [Output - configuration](#output---configuration).</span><span class="sxs-lookup"><span data-stu-id="439a5-202">For information about attribute properties that you can configure, see [Output - configuration](#output---configuration).</span></span> <span data-ttu-id="439a5-203">Here's a `MobileTable` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="439a5-203">Here's a `MobileTable` attribute example in a method signature:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
    TraceWriter log)
{
    ...
}
```

<span data-ttu-id="439a5-204">For a complete example, see [Output - C# example](#output---c-example).</span><span class="sxs-lookup"><span data-stu-id="439a5-204">For a complete example, see [Output - C# example](#output---c-example).</span></span>

## <a name="output---configuration"></a><span data-ttu-id="439a5-205">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="439a5-205">Output - configuration</span></span>

<span data-ttu-id="439a5-206">The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.</span><span class="sxs-lookup"><span data-stu-id="439a5-206">The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.</span></span>

|<span data-ttu-id="439a5-207">function.json property</span><span class="sxs-lookup"><span data-stu-id="439a5-207">function.json property</span></span> | <span data-ttu-id="439a5-208">Attribute property</span><span class="sxs-lookup"><span data-stu-id="439a5-208">Attribute property</span></span> |<span data-ttu-id="439a5-209">Description</span><span class="sxs-lookup"><span data-stu-id="439a5-209">Description</span></span>|
|---------|---------|----------------------|
| <span data-ttu-id="439a5-210">**type**</span><span class="sxs-lookup"><span data-stu-id="439a5-210">**type**</span></span>|| <span data-ttu-id="439a5-211">Must be set to "mobileTable"</span><span class="sxs-lookup"><span data-stu-id="439a5-211">Must be set to "mobileTable"</span></span>|
| <span data-ttu-id="439a5-212">**direction**</span><span class="sxs-lookup"><span data-stu-id="439a5-212">**direction**</span></span>||<span data-ttu-id="439a5-213">Must be set to "out"</span><span class="sxs-lookup"><span data-stu-id="439a5-213">Must be set to "out"</span></span>|
| <span data-ttu-id="439a5-214">**name**</span><span class="sxs-lookup"><span data-stu-id="439a5-214">**name**</span></span>|| <span data-ttu-id="439a5-215">Name of output parameter in function signature.</span><span class="sxs-lookup"><span data-stu-id="439a5-215">Name of output parameter in function signature.</span></span>|
|<span data-ttu-id="439a5-216">**tableName**</span><span class="sxs-lookup"><span data-stu-id="439a5-216">**tableName**</span></span> |<span data-ttu-id="439a5-217">**TableName**</span><span class="sxs-lookup"><span data-stu-id="439a5-217">**TableName**</span></span>|<span data-ttu-id="439a5-218">Name of the mobile app's data table</span><span class="sxs-lookup"><span data-stu-id="439a5-218">Name of the mobile app's data table</span></span>|
|<span data-ttu-id="439a5-219">**connection**</span><span class="sxs-lookup"><span data-stu-id="439a5-219">**connection**</span></span>|<span data-ttu-id="439a5-220">**MobileAppUriSetting**</span><span class="sxs-lookup"><span data-stu-id="439a5-220">**MobileAppUriSetting**</span></span>|<span data-ttu-id="439a5-221">The name of an app setting that has the mobile app's URL.</span><span class="sxs-lookup"><span data-stu-id="439a5-221">The name of an app setting that has the mobile app's URL.</span></span> <span data-ttu-id="439a5-222">The function uses this URL to construct the required REST operations against your mobile app.</span><span class="sxs-lookup"><span data-stu-id="439a5-222">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="439a5-223">Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding.</span><span class="sxs-lookup"><span data-stu-id="439a5-223">Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding.</span></span> <span data-ttu-id="439a5-224">The URL looks like `http://<appname>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="439a5-224">The URL looks like `http://<appname>.azurewebsites.net`.</span></span>
|<span data-ttu-id="439a5-225">**apiKey**</span><span class="sxs-lookup"><span data-stu-id="439a5-225">**apiKey**</span></span>|<span data-ttu-id="439a5-226">**ApiKeySetting**</span><span class="sxs-lookup"><span data-stu-id="439a5-226">**ApiKeySetting**</span></span>|<span data-ttu-id="439a5-227">The name of an app setting that has your mobile app's API key.</span><span class="sxs-lookup"><span data-stu-id="439a5-227">The name of an app setting that has your mobile app's API key.</span></span> <span data-ttu-id="439a5-228">Provide the API key if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="439a5-228">Provide the API key if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="439a5-229">To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span><span class="sxs-lookup"><span data-stu-id="439a5-229">To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

> [!IMPORTANT]
> <span data-ttu-id="439a5-230">Don't share the API key with your mobile app clients.</span><span class="sxs-lookup"><span data-stu-id="439a5-230">Don't share the API key with your mobile app clients.</span></span> <span data-ttu-id="439a5-231">It should only be distributed securely to service-side clients, like Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="439a5-231">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> <span data-ttu-id="439a5-232">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span><span class="sxs-lookup"><span data-stu-id="439a5-232">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="439a5-233">This safeguards your sensitive information.</span><span class="sxs-lookup"><span data-stu-id="439a5-233">This safeguards your sensitive information.</span></span>

## <a name="output---usage"></a><span data-ttu-id="439a5-234">Output - usage</span><span class="sxs-lookup"><span data-stu-id="439a5-234">Output - usage</span></span>

<span data-ttu-id="439a5-235">In C# script functions, use a named output parameter of type `out object` to access the output record.</span><span class="sxs-lookup"><span data-stu-id="439a5-235">In C# script functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="439a5-236">In C# class libraries, the `MobileTable` attribute can be used with any of the following types:</span><span class="sxs-lookup"><span data-stu-id="439a5-236">In C# class libraries, the `MobileTable` attribute can be used with any of the following types:</span></span>

* <span data-ttu-id="439a5-237">`ICollector<T>` or `IAsyncCollector<T>`, where `T` is either `JObject` or any type with a `public string Id` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-237">`ICollector<T>` or `IAsyncCollector<T>`, where `T` is either `JObject` or any type with a `public string Id` property.</span></span>
* `out JObject`
* <span data-ttu-id="439a5-238">`out T` or `out T[]`, where `T` is any Type with a `public string Id` property.</span><span class="sxs-lookup"><span data-stu-id="439a5-238">`out T` or `out T[]`, where `T` is any Type with a `public string Id` property.</span></span>

<span data-ttu-id="439a5-239">In Node.js functions, use `context.bindings.<name>` to access the output record.</span><span class="sxs-lookup"><span data-stu-id="439a5-239">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

## <a name="next-steps"></a><span data-ttu-id="439a5-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="439a5-240">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="439a5-241">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="439a5-241">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
