---
title: Working with proxies in Azure Functions | Microsoft Docs
description: Overview of how to use Azure Functions Proxies
services: functions
documentationcenter: ''
author: mattchenderson
manager: erikre
editor: ''
ms.assetid: ''
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 02/19/2017
ms.author: mahender
ms.openlocfilehash: 3e8b8f9908cf24baf7a5d70521c79dbd470001f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563893"
---
# <a name="working-with-azure-functions-proxies-preview"></a><span data-ttu-id="60bdf-103">Working with Azure Functions Proxies (preview)</span><span class="sxs-lookup"><span data-stu-id="60bdf-103">Working with Azure Functions Proxies (preview)</span></span>

> [!Note] 
> <span data-ttu-id="60bdf-104">Azure Functions Proxies is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="60bdf-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="60bdf-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span><span class="sxs-lookup"><span data-stu-id="60bdf-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="60bdf-106">See [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/) for more information.</span><span class="sxs-lookup"><span data-stu-id="60bdf-106">See [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/) for more information.</span></span>

<span data-ttu-id="60bdf-107">This article explains how to configure and work with Azure Functions Proxies.</span><span class="sxs-lookup"><span data-stu-id="60bdf-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="60bdf-108">This feature allows you to specify endpoints on your function app that are implemented by another resource.</span><span class="sxs-lookup"><span data-stu-id="60bdf-108">This feature allows you to specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="60bdf-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span><span class="sxs-lookup"><span data-stu-id="60bdf-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a><span data-ttu-id="60bdf-110">Enabling Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="60bdf-110">Enabling Azure Functions Proxies</span></span>

<span data-ttu-id="60bdf-111">Proxies are not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="60bdf-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="60bdf-112">You can create proxies while the feature is disabled, but they will not execute.</span><span class="sxs-lookup"><span data-stu-id="60bdf-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="60bdf-113">The following steps will show you how to enable proxies:</span><span class="sxs-lookup"><span data-stu-id="60bdf-113">The following steps will show you how to enable proxies:</span></span>

1. <span data-ttu-id="60bdf-114">Open the [Azure portal] and navigate to your function app.</span><span class="sxs-lookup"><span data-stu-id="60bdf-114">Open the [Azure portal] and navigate to your function app.</span></span>
2. <span data-ttu-id="60bdf-115">Select **Function app settings**.</span><span class="sxs-lookup"><span data-stu-id="60bdf-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="60bdf-116">Toggle **Enable Azure Functions Proxies (preview)** to On.</span><span class="sxs-lookup"><span data-stu-id="60bdf-116">Toggle **Enable Azure Functions Proxies (preview)** to On.</span></span>

<span data-ttu-id="60bdf-117">You can also return here to update the proxy runtime as new features become available.</span><span class="sxs-lookup"><span data-stu-id="60bdf-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <a name="creating-a-proxy"></a><span data-ttu-id="60bdf-118">Creating a proxy</span><span class="sxs-lookup"><span data-stu-id="60bdf-118">Creating a proxy</span></span>

<span data-ttu-id="60bdf-119">This section will show you how to create a proxy in the Functions portal.</span><span class="sxs-lookup"><span data-stu-id="60bdf-119">This section will show you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="60bdf-120">Open the [Azure portal] and navigate to your function app.</span><span class="sxs-lookup"><span data-stu-id="60bdf-120">Open the [Azure portal] and navigate to your function app.</span></span>
2. <span data-ttu-id="60bdf-121">In the left-hand navigation, select **New proxy**.</span><span class="sxs-lookup"><span data-stu-id="60bdf-121">In the left-hand navigation, select **New proxy**.</span></span>
3. <span data-ttu-id="60bdf-122">Provide a name for your proxy.</span><span class="sxs-lookup"><span data-stu-id="60bdf-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="60bdf-123">Configure the endpoint exposed on this function app by specifying the **route template** and **HTTP methods**.</span><span class="sxs-lookup"><span data-stu-id="60bdf-123">Configure the endpoint exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="60bdf-124">These parameters behave according to the rules for [HTTP triggers]</span><span class="sxs-lookup"><span data-stu-id="60bdf-124">These parameters behave according to the rules for [HTTP triggers]</span></span>
5. <span data-ttu-id="60bdf-125">Set the **backend URL** to another endpoint.</span><span class="sxs-lookup"><span data-stu-id="60bdf-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="60bdf-126">This could be a function in another function app, or it could be any other API.</span><span class="sxs-lookup"><span data-stu-id="60bdf-126">This could be a function in another function app, or it could be any other API.</span></span>
6. <span data-ttu-id="60bdf-127">Click Create.</span><span class="sxs-lookup"><span data-stu-id="60bdf-127">Click Create.</span></span>

