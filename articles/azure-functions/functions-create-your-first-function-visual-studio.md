---
title: Create your first function in Azure using Visual Studio | Microsoft Docs
description: Create and publish an HTTP triggered Azure Function using Visual Studio.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, compute, serverless architecture
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 05/22/2018
ms.author: glenga
ms.custom: mvc, devcenter, , vs-azure, 23113853-34f2-4f
ms.openlocfilehash: 582e949c6fdf4333690264dfd5b1cf04234efdd4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865822"
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="3b56e-104">Create your first function using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3b56e-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="3b56e-105">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span><span class="sxs-lookup"><span data-stu-id="3b56e-105">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="3b56e-106">In this article, you learn how to use the Visual Studio 2017 tools for Azure Functions to locally create and test a "hello world" function.</span><span class="sxs-lookup"><span data-stu-id="3b56e-106">In this article, you learn how to use the Visual Studio 2017 tools for Azure Functions to locally create and test a "hello world" function.</span></span> <span data-ttu-id="3b56e-107">You then publish the function code to Azure.</span><span class="sxs-lookup"><span data-stu-id="3b56e-107">You then publish the function code to Azure.</span></span> <span data-ttu-id="3b56e-108">These tools are available as part of the Azure development workload in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3b56e-108">These tools are available as part of the Azure development workload in Visual Studio 2017.</span></span>

