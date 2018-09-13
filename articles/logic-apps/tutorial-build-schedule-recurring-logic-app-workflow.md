---
title: Build schedule-based automated workflows - Azure Logic Apps | Microsoft Docs
description: Tutorial - How to create a schedule-based, recurring, automated workflow with Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: tutorial
ms.custom: mvc
ms.date: 01/12/2018
ms.openlocfilehash: 43f826414ae7f279c23f6e9e2e39d4d21267e158
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870421"
---
# <a name="check-traffic-with-a-schedule-based-logic-app"></a><span data-ttu-id="aa946-103">Check traffic with a schedule-based logic app</span><span class="sxs-lookup"><span data-stu-id="aa946-103">Check traffic with a schedule-based logic app</span></span>

<span data-ttu-id="aa946-104">Azure Logic Apps helps you automate workflows that run on a schedule.</span><span class="sxs-lookup"><span data-stu-id="aa946-104">Azure Logic Apps helps you automate workflows that run on a schedule.</span></span> <span data-ttu-id="aa946-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) with a scheduler trigger that runs every weekday morning and checks the travel time, including traffic, between two places.</span><span class="sxs-lookup"><span data-stu-id="aa946-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) with a scheduler trigger that runs every weekday morning and checks the travel time, including traffic, between two places.</span></span> <span data-ttu-id="aa946-106">If the time exceeds a specific limit, the logic app sends email with the travel time and the extra time necessary for your destination.</span><span class="sxs-lookup"><span data-stu-id="aa946-106">If the time exceeds a specific limit, the logic app sends email with the travel time and the extra time necessary for your destination.</span></span>

<span data-ttu-id="aa946-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="aa946-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa946-108">Create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-108">Create a blank logic app.</span></span> 
> * <span data-ttu-id="aa946-109">Add a trigger that works as a scheduler for your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-109">Add a trigger that works as a scheduler for your logic app.</span></span>
> * <span data-ttu-id="aa946-110">Add an action that gets the travel time for a route.</span><span class="sxs-lookup"><span data-stu-id="aa946-110">Add an action that gets the travel time for a route.</span></span>
> * <span data-ttu-id="aa946-111">Add an action that creates a variable, converts the travel time from seconds to minutes, and saves that result in the variable.</span><span class="sxs-lookup"><span data-stu-id="aa946-111">Add an action that creates a variable, converts the travel time from seconds to minutes, and saves that result in the variable.</span></span>
> * <span data-ttu-id="aa946-112">Add a condition that compares the travel time against a specified limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-112">Add a condition that compares the travel time against a specified limit.</span></span>
> * <span data-ttu-id="aa946-113">Add an action that sends email if the travel time exceeds the limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-113">Add an action that sends email if the travel time exceeds the limit.</span></span>

<span data-ttu-id="aa946-114">When you're done, your logic app looks like this workflow at a high level:</span><span class="sxs-lookup"><span data-stu-id="aa946-114">When you're done, your logic app looks like this workflow at a high level:</span></span>

![High-level logic app](./media/tutorial-build-scheduled-recurring-logic-app-workflow/check-travel-time-overview.png)

<span data-ttu-id="aa946-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span><span class="sxs-lookup"><span data-stu-id="aa946-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa946-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa946-117">Prerequisites</span></span>

* <span data-ttu-id="aa946-118">An email account from an email provider supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span><span class="sxs-lookup"><span data-stu-id="aa946-118">An email account from an email provider supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span></span> <span data-ttu-id="aa946-119">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span><span class="sxs-lookup"><span data-stu-id="aa946-119">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span></span> <span data-ttu-id="aa946-120">This quickstart uses an Outlook.com account.</span><span class="sxs-lookup"><span data-stu-id="aa946-120">This quickstart uses an Outlook.com account.</span></span> <span data-ttu-id="aa946-121">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span><span class="sxs-lookup"><span data-stu-id="aa946-121">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span></span>

* <span data-ttu-id="aa946-122">To get the travel time for a route, you need an access key for the Bing Maps API.</span><span class="sxs-lookup"><span data-stu-id="aa946-122">To get the travel time for a route, you need an access key for the Bing Maps API.</span></span> <span data-ttu-id="aa946-123">To get this key, follow the steps for <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">how to get a Bing Maps key</a>.</span><span class="sxs-lookup"><span data-stu-id="aa946-123">To get this key, follow the steps for <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">how to get a Bing Maps key</a>.</span></span> 

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="aa946-124">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="aa946-124">Sign in to the Azure portal</span></span>

<span data-ttu-id="aa946-125">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="aa946-125">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span></span>

## <a name="create-your-logic-app"></a><span data-ttu-id="aa946-126">Create your logic app</span><span class="sxs-lookup"><span data-stu-id="aa946-126">Create your logic app</span></span>

1. <span data-ttu-id="aa946-127">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="aa946-127">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/tutorial-build-scheduled-recurring-logic-app-workflow/create-logic-app.png)

2. <span data-ttu-id="aa946-129">Under **Create logic app**, provide this information about your logic app as shown and described.</span><span class="sxs-lookup"><span data-stu-id="aa946-129">Under **Create logic app**, provide this information about your logic app as shown and described.</span></span> <span data-ttu-id="aa946-130">When you're done, choose **Pin to dashboard** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa946-130">When you're done, choose **Pin to dashboard** > **Create**.</span></span>

   ![Provide logic app information](./media/tutorial-build-scheduled-recurring-logic-app-workflow/create-logic-app-settings.png)

   | <span data-ttu-id="aa946-132">Setting</span><span class="sxs-lookup"><span data-stu-id="aa946-132">Setting</span></span> | <span data-ttu-id="aa946-133">Value</span><span class="sxs-lookup"><span data-stu-id="aa946-133">Value</span></span> | <span data-ttu-id="aa946-134">Description</span><span class="sxs-lookup"><span data-stu-id="aa946-134">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="aa946-135">**Name**</span><span class="sxs-lookup"><span data-stu-id="aa946-135">**Name**</span></span> | <span data-ttu-id="aa946-136">LA-TravelTime</span><span class="sxs-lookup"><span data-stu-id="aa946-136">LA-TravelTime</span></span> | <span data-ttu-id="aa946-137">The name for your logic app</span><span class="sxs-lookup"><span data-stu-id="aa946-137">The name for your logic app</span></span> | 
   | <span data-ttu-id="aa946-138">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="aa946-138">**Subscription**</span></span> | <span data-ttu-id="aa946-139"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="aa946-139"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="aa946-140">The name for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="aa946-140">The name for your Azure subscription</span></span> | 
   | <span data-ttu-id="aa946-141">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="aa946-141">**Resource group**</span></span> | <span data-ttu-id="aa946-142">LA-TravelTime-RG</span><span class="sxs-lookup"><span data-stu-id="aa946-142">LA-TravelTime-RG</span></span> | <span data-ttu-id="aa946-143">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span><span class="sxs-lookup"><span data-stu-id="aa946-143">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources</span></span> | 
   | <span data-ttu-id="aa946-144">**Location**</span><span class="sxs-lookup"><span data-stu-id="aa946-144">**Location**</span></span> | <span data-ttu-id="aa946-145">East US 2</span><span class="sxs-lookup"><span data-stu-id="aa946-145">East US 2</span></span> | <span data-ttu-id="aa946-146">The region where to store information about your logic app</span><span class="sxs-lookup"><span data-stu-id="aa946-146">The region where to store information about your logic app</span></span> | 
   | <span data-ttu-id="aa946-147">**Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="aa946-147">**Log Analytics**</span></span> | <span data-ttu-id="aa946-148">Off</span><span class="sxs-lookup"><span data-stu-id="aa946-148">Off</span></span> | <span data-ttu-id="aa946-149">Keep the **Off** setting for diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="aa946-149">Keep the **Off** setting for diagnostic logging.</span></span> | 
   |||| 

