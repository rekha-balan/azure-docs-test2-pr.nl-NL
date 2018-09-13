---
title: Event Grid trigger for Azure Functions
description: Understand how to handle Event Grid events in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 08/23/2018
ms.author: glenga
ms.openlocfilehash: 6d15405ef22f47dc8a94c07d9d09d343a743408e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856544"
---
# <a name="event-grid-trigger-for-azure-functions"></a><span data-ttu-id="c875d-103">Event Grid trigger for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c875d-103">Event Grid trigger for Azure Functions</span></span>

<span data-ttu-id="c875d-104">This article explains how to handle [Event Grid](../event-grid/overview.md) events in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c875d-104">This article explains how to handle [Event Grid](../event-grid/overview.md) events in Azure Functions.</span></span>

<span data-ttu-id="c875d-105">Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in *publishers*.</span><span class="sxs-lookup"><span data-stu-id="c875d-105">Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in *publishers*.</span></span> <span data-ttu-id="c875d-106">A publisher is the service or resource that originates the event.</span><span class="sxs-lookup"><span data-stu-id="c875d-106">A publisher is the service or resource that originates the event.</span></span> <span data-ttu-id="c875d-107">For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c875d-107">For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview.md).</span></span> <span data-ttu-id="c875d-108">Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/overview.md#event-sources).</span><span class="sxs-lookup"><span data-stu-id="c875d-108">Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/overview.md#event-sources).</span></span> 

<span data-ttu-id="c875d-109">Event *handlers* receive and process events.</span><span class="sxs-lookup"><span data-stu-id="c875d-109">Event *handlers* receive and process events.</span></span> <span data-ttu-id="c875d-110">Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview.md#event-handlers).</span><span class="sxs-lookup"><span data-stu-id="c875d-110">Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview.md#event-handlers).</span></span> <span data-ttu-id="c875d-111">In this article, you learn how to use an Event Grid trigger to invoke a function when an event is received from Event Grid.</span><span class="sxs-lookup"><span data-stu-id="c875d-111">In this article, you learn how to use an Event Grid trigger to invoke a function when an event is received from Event Grid.</span></span>

