---
title: Azure Functions HTTP and webhook bindings
description: Understand how to use HTTP and webhook triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture, HTTP, API, REST
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: 41870f4f3cf4a0aba461021b4787e1ba004e5ead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44777094"
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="73a67-104">Azure Functions HTTP and webhook bindings</span><span class="sxs-lookup"><span data-stu-id="73a67-104">Azure Functions HTTP and webhook bindings</span></span>

<span data-ttu-id="73a67-105">This article explains how to work with HTTP bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="73a67-105">This article explains how to work with HTTP bindings in Azure Functions.</span></span> <span data-ttu-id="73a67-106">Azure Functions supports HTTP triggers and output bindings.</span><span class="sxs-lookup"><span data-stu-id="73a67-106">Azure Functions supports HTTP triggers and output bindings.</span></span>

<span data-ttu-id="73a67-107">An HTTP trigger can be customized to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="73a67-107">An HTTP trigger can be customized to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="73a67-108">A webhook trigger accepts only a  JSON payload and validates the JSON.</span><span class="sxs-lookup"><span data-stu-id="73a67-108">A webhook trigger accepts only a  JSON payload and validates the JSON.</span></span> <span data-ttu-id="73a67-109">There are special versions of the webhook trigger that make it easier to handle webhooks from certain providers, such as GitHub and Slack.</span><span class="sxs-lookup"><span data-stu-id="73a67-109">There are special versions of the webhook trigger that make it easier to handle webhooks from certain providers, such as GitHub and Slack.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="73a67-110">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="73a67-110">Packages - Functions 1.x</span></span>

<span data-ttu-id="73a67-111">The HTTP bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Http](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http) NuGet package, version 1.x.</span><span class="sxs-lookup"><span data-stu-id="73a67-111">The HTTP bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Http](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http) NuGet package, version 1.x.</span></span> <span data-ttu-id="73a67-112">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.Http) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="73a67-112">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.Http) GitHub repository.</span></span>

[!INCLUDE [functions-package-auto](../../includes/functions-package-auto.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="73a67-113">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="73a67-113">Packages - Functions 2.x</span></span>

<span data-ttu-id="73a67-114">The HTTP bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Http](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="73a67-114">The HTTP bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Http](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http) NuGet package, version 3.x.</span></span> <span data-ttu-id="73a67-115">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Http/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="73a67-115">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Http/) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package-auto.md)]

## <a name="trigger"></a><span data-ttu-id="73a67-116">Trigger</span><span class="sxs-lookup"><span data-stu-id="73a67-116">Trigger</span></span>

<span data-ttu-id="73a67-117">The HTTP trigger lets you invoke a function with an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-117">The HTTP trigger lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="73a67-118">You can use an HTTP trigger to build serverless APIs and respond to webhooks.</span><span class="sxs-lookup"><span data-stu-id="73a67-118">You can use an HTTP trigger to build serverless APIs and respond to webhooks.</span></span> 

