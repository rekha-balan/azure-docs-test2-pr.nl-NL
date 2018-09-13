---
title: Work with proxies in Azure Functions | Microsoft Docs
description: Overview of how to use Azure Functions Proxies
services: functions
author: alexkarcher-msft
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: alkarche
ms.openlocfilehash: 2aa8036149f4056f2d197f0712b86104f5cf2215
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44816054"
---
# <a name="work-with-azure-functions-proxies"></a><span data-ttu-id="5071e-103">Work with Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="5071e-103">Work with Azure Functions Proxies</span></span>

<span data-ttu-id="5071e-104">This article explains how to configure and work with Azure Functions Proxies.</span><span class="sxs-lookup"><span data-stu-id="5071e-104">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="5071e-105">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span><span class="sxs-lookup"><span data-stu-id="5071e-105">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="5071e-106">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span><span class="sxs-lookup"><span data-stu-id="5071e-106">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE] 
> <span data-ttu-id="5071e-107">Standard Functions billing applies to proxy executions.</span><span class="sxs-lookup"><span data-stu-id="5071e-107">Standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="5071e-108">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="5071e-108">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

## <a name="create"></a><span data-ttu-id="5071e-109">Create a proxy</span><span class="sxs-lookup"><span data-stu-id="5071e-109">Create a proxy</span></span>

<span data-ttu-id="5071e-110">This section shows you how to create a proxy in the Functions portal.</span><span class="sxs-lookup"><span data-stu-id="5071e-110">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="5071e-111">Open the [Azure portal], and then go to your function app.</span><span class="sxs-lookup"><span data-stu-id="5071e-111">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="5071e-112">In the left pane, select **New proxy**.</span><span class="sxs-lookup"><span data-stu-id="5071e-112">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="5071e-113">Provide a name for your proxy.</span><span class="sxs-lookup"><span data-stu-id="5071e-113">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="5071e-114">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span><span class="sxs-lookup"><span data-stu-id="5071e-114">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="5071e-115">These parameters behave according to the rules for [HTTP triggers].</span><span class="sxs-lookup"><span data-stu-id="5071e-115">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="5071e-116">Set the **backend URL** to another endpoint.</span><span class="sxs-lookup"><span data-stu-id="5071e-116">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="5071e-117">This endpoint could be a function in another function app, or it could be any other API.</span><span class="sxs-lookup"><span data-stu-id="5071e-117">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="5071e-118">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span><span class="sxs-lookup"><span data-stu-id="5071e-118">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="5071e-119">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5071e-119">Click **Create**.</span></span>

<span data-ttu-id="5071e-120">Your proxy now exists as a new endpoint on your function app.</span><span class="sxs-lookup"><span data-stu-id="5071e-120">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="5071e-121">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5071e-121">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="5071e-122">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span><span class="sxs-lookup"><span data-stu-id="5071e-122">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <a name="modify-requests-responses"></a><span data-ttu-id="5071e-123">Modify requests and responses</span><span class="sxs-lookup"><span data-stu-id="5071e-123">Modify requests and responses</span></span>

<span data-ttu-id="5071e-124">With Azure Functions Proxies, you can modify requests to and responses from the back-end.</span><span class="sxs-lookup"><span data-stu-id="5071e-124">With Azure Functions Proxies, you can modify requests to and responses from the back-end.</span></span> <span data-ttu-id="5071e-125">These transformations can use variables as defined in [Use variables].</span><span class="sxs-lookup"><span data-stu-id="5071e-125">These transformations can use variables as defined in [Use variables].</span></span>

### <a name="modify-backend-request"></a><span data-ttu-id="5071e-126">Modify the back-end request</span><span class="sxs-lookup"><span data-stu-id="5071e-126">Modify the back-end request</span></span>

<span data-ttu-id="5071e-127">By default, the back-end request is initialized as a copy of the original request.</span><span class="sxs-lookup"><span data-stu-id="5071e-127">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="5071e-128">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span><span class="sxs-lookup"><span data-stu-id="5071e-128">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="5071e-129">The modified values can reference [application settings] and [parameters from the original client request].</span><span class="sxs-lookup"><span data-stu-id="5071e-129">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="5071e-130">Back-end requests can be modified in the portal by expading the *request override* section of the proxy detail page.</span><span class="sxs-lookup"><span data-stu-id="5071e-130">Back-end requests can be modified in the portal by expading the *request override* section of the proxy detail page.</span></span> 

### <a name="modify-response"></a><span data-ttu-id="5071e-131">Modify the response</span><span class="sxs-lookup"><span data-stu-id="5071e-131">Modify the response</span></span>

