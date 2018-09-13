---
title: Create a serverless API using Azure Functions | Microsoft Docs
description: How to create a serverless API using Azure Functions
services: functions
author: mattchenderson
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 6fc523d1eb053ad70a4eb1c57740e636090371c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865131"
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="0d812-103">Create a serverless API using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0d812-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="0d812-104">In this tutorial, you will learn how Azure Functions allows you to build highly scalable APIs.</span><span class="sxs-lookup"><span data-stu-id="0d812-104">In this tutorial, you will learn how Azure Functions allows you to build highly scalable APIs.</span></span> <span data-ttu-id="0d812-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings, which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span><span class="sxs-lookup"><span data-stu-id="0d812-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings, which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="0d812-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span><span class="sxs-lookup"><span data-stu-id="0d812-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="0d812-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span><span class="sxs-lookup"><span data-stu-id="0d812-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="0d812-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span><span class="sxs-lookup"><span data-stu-id="0d812-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d812-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0d812-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="0d812-110">The resulting function will be used for the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0d812-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="0d812-111">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="0d812-111">Sign in to Azure</span></span>

<span data-ttu-id="0d812-112">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d812-112">Open the Azure portal.</span></span> <span data-ttu-id="0d812-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="0d812-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="0d812-114">Customize your HTTP function</span><span class="sxs-lookup"><span data-stu-id="0d812-114">Customize your HTTP function</span></span>

<span data-ttu-id="0d812-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span><span class="sxs-lookup"><span data-stu-id="0d812-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="0d812-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="0d812-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="0d812-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="0d812-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="0d812-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span><span class="sxs-lookup"><span data-stu-id="0d812-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

1. <span data-ttu-id="0d812-119">Navigate to your function in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d812-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="0d812-120">Select **Integrate** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="0d812-120">Select **Integrate** in the left navigation.</span></span>

    ![Customizing an HTTP function](./media/functions-create-serverless-api/customizing-http.png)

1. <span data-ttu-id="0d812-122">Use the HTTP trigger settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="0d812-122">Use the HTTP trigger settings as specified in the table.</span></span>

    | <span data-ttu-id="0d812-123">Field</span><span class="sxs-lookup"><span data-stu-id="0d812-123">Field</span></span> | <span data-ttu-id="0d812-124">Sample value</span><span class="sxs-lookup"><span data-stu-id="0d812-124">Sample value</span></span> | <span data-ttu-id="0d812-125">Description</span><span class="sxs-lookup"><span data-stu-id="0d812-125">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="0d812-126">Allowed HTTP methods</span><span class="sxs-lookup"><span data-stu-id="0d812-126">Allowed HTTP methods</span></span> | <span data-ttu-id="0d812-127">Selected methods</span><span class="sxs-lookup"><span data-stu-id="0d812-127">Selected methods</span></span> | <span data-ttu-id="0d812-128">Determines what HTTP methods may be used to invoke this function</span><span class="sxs-lookup"><span data-stu-id="0d812-128">Determines what HTTP methods may be used to invoke this function</span></span> |
    | <span data-ttu-id="0d812-129">Selected HTTP methods</span><span class="sxs-lookup"><span data-stu-id="0d812-129">Selected HTTP methods</span></span> | <span data-ttu-id="0d812-130">GET</span><span class="sxs-lookup"><span data-stu-id="0d812-130">GET</span></span> | <span data-ttu-id="0d812-131">Allows only selected HTTP methods to be used to invoke this function</span><span class="sxs-lookup"><span data-stu-id="0d812-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
    | <span data-ttu-id="0d812-132">Route template</span><span class="sxs-lookup"><span data-stu-id="0d812-132">Route template</span></span> | <span data-ttu-id="0d812-133">/hello</span><span class="sxs-lookup"><span data-stu-id="0d812-133">/hello</span></span> | <span data-ttu-id="0d812-134">Determines what route is used to invoke this function</span><span class="sxs-lookup"><span data-stu-id="0d812-134">Determines what route is used to invoke this function</span></span> |
    | <span data-ttu-id="0d812-135">Authorization Level</span><span class="sxs-lookup"><span data-stu-id="0d812-135">Authorization Level</span></span> | <span data-ttu-id="0d812-136">Anonymous</span><span class="sxs-lookup"><span data-stu-id="0d812-136">Anonymous</span></span> | <span data-ttu-id="0d812-137">Optional: Makes your function accessible without an API key</span><span class="sxs-lookup"><span data-stu-id="0d812-137">Optional: Makes your function accessible without an API key</span></span> |

    > [!NOTE] 
    > <span data-ttu-id="0d812-138">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span><span class="sxs-lookup"><span data-stu-id="0d812-138">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

