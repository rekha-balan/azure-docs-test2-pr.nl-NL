---
title: Create a function in Azure triggered by a GitHub webhook | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by a GitHub webhook.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: glenga
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: 671c19aec1fd1a742f3ee606e88c45e1750ad303
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865398"
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="720b9-103">Create a function triggered by a GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="720b9-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="720b9-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span><span class="sxs-lookup"><span data-stu-id="720b9-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook triggered function in the Azure portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="720b9-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="720b9-106">Prerequisites</span></span>

+ <span data-ttu-id="720b9-107">A GitHub account with at least one project.</span><span class="sxs-lookup"><span data-stu-id="720b9-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="720b9-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="720b9-108">An Azure subscription.</span></span> <span data-ttu-id="720b9-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="720b9-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="720b9-110">Create an Azure Function app</span><span class="sxs-lookup"><span data-stu-id="720b9-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function app successfully created.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="720b9-112">Next, you create a function in the new function app.</span><span class="sxs-lookup"><span data-stu-id="720b9-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="720b9-113">Create a GitHub webhook triggered function</span><span class="sxs-lookup"><span data-stu-id="720b9-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="720b9-114">Expand your function app and click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="720b9-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="720b9-115">If this is the first function in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="720b9-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="720b9-116">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="720b9-116">This displays the complete set of function templates.</span></span>

    ![Functions quickstart page in the Azure portal](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="720b9-118">In the search field, type `github` and then choose your desired language for the GitHub webhook trigger template.</span><span class="sxs-lookup"><span data-stu-id="720b9-118">In the search field, type `github` and then choose your desired language for the GitHub webhook trigger template.</span></span> 

     ![Choose the GitHub webhook trigger template](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

2. <span data-ttu-id="720b9-120">Type a **Name** for your function, then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="720b9-120">Type a **Name** for your function, then select **Create**.</span></span> 

     ![Configure the GitHub webhook triggered function in the Azure portal](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger-2.png) 

3. <span data-ttu-id="720b9-122">In your new function, click **</> Get function URL**, then copy and save the values.</span><span class="sxs-lookup"><span data-stu-id="720b9-122">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="720b9-123">Do the same thing for **</> Get GitHub secret**.</span><span class="sxs-lookup"><span data-stu-id="720b9-123">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="720b9-124">You use these values to configure the webhook in GitHub.</span><span class="sxs-lookup"><span data-stu-id="720b9-124">You use these values to configure the webhook in GitHub.</span></span>

    ![Review the function code](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="720b9-126">Next, you create a webhook in your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="720b9-126">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="720b9-127">Configure the webhook</span><span class="sxs-lookup"><span data-stu-id="720b9-127">Configure the webhook</span></span>

1. <span data-ttu-id="720b9-128">In GitHub, navigate to a repository that you own.</span><span class="sxs-lookup"><span data-stu-id="720b9-128">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="720b9-129">You can also use any repository that you have forked.</span><span class="sxs-lookup"><span data-stu-id="720b9-129">You can also use any repository that you have forked.</span></span> <span data-ttu-id="720b9-130">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="720b9-130">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

2. <span data-ttu-id="720b9-131">Choose **Settings** > **Options** and make sure that **Issues** is enabled under **Features**.</span><span class="sxs-lookup"><span data-stu-id="720b9-131">Choose **Settings** > **Options** and make sure that **Issues** is enabled under **Features**.</span></span>

   ![Enable Issues](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook.png)

1. <span data-ttu-id="720b9-133">In **Settings**, choose **Webhooks** > **Add webhook**.</span><span class="sxs-lookup"><span data-stu-id="720b9-133">In **Settings**, choose **Webhooks** > **Add webhook**.</span></span>

    ![Add a GitHub webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="720b9-135">Use settings as specified in the following table, then click **Add webhook**:</span><span class="sxs-lookup"><span data-stu-id="720b9-135">Use settings as specified in the following table, then click **Add webhook**:</span></span>

    ![Set the webhook URL and secret](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="720b9-137">Setting</span><span class="sxs-lookup"><span data-stu-id="720b9-137">Setting</span></span> | <span data-ttu-id="720b9-138">Suggested value</span><span class="sxs-lookup"><span data-stu-id="720b9-138">Suggested value</span></span> | <span data-ttu-id="720b9-139">Description</span><span class="sxs-lookup"><span data-stu-id="720b9-139">Description</span></span> |
|---|---|---|
| <span data-ttu-id="720b9-140">**Payload URL**</span><span class="sxs-lookup"><span data-stu-id="720b9-140">**Payload URL**</span></span> | <span data-ttu-id="720b9-141">Copied value</span><span class="sxs-lookup"><span data-stu-id="720b9-141">Copied value</span></span> | <span data-ttu-id="720b9-142">Use the value returned by  **</> Get function URL**.</span><span class="sxs-lookup"><span data-stu-id="720b9-142">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="720b9-143">**Content type**</span><span class="sxs-lookup"><span data-stu-id="720b9-143">**Content type**</span></span> | <span data-ttu-id="720b9-144">application/json</span><span class="sxs-lookup"><span data-stu-id="720b9-144">application/json</span></span> | <span data-ttu-id="720b9-145">The function expects a JSON payload.</span><span class="sxs-lookup"><span data-stu-id="720b9-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="720b9-146">**Secret**</span><span class="sxs-lookup"><span data-stu-id="720b9-146">**Secret**</span></span>   | <span data-ttu-id="720b9-147">Copied value</span><span class="sxs-lookup"><span data-stu-id="720b9-147">Copied value</span></span> | <span data-ttu-id="720b9-148">Use the value returned by  **</> Get GitHub secret**.</span><span class="sxs-lookup"><span data-stu-id="720b9-148">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="720b9-149">Event triggers</span><span class="sxs-lookup"><span data-stu-id="720b9-149">Event triggers</span></span> | <span data-ttu-id="720b9-150">Let me select individual events</span><span class="sxs-lookup"><span data-stu-id="720b9-150">Let me select individual events</span></span> | <span data-ttu-id="720b9-151">We only want to trigger on issue comment events.</span><span class="sxs-lookup"><span data-stu-id="720b9-151">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="720b9-152">Issue comment</span><span class="sxs-lookup"><span data-stu-id="720b9-152">Issue comment</span></span> |  |

<span data-ttu-id="720b9-153">Now, the webhook is configured to trigger your function when a new issue comment is added.</span><span class="sxs-lookup"><span data-stu-id="720b9-153">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="720b9-154">Test the function</span><span class="sxs-lookup"><span data-stu-id="720b9-154">Test the function</span></span>

1. <span data-ttu-id="720b9-155">In your GitHub repository, open the **Issues** tab in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="720b9-155">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="720b9-156">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span><span class="sxs-lookup"><span data-stu-id="720b9-156">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="720b9-157">In the issue, type a comment and click **Comment**.</span><span class="sxs-lookup"><span data-stu-id="720b9-157">In the issue, type a comment and click **Comment**.</span></span>

    ![Add a GitHub issue comment.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="720b9-159">Go back to the portal and view the logs.</span><span class="sxs-lookup"><span data-stu-id="720b9-159">Go back to the portal and view the logs.</span></span> <span data-ttu-id="720b9-160">You should see a trace entry with the new comment text.</span><span class="sxs-lookup"><span data-stu-id="720b9-160">You should see a trace entry with the new comment text.</span></span>

     ![View the comment text in the logs.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="720b9-162">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="720b9-162">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="720b9-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="720b9-163">Next steps</span></span>

<span data-ttu-id="720b9-164">You have created a function that is triggered when a request is received from a GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="720b9-164">You have created a function that is triggered when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="720b9-165">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="720b9-165">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