<span data-ttu-id="60bdf-128">Your proxy now exists as a new endpoint on your function app.</span><span class="sxs-lookup"><span data-stu-id="60bdf-128">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="60bdf-129">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="60bdf-129">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="60bdf-130">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span><span class="sxs-lookup"><span data-stu-id="60bdf-130">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>


## <a name="modify-requests"></a><span data-ttu-id="60bdf-131">Modifying backend requests</span><span class="sxs-lookup"><span data-stu-id="60bdf-131">Modifying backend requests</span></span>

<span data-ttu-id="60bdf-132">The backend URL parameter does not need to be static.</span><span class="sxs-lookup"><span data-stu-id="60bdf-132">The backend URL parameter does not need to be static.</span></span> <span data-ttu-id="60bdf-133">You can condition it on input from the request or application settings.</span><span class="sxs-lookup"><span data-stu-id="60bdf-133">You can condition it on input from the request or application settings.</span></span>


### <a name="using-request-parameters"></a><span data-ttu-id="60bdf-134">Using request parameters</span><span class="sxs-lookup"><span data-stu-id="60bdf-134">Using request parameters</span></span>

<span data-ttu-id="60bdf-135">Parameters used in the route template may be used as inputs to the backend URL property.</span><span class="sxs-lookup"><span data-stu-id="60bdf-135">Parameters used in the route template may be used as inputs to the backend URL property.</span></span> <span data-ttu-id="60bdf-136">Values are referenced by name, enclosed in curly braces "{}".</span><span class="sxs-lookup"><span data-stu-id="60bdf-136">Values are referenced by name, enclosed in curly braces "{}".</span></span>

<span data-ttu-id="60bdf-137">For example, if a proxy has a route template like `/pets/{petId}`, the backend URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="60bdf-137">For example, if a proxy has a route template like `/pets/{petId}`, the backend URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="60bdf-138">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` will be a string representation of the remaining path segments from the incoming request.</span><span class="sxs-lookup"><span data-stu-id="60bdf-138">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` will be a string representation of the remaining path segments from the incoming request.</span></span>


### <a name="using-application-settings"></a><span data-ttu-id="60bdf-139">Using application settings</span><span class="sxs-lookup"><span data-stu-id="60bdf-139">Using application settings</span></span>