<span data-ttu-id="5071e-132">By default, the client response is initialized as a copy of the back-end response.</span><span class="sxs-lookup"><span data-stu-id="5071e-132">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="5071e-133">You can make changes to the response's status code, reason phrase, headers, and body.</span><span class="sxs-lookup"><span data-stu-id="5071e-133">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="5071e-134">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span><span class="sxs-lookup"><span data-stu-id="5071e-134">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="5071e-135">Back-end requests can be modified in the portal by expading the *response override* section of the proxy detail page.</span><span class="sxs-lookup"><span data-stu-id="5071e-135">Back-end requests can be modified in the portal by expading the *response override* section of the proxy detail page.</span></span> 

## <a name="using-variables"></a><span data-ttu-id="5071e-136">Use variables</span><span class="sxs-lookup"><span data-stu-id="5071e-136">Use variables</span></span>

<span data-ttu-id="5071e-137">The configuration for a proxy does not need to be static.</span><span class="sxs-lookup"><span data-stu-id="5071e-137">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="5071e-138">You can condition it to use variables from the original client request, the back-end response, or application settings.</span><span class="sxs-lookup"><span data-stu-id="5071e-138">You can condition it to use variables from the original client request, the back-end response, or application settings.</span></span>

### <a name="reference-localhost"></a><span data-ttu-id="5071e-139">Reference local functions</span><span class="sxs-lookup"><span data-stu-id="5071e-139">Reference local functions</span></span>
<span data-ttu-id="5071e-140">You can use `localhost` to reference a function inside the same function app directly, without a roundtrip proxy request.</span><span class="sxs-lookup"><span data-stu-id="5071e-140">You can use `localhost` to reference a function inside the same function app directly, without a roundtrip proxy request.</span></span>

<span data-ttu-id="5071e-141">`"backendurl": "https://localhost/api/httptriggerC#1"` will reference a local HTTP triggered function at the route `/api/httptriggerC#1`</span><span class="sxs-lookup"><span data-stu-id="5071e-141">`"backendurl": "https://localhost/api/httptriggerC#1"` will reference a local HTTP triggered function at the route `/api/httptriggerC#1`</span></span>

 
>[!Note]  
><span data-ttu-id="5071e-142">If your function uses *function, admin or sys* authorization levels, you will need to provide the code and clientId, as per the original function URL.</span><span class="sxs-lookup"><span data-stu-id="5071e-142">If your function uses *function, admin or sys* authorization levels, you will need to provide the code and clientId, as per the original function URL.</span></span> <span data-ttu-id="5071e-143">In this case the reference would look like: `"backendurl": "https://localhost/api/httptriggerC#1?code=<keyvalue>&clientId=<keyname>"`</span><span class="sxs-lookup"><span data-stu-id="5071e-143">In this case the reference would look like: `"backendurl": "https://localhost/api/httptriggerC#1?code=<keyvalue>&clientId=<keyname>"`</span></span>

### <a name="request-parameters"></a><span data-ttu-id="5071e-144">Reference request parameters</span><span class="sxs-lookup"><span data-stu-id="5071e-144">Reference request parameters</span></span>

<span data-ttu-id="5071e-145">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span><span class="sxs-lookup"><span data-stu-id="5071e-145">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="5071e-146">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span><span class="sxs-lookup"><span data-stu-id="5071e-146">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="5071e-147">Route template parameters</span><span class="sxs-lookup"><span data-stu-id="5071e-147">Route template parameters</span></span>
<span data-ttu-id="5071e-148">Parameters that are used in the route template are available to be referenced by name.</span><span class="sxs-lookup"><span data-stu-id="5071e-148">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="5071e-149">The parameter names are enclosed in braces ({}).</span><span class="sxs-lookup"><span data-stu-id="5071e-149">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="5071e-150">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="5071e-150">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="5071e-151">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span><span class="sxs-lookup"><span data-stu-id="5071e-151">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="5071e-152">Additional request parameters</span><span class="sxs-lookup"><span data-stu-id="5071e-152">Additional request parameters</span></span>
<span data-ttu-id="5071e-153">In addition to the route template parameters, the following values can be used in config values:</span><span class="sxs-lookup"><span data-stu-id="5071e-153">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="5071e-154">**{request.method}**: The HTTP method that's used on the original request.</span><span class="sxs-lookup"><span data-stu-id="5071e-154">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="5071e-155">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span><span class="sxs-lookup"><span data-stu-id="5071e-155">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="5071e-156">Replace *\<HeaderName\>* with the name of the header that you want to read.</span><span class="sxs-lookup"><span data-stu-id="5071e-156">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="5071e-157">If the header is not included on the request, the value will be the empty string.</span><span class="sxs-lookup"><span data-stu-id="5071e-157">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="5071e-158">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span><span class="sxs-lookup"><span data-stu-id="5071e-158">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="5071e-159">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span><span class="sxs-lookup"><span data-stu-id="5071e-159">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="5071e-160">If the parameter is not included on the request, the value will be the empty string.</span><span class="sxs-lookup"><span data-stu-id="5071e-160">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <a name="response-parameters"></a><span data-ttu-id="5071e-161">Reference back-end response parameters</span><span class="sxs-lookup"><span data-stu-id="5071e-161">Reference back-end response parameters</span></span>

