---
title: Create a function that integrates with Azure Logic Apps | Microsoft Docs
description: Create a function that integrates with Azure Logic Apps and Azure Cognitive Services to categorize tweet sentiment and send notifications when sentiment is poor.
services: functions, logic-apps, cognitive-services
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
author: ggailey777
manager: jeconnoc
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: azure-functions
ms.topic: tutorial
ms.date: 12/12/2017
ms.author: glenga
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: 23db8d307892b100f291a1f32c9b77c73a60f23e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868516"
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="75f48-104">Create a function that integrates with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="75f48-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="75f48-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="75f48-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="75f48-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span><span class="sxs-lookup"><span data-stu-id="75f48-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="75f48-107">This tutorial shows you how to use Functions with Logic Apps and Microsoft Cognitive Services on Azure to analyze sentiment from Twitter posts.</span><span class="sxs-lookup"><span data-stu-id="75f48-107">This tutorial shows you how to use Functions with Logic Apps and Microsoft Cognitive Services on Azure to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="75f48-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span><span class="sxs-lookup"><span data-stu-id="75f48-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="75f48-109">An email is sent when poor sentiment is detected.</span><span class="sxs-lookup"><span data-stu-id="75f48-109">An email is sent when poor sentiment is detected.</span></span> 

![image first two steps of app in Logic App Designer](media/functions-twitter-email/designer1.png)

<span data-ttu-id="75f48-111">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="75f48-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75f48-112">Create a Cognitive Services API Resource.</span><span class="sxs-lookup"><span data-stu-id="75f48-112">Create a Cognitive Services API Resource.</span></span>
> * <span data-ttu-id="75f48-113">Create a function that categorizes tweet sentiment.</span><span class="sxs-lookup"><span data-stu-id="75f48-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="75f48-114">Create a logic app that connects to Twitter.</span><span class="sxs-lookup"><span data-stu-id="75f48-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="75f48-115">Add sentiment detection to the logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="75f48-116">Connect the logic app to the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="75f48-117">Send an email based on the response from the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75f48-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75f48-118">Prerequisites</span></span>

