---
title: Build approval workflows to process mailing list requests - Azure Logic Apps | Microsoft Docs
description: Tutorial - How to create automated approval workflows for processing mailing list subscriptions with Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: tutorial
ms.custom: mvc
ms.date: 01/12/2018
ms.openlocfilehash: 4ac5861dabbc473099886b4f099824cde60f38b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969075"
---
# <a name="manage-mailing-list-requests-with-a-logic-app"></a><span data-ttu-id="bfe01-103">Manage mailing list requests with a logic app</span><span class="sxs-lookup"><span data-stu-id="bfe01-103">Manage mailing list requests with a logic app</span></span>

<span data-ttu-id="bfe01-104">Azure Logic Apps helps you automate workflows and integrate data across Azure services, Microsoft services, other software-as-a-service (SaaS) apps, and on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="bfe01-104">Azure Logic Apps helps you automate workflows and integrate data across Azure services, Microsoft services, other software-as-a-service (SaaS) apps, and on-premises systems.</span></span> <span data-ttu-id="bfe01-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) that processes subscription requests for a mailing list managed by the [MailChimp](https://mailchimp.com/) service.</span><span class="sxs-lookup"><span data-stu-id="bfe01-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) that processes subscription requests for a mailing list managed by the [MailChimp](https://mailchimp.com/) service.</span></span>
<span data-ttu-id="bfe01-106">This logic app monitors an email account for these requests, sends these requests for approval, and adds approved members to the mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-106">This logic app monitors an email account for these requests, sends these requests for approval, and adds approved members to the mailing list.</span></span>

<span data-ttu-id="bfe01-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="bfe01-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bfe01-108">Create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-108">Create a blank logic app.</span></span>
> * <span data-ttu-id="bfe01-109">Add a trigger that monitors emails for subscription requests.</span><span class="sxs-lookup"><span data-stu-id="bfe01-109">Add a trigger that monitors emails for subscription requests.</span></span>
> * <span data-ttu-id="bfe01-110">Add an action that sends emails for approving or rejecting these requests.</span><span class="sxs-lookup"><span data-stu-id="bfe01-110">Add an action that sends emails for approving or rejecting these requests.</span></span>
> * <span data-ttu-id="bfe01-111">Add a condition that checks the approval response.</span><span class="sxs-lookup"><span data-stu-id="bfe01-111">Add a condition that checks the approval response.</span></span>
> * <span data-ttu-id="bfe01-112">Add an action that adds approved members to the mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-112">Add an action that adds approved members to the mailing list.</span></span>
> * <span data-ttu-id="bfe01-113">Add a condition that checks whether these members successfully joined the list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-113">Add a condition that checks whether these members successfully joined the list.</span></span>
> * <span data-ttu-id="bfe01-114">Add an action that sends emails confirming whether these members successfully joined the list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-114">Add an action that sends emails confirming whether these members successfully joined the list.</span></span>

<span data-ttu-id="bfe01-115">When you're done, your logic app looks like this workflow at a high level:</span><span class="sxs-lookup"><span data-stu-id="bfe01-115">When you're done, your logic app looks like this workflow at a high level:</span></span>

![High-level finished logic app](./media/tutorial-process-mailing-list-subscriptions-workflow/tutorial-overview.png)

<span data-ttu-id="bfe01-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span><span class="sxs-lookup"><span data-stu-id="bfe01-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfe01-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfe01-118">Prerequisites</span></span>

* <span data-ttu-id="bfe01-119">A MailChimp account.</span><span class="sxs-lookup"><span data-stu-id="bfe01-119">A MailChimp account.</span></span> <span data-ttu-id="bfe01-120">Create a list named "test-members-ML" where your logic app can add email addresses for approved members.</span><span class="sxs-lookup"><span data-stu-id="bfe01-120">Create a list named "test-members-ML" where your logic app can add email addresses for approved members.</span></span> <span data-ttu-id="bfe01-121">If you don't have an account, [sign up for a free account](https://login.mailchimp.com/signup/) and learn [how to create  a list](https://us17.admin.mailchimp.com/lists/#).</span><span class="sxs-lookup"><span data-stu-id="bfe01-121">If you don't have an account, [sign up for a free account](https://login.mailchimp.com/signup/) and learn [how to create  a list](https://us17.admin.mailchimp.com/lists/#).</span></span> 

* <span data-ttu-id="bfe01-122">An email account with Office 365 Outlook or Outlook.com, which support approval workflows.</span><span class="sxs-lookup"><span data-stu-id="bfe01-122">An email account with Office 365 Outlook or Outlook.com, which support approval workflows.</span></span> <span data-ttu-id="bfe01-123">This article uses Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="bfe01-123">This article uses Office 365 Outlook.</span></span> <span data-ttu-id="bfe01-124">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span><span class="sxs-lookup"><span data-stu-id="bfe01-124">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="bfe01-125">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bfe01-125">Sign in to the Azure portal</span></span>

<span data-ttu-id="bfe01-126">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="bfe01-126">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span></span>

## <a name="create-your-logic-app"></a><span data-ttu-id="bfe01-127">Create your logic app</span><span class="sxs-lookup"><span data-stu-id="bfe01-127">Create your logic app</span></span>

1. <span data-ttu-id="bfe01-128">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-128">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/tutorial-process-mailing-list-subscriptions-workflow/create-logic-app.png)

2. <span data-ttu-id="bfe01-130">Under **Create logic app**, provide this information about your logic app as shown and described.</span><span class="sxs-lookup"><span data-stu-id="bfe01-130">Under **Create logic app**, provide this information about your logic app as shown and described.</span></span> <span data-ttu-id="bfe01-131">When you're done, choose **Pin to dashboard** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-131">When you're done, choose **Pin to dashboard** > **Create**.</span></span>

   ![Provide logic app information](./media/tutorial-process-mailing-list-subscriptions-workflow/create-logic-app-settings.png)

   | <span data-ttu-id="bfe01-133">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-133">Setting</span></span> | <span data-ttu-id="bfe01-134">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-134">Value</span></span> | <span data-ttu-id="bfe01-135">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-135">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="bfe01-136">**Name**</span><span class="sxs-lookup"><span data-stu-id="bfe01-136">**Name**</span></span> | <span data-ttu-id="bfe01-137">LA-MailingList</span><span class="sxs-lookup"><span data-stu-id="bfe01-137">LA-MailingList</span></span> | <span data-ttu-id="bfe01-138">The name for your logic app</span><span class="sxs-lookup"><span data-stu-id="bfe01-138">The name for your logic app</span></span> | 
   | <span data-ttu-id="bfe01-139">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="bfe01-139">**Subscription**</span></span> | <span data-ttu-id="bfe01-140"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="bfe01-140"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="bfe01-141">The name for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="bfe01-141">The name for your Azure subscription</span></span> | 
   | <span data-ttu-id="bfe01-142">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="bfe01-142">**Resource group**</span></span> | <span data-ttu-id="bfe01-143">LA-MailingList-RG</span><span class="sxs-lookup"><span data-stu-id="bfe01-143">LA-MailingList-RG</span></span> | <span data-ttu-id="bfe01-144">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span><span class="sxs-lookup"><span data-stu-id="bfe01-144">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span></span> | 
   | <span data-ttu-id="bfe01-145">**Location**</span><span class="sxs-lookup"><span data-stu-id="bfe01-145">**Location**</span></span> | <span data-ttu-id="bfe01-146">East US 2</span><span class="sxs-lookup"><span data-stu-id="bfe01-146">East US 2</span></span> | <span data-ttu-id="bfe01-147">The region where to store information about your logic app</span><span class="sxs-lookup"><span data-stu-id="bfe01-147">The region where to store information about your logic app</span></span> | 
   | <span data-ttu-id="bfe01-148">**Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="bfe01-148">**Log Analytics**</span></span> | <span data-ttu-id="bfe01-149">Off</span><span class="sxs-lookup"><span data-stu-id="bfe01-149">Off</span></span> | <span data-ttu-id="bfe01-150">Keep the **Off** setting for diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="bfe01-150">Keep the **Off** setting for diagnostic logging.</span></span> | 
   |||| 

3. <span data-ttu-id="bfe01-151">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span><span class="sxs-lookup"><span data-stu-id="bfe01-151">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span></span> <span data-ttu-id="bfe01-152">Under **Templates**, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-152">Under **Templates**, choose **Blank Logic App**.</span></span>

   ![Choose blank logic app template](./media/tutorial-process-mailing-list-subscriptions-workflow/choose-logic-app-template.png)

<span data-ttu-id="bfe01-154">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that listens for incoming emails with subscription requests.</span><span class="sxs-lookup"><span data-stu-id="bfe01-154">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that listens for incoming emails with subscription requests.</span></span>
<span data-ttu-id="bfe01-155">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span><span class="sxs-lookup"><span data-stu-id="bfe01-155">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span></span> <span data-ttu-id="bfe01-156">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="bfe01-156">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="add-trigger-to-monitor-emails"></a><span data-ttu-id="bfe01-157">Add trigger to monitor emails</span><span class="sxs-lookup"><span data-stu-id="bfe01-157">Add trigger to monitor emails</span></span>

1. <span data-ttu-id="bfe01-158">On the designer, enter "when email arrives" in the search box.</span><span class="sxs-lookup"><span data-stu-id="bfe01-158">On the designer, enter "when email arrives" in the search box.</span></span> <span data-ttu-id="bfe01-159">Select the trigger for your email provider: **<*your-email-provider*> - When a new email arrives**</span><span class="sxs-lookup"><span data-stu-id="bfe01-159">Select the trigger for your email provider: **<*your-email-provider*> - When a new email arrives**</span></span>
   
   ![Select this trigger for email provider: "When a new email arrives"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-trigger-new-email.png)

   * <span data-ttu-id="bfe01-161">For Azure work or school accounts, select Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="bfe01-161">For Azure work or school accounts, select Office 365 Outlook.</span></span>
   * <span data-ttu-id="bfe01-162">For personal Microsoft accounts, select Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="bfe01-162">For personal Microsoft accounts, select Outlook.com.</span></span>

2. <span data-ttu-id="bfe01-163">If you're asked for credentials, sign in to your email account so that Logic Apps can create a connection to your email account.</span><span class="sxs-lookup"><span data-stu-id="bfe01-163">If you're asked for credentials, sign in to your email account so that Logic Apps can create a connection to your email account.</span></span>

3. <span data-ttu-id="bfe01-164">Now specify the criteria that the trigger checks in all new email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-164">Now specify the criteria that the trigger checks in all new email.</span></span>

   1. <span data-ttu-id="bfe01-165">Specify the folder, interval, and frequency for checking emails.</span><span class="sxs-lookup"><span data-stu-id="bfe01-165">Specify the folder, interval, and frequency for checking emails.</span></span>

      ![Specify folder, interval, and frequency for checking mails](./media/tutorial-process-mailing-list-subscriptions-workflow/add-trigger-set-up-email.png)

      | <span data-ttu-id="bfe01-167">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-167">Setting</span></span> | <span data-ttu-id="bfe01-168">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-168">Value</span></span> | <span data-ttu-id="bfe01-169">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-169">Description</span></span> | 
      | ------- | ----- | ----------- | 
      | <span data-ttu-id="bfe01-170">**Folder**</span><span class="sxs-lookup"><span data-stu-id="bfe01-170">**Folder**</span></span> | <span data-ttu-id="bfe01-171">Inbox</span><span class="sxs-lookup"><span data-stu-id="bfe01-171">Inbox</span></span> | <span data-ttu-id="bfe01-172">The email folder to monitor</span><span class="sxs-lookup"><span data-stu-id="bfe01-172">The email folder to monitor</span></span> | 
      | <span data-ttu-id="bfe01-173">**Interval**</span><span class="sxs-lookup"><span data-stu-id="bfe01-173">**Interval**</span></span> | <span data-ttu-id="bfe01-174">1</span><span class="sxs-lookup"><span data-stu-id="bfe01-174">1</span></span> | <span data-ttu-id="bfe01-175">The number of intervals to wait between checks</span><span class="sxs-lookup"><span data-stu-id="bfe01-175">The number of intervals to wait between checks</span></span> | 
      | <span data-ttu-id="bfe01-176">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="bfe01-176">**Frequency**</span></span> | <span data-ttu-id="bfe01-177">Hour</span><span class="sxs-lookup"><span data-stu-id="bfe01-177">Hour</span></span> | <span data-ttu-id="bfe01-178">The unit of time for each interval between checks</span><span class="sxs-lookup"><span data-stu-id="bfe01-178">The unit of time for each interval between checks</span></span>  | 
      |  |  |  | 

   2. <span data-ttu-id="bfe01-179">Choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-179">Choose **Show advanced options**.</span></span> <span data-ttu-id="bfe01-180">In the **Subject Filter** box, enter this text for the trigger to find in the email subject: ```subscribe-test-members-ML```</span><span class="sxs-lookup"><span data-stu-id="bfe01-180">In the **Subject Filter** box, enter this text for the trigger to find in the email subject: ```subscribe-test-members-ML```</span></span>

      ![Set advanced options](./media/tutorial-process-mailing-list-subscriptions-workflow/add-trigger-set-advanced-options.png)

4. <span data-ttu-id="bfe01-182">To hide the trigger's details for now, click the trigger's title bar.</span><span class="sxs-lookup"><span data-stu-id="bfe01-182">To hide the trigger's details for now, click the trigger's title bar.</span></span>

   ![Collapse shape to hide details](./media/tutorial-process-mailing-list-subscriptions-workflow/collapse-trigger-shape.png)

5. <span data-ttu-id="bfe01-184">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-184">Save your logic app.</span></span> <span data-ttu-id="bfe01-185">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-185">On the designer toolbar, choose **Save**.</span></span>

   <span data-ttu-id="bfe01-186">Your logic app is now live but doesn't do anything other than check your incoming email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-186">Your logic app is now live but doesn't do anything other than check your incoming email.</span></span> 
   <span data-ttu-id="bfe01-187">So, add an action that responds when the trigger fires.</span><span class="sxs-lookup"><span data-stu-id="bfe01-187">So, add an action that responds when the trigger fires.</span></span>

## <a name="send-approval-email"></a><span data-ttu-id="bfe01-188">Send approval email</span><span class="sxs-lookup"><span data-stu-id="bfe01-188">Send approval email</span></span>

<span data-ttu-id="bfe01-189">Now that you have a trigger, add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that sends an email to approve or reject the request.</span><span class="sxs-lookup"><span data-stu-id="bfe01-189">Now that you have a trigger, add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that sends an email to approve or reject the request.</span></span> 

1. <span data-ttu-id="bfe01-190">Under the trigger, choose **+ New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-190">Under the trigger, choose **+ New step** > **Add an action**.</span></span> <span data-ttu-id="bfe01-191">Search for "approval", and select this action: **<*your-email-provider*> - Send approval email**</span><span class="sxs-lookup"><span data-stu-id="bfe01-191">Search for "approval", and select this action: **<*your-email-provider*> - Send approval email**</span></span>

   ![Choose "<your-email-provider> - Send approval email"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-send-approval-email.png)

2. <span data-ttu-id="bfe01-193">Provide information for this action as shown and described:</span><span class="sxs-lookup"><span data-stu-id="bfe01-193">Provide information for this action as shown and described:</span></span> 

   ![Set approval email settings](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-approval-email-settings.png)

   | <span data-ttu-id="bfe01-195">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-195">Setting</span></span> | <span data-ttu-id="bfe01-196">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-196">Value</span></span> | <span data-ttu-id="bfe01-197">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-197">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="bfe01-198">**To**</span><span class="sxs-lookup"><span data-stu-id="bfe01-198">**To**</span></span> | <span data-ttu-id="bfe01-199"><*approver-email-address*></span><span class="sxs-lookup"><span data-stu-id="bfe01-199"><*approver-email-address*></span></span> | <span data-ttu-id="bfe01-200">The approver's email address.</span><span class="sxs-lookup"><span data-stu-id="bfe01-200">The approver's email address.</span></span> <span data-ttu-id="bfe01-201">For testing purposes, you can use your own address.</span><span class="sxs-lookup"><span data-stu-id="bfe01-201">For testing purposes, you can use your own address.</span></span> | 
   | <span data-ttu-id="bfe01-202">**User Options**</span><span class="sxs-lookup"><span data-stu-id="bfe01-202">**User Options**</span></span> | <span data-ttu-id="bfe01-203">Approve, Reject</span><span class="sxs-lookup"><span data-stu-id="bfe01-203">Approve, Reject</span></span> | <span data-ttu-id="bfe01-204">The response options that the approver can choose.</span><span class="sxs-lookup"><span data-stu-id="bfe01-204">The response options that the approver can choose.</span></span> <span data-ttu-id="bfe01-205">By default, the approver can choose either "Approve" or "Reject" as their response.</span><span class="sxs-lookup"><span data-stu-id="bfe01-205">By default, the approver can choose either "Approve" or "Reject" as their response.</span></span> | 
   | <span data-ttu-id="bfe01-206">**Subject**</span><span class="sxs-lookup"><span data-stu-id="bfe01-206">**Subject**</span></span> | <span data-ttu-id="bfe01-207">Approve member request for test-members-ML</span><span class="sxs-lookup"><span data-stu-id="bfe01-207">Approve member request for test-members-ML</span></span> | <span data-ttu-id="bfe01-208">A descriptive email subject</span><span class="sxs-lookup"><span data-stu-id="bfe01-208">A descriptive email subject</span></span> | 
   |  |  |  | 

   <span data-ttu-id="bfe01-209">For now, ignore the dynamic content list or inline parameter list that appears when you click inside specific edit boxes.</span><span class="sxs-lookup"><span data-stu-id="bfe01-209">For now, ignore the dynamic content list or inline parameter list that appears when you click inside specific edit boxes.</span></span> 
   <span data-ttu-id="bfe01-210">This list lets you select parameters from previous actions that you can use as inputs in your workflow.</span><span class="sxs-lookup"><span data-stu-id="bfe01-210">This list lets you select parameters from previous actions that you can use as inputs in your workflow.</span></span> 
   <span data-ttu-id="bfe01-211">Your browser width determines which list appears.</span><span class="sxs-lookup"><span data-stu-id="bfe01-211">Your browser width determines which list appears.</span></span> 
 
4. <span data-ttu-id="bfe01-212">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-212">Save your logic app.</span></span>

<span data-ttu-id="bfe01-213">Next, add a condition to check the approver's chosen response.</span><span class="sxs-lookup"><span data-stu-id="bfe01-213">Next, add a condition to check the approver's chosen response.</span></span>

## <a name="check-approval-response"></a><span data-ttu-id="bfe01-214">Check approval response</span><span class="sxs-lookup"><span data-stu-id="bfe01-214">Check approval response</span></span>

1. <span data-ttu-id="bfe01-215">Under the **Send approval email** action, choose **+ New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-215">Under the **Send approval email** action, choose **+ New step** > **Add a condition**.</span></span>

   <span data-ttu-id="bfe01-216">The condition shape appears, along with any available parameters that you can include as input to your workflow.</span><span class="sxs-lookup"><span data-stu-id="bfe01-216">The condition shape appears, along with any available parameters that you can include as input to your workflow.</span></span> 

2. <span data-ttu-id="bfe01-217">Rename the condition with a better description.</span><span class="sxs-lookup"><span data-stu-id="bfe01-217">Rename the condition with a better description.</span></span>

   1. <span data-ttu-id="bfe01-218">On the condition's title bar, choose **ellipses** (**...**) button > **Rename**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-218">On the condition's title bar, choose **ellipses** (**...**) button > **Rename**.</span></span>

      <span data-ttu-id="bfe01-219">For example, if your browser is in narrow view:</span><span class="sxs-lookup"><span data-stu-id="bfe01-219">For example, if your browser is in narrow view:</span></span>

      ![Rename condition](./media/tutorial-process-mailing-list-subscriptions-workflow/condition-rename.png)

      <span data-ttu-id="bfe01-221">If your browser is in wide view, and the dynamic content list blocks access to the ellipses button, close the list by choosing **Add dynamic content** inside the condition.</span><span class="sxs-lookup"><span data-stu-id="bfe01-221">If your browser is in wide view, and the dynamic content list blocks access to the ellipses button, close the list by choosing **Add dynamic content** inside the condition.</span></span>

   2. <span data-ttu-id="bfe01-222">Rename your condition with this description: ```If request approved```</span><span class="sxs-lookup"><span data-stu-id="bfe01-222">Rename your condition with this description: ```If request approved```</span></span>

3. <span data-ttu-id="bfe01-223">Build a condition that checks whether the approver selected **Approve**:</span><span class="sxs-lookup"><span data-stu-id="bfe01-223">Build a condition that checks whether the approver selected **Approve**:</span></span>

   1. <span data-ttu-id="bfe01-224">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span><span class="sxs-lookup"><span data-stu-id="bfe01-224">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span></span>
   <span data-ttu-id="bfe01-225">From either the parameter list or the dynamic content list, select the **SelectedOption** field under **Send approval email**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-225">From either the parameter list or the dynamic content list, select the **SelectedOption** field under **Send approval email**.</span></span>

      <span data-ttu-id="bfe01-226">For example, if you're working in wide view, your condition looks like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-226">For example, if you're working in wide view, your condition looks like this example:</span></span>

      ![Under "Send approval email", select "SelectedOption"](./media/tutorial-process-mailing-list-subscriptions-workflow/build-condition-check-approval-response.png)

   2. <span data-ttu-id="bfe01-228">In the comparison operator box, select this operator: **is equal to**</span><span class="sxs-lookup"><span data-stu-id="bfe01-228">In the comparison operator box, select this operator: **is equal to**</span></span>

   3. <span data-ttu-id="bfe01-229">In the right (wide view) or bottom (narrow view) **Choose a value** box, enter this value: ```Approve```</span><span class="sxs-lookup"><span data-stu-id="bfe01-229">In the right (wide view) or bottom (narrow view) **Choose a value** box, enter this value: ```Approve```</span></span>

      <span data-ttu-id="bfe01-230">When you're done, your condition looks like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-230">When you're done, your condition looks like this example:</span></span>

      ![Complete condition](./media/tutorial-process-mailing-list-subscriptions-workflow/build-condition-check-approval-response-2.png)

4. <span data-ttu-id="bfe01-232">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-232">Save your logic app.</span></span>

<span data-ttu-id="bfe01-233">Next, specify the action that your logic app performs when the reviewer approves the request.</span><span class="sxs-lookup"><span data-stu-id="bfe01-233">Next, specify the action that your logic app performs when the reviewer approves the request.</span></span> 

## <a name="add-member-to-mailchimp-list"></a><span data-ttu-id="bfe01-234">Add member to MailChimp list</span><span class="sxs-lookup"><span data-stu-id="bfe01-234">Add member to MailChimp list</span></span>

<span data-ttu-id="bfe01-235">Now, add an action that adds the approved member to your mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-235">Now, add an action that adds the approved member to your mailing list.</span></span>

1. <span data-ttu-id="bfe01-236">Inside the condition's **If true** branch, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-236">Inside the condition's **If true** branch, choose **Add an action**.</span></span>
<span data-ttu-id="bfe01-237">Search for "mailchimp", and select this action: **MailChimp - Add member to list**</span><span class="sxs-lookup"><span data-stu-id="bfe01-237">Search for "mailchimp", and select this action: **MailChimp - Add member to list**</span></span>

   ![Select "MailChimp - Add member to list"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-mailchimp-add-member.png)

3. <span data-ttu-id="bfe01-239">If you're asked to sign in to your MailChimp account, sign in with your MailChimp credentials.</span><span class="sxs-lookup"><span data-stu-id="bfe01-239">If you're asked to sign in to your MailChimp account, sign in with your MailChimp credentials.</span></span>

4. <span data-ttu-id="bfe01-240">Provide information for this action as shown and described here:</span><span class="sxs-lookup"><span data-stu-id="bfe01-240">Provide information for this action as shown and described here:</span></span>

   ![Provide information for "Add member to list"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-mailchimp-add-member-settings.png)

   | <span data-ttu-id="bfe01-242">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-242">Setting</span></span> | <span data-ttu-id="bfe01-243">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-243">Value</span></span> | <span data-ttu-id="bfe01-244">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-244">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="bfe01-245">**List Id**</span><span class="sxs-lookup"><span data-stu-id="bfe01-245">**List Id**</span></span> | <span data-ttu-id="bfe01-246">test-members-ML</span><span class="sxs-lookup"><span data-stu-id="bfe01-246">test-members-ML</span></span> | <span data-ttu-id="bfe01-247">The name for your MailChimp mailing list</span><span class="sxs-lookup"><span data-stu-id="bfe01-247">The name for your MailChimp mailing list</span></span> | 
   | <span data-ttu-id="bfe01-248">**Status**</span><span class="sxs-lookup"><span data-stu-id="bfe01-248">**Status**</span></span> | <span data-ttu-id="bfe01-249">subscribed</span><span class="sxs-lookup"><span data-stu-id="bfe01-249">subscribed</span></span> | <span data-ttu-id="bfe01-250">The subscription status for the new member.</span><span class="sxs-lookup"><span data-stu-id="bfe01-250">The subscription status for the new member.</span></span> <span data-ttu-id="bfe01-251">For more information, see <a href="https://developer.mailchimp.com/documentation/mailchimp/guides/manage-subscribers-with-the-mailchimp-api/" target="_blank">Manage subscribers with the MailChimp API</a>.</span><span class="sxs-lookup"><span data-stu-id="bfe01-251">For more information, see <a href="https://developer.mailchimp.com/documentation/mailchimp/guides/manage-subscribers-with-the-mailchimp-api/" target="_blank">Manage subscribers with the MailChimp API</a>.</span></span> | 
   | <span data-ttu-id="bfe01-252">**Email Address**</span><span class="sxs-lookup"><span data-stu-id="bfe01-252">**Email Address**</span></span> | <span data-ttu-id="bfe01-253"><*new-member-email-address*></span><span class="sxs-lookup"><span data-stu-id="bfe01-253"><*new-member-email-address*></span></span> | <span data-ttu-id="bfe01-254">From either the parameter list or dynamic content list, select **From** under **When a new mail arrives**, which passes in the email address for the new member.</span><span class="sxs-lookup"><span data-stu-id="bfe01-254">From either the parameter list or dynamic content list, select **From** under **When a new mail arrives**, which passes in the email address for the new member.</span></span> 
   |  |  |  | 

5. <span data-ttu-id="bfe01-255">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-255">Save your logic app.</span></span>

<span data-ttu-id="bfe01-256">Next, add a condition so that you can check whether the new member successfully joined your mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-256">Next, add a condition so that you can check whether the new member successfully joined your mailing list.</span></span> <span data-ttu-id="bfe01-257">That way, your logic app notifies you whether this operation succeeds or fails.</span><span class="sxs-lookup"><span data-stu-id="bfe01-257">That way, your logic app notifies you whether this operation succeeds or fails.</span></span>

## <a name="check-for-success-or-failure"></a><span data-ttu-id="bfe01-258">Check for success or failure</span><span class="sxs-lookup"><span data-stu-id="bfe01-258">Check for success or failure</span></span>

1. <span data-ttu-id="bfe01-259">In the **If true** branch, under the **Add member to list** action, choose **More...** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-259">In the **If true** branch, under the **Add member to list** action, choose **More...** > **Add a condition**.</span></span>

2. <span data-ttu-id="bfe01-260">Rename the condition with this description: ```If add member succeeded```</span><span class="sxs-lookup"><span data-stu-id="bfe01-260">Rename the condition with this description: ```If add member succeeded```</span></span>

3. <span data-ttu-id="bfe01-261">Build a condition that checks whether the approved member succeeds or fails in joining your mailing list:</span><span class="sxs-lookup"><span data-stu-id="bfe01-261">Build a condition that checks whether the approved member succeeds or fails in joining your mailing list:</span></span>

   1. <span data-ttu-id="bfe01-262">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span><span class="sxs-lookup"><span data-stu-id="bfe01-262">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span></span>
   <span data-ttu-id="bfe01-263">From either the parameter list or the dynamic content list, select the **Status** field under **Add member to list**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-263">From either the parameter list or the dynamic content list, select the **Status** field under **Add member to list**.</span></span>

      <span data-ttu-id="bfe01-264">For example, if you're working in wide view, your condition looks like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-264">For example, if you're working in wide view, your condition looks like this example:</span></span>

      ![Under "Add member to list", select "Status"](./media/tutorial-process-mailing-list-subscriptions-workflow/build-condition-check-added-member.png)

   2. <span data-ttu-id="bfe01-266">In the comparison operator box, select this operator: **is equal to**</span><span class="sxs-lookup"><span data-stu-id="bfe01-266">In the comparison operator box, select this operator: **is equal to**</span></span>

   3. <span data-ttu-id="bfe01-267">In the right (wide view) or bottom (narrow view) **Choose a value** box, enter this value: ```subscribed```</span><span class="sxs-lookup"><span data-stu-id="bfe01-267">In the right (wide view) or bottom (narrow view) **Choose a value** box, enter this value: ```subscribed```</span></span>

   <span data-ttu-id="bfe01-268">When you're done, your condition looks like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-268">When you're done, your condition looks like this example:</span></span>

   ![Completed condition](./media/tutorial-process-mailing-list-subscriptions-workflow/build-condition-check-added-member-2.png)

<span data-ttu-id="bfe01-270">Next, set up the emails to send when the approved member succeeds or fails in joining your mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-270">Next, set up the emails to send when the approved member succeeds or fails in joining your mailing list.</span></span>

## <a name="send-email-if-member-added"></a><span data-ttu-id="bfe01-271">Send email if member added</span><span class="sxs-lookup"><span data-stu-id="bfe01-271">Send email if member added</span></span>

1. <span data-ttu-id="bfe01-272">In the **If true** branch for the condition **If add member succeeded**, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-272">In the **If true** branch for the condition **If add member succeeded**, choose **Add an action**.</span></span>

   ![In "If true" branch for condition, choose "Add an action"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-success.png)

2. <span data-ttu-id="bfe01-274">Search for "outlook send email", and select this action: **<*your-email-provider*> - Send an email**</span><span class="sxs-lookup"><span data-stu-id="bfe01-274">Search for "outlook send email", and select this action: **<*your-email-provider*> - Send an email**</span></span>

   ![Add action for "Send an email"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-success-2.png)

3. <span data-ttu-id="bfe01-276">Rename the action with this description: ```Send email on success```</span><span class="sxs-lookup"><span data-stu-id="bfe01-276">Rename the action with this description: ```Send email on success```</span></span>

4. <span data-ttu-id="bfe01-277">Provide information for this action as shown and described:</span><span class="sxs-lookup"><span data-stu-id="bfe01-277">Provide information for this action as shown and described:</span></span>

   ![Provide information for success email](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-success-settings.png)

   | <span data-ttu-id="bfe01-279">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-279">Setting</span></span> | <span data-ttu-id="bfe01-280">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-280">Value</span></span> | <span data-ttu-id="bfe01-281">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-281">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="bfe01-282">**To**</span><span class="sxs-lookup"><span data-stu-id="bfe01-282">**To**</span></span> | <span data-ttu-id="bfe01-283"><*your-email-address*></span><span class="sxs-lookup"><span data-stu-id="bfe01-283"><*your-email-address*></span></span> | <span data-ttu-id="bfe01-284">The email address for where to send the success email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-284">The email address for where to send the success email.</span></span> <span data-ttu-id="bfe01-285">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="bfe01-285">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="bfe01-286">**Subject**</span><span class="sxs-lookup"><span data-stu-id="bfe01-286">**Subject**</span></span> | <span data-ttu-id="bfe01-287"><*subject-for-success-email*></span><span class="sxs-lookup"><span data-stu-id="bfe01-287"><*subject-for-success-email*></span></span> | <span data-ttu-id="bfe01-288">The subject for the success email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-288">The subject for the success email.</span></span> <span data-ttu-id="bfe01-289">For this tutorial, enter this text and select the specified field under **Add member to list** from the parameter list or dynamic content list:</span><span class="sxs-lookup"><span data-stu-id="bfe01-289">For this tutorial, enter this text and select the specified field under **Add member to list** from the parameter list or dynamic content list:</span></span> <p><span data-ttu-id="bfe01-290">"Success!</span><span class="sxs-lookup"><span data-stu-id="bfe01-290">"Success!</span></span> <span data-ttu-id="bfe01-291">Member added to 'test-members-ML': **Email Address**"</span><span class="sxs-lookup"><span data-stu-id="bfe01-291">Member added to 'test-members-ML': **Email Address**"</span></span> | 
   | <span data-ttu-id="bfe01-292">**Body**</span><span class="sxs-lookup"><span data-stu-id="bfe01-292">**Body**</span></span> | <span data-ttu-id="bfe01-293"><*body-for-success-email*></span><span class="sxs-lookup"><span data-stu-id="bfe01-293"><*body-for-success-email*></span></span> | <span data-ttu-id="bfe01-294">The body content for the success email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-294">The body content for the success email.</span></span> <span data-ttu-id="bfe01-295">For this tutorial, enter this text and select the specified fields under **Add member to list** from the parameter list or dynamic content list:</span><span class="sxs-lookup"><span data-stu-id="bfe01-295">For this tutorial, enter this text and select the specified fields under **Add member to list** from the parameter list or dynamic content list:</span></span>  <p><span data-ttu-id="bfe01-296">"New member has joined 'test-members-ML': **Email Address**"</span><span class="sxs-lookup"><span data-stu-id="bfe01-296">"New member has joined 'test-members-ML': **Email Address**"</span></span></br><span data-ttu-id="bfe01-297">"Member opt-in status: **Status**"</span><span class="sxs-lookup"><span data-stu-id="bfe01-297">"Member opt-in status: **Status**"</span></span> | 
   | | | | 

5. <span data-ttu-id="bfe01-298">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-298">Save your logic app.</span></span>

## <a name="send-email-if-member-not-added"></a><span data-ttu-id="bfe01-299">Send email if member not added</span><span class="sxs-lookup"><span data-stu-id="bfe01-299">Send email if member not added</span></span>

1. <span data-ttu-id="bfe01-300">In the **If false** branch for the condition **If add member succeeded**, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-300">In the **If false** branch for the condition **If add member succeeded**, choose **Add an action**.</span></span>

   ![In "If false" branch for condition, choose "Add an action"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-failed.png)

2. <span data-ttu-id="bfe01-302">Search for "outlook send email", and select this action: **<*your-email-provider*> - Send an email**</span><span class="sxs-lookup"><span data-stu-id="bfe01-302">Search for "outlook send email", and select this action: **<*your-email-provider*> - Send an email**</span></span>

   ![Add action for "Send an email"](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-failed-2.png)

3. <span data-ttu-id="bfe01-304">Rename the action with this description: ```Send email on failure```</span><span class="sxs-lookup"><span data-stu-id="bfe01-304">Rename the action with this description: ```Send email on failure```</span></span>

4. <span data-ttu-id="bfe01-305">Provide information for this action as shown and described here:</span><span class="sxs-lookup"><span data-stu-id="bfe01-305">Provide information for this action as shown and described here:</span></span>

   ![Provide information for failed email](./media/tutorial-process-mailing-list-subscriptions-workflow/add-action-email-failed-settings.png)

   | <span data-ttu-id="bfe01-307">Setting</span><span class="sxs-lookup"><span data-stu-id="bfe01-307">Setting</span></span> | <span data-ttu-id="bfe01-308">Value</span><span class="sxs-lookup"><span data-stu-id="bfe01-308">Value</span></span> | <span data-ttu-id="bfe01-309">Description</span><span class="sxs-lookup"><span data-stu-id="bfe01-309">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="bfe01-310">**To**</span><span class="sxs-lookup"><span data-stu-id="bfe01-310">**To**</span></span> | <span data-ttu-id="bfe01-311"><*your-email-address*></span><span class="sxs-lookup"><span data-stu-id="bfe01-311"><*your-email-address*></span></span> | <span data-ttu-id="bfe01-312">The email address for where to send the failure email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-312">The email address for where to send the failure email.</span></span> <span data-ttu-id="bfe01-313">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="bfe01-313">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="bfe01-314">**Subject**</span><span class="sxs-lookup"><span data-stu-id="bfe01-314">**Subject**</span></span> | <span data-ttu-id="bfe01-315"><*subject-for-failure-email*></span><span class="sxs-lookup"><span data-stu-id="bfe01-315"><*subject-for-failure-email*></span></span> | <span data-ttu-id="bfe01-316">The subject for the failure email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-316">The subject for the failure email.</span></span> <span data-ttu-id="bfe01-317">For this tutorial, enter this text and select the specified field under **Add member to list** from the parameter list or dynamic content list:</span><span class="sxs-lookup"><span data-stu-id="bfe01-317">For this tutorial, enter this text and select the specified field under **Add member to list** from the parameter list or dynamic content list:</span></span> <p><span data-ttu-id="bfe01-318">"Failed, member not added to 'test-members-ML': **Email Address**"</span><span class="sxs-lookup"><span data-stu-id="bfe01-318">"Failed, member not added to 'test-members-ML': **Email Address**"</span></span> | 
   | <span data-ttu-id="bfe01-319">**Body**</span><span class="sxs-lookup"><span data-stu-id="bfe01-319">**Body**</span></span> | <span data-ttu-id="bfe01-320"><*body-for-failure-email*></span><span class="sxs-lookup"><span data-stu-id="bfe01-320"><*body-for-failure-email*></span></span> | <span data-ttu-id="bfe01-321">The body content for the failure email.</span><span class="sxs-lookup"><span data-stu-id="bfe01-321">The body content for the failure email.</span></span> <span data-ttu-id="bfe01-322">For this tutorial, enter this text:</span><span class="sxs-lookup"><span data-stu-id="bfe01-322">For this tutorial, enter this text:</span></span> <p><span data-ttu-id="bfe01-323">"Member might already exist.</span><span class="sxs-lookup"><span data-stu-id="bfe01-323">"Member might already exist.</span></span> <span data-ttu-id="bfe01-324">Check your MailChimp account."</span><span class="sxs-lookup"><span data-stu-id="bfe01-324">Check your MailChimp account."</span></span> | 
   | | | | 

5. <span data-ttu-id="bfe01-325">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-325">Save your logic app.</span></span> 

<span data-ttu-id="bfe01-326">Next, test your logic app, which now looks similar to this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-326">Next, test your logic app, which now looks similar to this example:</span></span>

 ![Finished logic app](./media/tutorial-process-mailing-list-subscriptions-workflow/tutorial-complete.png)

## <a name="run-your-logic-app"></a><span data-ttu-id="bfe01-328">Run your logic app</span><span class="sxs-lookup"><span data-stu-id="bfe01-328">Run your logic app</span></span>

1. <span data-ttu-id="bfe01-329">Send yourself an email request to join your mailing list.</span><span class="sxs-lookup"><span data-stu-id="bfe01-329">Send yourself an email request to join your mailing list.</span></span>
<span data-ttu-id="bfe01-330">Wait for the request to appear in your inbox.</span><span class="sxs-lookup"><span data-stu-id="bfe01-330">Wait for the request to appear in your inbox.</span></span>

3. <span data-ttu-id="bfe01-331">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-331">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span></span> 

   <span data-ttu-id="bfe01-332">If your email has a subject that matches the trigger's subject filter, your logic app sends you email to approve the subscription request.</span><span class="sxs-lookup"><span data-stu-id="bfe01-332">If your email has a subject that matches the trigger's subject filter, your logic app sends you email to approve the subscription request.</span></span>

4. <span data-ttu-id="bfe01-333">In the approval email, choose **Approve**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-333">In the approval email, choose **Approve**.</span></span>

5. <span data-ttu-id="bfe01-334">If the subscriber's email address doesn't exist on your mailing list, your logic app adds that person's email address and sends you an email like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-334">If the subscriber's email address doesn't exist on your mailing list, your logic app adds that person's email address and sends you an email like this example:</span></span>

   ![Success email](./media/tutorial-process-mailing-list-subscriptions-workflow/add-member-success.png)

   <span data-ttu-id="bfe01-336">If your logic app can't add the subscriber, you get an email like this example:</span><span class="sxs-lookup"><span data-stu-id="bfe01-336">If your logic app can't add the subscriber, you get an email like this example:</span></span>

   ![Failed email](./media/tutorial-process-mailing-list-subscriptions-workflow/add-member-failed.png)

   <span data-ttu-id="bfe01-338">If you don't get any emails, check your email's junk folder.</span><span class="sxs-lookup"><span data-stu-id="bfe01-338">If you don't get any emails, check your email's junk folder.</span></span> 
   <span data-ttu-id="bfe01-339">Your email junk filter might redirect these kinds of mails.</span><span class="sxs-lookup"><span data-stu-id="bfe01-339">Your email junk filter might redirect these kinds of mails.</span></span> 
   <span data-ttu-id="bfe01-340">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="bfe01-340">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

<span data-ttu-id="bfe01-341">Congratulations, you've now created and run a logic app that integrates information across Azure, Microsoft services, and other SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bfe01-341">Congratulations, you've now created and run a logic app that integrates information across Azure, Microsoft services, and other SaaS apps.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bfe01-342">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bfe01-342">Clean up resources</span></span>

<span data-ttu-id="bfe01-343">When no longer needed, delete the resource group that contains your logic app and related resources.</span><span class="sxs-lookup"><span data-stu-id="bfe01-343">When no longer needed, delete the resource group that contains your logic app and related resources.</span></span> <span data-ttu-id="bfe01-344">On the main Azure menu, go to **Resource groups**, and select the resource group for your logic app.</span><span class="sxs-lookup"><span data-stu-id="bfe01-344">On the main Azure menu, go to **Resource groups**, and select the resource group for your logic app.</span></span> <span data-ttu-id="bfe01-345">Choose **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-345">Choose **Delete resource group**.</span></span> <span data-ttu-id="bfe01-346">Enter the resource group name as confirmation, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bfe01-346">Enter the resource group name as confirmation, and choose **Delete**.</span></span>

!["Overview" > "Delete resource group"](./media/tutorial-process-mailing-list-subscriptions-workflow/delete-resource-group.png)

## <a name="get-support"></a><span data-ttu-id="bfe01-348">Get support</span><span class="sxs-lookup"><span data-stu-id="bfe01-348">Get support</span></span>

* <span data-ttu-id="bfe01-349">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="bfe01-349">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="bfe01-350">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="bfe01-350">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfe01-351">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfe01-351">Next steps</span></span>

<span data-ttu-id="bfe01-352">In this tutorial, you created a logic app that manages approvals for mailing list requests.</span><span class="sxs-lookup"><span data-stu-id="bfe01-352">In this tutorial, you created a logic app that manages approvals for mailing list requests.</span></span> <span data-ttu-id="bfe01-353">Now, learn how to build a logic app that processes and stores email attachments by integrating Azure services, such as Azure Storage and Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bfe01-353">Now, learn how to build a logic app that processes and stores email attachments by integrating Azure services, such as Azure Storage and Azure Functions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfe01-354">Process email attachments</span><span class="sxs-lookup"><span data-stu-id="bfe01-354">Process email attachments</span></span>](../logic-apps/tutorial-process-email-attachments-workflow.md)