<span data-ttu-id="5071e-162">Response parameters can be used as part of modifying the response to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-162">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="5071e-163">The following values can be used in config values:</span><span class="sxs-lookup"><span data-stu-id="5071e-163">The following values can be used in config values:</span></span>

* <span data-ttu-id="5071e-164">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span><span class="sxs-lookup"><span data-stu-id="5071e-164">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="5071e-165">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span><span class="sxs-lookup"><span data-stu-id="5071e-165">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="5071e-166">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span><span class="sxs-lookup"><span data-stu-id="5071e-166">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="5071e-167">Replace *\<HeaderName\>* with the name of the header you want to read.</span><span class="sxs-lookup"><span data-stu-id="5071e-167">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="5071e-168">If the header is not included on the response, the value will be the empty string.</span><span class="sxs-lookup"><span data-stu-id="5071e-168">If the header is not included on the response, the value will be the empty string.</span></span>

### <a name="use-appsettings"></a><span data-ttu-id="5071e-169">Reference application settings</span><span class="sxs-lookup"><span data-stu-id="5071e-169">Reference application settings</span></span>

<span data-ttu-id="5071e-170">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span><span class="sxs-lookup"><span data-stu-id="5071e-170">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="5071e-171">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span><span class="sxs-lookup"><span data-stu-id="5071e-171">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="5071e-172">Use application settings for back-end hosts when you have multiple deployments or test environments.</span><span class="sxs-lookup"><span data-stu-id="5071e-172">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="5071e-173">That way, you can make sure that you are always talking to the right back-end for that environment.</span><span class="sxs-lookup"><span data-stu-id="5071e-173">That way, you can make sure that you are always talking to the right back-end for that environment.</span></span>

## <a name="debugProxies"></a><span data-ttu-id="5071e-174">Troubleshoot Proxies</span><span class="sxs-lookup"><span data-stu-id="5071e-174">Troubleshoot Proxies</span></span>

<span data-ttu-id="5071e-175">By adding the flag `"debug":true` to any proxy in your `proxies.json` you will enable debug logging.</span><span class="sxs-lookup"><span data-stu-id="5071e-175">By adding the flag `"debug":true` to any proxy in your `proxies.json` you will enable debug logging.</span></span> <span data-ttu-id="5071e-176">Logs are stored in `D:\home\LogFiles\Application\Proxies\DetailedTrace` and accessible through the advanced tools (kudu).</span><span class="sxs-lookup"><span data-stu-id="5071e-176">Logs are stored in `D:\home\LogFiles\Application\Proxies\DetailedTrace` and accessible through the advanced tools (kudu).</span></span> <span data-ttu-id="5071e-177">Any HTTP responses will also contain a `Proxy-Trace-Location` header with a URL to access the log file.</span><span class="sxs-lookup"><span data-stu-id="5071e-177">Any HTTP responses will also contain a `Proxy-Trace-Location` header with a URL to access the log file.</span></span>

<span data-ttu-id="5071e-178">You can debug a proxy from the client side by adding a `Proxy-Trace-Enabled` header set to `true`.</span><span class="sxs-lookup"><span data-stu-id="5071e-178">You can debug a proxy from the client side by adding a `Proxy-Trace-Enabled` header set to `true`.</span></span> <span data-ttu-id="5071e-179">This will also log a trace to the file system, and return the trace URL as a header in the response.</span><span class="sxs-lookup"><span data-stu-id="5071e-179">This will also log a trace to the file system, and return the trace URL as a header in the response.</span></span>

### <a name="block-proxy-traces"></a><span data-ttu-id="5071e-180">Block proxy traces</span><span class="sxs-lookup"><span data-stu-id="5071e-180">Block proxy traces</span></span>

