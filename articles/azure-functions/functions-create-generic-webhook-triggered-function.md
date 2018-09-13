---
title: Create a function in Azure triggered by a generic webhook | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by a webhook in Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: glenga
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: 3ac16c1abd72b62a979e35b3fb86547a53417667
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865001"
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="e0d4e-103">Create a function triggered by a generic webhook</span><span class="sxs-lookup"><span data-stu-id="e0d4e-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="e0d4e-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="e0d4e-105">For example, you can configure a function to be triggered by an alert raised by Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-105">For example, you can configure a function to be triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="e0d4e-106">This topic shows you how to execute C# code when a resource group is added to your subscription.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-106">This topic shows you how to execute C# code when a resource group is added to your subscription.</span></span>   

![Generic webhook triggered function in the Azure portal](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="e0d4e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0d4e-108">Prerequisites</span></span> 

<span data-ttu-id="e0d4e-109">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="e0d4e-109">To complete this tutorial:</span></span>

+ <span data-ttu-id="e0d4e-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="e0d4e-111">Create an Azure Function app</span><span class="sxs-lookup"><span data-stu-id="e0d4e-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="e0d4e-112">Next, you create a function in the new function app.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-112">Next, you create a function in the new function app.</span></span>

## <a name="create-function"></a><span data-ttu-id="e0d4e-113">Create a generic webhook triggered function</span><span class="sxs-lookup"><span data-stu-id="e0d4e-113">Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="e0d4e-114">Expand your function app and click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="e0d4e-115">If this function is the first one in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-115">If this function is the first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="e0d4e-116">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-116">This displays the complete set of function templates.</span></span>

    ![Functions quickstart page in the Azure portal](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="e0d4e-118">In the search field, type `generic` and then choose your desired language for the generic webhook trigger template.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-118">In the search field, type `generic` and then choose your desired language for the generic webhook trigger template.</span></span> <span data-ttu-id="e0d4e-119">This topic uses a C# function.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-119">This topic uses a C# function.</span></span>

     ![Choose the generic webhook trigger template](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png)

2. <span data-ttu-id="e0d4e-121">Type a **Name** for your function, then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-121">Type a **Name** for your function, then select **Create**.</span></span> 

     ![Create a generic webhook triggered function in the Azure portal](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger-2.png) 

2. <span data-ttu-id="e0d4e-123">In your new function, click **</> Get function URL**, then copy and save the value.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-123">In your new function, click **</> Get function URL**, then copy and save the value.</span></span> <span data-ttu-id="e0d4e-124">You use this value to configure the webhook.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-124">You use this value to configure the webhook.</span></span> 

    ![Review the function code](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="e0d4e-126">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-126">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="e0d4e-127">Create an activity log alert</span><span class="sxs-lookup"><span data-stu-id="e0d4e-127">Create an activity log alert</span></span>

1. <span data-ttu-id="e0d4e-128">In the Azure portal, navigate to the **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-128">In the Azure portal, navigate to the **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Monitor](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="e0d4e-130">Use the settings as specified in the table:</span><span class="sxs-lookup"><span data-stu-id="e0d4e-130">Use the settings as specified in the table:</span></span>

    ![Create an activity log alert](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="e0d4e-132">Setting</span><span class="sxs-lookup"><span data-stu-id="e0d4e-132">Setting</span></span>      |  <span data-ttu-id="e0d4e-133">Suggested value</span><span class="sxs-lookup"><span data-stu-id="e0d4e-133">Suggested value</span></span>   | <span data-ttu-id="e0d4e-134">Description</span><span class="sxs-lookup"><span data-stu-id="e0d4e-134">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="e0d4e-135">**Activity log alert name**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-135">**Activity log alert name**</span></span> | <span data-ttu-id="e0d4e-136">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="e0d4e-136">resource-group-create-alert</span></span> | <span data-ttu-id="e0d4e-137">Name of the activity log alert.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-137">Name of the activity log alert.</span></span> |
    | <span data-ttu-id="e0d4e-138">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-138">**Subscription**</span></span> | <span data-ttu-id="e0d4e-139">Your subscription</span><span class="sxs-lookup"><span data-stu-id="e0d4e-139">Your subscription</span></span> | <span data-ttu-id="e0d4e-140">The subscription you are using for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-140">The subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="e0d4e-141">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-141">**Resource Group**</span></span> | <span data-ttu-id="e0d4e-142">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0d4e-142">myResourceGroup</span></span> | <span data-ttu-id="e0d4e-143">The resource group that the alert resources are deployed to.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-143">The resource group that the alert resources are deployed to.</span></span> <span data-ttu-id="e0d4e-144">Using the same resource group as your function app makes it easier to clean up after you complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-144">Using the same resource group as your function app makes it easier to clean up after you complete the tutorial.</span></span> |
    | <span data-ttu-id="e0d4e-145">**Event category**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-145">**Event category**</span></span> | <span data-ttu-id="e0d4e-146">Administrative</span><span class="sxs-lookup"><span data-stu-id="e0d4e-146">Administrative</span></span> | <span data-ttu-id="e0d4e-147">This category includes changes made to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-147">This category includes changes made to Azure resources.</span></span>  |
    | <span data-ttu-id="e0d4e-148">**Resource type**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-148">**Resource type**</span></span> | <span data-ttu-id="e0d4e-149">Resource groups</span><span class="sxs-lookup"><span data-stu-id="e0d4e-149">Resource groups</span></span> | <span data-ttu-id="e0d4e-150">Filters alerts to resource group activities.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-150">Filters alerts to resource group activities.</span></span> |
    | <span data-ttu-id="e0d4e-151">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-151">**Resource Group**</span></span><br/><span data-ttu-id="e0d4e-152">and **Resource**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-152">and **Resource**</span></span> | <span data-ttu-id="e0d4e-153">All</span><span class="sxs-lookup"><span data-stu-id="e0d4e-153">All</span></span> | <span data-ttu-id="e0d4e-154">Monitor all resources.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-154">Monitor all resources.</span></span> |
    | <span data-ttu-id="e0d4e-155">**Operation name**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-155">**Operation name**</span></span> | <span data-ttu-id="e0d4e-156">Create Resource Group</span><span class="sxs-lookup"><span data-stu-id="e0d4e-156">Create Resource Group</span></span> | <span data-ttu-id="e0d4e-157">Filters alerts to create operations.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-157">Filters alerts to create operations.</span></span> |
    | <span data-ttu-id="e0d4e-158">**Level**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-158">**Level**</span></span> | <span data-ttu-id="e0d4e-159">Informational</span><span class="sxs-lookup"><span data-stu-id="e0d4e-159">Informational</span></span> | <span data-ttu-id="e0d4e-160">Include informational level alerts.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-160">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="e0d4e-161">**Status**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-161">**Status**</span></span> | <span data-ttu-id="e0d4e-162">Succeeded</span><span class="sxs-lookup"><span data-stu-id="e0d4e-162">Succeeded</span></span> | <span data-ttu-id="e0d4e-163">Filters alerts to actions that have completed successfully.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-163">Filters alerts to actions that have completed successfully.</span></span> |
    | <span data-ttu-id="e0d4e-164">**Action group**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-164">**Action group**</span></span> | <span data-ttu-id="e0d4e-165">New</span><span class="sxs-lookup"><span data-stu-id="e0d4e-165">New</span></span> | <span data-ttu-id="e0d4e-166">Create a new action group, which defines the action takes when an alert is raised.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-166">Create a new action group, which defines the action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="e0d4e-167">**Action group name**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-167">**Action group name**</span></span> | <span data-ttu-id="e0d4e-168">function-webhook</span><span class="sxs-lookup"><span data-stu-id="e0d4e-168">function-webhook</span></span> | <span data-ttu-id="e0d4e-169">A name to identify the action group.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-169">A name to identify the action group.</span></span>  | 
    | <span data-ttu-id="e0d4e-170">**Short name**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-170">**Short name**</span></span> | <span data-ttu-id="e0d4e-171">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="e0d4e-171">funcwebhook</span></span> | <span data-ttu-id="e0d4e-172">A short name for the action group.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-172">A short name for the action group.</span></span> |  

3. <span data-ttu-id="e0d4e-173">In **Actions**, add an action using the settings as specified in the table:</span><span class="sxs-lookup"><span data-stu-id="e0d4e-173">In **Actions**, add an action using the settings as specified in the table:</span></span> 

    ![Add an action group](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="e0d4e-175">Setting</span><span class="sxs-lookup"><span data-stu-id="e0d4e-175">Setting</span></span>      |  <span data-ttu-id="e0d4e-176">Suggested value</span><span class="sxs-lookup"><span data-stu-id="e0d4e-176">Suggested value</span></span>   | <span data-ttu-id="e0d4e-177">Description</span><span class="sxs-lookup"><span data-stu-id="e0d4e-177">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="e0d4e-178">**Name**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-178">**Name**</span></span> | <span data-ttu-id="e0d4e-179">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="e0d4e-179">CallFunctionWebhook</span></span> | <span data-ttu-id="e0d4e-180">A name for the action.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-180">A name for the action.</span></span> |
    | <span data-ttu-id="e0d4e-181">**Action type**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-181">**Action type**</span></span> | <span data-ttu-id="e0d4e-182">Webhook</span><span class="sxs-lookup"><span data-stu-id="e0d4e-182">Webhook</span></span> | <span data-ttu-id="e0d4e-183">The response to the alert is that a Webhook URL is called.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-183">The response to the alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="e0d4e-184">**Details**</span><span class="sxs-lookup"><span data-stu-id="e0d4e-184">**Details**</span></span> | <span data-ttu-id="e0d4e-185">Function URL</span><span class="sxs-lookup"><span data-stu-id="e0d4e-185">Function URL</span></span> | <span data-ttu-id="e0d4e-186">Paste in the webhook URL of the function that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-186">Paste in the webhook URL of the function that you copied earlier.</span></span> |<span data-ttu-id="e0d4e-187">v</span><span class="sxs-lookup"><span data-stu-id="e0d4e-187">v</span></span>

4. <span data-ttu-id="e0d4e-188">Click **OK** to create the alert and action group.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-188">Click **OK** to create the alert and action group.</span></span>  

<span data-ttu-id="e0d4e-189">The webhook is now called when a resource group is created in your subscription.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-189">The webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="e0d4e-190">Next, you update the code in your function to handle the JSON log data in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-190">Next, you update the code in your function to handle the JSON log data in the body of the request.</span></span>   

## <a name="update-the-function-code"></a><span data-ttu-id="e0d4e-191">Update the function code</span><span class="sxs-lookup"><span data-stu-id="e0d4e-191">Update the function code</span></span>

1. <span data-ttu-id="e0d4e-192">Navigate back to your function app in the portal, and expand your function.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-192">Navigate back to your function app in the portal, and expand your function.</span></span> 

2. <span data-ttu-id="e0d4e-193">Replace the C# script code in the function in the portal with the following code:</span><span class="sxs-lookup"><span data-stu-id="e0d4e-193">Replace the C# script code in the function in the portal with the following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get the activityLog object from the JSON in the message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if the resource in the activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourceGroups", 
            System.StringComparison.OrdinalIgnoreCase))
        {
            log.Error("An error occurred");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about the created resource group to the streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="e0d4e-194">Now you can test the function by creating a new resource group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-194">Now you can test the function by creating a new resource group in your subscription.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="e0d4e-195">Test the function</span><span class="sxs-lookup"><span data-stu-id="e0d4e-195">Test the function</span></span>

1. <span data-ttu-id="e0d4e-196">Click the resource group icon in the left of the Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** to create an empty resource group.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-196">Click the resource group icon in the left of the Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** to create an empty resource group.</span></span>
    
    ![Create a resource group.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="e0d4e-198">Go back to your function and expand the **Logs** window.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-198">Go back to your function and expand the **Logs** window.</span></span> <span data-ttu-id="e0d4e-199">After the resource group is created, the activity log alert triggers the webhook and the function executes.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-199">After the resource group is created, the activity log alert triggers the webhook and the function executes.</span></span> <span data-ttu-id="e0d4e-200">You see the name of the new resource group written to the logs.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-200">You see the name of the new resource group written to the logs.</span></span>  

    ![Add a test application setting.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="e0d4e-202">(Optional) Go back and delete the resource group that you created.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-202">(Optional) Go back and delete the resource group that you created.</span></span> <span data-ttu-id="e0d4e-203">Note that this activity doesn't trigger the function.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-203">Note that this activity doesn't trigger the function.</span></span> <span data-ttu-id="e0d4e-204">This is because delete operations are filtered out by the alert.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-204">This is because delete operations are filtered out by the alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="e0d4e-205">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e0d4e-205">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="e0d4e-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0d4e-206">Next steps</span></span>

<span data-ttu-id="e0d4e-207">You have created a function that runs when a request is received from a generic webhook.</span><span class="sxs-lookup"><span data-stu-id="e0d4e-207">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="e0d4e-208">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="e0d4e-208">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="e0d4e-209">To learn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e0d4e-209">To learn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