+ <span data-ttu-id="75f48-119">An active [Twitter](https://twitter.com/) account.</span><span class="sxs-lookup"><span data-stu-id="75f48-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="75f48-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span><span class="sxs-lookup"><span data-stu-id="75f48-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="75f48-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="75f48-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="75f48-122">If you haven't already done so, complete these steps now to create your function app.</span><span class="sxs-lookup"><span data-stu-id="75f48-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-resource"></a><span data-ttu-id="75f48-123">Create a Cognitive Services resource</span><span class="sxs-lookup"><span data-stu-id="75f48-123">Create a Cognitive Services resource</span></span>

<span data-ttu-id="75f48-124">The Cognitive Services APIs are available in Azure as individual resources.</span><span class="sxs-lookup"><span data-stu-id="75f48-124">The Cognitive Services APIs are available in Azure as individual resources.</span></span> <span data-ttu-id="75f48-125">Use the Text Analytics API to detect the sentiment of the tweets being monitored.</span><span class="sxs-lookup"><span data-stu-id="75f48-125">Use the Text Analytics API to detect the sentiment of the tweets being monitored.</span></span>

1. <span data-ttu-id="75f48-126">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75f48-126">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="75f48-127">Click **Create a resource** in the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75f48-127">Click **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="75f48-128">Click **AI + Analytics** > **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="75f48-128">Click **AI + Analytics** > **Text Analytics API**.</span></span> <span data-ttu-id="75f48-129">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="75f48-129">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Create Cognitive resource page](media/functions-twitter-email/cog_svcs_resource.png)

    | <span data-ttu-id="75f48-131">Setting</span><span class="sxs-lookup"><span data-stu-id="75f48-131">Setting</span></span>      |  <span data-ttu-id="75f48-132">Suggested value</span><span class="sxs-lookup"><span data-stu-id="75f48-132">Suggested value</span></span>   | <span data-ttu-id="75f48-133">Description</span><span class="sxs-lookup"><span data-stu-id="75f48-133">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="75f48-134">**Name**</span><span class="sxs-lookup"><span data-stu-id="75f48-134">**Name**</span></span> | <span data-ttu-id="75f48-135">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="75f48-135">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="75f48-136">Choose a unique account name.</span><span class="sxs-lookup"><span data-stu-id="75f48-136">Choose a unique account name.</span></span> |
    | <span data-ttu-id="75f48-137">**Location**</span><span class="sxs-lookup"><span data-stu-id="75f48-137">**Location**</span></span> | <span data-ttu-id="75f48-138">West US</span><span class="sxs-lookup"><span data-stu-id="75f48-138">West US</span></span> | <span data-ttu-id="75f48-139">Use the location nearest you.</span><span class="sxs-lookup"><span data-stu-id="75f48-139">Use the location nearest you.</span></span> |
    | <span data-ttu-id="75f48-140">**Pricing tier**</span><span class="sxs-lookup"><span data-stu-id="75f48-140">**Pricing tier**</span></span> | <span data-ttu-id="75f48-141">F0</span><span class="sxs-lookup"><span data-stu-id="75f48-141">F0</span></span> | <span data-ttu-id="75f48-142">Start with the lowest tier.</span><span class="sxs-lookup"><span data-stu-id="75f48-142">Start with the lowest tier.</span></span> <span data-ttu-id="75f48-143">If you run out of calls, scale to a higher tier.</span><span class="sxs-lookup"><span data-stu-id="75f48-143">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="75f48-144">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="75f48-144">**Resource group**</span></span> | <span data-ttu-id="75f48-145">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75f48-145">myResourceGroup</span></span> | <span data-ttu-id="75f48-146">Use the same resource group for all services in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="75f48-146">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="75f48-147">Click **Create** to create your resource.</span><span class="sxs-lookup"><span data-stu-id="75f48-147">Click **Create** to create your resource.</span></span> <span data-ttu-id="75f48-148">After it is created, select your new Cognitive Services resource pinned to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="75f48-148">After it is created, select your new Cognitive Services resource pinned to the dashboard.</span></span> 

5. <span data-ttu-id="75f48-149">In the left navigation column, click **Keys**, and then copy the value of **Key 1** and save it.</span><span class="sxs-lookup"><span data-stu-id="75f48-149">In the left navigation column, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="75f48-150">You use this key to connect the logic app to your Cognitive Services API.</span><span class="sxs-lookup"><span data-stu-id="75f48-150">You use this key to connect the logic app to your Cognitive Services API.</span></span> 
 
    ![Keys](media/functions-twitter-email/keys.png)

## <a name="create-the-function-app"></a><span data-ttu-id="75f48-152">Create the function app</span><span class="sxs-lookup"><span data-stu-id="75f48-152">Create the function app</span></span>

<span data-ttu-id="75f48-153">Functions provides a great way to offload processing tasks in a logic apps workflow.</span><span class="sxs-lookup"><span data-stu-id="75f48-153">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="75f48-154">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span><span class="sxs-lookup"><span data-stu-id="75f48-154">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

## <a name="create-an-http-triggered-function"></a><span data-ttu-id="75f48-155">Create an HTTP triggered function</span><span class="sxs-lookup"><span data-stu-id="75f48-155">Create an HTTP triggered function</span></span>  

1. <span data-ttu-id="75f48-156">Expand your function app and click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="75f48-156">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="75f48-157">If this is the first function in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="75f48-157">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="75f48-158">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="75f48-158">This displays the complete set of function templates.</span></span>

    ![Functions quickstart page in the Azure portal](media/functions-twitter-email/add-first-function.png)