<span data-ttu-id="73a67-119">By default, an HTTP trigger returns HTTP 200 OK with an empty body in Functions 1.x, or HTTP 204 No Content with an empty body in Functions 2.x.</span><span class="sxs-lookup"><span data-stu-id="73a67-119">By default, an HTTP trigger returns HTTP 200 OK with an empty body in Functions 1.x, or HTTP 204 No Content with an empty body in Functions 2.x.</span></span> <span data-ttu-id="73a67-120">To modify the response, configure an [HTTP output binding](#http-output-binding).</span><span class="sxs-lookup"><span data-stu-id="73a67-120">To modify the response, configure an [HTTP output binding](#http-output-binding).</span></span>

## <a name="trigger---example"></a><span data-ttu-id="73a67-121">Trigger - example</span><span class="sxs-lookup"><span data-stu-id="73a67-121">Trigger - example</span></span>

<span data-ttu-id="73a67-122">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="73a67-122">See the language-specific example:</span></span>

* [<span data-ttu-id="73a67-123">C#</span><span class="sxs-lookup"><span data-stu-id="73a67-123">C#</span></span>](#trigger---c-example)
* [<span data-ttu-id="73a67-124">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="73a67-124">C# script (.csx)</span></span>](#trigger---c-script-example)
* [<span data-ttu-id="73a67-125">F#</span><span class="sxs-lookup"><span data-stu-id="73a67-125">F#</span></span>](#trigger---f-example)
* [<span data-ttu-id="73a67-126">JavaScript</span><span class="sxs-lookup"><span data-stu-id="73a67-126">JavaScript</span></span>](#trigger---javascript-example)
* [<span data-ttu-id="73a67-127">Java</span><span class="sxs-lookup"><span data-stu-id="73a67-127">Java</span></span>](#trigger---java-example)

### <a name="trigger---c-example"></a><span data-ttu-id="73a67-128">Trigger - C# example</span><span class="sxs-lookup"><span data-stu-id="73a67-128">Trigger - C# example</span></span>

<span data-ttu-id="73a67-129">The following example shows a [C# function](functions-dotnet-class-library.md) that looks for a `name` parameter either in the query string or the body of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-129">The following example shows a [C# function](functions-dotnet-class-library.md) that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span> <span data-ttu-id="73a67-130">Notice that the return value is used for the output binding, but a return value attribute isn't required.</span><span class="sxs-lookup"><span data-stu-id="73a67-130">Notice that the return value is used for the output binding, but a return value attribute isn't required.</span></span>

```cs
[FunctionName("HttpTriggerCSharp")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)]HttpRequestMessage req, 
    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

### <a name="trigger---c-script-example"></a><span data-ttu-id="73a67-131">Trigger - C# script example</span><span class="sxs-lookup"><span data-stu-id="73a67-131">Trigger - C# script example</span></span>

<span data-ttu-id="73a67-132">The following example shows a trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-132">The following example shows a trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="73a67-133">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-133">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

<span data-ttu-id="73a67-134">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-134">Here's the *function.json* file:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "authLevel": "function",
            "name": "req",
            "type": "httpTrigger",
            "direction": "in",
            "methods": [
                "get",
                "post"
            ]
        },
        {
            "name": "$return",
            "type": "http",
            "direction": "out"
        }
    ]
}
```

<span data-ttu-id="73a67-135">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-135">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-136">Here's C# script code that binds to `HttpRequestMessage`:</span><span class="sxs-lookup"><span data-stu-id="73a67-136">Here's C# script code that binds to `HttpRequestMessage`:</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="73a67-137">You can bind to a custom object instead of `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="73a67-137">You can bind to a custom object instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="73a67-138">This object is created from the body of the request, parsed as JSON.</span><span class="sxs-lookup"><span data-stu-id="73a67-138">This object is created from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="73a67-139">Similarly, a type can be passed to the HTTP response output binding and returned as the response body, along with a 200 status code.</span><span class="sxs-lookup"><span data-stu-id="73a67-139">Similarly, a type can be passed to the HTTP response output binding and returned as the response body, along with a 200 status code.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
```

### <a name="trigger---f-example"></a><span data-ttu-id="73a67-140">Trigger - F# example</span><span class="sxs-lookup"><span data-stu-id="73a67-140">Trigger - F# example</span></span>

<span data-ttu-id="73a67-141">The following example shows a trigger binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-141">The following example shows a trigger binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="73a67-142">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-142">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

<span data-ttu-id="73a67-143">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-143">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "authLevel": "function",
      "name": "req",
      "type": "httpTrigger",
      "direction": "in"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="73a67-144">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-144">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-145">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="73a67-145">Here's the F# code:</span></span>

```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="73a67-146">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="73a67-146">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, as shown in the following example:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

### <a name="trigger---javascript-example"></a><span data-ttu-id="73a67-147">Trigger - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="73a67-147">Trigger - JavaScript example</span></span>

<span data-ttu-id="73a67-148">The following example shows a trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-148">The following example shows a trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="73a67-149">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-149">The function looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

<span data-ttu-id="73a67-150">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-150">Here's the *function.json* file:</span></span>

```json
{
    "disabled": false,    
    "bindings": [
        {
            "authLevel": "function",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req"
        },
        {
            "type": "http",
            "direction": "out",
            "name": "res"
        }
    ]
}
```

<span data-ttu-id="73a67-151">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-151">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-152">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="73a67-152">Here's the JavaScript code:</span></span>

```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```

### <a name="trigger---java-example"></a><span data-ttu-id="73a67-153">Trigger - Java example</span><span class="sxs-lookup"><span data-stu-id="73a67-153">Trigger - Java example</span></span>

<span data-ttu-id="73a67-154">The following example shows a trigger binding in a *function.json* file and a [Java function](functions-reference-java.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-154">The following example shows a trigger binding in a *function.json* file and a [Java function](functions-reference-java.md) that uses the binding.</span></span> <span data-ttu-id="73a67-155">The function returns a HTTP status code 200 response with arequest body that prefixes the triggering request body with a "Hello, " greeting.</span><span class="sxs-lookup"><span data-stu-id="73a67-155">The function returns a HTTP status code 200 response with arequest body that prefixes the triggering request body with a "Hello, " greeting.</span></span>


<span data-ttu-id="73a67-156">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-156">Here's the *function.json* file:</span></span>

```json
{
    "disabled": false,    
    "bindings": [
        {
            "authLevel": "anonymous",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req"
        },
        {
            "type": "http",
            "direction": "out",
            "name": "res"
        }
    ]
}
```

<span data-ttu-id="73a67-157">Here's the Java code:</span><span class="sxs-lookup"><span data-stu-id="73a67-157">Here's the Java code:</span></span>

```java
@FunctionName("hello")
public HttpResponseMessage<String> hello(@HttpTrigger(name = "req", methods = {"post"}, authLevel = AuthorizationLevel.ANONYMOUS), Optional<String> request,
                        final ExecutionContext context) 
    {
        // default HTTP 200 response code
        return String.format("Hello, %s!", request);
    }
}
```
     
## <a name="trigger---webhook-example"></a><span data-ttu-id="73a67-158">Trigger - webhook example</span><span class="sxs-lookup"><span data-stu-id="73a67-158">Trigger - webhook example</span></span>

<span data-ttu-id="73a67-159">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="73a67-159">See the language-specific example:</span></span>

* [<span data-ttu-id="73a67-160">C#</span><span class="sxs-lookup"><span data-stu-id="73a67-160">C#</span></span>](#webhook---c-example)
* [<span data-ttu-id="73a67-161">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="73a67-161">C# script (.csx)</span></span>](#webhook---c-script-example)
* [<span data-ttu-id="73a67-162">F#</span><span class="sxs-lookup"><span data-stu-id="73a67-162">F#</span></span>](#webhook---f-example)
* [<span data-ttu-id="73a67-163">JavaScript</span><span class="sxs-lookup"><span data-stu-id="73a67-163">JavaScript</span></span>](#webhook---javascript-example)

### <a name="webhook---c-example"></a><span data-ttu-id="73a67-164">Webhook - C# example</span><span class="sxs-lookup"><span data-stu-id="73a67-164">Webhook - C# example</span></span>

<span data-ttu-id="73a67-165">The following example shows a [C# function](functions-dotnet-class-library.md) that sends an HTTP 200 in response to a generic JSON request.</span><span class="sxs-lookup"><span data-stu-id="73a67-165">The following example shows a [C# function](functions-dotnet-class-library.md) that sends an HTTP 200 in response to a generic JSON request.</span></span>

```cs
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

### <a name="webhook---c-script-example"></a><span data-ttu-id="73a67-166">Webhook - C# script example</span><span class="sxs-lookup"><span data-stu-id="73a67-166">Webhook - C# script example</span></span>

<span data-ttu-id="73a67-167">The following example shows a webhook trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-167">The following example shows a webhook trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="73a67-168">The function logs GitHub issue comments.</span><span class="sxs-lookup"><span data-stu-id="73a67-168">The function logs GitHub issue comments.</span></span>

<span data-ttu-id="73a67-169">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-169">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "github",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="73a67-170">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-170">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-171">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="73a67-171">Here's the C# script code:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

### <a name="webhook---f-example"></a><span data-ttu-id="73a67-172">Webhook - F# example</span><span class="sxs-lookup"><span data-stu-id="73a67-172">Webhook - F# example</span></span>

<span data-ttu-id="73a67-173">The following example shows a webhook trigger binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-173">The following example shows a webhook trigger binding in a *function.json* file and an [F# function](functions-reference-fsharp.md) that uses the binding.</span></span> <span data-ttu-id="73a67-174">The function logs GitHub issue comments.</span><span class="sxs-lookup"><span data-stu-id="73a67-174">The function logs GitHub issue comments.</span></span>

<span data-ttu-id="73a67-175">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-175">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "github",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="73a67-176">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-176">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-177">Here's the F# code:</span><span class="sxs-lookup"><span data-stu-id="73a67-177">Here's the F# code:</span></span>

```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

### <a name="webhook---javascript-example"></a><span data-ttu-id="73a67-178">Webhook - JavaScript example</span><span class="sxs-lookup"><span data-stu-id="73a67-178">Webhook - JavaScript example</span></span>

<span data-ttu-id="73a67-179">The following example shows a webhook trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-179">The following example shows a webhook trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span> <span data-ttu-id="73a67-180">The function logs GitHub issue comments.</span><span class="sxs-lookup"><span data-stu-id="73a67-180">The function logs GitHub issue comments.</span></span>

<span data-ttu-id="73a67-181">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="73a67-181">Here's the binding data in the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "github",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="73a67-182">The [configuration](#trigger---configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-182">The [configuration](#trigger---configuration) section explains these properties.</span></span>

<span data-ttu-id="73a67-183">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="73a67-183">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```

## <a name="trigger---attributes"></a><span data-ttu-id="73a67-184">Trigger - attributes</span><span class="sxs-lookup"><span data-stu-id="73a67-184">Trigger - attributes</span></span>

<span data-ttu-id="73a67-185">In [C# class libraries](functions-dotnet-class-library.md), use the [HttpTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="73a67-185">In [C# class libraries](functions-dotnet-class-library.md), use the [HttpTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs) attribute.</span></span>

<span data-ttu-id="73a67-186">You can set the authorization level and allowable HTTP methods in attribute constructor parameters, and there are properties for webhook type and route template.</span><span class="sxs-lookup"><span data-stu-id="73a67-186">You can set the authorization level and allowable HTTP methods in attribute constructor parameters, and there are properties for webhook type and route template.</span></span> <span data-ttu-id="73a67-187">For more information about these settings, see [Trigger - configuration](#trigger---configuration).</span><span class="sxs-lookup"><span data-stu-id="73a67-187">For more information about these settings, see [Trigger - configuration](#trigger---configuration).</span></span> <span data-ttu-id="73a67-188">Here's an `HttpTrigger` attribute in a method signature:</span><span class="sxs-lookup"><span data-stu-id="73a67-188">Here's an `HttpTrigger` attribute in a method signature:</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    ...
}
 ```

<span data-ttu-id="73a67-189">For a complete example, see [Trigger - C# example](#trigger---c-example).</span><span class="sxs-lookup"><span data-stu-id="73a67-189">For a complete example, see [Trigger - C# example](#trigger---c-example).</span></span>

## <a name="trigger---configuration"></a><span data-ttu-id="73a67-190">Trigger - configuration</span><span class="sxs-lookup"><span data-stu-id="73a67-190">Trigger - configuration</span></span>

<span data-ttu-id="73a67-191">The following table explains the binding configuration properties that you set in the *function.json* file and the `HttpTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="73a67-191">The following table explains the binding configuration properties that you set in the *function.json* file and the `HttpTrigger` attribute.</span></span>

|<span data-ttu-id="73a67-192">function.json property</span><span class="sxs-lookup"><span data-stu-id="73a67-192">function.json property</span></span> | <span data-ttu-id="73a67-193">Attribute property</span><span class="sxs-lookup"><span data-stu-id="73a67-193">Attribute property</span></span> |<span data-ttu-id="73a67-194">Description</span><span class="sxs-lookup"><span data-stu-id="73a67-194">Description</span></span>|
|---------|---------|----------------------|
| <span data-ttu-id="73a67-195">**type**</span><span class="sxs-lookup"><span data-stu-id="73a67-195">**type**</span></span> | <span data-ttu-id="73a67-196">n/a</span><span class="sxs-lookup"><span data-stu-id="73a67-196">n/a</span></span>| <span data-ttu-id="73a67-197">Required - must be set to `httpTrigger`.</span><span class="sxs-lookup"><span data-stu-id="73a67-197">Required - must be set to `httpTrigger`.</span></span> |
| <span data-ttu-id="73a67-198">**direction**</span><span class="sxs-lookup"><span data-stu-id="73a67-198">**direction**</span></span> | <span data-ttu-id="73a67-199">n/a</span><span class="sxs-lookup"><span data-stu-id="73a67-199">n/a</span></span>| <span data-ttu-id="73a67-200">Required - must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="73a67-200">Required - must be set to `in`.</span></span> |
| <span data-ttu-id="73a67-201">**name**</span><span class="sxs-lookup"><span data-stu-id="73a67-201">**name**</span></span> | <span data-ttu-id="73a67-202">n/a</span><span class="sxs-lookup"><span data-stu-id="73a67-202">n/a</span></span>| <span data-ttu-id="73a67-203">Required - the variable name used in function code for the request or request body.</span><span class="sxs-lookup"><span data-stu-id="73a67-203">Required - the variable name used in function code for the request or request body.</span></span> |
| <a name="http-auth"></a><span data-ttu-id="73a67-204">**authLevel**</span><span class="sxs-lookup"><span data-stu-id="73a67-204">**authLevel**</span></span> |  <span data-ttu-id="73a67-205">**AuthLevel**</span><span class="sxs-lookup"><span data-stu-id="73a67-205">**AuthLevel**</span></span> |<span data-ttu-id="73a67-206">Determines what keys, if any, need to be present on the request in order to invoke the function.</span><span class="sxs-lookup"><span data-stu-id="73a67-206">Determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="73a67-207">The authorization level can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="73a67-207">The authorization level can be one of the following values:</span></span> <ul><li><span data-ttu-id="73a67-208"><code>anonymous</code>&mdash;No API key is required.</span><span class="sxs-lookup"><span data-stu-id="73a67-208"><code>anonymous</code>&mdash;No API key is required.</span></span></li><li><span data-ttu-id="73a67-209"><code>function</code>&mdash;A function-specific API key is required.</span><span class="sxs-lookup"><span data-stu-id="73a67-209"><code>function</code>&mdash;A function-specific API key is required.</span></span> <span data-ttu-id="73a67-210">This is the default value if none is provided.</span><span class="sxs-lookup"><span data-stu-id="73a67-210">This is the default value if none is provided.</span></span></li><li><span data-ttu-id="73a67-211"><code>admin</code>&mdash;The master key is required.</span><span class="sxs-lookup"><span data-stu-id="73a67-211"><code>admin</code>&mdash;The master key is required.</span></span></li></ul> <span data-ttu-id="73a67-212">For more information, see the section about [authorization keys](#authorization-keys).</span><span class="sxs-lookup"><span data-stu-id="73a67-212">For more information, see the section about [authorization keys](#authorization-keys).</span></span> |
| <span data-ttu-id="73a67-213">**methods**</span><span class="sxs-lookup"><span data-stu-id="73a67-213">**methods**</span></span> |<span data-ttu-id="73a67-214">**Methods**</span><span class="sxs-lookup"><span data-stu-id="73a67-214">**Methods**</span></span> | <span data-ttu-id="73a67-215">An array of the HTTP methods to which the function  responds.</span><span class="sxs-lookup"><span data-stu-id="73a67-215">An array of the HTTP methods to which the function  responds.</span></span> <span data-ttu-id="73a67-216">If not specified, the function responds to all HTTP methods.</span><span class="sxs-lookup"><span data-stu-id="73a67-216">If not specified, the function responds to all HTTP methods.</span></span> <span data-ttu-id="73a67-217">See [customize the http endpoint](#customize-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="73a67-217">See [customize the http endpoint](#customize-the-http-endpoint).</span></span> |
| <span data-ttu-id="73a67-218">**route**</span><span class="sxs-lookup"><span data-stu-id="73a67-218">**route**</span></span> | <span data-ttu-id="73a67-219">**Route**</span><span class="sxs-lookup"><span data-stu-id="73a67-219">**Route**</span></span> | <span data-ttu-id="73a67-220">Defines the route template, controlling to which request URLs your function responds.</span><span class="sxs-lookup"><span data-stu-id="73a67-220">Defines the route template, controlling to which request URLs your function responds.</span></span> <span data-ttu-id="73a67-221">The default value if none is provided is `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="73a67-221">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="73a67-222">For more information, see [customize the http endpoint](#customize-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="73a67-222">For more information, see [customize the http endpoint](#customize-the-http-endpoint).</span></span> |
| <span data-ttu-id="73a67-223">**webHookType**</span><span class="sxs-lookup"><span data-stu-id="73a67-223">**webHookType**</span></span> | <span data-ttu-id="73a67-224">**WebHookType**</span><span class="sxs-lookup"><span data-stu-id="73a67-224">**WebHookType**</span></span> |<span data-ttu-id="73a67-225">Configures the HTTP trigger to act as a [webhook](https://en.wikipedia.org/wiki/Webhook) receiver for the specified provider.</span><span class="sxs-lookup"><span data-stu-id="73a67-225">Configures the HTTP trigger to act as a [webhook](https://en.wikipedia.org/wiki/Webhook) receiver for the specified provider.</span></span> <span data-ttu-id="73a67-226">Don't set the `methods` property if you set this property.</span><span class="sxs-lookup"><span data-stu-id="73a67-226">Don't set the `methods` property if you set this property.</span></span> <span data-ttu-id="73a67-227">The webhook type can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="73a67-227">The webhook type can be one of the following values:</span></span><ul><li><span data-ttu-id="73a67-228"><code>genericJson</code>&mdash;A general-purpose webhook endpoint without logic for a specific provider.</span><span class="sxs-lookup"><span data-stu-id="73a67-228"><code>genericJson</code>&mdash;A general-purpose webhook endpoint without logic for a specific provider.</span></span> <span data-ttu-id="73a67-229">This setting restricts requests to only those using HTTP POST and with the `application/json` content type.</span><span class="sxs-lookup"><span data-stu-id="73a67-229">This setting restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span></li><li><span data-ttu-id="73a67-230"><code>github</code>&mdash;The function responds to [GitHub webhooks](https://developer.github.com/webhooks/).</span><span class="sxs-lookup"><span data-stu-id="73a67-230"><code>github</code>&mdash;The function responds to [GitHub webhooks](https://developer.github.com/webhooks/).</span></span> <span data-ttu-id="73a67-231">Do not use the  _authLevel_ property with GitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="73a67-231">Do not use the  _authLevel_ property with GitHub webhooks.</span></span> <span data-ttu-id="73a67-232">For more information, see the GitHub webhooks section later in this article.</span><span class="sxs-lookup"><span data-stu-id="73a67-232">For more information, see the GitHub webhooks section later in this article.</span></span></li><li><span data-ttu-id="73a67-233"><code>slack</code>&mdash;The function responds to [Slack webhooks](https://api.slack.com/outgoing-webhooks).</span><span class="sxs-lookup"><span data-stu-id="73a67-233"><code>slack</code>&mdash;The function responds to [Slack webhooks](https://api.slack.com/outgoing-webhooks).</span></span> <span data-ttu-id="73a67-234">Do not use the _authLevel_ property with Slack webhooks.</span><span class="sxs-lookup"><span data-stu-id="73a67-234">Do not use the _authLevel_ property with Slack webhooks.</span></span> <span data-ttu-id="73a67-235">For more information, see the Slack webhooks section later in this article.</span><span class="sxs-lookup"><span data-stu-id="73a67-235">For more information, see the Slack webhooks section later in this article.</span></span></li></ul>|

## <a name="trigger---usage"></a><span data-ttu-id="73a67-236">Trigger - usage</span><span class="sxs-lookup"><span data-stu-id="73a67-236">Trigger - usage</span></span>

<span data-ttu-id="73a67-237">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span><span class="sxs-lookup"><span data-stu-id="73a67-237">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="73a67-238">If you choose `HttpRequestMessage`, you get full access to the request object.</span><span class="sxs-lookup"><span data-stu-id="73a67-238">If you choose `HttpRequestMessage`, you get full access to the request object.</span></span> <span data-ttu-id="73a67-239">For a custom type, Functions tries to parse the JSON request body to set the object properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-239">For a custom type, Functions tries to parse the JSON request body to set the object properties.</span></span> 

<span data-ttu-id="73a67-240">For JavaScript functions, the Functions runtime provides the request body instead of the request object.</span><span class="sxs-lookup"><span data-stu-id="73a67-240">For JavaScript functions, the Functions runtime provides the request body instead of the request object.</span></span> <span data-ttu-id="73a67-241">For more information, see the [JavaScript trigger example](#trigger---javascript-example).</span><span class="sxs-lookup"><span data-stu-id="73a67-241">For more information, see the [JavaScript trigger example](#trigger---javascript-example).</span></span>

### <a name="github-webhooks"></a><span data-ttu-id="73a67-242">GitHub webhooks</span><span class="sxs-lookup"><span data-stu-id="73a67-242">GitHub webhooks</span></span>

<span data-ttu-id="73a67-243">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the **webHookType** property to `github`.</span><span class="sxs-lookup"><span data-stu-id="73a67-243">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the **webHookType** property to `github`.</span></span> <span data-ttu-id="73a67-244">Then copy its URL and API key into the **Add webhook** page of your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="73a67-244">Then copy its URL and API key into the **Add webhook** page of your GitHub repository.</span></span> 

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

<span data-ttu-id="73a67-245">For an example, see [Create a function triggered by a GitHub webhook](functions-create-github-webhook-triggered-function.md).</span><span class="sxs-lookup"><span data-stu-id="73a67-245">For an example, see [Create a function triggered by a GitHub webhook](functions-create-github-webhook-triggered-function.md).</span></span>

### <a name="slack-webhooks"></a><span data-ttu-id="73a67-246">Slack webhooks</span><span class="sxs-lookup"><span data-stu-id="73a67-246">Slack webhooks</span></span>

<span data-ttu-id="73a67-247">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span><span class="sxs-lookup"><span data-stu-id="73a67-247">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="73a67-248">See [Authorization keys](#authorization-keys).</span><span class="sxs-lookup"><span data-stu-id="73a67-248">See [Authorization keys](#authorization-keys).</span></span>

### <a name="customize-the-http-endpoint"></a><span data-ttu-id="73a67-249">Customize the HTTP endpoint</span><span class="sxs-lookup"><span data-stu-id="73a67-249">Customize the HTTP endpoint</span></span>

<span data-ttu-id="73a67-250">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span><span class="sxs-lookup"><span data-stu-id="73a67-250">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="73a67-251">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span><span class="sxs-lookup"><span data-stu-id="73a67-251">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="73a67-252">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span><span class="sxs-lookup"><span data-stu-id="73a67-252">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
{
    "bindings": [
    {
        "type": "httpTrigger",
        "name": "req",
        "direction": "in",
        "methods": [ "get" ],
        "route": "products/{category:alpha}/{id:int?}"
    },
    {
        "type": "http",
        "name": "res",
        "direction": "out"
    }
    ]
}
```

<span data-ttu-id="73a67-253">Using this configuration, the function is now addressable with the following route instead of the original route.</span><span class="sxs-lookup"><span data-stu-id="73a67-253">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

```
http://<yourapp>.azurewebsites.net/api/products/electronics/357
```

<span data-ttu-id="73a67-254">This allows the function code to support two parameters in the address, _category_ and _id_. You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span><span class="sxs-lookup"><span data-stu-id="73a67-254">This allows the function code to support two parameters in the address, _category_ and _id_. You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="73a67-255">The following C# function code makes use of both parameters.</span><span class="sxs-lookup"><span data-stu-id="73a67-255">The following C# function code makes use of both parameters.</span></span>

```csharp
public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                TraceWriter log)
{
    if (id == null)
        return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
    else
        return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
}
```

<span data-ttu-id="73a67-256">Here is Node.js function code that uses the same route parameters.</span><span class="sxs-lookup"><span data-stu-id="73a67-256">Here is Node.js function code that uses the same route parameters.</span></span>

```javascript
module.exports = function (context, req) {

    var category = context.bindingData.category;
    var id = context.bindingData.id;

    if (!id) {
        context.res = {
            // status defaults to 200 */
            body: "All " + category + " items were requested."
        };
    }
    else {
        context.res = {
            // status defaults to 200 */
            body: category + " item with id = " + id + " was requested."
        };
    }

    context.done();
} 
```

<span data-ttu-id="73a67-257">By default, all function routes are prefixed with *api*.</span><span class="sxs-lookup"><span data-stu-id="73a67-257">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="73a67-258">You can also customize or remove the prefix using the `http.routePrefix` property in your [host.json](functions-host-json.md) file.</span><span class="sxs-lookup"><span data-stu-id="73a67-258">You can also customize or remove the prefix using the `http.routePrefix` property in your [host.json](functions-host-json.md) file.</span></span> <span data-ttu-id="73a67-259">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="73a67-259">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
{
    "http": {
    "routePrefix": ""
    }
}
```

### <a name="authorization-keys"></a><span data-ttu-id="73a67-260">Authorization keys</span><span class="sxs-lookup"><span data-stu-id="73a67-260">Authorization keys</span></span>

<span data-ttu-id="73a67-261">HTTP triggers let you use keys for added security.</span><span class="sxs-lookup"><span data-stu-id="73a67-261">HTTP triggers let you use keys for added security.</span></span> <span data-ttu-id="73a67-262">A standard HTTP trigger can use these as an API key, requiring the key to be present on the request.</span><span class="sxs-lookup"><span data-stu-id="73a67-262">A standard HTTP trigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="73a67-263">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span><span class="sxs-lookup"><span data-stu-id="73a67-263">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

> [!NOTE]
> <span data-ttu-id="73a67-264">When running functions locally, authorization is disabled no matter the `authLevel` set in `function.json`.</span><span class="sxs-lookup"><span data-stu-id="73a67-264">When running functions locally, authorization is disabled no matter the `authLevel` set in `function.json`.</span></span> <span data-ttu-id="73a67-265">As soon as you publish to Azure Functions, the `authLevel` immediately takes effect.</span><span class="sxs-lookup"><span data-stu-id="73a67-265">As soon as you publish to Azure Functions, the `authLevel` immediately takes effect.</span></span>

<span data-ttu-id="73a67-266">Keys are stored as part of your function app in Azure and are encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="73a67-266">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="73a67-267">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions in the portal and select "Manage."</span><span class="sxs-lookup"><span data-stu-id="73a67-267">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions in the portal and select "Manage."</span></span> 

<span data-ttu-id="73a67-268">There are two types of keys:</span><span class="sxs-lookup"><span data-stu-id="73a67-268">There are two types of keys:</span></span>

- <span data-ttu-id="73a67-269">**Host keys**: These keys are shared by all functions within the function app.</span><span class="sxs-lookup"><span data-stu-id="73a67-269">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="73a67-270">When used as an API key, these allow access to any function within the function app.</span><span class="sxs-lookup"><span data-stu-id="73a67-270">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="73a67-271">**Function keys**: These keys apply only to the specific functions under which they are defined.</span><span class="sxs-lookup"><span data-stu-id="73a67-271">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="73a67-272">When used as an API key, these only allow access to that function.</span><span class="sxs-lookup"><span data-stu-id="73a67-272">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="73a67-273">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span><span class="sxs-lookup"><span data-stu-id="73a67-273">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="73a67-274">Function keys take precedence over host keys.</span><span class="sxs-lookup"><span data-stu-id="73a67-274">Function keys take precedence over host keys.</span></span> <span data-ttu-id="73a67-275">When two keys are defined with the same name, the function key is always used.</span><span class="sxs-lookup"><span data-stu-id="73a67-275">When two keys are defined with the same name, the function key is always used.</span></span>

<span data-ttu-id="73a67-276">The **master key** is a default host key named "_master" that is defined for each function app.</span><span class="sxs-lookup"><span data-stu-id="73a67-276">The **master key** is a default host key named "_master" that is defined for each function app.</span></span> <span data-ttu-id="73a67-277">This key cannot be revoked.</span><span class="sxs-lookup"><span data-stu-id="73a67-277">This key cannot be revoked.</span></span> <span data-ttu-id="73a67-278">It provides administrative access to the runtime APIs.</span><span class="sxs-lookup"><span data-stu-id="73a67-278">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="73a67-279">Using `"authLevel": "admin"` in the binding JSON requires this key to be presented on the request; any other key results in authorization failure.</span><span class="sxs-lookup"><span data-stu-id="73a67-279">Using `"authLevel": "admin"` in the binding JSON requires this key to be presented on the request; any other key results in authorization failure.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="73a67-280">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span><span class="sxs-lookup"><span data-stu-id="73a67-280">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="73a67-281">Use caution when choosing the admin authorization level.</span><span class="sxs-lookup"><span data-stu-id="73a67-281">Use caution when choosing the admin authorization level.</span></span>

### <a name="api-key-authorization"></a><span data-ttu-id="73a67-282">API key authorization</span><span class="sxs-lookup"><span data-stu-id="73a67-282">API key authorization</span></span>

<span data-ttu-id="73a67-283">By default, an HTTP trigger requires an API key in the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="73a67-283">By default, an HTTP trigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="73a67-284">So your HTTP request normally looks like the following:</span><span class="sxs-lookup"><span data-stu-id="73a67-284">So your HTTP request normally looks like the following:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="73a67-285">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span><span class="sxs-lookup"><span data-stu-id="73a67-285">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="73a67-286">The value of the key can be any function key defined for the function, or any host key.</span><span class="sxs-lookup"><span data-stu-id="73a67-286">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="73a67-287">You can allow anonymous requests, which do not require keys.</span><span class="sxs-lookup"><span data-stu-id="73a67-287">You can allow anonymous requests, which do not require keys.</span></span> <span data-ttu-id="73a67-288">You can also require that the master key be used.</span><span class="sxs-lookup"><span data-stu-id="73a67-288">You can also require that the master key be used.</span></span> <span data-ttu-id="73a67-289">You change the default authorization level by using the `authLevel` property in the binding JSON.</span><span class="sxs-lookup"><span data-stu-id="73a67-289">You change the default authorization level by using the `authLevel` property in the binding JSON.</span></span> <span data-ttu-id="73a67-290">For more information, see [Trigger - configuration](#trigger---configuration).</span><span class="sxs-lookup"><span data-stu-id="73a67-290">For more information, see [Trigger - configuration](#trigger---configuration).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="73a67-291">Keys and webhooks</span><span class="sxs-lookup"><span data-stu-id="73a67-291">Keys and webhooks</span></span>

<span data-ttu-id="73a67-292">Webhook authorization is handled by the webhook receiver component, part of the HTTP trigger, and the mechanism varies based on the webhook type.</span><span class="sxs-lookup"><span data-stu-id="73a67-292">Webhook authorization is handled by the webhook receiver component, part of the HTTP trigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="73a67-293">Each mechanism does, however rely on a key.</span><span class="sxs-lookup"><span data-stu-id="73a67-293">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="73a67-294">By default, the function key named "default" is used.</span><span class="sxs-lookup"><span data-stu-id="73a67-294">By default, the function key named "default" is used.</span></span> <span data-ttu-id="73a67-295">To use a different key, configure the webhook provider to send the key name with the request in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="73a67-295">To use a different key, configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="73a67-296">**Query string**: The provider passes the key name in the `clientid` query string parameter, such as `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`.</span><span class="sxs-lookup"><span data-stu-id="73a67-296">**Query string**: The provider passes the key name in the `clientid` query string parameter, such as `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`.</span></span>
- <span data-ttu-id="73a67-297">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span><span class="sxs-lookup"><span data-stu-id="73a67-297">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

## <a name="trigger---limits"></a><span data-ttu-id="73a67-298">Trigger - limits</span><span class="sxs-lookup"><span data-stu-id="73a67-298">Trigger - limits</span></span>

<span data-ttu-id="73a67-299">The HTTP request length is limited to 100MB (104,857,600 bytes), and the URL length is limited to 4KB (4,096 bytes).</span><span class="sxs-lookup"><span data-stu-id="73a67-299">The HTTP request length is limited to 100MB (104,857,600 bytes), and the URL length is limited to 4KB (4,096 bytes).</span></span> <span data-ttu-id="73a67-300">These limits are specified by the `httpRuntime` element of the runtime's [Web.config file](https://github.com/Azure/azure-webjobs-sdk-script/blob/v1.x/src/WebJobs.Script.WebHost/Web.config).</span><span class="sxs-lookup"><span data-stu-id="73a67-300">These limits are specified by the `httpRuntime` element of the runtime's [Web.config file](https://github.com/Azure/azure-webjobs-sdk-script/blob/v1.x/src/WebJobs.Script.WebHost/Web.config).</span></span>

<span data-ttu-id="73a67-301">If a function that uses the HTTP trigger doesn't complete within about 2.5 minutes, the gateway will timeout and return an HTTP 502 error.</span><span class="sxs-lookup"><span data-stu-id="73a67-301">If a function that uses the HTTP trigger doesn't complete within about 2.5 minutes, the gateway will timeout and return an HTTP 502 error.</span></span> <span data-ttu-id="73a67-302">The function will continue running but will be unable to return an HTTP response.</span><span class="sxs-lookup"><span data-stu-id="73a67-302">The function will continue running but will be unable to return an HTTP response.</span></span> <span data-ttu-id="73a67-303">For long-running functions, we recommend that you follow async patterns and return a location where you can ping the status of the request.</span><span class="sxs-lookup"><span data-stu-id="73a67-303">For long-running functions, we recommend that you follow async patterns and return a location where you can ping the status of the request.</span></span> <span data-ttu-id="73a67-304">For information about how long a function can run, see [Scale and hosting - Consumption plan](functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="73a67-304">For information about how long a function can run, see [Scale and hosting - Consumption plan](functions-scale.md#consumption-plan).</span></span> 

## <a name="trigger---hostjson-properties"></a><span data-ttu-id="73a67-305">Trigger - host.json properties</span><span class="sxs-lookup"><span data-stu-id="73a67-305">Trigger - host.json properties</span></span>

<span data-ttu-id="73a67-306">The [host.json](functions-host-json.md) file contains settings that control HTTP trigger behavior.</span><span class="sxs-lookup"><span data-stu-id="73a67-306">The [host.json](functions-host-json.md) file contains settings that control HTTP trigger behavior.</span></span>

[!INCLUDE [functions-host-json-http](../../includes/functions-host-json-http.md)]

## <a name="output"></a><span data-ttu-id="73a67-307">Output</span><span class="sxs-lookup"><span data-stu-id="73a67-307">Output</span></span>

<span data-ttu-id="73a67-308">Use the HTTP output binding to respond to the HTTP request sender.</span><span class="sxs-lookup"><span data-stu-id="73a67-308">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="73a67-309">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span><span class="sxs-lookup"><span data-stu-id="73a67-309">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="73a67-310">If an HTTP output binding is not provided, an HTTP trigger returns HTTP 200 OK with an empty body in Functions 1.x, or HTTP 204 No Content with an empty body in Functions 2.x.</span><span class="sxs-lookup"><span data-stu-id="73a67-310">If an HTTP output binding is not provided, an HTTP trigger returns HTTP 200 OK with an empty body in Functions 1.x, or HTTP 204 No Content with an empty body in Functions 2.x.</span></span>

## <a name="output---configuration"></a><span data-ttu-id="73a67-311">Output - configuration</span><span class="sxs-lookup"><span data-stu-id="73a67-311">Output - configuration</span></span>

<span data-ttu-id="73a67-312">The following table explains the binding configuration properties that you set in the *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="73a67-312">The following table explains the binding configuration properties that you set in the *function.json* file.</span></span> <span data-ttu-id="73a67-313">For C# class libraries there are no attribute properties that correspond to these *function.json* properties.</span><span class="sxs-lookup"><span data-stu-id="73a67-313">For C# class libraries there are no attribute properties that correspond to these *function.json* properties.</span></span> 

|<span data-ttu-id="73a67-314">Property</span><span class="sxs-lookup"><span data-stu-id="73a67-314">Property</span></span>  |<span data-ttu-id="73a67-315">Description</span><span class="sxs-lookup"><span data-stu-id="73a67-315">Description</span></span>  |
|---------|---------|
| <span data-ttu-id="73a67-316">**type**</span><span class="sxs-lookup"><span data-stu-id="73a67-316">**type**</span></span> |<span data-ttu-id="73a67-317">Must be set to `http`.</span><span class="sxs-lookup"><span data-stu-id="73a67-317">Must be set to `http`.</span></span> |
| <span data-ttu-id="73a67-318">**direction**</span><span class="sxs-lookup"><span data-stu-id="73a67-318">**direction**</span></span> | <span data-ttu-id="73a67-319">Must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="73a67-319">Must be set to `out`.</span></span> |
|<span data-ttu-id="73a67-320">**name**</span><span class="sxs-lookup"><span data-stu-id="73a67-320">**name**</span></span> | <span data-ttu-id="73a67-321">The variable name used in function code for the response, or `$return` to use the return value.</span><span class="sxs-lookup"><span data-stu-id="73a67-321">The variable name used in function code for the response, or `$return` to use the return value.</span></span> |

## <a name="output---usage"></a><span data-ttu-id="73a67-322">Output - usage</span><span class="sxs-lookup"><span data-stu-id="73a67-322">Output - usage</span></span>

<span data-ttu-id="73a67-323">To send an HTTP response, use the language-standard response patterns.</span><span class="sxs-lookup"><span data-stu-id="73a67-323">To send an HTTP response, use the language-standard response patterns.</span></span> <span data-ttu-id="73a67-324">In C# or C# script, make the function return type `HttpResponseMessage` or `Task<HttpResponseMessage>`.</span><span class="sxs-lookup"><span data-stu-id="73a67-324">In C# or C# script, make the function return type `HttpResponseMessage` or `Task<HttpResponseMessage>`.</span></span> <span data-ttu-id="73a67-325">In C#, a return value attribute isn't required.</span><span class="sxs-lookup"><span data-stu-id="73a67-325">In C#, a return value attribute isn't required.</span></span>

<span data-ttu-id="73a67-326">For example responses, see the [trigger example](#trigger---example) and the [webhook example](#trigger---webhook-example).</span><span class="sxs-lookup"><span data-stu-id="73a67-326">For example responses, see the [trigger example](#trigger---example) and the [webhook example](#trigger---webhook-example).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73a67-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="73a67-327">Next steps</span></span>

[<span data-ttu-id="73a67-328">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="73a67-328">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