<span data-ttu-id="5071e-181">For security reasons you may not want to allow anyone calling your service to generate a trace.</span><span class="sxs-lookup"><span data-stu-id="5071e-181">For security reasons you may not want to allow anyone calling your service to generate a trace.</span></span> <span data-ttu-id="5071e-182">They will not be able to access the trace contents without your login credentials, but generating the trace consumes resources and exposes that you are using Function Proxies.</span><span class="sxs-lookup"><span data-stu-id="5071e-182">They will not be able to access the trace contents without your login credentials, but generating the trace consumes resources and exposes that you are using Function Proxies.</span></span>

<span data-ttu-id="5071e-183">Disable traces altogether by adding `"debug":false` to any particular proxy in your `proxies.json`.</span><span class="sxs-lookup"><span data-stu-id="5071e-183">Disable traces altogether by adding `"debug":false` to any particular proxy in your `proxies.json`.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="5071e-184">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="5071e-184">Advanced configuration</span></span>

<span data-ttu-id="5071e-185">The proxies that you configure are stored in a *proxies.json* file, which is located in the root of a function app directory.</span><span class="sxs-lookup"><span data-stu-id="5071e-185">The proxies that you configure are stored in a *proxies.json* file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="5071e-186">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span><span class="sxs-lookup"><span data-stu-id="5071e-186">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> 

> [!TIP] 
> <span data-ttu-id="5071e-187">If you have not set up one of the deployment methods, you can also work with the *proxies.json* file in the portal.</span><span class="sxs-lookup"><span data-stu-id="5071e-187">If you have not set up one of the deployment methods, you can also work with the *proxies.json* file in the portal.</span></span> <span data-ttu-id="5071e-188">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span><span class="sxs-lookup"><span data-stu-id="5071e-188">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="5071e-189">By doing so, you can view the entire file structure of your function app and then make changes.</span><span class="sxs-lookup"><span data-stu-id="5071e-189">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="5071e-190">*Proxies.json* is defined by a proxies object, which is composed of named proxies and their definitions.</span><span class="sxs-lookup"><span data-stu-id="5071e-190">*Proxies.json* is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="5071e-191">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span><span class="sxs-lookup"><span data-stu-id="5071e-191">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="5071e-192">An example file might look like the following:</span><span class="sxs-lookup"><span data-stu-id="5071e-192">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
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

<span data-ttu-id="5071e-193">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="5071e-193">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="5071e-194">The corresponding proxy definition object is defined by the following properties:</span><span class="sxs-lookup"><span data-stu-id="5071e-194">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="5071e-195">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span><span class="sxs-lookup"><span data-stu-id="5071e-195">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="5071e-196">It contains two properties that are shared with [HTTP triggers]:</span><span class="sxs-lookup"><span data-stu-id="5071e-196">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="5071e-197">_methods_: An array of the HTTP methods that the proxy responds to.</span><span class="sxs-lookup"><span data-stu-id="5071e-197">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="5071e-198">If it is not specified, the proxy responds to all HTTP methods on the route.</span><span class="sxs-lookup"><span data-stu-id="5071e-198">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="5071e-199">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span><span class="sxs-lookup"><span data-stu-id="5071e-199">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="5071e-200">Unlike in HTTP triggers, there is no default value.</span><span class="sxs-lookup"><span data-stu-id="5071e-200">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="5071e-201">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span><span class="sxs-lookup"><span data-stu-id="5071e-201">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="5071e-202">This value can reference application settings and parameters from the original client request.</span><span class="sxs-lookup"><span data-stu-id="5071e-202">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="5071e-203">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="5071e-203">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="5071e-204">**requestOverrides**: An object that defines transformations to the back-end request.</span><span class="sxs-lookup"><span data-stu-id="5071e-204">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="5071e-205">See [Define a requestOverrides object].</span><span class="sxs-lookup"><span data-stu-id="5071e-205">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="5071e-206">**responseOverrides**: An object that defines transformations to the client response.</span><span class="sxs-lookup"><span data-stu-id="5071e-206">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="5071e-207">See [Define a responseOverrides object].</span><span class="sxs-lookup"><span data-stu-id="5071e-207">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="5071e-208">The *route* property in Azure Functions Proxies does not honor the *routePrefix* property of the Function App host configuration.</span><span class="sxs-lookup"><span data-stu-id="5071e-208">The *route* property in Azure Functions Proxies does not honor the *routePrefix* property of the Function App host configuration.</span></span> <span data-ttu-id="5071e-209">If you want to include a prefix such as `/api`, it must be included in the *route* property.</span><span class="sxs-lookup"><span data-stu-id="5071e-209">If you want to include a prefix such as `/api`, it must be included in the *route* property.</span></span>

### <a name="disableProxies"></a><span data-ttu-id="5071e-210">Disable individual proxies</span><span class="sxs-lookup"><span data-stu-id="5071e-210">Disable individual proxies</span></span>

