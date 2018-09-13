---
title: Create your first function from the Azure Portal | Microsoft Docs
description: Learn how to create your first Azure Function for serverless execution using the Azure portal.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: glenga
ms.custom: mvc, devcenter, cc996988-fb4f-47
ms.openlocfilehash: d208a4b72a27eb288d46ee591f42a8f6b71c4f70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821488"
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="ea37d-103">Create your first function in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ea37d-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="ea37d-104">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span><span class="sxs-lookup"><span data-stu-id="ea37d-104">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="ea37d-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ea37d-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Create function app in the Azure portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

> [!NOTE]
> <span data-ttu-id="ea37d-107">C# developers should consider [creating your first function in Visual Studio 2017](functions-create-your-first-function-visual-studio.md) instead of in the portal.</span><span class="sxs-lookup"><span data-stu-id="ea37d-107">C# developers should consider [creating your first function in Visual Studio 2017](functions-create-your-first-function-visual-studio.md) instead of in the portal.</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="ea37d-108">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="ea37d-108">Log in to Azure</span></span>

<span data-ttu-id="ea37d-109">Sign in to the Azure portal at <http://portal.azure.com> with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="ea37d-109">Sign in to the Azure portal at <http://portal.azure.com> with your Azure account.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="ea37d-110">Create a function app</span><span class="sxs-lookup"><span data-stu-id="ea37d-110">Create a function app</span></span>

<span data-ttu-id="ea37d-111">You must have a function app to host the execution of your functions.</span><span class="sxs-lookup"><span data-stu-id="ea37d-111">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="ea37d-112">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="ea37d-112">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="ea37d-113">Next, you create a function in the new function app.</span><span class="sxs-lookup"><span data-stu-id="ea37d-113">Next, you create a function in the new function app.</span></span>

## <a name="create-function"></a><span data-ttu-id="ea37d-114">Create an HTTP triggered function</span><span class="sxs-lookup"><span data-stu-id="ea37d-114">Create an HTTP triggered function</span></span>

1. <span data-ttu-id="ea37d-115">Expand your new function app, then click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="ea37d-115">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="ea37d-116">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span><span class="sxs-lookup"><span data-stu-id="ea37d-116">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Functions quickstart in the Azure portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="ea37d-118">A function is created in your chosen language using the template for an HTTP triggered function.</span><span class="sxs-lookup"><span data-stu-id="ea37d-118">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="ea37d-119">This topic shows a C# script function in the portal, but you can create a function in any [supported language](supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="ea37d-119">This topic shows a C# script function in the portal, but you can create a function in any [supported language](supported-languages.md).</span></span> 

<span data-ttu-id="ea37d-120">Now, you can run the new function by sending an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="ea37d-120">Now, you can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="ea37d-121">Test the function</span><span class="sxs-lookup"><span data-stu-id="ea37d-121">Test the function</span></span>

1. <span data-ttu-id="ea37d-122">In your new function, click **</> Get function URL** at the top right, select **default (Function key)**, and then click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="ea37d-122">In your new function, click **</> Get function URL** at the top right, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copy the function URL from the Azure portal](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="ea37d-124">Paste the function URL into your browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="ea37d-124">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="ea37d-125">Add the query string value `&name=<yourname>` to the end of this URL and press the `Enter` key on your keyboard to execute the request.</span><span class="sxs-lookup"><span data-stu-id="ea37d-125">Add the query string value `&name=<yourname>` to the end of this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="ea37d-126">You should see the response returned by the function displayed in the browser.</span><span class="sxs-lookup"><span data-stu-id="ea37d-126">You should see the response returned by the function displayed in the browser.</span></span>  

    <span data-ttu-id="ea37d-127">The following example shows the response in the Edge browser (other browsers may include displayed XML):</span><span class="sxs-lookup"><span data-stu-id="ea37d-127">The following example shows the response in the Edge browser (other browsers may include displayed XML):</span></span>

    ![Function response in the browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="ea37d-129">The request URL includes a key that is required, by default, to access your function over HTTP.</span><span class="sxs-lookup"><span data-stu-id="ea37d-129">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="ea37d-130">When your function runs, trace information is written to the logs.</span><span class="sxs-lookup"><span data-stu-id="ea37d-130">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="ea37d-131">To see the trace output from the previous execution, return to your function in the portal and click the arrow at the bottom of the screen to expand the **Logs**.</span><span class="sxs-lookup"><span data-stu-id="ea37d-131">To see the trace output from the previous execution, return to your function in the portal and click the arrow at the bottom of the screen to expand the **Logs**.</span></span> 

   ![Functions log viewer in the Azure portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ea37d-133">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ea37d-133">Clean up resources</span></span>

[!INCLUDE [Clean-up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="ea37d-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea37d-134">Next steps</span></span>

<span data-ttu-id="ea37d-135">You have created a function app with a simple HTTP triggered function.</span><span class="sxs-lookup"><span data-stu-id="ea37d-135">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="ea37d-136">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="ea37d-136">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