3. <span data-ttu-id="aa946-150">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span><span class="sxs-lookup"><span data-stu-id="aa946-150">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span></span> <span data-ttu-id="aa946-151">Under **Templates**, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="aa946-151">Under **Templates**, choose **Blank Logic App**.</span></span>

   ![Choose blank logic app template](./media/tutorial-build-scheduled-recurring-logic-app-workflow/choose-logic-app-template.png)

<span data-ttu-id="aa946-153">Next, add the recurrence [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires based on a specified schedule.</span><span class="sxs-lookup"><span data-stu-id="aa946-153">Next, add the recurrence [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires based on a specified schedule.</span></span> <span data-ttu-id="aa946-154">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span><span class="sxs-lookup"><span data-stu-id="aa946-154">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span></span> <span data-ttu-id="aa946-155">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="aa946-155">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="add-scheduler-trigger"></a><span data-ttu-id="aa946-156">Add scheduler trigger</span><span class="sxs-lookup"><span data-stu-id="aa946-156">Add scheduler trigger</span></span>

1. <span data-ttu-id="aa946-157">On the designer, enter "recurrence" in the search box.</span><span class="sxs-lookup"><span data-stu-id="aa946-157">On the designer, enter "recurrence" in the search box.</span></span> <span data-ttu-id="aa946-158">Select this trigger: **Schedule - Recurrence**</span><span class="sxs-lookup"><span data-stu-id="aa946-158">Select this trigger: **Schedule - Recurrence**</span></span>

   ![Find and add "Schedule-Recurrence" trigger](./media/tutorial-build-scheduled-recurring-logic-app-workflow/add-schedule-recurrence-trigger.png)

2. <span data-ttu-id="aa946-160">On the **Recurrence** shape, choose the **ellipses** (**...**) button, and choose **Rename**.</span><span class="sxs-lookup"><span data-stu-id="aa946-160">On the **Recurrence** shape, choose the **ellipses** (**...**) button, and choose **Rename**.</span></span> <span data-ttu-id="aa946-161">Rename the trigger with this description: ```Check travel time every weekday morning```</span><span class="sxs-lookup"><span data-stu-id="aa946-161">Rename the trigger with this description: ```Check travel time every weekday morning```</span></span>

   ![Rename trigger](./media/tutorial-build-scheduled-recurring-logic-app-workflow/rename-recurrence-schedule-trigger.png)

3. <span data-ttu-id="aa946-163">Inside the trigger, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="aa946-163">Inside the trigger, choose **Show advanced options**.</span></span>

4. <span data-ttu-id="aa946-164">Provide the schedule and recurrence details for your trigger as shown and described:</span><span class="sxs-lookup"><span data-stu-id="aa946-164">Provide the schedule and recurrence details for your trigger as shown and described:</span></span>

   ![Provide schedule and recurrence details](./media/tutorial-build-scheduled-recurring-logic-app-workflow/schedule-recurrence-trigger-settings.png)

   | <span data-ttu-id="aa946-166">Setting</span><span class="sxs-lookup"><span data-stu-id="aa946-166">Setting</span></span> | <span data-ttu-id="aa946-167">Value</span><span class="sxs-lookup"><span data-stu-id="aa946-167">Value</span></span> | <span data-ttu-id="aa946-168">Description</span><span class="sxs-lookup"><span data-stu-id="aa946-168">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="aa946-169">**Interval**</span><span class="sxs-lookup"><span data-stu-id="aa946-169">**Interval**</span></span> | <span data-ttu-id="aa946-170">1</span><span class="sxs-lookup"><span data-stu-id="aa946-170">1</span></span> | <span data-ttu-id="aa946-171">The number of intervals to wait between checks</span><span class="sxs-lookup"><span data-stu-id="aa946-171">The number of intervals to wait between checks</span></span> | 
   | <span data-ttu-id="aa946-172">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="aa946-172">**Frequency**</span></span> | <span data-ttu-id="aa946-173">Week</span><span class="sxs-lookup"><span data-stu-id="aa946-173">Week</span></span> | <span data-ttu-id="aa946-174">The unit of time to use for the recurrence</span><span class="sxs-lookup"><span data-stu-id="aa946-174">The unit of time to use for the recurrence</span></span> | 
   | <span data-ttu-id="aa946-175">**Time zone**</span><span class="sxs-lookup"><span data-stu-id="aa946-175">**Time zone**</span></span> | <span data-ttu-id="aa946-176">None</span><span class="sxs-lookup"><span data-stu-id="aa946-176">None</span></span> | <span data-ttu-id="aa946-177">Applies only when you specify a start time.</span><span class="sxs-lookup"><span data-stu-id="aa946-177">Applies only when you specify a start time.</span></span> <span data-ttu-id="aa946-178">Useful for specifying a non-local time zone.</span><span class="sxs-lookup"><span data-stu-id="aa946-178">Useful for specifying a non-local time zone.</span></span> | 
   | <span data-ttu-id="aa946-179">**Start time**</span><span class="sxs-lookup"><span data-stu-id="aa946-179">**Start time**</span></span> | <span data-ttu-id="aa946-180">None</span><span class="sxs-lookup"><span data-stu-id="aa946-180">None</span></span> | <span data-ttu-id="aa946-181">Delay the recurrence until a specific date and time.</span><span class="sxs-lookup"><span data-stu-id="aa946-181">Delay the recurrence until a specific date and time.</span></span> <span data-ttu-id="aa946-182">For more information, see [Schedule tasks and workflows that run regularly](../connectors/connectors-native-recurrence.md).</span><span class="sxs-lookup"><span data-stu-id="aa946-182">For more information, see [Schedule tasks and workflows that run regularly](../connectors/connectors-native-recurrence.md).</span></span> | 
   | <span data-ttu-id="aa946-183">**On these days**</span><span class="sxs-lookup"><span data-stu-id="aa946-183">**On these days**</span></span> | <span data-ttu-id="aa946-184">Monday,Tuesday,Wednesday,Thursday,Friday</span><span class="sxs-lookup"><span data-stu-id="aa946-184">Monday,Tuesday,Wednesday,Thursday,Friday</span></span> | <span data-ttu-id="aa946-185">Available only when **Frequency** is set to "Week"</span><span class="sxs-lookup"><span data-stu-id="aa946-185">Available only when **Frequency** is set to "Week"</span></span> | 
   | <span data-ttu-id="aa946-186">**At these hours**</span><span class="sxs-lookup"><span data-stu-id="aa946-186">**At these hours**</span></span> | <span data-ttu-id="aa946-187">7,8,9</span><span class="sxs-lookup"><span data-stu-id="aa946-187">7,8,9</span></span> | <span data-ttu-id="aa946-188">Available only when **Frequency** is set to "Week" or "Day".</span><span class="sxs-lookup"><span data-stu-id="aa946-188">Available only when **Frequency** is set to "Week" or "Day".</span></span> <span data-ttu-id="aa946-189">Select the hours of the day to run this recurrence.</span><span class="sxs-lookup"><span data-stu-id="aa946-189">Select the hours of the day to run this recurrence.</span></span> <span data-ttu-id="aa946-190">This example runs at the 7, 8, and 9-hour marks.</span><span class="sxs-lookup"><span data-stu-id="aa946-190">This example runs at the 7, 8, and 9-hour marks.</span></span> | 
   | <span data-ttu-id="aa946-191">**At these minutes**</span><span class="sxs-lookup"><span data-stu-id="aa946-191">**At these minutes**</span></span> | <span data-ttu-id="aa946-192">0,15,30,45</span><span class="sxs-lookup"><span data-stu-id="aa946-192">0,15,30,45</span></span> | <span data-ttu-id="aa946-193">Available only when **Frequency** is set to "Week" or "Day".</span><span class="sxs-lookup"><span data-stu-id="aa946-193">Available only when **Frequency** is set to "Week" or "Day".</span></span> <span data-ttu-id="aa946-194">Select the minutes of the day to run this recurrence.</span><span class="sxs-lookup"><span data-stu-id="aa946-194">Select the minutes of the day to run this recurrence.</span></span> <span data-ttu-id="aa946-195">This example runs every 15 minutes starting at the zero-hour mark.</span><span class="sxs-lookup"><span data-stu-id="aa946-195">This example runs every 15 minutes starting at the zero-hour mark.</span></span> | 
   ||||

   <span data-ttu-id="aa946-196">This trigger fires every weekday, every 15 minutes, starting at 7:00 AM and ending at 9:45 AM.</span><span class="sxs-lookup"><span data-stu-id="aa946-196">This trigger fires every weekday, every 15 minutes, starting at 7:00 AM and ending at 9:45 AM.</span></span> 
   <span data-ttu-id="aa946-197">The **Preview** box shows the recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="aa946-197">The **Preview** box shows the recurrence schedule.</span></span> 
   <span data-ttu-id="aa946-198">For more information, see [Schedule tasks and workflows](../connectors/connectors-native-recurrence.md) and [Workflow actions and triggers](../logic-apps/logic-apps-workflow-actions-triggers.md#recurrence-trigger).</span><span class="sxs-lookup"><span data-stu-id="aa946-198">For more information, see [Schedule tasks and workflows](../connectors/connectors-native-recurrence.md) and [Workflow actions and triggers](../logic-apps/logic-apps-workflow-actions-triggers.md#recurrence-trigger).</span></span>

5. <span data-ttu-id="aa946-199">To hide the trigger's details for now, click inside the shape's title bar.</span><span class="sxs-lookup"><span data-stu-id="aa946-199">To hide the trigger's details for now, click inside the shape's title bar.</span></span>

   ![Collapse shape to hide details](./media/tutorial-build-scheduled-recurring-logic-app-workflow/collapse-trigger-shape.png)

6. <span data-ttu-id="aa946-201">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-201">Save your logic app.</span></span> <span data-ttu-id="aa946-202">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa946-202">On the designer toolbar, choose **Save**.</span></span> 

<span data-ttu-id="aa946-203">Your logic app is now live but doesn't do anything other recur.</span><span class="sxs-lookup"><span data-stu-id="aa946-203">Your logic app is now live but doesn't do anything other recur.</span></span> <span data-ttu-id="aa946-204">So, add an action that responds when the trigger fires.</span><span class="sxs-lookup"><span data-stu-id="aa946-204">So, add an action that responds when the trigger fires.</span></span>

## <a name="get-the-travel-time-for-a-route"></a><span data-ttu-id="aa946-205">Get the travel time for a route</span><span class="sxs-lookup"><span data-stu-id="aa946-205">Get the travel time for a route</span></span>

<span data-ttu-id="aa946-206">Now that you have a trigger, add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that gets the travel time between two places.</span><span class="sxs-lookup"><span data-stu-id="aa946-206">Now that you have a trigger, add an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) that gets the travel time between two places.</span></span> <span data-ttu-id="aa946-207">Logic Apps provides a connector for the Bing Maps API so that you can easily get this information.</span><span class="sxs-lookup"><span data-stu-id="aa946-207">Logic Apps provides a connector for the Bing Maps API so that you can easily get this information.</span></span> <span data-ttu-id="aa946-208">Before you start this task, make sure that you have a Bing Maps API key as described in this tutorial's prerequisites.</span><span class="sxs-lookup"><span data-stu-id="aa946-208">Before you start this task, make sure that you have a Bing Maps API key as described in this tutorial's prerequisites.</span></span>

1. <span data-ttu-id="aa946-209">In the Logic App Designer, under your trigger, choose **+ New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="aa946-209">In the Logic App Designer, under your trigger, choose **+ New step** > **Add an action**.</span></span>

2. <span data-ttu-id="aa946-210">Search for "maps", and select this action: **Bing Maps - Get route**</span><span class="sxs-lookup"><span data-stu-id="aa946-210">Search for "maps", and select this action: **Bing Maps - Get route**</span></span>

3. <span data-ttu-id="aa946-211">If you don't have a Bing Maps connection, you're asked to create a connection.</span><span class="sxs-lookup"><span data-stu-id="aa946-211">If you don't have a Bing Maps connection, you're asked to create a connection.</span></span> <span data-ttu-id="aa946-212">Provide these connection details, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa946-212">Provide these connection details, and choose **Create**.</span></span>

   ![Select "Bing Maps - Get route" action](./media/tutorial-build-scheduled-recurring-logic-app-workflow/create-maps-connection.png)

   | <span data-ttu-id="aa946-214">Setting</span><span class="sxs-lookup"><span data-stu-id="aa946-214">Setting</span></span> | <span data-ttu-id="aa946-215">Value</span><span class="sxs-lookup"><span data-stu-id="aa946-215">Value</span></span> | <span data-ttu-id="aa946-216">Description</span><span class="sxs-lookup"><span data-stu-id="aa946-216">Description</span></span> |
   | ------- | ----- | ----------- |
   | <span data-ttu-id="aa946-217">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="aa946-217">**Connection Name**</span></span> | <span data-ttu-id="aa946-218">BingMapsConnection</span><span class="sxs-lookup"><span data-stu-id="aa946-218">BingMapsConnection</span></span> | <span data-ttu-id="aa946-219">Provide a name for your connection.</span><span class="sxs-lookup"><span data-stu-id="aa946-219">Provide a name for your connection.</span></span> | 
   | <span data-ttu-id="aa946-220">**API Key**</span><span class="sxs-lookup"><span data-stu-id="aa946-220">**API Key**</span></span> | <span data-ttu-id="aa946-221"><*your-Bing-Maps-key*></span><span class="sxs-lookup"><span data-stu-id="aa946-221"><*your-Bing-Maps-key*></span></span> | <span data-ttu-id="aa946-222">Enter the Bing Maps key that you previously received.</span><span class="sxs-lookup"><span data-stu-id="aa946-222">Enter the Bing Maps key that you previously received.</span></span> <span data-ttu-id="aa946-223">If you don't have a Bing Maps key, learn <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">how to get a key</a>.</span><span class="sxs-lookup"><span data-stu-id="aa946-223">If you don't have a Bing Maps key, learn <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">how to get a key</a>.</span></span> | 
   | | | |  

4. <span data-ttu-id="aa946-224">Rename the action with this description: ```Get route and travel time with traffic```</span><span class="sxs-lookup"><span data-stu-id="aa946-224">Rename the action with this description: ```Get route and travel time with traffic```</span></span>

5. <span data-ttu-id="aa946-225">Provide details for the **Get route** action as shown and described here, for example:</span><span class="sxs-lookup"><span data-stu-id="aa946-225">Provide details for the **Get route** action as shown and described here, for example:</span></span>

   ![Provide information for "Bing Maps - Get route" action](./media/tutorial-build-scheduled-recurring-logic-app-workflow/get-route-action-settings.png) 

   | <span data-ttu-id="aa946-227">Setting</span><span class="sxs-lookup"><span data-stu-id="aa946-227">Setting</span></span> | <span data-ttu-id="aa946-228">Value</span><span class="sxs-lookup"><span data-stu-id="aa946-228">Value</span></span> | <span data-ttu-id="aa946-229">Description</span><span class="sxs-lookup"><span data-stu-id="aa946-229">Description</span></span> |
   | ------- | ----- | ----------- |
   | <span data-ttu-id="aa946-230">**Waypoint 1**</span><span class="sxs-lookup"><span data-stu-id="aa946-230">**Waypoint 1**</span></span> | <span data-ttu-id="aa946-231"><*start-location*></span><span class="sxs-lookup"><span data-stu-id="aa946-231"><*start-location*></span></span> | <span data-ttu-id="aa946-232">Your route's origin</span><span class="sxs-lookup"><span data-stu-id="aa946-232">Your route's origin</span></span> | 
   | <span data-ttu-id="aa946-233">**Waypoint 2**</span><span class="sxs-lookup"><span data-stu-id="aa946-233">**Waypoint 2**</span></span> | <span data-ttu-id="aa946-234"><*end-location*></span><span class="sxs-lookup"><span data-stu-id="aa946-234"><*end-location*></span></span> | <span data-ttu-id="aa946-235">Your route's destination</span><span class="sxs-lookup"><span data-stu-id="aa946-235">Your route's destination</span></span> | 
   | <span data-ttu-id="aa946-236">**Avoid**</span><span class="sxs-lookup"><span data-stu-id="aa946-236">**Avoid**</span></span> | <span data-ttu-id="aa946-237">None</span><span class="sxs-lookup"><span data-stu-id="aa946-237">None</span></span> | <span data-ttu-id="aa946-238">Any items to avoid on your route, such as highways, tolls, and so on</span><span class="sxs-lookup"><span data-stu-id="aa946-238">Any items to avoid on your route, such as highways, tolls, and so on</span></span> | 
   | <span data-ttu-id="aa946-239">**Optimize**</span><span class="sxs-lookup"><span data-stu-id="aa946-239">**Optimize**</span></span> | <span data-ttu-id="aa946-240">timeWithTraffic</span><span class="sxs-lookup"><span data-stu-id="aa946-240">timeWithTraffic</span></span> | <span data-ttu-id="aa946-241">A parameter to optimize your route, such as distance, travel time with current traffic, and so on.</span><span class="sxs-lookup"><span data-stu-id="aa946-241">A parameter to optimize your route, such as distance, travel time with current traffic, and so on.</span></span> <span data-ttu-id="aa946-242">Select this parameter: "timeWithTraffic"</span><span class="sxs-lookup"><span data-stu-id="aa946-242">Select this parameter: "timeWithTraffic"</span></span> | 
   | <span data-ttu-id="aa946-243">**Distance unit**</span><span class="sxs-lookup"><span data-stu-id="aa946-243">**Distance unit**</span></span> | <span data-ttu-id="aa946-244"><*your-preference*></span><span class="sxs-lookup"><span data-stu-id="aa946-244"><*your-preference*></span></span> | <span data-ttu-id="aa946-245">The unit of distance for your route.</span><span class="sxs-lookup"><span data-stu-id="aa946-245">The unit of distance for your route.</span></span> <span data-ttu-id="aa946-246">This article uses this unit: "Mile"</span><span class="sxs-lookup"><span data-stu-id="aa946-246">This article uses this unit: "Mile"</span></span>  | 
   | <span data-ttu-id="aa946-247">**Travel mode**</span><span class="sxs-lookup"><span data-stu-id="aa946-247">**Travel mode**</span></span> | <span data-ttu-id="aa946-248">Driving</span><span class="sxs-lookup"><span data-stu-id="aa946-248">Driving</span></span> | <span data-ttu-id="aa946-249">The travel mode for your route.</span><span class="sxs-lookup"><span data-stu-id="aa946-249">The travel mode for your route.</span></span> <span data-ttu-id="aa946-250">Select this mode: "Driving"</span><span class="sxs-lookup"><span data-stu-id="aa946-250">Select this mode: "Driving"</span></span> | 
   | <span data-ttu-id="aa946-251">**Transit Date-Time**</span><span class="sxs-lookup"><span data-stu-id="aa946-251">**Transit Date-Time**</span></span> | <span data-ttu-id="aa946-252">None</span><span class="sxs-lookup"><span data-stu-id="aa946-252">None</span></span> | <span data-ttu-id="aa946-253">Applies to transit mode only</span><span class="sxs-lookup"><span data-stu-id="aa946-253">Applies to transit mode only</span></span> | 
   | <span data-ttu-id="aa946-254">**Date-Time Type**</span><span class="sxs-lookup"><span data-stu-id="aa946-254">**Date-Time Type**</span></span> | <span data-ttu-id="aa946-255">None</span><span class="sxs-lookup"><span data-stu-id="aa946-255">None</span></span> | <span data-ttu-id="aa946-256">Applies to transit mode only</span><span class="sxs-lookup"><span data-stu-id="aa946-256">Applies to transit mode only</span></span> | 
   |||| 

   <span data-ttu-id="aa946-257">For more information about these parameters, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa946-257">For more information about these parameters, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span></span>

6. <span data-ttu-id="aa946-258">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-258">Save your logic app.</span></span>

<span data-ttu-id="aa946-259">Next, create a variable so that you can convert and store the current travel time as minutes, rather than seconds.</span><span class="sxs-lookup"><span data-stu-id="aa946-259">Next, create a variable so that you can convert and store the current travel time as minutes, rather than seconds.</span></span> <span data-ttu-id="aa946-260">That way, you can avoid repeating the conversion and use the value more easily in later steps.</span><span class="sxs-lookup"><span data-stu-id="aa946-260">That way, you can avoid repeating the conversion and use the value more easily in later steps.</span></span> 

## <a name="create-variable-to-store-travel-time"></a><span data-ttu-id="aa946-261">Create variable to store travel time</span><span class="sxs-lookup"><span data-stu-id="aa946-261">Create variable to store travel time</span></span>

<span data-ttu-id="aa946-262">Sometimes, you might want to perform operations on data in your workflow and use the results in later actions.</span><span class="sxs-lookup"><span data-stu-id="aa946-262">Sometimes, you might want to perform operations on data in your workflow and use the results in later actions.</span></span> <span data-ttu-id="aa946-263">To save these results so that you can easily reuse or reference them, you can create variables to store those results after processing them.</span><span class="sxs-lookup"><span data-stu-id="aa946-263">To save these results so that you can easily reuse or reference them, you can create variables to store those results after processing them.</span></span> <span data-ttu-id="aa946-264">You can create variables only at the top level in your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-264">You can create variables only at the top level in your logic app.</span></span>

<span data-ttu-id="aa946-265">By default, the previous **Get route** action returns the current travel time with traffic in seconds through the **Travel Duration Traffic** field.</span><span class="sxs-lookup"><span data-stu-id="aa946-265">By default, the previous **Get route** action returns the current travel time with traffic in seconds through the **Travel Duration Traffic** field.</span></span> <span data-ttu-id="aa946-266">By converting and storing this value as minutes instead, you make the value easier to reuse later without converting again.</span><span class="sxs-lookup"><span data-stu-id="aa946-266">By converting and storing this value as minutes instead, you make the value easier to reuse later without converting again.</span></span>

1. <span data-ttu-id="aa946-267">Under the **Get route** action, choose **+ New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="aa946-267">Under the **Get route** action, choose **+ New step** > **Add an action**.</span></span>

2. <span data-ttu-id="aa946-268">Search for "variables", and select this action: **Variables - Initialize variable**</span><span class="sxs-lookup"><span data-stu-id="aa946-268">Search for "variables", and select this action: **Variables - Initialize variable**</span></span>

   ![Select "Variables - Initialize variable" action](./media/tutorial-build-scheduled-recurring-logic-app-workflow/select-initialize-variable-action.png)

3. <span data-ttu-id="aa946-270">Rename this action with this description: ```Create variable to store travel time```</span><span class="sxs-lookup"><span data-stu-id="aa946-270">Rename this action with this description: ```Create variable to store travel time```</span></span>

4. <span data-ttu-id="aa946-271">Provide the details for your variable as described here:</span><span class="sxs-lookup"><span data-stu-id="aa946-271">Provide the details for your variable as described here:</span></span>

   | <span data-ttu-id="aa946-272">Setting</span><span class="sxs-lookup"><span data-stu-id="aa946-272">Setting</span></span> | <span data-ttu-id="aa946-273">Value</span><span class="sxs-lookup"><span data-stu-id="aa946-273">Value</span></span> | <span data-ttu-id="aa946-274">Description</span><span class="sxs-lookup"><span data-stu-id="aa946-274">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="aa946-275">**Name**</span><span class="sxs-lookup"><span data-stu-id="aa946-275">**Name**</span></span> | <span data-ttu-id="aa946-276">travelTime</span><span class="sxs-lookup"><span data-stu-id="aa946-276">travelTime</span></span> | <span data-ttu-id="aa946-277">The name for your variable</span><span class="sxs-lookup"><span data-stu-id="aa946-277">The name for your variable</span></span> | 
   | <span data-ttu-id="aa946-278">**Type**</span><span class="sxs-lookup"><span data-stu-id="aa946-278">**Type**</span></span> | <span data-ttu-id="aa946-279">Integer</span><span class="sxs-lookup"><span data-stu-id="aa946-279">Integer</span></span> | <span data-ttu-id="aa946-280">The data type for your variable</span><span class="sxs-lookup"><span data-stu-id="aa946-280">The data type for your variable</span></span> | 
   | <span data-ttu-id="aa946-281">**Value**</span><span class="sxs-lookup"><span data-stu-id="aa946-281">**Value**</span></span> | <span data-ttu-id="aa946-282">An expression that converts the current travel time from seconds to minutes (see steps under this table).</span><span class="sxs-lookup"><span data-stu-id="aa946-282">An expression that converts the current travel time from seconds to minutes (see steps under this table).</span></span> | <span data-ttu-id="aa946-283">The initial value for your variable</span><span class="sxs-lookup"><span data-stu-id="aa946-283">The initial value for your variable</span></span> | 
   |||| 

   1. <span data-ttu-id="aa946-284">To create the expression for the **Value** field, click inside the field so that the dynamic content list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-284">To create the expression for the **Value** field, click inside the field so that the dynamic content list appears.</span></span> 
   <span data-ttu-id="aa946-285">If necessary, widen your browser until the list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-285">If necessary, widen your browser until the list appears.</span></span> 
   <span data-ttu-id="aa946-286">In the dynamic content list, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="aa946-286">In the dynamic content list, choose **Expression**.</span></span> 

      ![Provide information for "Variables - Initialize variable" action](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings.png)

      <span data-ttu-id="aa946-288">When you click inside some edit boxes, either a dynamic content list or an inline parameter list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-288">When you click inside some edit boxes, either a dynamic content list or an inline parameter list appears.</span></span> <span data-ttu-id="aa946-289">This list shows any parameters from previous actions that you can use as inputs in your workflow.</span><span class="sxs-lookup"><span data-stu-id="aa946-289">This list shows any parameters from previous actions that you can use as inputs in your workflow.</span></span> 
      <span data-ttu-id="aa946-290">The dynamic content list has an expression editor where you can select functions for performing operations.</span><span class="sxs-lookup"><span data-stu-id="aa946-290">The dynamic content list has an expression editor where you can select functions for performing operations.</span></span> 
      <span data-ttu-id="aa946-291">This expression editor appears only in the dynamic content list.</span><span class="sxs-lookup"><span data-stu-id="aa946-291">This expression editor appears only in the dynamic content list.</span></span>

      <span data-ttu-id="aa946-292">Your browser width determines which list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-292">Your browser width determines which list appears.</span></span> 
      <span data-ttu-id="aa946-293">If your browser is wide, the dynamic content list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-293">If your browser is wide, the dynamic content list appears.</span></span> 
      <span data-ttu-id="aa946-294">If your browser is narrow, a parameter list appears inline under the edit box that currently has focus.</span><span class="sxs-lookup"><span data-stu-id="aa946-294">If your browser is narrow, a parameter list appears inline under the edit box that currently has focus.</span></span>

   2. <span data-ttu-id="aa946-295">In the expression editor, enter this expression: ```div(,60)```</span><span class="sxs-lookup"><span data-stu-id="aa946-295">In the expression editor, enter this expression: ```div(,60)```</span></span>

      ![Enter this expression: "div(,60)"](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings-2.png)

   3. <span data-ttu-id="aa946-297">Put your cursor inside the expression between the left parenthesis (**(**) and the comma (**,**).</span><span class="sxs-lookup"><span data-stu-id="aa946-297">Put your cursor inside the expression between the left parenthesis (**(**) and the comma (**,**).</span></span> 
   <span data-ttu-id="aa946-298">Choose **Dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="aa946-298">Choose **Dynamic content**.</span></span>

      ![Position cursor, choose "Dynamic content"](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings-3.png)

   4. <span data-ttu-id="aa946-300">In the dynamic content list, select **Travel Duration Traffic**.</span><span class="sxs-lookup"><span data-stu-id="aa946-300">In the dynamic content list, select **Travel Duration Traffic**.</span></span>

      ![Select "Travel Duration Traffic" field](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings-4.png)

   5. <span data-ttu-id="aa946-302">After the field resolves inside the expression, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="aa946-302">After the field resolves inside the expression, choose **OK**.</span></span>

      ![Choose "OK"](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings-5.png)

      <span data-ttu-id="aa946-304">The **Value** field now appears as shown here:</span><span class="sxs-lookup"><span data-stu-id="aa946-304">The **Value** field now appears as shown here:</span></span>

      !["Value" field with resolved expression](./media/tutorial-build-scheduled-recurring-logic-app-workflow/initialize-variable-action-settings-6.png)

5. <span data-ttu-id="aa946-306">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-306">Save your logic app.</span></span>

<span data-ttu-id="aa946-307">Next, add a condition that checks whether the current travel time is greater than a specific limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-307">Next, add a condition that checks whether the current travel time is greater than a specific limit.</span></span>

## <a name="compare-travel-time-with-limit"></a><span data-ttu-id="aa946-308">Compare travel time with limit</span><span class="sxs-lookup"><span data-stu-id="aa946-308">Compare travel time with limit</span></span>

1. <span data-ttu-id="aa946-309">Under the previous action, choose **+ New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="aa946-309">Under the previous action, choose **+ New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="aa946-310">Rename the condition with this description: ```If travel time exceeds limit```</span><span class="sxs-lookup"><span data-stu-id="aa946-310">Rename the condition with this description: ```If travel time exceeds limit```</span></span>

3. <span data-ttu-id="aa946-311">Build a condition that checks whether **travelTime** exceeds your specified limit as described and shown here:</span><span class="sxs-lookup"><span data-stu-id="aa946-311">Build a condition that checks whether **travelTime** exceeds your specified limit as described and shown here:</span></span>

   1. <span data-ttu-id="aa946-312">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span><span class="sxs-lookup"><span data-stu-id="aa946-312">Inside the condition, click inside the **Choose a value** box, which is on the left (wide browser view) or on top (narrow browser view).</span></span>

   2. <span data-ttu-id="aa946-313">From either the dynamic content list or the parameter list, select the **travelTime** field under **Variables**.</span><span class="sxs-lookup"><span data-stu-id="aa946-313">From either the dynamic content list or the parameter list, select the **travelTime** field under **Variables**.</span></span>

   3. <span data-ttu-id="aa946-314">In the comparison box, select this operator: **is greater than**</span><span class="sxs-lookup"><span data-stu-id="aa946-314">In the comparison box, select this operator: **is greater than**</span></span>

   4. <span data-ttu-id="aa946-315">In the **Choose a value** box on the right (wide view) or bottom (narrow view), enter this limit: ```15```</span><span class="sxs-lookup"><span data-stu-id="aa946-315">In the **Choose a value** box on the right (wide view) or bottom (narrow view), enter this limit: ```15```</span></span>

   <span data-ttu-id="aa946-316">For example, if you're working in narrow view, here is how you build this condition:</span><span class="sxs-lookup"><span data-stu-id="aa946-316">For example, if you're working in narrow view, here is how you build this condition:</span></span>

   ![Build condition in narrow view](./media/tutorial-build-scheduled-recurring-logic-app-workflow/build-condition-check-travel-time-narrow.png)

4. <span data-ttu-id="aa946-318">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-318">Save your logic app.</span></span>

<span data-ttu-id="aa946-319">Next, add the action to perform when the travel time exceeds your limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-319">Next, add the action to perform when the travel time exceeds your limit.</span></span>

## <a name="send-email-when-limit-exceeded"></a><span data-ttu-id="aa946-320">Send email when limit exceeded</span><span class="sxs-lookup"><span data-stu-id="aa946-320">Send email when limit exceeded</span></span>

<span data-ttu-id="aa946-321">Now, add an action that emails you when the travel time exceeds your limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-321">Now, add an action that emails you when the travel time exceeds your limit.</span></span> <span data-ttu-id="aa946-322">This email includes the current travel time and the extra time necessary to travel the specified route.</span><span class="sxs-lookup"><span data-stu-id="aa946-322">This email includes the current travel time and the extra time necessary to travel the specified route.</span></span> 

1. <span data-ttu-id="aa946-323">In the condition's **If true** branch, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="aa946-323">In the condition's **If true** branch, choose **Add an action**.</span></span>

2. <span data-ttu-id="aa946-324">Search for "send email", and select the email connector and the "send email action" that you want to use.</span><span class="sxs-lookup"><span data-stu-id="aa946-324">Search for "send email", and select the email connector and the "send email action" that you want to use.</span></span>

   ![Find and select "send email" action](./media/tutorial-build-scheduled-recurring-logic-app-workflow/add-action-send-email.png)

   * <span data-ttu-id="aa946-326">For personal Microsoft accounts, select **Outlook.com**.</span><span class="sxs-lookup"><span data-stu-id="aa946-326">For personal Microsoft accounts, select **Outlook.com**.</span></span> 
   * <span data-ttu-id="aa946-327">For Azure work or school accounts, select **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="aa946-327">For Azure work or school accounts, select **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="aa946-328">If you don't already have a connection, you're asked to sign in to your email account.</span><span class="sxs-lookup"><span data-stu-id="aa946-328">If you don't already have a connection, you're asked to sign in to your email account.</span></span>

   <span data-ttu-id="aa946-329">Logic Apps creates a connection to your email account.</span><span class="sxs-lookup"><span data-stu-id="aa946-329">Logic Apps creates a connection to your email account.</span></span>

4. <span data-ttu-id="aa946-330">Rename the action with this description: ```Send email with travel time```</span><span class="sxs-lookup"><span data-stu-id="aa946-330">Rename the action with this description: ```Send email with travel time```</span></span>

5. <span data-ttu-id="aa946-331">In the **To** box, enter the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="aa946-331">In the **To** box, enter the recipient's email address.</span></span> <span data-ttu-id="aa946-332">For testing purposes, use your email address.</span><span class="sxs-lookup"><span data-stu-id="aa946-332">For testing purposes, use your email address.</span></span>

6. <span data-ttu-id="aa946-333">In the **Subject** box, specify the email's subject, and include the **travelTime** variable.</span><span class="sxs-lookup"><span data-stu-id="aa946-333">In the **Subject** box, specify the email's subject, and include the **travelTime** variable.</span></span>

   1. <span data-ttu-id="aa946-334">Enter the text ```Current travel time (minutes): ``` with a trailing space.</span><span class="sxs-lookup"><span data-stu-id="aa946-334">Enter the text ```Current travel time (minutes): ``` with a trailing space.</span></span> 
   
   2. <span data-ttu-id="aa946-335">From either the parameter list or the dynamic content list, select **travelTime** under **Variables**.</span><span class="sxs-lookup"><span data-stu-id="aa946-335">From either the parameter list or the dynamic content list, select **travelTime** under **Variables**.</span></span> 
   
      <span data-ttu-id="aa946-336">For example, if your browser is in narrow view:</span><span class="sxs-lookup"><span data-stu-id="aa946-336">For example, if your browser is in narrow view:</span></span>

      ![Enter subject text and expression that returns the travel time](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-subject-settings.png)

7. <span data-ttu-id="aa946-338">In the **Body** box, specify the content for the email body.</span><span class="sxs-lookup"><span data-stu-id="aa946-338">In the **Body** box, specify the content for the email body.</span></span> 

   1. <span data-ttu-id="aa946-339">Enter the text ```Add extra travel time (minutes): ``` with a trailing space.</span><span class="sxs-lookup"><span data-stu-id="aa946-339">Enter the text ```Add extra travel time (minutes): ``` with a trailing space.</span></span> 
   
   2. <span data-ttu-id="aa946-340">If necessary, widen your browser until the dynamic content list appears.</span><span class="sxs-lookup"><span data-stu-id="aa946-340">If necessary, widen your browser until the dynamic content list appears.</span></span> 
   <span data-ttu-id="aa946-341">In the dynamic content list, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="aa946-341">In the dynamic content list, choose **Expression**.</span></span>

      ![Build expression for email body](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings.png)

   3. <span data-ttu-id="aa946-343">In the expression editor, enter this expression so that you can calculate the number of minutes that exceed your limit: ```sub(,15)```</span><span class="sxs-lookup"><span data-stu-id="aa946-343">In the expression editor, enter this expression so that you can calculate the number of minutes that exceed your limit: ```sub(,15)```</span></span>

      ![Enter expression to calculate extra minutes travel time](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings-2.png)

   4. <span data-ttu-id="aa946-345">Put your cursor inside the expression between the left parenthesis (**(**) and the comma (**,**).</span><span class="sxs-lookup"><span data-stu-id="aa946-345">Put your cursor inside the expression between the left parenthesis (**(**) and the comma (**,**).</span></span> <span data-ttu-id="aa946-346">Choose **Dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="aa946-346">Choose **Dynamic content**.</span></span>

      ![Continue building expression to calculate extra minutes travel time](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings-3.png)

   5. <span data-ttu-id="aa946-348">Under **Variables**, select **travelTime**.</span><span class="sxs-lookup"><span data-stu-id="aa946-348">Under **Variables**, select **travelTime**.</span></span>

      ![Select "travelTime" field to use in expression](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings-4.png)

   6. <span data-ttu-id="aa946-350">After the field resolves inside the expression, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="aa946-350">After the field resolves inside the expression, choose **OK**.</span></span>

      !["Body" field with resolved expression](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings-5.png)

      <span data-ttu-id="aa946-352">The **Body** field now appears as shown here:</span><span class="sxs-lookup"><span data-stu-id="aa946-352">The **Body** field now appears as shown here:</span></span>

      !["Body" field with resolved expression](./media/tutorial-build-scheduled-recurring-logic-app-workflow/send-email-body-settings-6.png)

8. <span data-ttu-id="aa946-354">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-354">Save your logic app.</span></span>

<span data-ttu-id="aa946-355">Next, test your logic app, which now looks similar to this example:</span><span class="sxs-lookup"><span data-stu-id="aa946-355">Next, test your logic app, which now looks similar to this example:</span></span>

![Finished logic app](./media/tutorial-build-scheduled-recurring-logic-app-workflow/check-travel-time-finished.png)

## <a name="run-your-logic-app"></a><span data-ttu-id="aa946-357">Run your logic app</span><span class="sxs-lookup"><span data-stu-id="aa946-357">Run your logic app</span></span>

<span data-ttu-id="aa946-358">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="aa946-358">To manually start your logic app, on the designer toolbar bar, choose **Run**.</span></span> <span data-ttu-id="aa946-359">If the current travel time stays under your limit, your logic app does nothing else and waits for the next interval before checking again.</span><span class="sxs-lookup"><span data-stu-id="aa946-359">If the current travel time stays under your limit, your logic app does nothing else and waits for the next interval before checking again.</span></span>
<span data-ttu-id="aa946-360">But if the current travel time exceeds your limit, you get an email with the current travel time and the number of minutes above your limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-360">But if the current travel time exceeds your limit, you get an email with the current travel time and the number of minutes above your limit.</span></span> <span data-ttu-id="aa946-361">Here is an example email that your logic app sends:</span><span class="sxs-lookup"><span data-stu-id="aa946-361">Here is an example email that your logic app sends:</span></span>

![Email sent with travel time](./media/tutorial-build-scheduled-recurring-logic-app-workflow/email-notification.png)

<span data-ttu-id="aa946-363">If you don't get any emails, check your email's junk folder.</span><span class="sxs-lookup"><span data-stu-id="aa946-363">If you don't get any emails, check your email's junk folder.</span></span> <span data-ttu-id="aa946-364">Your email junk filter might redirect these kinds of mails.</span><span class="sxs-lookup"><span data-stu-id="aa946-364">Your email junk filter might redirect these kinds of mails.</span></span> <span data-ttu-id="aa946-365">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="aa946-365">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

<span data-ttu-id="aa946-366">Congratulations, you've now created and run a schedule-based recurring logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-366">Congratulations, you've now created and run a schedule-based recurring logic app.</span></span> 

<span data-ttu-id="aa946-367">To create other logic apps that use the **Schedule - Recurrence** trigger, check out these templates, which available after you create a logic app:</span><span class="sxs-lookup"><span data-stu-id="aa946-367">To create other logic apps that use the **Schedule - Recurrence** trigger, check out these templates, which available after you create a logic app:</span></span>

* <span data-ttu-id="aa946-368">Get daily reminders sent to you.</span><span class="sxs-lookup"><span data-stu-id="aa946-368">Get daily reminders sent to you.</span></span>
* <span data-ttu-id="aa946-369">Delete older Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="aa946-369">Delete older Azure blobs.</span></span>
* <span data-ttu-id="aa946-370">Add a message to an Azure Storage queue.</span><span class="sxs-lookup"><span data-stu-id="aa946-370">Add a message to an Azure Storage queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="aa946-371">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="aa946-371">Clean up resources</span></span>

<span data-ttu-id="aa946-372">When no longer needed, delete the resource group that contains your logic app and related resources.</span><span class="sxs-lookup"><span data-stu-id="aa946-372">When no longer needed, delete the resource group that contains your logic app and related resources.</span></span> <span data-ttu-id="aa946-373">On the main Azure menu, go to **Resource groups**, and select the resource group for your logic app.</span><span class="sxs-lookup"><span data-stu-id="aa946-373">On the main Azure menu, go to **Resource groups**, and select the resource group for your logic app.</span></span> <span data-ttu-id="aa946-374">Choose **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="aa946-374">Choose **Delete resource group**.</span></span> <span data-ttu-id="aa946-375">Enter the resource group name as confirmation, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="aa946-375">Enter the resource group name as confirmation, and choose **Delete**.</span></span>

!["Overview" > "Delete resource group"](./media/tutorial-build-scheduled-recurring-logic-app-workflow/delete-resource-group.png)

## <a name="get-support"></a><span data-ttu-id="aa946-377">Get support</span><span class="sxs-lookup"><span data-stu-id="aa946-377">Get support</span></span>

* <span data-ttu-id="aa946-378">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="aa946-378">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="aa946-379">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="aa946-379">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa946-380">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa946-380">Next steps</span></span>

<span data-ttu-id="aa946-381">In this tutorial, you created a logic app that checks traffic based on a specified schedule (on weekday mornings), and takes action (sends email) when the travel time exceeds a specified limit.</span><span class="sxs-lookup"><span data-stu-id="aa946-381">In this tutorial, you created a logic app that checks traffic based on a specified schedule (on weekday mornings), and takes action (sends email) when the travel time exceeds a specified limit.</span></span> <span data-ttu-id="aa946-382">Now, learn how to build a logic app that sends mailing list requests for approval by integrating Azure services, Microsoft services, and other SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="aa946-382">Now, learn how to build a logic app that sends mailing list requests for approval by integrating Azure services, Microsoft services, and other SaaS apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa946-383">Manage mailing list requests</span><span class="sxs-lookup"><span data-stu-id="aa946-383">Manage mailing list requests</span></span>](../logic-apps/tutorial-process-mailing-list-subscriptions-workflow.md)