1. <span data-ttu-id="0d812-139">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d812-139">Click **Save**.</span></span>

<span data-ttu-id="0d812-140">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0d812-140">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="0d812-141">Test your API</span><span class="sxs-lookup"><span data-stu-id="0d812-141">Test your API</span></span>

<span data-ttu-id="0d812-142">Next, test your function to see it working with the new API surface.</span><span class="sxs-lookup"><span data-stu-id="0d812-142">Next, test your function to see it working with the new API surface.</span></span>
1. <span data-ttu-id="0d812-143">Navigate back to the development page by clicking on the function's name in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="0d812-143">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>
1. <span data-ttu-id="0d812-144">Click **Get function URL** and copy the URL.</span><span class="sxs-lookup"><span data-stu-id="0d812-144">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="0d812-145">You should see that it uses the `/api/hello` route now.</span><span class="sxs-lookup"><span data-stu-id="0d812-145">You should see that it uses the `/api/hello` route now.</span></span>
1. <span data-ttu-id="0d812-146">Copy the URL into a new browser tab or your preferred REST client.</span><span class="sxs-lookup"><span data-stu-id="0d812-146">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="0d812-147">Browsers will use GET by default.</span><span class="sxs-lookup"><span data-stu-id="0d812-147">Browsers will use GET by default.</span></span>
1. <span data-ttu-id="0d812-148">Add parameters to the query string in your URL e.g. `/api/hello/?name=John`</span><span class="sxs-lookup"><span data-stu-id="0d812-148">Add parameters to the query string in your URL e.g. `/api/hello/?name=John`</span></span>
1. <span data-ttu-id="0d812-149">Hit 'Enter' to confirm that it is working.</span><span class="sxs-lookup"><span data-stu-id="0d812-149">Hit 'Enter' to confirm that it is working.</span></span> <span data-ttu-id="0d812-150">You should see the response "*Hello John*"</span><span class="sxs-lookup"><span data-stu-id="0d812-150">You should see the response "*Hello John*"</span></span>
1. <span data-ttu-id="0d812-151">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span><span class="sxs-lookup"><span data-stu-id="0d812-151">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="0d812-152">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0d812-152">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="0d812-153">Proxies overview</span><span class="sxs-lookup"><span data-stu-id="0d812-153">Proxies overview</span></span>

<span data-ttu-id="0d812-154">In the next section, you will surface your API through a proxy.</span><span class="sxs-lookup"><span data-stu-id="0d812-154">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="0d812-155">Azure Functions Proxies allows you to forward requests to other resources.</span><span class="sxs-lookup"><span data-stu-id="0d812-155">Azure Functions Proxies allows you to forward requests to other resources.</span></span> <span data-ttu-id="0d812-156">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span><span class="sxs-lookup"><span data-stu-id="0d812-156">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="0d812-157">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span><span class="sxs-lookup"><span data-stu-id="0d812-157">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="0d812-158">This is particularly useful if you wish to build your API as microservices.</span><span class="sxs-lookup"><span data-stu-id="0d812-158">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="0d812-159">A proxy can point to any HTTP resource, such as:</span><span class="sxs-lookup"><span data-stu-id="0d812-159">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="0d812-160">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0d812-160">Azure Functions</span></span> 
- <span data-ttu-id="0d812-161">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview)</span><span class="sxs-lookup"><span data-stu-id="0d812-161">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview)</span></span>
- <span data-ttu-id="0d812-162">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro)</span><span class="sxs-lookup"><span data-stu-id="0d812-162">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro)</span></span>
- <span data-ttu-id="0d812-163">Any other hosted API</span><span class="sxs-lookup"><span data-stu-id="0d812-163">Any other hosted API</span></span>

<span data-ttu-id="0d812-164">To learn more about proxies, see [Working with Azure Functions Proxies].</span><span class="sxs-lookup"><span data-stu-id="0d812-164">To learn more about proxies, see [Working with Azure Functions Proxies].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="0d812-165">Create your first proxy</span><span class="sxs-lookup"><span data-stu-id="0d812-165">Create your first proxy</span></span>

<span data-ttu-id="0d812-166">In this section, you will create a new proxy which serves as a frontend to your overall API.</span><span class="sxs-lookup"><span data-stu-id="0d812-166">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="0d812-167">Setting up the frontend environment</span><span class="sxs-lookup"><span data-stu-id="0d812-167">Setting up the frontend environment</span></span>

<span data-ttu-id="0d812-168">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span><span class="sxs-lookup"><span data-stu-id="0d812-168">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="0d812-169">This new app's URL will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span><span class="sxs-lookup"><span data-stu-id="0d812-169">This new app's URL will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

1. <span data-ttu-id="0d812-170">Navigate to your new frontend function app in the portal.</span><span class="sxs-lookup"><span data-stu-id="0d812-170">Navigate to your new frontend function app in the portal.</span></span>
1. <span data-ttu-id="0d812-171">Select **Platform Features** and choose **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="0d812-171">Select **Platform Features** and choose **Application Settings**.</span></span>
1. <span data-ttu-id="0d812-172">Scroll down to **Application settings** where key/value pairs are stored and create a new setting with key "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="0d812-172">Scroll down to **Application settings** where key/value pairs are stored and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="0d812-173">Set its value to the host of your backend function app, such as `<YourBackendApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0d812-173">Set its value to the host of your backend function app, such as `<YourBackendApp>.azurewebsites.net`.</span></span> <span data-ttu-id="0d812-174">This is part of the URL that you copied earlier when testing your HTTP function.</span><span class="sxs-lookup"><span data-stu-id="0d812-174">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="0d812-175">You'll reference this setting in the configuration later.</span><span class="sxs-lookup"><span data-stu-id="0d812-175">You'll reference this setting in the configuration later.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0d812-176">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span><span class="sxs-lookup"><span data-stu-id="0d812-176">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="0d812-177">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span><span class="sxs-lookup"><span data-stu-id="0d812-177">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

1. <span data-ttu-id="0d812-178">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d812-178">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="0d812-179">Creating a proxy on the frontend</span><span class="sxs-lookup"><span data-stu-id="0d812-179">Creating a proxy on the frontend</span></span>