2. <span data-ttu-id="75f48-160">In the search field, type `http` and then choose **C#** for the HTTP trigger template.</span><span class="sxs-lookup"><span data-stu-id="75f48-160">In the search field, type `http` and then choose **C#** for the HTTP trigger template.</span></span> 

    ![Choose the HTTP trigger](./media/functions-twitter-email/select-http-trigger-portal.png)

3. <span data-ttu-id="75f48-162">Type a **Name** for your function, choose `Function` for **[Authentication level](functions-bindings-http-webhook.md#http-auth)**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75f48-162">Type a **Name** for your function, choose `Function` for **[Authentication level](functions-bindings-http-webhook.md#http-auth)**, and then select **Create**.</span></span> 

    ![Create the HTTP triggered function](./media/functions-twitter-email/select-http-trigger-portal-2.png)

    <span data-ttu-id="75f48-164">This creates a C# script function using the HTTP Trigger template.</span><span class="sxs-lookup"><span data-stu-id="75f48-164">This creates a C# script function using the HTTP Trigger template.</span></span> <span data-ttu-id="75f48-165">Your code appears in a new window as `run.csx`.</span><span class="sxs-lookup"><span data-stu-id="75f48-165">Your code appears in a new window as `run.csx`.</span></span>

4. <span data-ttu-id="75f48-166">Replace the contents of the `run.csx` file with the following code, then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="75f48-166">Replace the contents of the `run.csx` file with the following code, then click **Save**:</span></span>

    ```csharp
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="75f48-167">This function code returns a color category based on the sentiment score received in the request.</span><span class="sxs-lookup"><span data-stu-id="75f48-167">This function code returns a color category based on the sentiment score received in the request.</span></span> 

4. <span data-ttu-id="75f48-168">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="75f48-168">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="75f48-169">A value of **RED** is returned in the body of the response.</span><span class="sxs-lookup"><span data-stu-id="75f48-169">A value of **RED** is returned in the body of the response.</span></span> 

    ![Test the function in the Azure portal](./media/functions-twitter-email/test.png)

<span data-ttu-id="75f48-171">Now you have a function that categorizes sentiment scores.</span><span class="sxs-lookup"><span data-stu-id="75f48-171">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="75f48-172">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services API.</span><span class="sxs-lookup"><span data-stu-id="75f48-172">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services API.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="75f48-173">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="75f48-173">Create a logic app</span></span>   

1. <span data-ttu-id="75f48-174">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75f48-174">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="75f48-175">Click **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="75f48-175">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="75f48-176">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="75f48-176">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="75f48-177">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="75f48-177">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Create logic app in the Azure portal](./media/functions-twitter-email/new_logic_app.png)

    | <span data-ttu-id="75f48-179">Setting</span><span class="sxs-lookup"><span data-stu-id="75f48-179">Setting</span></span>      |  <span data-ttu-id="75f48-180">Suggested value</span><span class="sxs-lookup"><span data-stu-id="75f48-180">Suggested value</span></span>   | <span data-ttu-id="75f48-181">Description</span><span class="sxs-lookup"><span data-stu-id="75f48-181">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="75f48-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="75f48-182">**Name**</span></span> | <span data-ttu-id="75f48-183">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="75f48-183">TweetSentiment</span></span> | <span data-ttu-id="75f48-184">Choose an appropriate name for your app.</span><span class="sxs-lookup"><span data-stu-id="75f48-184">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="75f48-185">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="75f48-185">**Resource group**</span></span> | <span data-ttu-id="75f48-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75f48-186">myResourceGroup</span></span> | <span data-ttu-id="75f48-187">Choose the same existing resource group as before.</span><span class="sxs-lookup"><span data-stu-id="75f48-187">Choose the same existing resource group as before.</span></span> |
    | <span data-ttu-id="75f48-188">**Location**</span><span class="sxs-lookup"><span data-stu-id="75f48-188">**Location**</span></span> | <span data-ttu-id="75f48-189">East US</span><span class="sxs-lookup"><span data-stu-id="75f48-189">East US</span></span> | <span data-ttu-id="75f48-190">Choose a location close to you.</span><span class="sxs-lookup"><span data-stu-id="75f48-190">Choose a location close to you.</span></span> |    

4. <span data-ttu-id="75f48-191">Choose **Pin to dashboard**, and then click **Create** to create your logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-191">Choose **Pin to dashboard**, and then click **Create** to create your logic app.</span></span> 

5. <span data-ttu-id="75f48-192">After the app is created, click your new logic app pinned to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="75f48-192">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="75f48-193">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span><span class="sxs-lookup"><span data-stu-id="75f48-193">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Blank Logic Apps template](media/functions-twitter-email/blank.png)

<span data-ttu-id="75f48-195">You can now use the Logic Apps Designer to add services and triggers to your app.</span><span class="sxs-lookup"><span data-stu-id="75f48-195">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="75f48-196">Connect to Twitter</span><span class="sxs-lookup"><span data-stu-id="75f48-196">Connect to Twitter</span></span>

<span data-ttu-id="75f48-197">First, create a connection to your Twitter account.</span><span class="sxs-lookup"><span data-stu-id="75f48-197">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="75f48-198">The logic app polls for tweets, which trigger the app to run.</span><span class="sxs-lookup"><span data-stu-id="75f48-198">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="75f48-199">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span><span class="sxs-lookup"><span data-stu-id="75f48-199">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="75f48-200">Sign in to your Twitter account and authorize Logic Apps to use your account.</span><span class="sxs-lookup"><span data-stu-id="75f48-200">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="75f48-201">Use the Twitter trigger settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="75f48-201">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Twitter connector settings](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="75f48-203">Setting</span><span class="sxs-lookup"><span data-stu-id="75f48-203">Setting</span></span>      |  <span data-ttu-id="75f48-204">Suggested value</span><span class="sxs-lookup"><span data-stu-id="75f48-204">Suggested value</span></span>   | <span data-ttu-id="75f48-205">Description</span><span class="sxs-lookup"><span data-stu-id="75f48-205">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="75f48-206">**Search text**</span><span class="sxs-lookup"><span data-stu-id="75f48-206">**Search text**</span></span> | <span data-ttu-id="75f48-207">#Azure</span><span class="sxs-lookup"><span data-stu-id="75f48-207">#Azure</span></span> | <span data-ttu-id="75f48-208">Use a hashtag that is popular enough to generate new tweets in the chosen interval.</span><span class="sxs-lookup"><span data-stu-id="75f48-208">Use a hashtag that is popular enough to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="75f48-209">When using the Free tier and your hashtag is too popular, you can quickly use up the transaction quota in your Cognitive Services API.</span><span class="sxs-lookup"><span data-stu-id="75f48-209">When using the Free tier and your hashtag is too popular, you can quickly use up the transaction quota in your Cognitive Services API.</span></span> |
    | <span data-ttu-id="75f48-210">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="75f48-210">**Frequency**</span></span> | <span data-ttu-id="75f48-211">Minute</span><span class="sxs-lookup"><span data-stu-id="75f48-211">Minute</span></span> | <span data-ttu-id="75f48-212">The frequency unit used for polling Twitter.</span><span class="sxs-lookup"><span data-stu-id="75f48-212">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="75f48-213">**Interval**</span><span class="sxs-lookup"><span data-stu-id="75f48-213">**Interval**</span></span> | <span data-ttu-id="75f48-214">15</span><span class="sxs-lookup"><span data-stu-id="75f48-214">15</span></span> | <span data-ttu-id="75f48-215">The time elapsed between Twitter requests, in frequency units.</span><span class="sxs-lookup"><span data-stu-id="75f48-215">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="75f48-216">Click  **Save** to connect to your Twitter account.</span><span class="sxs-lookup"><span data-stu-id="75f48-216">Click  **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="75f48-217">Now your app is connected to Twitter.</span><span class="sxs-lookup"><span data-stu-id="75f48-217">Now your app is connected to Twitter.</span></span> <span data-ttu-id="75f48-218">Next, you connect to text analytics to detect the sentiment of collected tweets.</span><span class="sxs-lookup"><span data-stu-id="75f48-218">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="75f48-219">Add sentiment detection</span><span class="sxs-lookup"><span data-stu-id="75f48-219">Add sentiment detection</span></span>

1. <span data-ttu-id="75f48-220">Click **New Step**, and then **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="75f48-220">Click **New Step**, and then **Add an action**.</span></span>

    ![New Step, and then Add an action](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="75f48-222">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span><span class="sxs-lookup"><span data-stu-id="75f48-222">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Detect Sentiment](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="75f48-224">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services API that you saved, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="75f48-224">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services API that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="75f48-225">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="75f48-225">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detect Sentiment](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="75f48-227">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span><span class="sxs-lookup"><span data-stu-id="75f48-227">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="75f48-228">Connect sentiment output to your function</span><span class="sxs-lookup"><span data-stu-id="75f48-228">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="75f48-229">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="75f48-229">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="75f48-230">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span><span class="sxs-lookup"><span data-stu-id="75f48-230">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure Function box showing Choose an Azure function](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="75f48-232">In **Request Body**, click **Score** and then **Save**.</span><span class="sxs-lookup"><span data-stu-id="75f48-232">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="75f48-234">Now, your function is triggered when a sentiment score is sent from the logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-234">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="75f48-235">A color-coded category is returned to the logic app by the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-235">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="75f48-236">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-236">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="75f48-237">Add email notifications</span><span class="sxs-lookup"><span data-stu-id="75f48-237">Add email notifications</span></span>

<span data-ttu-id="75f48-238">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span><span class="sxs-lookup"><span data-stu-id="75f48-238">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="75f48-239">This topic uses an Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="75f48-239">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="75f48-240">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="75f48-240">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="75f48-241">In the Logic Apps Designer, click **New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="75f48-241">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="75f48-242">Click **Choose a value**, then click **Body**.</span><span class="sxs-lookup"><span data-stu-id="75f48-242">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="75f48-243">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="75f48-243">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Add a condition to the logic app.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="75f48-245">In **IF TRUE**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span><span class="sxs-lookup"><span data-stu-id="75f48-245">In **IF TRUE**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Choose an action for the condition.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="75f48-247">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="75f48-247">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="75f48-248">In the **Send an email** action, use the email settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="75f48-248">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Configure the email for the send an email action.](media/functions-twitter-email/send_email.png)

    | <span data-ttu-id="75f48-250">Setting</span><span class="sxs-lookup"><span data-stu-id="75f48-250">Setting</span></span>      |  <span data-ttu-id="75f48-251">Suggested value</span><span class="sxs-lookup"><span data-stu-id="75f48-251">Suggested value</span></span>   | <span data-ttu-id="75f48-252">Description</span><span class="sxs-lookup"><span data-stu-id="75f48-252">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="75f48-253">**To**</span><span class="sxs-lookup"><span data-stu-id="75f48-253">**To**</span></span> | <span data-ttu-id="75f48-254">Type your email address</span><span class="sxs-lookup"><span data-stu-id="75f48-254">Type your email address</span></span> | <span data-ttu-id="75f48-255">The email address that receives the notification.</span><span class="sxs-lookup"><span data-stu-id="75f48-255">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="75f48-256">**Subject**</span><span class="sxs-lookup"><span data-stu-id="75f48-256">**Subject**</span></span> | <span data-ttu-id="75f48-257">Negative tweet sentiment detected</span><span class="sxs-lookup"><span data-stu-id="75f48-257">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="75f48-258">The subject line of the email notification.</span><span class="sxs-lookup"><span data-stu-id="75f48-258">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="75f48-259">**Body**</span><span class="sxs-lookup"><span data-stu-id="75f48-259">**Body**</span></span> | <span data-ttu-id="75f48-260">Tweet text, Location</span><span class="sxs-lookup"><span data-stu-id="75f48-260">Tweet text, Location</span></span> | <span data-ttu-id="75f48-261">Click the **Tweet text** and **Location** parameters.</span><span class="sxs-lookup"><span data-stu-id="75f48-261">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="75f48-262">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="75f48-262">Click **Save**.</span></span>

<span data-ttu-id="75f48-263">Now that the workflow is complete, you can enable the logic app and see the function at work.</span><span class="sxs-lookup"><span data-stu-id="75f48-263">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="75f48-264">Test the workflow</span><span class="sxs-lookup"><span data-stu-id="75f48-264">Test the workflow</span></span>

1. <span data-ttu-id="75f48-265">In the Logic App Designer, click **Run** to start the app.</span><span class="sxs-lookup"><span data-stu-id="75f48-265">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="75f48-266">In the left column, click **Overview** to see the status of the logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-266">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Logic app execution status](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="75f48-268">(Optional) Click one of the runs to see details of the execution.</span><span class="sxs-lookup"><span data-stu-id="75f48-268">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="75f48-269">Go to your function, view the logs, and verify that sentiment values were received and processed.</span><span class="sxs-lookup"><span data-stu-id="75f48-269">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![View function logs](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="75f48-271">When a potentially negative sentiment is detected, you receive an email.</span><span class="sxs-lookup"><span data-stu-id="75f48-271">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="75f48-272">If you haven't received an email, you can change the function code to return RED every time:</span><span class="sxs-lookup"><span data-stu-id="75f48-272">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="75f48-273">After you have verified email notifications, change back to the original code:</span><span class="sxs-lookup"><span data-stu-id="75f48-273">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="75f48-274">After you have completed this tutorial, you should disable the logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-274">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="75f48-275">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services API.</span><span class="sxs-lookup"><span data-stu-id="75f48-275">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services API.</span></span>

<span data-ttu-id="75f48-276">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span><span class="sxs-lookup"><span data-stu-id="75f48-276">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="75f48-277">Disable the logic app</span><span class="sxs-lookup"><span data-stu-id="75f48-277">Disable the logic app</span></span>

<span data-ttu-id="75f48-278">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="75f48-278">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="75f48-279">This stops the logic app from running and incurring charges without deleting the app.</span><span class="sxs-lookup"><span data-stu-id="75f48-279">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![Function logs](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="75f48-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="75f48-281">Next steps</span></span>

<span data-ttu-id="75f48-282">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="75f48-282">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75f48-283">Create a Cognitive Services API Resource.</span><span class="sxs-lookup"><span data-stu-id="75f48-283">Create a Cognitive Services API Resource.</span></span>
> * <span data-ttu-id="75f48-284">Create a function that categorizes tweet sentiment.</span><span class="sxs-lookup"><span data-stu-id="75f48-284">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="75f48-285">Create a logic app that connects to Twitter.</span><span class="sxs-lookup"><span data-stu-id="75f48-285">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="75f48-286">Add sentiment detection to the logic app.</span><span class="sxs-lookup"><span data-stu-id="75f48-286">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="75f48-287">Connect the logic app to the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-287">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="75f48-288">Send an email based on the response from the function.</span><span class="sxs-lookup"><span data-stu-id="75f48-288">Send an email based on the response from the function.</span></span>

<span data-ttu-id="75f48-289">Advance to the next tutorial to learn how to create a serverless API for your function.</span><span class="sxs-lookup"><span data-stu-id="75f48-289">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="75f48-290">Create a serverless API using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="75f48-290">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="75f48-291">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75f48-291">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span></span>

