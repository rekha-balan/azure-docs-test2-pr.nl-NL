---
title: Azure Functions HTTP and webhook bindings | Microsoft Docs
description: Understand how to use HTTP and webhook triggers and bindings in Azure Functions.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture, HTTP, API, REST
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: 7a088dd76a33f6a7d7a0d96e3d75a13b8e2da12f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556520"
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="45108-104">Azure Functions HTTP and webhook bindings</span><span class="sxs-lookup"><span data-stu-id="45108-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="45108-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="45108-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="45108-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span><span class="sxs-lookup"><span data-stu-id="45108-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="45108-107">Azure Functions provides the following bindings:</span><span class="sxs-lookup"><span data-stu-id="45108-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="45108-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="45108-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="45108-109">This can be customized to respond to [webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="45108-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="45108-110">An [HTTP output binding](#output) allows you to respond to the request.</span><span class="sxs-lookup"><span data-stu-id="45108-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!TIP]
>
> <span data-ttu-id="45108-111">We suggest reading this best practices document on [HTTPClient](https://github.com/mspnp/performance-optimization/blob/master/ImproperInstantiation/docs/ImproperInstantiation.md).</span><span class="sxs-lookup"><span data-stu-id="45108-111">We suggest reading this best practices document on [HTTPClient](https://github.com/mspnp/performance-optimization/blob/master/ImproperInstantiation/docs/ImproperInstantiation.md).</span></span>
>

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="45108-112">HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="45108-112">HTTP trigger</span></span>
<span data-ttu-id="45108-113">The HTTP trigger will execute your function in response to an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="45108-113">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="45108-114">You can customize it to respond to a particular URL or set of HTTP methods.</span><span class="sxs-lookup"><span data-stu-id="45108-114">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="45108-115">An HTTP trigger can also be configured to respond to webhooks.</span><span class="sxs-lookup"><span data-stu-id="45108-115">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="45108-116">If using the Functions portal, you can also get started right away using a pre-made template.</span><span class="sxs-lookup"><span data-stu-id="45108-116">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="45108-117">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span><span class="sxs-lookup"><span data-stu-id="45108-117">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="45108-118">Select one of the templates and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="45108-118">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="45108-119">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span><span class="sxs-lookup"><span data-stu-id="45108-119">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="45108-120">To modify the response, configure an [HTTP output binding](#output)</span><span class="sxs-lookup"><span data-stu-id="45108-120">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="45108-121">Configuring an HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="45108-121">Configuring an HTTP trigger</span></span>
<span data-ttu-id="45108-122">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="45108-122">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "GET" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="45108-123">The binding supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="45108-123">The binding supports the following properties:</span></span>

* <span data-ttu-id="45108-124">**name** : Required - the variable name used in function code for the request or request body.</span><span class="sxs-lookup"><span data-stu-id="45108-124">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="45108-125">See [Working with an HTTP trigger from code](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="45108-125">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="45108-126">**type** : Required - must be set to "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="45108-126">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="45108-127">**direction** : Required - must be set to "in".</span><span class="sxs-lookup"><span data-stu-id="45108-127">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="45108-128">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span><span class="sxs-lookup"><span data-stu-id="45108-128">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="45108-129">See [Working with keys](#keys) below.</span><span class="sxs-lookup"><span data-stu-id="45108-129">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="45108-130">The value can be one of the following:</span><span class="sxs-lookup"><span data-stu-id="45108-130">The value can be one of the following:</span></span>
    * <span data-ttu-id="45108-131">_anonymous_: No API key is required.</span><span class="sxs-lookup"><span data-stu-id="45108-131">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="45108-132">_function_: A function-specific API key is required.</span><span class="sxs-lookup"><span data-stu-id="45108-132">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="45108-133">This is the default value if none is provided.</span><span class="sxs-lookup"><span data-stu-id="45108-133">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="45108-134">_admin_ : The master key is required.</span><span class="sxs-lookup"><span data-stu-id="45108-134">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="45108-135">**methods** : This is an array of the HTTP methods to which the function will respond.</span><span class="sxs-lookup"><span data-stu-id="45108-135">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="45108-136">If not specified, the function will respond to all HTTP methods.</span><span class="sxs-lookup"><span data-stu-id="45108-136">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="45108-137">See [Customizing the HTTP endpoint](#url).</span><span class="sxs-lookup"><span data-stu-id="45108-137">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="45108-138">**route** : This defines the route template, controlling to which request URLs your function will respond.</span><span class="sxs-lookup"><span data-stu-id="45108-138">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="45108-139">The default value if none is provided is `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="45108-139">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="45108-140">See [Customizing the HTTP endpoint](#url).</span><span class="sxs-lookup"><span data-stu-id="45108-140">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="45108-141">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span><span class="sxs-lookup"><span data-stu-id="45108-141">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="45108-142">The _methods_ property should not be set if this is chosen.</span><span class="sxs-lookup"><span data-stu-id="45108-142">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="45108-143">See [Responding to webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="45108-143">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="45108-144">The value can be one of the following:</span><span class="sxs-lookup"><span data-stu-id="45108-144">The value can be one of the following:</span></span>
    * <span data-ttu-id="45108-145">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span><span class="sxs-lookup"><span data-stu-id="45108-145">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="45108-146">_github_ : The function will respond to GitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="45108-146">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="45108-147">The _authLevel_ property should not be set if this is chosen.</span><span class="sxs-lookup"><span data-stu-id="45108-147">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="45108-148">_slack_ : The function will respond to Slack webhooks.</span><span class="sxs-lookup"><span data-stu-id="45108-148">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="45108-149">The _authLevel_ property should not be set if this is chosen.</span><span class="sxs-lookup"><span data-stu-id="45108-149">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="45108-150">Working with an HTTP trigger from code</span><span class="sxs-lookup"><span data-stu-id="45108-150">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="45108-151">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span><span class="sxs-lookup"><span data-stu-id="45108-151">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="45108-152">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span><span class="sxs-lookup"><span data-stu-id="45108-152">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="45108-153">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span><span class="sxs-lookup"><span data-stu-id="45108-153">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="45108-154">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span><span class="sxs-lookup"><span data-stu-id="45108-154">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="45108-155">See [HTTP trigger samples](#httptriggersample) for example usages.</span><span class="sxs-lookup"><span data-stu-id="45108-155">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="45108-156">HTTP response output binding</span><span class="sxs-lookup"><span data-stu-id="45108-156">HTTP response output binding</span></span>
<span data-ttu-id="45108-157">Use the HTTP output binding to respond to the HTTP request sender.</span><span class="sxs-lookup"><span data-stu-id="45108-157">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="45108-158">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span><span class="sxs-lookup"><span data-stu-id="45108-158">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="45108-159">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span><span class="sxs-lookup"><span data-stu-id="45108-159">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="45108-160">Configuring an HTTP output binding</span><span class="sxs-lookup"><span data-stu-id="45108-160">Configuring an HTTP output binding</span></span>
<span data-ttu-id="45108-161">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="45108-161">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="45108-162">The binding contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="45108-162">The binding contains the following properties:</span></span>

* <span data-ttu-id="45108-163">**name** : Required - the variable name used in function code for the response.</span><span class="sxs-lookup"><span data-stu-id="45108-163">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="45108-164">See [Working with an HTTP output binding from code](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="45108-164">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="45108-165">**type** : Required - must be set to "http".</span><span class="sxs-lookup"><span data-stu-id="45108-165">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="45108-166">**direction** : Required - must be set to "out".</span><span class="sxs-lookup"><span data-stu-id="45108-166">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="45108-167">Working with an HTTP output binding from code</span><span class="sxs-lookup"><span data-stu-id="45108-167">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="45108-168">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span><span class="sxs-lookup"><span data-stu-id="45108-168">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="45108-169">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span><span class="sxs-lookup"><span data-stu-id="45108-169">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="45108-170">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="45108-170">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="45108-171">Responding to webhooks</span><span class="sxs-lookup"><span data-stu-id="45108-171">Responding to webhooks</span></span>
<span data-ttu-id="45108-172">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="45108-172">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="45108-173">The basic configuration uses the "genericJson" setting.</span><span class="sxs-lookup"><span data-stu-id="45108-173">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="45108-174">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span><span class="sxs-lookup"><span data-stu-id="45108-174">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="45108-175">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="45108-175">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="45108-176">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span><span class="sxs-lookup"><span data-stu-id="45108-176">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="45108-177">Configuring GitHub as a webhook provider</span><span class="sxs-lookup"><span data-stu-id="45108-177">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="45108-178">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span><span class="sxs-lookup"><span data-stu-id="45108-178">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="45108-179">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span><span class="sxs-lookup"><span data-stu-id="45108-179">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="45108-180">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span><span class="sxs-lookup"><span data-stu-id="45108-180">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="45108-181">Configuring Slack as a webhook provider</span><span class="sxs-lookup"><span data-stu-id="45108-181">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="45108-182">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span><span class="sxs-lookup"><span data-stu-id="45108-182">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="45108-183">See [Working with keys](#keys).</span><span class="sxs-lookup"><span data-stu-id="45108-183">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="45108-184">Customizing the HTTP endpoint</span><span class="sxs-lookup"><span data-stu-id="45108-184">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="45108-185">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span><span class="sxs-lookup"><span data-stu-id="45108-185">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="45108-186">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span><span class="sxs-lookup"><span data-stu-id="45108-186">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="45108-187">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span><span class="sxs-lookup"><span data-stu-id="45108-187">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="45108-188">Using this configuration, the function is now addressable with the following route instead of the original route.</span><span class="sxs-lookup"><span data-stu-id="45108-188">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="45108-189">This allows the function code to support two parameters in the address, "category" and "id".</span><span class="sxs-lookup"><span data-stu-id="45108-189">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="45108-190">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span><span class="sxs-lookup"><span data-stu-id="45108-190">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="45108-191">The following C# function code makes use of both parameters.</span><span class="sxs-lookup"><span data-stu-id="45108-191">The following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage request, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="45108-192">Here is Node.js function code to use the same route parameters.</span><span class="sxs-lookup"><span data-stu-id="45108-192">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="45108-193">By default, all function routes are prefixed with *api*.</span><span class="sxs-lookup"><span data-stu-id="45108-193">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="45108-194">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="45108-194">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="45108-195">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="45108-195">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="45108-196">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="45108-196">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="45108-197">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="45108-197">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="45108-198">Working with keys</span><span class="sxs-lookup"><span data-stu-id="45108-198">Working with keys</span></span>
<span data-ttu-id="45108-199">HttpTriggers can leverage keys for added security.</span><span class="sxs-lookup"><span data-stu-id="45108-199">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="45108-200">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span><span class="sxs-lookup"><span data-stu-id="45108-200">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="45108-201">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span><span class="sxs-lookup"><span data-stu-id="45108-201">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="45108-202">Keys are stored as part of your function app in Azure and are encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="45108-202">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="45108-203">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span><span class="sxs-lookup"><span data-stu-id="45108-203">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="45108-204">There are two types of keys:</span><span class="sxs-lookup"><span data-stu-id="45108-204">There are two types of keys:</span></span>
- <span data-ttu-id="45108-205">**Host keys**: These keys are shared by all functions within the function app.</span><span class="sxs-lookup"><span data-stu-id="45108-205">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="45108-206">When used as an API key, these allow access to any function within the function app.</span><span class="sxs-lookup"><span data-stu-id="45108-206">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="45108-207">**Function keys**: These keys apply only to the specific functions under which they are defined.</span><span class="sxs-lookup"><span data-stu-id="45108-207">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="45108-208">When used as an API key, these only allow access to that function.</span><span class="sxs-lookup"><span data-stu-id="45108-208">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="45108-209">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span><span class="sxs-lookup"><span data-stu-id="45108-209">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="45108-210">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span><span class="sxs-lookup"><span data-stu-id="45108-210">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="45108-211">It provides administrative access to the runtime APIs.</span><span class="sxs-lookup"><span data-stu-id="45108-211">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="45108-212">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span><span class="sxs-lookup"><span data-stu-id="45108-212">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="45108-213">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span><span class="sxs-lookup"><span data-stu-id="45108-213">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="45108-214">Exercise caution when choosing the admin authorization level.</span><span class="sxs-lookup"><span data-stu-id="45108-214">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="45108-215">API key authorization</span><span class="sxs-lookup"><span data-stu-id="45108-215">API key authorization</span></span>
<span data-ttu-id="45108-216">By default, an HttpTrigger requires an API key in the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="45108-216">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="45108-217">So your HTTP request normally looks like this:</span><span class="sxs-lookup"><span data-stu-id="45108-217">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="45108-218">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span><span class="sxs-lookup"><span data-stu-id="45108-218">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="45108-219">The value of the key can be any function key defined for the function, or any host key.</span><span class="sxs-lookup"><span data-stu-id="45108-219">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="45108-220">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="45108-220">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="45108-221">Keys and webhooks</span><span class="sxs-lookup"><span data-stu-id="45108-221">Keys and webhooks</span></span>
<span data-ttu-id="45108-222">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span><span class="sxs-lookup"><span data-stu-id="45108-222">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="45108-223">Each mechanism does, however rely on a key.</span><span class="sxs-lookup"><span data-stu-id="45108-223">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="45108-224">By default, the function key named "default" will be used.</span><span class="sxs-lookup"><span data-stu-id="45108-224">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="45108-225">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="45108-225">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="45108-226">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="45108-226">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="45108-227">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span><span class="sxs-lookup"><span data-stu-id="45108-227">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="45108-228">Function keys take precedence over host keys.</span><span class="sxs-lookup"><span data-stu-id="45108-228">Function keys take precedence over host keys.</span></span> <span data-ttu-id="45108-229">If two keys are defined with the same name, the function key will be used.</span><span class="sxs-lookup"><span data-stu-id="45108-229">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="45108-230">HTTP trigger samples</span><span class="sxs-lookup"><span data-stu-id="45108-230">HTTP trigger samples</span></span>
<span data-ttu-id="45108-231">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="45108-231">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="45108-232">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="45108-232">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="45108-233">C#</span><span class="sxs-lookup"><span data-stu-id="45108-233">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="45108-234">F#</span><span class="sxs-lookup"><span data-stu-id="45108-234">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="45108-235">Node.js</span><span class="sxs-lookup"><span data-stu-id="45108-235">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="45108-236">HTTP trigger sample in C#</span><span class="sxs-lookup"><span data-stu-id="45108-236">HTTP trigger sample in C#</span></span> #
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

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="45108-237">HTTP trigger sample in F#</span><span class="sxs-lookup"><span data-stu-id="45108-237">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="45108-238">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span><span class="sxs-lookup"><span data-stu-id="45108-238">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="45108-239">This will use NuGet to fetch your dependencies and will reference them in your script.</span><span class="sxs-lookup"><span data-stu-id="45108-239">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="45108-240">HTTP trigger sample in Node.JS</span><span class="sxs-lookup"><span data-stu-id="45108-240">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
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



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="45108-241">Webhook samples</span><span class="sxs-lookup"><span data-stu-id="45108-241">Webhook samples</span></span>
<span data-ttu-id="45108-242">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="45108-242">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="45108-243">See the language-specific sample that logs GitHub issue comments.</span><span class="sxs-lookup"><span data-stu-id="45108-243">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="45108-244">C#</span><span class="sxs-lookup"><span data-stu-id="45108-244">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="45108-245">F#</span><span class="sxs-lookup"><span data-stu-id="45108-245">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="45108-246">Node.js</span><span class="sxs-lookup"><span data-stu-id="45108-246">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="45108-247">Webhook sample in C#</span><span class="sxs-lookup"><span data-stu-id="45108-247">Webhook sample in C#</span></span> #
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

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="45108-248">Webhook sample in F#</span><span class="sxs-lookup"><span data-stu-id="45108-248">Webhook sample in F#</span></span> #
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

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="45108-249">Webhook sample in Node.JS</span><span class="sxs-lookup"><span data-stu-id="45108-249">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="45108-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="45108-250">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