<span data-ttu-id="60bdf-140">You can also reference [application settings](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs '%'.</span><span class="sxs-lookup"><span data-stu-id="60bdf-140">You can also reference [application settings](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs '%'.</span></span>

<span data-ttu-id="60bdf-141">For example, a backend URL of `https://%ORDER_PROCESSING_HOST%/api/orders` will have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span><span class="sxs-lookup"><span data-stu-id="60bdf-141">For example, a backend URL of `https://%ORDER_PROCESSING_HOST%/api/orders` will have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="60bdf-142">Use application settings for backend hosts when you have multiple deployments or test environments.</span><span class="sxs-lookup"><span data-stu-id="60bdf-142">Use application settings for backend hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="60bdf-143">That way, you can make sure that you are always talking to the right backend for that environment.</span><span class="sxs-lookup"><span data-stu-id="60bdf-143">That way, you can make sure that you are always talking to the right backend for that environment.</span></span>



## <a name="deployment-methods"></a><span data-ttu-id="60bdf-144">Deployment methods</span><span class="sxs-lookup"><span data-stu-id="60bdf-144">Deployment methods</span></span>

<span data-ttu-id="60bdf-145">The proxies that you configure are stored in a proxies.json file, located in the root of a function app directory.</span><span class="sxs-lookup"><span data-stu-id="60bdf-145">The proxies that you configure are stored in a proxies.json file, located in the root of a function app directory.</span></span> <span data-ttu-id="60bdf-146">You can manually edit this file and deploy it as part of your app when using any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span><span class="sxs-lookup"><span data-stu-id="60bdf-146">You can manually edit this file and deploy it as part of your app when using any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span>

<span data-ttu-id="60bdf-147">The feature must be enabled in order for the file to be processed.</span><span class="sxs-lookup"><span data-stu-id="60bdf-147">The feature must be enabled in order for the file to be processed.</span></span> <span data-ttu-id="60bdf-148">You can do this by following the instructions in [Enabling Azure Functions Proxies](#enable).</span><span class="sxs-lookup"><span data-stu-id="60bdf-148">You can do this by following the instructions in [Enabling Azure Functions Proxies](#enable).</span></span>

<span data-ttu-id="60bdf-149">Proxies.json is defined by a proxies object, composed of named proxies and their definitions.</span><span class="sxs-lookup"><span data-stu-id="60bdf-149">Proxies.json is defined by a proxies object, composed of named proxies and their definitions.</span></span> <span data-ttu-id="60bdf-150">An example file might look like the following:</span><span class="sxs-lookup"><span data-stu-id="60bdf-150">An example file might look like the following:</span></span>

```json
{
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="60bdf-151">Each proxy has a friendly name, such as "proxy1" in the example above.</span><span class="sxs-lookup"><span data-stu-id="60bdf-151">Each proxy has a friendly name, such as "proxy1" in the example above.</span></span> <span data-ttu-id="60bdf-152">The corresponding proxy definition object is defined by the following properties:</span><span class="sxs-lookup"><span data-stu-id="60bdf-152">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="60bdf-153">**matchCondition** : Required - an object defining the requests that will trigger the execution of this proxy.</span><span class="sxs-lookup"><span data-stu-id="60bdf-153">**matchCondition** : Required - an object defining the requests that will trigger the execution of this proxy.</span></span> <span data-ttu-id="60bdf-154">It contains two properties shared with [HTTP triggers]:</span><span class="sxs-lookup"><span data-stu-id="60bdf-154">It contains two properties shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="60bdf-155">_methods_ : This is an array of the HTTP methods to which the proxy will respond.</span><span class="sxs-lookup"><span data-stu-id="60bdf-155">_methods_ : This is an array of the HTTP methods to which the proxy will respond.</span></span> <span data-ttu-id="60bdf-156">If not specified, the proxy will respond to all HTTP methods on the route.</span><span class="sxs-lookup"><span data-stu-id="60bdf-156">If not specified, the proxy will respond to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="60bdf-157">_route_ : Required - This defines the route template, controlling to which request URLs your proxy will respond.</span><span class="sxs-lookup"><span data-stu-id="60bdf-157">_route_ : Required - This defines the route template, controlling to which request URLs your proxy will respond.</span></span> <span data-ttu-id="60bdf-158">Unlike in HTTP triggers, there is no default value.</span><span class="sxs-lookup"><span data-stu-id="60bdf-158">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="60bdf-159">**backendUri** : The URL of the backend resource to which the request should be proxied.</span><span class="sxs-lookup"><span data-stu-id="60bdf-159">**backendUri** : The URL of the backend resource to which the request should be proxied.</span></span> <span data-ttu-id="60bdf-160">This value may be templated, as described in [Modifying backend requests](#modify-requests).</span><span class="sxs-lookup"><span data-stu-id="60bdf-160">This value may be templated, as described in [Modifying backend requests](#modify-requests).</span></span> <span data-ttu-id="60bdf-161">If this property is not included, Azure Functions will respond with an HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="60bdf-161">If this property is not included, Azure Functions will respond with an HTTP 200 OK.</span></span>

> [!Note] 
> <span data-ttu-id="60bdf-162">The route property Azure Functions Proxies do not honor the routePrefix property of the Functions host configuration.</span><span class="sxs-lookup"><span data-stu-id="60bdf-162">The route property Azure Functions Proxies do not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="60bdf-163">If you wish to include a prefix such as /api, it must be included in the route property.</span><span class="sxs-lookup"><span data-stu-id="60bdf-163">If you wish to include a prefix such as /api, it must be included in the route property.</span></span>



[Azure portal]: https://portal.azure.com
[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger