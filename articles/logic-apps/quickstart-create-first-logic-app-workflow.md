---
title: Create and automate your first workflow - Azure Logic Apps | Microsoft Docs
description: Quickstart for how to create your first logic app that automates tasks, processes, and workflows with Azure Logic Apps. Create logic apps for system integration and enterprise application integration (EAI) solutions for your systems & cloud services
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: quickstart
ms.custom: mvc
ms.date: 07/20/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 0f38aabf008f0335a6f9e21717aa38aefdd21615
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966104"
---
# <a name="quickstart-create-your-first-automated-workflow-with-azure-logic-apps---azure-portal"></a><span data-ttu-id="cb4e3-104">Quickstart: Create your first automated workflow with Azure Logic Apps - Azure portal</span><span class="sxs-lookup"><span data-stu-id="cb4e3-104">Quickstart: Create your first automated workflow with Azure Logic Apps - Azure portal</span></span>

<span data-ttu-id="cb4e3-105">This quickstart introduces how to build your first automated workflow with [Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb4e3-105">This quickstart introduces how to build your first automated workflow with [Azure Logic Apps](../logic-apps/logic-apps-overview.md).</span></span> <span data-ttu-id="cb4e3-106">In this article, you create a logic app that regularly checks a website's RSS feed for new items.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-106">In this article, you create a logic app that regularly checks a website's RSS feed for new items.</span></span> <span data-ttu-id="cb4e3-107">If new items exist, the logic app sends an email for each item.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-107">If new items exist, the logic app sends an email for each item.</span></span> <span data-ttu-id="cb4e3-108">When you're done, your logic app looks like this workflow at a high level:</span><span class="sxs-lookup"><span data-stu-id="cb4e3-108">When you're done, your logic app looks like this workflow at a high level:</span></span>

![Overview - logic app example](./media/quickstart-create-first-logic-app-workflow/overview.png)

<span data-ttu-id="cb4e3-110">To follow this quickstart, you need an email account from a provider that's supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-110">To follow this quickstart, you need an email account from a provider that's supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span></span> <span data-ttu-id="cb4e3-111">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span><span class="sxs-lookup"><span data-stu-id="cb4e3-111">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span></span> <span data-ttu-id="cb4e3-112">This logic app uses an Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-112">This logic app uses an Office 365 Outlook account.</span></span> <span data-ttu-id="cb4e3-113">If you use another email account, the overall steps are the same, but your UI might slightly differ.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-113">If you use another email account, the overall steps are the same, but your UI might slightly differ.</span></span> 

<span data-ttu-id="cb4e3-114">Also, if you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-114">Also, if you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="cb4e3-115">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cb4e3-115">Sign in to the Azure portal</span></span>

<span data-ttu-id="cb4e3-116">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-116">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span></span>

## <a name="create-your-logic-app"></a><span data-ttu-id="cb4e3-117">Create your logic app</span><span class="sxs-lookup"><span data-stu-id="cb4e3-117">Create your logic app</span></span> 

1. <span data-ttu-id="cb4e3-118">From the main Azure menu, choose **Create a resource** > **Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-118">From the main Azure menu, choose **Create a resource** > **Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/quickstart-create-first-logic-app-workflow/create-logic-app.png)

3. <span data-ttu-id="cb4e3-120">Under **Create logic app**, provide details about your logic app as shown here.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-120">Under **Create logic app**, provide details about your logic app as shown here.</span></span> <span data-ttu-id="cb4e3-121">After you're done, choose **Pin to dashboard** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-121">After you're done, choose **Pin to dashboard** > **Create**.</span></span>

   ![Provide logic app details](./media/quickstart-create-first-logic-app-workflow/create-logic-app-settings.png)

   | <span data-ttu-id="cb4e3-123">Property</span><span class="sxs-lookup"><span data-stu-id="cb4e3-123">Property</span></span> | <span data-ttu-id="cb4e3-124">Value</span><span class="sxs-lookup"><span data-stu-id="cb4e3-124">Value</span></span> | <span data-ttu-id="cb4e3-125">Description</span><span class="sxs-lookup"><span data-stu-id="cb4e3-125">Description</span></span> | 
   |----------|-------|-------------| 
   | <span data-ttu-id="cb4e3-126">**Name**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-126">**Name**</span></span> | <span data-ttu-id="cb4e3-127">MyFirstLogicApp</span><span class="sxs-lookup"><span data-stu-id="cb4e3-127">MyFirstLogicApp</span></span> | <span data-ttu-id="cb4e3-128">The name for your logic app</span><span class="sxs-lookup"><span data-stu-id="cb4e3-128">The name for your logic app</span></span> | 
   | <span data-ttu-id="cb4e3-129">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-129">**Subscription**</span></span> | <span data-ttu-id="cb4e3-130"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="cb4e3-130"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="cb4e3-131">The name for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cb4e3-131">The name for your Azure subscription</span></span> | 
   | <span data-ttu-id="cb4e3-132">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-132">**Resource group**</span></span> | <span data-ttu-id="cb4e3-133">My-First-LA-RG</span><span class="sxs-lookup"><span data-stu-id="cb4e3-133">My-First-LA-RG</span></span> | <span data-ttu-id="cb4e3-134">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span><span class="sxs-lookup"><span data-stu-id="cb4e3-134">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span></span> | 
   | <span data-ttu-id="cb4e3-135">**Location**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-135">**Location**</span></span> | <span data-ttu-id="cb4e3-136">West US</span><span class="sxs-lookup"><span data-stu-id="cb4e3-136">West US</span></span> | <span data-ttu-id="cb4e3-137">The region where to store your logic app information</span><span class="sxs-lookup"><span data-stu-id="cb4e3-137">The region where to store your logic app information</span></span> | 
   | <span data-ttu-id="cb4e3-138">**Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-138">**Log Analytics**</span></span> | <span data-ttu-id="cb4e3-139">Off</span><span class="sxs-lookup"><span data-stu-id="cb4e3-139">Off</span></span> | <span data-ttu-id="cb4e3-140">Keep the **Off** setting for diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-140">Keep the **Off** setting for diagnostic logging.</span></span> | 
   |||| 

3. <span data-ttu-id="cb4e3-141">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and commonly used triggers.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-141">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and commonly used triggers.</span></span> <span data-ttu-id="cb4e3-142">Under **Templates**, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-142">Under **Templates**, choose **Blank Logic App**.</span></span>

   ![Choose blank logic app template](./media/quickstart-create-first-logic-app-workflow/choose-logic-app-template.png)

<span data-ttu-id="cb4e3-144">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that fires when a new RSS feed item appears.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-144">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that fires when a new RSS feed item appears.</span></span> <span data-ttu-id="cb4e3-145">Every logic app must start with a trigger, which fires when a specific event happens or when a specific condition is met.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-145">Every logic app must start with a trigger, which fires when a specific event happens or when a specific condition is met.</span></span> <span data-ttu-id="cb4e3-146">Each time the trigger fires, the Logic Apps engine creates a logic app instance that starts and runs your workflow.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-146">Each time the trigger fires, the Logic Apps engine creates a logic app instance that starts and runs your workflow.</span></span>

<a name="add-rss-trigger"></a>

## <a name="check-rss-feed-with-a-trigger"></a><span data-ttu-id="cb4e3-147">Check RSS feed with a trigger</span><span class="sxs-lookup"><span data-stu-id="cb4e3-147">Check RSS feed with a trigger</span></span>

1. <span data-ttu-id="cb4e3-148">On the designer, enter "rss" in the search box.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-148">On the designer, enter "rss" in the search box.</span></span> <span data-ttu-id="cb4e3-149">Select this trigger: **RSS - When a feed item is published**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-149">Select this trigger: **RSS - When a feed item is published**</span></span>

   ![Select trigger: "RSS - When a feed item is published"](./media/quickstart-create-first-logic-app-workflow/add-trigger-rss.png)

2. <span data-ttu-id="cb4e3-151">Provide this information for your trigger as shown and described:</span><span class="sxs-lookup"><span data-stu-id="cb4e3-151">Provide this information for your trigger as shown and described:</span></span> 

   ![Set up trigger with RSS feed, frequency, and interval](./media/quickstart-create-first-logic-app-workflow/add-trigger-rss-settings.png)

   | <span data-ttu-id="cb4e3-153">Property</span><span class="sxs-lookup"><span data-stu-id="cb4e3-153">Property</span></span> | <span data-ttu-id="cb4e3-154">Value</span><span class="sxs-lookup"><span data-stu-id="cb4e3-154">Value</span></span> | <span data-ttu-id="cb4e3-155">Description</span><span class="sxs-lookup"><span data-stu-id="cb4e3-155">Description</span></span> | 
   |----------|-------|-------------| 
   | <span data-ttu-id="cb4e3-156">**The RSS feed URL**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-156">**The RSS feed URL**</span></span> | ```http://feeds.reuters.com/reuters/topNews``` | <span data-ttu-id="cb4e3-157">The link for the RSS feed that you want to monitor</span><span class="sxs-lookup"><span data-stu-id="cb4e3-157">The link for the RSS feed that you want to monitor</span></span> | 
   | <span data-ttu-id="cb4e3-158">**Interval**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-158">**Interval**</span></span> | <span data-ttu-id="cb4e3-159">1</span><span class="sxs-lookup"><span data-stu-id="cb4e3-159">1</span></span> | <span data-ttu-id="cb4e3-160">The number of intervals to wait between checks</span><span class="sxs-lookup"><span data-stu-id="cb4e3-160">The number of intervals to wait between checks</span></span> | 
   | <span data-ttu-id="cb4e3-161">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-161">**Frequency**</span></span> | <span data-ttu-id="cb4e3-162">Minute</span><span class="sxs-lookup"><span data-stu-id="cb4e3-162">Minute</span></span> | <span data-ttu-id="cb4e3-163">The unit of time for each interval between checks</span><span class="sxs-lookup"><span data-stu-id="cb4e3-163">The unit of time for each interval between checks</span></span>  | 
   |||| 

   <span data-ttu-id="cb4e3-164">Together, the interval and frequency define the schedule for your logic app's trigger.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-164">Together, the interval and frequency define the schedule for your logic app's trigger.</span></span> 
   <span data-ttu-id="cb4e3-165">This logic app checks the feed every minute.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-165">This logic app checks the feed every minute.</span></span>

3. <span data-ttu-id="cb4e3-166">To hide the trigger details for now, click inside the trigger's title bar.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-166">To hide the trigger details for now, click inside the trigger's title bar.</span></span>

   ![Collapse shape to hide details](./media/quickstart-create-first-logic-app-workflow/collapse-trigger-shape.png)

4. <span data-ttu-id="cb4e3-168">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-168">Save your logic app.</span></span> <span data-ttu-id="cb4e3-169">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-169">On the designer toolbar, choose **Save**.</span></span> 

<span data-ttu-id="cb4e3-170">Your logic app is now live but doesn't do anything other than check the RSS feed.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-170">Your logic app is now live but doesn't do anything other than check the RSS feed.</span></span> <span data-ttu-id="cb4e3-171">So, add an action that responds when the trigger fires.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-171">So, add an action that responds when the trigger fires.</span></span>

## <a name="send-email-with-an-action"></a><span data-ttu-id="cb4e3-172">Send email with an action</span><span class="sxs-lookup"><span data-stu-id="cb4e3-172">Send email with an action</span></span>

<span data-ttu-id="cb4e3-173">Now add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that sends email when a new item appears in the RSS feed.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-173">Now add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that sends email when a new item appears in the RSS feed.</span></span> 

1. <span data-ttu-id="cb4e3-174">Under the **When a feed item is published** trigger, choose **+ New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-174">Under the **When a feed item is published** trigger, choose **+ New step** > **Add an action**.</span></span>

   ![Add an action](./media/quickstart-create-first-logic-app-workflow/add-new-action.png)

2. <span data-ttu-id="cb4e3-176">Under **Choose an action**, enter "send an email" as your filter.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-176">Under **Choose an action**, enter "send an email" as your filter.</span></span> <span data-ttu-id="cb4e3-177">From the actions list, select the "send an email" action for the email provider that you want.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-177">From the actions list, select the "send an email" action for the email provider that you want.</span></span> 

   ![Select this action: "Office 365 Outlook - Send an email"](./media/quickstart-create-first-logic-app-workflow/add-action-send-email.png)

   <span data-ttu-id="cb4e3-179">To filter the actions list to a specific app or service, you can select that app or service first:</span><span class="sxs-lookup"><span data-stu-id="cb4e3-179">To filter the actions list to a specific app or service, you can select that app or service first:</span></span>

   * <span data-ttu-id="cb4e3-180">For Azure work or school accounts, select Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-180">For Azure work or school accounts, select Office 365 Outlook.</span></span> 
   * <span data-ttu-id="cb4e3-181">For personal Microsoft accounts, select Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-181">For personal Microsoft accounts, select Outlook.com.</span></span>

3. <span data-ttu-id="cb4e3-182">If asked for credentials, sign in to your email account so that Logic Apps creates a connection to your email account.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-182">If asked for credentials, sign in to your email account so that Logic Apps creates a connection to your email account.</span></span>

4. <span data-ttu-id="cb4e3-183">In the **Send an email** action, specify the data that you want the email to include.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-183">In the **Send an email** action, specify the data that you want the email to include.</span></span> 

   1. <span data-ttu-id="cb4e3-184">In the **To** box, enter the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-184">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="cb4e3-185">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-185">For testing purposes, you can use your own email address.</span></span>

      <span data-ttu-id="cb4e3-186">For now, ignore the **Add dynamic content** list that appears.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-186">For now, ignore the **Add dynamic content** list that appears.</span></span> 
      <span data-ttu-id="cb4e3-187">When you click inside some edit boxes, this list appears and shows any available parameters from the previous step that you can include as inputs in your workflow.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-187">When you click inside some edit boxes, this list appears and shows any available parameters from the previous step that you can include as inputs in your workflow.</span></span> 

   2. <span data-ttu-id="cb4e3-188">In the **Subject** box, enter this text with a trailing blank space: ```New RSS item: ```</span><span class="sxs-lookup"><span data-stu-id="cb4e3-188">In the **Subject** box, enter this text with a trailing blank space: ```New RSS item: ```</span></span>

      ![Enter the email subject](./media/quickstart-create-first-logic-app-workflow/add-action-send-email-subject.png)
 
   3. <span data-ttu-id="cb4e3-190">From the **Add dynamic content** list, select **Feed title** to include the RSS item title.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-190">From the **Add dynamic content** list, select **Feed title** to include the RSS item title.</span></span>

      ![Dynamic content list - "Feed title"](./media/quickstart-create-first-logic-app-workflow/add-action-send-email-subject-dynamic-content.png)

      <span data-ttu-id="cb4e3-192">When you're done, the email subject looks like this example:</span><span class="sxs-lookup"><span data-stu-id="cb4e3-192">When you're done, the email subject looks like this example:</span></span>

      ![Added feed title](./media/quickstart-create-first-logic-app-workflow/add-action-send-email-feed-title.png)

      <span data-ttu-id="cb4e3-194">If a "For each" loop appears on the designer, then you selected a token for an array, for example, the **categories-Item** token.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-194">If a "For each" loop appears on the designer, then you selected a token for an array, for example, the **categories-Item** token.</span></span> 
      <span data-ttu-id="cb4e3-195">For these kinds of tokens, the designer automatically adds this loop around the action that references that token.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-195">For these kinds of tokens, the designer automatically adds this loop around the action that references that token.</span></span> 
      <span data-ttu-id="cb4e3-196">That way, your logic app performs the same action on each array item.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-196">That way, your logic app performs the same action on each array item.</span></span> 
      <span data-ttu-id="cb4e3-197">To remove the loop, choose the **ellipses** (**...**) on the loop's title bar, then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-197">To remove the loop, choose the **ellipses** (**...**) on the loop's title bar, then choose **Delete**.</span></span>

   4. <span data-ttu-id="cb4e3-198">In the **Body** box, enter this text, and select these tokens for the email body.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-198">In the **Body** box, enter this text, and select these tokens for the email body.</span></span> 
   <span data-ttu-id="cb4e3-199">To add blank lines in an edit box, press Shift + Enter.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-199">To add blank lines in an edit box, press Shift + Enter.</span></span> 

      ![Add contents for email body](./media/quickstart-create-first-logic-app-workflow/add-action-send-email-body.png)

      | <span data-ttu-id="cb4e3-201">Property</span><span class="sxs-lookup"><span data-stu-id="cb4e3-201">Property</span></span> | <span data-ttu-id="cb4e3-202">Description</span><span class="sxs-lookup"><span data-stu-id="cb4e3-202">Description</span></span> | 
      |----------|-------------| 
      | <span data-ttu-id="cb4e3-203">**Feed title**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-203">**Feed title**</span></span> | <span data-ttu-id="cb4e3-204">The item's title</span><span class="sxs-lookup"><span data-stu-id="cb4e3-204">The item's title</span></span> | 
      | <span data-ttu-id="cb4e3-205">**Feed published on**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-205">**Feed published on**</span></span> | <span data-ttu-id="cb4e3-206">The item's publishing date and time</span><span class="sxs-lookup"><span data-stu-id="cb4e3-206">The item's publishing date and time</span></span> | 
      | <span data-ttu-id="cb4e3-207">**Primary feed link**</span><span class="sxs-lookup"><span data-stu-id="cb4e3-207">**Primary feed link**</span></span> | <span data-ttu-id="cb4e3-208">The URL for the item</span><span class="sxs-lookup"><span data-stu-id="cb4e3-208">The URL for the item</span></span> | 
      ||| 
   
5. <span data-ttu-id="cb4e3-209">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-209">Save your logic app.</span></span>

<span data-ttu-id="cb4e3-210">Next, test your logic app.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-210">Next, test your logic app.</span></span>

## <a name="run-your-logic-app"></a><span data-ttu-id="cb4e3-211">Run your logic app</span><span class="sxs-lookup"><span data-stu-id="cb4e3-211">Run your logic app</span></span>

<span data-ttu-id="cb4e3-212">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-212">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span></span> <span data-ttu-id="cb4e3-213">Or, wait for your logic app to check the RSS feed based on your specified schedule (every minute).</span><span class="sxs-lookup"><span data-stu-id="cb4e3-213">Or, wait for your logic app to check the RSS feed based on your specified schedule (every minute).</span></span> <span data-ttu-id="cb4e3-214">If the RSS feed has new items, your logic app sends an email for each new item.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-214">If the RSS feed has new items, your logic app sends an email for each new item.</span></span> <span data-ttu-id="cb4e3-215">Otherwise, your logic app waits until the next interval before checking again.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-215">Otherwise, your logic app waits until the next interval before checking again.</span></span> 

<span data-ttu-id="cb4e3-216">For example, here is a sample email that this logic app sends.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-216">For example, here is a sample email that this logic app sends.</span></span> <span data-ttu-id="cb4e3-217">If you don't get any emails, check your junk email folder.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-217">If you don't get any emails, check your junk email folder.</span></span>

![Email sent for new RSS feed item](./media/quickstart-create-first-logic-app-workflow/monitor-rss-feed-email.png)

<span data-ttu-id="cb4e3-219">Technically, when the trigger checks the RSS feed and finds new items, the trigger fires, and the Logic Apps engine creates an instance of your logic app workflow that runs the actions in the workflow.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-219">Technically, when the trigger checks the RSS feed and finds new items, the trigger fires, and the Logic Apps engine creates an instance of your logic app workflow that runs the actions in the workflow.</span></span>
<span data-ttu-id="cb4e3-220">If the trigger doesn't find new items, the trigger doesn't fire and "skips" instantiating the workflow.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-220">If the trigger doesn't find new items, the trigger doesn't fire and "skips" instantiating the workflow.</span></span>

<span data-ttu-id="cb4e3-221">Congratulations, you've now successfully built and run your first logic app with the Azure portal!</span><span class="sxs-lookup"><span data-stu-id="cb4e3-221">Congratulations, you've now successfully built and run your first logic app with the Azure portal!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="cb4e3-222">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cb4e3-222">Clean up resources</span></span>

<span data-ttu-id="cb4e3-223">When you no longer need this sample, delete the resource group that contains your logic app and related resources.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-223">When you no longer need this sample, delete the resource group that contains your logic app and related resources.</span></span> 

1. <span data-ttu-id="cb4e3-224">On the main Azure menu, go to **Resource groups**, and select your logic app's resource group.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-224">On the main Azure menu, go to **Resource groups**, and select your logic app's resource group.</span></span> <span data-ttu-id="cb4e3-225">On the **Overview** page, choose **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-225">On the **Overview** page, choose **Delete resource group**.</span></span> 

   !["Resource groups" > "Overview" > "Delete resource group"](./media/quickstart-create-first-logic-app-workflow/delete-resource-group.png)

2. <span data-ttu-id="cb4e3-227">Enter the resource group name as confirmation, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-227">Enter the resource group name as confirmation, and choose **Delete**.</span></span>

   ![Confirm deletion](./media/quickstart-create-first-logic-app-workflow/delete-resource-group-2.png)

> [!NOTE]
> <span data-ttu-id="cb4e3-229">When you delete a logic app, no new runs are instantiated.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-229">When you delete a logic app, no new runs are instantiated.</span></span> <span data-ttu-id="cb4e3-230">All in-progress and pending runs are canceled.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-230">All in-progress and pending runs are canceled.</span></span> <span data-ttu-id="cb4e3-231">If you have thousands of runs, cancellation might take significant time to complete.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-231">If you have thousands of runs, cancellation might take significant time to complete.</span></span>

## <a name="get-support"></a><span data-ttu-id="cb4e3-232">Get support</span><span class="sxs-lookup"><span data-stu-id="cb4e3-232">Get support</span></span>

* <span data-ttu-id="cb4e3-233">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="cb4e3-233">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="cb4e3-234">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="cb4e3-234">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb4e3-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb4e3-235">Next steps</span></span>

<span data-ttu-id="cb4e3-236">In this quickstart, you created your first logic app that checks for RSS updates based your specified schedule (every minute), and takes action (sends email) when updates exist.</span><span class="sxs-lookup"><span data-stu-id="cb4e3-236">In this quickstart, you created your first logic app that checks for RSS updates based your specified schedule (every minute), and takes action (sends email) when updates exist.</span></span> <span data-ttu-id="cb4e3-237">To learn more, continue with this tutorial that creates more advanced schedule-based workflows:</span><span class="sxs-lookup"><span data-stu-id="cb4e3-237">To learn more, continue with this tutorial that creates more advanced schedule-based workflows:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb4e3-238">Check traffic with a scheduled-based logic app</span><span class="sxs-lookup"><span data-stu-id="cb4e3-238">Check traffic with a scheduled-based logic app</span></span>](../logic-apps/tutorial-build-schedule-recurring-logic-app-workflow.md)
