---
title: Create a web hook or API Azure Function | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by a WebHook or API call.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: glenga
ms.openlocfilehash: b0aa38e9164f1ebd9f1c3c0f6326c9b51d0044af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564553"
---
# <a name="create-a-webhook-or-api-azure-function"></a><span data-ttu-id="b5e1d-103">Create a webhook or API Azure Function</span><span class="sxs-lookup"><span data-stu-id="b5e1d-103">Create a webhook or API Azure Function</span></span>
<span data-ttu-id="b5e1d-104">Azure Functions is an event-driven, compute-on-demand experience that enables you to create scheduled or triggered units of code implemented in various programming languages.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-104">Azure Functions is an event-driven, compute-on-demand experience that enables you to create scheduled or triggered units of code implemented in various programming languages.</span></span> <span data-ttu-id="b5e1d-105">To learn more about Azure Functions, see the [Azure Functions Overview](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5e1d-105">To learn more about Azure Functions, see the [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="b5e1d-106">This topic shows you how to create a JavaScript function that is invoked by a GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-106">This topic shows you how to create a JavaScript function that is invoked by a GitHub webhook.</span></span> <span data-ttu-id="b5e1d-107">The new function is created based on a pre-defined template in the Azure Functions portal.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-107">The new function is created based on a pre-defined template in the Azure Functions portal.</span></span> <span data-ttu-id="b5e1d-108">You can also watch a short video to see how these steps are performed in the portal.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-108">You can also watch a short video to see how these steps are performed in the portal.</span></span>

<span data-ttu-id="b5e1d-109">The general steps in this tutorial can also be used to create a function in C# or F# instead of JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-109">The general steps in this tutorial can also be used to create a function in C# or F# instead of JavaScript.</span></span> 

## <a name="watch-the-video"></a><span data-ttu-id="b5e1d-110">Watch the video</span><span class="sxs-lookup"><span data-stu-id="b5e1d-110">Watch the video</span></span>
<span data-ttu-id="b5e1d-111">The following video shows how to perform the basic steps in this tutorial</span><span class="sxs-lookup"><span data-stu-id="b5e1d-111">The following video shows how to perform the basic steps in this tutorial</span></span> 

>[!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-a-Web-Hook-or-API-Azure-Function/player]
>
>

## <a name="prerequisites"></a><span data-ttu-id="b5e1d-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b5e1d-112">Prerequisites</span></span>

<span data-ttu-id="b5e1d-113">To complete this tutorial, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="b5e1d-113">To complete this tutorial, you will need the following:</span></span>

+ <span data-ttu-id="b5e1d-114">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-114">An active Azure account.</span></span> <span data-ttu-id="b5e1d-115">If you don't already have an account, you can [sign up for a free Azure acccount](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b5e1d-115">If you don't already have an account, you can [sign up for a free Azure acccount](https://azure.microsoft.com/free/).</span></span>  
 <span data-ttu-id="b5e1d-116">You can also use the [Try Functions](https://functions.azure.com/try) experience to complete this tutorial without an Azure account.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-116">You can also use the [Try Functions](https://functions.azure.com/try) experience to complete this tutorial without an Azure account.</span></span>
+ <span data-ttu-id="b5e1d-117">A GitHub account.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-117">A GitHub account.</span></span> <span data-ttu-id="b5e1d-118">You can [sign up for a free GitHub account](https://github.com/join), if you don't already have one.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-118">You can [sign up for a free GitHub account](https://github.com/join), if you don't already have one.</span></span> 

## <a name="create-a-webhook-triggered-function-from-the-template"></a><span data-ttu-id="b5e1d-119">Create a webhook-triggered function from the template</span><span class="sxs-lookup"><span data-stu-id="b5e1d-119">Create a webhook-triggered function from the template</span></span>
<span data-ttu-id="b5e1d-120">A function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-120">A function app hosts the execution of your functions in Azure.</span></span> 

1. <span data-ttu-id="b5e1d-121">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-121">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span></span>

2. <span data-ttu-id="b5e1d-122">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-122">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span></span> <span data-ttu-id="b5e1d-123">To create a function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-123">To create a function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span></span> 

3. <span data-ttu-id="b5e1d-124">In your function app, click **+ New Function** > **GitHub Webhook - JavaScript** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-124">In your function app, click **+ New Function** > **GitHub Webhook - JavaScript** > **Create**.</span></span> <span data-ttu-id="b5e1d-125">This step creates a function with a default name that is based on the specified template.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-125">This step creates a function with a default name that is based on the specified template.</span></span> <span data-ttu-id="b5e1d-126">You can alternately create a C# or F# function.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-126">You can alternately create a C# or F# function.</span></span>
   
    ![Create a GitHub webhook triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-a-web-hook-or-api-function/functions-create-new-github-webhook.png) 

4. <span data-ttu-id="b5e1d-128">In **Develop**, note the sample express.js function in the **Code** window.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-128">In **Develop**, note the sample express.js function in the **Code** window.</span></span> <span data-ttu-id="b5e1d-129">This function receives a GitHub request from an issue comment webhook, logs the issue text and sends a response to the webhook as `New GitHub comment: <Your issue comment text>`.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-129">This function receives a GitHub request from an issue comment webhook, logs the issue text and sends a response to the webhook as `New GitHub comment: <Your issue comment text>`.</span></span>

    ![Review the function code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-a-web-hook-or-api-function/functions-new-webhook-in-portal.png) 

1. <span data-ttu-id="b5e1d-131">Copy and save the **Function URL** and **GitHub Secret** values.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-131">Copy and save the **Function URL** and **GitHub Secret** values.</span></span> <span data-ttu-id="b5e1d-132">You will use these values in the next section to configure the webhook in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-132">You will use these values in the next section to configure the webhook in GitHub.</span></span> 

2. <span data-ttu-id="b5e1d-133">Click **Test**, note the predefined JSON body of an issue comment in the **Request body**, then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-133">Click **Test**, note the predefined JSON body of an issue comment in the **Request body**, then click **Run**.</span></span> 

    ![Test webhook function in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-a-web-hook-or-api-function/functions-test-webhook-in-portal.png)
   
    > [!NOTE]
    > <span data-ttu-id="b5e1d-135">You can always test a new template-based function right in the **Develop** tab by supplying any expected body JSON data and clicking the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-135">You can always test a new template-based function right in the **Develop** tab by supplying any expected body JSON data and clicking the **Run** button.</span></span> <span data-ttu-id="b5e1d-136">In this case, the template has a predefined body for an issue comment.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-136">In this case, the template has a predefined body for an issue comment.</span></span> 

<span data-ttu-id="b5e1d-137">Next, you will create the actual webhook in your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-137">Next, you will create the actual webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="b5e1d-138">Configure the webhook</span><span class="sxs-lookup"><span data-stu-id="b5e1d-138">Configure the webhook</span></span>
1. <span data-ttu-id="b5e1d-139">In GitHub, navigate to a repository that you own.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-139">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="b5e1d-140">You can also use any repositories that you have forked.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-140">You can also use any repositories that you have forked.</span></span>
 
2. <span data-ttu-id="b5e1d-141">Click **Settings** > **Webhooks & services** > **Add webhook**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-141">Click **Settings** > **Webhooks & services** > **Add webhook**.</span></span>
   
    ![Add a GitHub webhook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-a-web-hook-or-api-function/functions-create-new-github-webhook-2.png)   

3. <span data-ttu-id="b5e1d-143">Paste your function's URL and secret into **Payload URL** and **Secret** and select **application/json** for **Content type**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-143">Paste your function's URL and secret into **Payload URL** and **Secret** and select **application/json** for **Content type**.</span></span>

4. <span data-ttu-id="b5e1d-144">Click **Let me select individual events**, select **Issue comment**, and click **Add webhook**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-144">Click **Let me select individual events**, select **Issue comment**, and click **Add webhook**.</span></span>
   
    ![Set the webhook URL and secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-a-web-hook-or-api-function/functions-create-new-github-webhook-3.png) 

<span data-ttu-id="b5e1d-146">At this point, the GitHub webhook is configured to trigger your function when a new issue comment is added.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-146">At this point, the GitHub webhook is configured to trigger your function when a new issue comment is added.</span></span>  
<span data-ttu-id="b5e1d-147">Now, it's time to test it out.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-147">Now, it's time to test it out.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="b5e1d-148">Test the function</span><span class="sxs-lookup"><span data-stu-id="b5e1d-148">Test the function</span></span>
1. <span data-ttu-id="b5e1d-149">In your GitHub repo, open the **Issues** tab in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-149">In your GitHub repo, open the **Issues** tab in a new browser window.</span></span>

2. <span data-ttu-id="b5e1d-150">In the new window, click **New Issue**, type a title then click **Submit new issue**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-150">In the new window, click **New Issue**, type a title then click **Submit new issue**.</span></span> <span data-ttu-id="b5e1d-151">You can also open an existing issue.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-151">You can also open an existing issue.</span></span>

2. <span data-ttu-id="b5e1d-152">In the issue, type a comment and click **Comment**.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-152">In the issue, type a comment and click **Comment**.</span></span> 

3. <span data-ttu-id="b5e1d-153">In the other GitHub window, click **Edit** next to your new webhook, scroll down to **Recent Deliveries**, and verify that a webhook request was sent and that the body of response is `New GitHub comment: <Your issue comment text>`.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-153">In the other GitHub window, click **Edit** next to your new webhook, scroll down to **Recent Deliveries**, and verify that a webhook request was sent and that the body of response is `New GitHub comment: <Your issue comment text>`.</span></span>

3. <span data-ttu-id="b5e1d-154">Back in the Functions portal, scroll down to the logs and see that the function has been triggered and the value `New GitHub comment: <Your issue comment text>` is written to the streaming logs.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-154">Back in the Functions portal, scroll down to the logs and see that the function has been triggered and the value `New GitHub comment: <Your issue comment text>` is written to the streaming logs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5e1d-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5e1d-155">Next steps</span></span>
<span data-ttu-id="b5e1d-156">See these topics for more information about Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-156">See these topics for more information about Azure Functions.</span></span>

* [<span data-ttu-id="b5e1d-157">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="b5e1d-157">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="b5e1d-158">Programmer reference for coding functions.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-158">Programmer reference for coding functions.</span></span>
* [<span data-ttu-id="b5e1d-159">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5e1d-159">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="b5e1d-160">Describes various tools and techniques for testing your functions.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-160">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="b5e1d-161">How to scale Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5e1d-161">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="b5e1d-162">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span><span class="sxs-lookup"><span data-stu-id="b5e1d-162">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span>  

[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]