<span data-ttu-id="5071e-211">You can disable individual proxies by adding `"disabled": true` to the proxy in the `proxies.json` file.</span><span class="sxs-lookup"><span data-stu-id="5071e-211">You can disable individual proxies by adding `"disabled": true` to the proxy in the `proxies.json` file.</span></span> <span data-ttu-id="5071e-212">This will cause any requests meeting the matchCondidtion to return 404.</span><span class="sxs-lookup"><span data-stu-id="5071e-212">This will cause any requests meeting the matchCondidtion to return 404.</span></span>
```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "Root": {
            "disabled":true,
            "matchCondition": {
                "route": "/example"
            },
            "backendUri": "www.example.com"
        }
    }
}
```

### <a name="requestOverrides"></a><span data-ttu-id="5071e-213">Define a requestOverrides object</span><span class="sxs-lookup"><span data-stu-id="5071e-213">Define a requestOverrides object</span></span>

<span data-ttu-id="5071e-214">The requestOverrides object defines changes made to the request when the back-end resource is called.</span><span class="sxs-lookup"><span data-stu-id="5071e-214">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="5071e-215">The object is defined by the following properties:</span><span class="sxs-lookup"><span data-stu-id="5071e-215">The object is defined by the following properties:</span></span>

* <span data-ttu-id="5071e-216">**backend.request.method**: The HTTP method that's used to call the back-end.</span><span class="sxs-lookup"><span data-stu-id="5071e-216">**backend.request.method**: The HTTP method that's used to call the back-end.</span></span>
* <span data-ttu-id="5071e-217">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back-end.</span><span class="sxs-lookup"><span data-stu-id="5071e-217">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back-end.</span></span> <span data-ttu-id="5071e-218">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span><span class="sxs-lookup"><span data-stu-id="5071e-218">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="5071e-219">If the empty string is provided, the parameter is not included on the back-end request.</span><span class="sxs-lookup"><span data-stu-id="5071e-219">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="5071e-220">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back-end.</span><span class="sxs-lookup"><span data-stu-id="5071e-220">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back-end.</span></span> <span data-ttu-id="5071e-221">Replace *\<HeaderName\>* with the name of the header that you want to set.</span><span class="sxs-lookup"><span data-stu-id="5071e-221">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="5071e-222">If you provide the empty string, the header is not included on the back-end request.</span><span class="sxs-lookup"><span data-stu-id="5071e-222">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="5071e-223">Values can reference application settings and parameters from the original client request.</span><span class="sxs-lookup"><span data-stu-id="5071e-223">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="5071e-224">An example configuration might look like the following:</span><span class="sxs-lookup"><span data-stu-id="5071e-224">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a><span data-ttu-id="5071e-225">Define a responseOverrides object</span><span class="sxs-lookup"><span data-stu-id="5071e-225">Define a responseOverrides object</span></span>

<span data-ttu-id="5071e-226">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-226">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="5071e-227">The object is defined by the following properties:</span><span class="sxs-lookup"><span data-stu-id="5071e-227">The object is defined by the following properties:</span></span>

* <span data-ttu-id="5071e-228">**response.statusCode**: The HTTP status code to be returned to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-228">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="5071e-229">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-229">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="5071e-230">**response.body**: The string representation of the body to be returned to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-230">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="5071e-231">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span><span class="sxs-lookup"><span data-stu-id="5071e-231">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="5071e-232">Replace *\<HeaderName\>* with the name of the header that you want to set.</span><span class="sxs-lookup"><span data-stu-id="5071e-232">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="5071e-233">If you provide the empty string, the header is not included on the response.</span><span class="sxs-lookup"><span data-stu-id="5071e-233">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="5071e-234">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span><span class="sxs-lookup"><span data-stu-id="5071e-234">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="5071e-235">An example configuration might look like the following:</span><span class="sxs-lookup"><span data-stu-id="5071e-235">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="5071e-236">In this example, the response body is set directly, so no `backendUri` property is needed.</span><span class="sxs-lookup"><span data-stu-id="5071e-236">In this example, the response body is set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="5071e-237">The example shows how you might use Azure Functions Proxies for mocking APIs.</span><span class="sxs-lookup"><span data-stu-id="5071e-237">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[Azure portal]: https://portal.azure.com
[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
[Define a requestOverrides object]: #requestOverrides
[Define a responseOverrides object]: #responseOverrides
[application settings]: #use-appsettings
[Use variables]: #using-variables
[parameters from the original client request]: #request-parameters
[parameters from the back-end response]: #response-parameters