1. <span data-ttu-id="0d812-180">Navigate back to your frontend function app in the portal.</span><span class="sxs-lookup"><span data-stu-id="0d812-180">Navigate back to your frontend function app in the portal.</span></span>
1. <span data-ttu-id="0d812-181">In the left-hand navigation, click the plus sign '+' next to "Proxies".</span><span class="sxs-lookup"><span data-stu-id="0d812-181">In the left-hand navigation, click the plus sign '+' next to "Proxies".</span></span>
    <span data-ttu-id="0d812-182">![Creating a proxy](./media/functions-create-serverless-api/creating-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="0d812-182">![Creating a proxy](./media/functions-create-serverless-api/creating-proxy.png)</span></span>
1. <span data-ttu-id="0d812-183">Use proxy settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="0d812-183">Use proxy settings as specified in the table.</span></span> 

    | <span data-ttu-id="0d812-184">Field</span><span class="sxs-lookup"><span data-stu-id="0d812-184">Field</span></span> | <span data-ttu-id="0d812-185">Sample value</span><span class="sxs-lookup"><span data-stu-id="0d812-185">Sample value</span></span> | <span data-ttu-id="0d812-186">Description</span><span class="sxs-lookup"><span data-stu-id="0d812-186">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="0d812-187">Name</span><span class="sxs-lookup"><span data-stu-id="0d812-187">Name</span></span> | <span data-ttu-id="0d812-188">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="0d812-188">HelloProxy</span></span> | <span data-ttu-id="0d812-189">A friendly name used only for management</span><span class="sxs-lookup"><span data-stu-id="0d812-189">A friendly name used only for management</span></span> |
    | <span data-ttu-id="0d812-190">Route template</span><span class="sxs-lookup"><span data-stu-id="0d812-190">Route template</span></span> | <span data-ttu-id="0d812-191">/api/hello</span><span class="sxs-lookup"><span data-stu-id="0d812-191">/api/hello</span></span> | <span data-ttu-id="0d812-192">Determines what route is used to invoke this proxy</span><span class="sxs-lookup"><span data-stu-id="0d812-192">Determines what route is used to invoke this proxy</span></span> |
    | <span data-ttu-id="0d812-193">Backend URL</span><span class="sxs-lookup"><span data-stu-id="0d812-193">Backend URL</span></span> | https://%HELLO_HOST%/api/hello | <span data-ttu-id="0d812-194">Specifies the endpoint to which the request should be proxied</span><span class="sxs-lookup"><span data-stu-id="0d812-194">Specifies the endpoint to which the request should be proxied</span></span> |
    
1. <span data-ttu-id="0d812-195">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span><span class="sxs-lookup"><span data-stu-id="0d812-195">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>
1. <span data-ttu-id="0d812-196">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span><span class="sxs-lookup"><span data-stu-id="0d812-196">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="0d812-197">The resolved URL will point to your original function.</span><span class="sxs-lookup"><span data-stu-id="0d812-197">The resolved URL will point to your original function.</span></span>
1. <span data-ttu-id="0d812-198">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d812-198">Click **Create**.</span></span>
1. <span data-ttu-id="0d812-199">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span><span class="sxs-lookup"><span data-stu-id="0d812-199">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>
    1. <span data-ttu-id="0d812-200">For an anonymous function use:</span><span class="sxs-lookup"><span data-stu-id="0d812-200">For an anonymous function use:</span></span>
        1. `https://YOURPROXYAPP.azurewebsites.net/api/hello?name="Proxies"`
    1. <span data-ttu-id="0d812-201">For a function with authorization use:</span><span class="sxs-lookup"><span data-stu-id="0d812-201">For a function with authorization use:</span></span>
        1. `https://YOURPROXYAPP.azurewebsites.net/api/hello?code=YOURCODE&name="Proxies"`

## <a name="create-a-mock-api"></a><span data-ttu-id="0d812-202">Create a mock API</span><span class="sxs-lookup"><span data-stu-id="0d812-202">Create a mock API</span></span>

<span data-ttu-id="0d812-203">Next, you will use a proxy to create a mock API for your solution.</span><span class="sxs-lookup"><span data-stu-id="0d812-203">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="0d812-204">This allows client development to progress, without needing the backend fully implemented.</span><span class="sxs-lookup"><span data-stu-id="0d812-204">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="0d812-205">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span><span class="sxs-lookup"><span data-stu-id="0d812-205">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="0d812-206">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="0d812-206">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="0d812-207">To get started, navigate to your function app in the portal.</span><span class="sxs-lookup"><span data-stu-id="0d812-207">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="0d812-208">Select **Platform features** and under **Development Tools** find **App Service Editor**.</span><span class="sxs-lookup"><span data-stu-id="0d812-208">Select **Platform features** and under **Development Tools** find **App Service Editor**.</span></span> <span data-ttu-id="0d812-209">Clicking this will open the App Service Editor in a new tab.</span><span class="sxs-lookup"><span data-stu-id="0d812-209">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="0d812-210">Select `proxies.json` in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="0d812-210">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="0d812-211">This is the file which stores the configuration for all of your proxies.</span><span class="sxs-lookup"><span data-stu-id="0d812-211">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="0d812-212">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span><span class="sxs-lookup"><span data-stu-id="0d812-212">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="0d812-213">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="0d812-213">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="0d812-214">If you've followed along so far, your proxies.json should look like the following:</span><span class="sxs-lookup"><span data-stu-id="0d812-214">If you've followed along so far, your proxies.json should look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="0d812-215">Next you'll add your mock API.</span><span class="sxs-lookup"><span data-stu-id="0d812-215">Next you'll add your mock API.</span></span> <span data-ttu-id="0d812-216">Replace your proxies.json file with the following:</span><span class="sxs-lookup"><span data-stu-id="0d812-216">Replace your proxies.json file with the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="0d812-217">This adds a new proxy, "GetUserByName", without the backendUri property.</span><span class="sxs-lookup"><span data-stu-id="0d812-217">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="0d812-218">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span><span class="sxs-lookup"><span data-stu-id="0d812-218">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="0d812-219">Request and response overrides can also be used in conjunction with a backend URL.</span><span class="sxs-lookup"><span data-stu-id="0d812-219">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="0d812-220">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="0d812-220">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="0d812-221">Test your mock API by calling the `<YourProxyApp>.azurewebsites.net/api/users/{username}` endpoint using a browser or your favorite REST client.</span><span class="sxs-lookup"><span data-stu-id="0d812-221">Test your mock API by calling the `<YourProxyApp>.azurewebsites.net/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="0d812-222">Be sure to replace _{username}_ with a string value representing a username.</span><span class="sxs-lookup"><span data-stu-id="0d812-222">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d812-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d812-223">Next steps</span></span>

<span data-ttu-id="0d812-224">In this tutorial, you learned how to build and customize an API on Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0d812-224">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="0d812-225">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span><span class="sxs-lookup"><span data-stu-id="0d812-225">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="0d812-226">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0d812-226">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="0d812-227">The following references may be helpful as you develop your API further:</span><span class="sxs-lookup"><span data-stu-id="0d812-227">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="0d812-228">Azure Functions HTTP and webhook bindings</span><span class="sxs-lookup"><span data-stu-id="0d812-228">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="0d812-229">[Working with Azure Functions Proxies]</span><span class="sxs-lookup"><span data-stu-id="0d812-229">[Working with Azure Functions Proxies]</span></span>
- [<span data-ttu-id="0d812-230">Documenting an Azure Functions API (preview)</span><span class="sxs-lookup"><span data-stu-id="0d812-230">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Working with Azure Functions Proxies]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