<span data-ttu-id="c875d-112">If you prefer, you can use an HTTP trigger to handle Event Grid Events; see [Use an HTTP trigger as an Event Grid trigger](#use-an-http-trigger-as-an-event-grid-trigger) later in this article.</span><span class="sxs-lookup"><span data-stu-id="c875d-112">If you prefer, you can use an HTTP trigger to handle Event Grid Events; see [Use an HTTP trigger as an Event Grid trigger](#use-an-http-trigger-as-an-event-grid-trigger) later in this article.</span></span> <span data-ttu-id="c875d-113">Currently, you can't use an Event Grid trigger for an Azure Functions app when the event is delivered in the [CloudEvents schema](../event-grid/cloudevents-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c875d-113">Currently, you can't use an Event Grid trigger for an Azure Functions app when the event is delivered in the [CloudEvents schema](../event-grid/cloudevents-schema.md).</span></span> <span data-ttu-id="c875d-114">Instead, use an HTTP trigger.</span><span class="sxs-lookup"><span data-stu-id="c875d-114">Instead, use an HTTP trigger.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="c875d-115">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="c875d-115">Packages - Functions 1.x</span></span>

<span data-ttu-id="c875d-116">The Event Grid trigger is provided in the [Microsoft.Azure.WebJobs.Extensions.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventGrid) NuGet package, version 1.x.</span><span class="sxs-lookup"><span data-stu-id="c875d-116">The Event Grid trigger is provided in the [Microsoft.Azure.WebJobs.Extensions.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventGrid) NuGet package, version 1.x.</span></span> <span data-ttu-id="c875d-117">Source code for the package is in the [azure-functions-eventgrid-extension](https://github.com/Azure/azure-functions-eventgrid-extension/tree/master) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="c875d-117">Source code for the package is in the [azure-functions-eventgrid-extension](https://github.com/Azure/azure-functions-eventgrid-extension/tree/master) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="c875d-118">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="c875d-118">Packages - Functions 2.x</span></span>

<span data-ttu-id="c875d-119">The Event Grid trigger is provided in the [Microsoft.Azure.WebJobs.Extensions.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventGrid) NuGet package, version 2.x.</span><span class="sxs-lookup"><span data-stu-id="c875d-119">The Event Grid trigger is provided in the [Microsoft.Azure.WebJobs.Extensions.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventGrid) NuGet package, version 2.x.</span></span> <span data-ttu-id="c875d-120">Source code for the package is in the [azure-functions-eventgrid-extension](https://github.com/Azure/azure-functions-eventgrid-extension/tree/v2.x) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="c875d-120">Source code for the package is in the [azure-functions-eventgrid-extension](https://github.com/Azure/azure-functions-eventgrid-extension/tree/v2.x) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="example"></a><span data-ttu-id="c875d-121">Example</span><span class="sxs-lookup"><span data-stu-id="c875d-121">Example</span></span>

<span data-ttu-id="c875d-122">See the language-specific example for an Event Grid trigger:</span><span class="sxs-lookup"><span data-stu-id="c875d-122">See the language-specific example for an Event Grid trigger:</span></span>

* [<span data-ttu-id="c875d-123">C#</span><span class="sxs-lookup"><span data-stu-id="c875d-123">C#</span></span>](#c-example)
* [<span data-ttu-id="c875d-124">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="c875d-124">C# script (.csx)</span></span>](#c-script-example)
* [<span data-ttu-id="c875d-125">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c875d-125">JavaScript</span></span>](#javascript-example)
* [<span data-ttu-id="c875d-126">Java</span><span class="sxs-lookup"><span data-stu-id="c875d-126">Java</span></span>](#trigger---java-example)

<span data-ttu-id="c875d-127">For an HTTP trigger example, see [How to use HTTP trigger](#use-an-http-trigger-as-an-event-grid-trigger) later in this article.</span><span class="sxs-lookup"><span data-stu-id="c875d-127">For an HTTP trigger example, see [How to use HTTP trigger](#use-an-http-trigger-as-an-event-grid-trigger) later in this article.</span></span>

### <a name="c-example"></a><span data-ttu-id="c875d-128">C# example</span><span class="sxs-lookup"><span data-stu-id="c875d-128">C# example</span></span>

<span data-ttu-id="c875d-129">The following example shows a Functions 1.x [C# function](functions-dotnet-class-library.md) that binds to `JObject`:</span><span class="sxs-lookup"><span data-stu-id="c875d-129">The following example shows a Functions 1.x [C# function](functions-dotnet-class-library.md) that binds to `JObject`:</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.EventGrid;
using Microsoft.Azure.WebJobs.Host;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

namespace Company.Function
{
    public static class EventGridTriggerCSharp
    {
        [FunctionName("EventGridTriggerCSharp")]
        public static void Run([EventGridTrigger]JObject eventGridEvent, TraceWriter log)
        {
            log.Info(eventGridEvent.ToString(Formatting.Indented));
        }
    }
}
```

<span data-ttu-id="c875d-130">The following example shows a Functions 2.x [C# function](functions-dotnet-class-library.md) that binds to `EventGridEvent`:</span><span class="sxs-lookup"><span data-stu-id="c875d-130">The following example shows a Functions 2.x [C# function](functions-dotnet-class-library.md) that binds to `EventGridEvent`:</span></span>

```cs
using Microsoft.Azure.EventGrid.Models;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.EventGrid;
using Microsoft.Azure.WebJobs.Host;

namespace Company.Function
{
    public static class EventGridTriggerCSharp
    {
        [FunctionName("EventGridTest")]
        public static void EventGridTest([EventGridTrigger]EventGridEvent eventGridEvent, TraceWriter log)
        {
            log.Info(eventGridEvent.Data.ToString());
        }
    }
}
```

<span data-ttu-id="c875d-131">For more information, see [Packages](#packages), [Attributes](#attributes), [Configuration](#configuration), and [Usage](#usage).</span><span class="sxs-lookup"><span data-stu-id="c875d-131">For more information, see [Packages](#packages), [Attributes](#attributes), [Configuration](#configuration), and [Usage](#usage).</span></span>

### <a name="c-script-example"></a><span data-ttu-id="c875d-132">C# script example</span><span class="sxs-lookup"><span data-stu-id="c875d-132">C# script example</span></span>

<span data-ttu-id="c875d-133">The following example shows a trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="c875d-133">The following example shows a trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span>

<span data-ttu-id="c875d-134">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="c875d-134">Here's the binding data in the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "eventGridTrigger",
      "name": "eventGridEvent",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="c875d-135">Here's Functions 1.x C# script code that binds to `JObject`:</span><span class="sxs-lookup"><span data-stu-id="c875d-135">Here's Functions 1.x C# script code that binds to `JObject`:</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(JObject eventGridEvent, TraceWriter log)
{
    log.Info(eventGridEvent.ToString(Formatting.Indented));
}
```

<span data-ttu-id="c875d-136">Here's Functions 2.x C# script code that binds to `EventGridEvent`:</span><span class="sxs-lookup"><span data-stu-id="c875d-136">Here's Functions 2.x C# script code that binds to `EventGridEvent`:</span></span>

```csharp
#r "Microsoft.Azure.EventGrid"
using Microsoft.Azure.EventGrid.Models;

public static void Run(EventGridEvent eventGridEvent, TraceWriter log)
{
    log.Info(eventGridEvent.Data.ToString());
}
```

<span data-ttu-id="c875d-137">For more information, see [Packages](#packages), [Attributes](#attributes), [Configuration](#configuration), and [Usage](#usage).</span><span class="sxs-lookup"><span data-stu-id="c875d-137">For more information, see [Packages](#packages), [Attributes](#attributes), [Configuration](#configuration), and [Usage](#usage).</span></span>

### <a name="javascript-example"></a><span data-ttu-id="c875d-138">JavaScript example</span><span class="sxs-lookup"><span data-stu-id="c875d-138">JavaScript example</span></span>

<span data-ttu-id="c875d-139">The following example shows a trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="c875d-139">The following example shows a trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span>

<span data-ttu-id="c875d-140">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="c875d-140">Here's the binding data in the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "eventGridTrigger",
      "name": "eventGridEvent",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="c875d-141">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="c875d-141">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, eventGridEvent) {
    context.log("JavaScript Event Grid function processed a request.");
    context.log("Subject: " + eventGridEvent.subject);
    context.log("Time: " + eventGridEvent.eventTime);
    context.log("Data: " + JSON.stringify(eventGridEvent.data));
    context.done();
};
```

### <a name="trigger---java-example"></a><span data-ttu-id="c875d-142">Trigger - Java example</span><span class="sxs-lookup"><span data-stu-id="c875d-142">Trigger - Java example</span></span>

<span data-ttu-id="c875d-143">The following example shows a trigger binding in a *function.json* file and a [Java function](functions-reference-java.md) that uses the binding and prints out an event.</span><span class="sxs-lookup"><span data-stu-id="c875d-143">The following example shows a trigger binding in a *function.json* file and a [Java function](functions-reference-java.md) that uses the binding and prints out an event.</span></span>

```json
{
  "bindings": [
    {
      "type": "eventGridTrigger",
      "name": "eventGridEvent",
      "direction": "in"
    }
  ]
}
```

<span data-ttu-id="c875d-144">Here's the Java code:</span><span class="sxs-lookup"><span data-stu-id="c875d-144">Here's the Java code:</span></span>

```java
@FunctionName("eventGridMonitor")
  public void logEvent(
     @EventGridTrigger(name = "event") String content,
      final ExecutionContext context
  ) { 
      context.getLogger().info(content);
    }
```

<span data-ttu-id="c875d-145">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `EventGridTrigger` annotation on parameters whose value would come from EventGrid.</span><span class="sxs-lookup"><span data-stu-id="c875d-145">In the [Java functions runtime library](/java/api/overview/azure/functions/runtime), use the `EventGridTrigger` annotation on parameters whose value would come from EventGrid.</span></span> <span data-ttu-id="c875d-146">Parameters with these annotations cause the function to run when an event arrives.</span><span class="sxs-lookup"><span data-stu-id="c875d-146">Parameters with these annotations cause the function to run when an event arrives.</span></span>  <span data-ttu-id="c875d-147">This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`.</span><span class="sxs-lookup"><span data-stu-id="c875d-147">This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`.</span></span> 
     
## <a name="attributes"></a><span data-ttu-id="c875d-148">Attributes</span><span class="sxs-lookup"><span data-stu-id="c875d-148">Attributes</span></span>

<span data-ttu-id="c875d-149">In [C# class libraries](functions-dotnet-class-library.md), use the [EventGridTrigger](https://github.com/Azure/azure-functions-eventgrid-extension/blob/master/src/EventGridExtension/EventGridTriggerAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="c875d-149">In [C# class libraries](functions-dotnet-class-library.md), use the [EventGridTrigger](https://github.com/Azure/azure-functions-eventgrid-extension/blob/master/src/EventGridExtension/EventGridTriggerAttribute.cs) attribute.</span></span>

<span data-ttu-id="c875d-150">Here's an `EventGridTrigger` attribute in a method signature:</span><span class="sxs-lookup"><span data-stu-id="c875d-150">Here's an `EventGridTrigger` attribute in a method signature:</span></span>

```csharp
[FunctionName("EventGridTest")]
public static void EventGridTest([EventGridTrigger] JObject eventGridEvent, TraceWriter log)
{
    ...
}
 ```

<span data-ttu-id="c875d-151">For a complete example, see [C# example](#c-example).</span><span class="sxs-lookup"><span data-stu-id="c875d-151">For a complete example, see [C# example](#c-example).</span></span>

## <a name="configuration"></a><span data-ttu-id="c875d-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="c875d-152">Configuration</span></span>

<span data-ttu-id="c875d-153">The following table explains the binding configuration properties that you set in the *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="c875d-153">The following table explains the binding configuration properties that you set in the *function.json* file.</span></span> <span data-ttu-id="c875d-154">There are no constructor parameters or properties to set in the `EventGridTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="c875d-154">There are no constructor parameters or properties to set in the `EventGridTrigger` attribute.</span></span>

|<span data-ttu-id="c875d-155">function.json property</span><span class="sxs-lookup"><span data-stu-id="c875d-155">function.json property</span></span> |<span data-ttu-id="c875d-156">Description</span><span class="sxs-lookup"><span data-stu-id="c875d-156">Description</span></span>|
|---------|---------|----------------------|
| <span data-ttu-id="c875d-157">**type**</span><span class="sxs-lookup"><span data-stu-id="c875d-157">**type**</span></span> | <span data-ttu-id="c875d-158">Required - must be set to `eventGridTrigger`.</span><span class="sxs-lookup"><span data-stu-id="c875d-158">Required - must be set to `eventGridTrigger`.</span></span> |
| <span data-ttu-id="c875d-159">**direction**</span><span class="sxs-lookup"><span data-stu-id="c875d-159">**direction**</span></span> | <span data-ttu-id="c875d-160">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="c875d-160">Required - must be set to `in`.</span></span> |
| <span data-ttu-id="c875d-161">**name**</span><span class="sxs-lookup"><span data-stu-id="c875d-161">**name**</span></span> | <span data-ttu-id="c875d-162">Required - the variable name used in function code for the parameter that receives the event data.</span><span class="sxs-lookup"><span data-stu-id="c875d-162">Required - the variable name used in function code for the parameter that receives the event data.</span></span> |

## <a name="usage"></a><span data-ttu-id="c875d-163">Usage</span><span class="sxs-lookup"><span data-stu-id="c875d-163">Usage</span></span>

<span data-ttu-id="c875d-164">For C# and F# functions in Azure Functions 1.x, you can use the following parameter types for the Event Grid trigger:</span><span class="sxs-lookup"><span data-stu-id="c875d-164">For C# and F# functions in Azure Functions 1.x, you can use the following parameter types for the Event Grid trigger:</span></span>

* `JObject`
* `string`

<span data-ttu-id="c875d-165">For C# and F# functions in Azure Functions 2.x, you also have the option to use the following parameter type for the Event Grid trigger:</span><span class="sxs-lookup"><span data-stu-id="c875d-165">For C# and F# functions in Azure Functions 2.x, you also have the option to use the following parameter type for the Event Grid trigger:</span></span>

* <span data-ttu-id="c875d-166">`Microsoft.Azure.EventGrid.Models.EventGridEvent`- Defines properties for the fields common to all event types.</span><span class="sxs-lookup"><span data-stu-id="c875d-166">`Microsoft.Azure.EventGrid.Models.EventGridEvent`- Defines properties for the fields common to all event types.</span></span>

> [!NOTE]
> <span data-ttu-id="c875d-167">In Functions v1 if you try to bind to `Microsoft.Azure.WebJobs.Extensions.EventGrid.EventGridEvent`, the compiler will display a "deprecated" message and advise you to use `Microsoft.Azure.EventGrid.Models.EventGridEvent` instead.</span><span class="sxs-lookup"><span data-stu-id="c875d-167">In Functions v1 if you try to bind to `Microsoft.Azure.WebJobs.Extensions.EventGrid.EventGridEvent`, the compiler will display a "deprecated" message and advise you to use `Microsoft.Azure.EventGrid.Models.EventGridEvent` instead.</span></span> <span data-ttu-id="c875d-168">To use the newer type, reference the [Microsoft.Azure.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.EventGrid) NuGet package and fully qualify the `EventGridEvent` type name by prefixing it with `Microsoft.Azure.EventGrid.Models`.</span><span class="sxs-lookup"><span data-stu-id="c875d-168">To use the newer type, reference the [Microsoft.Azure.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.EventGrid) NuGet package and fully qualify the `EventGridEvent` type name by prefixing it with `Microsoft.Azure.EventGrid.Models`.</span></span> <span data-ttu-id="c875d-169">For information about how to reference NuGet packages in a C# script function, see [Using NuGet packages](functions-reference-csharp.md#using-nuget-packages)</span><span class="sxs-lookup"><span data-stu-id="c875d-169">For information about how to reference NuGet packages in a C# script function, see [Using NuGet packages](functions-reference-csharp.md#using-nuget-packages)</span></span>

<span data-ttu-id="c875d-170">For JavaScript functions, the parameter named by the *function.json* `name` property has a reference to the event object.</span><span class="sxs-lookup"><span data-stu-id="c875d-170">For JavaScript functions, the parameter named by the *function.json* `name` property has a reference to the event object.</span></span>

## <a name="event-schema"></a><span data-ttu-id="c875d-171">Event schema</span><span class="sxs-lookup"><span data-stu-id="c875d-171">Event schema</span></span>

<span data-ttu-id="c875d-172">Data for an Event Grid event is received as a JSON object in the body of an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="c875d-172">Data for an Event Grid event is received as a JSON object in the body of an HTTP request.</span></span> <span data-ttu-id="c875d-173">The JSON looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="c875d-173">The JSON looks similar to the following example:</span></span>

```json
[{
  "topic": "/subscriptions/{subscriptionid}/resourceGroups/eg0122/providers/Microsoft.Storage/storageAccounts/egblobstore",
  "subject": "/blobServices/default/containers/{containername}/blobs/blobname.jpg",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2018-01-23T17:02:19.6069787Z",
  "id": "{guid}",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "{guid}",
    "requestId": "{guid}",
    "eTag": "0x8D562831044DDD0",
    "contentType": "application/octet-stream",
    "contentLength": 2248,
    "blobType": "BlockBlob",
    "url": "https://egblobstore.blob.core.windows.net/{containername}/blobname.jpg",
    "sequencer": "000000000000272D000000000003D60F",
    "storageDiagnostics": {
      "batchId": "{guid}"
    }
  },
  "dataVersion": "",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="c875d-174">The example shown is an array of one element.</span><span class="sxs-lookup"><span data-stu-id="c875d-174">The example shown is an array of one element.</span></span> <span data-ttu-id="c875d-175">Event Grid always sends an array and may send more than one event in the array.</span><span class="sxs-lookup"><span data-stu-id="c875d-175">Event Grid always sends an array and may send more than one event in the array.</span></span> <span data-ttu-id="c875d-176">The runtime invokes your function once for each array element.</span><span class="sxs-lookup"><span data-stu-id="c875d-176">The runtime invokes your function once for each array element.</span></span>

<span data-ttu-id="c875d-177">The top-level properties in the event JSON data are the same among all event types, while the contents of the `data` property are specific to each event type.</span><span class="sxs-lookup"><span data-stu-id="c875d-177">The top-level properties in the event JSON data are the same among all event types, while the contents of the `data` property are specific to each event type.</span></span> <span data-ttu-id="c875d-178">The example shown is for a blob storage event.</span><span class="sxs-lookup"><span data-stu-id="c875d-178">The example shown is for a blob storage event.</span></span>

<span data-ttu-id="c875d-179">For explanations of the common and event-specific properties, see [Event properties](../event-grid/event-schema.md#event-properties) in the Event Grid documentation.</span><span class="sxs-lookup"><span data-stu-id="c875d-179">For explanations of the common and event-specific properties, see [Event properties](../event-grid/event-schema.md#event-properties) in the Event Grid documentation.</span></span>

<span data-ttu-id="c875d-180">The `EventGridEvent` type defines only the top-level properties; the `Data` property is a `JObject`.</span><span class="sxs-lookup"><span data-stu-id="c875d-180">The `EventGridEvent` type defines only the top-level properties; the `Data` property is a `JObject`.</span></span> 

## <a name="create-a-subscription"></a><span data-ttu-id="c875d-181">Create a subscription</span><span class="sxs-lookup"><span data-stu-id="c875d-181">Create a subscription</span></span>

<span data-ttu-id="c875d-182">To start receiving Event Grid HTTP requests, create an Event Grid subscription that specifies the endpoint URL that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="c875d-182">To start receiving Event Grid HTTP requests, create an Event Grid subscription that specifies the endpoint URL that invokes the function.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c875d-183">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c875d-183">Azure portal</span></span>

<span data-ttu-id="c875d-184">For functions that you develop in the Azure portal with the Event Grid trigger, select **Add Event Grid subscription**.</span><span class="sxs-lookup"><span data-stu-id="c875d-184">For functions that you develop in the Azure portal with the Event Grid trigger, select **Add Event Grid subscription**.</span></span>

![Create subscription in portal](media/functions-bindings-event-grid/portal-sub-create.png)

<span data-ttu-id="c875d-186">When you select this link, the portal opens the **Create Event Subscription** page with the endpoint URL prefilled.</span><span class="sxs-lookup"><span data-stu-id="c875d-186">When you select this link, the portal opens the **Create Event Subscription** page with the endpoint URL prefilled.</span></span>

![Endpoint URL prefilled](media/functions-bindings-event-grid/endpoint-url.png)

<span data-ttu-id="c875d-188">For more information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal.md) in the Event Grid documentation.</span><span class="sxs-lookup"><span data-stu-id="c875d-188">For more information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal.md) in the Event Grid documentation.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="c875d-189">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c875d-189">Azure CLI</span></span>

<span data-ttu-id="c875d-190">To create a subscription by using [the Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), use the [az eventgrid event-subscription create](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-create) command.</span><span class="sxs-lookup"><span data-stu-id="c875d-190">To create a subscription by using [the Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), use the [az eventgrid event-subscription create](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-create) command.</span></span>

<span data-ttu-id="c875d-191">The command requires the endpoint URL that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="c875d-191">The command requires the endpoint URL that invokes the function.</span></span> <span data-ttu-id="c875d-192">The following example shows the URL pattern:</span><span class="sxs-lookup"><span data-stu-id="c875d-192">The following example shows the URL pattern:</span></span>

```
https://{functionappname}.azurewebsites.net/admin/extensions/EventGridExtensionConfig?functionName={functionname}&code={systemkey}
```

<span data-ttu-id="c875d-193">The system key is an authorization key that has to be included in the endpoint URL for an Event Grid trigger.</span><span class="sxs-lookup"><span data-stu-id="c875d-193">The system key is an authorization key that has to be included in the endpoint URL for an Event Grid trigger.</span></span> <span data-ttu-id="c875d-194">The following section explains how to get the system key.</span><span class="sxs-lookup"><span data-stu-id="c875d-194">The following section explains how to get the system key.</span></span>

<span data-ttu-id="c875d-195">Here's an example that subscribes to a blob storage account (with a placeholder for the system key):</span><span class="sxs-lookup"><span data-stu-id="c875d-195">Here's an example that subscribes to a blob storage account (with a placeholder for the system key):</span></span>

```azurecli
az eventgrid resource event-subscription create -g myResourceGroup \
--provider-namespace Microsoft.Storage --resource-type storageAccounts \
--resource-name glengablobstorage --name myFuncSub  \
--included-event-types Microsoft.Storage.BlobCreated \
--subject-begins-with /blobServices/default/containers/images/blobs/ \
--endpoint https://glengastorageevents.azurewebsites.net/admin/extensions/EventGridExtensionConfig?functionName=imageresizefunc&code=LUwlnhIsNtSiUjv/sNtSiUjvsNtSiUjvsNtSiUjvYb7XDonDUr/RUg==
```

<span data-ttu-id="c875d-196">For more information about how to create a subscription, see [the blob storage quickstart](../storage/blobs/storage-blob-event-quickstart.md#subscribe-to-your-storage-account) or the other Event Grid quickstarts.</span><span class="sxs-lookup"><span data-stu-id="c875d-196">For more information about how to create a subscription, see [the blob storage quickstart](../storage/blobs/storage-blob-event-quickstart.md#subscribe-to-your-storage-account) or the other Event Grid quickstarts.</span></span>

### <a name="get-the-system-key"></a><span data-ttu-id="c875d-197">Get the system key</span><span class="sxs-lookup"><span data-stu-id="c875d-197">Get the system key</span></span>

<span data-ttu-id="c875d-198">You can get the system key by using the following API (HTTP GET):</span><span class="sxs-lookup"><span data-stu-id="c875d-198">You can get the system key by using the following API (HTTP GET):</span></span>

```
http://{functionappname}.azurewebsites.net/admin/host/systemkeys/eventgridextensionconfig_extension?code={adminkey}
```

<span data-ttu-id="c875d-199">This is an admin API, so it requires your function app [master key](functions-bindings-http-webhook.md#authorization-keys).</span><span class="sxs-lookup"><span data-stu-id="c875d-199">This is an admin API, so it requires your function app [master key](functions-bindings-http-webhook.md#authorization-keys).</span></span> <span data-ttu-id="c875d-200">Don't confuse the system key (for invoking an Event Grid trigger function) with the master key (for performing administrative tasks on the function app).</span><span class="sxs-lookup"><span data-stu-id="c875d-200">Don't confuse the system key (for invoking an Event Grid trigger function) with the master key (for performing administrative tasks on the function app).</span></span> <span data-ttu-id="c875d-201">When you subscribe to an Event Grid topic, be sure to use the system key.</span><span class="sxs-lookup"><span data-stu-id="c875d-201">When you subscribe to an Event Grid topic, be sure to use the system key.</span></span> 

<span data-ttu-id="c875d-202">Here's an example of the response that provides the system key:</span><span class="sxs-lookup"><span data-stu-id="c875d-202">Here's an example of the response that provides the system key:</span></span>

```
{
  "name": "eventgridextensionconfig_extension",
  "value": "{the system key for the function}",
  "links": [
    {
      "rel": "self",
      "href": "{the URL for the function, without the system key}"
    }
  ]
}
```

<span data-ttu-id="c875d-203">For more information, see [Authorization keys](functions-bindings-http-webhook.md#authorization-keys) in the HTTP trigger reference article.</span><span class="sxs-lookup"><span data-stu-id="c875d-203">For more information, see [Authorization keys](functions-bindings-http-webhook.md#authorization-keys) in the HTTP trigger reference article.</span></span> 

<span data-ttu-id="c875d-204">Alternatively, you can send an HTTP PUT to specify the key value yourself.</span><span class="sxs-lookup"><span data-stu-id="c875d-204">Alternatively, you can send an HTTP PUT to specify the key value yourself.</span></span>

## <a name="local-testing-with-viewer-web-app"></a><span data-ttu-id="c875d-205">Local testing with viewer web app</span><span class="sxs-lookup"><span data-stu-id="c875d-205">Local testing with viewer web app</span></span>

<span data-ttu-id="c875d-206">To test an Event Grid trigger locally, you have to get Event Grid HTTP requests delivered from their origin in the cloud to your local machine.</span><span class="sxs-lookup"><span data-stu-id="c875d-206">To test an Event Grid trigger locally, you have to get Event Grid HTTP requests delivered from their origin in the cloud to your local machine.</span></span> <span data-ttu-id="c875d-207">One way to do that is by capturing requests online and manually resending them on your local machine:</span><span class="sxs-lookup"><span data-stu-id="c875d-207">One way to do that is by capturing requests online and manually resending them on your local machine:</span></span>

2. <span data-ttu-id="c875d-208">[Create a viewer web app](#create-a-viewer-web-app) that captures event messages.</span><span class="sxs-lookup"><span data-stu-id="c875d-208">[Create a viewer web app](#create-a-viewer-web-app) that captures event messages.</span></span>
3. <span data-ttu-id="c875d-209">[Create an Event Grid subscription](#create-an-event-grid-subscription) that sends events to the viewer app.</span><span class="sxs-lookup"><span data-stu-id="c875d-209">[Create an Event Grid subscription](#create-an-event-grid-subscription) that sends events to the viewer app.</span></span>
4. <span data-ttu-id="c875d-210">[Generate a request](#generate-a-request) and copy the request body from the viewer app.</span><span class="sxs-lookup"><span data-stu-id="c875d-210">[Generate a request](#generate-a-request) and copy the request body from the viewer app.</span></span>
5. <span data-ttu-id="c875d-211">[Manually post the request](#manually-post-the-request) to the localhost URL of your Event Grid trigger function.</span><span class="sxs-lookup"><span data-stu-id="c875d-211">[Manually post the request](#manually-post-the-request) to the localhost URL of your Event Grid trigger function.</span></span>

<span data-ttu-id="c875d-212">When you're done testing, you can use the same subscription for production by updating the endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-212">When you're done testing, you can use the same subscription for production by updating the endpoint.</span></span> <span data-ttu-id="c875d-213">Use the [az eventgrid event-subscription update](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-update) Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="c875d-213">Use the [az eventgrid event-subscription update](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-update) Azure CLI command.</span></span>

### <a name="create-a-viewer-web-app"></a><span data-ttu-id="c875d-214">Create a viewer web app</span><span class="sxs-lookup"><span data-stu-id="c875d-214">Create a viewer web app</span></span>

<span data-ttu-id="c875d-215">To simplify capturing event messages, you can deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span><span class="sxs-lookup"><span data-stu-id="c875d-215">To simplify capturing event messages, you can deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages.</span></span> <span data-ttu-id="c875d-216">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="c875d-216">The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.</span></span>

<span data-ttu-id="c875d-217">Select **Deploy to Azure** to deploy the solution to your subscription.</span><span class="sxs-lookup"><span data-stu-id="c875d-217">Select **Deploy to Azure** to deploy the solution to your subscription.</span></span> <span data-ttu-id="c875d-218">In the Azure portal, provide values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="c875d-218">In the Azure portal, provide values for the parameters.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fazure-event-grid-viewer%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

<span data-ttu-id="c875d-219">The deployment may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="c875d-219">The deployment may take a few minutes to complete.</span></span> <span data-ttu-id="c875d-220">After the deployment has succeeded, view your web app to make sure it's running.</span><span class="sxs-lookup"><span data-stu-id="c875d-220">After the deployment has succeeded, view your web app to make sure it's running.</span></span> <span data-ttu-id="c875d-221">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="c875d-221">In a web browser, navigate to: `https://<your-site-name>.azurewebsites.net`</span></span>

<span data-ttu-id="c875d-222">You see the site but no events have been posted to it yet.</span><span class="sxs-lookup"><span data-stu-id="c875d-222">You see the site but no events have been posted to it yet.</span></span>

![View new site](media/functions-bindings-event-grid/view-site.png)

### <a name="create-an-event-grid-subscription"></a><span data-ttu-id="c875d-224">Create an Event Grid subscription</span><span class="sxs-lookup"><span data-stu-id="c875d-224">Create an Event Grid subscription</span></span>

<span data-ttu-id="c875d-225">Create an Event Grid subscription of the type you want to test, and give it the URL from your web app as the endpoint for event notification.</span><span class="sxs-lookup"><span data-stu-id="c875d-225">Create an Event Grid subscription of the type you want to test, and give it the URL from your web app as the endpoint for event notification.</span></span> <span data-ttu-id="c875d-226">The endpoint for your web app must include the suffix `/api/updates/`.</span><span class="sxs-lookup"><span data-stu-id="c875d-226">The endpoint for your web app must include the suffix `/api/updates/`.</span></span> <span data-ttu-id="c875d-227">So, the full URL is `https://<your-site-name>.azurewebsites.net/api/updates`</span><span class="sxs-lookup"><span data-stu-id="c875d-227">So, the full URL is `https://<your-site-name>.azurewebsites.net/api/updates`</span></span>

<span data-ttu-id="c875d-228">For information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal.md) in the Event Grid documentation.</span><span class="sxs-lookup"><span data-stu-id="c875d-228">For information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal.md) in the Event Grid documentation.</span></span>

### <a name="generate-a-request"></a><span data-ttu-id="c875d-229">Generate a request</span><span class="sxs-lookup"><span data-stu-id="c875d-229">Generate a request</span></span>

<span data-ttu-id="c875d-230">Trigger an event that will generate HTTP traffic to your web app endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-230">Trigger an event that will generate HTTP traffic to your web app endpoint.</span></span>  <span data-ttu-id="c875d-231">For example, if you created a blob storage subscription, upload or delete a blob.</span><span class="sxs-lookup"><span data-stu-id="c875d-231">For example, if you created a blob storage subscription, upload or delete a blob.</span></span> <span data-ttu-id="c875d-232">When a request shows up in your web app, copy the request body.</span><span class="sxs-lookup"><span data-stu-id="c875d-232">When a request shows up in your web app, copy the request body.</span></span>

<span data-ttu-id="c875d-233">The subscription validation request will be received first; ignore any validation requests, and copy the event request.</span><span class="sxs-lookup"><span data-stu-id="c875d-233">The subscription validation request will be received first; ignore any validation requests, and copy the event request.</span></span>

![Copy request body from web app](media/functions-bindings-event-grid/view-results.png)

### <a name="manually-post-the-request"></a><span data-ttu-id="c875d-235">Manually post the request</span><span class="sxs-lookup"><span data-stu-id="c875d-235">Manually post the request</span></span>

<span data-ttu-id="c875d-236">Run your Event Grid function locally.</span><span class="sxs-lookup"><span data-stu-id="c875d-236">Run your Event Grid function locally.</span></span>

<span data-ttu-id="c875d-237">Use a tool such as [Postman](https://www.getpostman.com/) or [curl](https://curl.haxx.se/docs/httpscripting.html) to create an HTTP POST request:</span><span class="sxs-lookup"><span data-stu-id="c875d-237">Use a tool such as [Postman](https://www.getpostman.com/) or [curl](https://curl.haxx.se/docs/httpscripting.html) to create an HTTP POST request:</span></span>

* <span data-ttu-id="c875d-238">Set a `Content-Type: application/json` header.</span><span class="sxs-lookup"><span data-stu-id="c875d-238">Set a `Content-Type: application/json` header.</span></span>
* <span data-ttu-id="c875d-239">Set an `aeg-event-type: Notification` header.</span><span class="sxs-lookup"><span data-stu-id="c875d-239">Set an `aeg-event-type: Notification` header.</span></span>
* <span data-ttu-id="c875d-240">Paste the RequestBin data into the request body.</span><span class="sxs-lookup"><span data-stu-id="c875d-240">Paste the RequestBin data into the request body.</span></span> 
* <span data-ttu-id="c875d-241">Post to the URL of your Event Grid trigger function, using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="c875d-241">Post to the URL of your Event Grid trigger function, using the following pattern:</span></span>

```
http://localhost:7071/admin/extensions/EventGridExtensionConfig?functionName={functionname}
``` 

<span data-ttu-id="c875d-242">The `functionName` parameter must be the name specified in the `FunctionName` attribute.</span><span class="sxs-lookup"><span data-stu-id="c875d-242">The `functionName` parameter must be the name specified in the `FunctionName` attribute.</span></span>

<span data-ttu-id="c875d-243">The following screenshots show the headers and request body in Postman:</span><span class="sxs-lookup"><span data-stu-id="c875d-243">The following screenshots show the headers and request body in Postman:</span></span>

![Headers in Postman](media/functions-bindings-event-grid/postman2.png)

![Request body in Postman](media/functions-bindings-event-grid/postman.png)

<span data-ttu-id="c875d-246">The Event Grid trigger function executes and shows logs similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="c875d-246">The Event Grid trigger function executes and shows logs similar to the following example:</span></span>

![Sample Event Grid trigger function logs](media/functions-bindings-event-grid/eg-output.png)

## <a name="local-testing-with-ngrok"></a><span data-ttu-id="c875d-248">Local testing with ngrok</span><span class="sxs-lookup"><span data-stu-id="c875d-248">Local testing with ngrok</span></span>

<span data-ttu-id="c875d-249">Another way to test an Event Grid trigger locally is to automate the HTTP connection between the Internet and your development computer.</span><span class="sxs-lookup"><span data-stu-id="c875d-249">Another way to test an Event Grid trigger locally is to automate the HTTP connection between the Internet and your development computer.</span></span> <span data-ttu-id="c875d-250">You can do that with an open-source tool named [ngrok](https://ngrok.com/):</span><span class="sxs-lookup"><span data-stu-id="c875d-250">You can do that with an open-source tool named [ngrok](https://ngrok.com/):</span></span>

3. <span data-ttu-id="c875d-251">[Create an ngrok endpoint](#create-an-ngrok-endpoint).</span><span class="sxs-lookup"><span data-stu-id="c875d-251">[Create an ngrok endpoint](#create-an-ngrok-endpoint).</span></span>
4. <span data-ttu-id="c875d-252">[Run the Event Grid trigger function](#run-the-event-grid-trigger-function).</span><span class="sxs-lookup"><span data-stu-id="c875d-252">[Run the Event Grid trigger function](#run-the-event-grid-trigger-function).</span></span>
5. <span data-ttu-id="c875d-253">[Create an Event Grid subscription](#create-a-subscription) that sends events to the ngrok endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-253">[Create an Event Grid subscription](#create-a-subscription) that sends events to the ngrok endpoint.</span></span>
6. <span data-ttu-id="c875d-254">[Trigger an event](#trigger-an-event).</span><span class="sxs-lookup"><span data-stu-id="c875d-254">[Trigger an event](#trigger-an-event).</span></span>

<span data-ttu-id="c875d-255">When you're done testing, you can use the same subscription for production by updating the endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-255">When you're done testing, you can use the same subscription for production by updating the endpoint.</span></span> <span data-ttu-id="c875d-256">Use the [az eventgrid event-subscription update](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-update) Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="c875d-256">Use the [az eventgrid event-subscription update](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-update) Azure CLI command.</span></span>

### <a name="create-an-ngrok-endpoint"></a><span data-ttu-id="c875d-257">Create an ngrok endpoint</span><span class="sxs-lookup"><span data-stu-id="c875d-257">Create an ngrok endpoint</span></span>

<span data-ttu-id="c875d-258">Download *ngrok.exe* from [ngrok](https://ngrok.com/), and run with the following command:</span><span class="sxs-lookup"><span data-stu-id="c875d-258">Download *ngrok.exe* from [ngrok](https://ngrok.com/), and run with the following command:</span></span>

```
ngrok http -host-header=localhost 7071
```

<span data-ttu-id="c875d-259">The -host-header parameter is needed because the functions runtime expects requests from localhost when it runs on localhost.</span><span class="sxs-lookup"><span data-stu-id="c875d-259">The -host-header parameter is needed because the functions runtime expects requests from localhost when it runs on localhost.</span></span> <span data-ttu-id="c875d-260">7071 is the default port number when the runtime runs locally.</span><span class="sxs-lookup"><span data-stu-id="c875d-260">7071 is the default port number when the runtime runs locally.</span></span>

<span data-ttu-id="c875d-261">The command creates output like the following:</span><span class="sxs-lookup"><span data-stu-id="c875d-261">The command creates output like the following:</span></span>

```
Session Status                online
Version                       2.2.8
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://263db807.ngrok.io -> localhost:7071
Forwarding                    https://263db807.ngrok.io -> localhost:7071

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

<span data-ttu-id="c875d-262">You'll use the `https://{subdomain}.ngrok.io` URL for your Event Grid subscription.</span><span class="sxs-lookup"><span data-stu-id="c875d-262">You'll use the `https://{subdomain}.ngrok.io` URL for your Event Grid subscription.</span></span>

### <a name="run-the-event-grid-trigger-function"></a><span data-ttu-id="c875d-263">Run the Event Grid trigger function</span><span class="sxs-lookup"><span data-stu-id="c875d-263">Run the Event Grid trigger function</span></span>

<span data-ttu-id="c875d-264">The ngrok URL doesn't get special handling by Event Grid, so your function must be running locally when the subscription is created.</span><span class="sxs-lookup"><span data-stu-id="c875d-264">The ngrok URL doesn't get special handling by Event Grid, so your function must be running locally when the subscription is created.</span></span> <span data-ttu-id="c875d-265">If it isn't, the validation response doesn't get sent and the subscription creation fails.</span><span class="sxs-lookup"><span data-stu-id="c875d-265">If it isn't, the validation response doesn't get sent and the subscription creation fails.</span></span>

### <a name="create-a-subscription"></a><span data-ttu-id="c875d-266">Create a subscription</span><span class="sxs-lookup"><span data-stu-id="c875d-266">Create a subscription</span></span>

<span data-ttu-id="c875d-267">Create an Event Grid subscription of the type you want to test, and give it your ngrok endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-267">Create an Event Grid subscription of the type you want to test, and give it your ngrok endpoint.</span></span>

<span data-ttu-id="c875d-268">Use this endpoint pattern for Functions 1.x:</span><span class="sxs-lookup"><span data-stu-id="c875d-268">Use this endpoint pattern for Functions 1.x:</span></span>
```
https://{subdomain}.ngrok.io/admin/extensions/EventGridExtensionConfig?functionName={functionname}
``` 
<span data-ttu-id="c875d-269">Use this endpoint pattern for Functions 2.x:</span><span class="sxs-lookup"><span data-stu-id="c875d-269">Use this endpoint pattern for Functions 2.x:</span></span>
```
https://{subdomain}.ngrok.io/runtime/webhooks/EventGridExtensionConfig?functionName={functionName}
``` 
<span data-ttu-id="c875d-270">The `functionName` parameter must be the name specified in the `FunctionName` attribute.</span><span class="sxs-lookup"><span data-stu-id="c875d-270">The `functionName` parameter must be the name specified in the `FunctionName` attribute.</span></span>

<span data-ttu-id="c875d-271">Here's an example using the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="c875d-271">Here's an example using the Azure CLI:</span></span>

```
az eventgrid event-subscription create --resource-id /subscriptions/aeb4b7cb-b7cb-b7cb-b7cb-b7cbb6607f30/resourceGroups/eg0122/providers/Microsoft.Storage/storageAccounts/egblobstor0122 --name egblobsub0126 --endpoint https://263db807.ngrok.io/admin/extensions/EventGridExtensionConfig?functionName=EventGridTrigger
```

<span data-ttu-id="c875d-272">For information about how to create a subscription, see [Create a subscription](#create-a-subscription) earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="c875d-272">For information about how to create a subscription, see [Create a subscription](#create-a-subscription) earlier in this article.</span></span>

### <a name="trigger-an-event"></a><span data-ttu-id="c875d-273">Trigger an event</span><span class="sxs-lookup"><span data-stu-id="c875d-273">Trigger an event</span></span>

<span data-ttu-id="c875d-274">Trigger an event that will generate HTTP traffic to your ngrok endpoint.</span><span class="sxs-lookup"><span data-stu-id="c875d-274">Trigger an event that will generate HTTP traffic to your ngrok endpoint.</span></span>  <span data-ttu-id="c875d-275">For example, if you created a blob storage subscription, upload or delete a blob.</span><span class="sxs-lookup"><span data-stu-id="c875d-275">For example, if you created a blob storage subscription, upload or delete a blob.</span></span>

<span data-ttu-id="c875d-276">The Event Grid trigger function executes and shows logs similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="c875d-276">The Event Grid trigger function executes and shows logs similar to the following example:</span></span>

![Sample Event Grid trigger function logs](media/functions-bindings-event-grid/eg-output.png)

## <a name="use-an-http-trigger-as-an-event-grid-trigger"></a><span data-ttu-id="c875d-278">Use an HTTP trigger as an Event Grid trigger</span><span class="sxs-lookup"><span data-stu-id="c875d-278">Use an HTTP trigger as an Event Grid trigger</span></span>

<span data-ttu-id="c875d-279">Event Grid events are received as HTTP requests, so you can handle events by using an HTTP trigger instead of an Event Grid trigger.</span><span class="sxs-lookup"><span data-stu-id="c875d-279">Event Grid events are received as HTTP requests, so you can handle events by using an HTTP trigger instead of an Event Grid trigger.</span></span> <span data-ttu-id="c875d-280">One possible reason for doing that is to get more control over the endpoint URL that invokes the function.</span><span class="sxs-lookup"><span data-stu-id="c875d-280">One possible reason for doing that is to get more control over the endpoint URL that invokes the function.</span></span> <span data-ttu-id="c875d-281">Another reason is when you need to receive events in the [CloudEvents schema](../event-grid/cloudevents-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c875d-281">Another reason is when you need to receive events in the [CloudEvents schema](../event-grid/cloudevents-schema.md).</span></span> <span data-ttu-id="c875d-282">Currently, the Event Grid trigger doesn't support the CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-282">Currently, the Event Grid trigger doesn't support the CloudEvents schema.</span></span> <span data-ttu-id="c875d-283">The examples in this section show solutions for both Event Grid schema and CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-283">The examples in this section show solutions for both Event Grid schema and CloudEvents schema.</span></span>

<span data-ttu-id="c875d-284">If you use an HTTP trigger, you have to write code for what the Event Grid trigger does automatically:</span><span class="sxs-lookup"><span data-stu-id="c875d-284">If you use an HTTP trigger, you have to write code for what the Event Grid trigger does automatically:</span></span>

* <span data-ttu-id="c875d-285">Sends a validation response to a [subscription validation request](../event-grid/security-authentication.md#webhook-event-delivery).</span><span class="sxs-lookup"><span data-stu-id="c875d-285">Sends a validation response to a [subscription validation request](../event-grid/security-authentication.md#webhook-event-delivery).</span></span>
* <span data-ttu-id="c875d-286">Invokes the function once per element of the event array contained in the request body.</span><span class="sxs-lookup"><span data-stu-id="c875d-286">Invokes the function once per element of the event array contained in the request body.</span></span>

<span data-ttu-id="c875d-287">For information about the URL to use for invoking the function locally or when it runs in Azure, see the [HTTP trigger binding reference documentation](functions-bindings-http-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="c875d-287">For information about the URL to use for invoking the function locally or when it runs in Azure, see the [HTTP trigger binding reference documentation](functions-bindings-http-webhook.md)</span></span>

### <a name="event-grid-schema"></a><span data-ttu-id="c875d-288">Event Grid schema</span><span class="sxs-lookup"><span data-stu-id="c875d-288">Event Grid schema</span></span>

<span data-ttu-id="c875d-289">The following sample C# code for an HTTP trigger simulates Event Grid trigger behavior.</span><span class="sxs-lookup"><span data-stu-id="c875d-289">The following sample C# code for an HTTP trigger simulates Event Grid trigger behavior.</span></span> <span data-ttu-id="c875d-290">Use this example for events delivered in the Event Grid schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-290">Use this example for events delivered in the Event Grid schema.</span></span>

```csharp
[FunctionName("HttpTrigger")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "post")]HttpRequestMessage req,
    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    var messages = await req.Content.ReadAsAsync<JArray>();

    // If the request is for subscription validation, send back the validation code.
    if (messages.Count > 0 && string.Equals((string)messages[0]["eventType"], 
        "Microsoft.EventGrid.SubscriptionValidationEvent", 
        System.StringComparison.OrdinalIgnoreCase))
    {
        log.Info("Validate request received");
        return req.CreateResponse<object>(new
        {
            validationResponse = messages[0]["data"]["validationCode"]
        });
    }

    // The request is not for subscription validation, so it's for one or more events.
    foreach (JObject message in messages)
    {
        // Handle one event.
        EventGridEvent eventGridEvent = message.ToObject<EventGridEvent>();
        log.Info($"Subject: {eventGridEvent.Subject}");
        log.Info($"Time: {eventGridEvent.EventTime}");
        log.Info($"Event data: {eventGridEvent.Data.ToString()}");
    }

    return req.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="c875d-291">The following sample JavaScript code for an HTTP trigger simulates Event Grid trigger behavior.</span><span class="sxs-lookup"><span data-stu-id="c875d-291">The following sample JavaScript code for an HTTP trigger simulates Event Grid trigger behavior.</span></span> <span data-ttu-id="c875d-292">Use this example for events delivered in the Event Grid schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-292">Use this example for events delivered in the Event Grid schema.</span></span>

```javascript
module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    var messages = req.body;
    // If the request is for subscription validation, send back the validation code.
    if (messages.length > 0 && messages[0].eventType == "Microsoft.EventGrid.SubscriptionValidationEvent") {
        context.log('Validate request received');
        var code = messages[0].data.validationCode;
        context.res = { status: 200, body: { "ValidationResponse": code } };
    }
    else {
        // The request is not for subscription validation, so it's for one or more events.
        // Event Grid schema delivers events in an array.
        for (var i = 0; i < messages.length; i++) {
            // Handle one event.
            var message = messages[i];
            context.log('Subject: ' + message.subject);
            context.log('Time: ' + message.eventTime);
            context.log('Data: ' + JSON.stringify(message.data));
        }
    }
    context.done();
};
```

<span data-ttu-id="c875d-293">Your event-handling code goes inside the loop through the `messages` array.</span><span class="sxs-lookup"><span data-stu-id="c875d-293">Your event-handling code goes inside the loop through the `messages` array.</span></span>

### <a name="cloudevents-schema"></a><span data-ttu-id="c875d-294">CloudEvents schema</span><span class="sxs-lookup"><span data-stu-id="c875d-294">CloudEvents schema</span></span>

<span data-ttu-id="c875d-295">The following sample C# code for an HTTP trigger simulates Event Grid trigger behavior.</span><span class="sxs-lookup"><span data-stu-id="c875d-295">The following sample C# code for an HTTP trigger simulates Event Grid trigger behavior.</span></span>  <span data-ttu-id="c875d-296">Use this example for events delivered in the CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-296">Use this example for events delivered in the CloudEvents schema.</span></span>

```csharp
[FunctionName("HttpTrigger")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    var requestmessage = await req.Content.ReadAsStringAsync();
    var message = JToken.Parse(requestmessage);

    if (message.Type == JTokenType.Array)
    {
        // If the request is for subscription validation, send back the validation code.
        if (string.Equals((string)message[0]["eventType"],
        "Microsoft.EventGrid.SubscriptionValidationEvent",
        System.StringComparison.OrdinalIgnoreCase))
        {
            log.Info("Validate request received");
            return req.CreateResponse<object>(new
            {
                validationResponse = message[0]["data"]["validationCode"]
            });
        }
    }
    else
    {
        // The request is not for subscription validation, so it's for an event.
        // CloudEvents schema delivers one event at a time.
        log.Info($"Source: {message["source"]}");
        log.Info($"Time: {message["eventTime"]}");
        log.Info($"Event data: {message["data"].ToString()}");
    }

    return req.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="c875d-297">The following sample JavaScript code for an HTTP trigger simulates Event Grid trigger behavior.</span><span class="sxs-lookup"><span data-stu-id="c875d-297">The following sample JavaScript code for an HTTP trigger simulates Event Grid trigger behavior.</span></span> <span data-ttu-id="c875d-298">Use this example for events delivered in the CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="c875d-298">Use this example for events delivered in the CloudEvents schema.</span></span>

```javascript
module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    var message = req.body;
    // If the request is for subscription validation, send back the validation code.
    if (message.length > 0 && message[0].eventType == "Microsoft.EventGrid.SubscriptionValidationEvent") {
        context.log('Validate request received');
        var code = message[0].data.validationCode;
        context.res = { status: 200, body: { "ValidationResponse": code } };
    }
    else {
        // The request is not for subscription validation, so it's for an event.
        // CloudEvents schema delivers one event at a time.
        var event = JSON.parse(message);
        context.log('Source: ' + event.source);
        context.log('Time: ' + event.eventTime);
        context.log('Data: ' + JSON.stringify(event.data));
    }
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="c875d-299">Next steps</span><span class="sxs-lookup"><span data-stu-id="c875d-299">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c875d-300">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="c875d-300">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c875d-301">Learn more about Event Grid</span><span class="sxs-lookup"><span data-stu-id="c875d-301">Learn more about Event Grid</span></span>](../event-grid/overview.md)