<span data-ttu-id="3b56e-109">This topic includes [a video](#watch-the-video) that demonstrates the same basic steps.</span><span class="sxs-lookup"><span data-stu-id="3b56e-109">This topic includes [a video](#watch-the-video) that demonstrates the same basic steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b56e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b56e-110">Prerequisites</span></span>

<span data-ttu-id="3b56e-111">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="3b56e-111">To complete this tutorial:</span></span>

* <span data-ttu-id="3b56e-112">Install [Visual Studio 2017](https://azure.microsoft.com/downloads/) and ensure that the **Azure development** workload is also installed.</span><span class="sxs-lookup"><span data-stu-id="3b56e-112">Install [Visual Studio 2017](https://azure.microsoft.com/downloads/) and ensure that the **Azure development** workload is also installed.</span></span>

* <span data-ttu-id="3b56e-113">Make sure you have the [latest Azure Functions tools](functions-develop-vs.md#check-your-tools-version).</span><span class="sxs-lookup"><span data-stu-id="3b56e-113">Make sure you have the [latest Azure Functions tools](functions-develop-vs.md#check-your-tools-version).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-function-app-project"></a><span data-ttu-id="3b56e-114">Create a function app project</span><span class="sxs-lookup"><span data-stu-id="3b56e-114">Create a function app project</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="3b56e-115">Visual Studio creates a project and in it a class that contains boilerplate code for the chosen function type.</span><span class="sxs-lookup"><span data-stu-id="3b56e-115">Visual Studio creates a project and in it a class that contains boilerplate code for the chosen function type.</span></span> <span data-ttu-id="3b56e-116">The **FunctionName** attribute on the method sets the name of the function.</span><span class="sxs-lookup"><span data-stu-id="3b56e-116">The **FunctionName** attribute on the method sets the name of the function.</span></span> <span data-ttu-id="3b56e-117">The **HttpTrigger** attribute specifies that the function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="3b56e-117">The **HttpTrigger** attribute specifies that the function is triggered by an HTTP request.</span></span> <span data-ttu-id="3b56e-118">The boilerplate code sends an HTTP response that includes a value from the request body or query string.</span><span class="sxs-lookup"><span data-stu-id="3b56e-118">The boilerplate code sends an HTTP response that includes a value from the request body or query string.</span></span> <span data-ttu-id="3b56e-119">You can add input and output bindings to a function by applying the appropriate attributes to the method.</span><span class="sxs-lookup"><span data-stu-id="3b56e-119">You can add input and output bindings to a function by applying the appropriate attributes to the method.</span></span> <span data-ttu-id="3b56e-120">For more information, see the [Triggers and bindings](functions-dotnet-class-library.md#triggers-and-bindings) section of the [Azure Functions C# developer reference](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="3b56e-120">For more information, see the [Triggers and bindings](functions-dotnet-class-library.md#triggers-and-bindings) section of the [Azure Functions C# developer reference](functions-dotnet-class-library.md).</span></span>

<span data-ttu-id="3b56e-121">Now that you've created your function project and an HTTP-triggered function, you can test it on your local computer.</span><span class="sxs-lookup"><span data-stu-id="3b56e-121">Now that you've created your function project and an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="3b56e-122">Test the function locally</span><span class="sxs-lookup"><span data-stu-id="3b56e-122">Test the function locally</span></span>

<span data-ttu-id="3b56e-123">Azure Functions Core Tools lets you run an Azure Functions project on your local development computer.</span><span class="sxs-lookup"><span data-stu-id="3b56e-123">Azure Functions Core Tools lets you run an Azure Functions project on your local development computer.</span></span> <span data-ttu-id="3b56e-124">You are prompted to install these tools the first time you start a function from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b56e-124">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>

1. <span data-ttu-id="3b56e-125">To test your function, press F5.</span><span class="sxs-lookup"><span data-stu-id="3b56e-125">To test your function, press F5.</span></span> <span data-ttu-id="3b56e-126">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span><span class="sxs-lookup"><span data-stu-id="3b56e-126">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span> <span data-ttu-id="3b56e-127">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="3b56e-127">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="3b56e-128">Copy the URL of your function from the Azure Functions runtime output.</span><span class="sxs-lookup"><span data-stu-id="3b56e-128">Copy the URL of your function from the Azure Functions runtime output.</span></span>

    ![Azure local runtime](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="3b56e-130">Paste the URL for the HTTP request into your browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="3b56e-130">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="3b56e-131">Append the query string `?name=<yourname>` to this URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="3b56e-131">Append the query string `?name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="3b56e-132">The following shows the response in the browser to the local GET request returned by the function:</span><span class="sxs-lookup"><span data-stu-id="3b56e-132">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![Function localhost response in the browser](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="3b56e-134">To stop debugging, press Shift + F5.</span><span class="sxs-lookup"><span data-stu-id="3b56e-134">To stop debugging, press Shift + F5.</span></span>

<span data-ttu-id="3b56e-135">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span><span class="sxs-lookup"><span data-stu-id="3b56e-135">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="3b56e-136">Publish the project to Azure</span><span class="sxs-lookup"><span data-stu-id="3b56e-136">Publish the project to Azure</span></span>

<span data-ttu-id="3b56e-137">You must have a function app in your Azure subscription before you can publish your project.</span><span class="sxs-lookup"><span data-stu-id="3b56e-137">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="3b56e-138">You can create a function app right from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b56e-138">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="3b56e-139">Test your function in Azure</span><span class="sxs-lookup"><span data-stu-id="3b56e-139">Test your function in Azure</span></span>

1. <span data-ttu-id="3b56e-140">Copy the base URL of the function app from the Publish profile page.</span><span class="sxs-lookup"><span data-stu-id="3b56e-140">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="3b56e-141">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span><span class="sxs-lookup"><span data-stu-id="3b56e-141">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="3b56e-142">As before, make sure to append the query string `?name=<yourname>` to this URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="3b56e-142">As before, make sure to append the query string `?name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="3b56e-143">The URL that calls your HTTP triggered function should be in the following format:</span><span class="sxs-lookup"><span data-stu-id="3b56e-143">The URL that calls your HTTP triggered function should be in the following format:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="3b56e-144">Paste this new URL for the HTTP request into your browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="3b56e-144">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="3b56e-145">The following shows the response in the browser to the remote GET request returned by the function:</span><span class="sxs-lookup"><span data-stu-id="3b56e-145">The following shows the response in the browser to the remote GET request returned by the function:</span></span>

    ![Function response in the browser](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)

## <a name="watch-the-video"></a><span data-ttu-id="3b56e-147">Watch the video</span><span class="sxs-lookup"><span data-stu-id="3b56e-147">Watch the video</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/DrhG-Rdm80k]

## <a name="next-steps"></a><span data-ttu-id="3b56e-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b56e-148">Next steps</span></span>

<span data-ttu-id="3b56e-149">You have used Visual Studio to create and publish a C# function app with a simple HTTP triggered function.</span><span class="sxs-lookup"><span data-stu-id="3b56e-149">You have used Visual Studio to create and publish a C# function app with a simple HTTP triggered function.</span></span>

* [<span data-ttu-id="3b56e-150">Learn how to add input and output bindings that integrate with other services.</span><span class="sxs-lookup"><span data-stu-id="3b56e-150">Learn how to add input and output bindings that integrate with other services.</span></span>](functions-develop-vs.md#add-bindings)
* <span data-ttu-id="3b56e-151">[Learn more about developing functions as .NET class libraries](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="3b56e-151">[Learn more about developing functions as .NET class libraries](functions-dotnet-class-library.md).</span></span>
