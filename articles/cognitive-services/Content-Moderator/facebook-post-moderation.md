---
title: Facebook content moderation with Azure Content Moderator | Microsoft Docs
description: Moderate Facebook pages with machine-learning based Content Moderator
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/18/2017
ms.author: sajagtap
ms.openlocfilehash: 66caea65c21bb1f8bb6efa9b50c917599bb71e2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867625"
---
# <a name="facebook-content-moderation-with-content-moderator"></a><span data-ttu-id="0181d-103">Facebook content moderation with Content Moderator</span><span class="sxs-lookup"><span data-stu-id="0181d-103">Facebook content moderation with Content Moderator</span></span>

<span data-ttu-id="0181d-104">In this tutorial, we learn how to use machine-learning-based Content Moderator to help moderate Facebook posts and comments.</span><span class="sxs-lookup"><span data-stu-id="0181d-104">In this tutorial, we learn how to use machine-learning-based Content Moderator to help moderate Facebook posts and comments.</span></span>

<span data-ttu-id="0181d-105">The tutorial guides you through these steps:</span><span class="sxs-lookup"><span data-stu-id="0181d-105">The tutorial guides you through these steps:</span></span>

1. <span data-ttu-id="0181d-106">Create a Content Moderator team.</span><span class="sxs-lookup"><span data-stu-id="0181d-106">Create a Content Moderator team.</span></span>
2. <span data-ttu-id="0181d-107">Create Azure Functions that listen for HTTP events from Content Moderator and Facebook.</span><span class="sxs-lookup"><span data-stu-id="0181d-107">Create Azure Functions that listen for HTTP events from Content Moderator and Facebook.</span></span>
3. <span data-ttu-id="0181d-108">Create a Facebook Page and App, and connect it to Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="0181d-108">Create a Facebook Page and App, and connect it to Content Moderator.</span></span>

<span data-ttu-id="0181d-109">After we are done, Facebook will send the content posted by the visitors to Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="0181d-109">After we are done, Facebook will send the content posted by the visitors to Content Moderator.</span></span> <span data-ttu-id="0181d-110">Based on the match thresholds, your Content Moderator workflows either publish the content or create reviews within the review tool.</span><span class="sxs-lookup"><span data-stu-id="0181d-110">Based on the match thresholds, your Content Moderator workflows either publish the content or create reviews within the review tool.</span></span> 

<span data-ttu-id="0181d-111">The following figure shows the building blocks of the solution.</span><span class="sxs-lookup"><span data-stu-id="0181d-111">The following figure shows the building blocks of the solution.</span></span>

![Facebook post moderation](images/tutorial-facebook-moderation.png)

## <a name="create-a-content-moderator-team"></a><span data-ttu-id="0181d-113">Create a Content Moderator team</span><span class="sxs-lookup"><span data-stu-id="0181d-113">Create a Content Moderator team</span></span>

<span data-ttu-id="0181d-114">Refer to the [Quickstart](quick-start.md) page to sign up for Content Moderator and create a team.</span><span class="sxs-lookup"><span data-stu-id="0181d-114">Refer to the [Quickstart](quick-start.md) page to sign up for Content Moderator and create a team.</span></span>

## <a name="configure-image-moderation-workflow-threshold"></a><span data-ttu-id="0181d-115">Configure image moderation workflow (threshold)</span><span class="sxs-lookup"><span data-stu-id="0181d-115">Configure image moderation workflow (threshold)</span></span>

<span data-ttu-id="0181d-116">Refer to the [Workflows](review-tool-user-guide/workflows.md) page to configure a custom image workflow (threshold).</span><span class="sxs-lookup"><span data-stu-id="0181d-116">Refer to the [Workflows](review-tool-user-guide/workflows.md) page to configure a custom image workflow (threshold).</span></span> <span data-ttu-id="0181d-117">Note the workflow **name**.</span><span class="sxs-lookup"><span data-stu-id="0181d-117">Note the workflow **name**.</span></span>

## <a name="3-configure-text-moderation-workflow-threshold"></a><span data-ttu-id="0181d-118">3. Configure text moderation workflow (threshold)</span><span class="sxs-lookup"><span data-stu-id="0181d-118">3. Configure text moderation workflow (threshold)</span></span>

