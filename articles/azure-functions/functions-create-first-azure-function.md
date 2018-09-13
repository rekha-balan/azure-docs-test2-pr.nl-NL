---
title: Create your first function from the Azure Portal | Microsoft Docs
description: Welcome to Azure. Create your first Azure Function from the Azure portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/10/2017
ms.author: glenga
ms.custom: welcome-email
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: dd97b195b0ae8a0e566c9f6580abd1766202ba54
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563319"
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="b8942-104">Create your first function in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b8942-104">Create your first function in the Azure portal</span></span>

<span data-ttu-id="b8942-105">This topic shows you how to use Azure Functions to create a "hello world" function that is invoked by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b8942-105">This topic shows you how to use Azure Functions to create a "hello world" function that is invoked by an HTTP request.</span></span> <span data-ttu-id="b8942-106">Before you can create a function in the Azure portal, you must create a function app to host the serverless execution of your function.</span><span class="sxs-lookup"><span data-stu-id="b8942-106">Before you can create a function in the Azure portal, you must create a function app to host the serverless execution of your function.</span></span>

<span data-ttu-id="b8942-107">To complete this quickstart, you must have an Azure account.</span><span class="sxs-lookup"><span data-stu-id="b8942-107">To complete this quickstart, you must have an Azure account.</span></span> <span data-ttu-id="b8942-108">[Free accounts](https://azure.microsoft.com/free/) are available.</span><span class="sxs-lookup"><span data-stu-id="b8942-108">[Free accounts](https://azure.microsoft.com/free/) are available.</span></span> <span data-ttu-id="b8942-109">You can also [try Azure Functions](https://azure.microsoft.com/try/app-service/functions/) without having to register with Azure.</span><span class="sxs-lookup"><span data-stu-id="b8942-109">You can also [try Azure Functions](https://azure.microsoft.com/try/app-service/functions/) without having to register with Azure.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b8942-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="b8942-110">Log in to Azure</span></span>

<span data-ttu-id="b8942-111">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b8942-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="b8942-112">Create a function app</span><span class="sxs-lookup"><span data-stu-id="b8942-112">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="b8942-113">For more information, see [Create a function app from the Azure portal](functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8942-113">For more information, see [Create a function app from the Azure portal](functions-create-function-app-portal.md).</span></span>

## <a name="create-a-function"></a><span data-ttu-id="b8942-114">Create a function</span><span class="sxs-lookup"><span data-stu-id="b8942-114">Create a function</span></span>
<span data-ttu-id="b8942-115">These steps create a function in the new function app by using the Azure Functions quickstart.</span><span class="sxs-lookup"><span data-stu-id="b8942-115">These steps create a function in the new function app by using the Azure Functions quickstart.</span></span>

1. <span data-ttu-id="b8942-116">Click the **New** button, then click **WebHook + API**, choose a language for your function, and click **Create a function**.</span><span class="sxs-lookup"><span data-stu-id="b8942-116">Click the **New** button, then click **WebHook + API**, choose a language for your function, and click **Create a function**.</span></span> <span data-ttu-id="b8942-117">A function is created in your chosen language using the HTTP triggered function template.</span><span class="sxs-lookup"><span data-stu-id="b8942-117">A function is created in your chosen language using the HTTP triggered function template.</span></span>  
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="b8942-118">After the function is created, you can test it by sending an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b8942-118">After the function is created, you can test it by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="b8942-119">Test the function</span><span class="sxs-lookup"><span data-stu-id="b8942-119">Test the function</span></span>

<span data-ttu-id="b8942-120">Since the function templates contain working code, you can immediately test your new function right in the portal.</span><span class="sxs-lookup"><span data-stu-id="b8942-120">Since the function templates contain working code, you can immediately test your new function right in the portal.</span></span>

1. <span data-ttu-id="b8942-121">In your function app, click the new function and review the code from the template.</span><span class="sxs-lookup"><span data-stu-id="b8942-121">In your function app, click the new function and review the code from the template.</span></span> <span data-ttu-id="b8942-122">Notice that the function expects an HTTP request with a *name* value passed either in the message body or in a query string.</span><span class="sxs-lookup"><span data-stu-id="b8942-122">Notice that the function expects an HTTP request with a *name* value passed either in the message body or in a query string.</span></span> <span data-ttu-id="b8942-123">When the function runs, this value is returned in the response message.</span><span class="sxs-lookup"><span data-stu-id="b8942-123">When the function runs, this value is returned in the response message.</span></span> <span data-ttu-id="b8942-124">The example shown is a JavaScript function.</span><span class="sxs-lookup"><span data-stu-id="b8942-124">The example shown is a JavaScript function.</span></span>
   
2. <span data-ttu-id="b8942-125">Click **Run** to run the function.</span><span class="sxs-lookup"><span data-stu-id="b8942-125">Click **Run** to run the function.</span></span> <span data-ttu-id="b8942-126">You see that execution is triggered by a test HTTP request, information is written to the logs, and the "hello..." response is displayed in the **Output** in the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="b8942-126">You see that execution is triggered by a test HTTP request, information is written to the logs, and the "hello..." response is displayed in the **Output** in the **Test** tab.</span></span>
 
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

3. <span data-ttu-id="b8942-127">In the **Request body** text box, change the value of the *name* property to your name, and click **Run** again.</span><span class="sxs-lookup"><span data-stu-id="b8942-127">In the **Request body** text box, change the value of the *name* property to your name, and click **Run** again.</span></span> <span data-ttu-id="b8942-128">This time, the response in the **Output** contains your name.</span><span class="sxs-lookup"><span data-stu-id="b8942-128">This time, the response in the **Output** contains your name.</span></span>   

4. <span data-ttu-id="b8942-129">To trigger execution of the same function from an HTTP testing tool or from another browser window, click **</> Get function URL**, copy the request URL and paste it into the tool or browser address bar.</span><span class="sxs-lookup"><span data-stu-id="b8942-129">To trigger execution of the same function from an HTTP testing tool or from another browser window, click **</> Get function URL**, copy the request URL and paste it into the tool or browser address bar.</span></span> <span data-ttu-id="b8942-130">Append the query string value `&name=yourname` to the URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="b8942-130">Append the query string value `&name=yourname` to the URL and execute the request.</span></span> <span data-ttu-id="b8942-131">The same information is written to the logs and the same string is contained in the body of the response message.</span><span class="sxs-lookup"><span data-stu-id="b8942-131">The same information is written to the logs and the same string is contained in the body of the response message.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-first-azure-function/function-app-browser-testing.png)


## <a name="next-steps"></a><span data-ttu-id="b8942-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8942-132">Next steps</span></span>
[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]

[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]