<span data-ttu-id="0181d-119">Use steps similar to the [Workflows](review-tool-user-guide/workflows.md) page to configure a custom text threshold and workflow.</span><span class="sxs-lookup"><span data-stu-id="0181d-119">Use steps similar to the [Workflows](review-tool-user-guide/workflows.md) page to configure a custom text threshold and workflow.</span></span> <span data-ttu-id="0181d-120">Note the workflow **name**.</span><span class="sxs-lookup"><span data-stu-id="0181d-120">Note the workflow **name**.</span></span>

![Configure Text Workflow](images/text-workflow-configure.PNG)

<span data-ttu-id="0181d-122">Test your workflow by using the "Execute Workflow" button.</span><span class="sxs-lookup"><span data-stu-id="0181d-122">Test your workflow by using the "Execute Workflow" button.</span></span>

![Test Text Workflow](images/text-workflow-test.PNG)

## <a name="create-azure-functions"></a><span data-ttu-id="0181d-124">Create Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0181d-124">Create Azure Functions</span></span>

<span data-ttu-id="0181d-125">Sign in to the [Azure Management Portal](https://portal.azure.com/) to create your Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0181d-125">Sign in to the [Azure Management Portal](https://portal.azure.com/) to create your Azure Functions.</span></span> <span data-ttu-id="0181d-126">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="0181d-126">Follow these steps:</span></span>

1. <span data-ttu-id="0181d-127">Create an Azure Function App as shown on the [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page.</span><span class="sxs-lookup"><span data-stu-id="0181d-127">Create an Azure Function App as shown on the [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page.</span></span>
2. <span data-ttu-id="0181d-128">Open the newly created Function App.</span><span class="sxs-lookup"><span data-stu-id="0181d-128">Open the newly created Function App.</span></span>
3. <span data-ttu-id="0181d-129">Within the App, navigate to **Platform features -> Application Settings**</span><span class="sxs-lookup"><span data-stu-id="0181d-129">Within the App, navigate to **Platform features -> Application Settings**</span></span>
4. <span data-ttu-id="0181d-130">Define the following [application settings](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#settings):</span><span class="sxs-lookup"><span data-stu-id="0181d-130">Define the following [application settings](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#settings):</span></span>

> [!NOTE]
> <span data-ttu-id="0181d-131">The **cm: Region** should be the name of the region (without any spaces).</span><span class="sxs-lookup"><span data-stu-id="0181d-131">The **cm: Region** should be the name of the region (without any spaces).</span></span>
> <span data-ttu-id="0181d-132">For example, **westeurope**, not West Europe, **westcentralus**, not West Central US, and so on.</span><span class="sxs-lookup"><span data-stu-id="0181d-132">For example, **westeurope**, not West Europe, **westcentralus**, not West Central US, and so on.</span></span>
>

| <span data-ttu-id="0181d-133">App Setting</span><span class="sxs-lookup"><span data-stu-id="0181d-133">App Setting</span></span> | <span data-ttu-id="0181d-134">Description</span><span class="sxs-lookup"><span data-stu-id="0181d-134">Description</span></span>   | 
| -------------------- |-------------|
| <span data-ttu-id="0181d-135">cm:TeamId</span><span class="sxs-lookup"><span data-stu-id="0181d-135">cm:TeamId</span></span>   | <span data-ttu-id="0181d-136">Your Content Moderator TeamId</span><span class="sxs-lookup"><span data-stu-id="0181d-136">Your Content Moderator TeamId</span></span>  | 
| <span data-ttu-id="0181d-137">cm:SubscriptionKey</span><span class="sxs-lookup"><span data-stu-id="0181d-137">cm:SubscriptionKey</span></span> | <span data-ttu-id="0181d-138">Your Content Moderator subscription key - See [Credentials](review-tool-user-guide/credentials.md)</span><span class="sxs-lookup"><span data-stu-id="0181d-138">Your Content Moderator subscription key - See [Credentials](review-tool-user-guide/credentials.md)</span></span> | 
| <span data-ttu-id="0181d-139">cm:Region</span><span class="sxs-lookup"><span data-stu-id="0181d-139">cm:Region</span></span> | <span data-ttu-id="0181d-140">Your Content Moderator region name, without the spaces.</span><span class="sxs-lookup"><span data-stu-id="0181d-140">Your Content Moderator region name, without the spaces.</span></span> <span data-ttu-id="0181d-141">See preceding note.</span><span class="sxs-lookup"><span data-stu-id="0181d-141">See preceding note.</span></span> |
| <span data-ttu-id="0181d-142">cm:ImageWorkflow</span><span class="sxs-lookup"><span data-stu-id="0181d-142">cm:ImageWorkflow</span></span> | <span data-ttu-id="0181d-143">Name of the workflow to run on Images</span><span class="sxs-lookup"><span data-stu-id="0181d-143">Name of the workflow to run on Images</span></span> |
| <span data-ttu-id="0181d-144">cm:TextWorkflow</span><span class="sxs-lookup"><span data-stu-id="0181d-144">cm:TextWorkflow</span></span> | <span data-ttu-id="0181d-145">Name of the workflow to run on Text</span><span class="sxs-lookup"><span data-stu-id="0181d-145">Name of the workflow to run on Text</span></span> |
| <span data-ttu-id="0181d-146">cm:CallbackEndpoint</span><span class="sxs-lookup"><span data-stu-id="0181d-146">cm:CallbackEndpoint</span></span> | <span data-ttu-id="0181d-147">Url for the CMListener Function App that you create later in this guide</span><span class="sxs-lookup"><span data-stu-id="0181d-147">Url for the CMListener Function App that you create later in this guide</span></span> |
| <span data-ttu-id="0181d-148">fb:VerificationToken</span><span class="sxs-lookup"><span data-stu-id="0181d-148">fb:VerificationToken</span></span> | <span data-ttu-id="0181d-149">The secret token, also used to subscribe to the Facebook feed events</span><span class="sxs-lookup"><span data-stu-id="0181d-149">The secret token, also used to subscribe to the Facebook feed events</span></span> |
| <span data-ttu-id="0181d-150">fb:PageAccessToken</span><span class="sxs-lookup"><span data-stu-id="0181d-150">fb:PageAccessToken</span></span> | <span data-ttu-id="0181d-151">The Facebook graph api access token does not expire and allows the function Hide/Delete posts on your behalf.</span><span class="sxs-lookup"><span data-stu-id="0181d-151">The Facebook graph api access token does not expire and allows the function Hide/Delete posts on your behalf.</span></span> |

5. <span data-ttu-id="0181d-152">Create a new **HttpTrigger-CSharp** function named **FBListener**.</span><span class="sxs-lookup"><span data-stu-id="0181d-152">Create a new **HttpTrigger-CSharp** function named **FBListener**.</span></span> <span data-ttu-id="0181d-153">This function receives events from Facebook.</span><span class="sxs-lookup"><span data-stu-id="0181d-153">This function receives events from Facebook.</span></span> <span data-ttu-id="0181d-154">Create this function by following these steps:</span><span class="sxs-lookup"><span data-stu-id="0181d-154">Create this function by following these steps:</span></span>

    1. <span data-ttu-id="0181d-155">Keep the [Azure Functions Creation](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page open for reference.</span><span class="sxs-lookup"><span data-stu-id="0181d-155">Keep the [Azure Functions Creation](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page open for reference.</span></span>
    2. <span data-ttu-id="0181d-156">Click the **+** add to create new function.</span><span class="sxs-lookup"><span data-stu-id="0181d-156">Click the **+** add to create new function.</span></span>
    3. <span data-ttu-id="0181d-157">Instead of the built-in templates, choose the **Get started on your own/custom function** option.</span><span class="sxs-lookup"><span data-stu-id="0181d-157">Instead of the built-in templates, choose the **Get started on your own/custom function** option.</span></span>
    4. <span data-ttu-id="0181d-158">Click on the tile that says **HttpTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="0181d-158">Click on the tile that says **HttpTrigger-CSharp**.</span></span>
    5. <span data-ttu-id="0181d-159">Enter the name **FBListener**.</span><span class="sxs-lookup"><span data-stu-id="0181d-159">Enter the name **FBListener**.</span></span> <span data-ttu-id="0181d-160">The **Authorization Level** field should be set to **Function**.</span><span class="sxs-lookup"><span data-stu-id="0181d-160">The **Authorization Level** field should be set to **Function**.</span></span>
    6. <span data-ttu-id="0181d-161">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0181d-161">Click **Create**.</span></span>
    7. <span data-ttu-id="0181d-162">Replace the contents of the **run.csx** with the contents from [**FbListener/run.csx**](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/FbListener/run.csx).</span><span class="sxs-lookup"><span data-stu-id="0181d-162">Replace the contents of the **run.csx** with the contents from [**FbListener/run.csx**](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/FbListener/run.csx).</span></span>

6. <span data-ttu-id="0181d-163">Create a new **HttpTrigger-CSharp** function named **CMListener**.</span><span class="sxs-lookup"><span data-stu-id="0181d-163">Create a new **HttpTrigger-CSharp** function named **CMListener**.</span></span> <span data-ttu-id="0181d-164">This function receives events from Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="0181d-164">This function receives events from Content Moderator.</span></span> <span data-ttu-id="0181d-165">Follow these steps to create this function.</span><span class="sxs-lookup"><span data-stu-id="0181d-165">Follow these steps to create this function.</span></span>

    1. <span data-ttu-id="0181d-166">Keep the [Azure Functions Creation](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page open for reference.</span><span class="sxs-lookup"><span data-stu-id="0181d-166">Keep the [Azure Functions Creation](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) page open for reference.</span></span>
    2. <span data-ttu-id="0181d-167">Click the **+** add to create new function.</span><span class="sxs-lookup"><span data-stu-id="0181d-167">Click the **+** add to create new function.</span></span>
    3. <span data-ttu-id="0181d-168">Instead of the built-in templates, choose the **Get started on your own/custom function** option.</span><span class="sxs-lookup"><span data-stu-id="0181d-168">Instead of the built-in templates, choose the **Get started on your own/custom function** option.</span></span>
    4. <span data-ttu-id="0181d-169">Click on the tile that says **HttpTrigger-CSharp**</span><span class="sxs-lookup"><span data-stu-id="0181d-169">Click on the tile that says **HttpTrigger-CSharp**</span></span>
    5. <span data-ttu-id="0181d-170">Enter the name **CMListener**.</span><span class="sxs-lookup"><span data-stu-id="0181d-170">Enter the name **CMListener**.</span></span> <span data-ttu-id="0181d-171">The **Authorization Level** field should be set to **Function**.</span><span class="sxs-lookup"><span data-stu-id="0181d-171">The **Authorization Level** field should be set to **Function**.</span></span>
    6. <span data-ttu-id="0181d-172">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0181d-172">Click **Create**.</span></span>
    7. <span data-ttu-id="0181d-173">Replace the contents of the **run.csx** with the contents from [**CMListener/run.csx**](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/CmListener/run.csx).</span><span class="sxs-lookup"><span data-stu-id="0181d-173">Replace the contents of the **run.csx** with the contents from [**CMListener/run.csx**](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/CmListener/run.csx).</span></span>

## <a name="configure-the-facebook-page-and-app"></a><span data-ttu-id="0181d-174">Configure the Facebook page and App</span><span class="sxs-lookup"><span data-stu-id="0181d-174">Configure the Facebook page and App</span></span>
1. <span data-ttu-id="0181d-175">Create a Facebook App.</span><span class="sxs-lookup"><span data-stu-id="0181d-175">Create a Facebook App.</span></span>

    1. <span data-ttu-id="0181d-176">Navigate to the [Facebook developer site](https://developers.facebook.com/)</span><span class="sxs-lookup"><span data-stu-id="0181d-176">Navigate to the [Facebook developer site](https://developers.facebook.com/)</span></span>
    2. <span data-ttu-id="0181d-177">Click on **My Apps**.</span><span class="sxs-lookup"><span data-stu-id="0181d-177">Click on **My Apps**.</span></span>
    3. <span data-ttu-id="0181d-178">Add a New App.</span><span class="sxs-lookup"><span data-stu-id="0181d-178">Add a New App.</span></span>
    4. <span data-ttu-id="0181d-179">Select **Webhooks -> Get Started**</span><span class="sxs-lookup"><span data-stu-id="0181d-179">Select **Webhooks -> Get Started**</span></span>
    5. <span data-ttu-id="0181d-180">Select **Page -> Subscribe to this topic**</span><span class="sxs-lookup"><span data-stu-id="0181d-180">Select **Page -> Subscribe to this topic**</span></span>
    6. <span data-ttu-id="0181d-181">Provide the **FBListener Url** as the Callback URL and the **Verify Token** you configured under the **Function App Settings**</span><span class="sxs-lookup"><span data-stu-id="0181d-181">Provide the **FBListener Url** as the Callback URL and the **Verify Token** you configured under the **Function App Settings**</span></span>
    7. <span data-ttu-id="0181d-182">Once subscribed, scroll down to feed and select **subscribe**.</span><span class="sxs-lookup"><span data-stu-id="0181d-182">Once subscribed, scroll down to feed and select **subscribe**.</span></span>

2. <span data-ttu-id="0181d-183">Create a Facebook Page.</span><span class="sxs-lookup"><span data-stu-id="0181d-183">Create a Facebook Page.</span></span>

    1. <span data-ttu-id="0181d-184">Navigate to [Facebook](https://www.facebook.com/bookmarks/pages) and create a **new Facebook Page**.</span><span class="sxs-lookup"><span data-stu-id="0181d-184">Navigate to [Facebook](https://www.facebook.com/bookmarks/pages) and create a **new Facebook Page**.</span></span>
    2. <span data-ttu-id="0181d-185">Allow the Facebook App to access this page by following these steps:</span><span class="sxs-lookup"><span data-stu-id="0181d-185">Allow the Facebook App to access this page by following these steps:</span></span>
        1. <span data-ttu-id="0181d-186">Navigate to the [Graph API Explorer](https://developers.facebook.com/tools/explorer/).</span><span class="sxs-lookup"><span data-stu-id="0181d-186">Navigate to the [Graph API Explorer](https://developers.facebook.com/tools/explorer/).</span></span>
        2. <span data-ttu-id="0181d-187">Select **Application**.</span><span class="sxs-lookup"><span data-stu-id="0181d-187">Select **Application**.</span></span>
        3. <span data-ttu-id="0181d-188">Select **Page Access Token**, Send a **Get** request.</span><span class="sxs-lookup"><span data-stu-id="0181d-188">Select **Page Access Token**, Send a **Get** request.</span></span>
        4. <span data-ttu-id="0181d-189">Click the **Page ID** in the response.</span><span class="sxs-lookup"><span data-stu-id="0181d-189">Click the **Page ID** in the response.</span></span>
        5. <span data-ttu-id="0181d-190">Now append the **/subscribed_apps** to the URL and Send a **Get** (empty response) request.</span><span class="sxs-lookup"><span data-stu-id="0181d-190">Now append the **/subscribed_apps** to the URL and Send a **Get** (empty response) request.</span></span>
        6. <span data-ttu-id="0181d-191">Submit a **Post** request.</span><span class="sxs-lookup"><span data-stu-id="0181d-191">Submit a **Post** request.</span></span> <span data-ttu-id="0181d-192">You get the response as **success: true**.</span><span class="sxs-lookup"><span data-stu-id="0181d-192">You get the response as **success: true**.</span></span>

3. <span data-ttu-id="0181d-193">Create a non-expiring Graph API access token.</span><span class="sxs-lookup"><span data-stu-id="0181d-193">Create a non-expiring Graph API access token.</span></span>

    1. <span data-ttu-id="0181d-194">Navigate to the [Graph API Explorer](https://developers.facebook.com/tools/explorer/).</span><span class="sxs-lookup"><span data-stu-id="0181d-194">Navigate to the [Graph API Explorer](https://developers.facebook.com/tools/explorer/).</span></span>
    2. <span data-ttu-id="0181d-195">Select the **Application** option.</span><span class="sxs-lookup"><span data-stu-id="0181d-195">Select the **Application** option.</span></span>
    3. <span data-ttu-id="0181d-196">Select the **Get User Access Token** option.</span><span class="sxs-lookup"><span data-stu-id="0181d-196">Select the **Get User Access Token** option.</span></span>
    4. <span data-ttu-id="0181d-197">Under the **Select Permissions**, select **manage_pages** and **publish_pages** options.</span><span class="sxs-lookup"><span data-stu-id="0181d-197">Under the **Select Permissions**, select **manage_pages** and **publish_pages** options.</span></span>
    5. <span data-ttu-id="0181d-198">We will use the **access token** (Short Lived Token) in the next step.</span><span class="sxs-lookup"><span data-stu-id="0181d-198">We will use the **access token** (Short Lived Token) in the next step.</span></span>

4. <span data-ttu-id="0181d-199">We use Postman for the next few steps.</span><span class="sxs-lookup"><span data-stu-id="0181d-199">We use Postman for the next few steps.</span></span>

    1. <span data-ttu-id="0181d-200">Open **Postman** (or get it [here](https://www.getpostman.com/)).</span><span class="sxs-lookup"><span data-stu-id="0181d-200">Open **Postman** (or get it [here](https://www.getpostman.com/)).</span></span>
    2. <span data-ttu-id="0181d-201">Import these two files:</span><span class="sxs-lookup"><span data-stu-id="0181d-201">Import these two files:</span></span>
        1. [<span data-ttu-id="0181d-202">Postman Collection</span><span class="sxs-lookup"><span data-stu-id="0181d-202">Postman Collection</span></span>](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/Facebook%20Permanant%20Page%20Access%20Token.postman_collection.json)
        2. [<span data-ttu-id="0181d-203">Postman Environment</span><span class="sxs-lookup"><span data-stu-id="0181d-203">Postman Environment</span></span>](https://github.com/MicrosoftContentModerator/samples-fbPageModeration/blob/master/FB%20Page%20Access%20Token%20Environment.postman_environment.json)       
    3. <span data-ttu-id="0181d-204">Update these environment variables:</span><span class="sxs-lookup"><span data-stu-id="0181d-204">Update these environment variables:</span></span>
    
    | <span data-ttu-id="0181d-205">Key</span><span class="sxs-lookup"><span data-stu-id="0181d-205">Key</span></span> | <span data-ttu-id="0181d-206">Value</span><span class="sxs-lookup"><span data-stu-id="0181d-206">Value</span></span>   | 
    | -------------------- |-------------|
    | <span data-ttu-id="0181d-207">appId</span><span class="sxs-lookup"><span data-stu-id="0181d-207">appId</span></span>   | <span data-ttu-id="0181d-208">Insert your Facebook App Identifier here</span><span class="sxs-lookup"><span data-stu-id="0181d-208">Insert your Facebook App Identifier here</span></span>  | 
    | <span data-ttu-id="0181d-209">appSecret</span><span class="sxs-lookup"><span data-stu-id="0181d-209">appSecret</span></span> | <span data-ttu-id="0181d-210">Insert your Facebook App's secret here</span><span class="sxs-lookup"><span data-stu-id="0181d-210">Insert your Facebook App's secret here</span></span> | 
    | <span data-ttu-id="0181d-211">short_lived_token</span><span class="sxs-lookup"><span data-stu-id="0181d-211">short_lived_token</span></span> | <span data-ttu-id="0181d-212">Insert the short lived user access token you generated in the previous step</span><span class="sxs-lookup"><span data-stu-id="0181d-212">Insert the short lived user access token you generated in the previous step</span></span> |
    4. <span data-ttu-id="0181d-213">Now run the 3 APIs listed in the collection:</span><span class="sxs-lookup"><span data-stu-id="0181d-213">Now run the 3 APIs listed in the collection:</span></span> 
        1. <span data-ttu-id="0181d-214">Select **Generate Long-Lived Access Token** and click **Send**.</span><span class="sxs-lookup"><span data-stu-id="0181d-214">Select **Generate Long-Lived Access Token** and click **Send**.</span></span>
        2. <span data-ttu-id="0181d-215">Select **Get User ID** and click **Send**.</span><span class="sxs-lookup"><span data-stu-id="0181d-215">Select **Get User ID** and click **Send**.</span></span>
        3. <span data-ttu-id="0181d-216">Select **Get Permanent Page Access Token** and click **Send**.</span><span class="sxs-lookup"><span data-stu-id="0181d-216">Select **Get Permanent Page Access Token** and click **Send**.</span></span>
    5. <span data-ttu-id="0181d-217">Copy the **access_token** value from the response and assign it to the App setting, **fb:PageAccessToken**.</span><span class="sxs-lookup"><span data-stu-id="0181d-217">Copy the **access_token** value from the response and assign it to the App setting, **fb:PageAccessToken**.</span></span>

<span data-ttu-id="0181d-218">That's it!</span><span class="sxs-lookup"><span data-stu-id="0181d-218">That's it!</span></span>

<span data-ttu-id="0181d-219">The solution sends all images and text posted on your Facebook page to Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="0181d-219">The solution sends all images and text posted on your Facebook page to Content Moderator.</span></span> <span data-ttu-id="0181d-220">The workflows that you configured earlier are invoked.</span><span class="sxs-lookup"><span data-stu-id="0181d-220">The workflows that you configured earlier are invoked.</span></span> <span data-ttu-id="0181d-221">The content that does not pass your criteria defined in the workflows results in reviews within the review tool.</span><span class="sxs-lookup"><span data-stu-id="0181d-221">The content that does not pass your criteria defined in the workflows results in reviews within the review tool.</span></span> <span data-ttu-id="0181d-222">The rest of the content gets published.</span><span class="sxs-lookup"><span data-stu-id="0181d-222">The rest of the content gets published.</span></span>

## <a name="license"></a><span data-ttu-id="0181d-223">License</span><span class="sxs-lookup"><span data-stu-id="0181d-223">License</span></span>

<span data-ttu-id="0181d-224">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span><span class="sxs-lookup"><span data-stu-id="0181d-224">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span></span> <span data-ttu-id="0181d-225">For more details, see [LICENSE](https://microsoft.mit-license.org/).</span><span class="sxs-lookup"><span data-stu-id="0181d-225">For more details, see [LICENSE](https://microsoft.mit-license.org/).</span></span>

## <a name="developer-code-of-conduct"></a><span data-ttu-id="0181d-226">Developer Code of Conduct</span><span class="sxs-lookup"><span data-stu-id="0181d-226">Developer Code of Conduct</span></span>

<span data-ttu-id="0181d-227">Developers using Cognitive Services, including this client library & sample, are expected to follow the “Developer Code of Conduct for Microsoft Cognitive Services”, found at http://go.microsoft.com/fwlink/?LinkId=698895.</span><span class="sxs-lookup"><span data-stu-id="0181d-227">Developers using Cognitive Services, including this client library & sample, are expected to follow the “Developer Code of Conduct for Microsoft Cognitive Services”, found at http://go.microsoft.com/fwlink/?LinkId=698895.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0181d-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="0181d-228">Next steps</span></span>

1. <span data-ttu-id="0181d-229">[Watch a demo (video)](https://channel9.msdn.com/Events/Build/2017/T6033) of this solution from Microsoft Build 2017.</span><span class="sxs-lookup"><span data-stu-id="0181d-229">[Watch a demo (video)](https://channel9.msdn.com/Events/Build/2017/T6033) of this solution from Microsoft Build 2017.</span></span>
1. [<span data-ttu-id="0181d-230">The Facebook sample on Github</span><span class="sxs-lookup"><span data-stu-id="0181d-230">The Facebook sample on Github</span></span>](https://github.com/MicrosoftContentModerator/samples-fbPageModeration)
1. https://docs.microsoft.com/azure/azure-functions/functions-create-github-webhook-triggered-function
2. http://ukimiawz.github.io/facebook/2015/08/12/webhook-facebook-subscriptions/
3. http://stackoverflow.com/questions/17197970/facebook-permanent-page-access-token
