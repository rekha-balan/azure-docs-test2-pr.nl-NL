---
title: Add scopes that run actions based on group status - Azure Logic Apps | Microsoft Docs
description: How to create scopes that run workflow actions based on group action status in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.date: 03/05/2018
ms.topic: article
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 1258175eb3d28d39be8be08498ba8d2e0998aa43
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865512"
---
# <a name="create-scopes-that-run-workflow-actions-based-on-group-status-in-azure-logic-apps"></a><span data-ttu-id="415e5-103">Create scopes that run workflow actions based on group status in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="415e5-103">Create scopes that run workflow actions based on group status in Azure Logic Apps</span></span>

<span data-ttu-id="415e5-104">To run actions only after another group of actions succeed or fail, group those actions inside a *scope*.</span><span class="sxs-lookup"><span data-stu-id="415e5-104">To run actions only after another group of actions succeed or fail, group those actions inside a *scope*.</span></span> <span data-ttu-id="415e5-105">This structure is useful when you want to organize actions as a logical group, evaluate that group's status, and perform actions that are based on the scope's status.</span><span class="sxs-lookup"><span data-stu-id="415e5-105">This structure is useful when you want to organize actions as a logical group, evaluate that group's status, and perform actions that are based on the scope's status.</span></span> <span data-ttu-id="415e5-106">After all the actions in a scope finish running, the scope also gets its own status.</span><span class="sxs-lookup"><span data-stu-id="415e5-106">After all the actions in a scope finish running, the scope also gets its own status.</span></span> <span data-ttu-id="415e5-107">For example, you can use scopes when you want to implement [exception and error handling](../logic-apps/logic-apps-exception-handling.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="415e5-107">For example, you can use scopes when you want to implement [exception and error handling](../logic-apps/logic-apps-exception-handling.md#scopes).</span></span> 

<span data-ttu-id="415e5-108">To check a scope's status, you can use the same criteria that you use to determine a logic apps' run status, such as "Succeeded", "Failed", "Cancelled", and so on.</span><span class="sxs-lookup"><span data-stu-id="415e5-108">To check a scope's status, you can use the same criteria that you use to determine a logic apps' run status, such as "Succeeded", "Failed", "Cancelled", and so on.</span></span> <span data-ttu-id="415e5-109">By default, when all the scope's actions succeed, the scope's status is marked "Succeeded."</span><span class="sxs-lookup"><span data-stu-id="415e5-109">By default, when all the scope's actions succeed, the scope's status is marked "Succeeded."</span></span> <span data-ttu-id="415e5-110">But when any action in the scope fails or is canceled, the scope's status is marked "Failed."</span><span class="sxs-lookup"><span data-stu-id="415e5-110">But when any action in the scope fails or is canceled, the scope's status is marked "Failed."</span></span> <span data-ttu-id="415e5-111">For limits on scopes, see [Limits and config](../logic-apps/logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="415e5-111">For limits on scopes, see [Limits and config](../logic-apps/logic-apps-limits-and-config.md).</span></span> 

<span data-ttu-id="415e5-112">For example, here is a high-level logic app that uses a scope to run specific actions and a condition to check the scope's status.</span><span class="sxs-lookup"><span data-stu-id="415e5-112">For example, here is a high-level logic app that uses a scope to run specific actions and a condition to check the scope's status.</span></span> <span data-ttu-id="415e5-113">If any actions in the scope fail or end unexpectedly, the scope is marked "Failed" or "Aborted" respectively, and the logic app sends a "Scope failed" message.</span><span class="sxs-lookup"><span data-stu-id="415e5-113">If any actions in the scope fail or end unexpectedly, the scope is marked "Failed" or "Aborted" respectively, and the logic app sends a "Scope failed" message.</span></span> <span data-ttu-id="415e5-114">If all the scoped actions succeed, the logic app sends a "Scope succeeded" message.</span><span class="sxs-lookup"><span data-stu-id="415e5-114">If all the scoped actions succeed, the logic app sends a "Scope succeeded" message.</span></span>

![Set up "Schedule - Recurrence" trigger](./media/logic-apps-control-flow-run-steps-group-scopes/scope-high-level.png)

## <a name="prerequisites"></a><span data-ttu-id="415e5-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="415e5-116">Prerequisites</span></span>

<span data-ttu-id="415e5-117">To follow the example in this article, you need these items:</span><span class="sxs-lookup"><span data-stu-id="415e5-117">To follow the example in this article, you need these items:</span></span>

* <span data-ttu-id="415e5-118">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="415e5-118">An Azure subscription.</span></span> <span data-ttu-id="415e5-119">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="415e5-119">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span> 

* <span data-ttu-id="415e5-120">An email account from any email provider supported by Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="415e5-120">An email account from any email provider supported by Logic Apps.</span></span> <span data-ttu-id="415e5-121">This example uses Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="415e5-121">This example uses Outlook.com.</span></span> <span data-ttu-id="415e5-122">If you use a different provider, the general flow stays the same, but your UI appears different.</span><span class="sxs-lookup"><span data-stu-id="415e5-122">If you use a different provider, the general flow stays the same, but your UI appears different.</span></span>

* <span data-ttu-id="415e5-123">A Bing Maps key.</span><span class="sxs-lookup"><span data-stu-id="415e5-123">A Bing Maps key.</span></span> <span data-ttu-id="415e5-124">To get this key, see <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">Get a Bing Maps key</a>.</span><span class="sxs-lookup"><span data-stu-id="415e5-124">To get this key, see <a href="https://msdn.microsoft.com/library/ff428642.aspx" target="_blank">Get a Bing Maps key</a>.</span></span>

* <span data-ttu-id="415e5-125">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="415e5-125">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

## <a name="create-sample-logic-app"></a><span data-ttu-id="415e5-126">Create sample logic app</span><span class="sxs-lookup"><span data-stu-id="415e5-126">Create sample logic app</span></span>

<span data-ttu-id="415e5-127">First, create this sample logic app so that you can add a scope later:</span><span class="sxs-lookup"><span data-stu-id="415e5-127">First, create this sample logic app so that you can add a scope later:</span></span>

![Create sample logic app](./media/logic-apps-control-flow-run-steps-group-scopes/finished-sample-app.png)

* <span data-ttu-id="415e5-129">A **Schedule - Recurrence** trigger that checks the Bing Maps service at an interval that you specify</span><span class="sxs-lookup"><span data-stu-id="415e5-129">A **Schedule - Recurrence** trigger that checks the Bing Maps service at an interval that you specify</span></span>
* <span data-ttu-id="415e5-130">A **Bing Maps - Get route** action that checks the travel time between two locations</span><span class="sxs-lookup"><span data-stu-id="415e5-130">A **Bing Maps - Get route** action that checks the travel time between two locations</span></span>
* <span data-ttu-id="415e5-131">A conditional statement that checks whether the travel time exceeds your specified travel time</span><span class="sxs-lookup"><span data-stu-id="415e5-131">A conditional statement that checks whether the travel time exceeds your specified travel time</span></span>
* <span data-ttu-id="415e5-132">An action that sends you email that current travel time exceeds your specified time</span><span class="sxs-lookup"><span data-stu-id="415e5-132">An action that sends you email that current travel time exceeds your specified time</span></span>

<span data-ttu-id="415e5-133">You can save your logic app at any time, so save your work often.</span><span class="sxs-lookup"><span data-stu-id="415e5-133">You can save your logic app at any time, so save your work often.</span></span>

1. <span data-ttu-id="415e5-134">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="415e5-134">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, if you haven't already.</span></span> <span data-ttu-id="415e5-135">Create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="415e5-135">Create a blank logic app.</span></span>

2. <span data-ttu-id="415e5-136">Add the **Schedule - Recurrence** trigger with these settings: **Interval** = "1" and **Frequency** = "Minute"</span><span class="sxs-lookup"><span data-stu-id="415e5-136">Add the **Schedule - Recurrence** trigger with these settings: **Interval** = "1" and **Frequency** = "Minute"</span></span>

   ![Set up "Schedule - Recurrence" trigger](./media/logic-apps-control-flow-run-steps-group-scopes/recurrence.png)

   > [!TIP]
   > <span data-ttu-id="415e5-138">To visually simplify your view and hide each action's details in the designer, collapse each action's shape as you progress through these steps.</span><span class="sxs-lookup"><span data-stu-id="415e5-138">To visually simplify your view and hide each action's details in the designer, collapse each action's shape as you progress through these steps.</span></span>

3. <span data-ttu-id="415e5-139">Add the **Bing Maps - Get route** action.</span><span class="sxs-lookup"><span data-stu-id="415e5-139">Add the **Bing Maps - Get route** action.</span></span> 

   1. <span data-ttu-id="415e5-140">If you don't already have a Bing Maps connection, you're asked to create a connection.</span><span class="sxs-lookup"><span data-stu-id="415e5-140">If you don't already have a Bing Maps connection, you're asked to create a connection.</span></span>

      | <span data-ttu-id="415e5-141">Setting</span><span class="sxs-lookup"><span data-stu-id="415e5-141">Setting</span></span> | <span data-ttu-id="415e5-142">Value</span><span class="sxs-lookup"><span data-stu-id="415e5-142">Value</span></span> | <span data-ttu-id="415e5-143">Description</span><span class="sxs-lookup"><span data-stu-id="415e5-143">Description</span></span> |
      | ------- | ----- | ----------- |
      | <span data-ttu-id="415e5-144">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="415e5-144">**Connection Name**</span></span> | <span data-ttu-id="415e5-145">BingMapsConnection</span><span class="sxs-lookup"><span data-stu-id="415e5-145">BingMapsConnection</span></span> | <span data-ttu-id="415e5-146">Provide a name for your connection.</span><span class="sxs-lookup"><span data-stu-id="415e5-146">Provide a name for your connection.</span></span> | 
      | <span data-ttu-id="415e5-147">**API Key**</span><span class="sxs-lookup"><span data-stu-id="415e5-147">**API Key**</span></span> | <span data-ttu-id="415e5-148"><*your-Bing-Maps-key*></span><span class="sxs-lookup"><span data-stu-id="415e5-148"><*your-Bing-Maps-key*></span></span> | <span data-ttu-id="415e5-149">Enter the Bing Maps key that you previously received.</span><span class="sxs-lookup"><span data-stu-id="415e5-149">Enter the Bing Maps key that you previously received.</span></span> | 
      ||||  

   2. <span data-ttu-id="415e5-150">Set up your **Get route** action as shown the table below this image:</span><span class="sxs-lookup"><span data-stu-id="415e5-150">Set up your **Get route** action as shown the table below this image:</span></span>

      ![Set up "Bing Maps - Get route" action](./media/logic-apps-control-flow-run-steps-group-scopes/get-route.png) 

      <span data-ttu-id="415e5-152">For more information about these parameters, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span><span class="sxs-lookup"><span data-stu-id="415e5-152">For more information about these parameters, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span></span>

      | <span data-ttu-id="415e5-153">Setting</span><span class="sxs-lookup"><span data-stu-id="415e5-153">Setting</span></span> | <span data-ttu-id="415e5-154">Value</span><span class="sxs-lookup"><span data-stu-id="415e5-154">Value</span></span> | <span data-ttu-id="415e5-155">Description</span><span class="sxs-lookup"><span data-stu-id="415e5-155">Description</span></span> |
      | ------- | ----- | ----------- |
      | <span data-ttu-id="415e5-156">**Waypoint 1**</span><span class="sxs-lookup"><span data-stu-id="415e5-156">**Waypoint 1**</span></span> | <span data-ttu-id="415e5-157"><*start*></span><span class="sxs-lookup"><span data-stu-id="415e5-157"><*start*></span></span> | <span data-ttu-id="415e5-158">Enter your route's origin.</span><span class="sxs-lookup"><span data-stu-id="415e5-158">Enter your route's origin.</span></span> | 
      | <span data-ttu-id="415e5-159">**Waypoint 2**</span><span class="sxs-lookup"><span data-stu-id="415e5-159">**Waypoint 2**</span></span> | <span data-ttu-id="415e5-160"><*end*></span><span class="sxs-lookup"><span data-stu-id="415e5-160"><*end*></span></span> | <span data-ttu-id="415e5-161">Enter your route's destination.</span><span class="sxs-lookup"><span data-stu-id="415e5-161">Enter your route's destination.</span></span> | 
      | <span data-ttu-id="415e5-162">**Avoid**</span><span class="sxs-lookup"><span data-stu-id="415e5-162">**Avoid**</span></span> | <span data-ttu-id="415e5-163">None</span><span class="sxs-lookup"><span data-stu-id="415e5-163">None</span></span> | <span data-ttu-id="415e5-164">Enter items to avoid on your route, such as highways, tolls, and so on.</span><span class="sxs-lookup"><span data-stu-id="415e5-164">Enter items to avoid on your route, such as highways, tolls, and so on.</span></span> <span data-ttu-id="415e5-165">For possible values, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span><span class="sxs-lookup"><span data-stu-id="415e5-165">For possible values, see [Calculate a route](https://msdn.microsoft.com/library/ff701717.aspx).</span></span> | 
      | <span data-ttu-id="415e5-166">**Optimize**</span><span class="sxs-lookup"><span data-stu-id="415e5-166">**Optimize**</span></span> | <span data-ttu-id="415e5-167">timeWithTraffic</span><span class="sxs-lookup"><span data-stu-id="415e5-167">timeWithTraffic</span></span> | <span data-ttu-id="415e5-168">Select a parameter to optimize your route, such as distance, time with current traffic information, and so on.</span><span class="sxs-lookup"><span data-stu-id="415e5-168">Select a parameter to optimize your route, such as distance, time with current traffic information, and so on.</span></span> <span data-ttu-id="415e5-169">This example uses this value: "timeWithTraffic"</span><span class="sxs-lookup"><span data-stu-id="415e5-169">This example uses this value: "timeWithTraffic"</span></span> | 
      | <span data-ttu-id="415e5-170">**Distance unit**</span><span class="sxs-lookup"><span data-stu-id="415e5-170">**Distance unit**</span></span> | <span data-ttu-id="415e5-171"><*your-preference*></span><span class="sxs-lookup"><span data-stu-id="415e5-171"><*your-preference*></span></span> | <span data-ttu-id="415e5-172">Enter the unit of distance to calculate your route.</span><span class="sxs-lookup"><span data-stu-id="415e5-172">Enter the unit of distance to calculate your route.</span></span> <span data-ttu-id="415e5-173">This example uses this value: "Mile"</span><span class="sxs-lookup"><span data-stu-id="415e5-173">This example uses this value: "Mile"</span></span> | 
      | <span data-ttu-id="415e5-174">**Travel mode**</span><span class="sxs-lookup"><span data-stu-id="415e5-174">**Travel mode**</span></span> | <span data-ttu-id="415e5-175">Driving</span><span class="sxs-lookup"><span data-stu-id="415e5-175">Driving</span></span> | <span data-ttu-id="415e5-176">Enter the mode of travel for your route.</span><span class="sxs-lookup"><span data-stu-id="415e5-176">Enter the mode of travel for your route.</span></span> <span data-ttu-id="415e5-177">This example uses this value "Driving"</span><span class="sxs-lookup"><span data-stu-id="415e5-177">This example uses this value "Driving"</span></span> | 
      | <span data-ttu-id="415e5-178">**Transit Date-Time**</span><span class="sxs-lookup"><span data-stu-id="415e5-178">**Transit Date-Time**</span></span> | <span data-ttu-id="415e5-179">None</span><span class="sxs-lookup"><span data-stu-id="415e5-179">None</span></span> | <span data-ttu-id="415e5-180">Applies to transit mode only.</span><span class="sxs-lookup"><span data-stu-id="415e5-180">Applies to transit mode only.</span></span> | 
      | <span data-ttu-id="415e5-181">**Transit Date-Type Type**</span><span class="sxs-lookup"><span data-stu-id="415e5-181">**Transit Date-Type Type**</span></span> | <span data-ttu-id="415e5-182">None</span><span class="sxs-lookup"><span data-stu-id="415e5-182">None</span></span> | <span data-ttu-id="415e5-183">Applies to transit mode only.</span><span class="sxs-lookup"><span data-stu-id="415e5-183">Applies to transit mode only.</span></span> | 
      ||||  

4. <span data-ttu-id="415e5-184">Add a condition to heck whether the current travel time with traffic exceeds a specified time.</span><span class="sxs-lookup"><span data-stu-id="415e5-184">Add a condition to heck whether the current travel time with traffic exceeds a specified time.</span></span> <span data-ttu-id="415e5-185">For this example, follow the steps under this image:</span><span class="sxs-lookup"><span data-stu-id="415e5-185">For this example, follow the steps under this image:</span></span>

   ![Build condition](./media/logic-apps-control-flow-run-steps-group-scopes/build-condition.png)

   1. <span data-ttu-id="415e5-187">Rename the condition with this description: **If traffic time more than specified time**</span><span class="sxs-lookup"><span data-stu-id="415e5-187">Rename the condition with this description: **If traffic time more than specified time**</span></span>

   2. <span data-ttu-id="415e5-188">From the parameter list, select the **Travel Duration Traffic** field, which is in seconds.</span><span class="sxs-lookup"><span data-stu-id="415e5-188">From the parameter list, select the **Travel Duration Traffic** field, which is in seconds.</span></span> 

   3. <span data-ttu-id="415e5-189">For the comparison operator, select this operator: **is greater than**</span><span class="sxs-lookup"><span data-stu-id="415e5-189">For the comparison operator, select this operator: **is greater than**</span></span>

   4. <span data-ttu-id="415e5-190">For the comparison value, enter **600**, which is in seconds and equivalent to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="415e5-190">For the comparison value, enter **600**, which is in seconds and equivalent to 10 minutes.</span></span>

5. <span data-ttu-id="415e5-191">In the condition's **If true** branch, add a "send email" action for your email provider.</span><span class="sxs-lookup"><span data-stu-id="415e5-191">In the condition's **If true** branch, add a "send email" action for your email provider.</span></span> <span data-ttu-id="415e5-192">Set up this action with the details as shown in the table under this image:</span><span class="sxs-lookup"><span data-stu-id="415e5-192">Set up this action with the details as shown in the table under this image:</span></span>

   ![Add "Send an email" action to "If true" branch](./media/logic-apps-control-flow-run-steps-group-scopes/send-email.png)

   1. <span data-ttu-id="415e5-194">For the **To** field, enter your email address for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="415e5-194">For the **To** field, enter your email address for testing purposes.</span></span>

   2. <span data-ttu-id="415e5-195">For the **Subject** field, enter this text:</span><span class="sxs-lookup"><span data-stu-id="415e5-195">For the **Subject** field, enter this text:</span></span>

      ```Time to leave: Traffic more than 10 minutes```

   3. <span data-ttu-id="415e5-196">For the **Body** field, enter this text with a trailing space:</span><span class="sxs-lookup"><span data-stu-id="415e5-196">For the **Body** field, enter this text with a trailing space:</span></span> 

      ```Travel time: ```

      <span data-ttu-id="415e5-197">While your cursor appears in the **Body** field, the dynamic content list stays open so that you can select any parameters that are available at this point.</span><span class="sxs-lookup"><span data-stu-id="415e5-197">While your cursor appears in the **Body** field, the dynamic content list stays open so that you can select any parameters that are available at this point.</span></span>

   4. <span data-ttu-id="415e5-198">In the dynamic content list, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="415e5-198">In the dynamic content list, choose **Expression**.</span></span>

   5. <span data-ttu-id="415e5-199">Find and select the **div( )** function.</span><span class="sxs-lookup"><span data-stu-id="415e5-199">Find and select the **div( )** function.</span></span>

   6. <span data-ttu-id="415e5-200">While your cursor is inside the function's parentheses, choose **Dynamic content** so that you can add the **Traffic Duration Traffic** parameter next.</span><span class="sxs-lookup"><span data-stu-id="415e5-200">While your cursor is inside the function's parentheses, choose **Dynamic content** so that you can add the **Traffic Duration Traffic** parameter next.</span></span>

   7. <span data-ttu-id="415e5-201">Under **Get route** in the dynamic parameter list, select the **Traffic Duration Traffic** field.</span><span class="sxs-lookup"><span data-stu-id="415e5-201">Under **Get route** in the dynamic parameter list, select the **Traffic Duration Traffic** field.</span></span>

      ![Select "Traffic Duration Traffic"](./media/logic-apps-control-flow-run-steps-group-scopes/send-email-2.png)

   8. <span data-ttu-id="415e5-203">After the field resolves to JSON format, add a **comma** (```,```) followed by the number ```60``` so that you convert the value in **Traffic Duration Traffic** from seconds to minutes.</span><span class="sxs-lookup"><span data-stu-id="415e5-203">After the field resolves to JSON format, add a **comma** (```,```) followed by the number ```60``` so that you convert the value in **Traffic Duration Traffic** from seconds to minutes.</span></span> 
   
      ```
      div(body('Get_route')?['travelDurationTraffic'],60)
      ```

      <span data-ttu-id="415e5-204">Your expression now looks like this example:</span><span class="sxs-lookup"><span data-stu-id="415e5-204">Your expression now looks like this example:</span></span>

      ![Finish expression](./media/logic-apps-control-flow-run-steps-group-scopes/send-email-3.png)  

   9. <span data-ttu-id="415e5-206">Make sure that you choose **OK** when you're done.</span><span class="sxs-lookup"><span data-stu-id="415e5-206">Make sure that you choose **OK** when you're done.</span></span>

  10. <span data-ttu-id="415e5-207">After the expression resolves, add this text with a leading space: ``` minutes```</span><span class="sxs-lookup"><span data-stu-id="415e5-207">After the expression resolves, add this text with a leading space: ``` minutes```</span></span>
  
      <span data-ttu-id="415e5-208">Your **Body** field now looks like this example:</span><span class="sxs-lookup"><span data-stu-id="415e5-208">Your **Body** field now looks like this example:</span></span>

      ![Finished "Body" field](./media/logic-apps-control-flow-run-steps-group-scopes/send-email-4.png)

6. <span data-ttu-id="415e5-210">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="415e5-210">Save your logic app.</span></span>

<span data-ttu-id="415e5-211">Next, add a scope so that you can group specific actions and evaluate their status.</span><span class="sxs-lookup"><span data-stu-id="415e5-211">Next, add a scope so that you can group specific actions and evaluate their status.</span></span>

## <a name="add-a-scope"></a><span data-ttu-id="415e5-212">Add a scope</span><span class="sxs-lookup"><span data-stu-id="415e5-212">Add a scope</span></span>

1. <span data-ttu-id="415e5-213">If you haven't already, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="415e5-213">If you haven't already, open your logic app in Logic App Designer.</span></span> 

2. <span data-ttu-id="415e5-214">Add a scope at the workflow location that you want.</span><span class="sxs-lookup"><span data-stu-id="415e5-214">Add a scope at the workflow location that you want.</span></span> <span data-ttu-id="415e5-215">For example:</span><span class="sxs-lookup"><span data-stu-id="415e5-215">For example:</span></span>

   * <span data-ttu-id="415e5-216">To add a scope between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the scope.</span><span class="sxs-lookup"><span data-stu-id="415e5-216">To add a scope between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the scope.</span></span> 
   <span data-ttu-id="415e5-217">Choose the **plus sign** (**+**) > **Add a scope**.</span><span class="sxs-lookup"><span data-stu-id="415e5-217">Choose the **plus sign** (**+**) > **Add a scope**.</span></span>

     ![Add a scope](./media/logic-apps-control-flow-run-steps-group-scopes/add-scope.png)

     <span data-ttu-id="415e5-219">When you want to add a scope at the end of your workflow, at the bottom of your logic app, choose **+ New step** > **...More** > **Add a scope**.</span><span class="sxs-lookup"><span data-stu-id="415e5-219">When you want to add a scope at the end of your workflow, at the bottom of your logic app, choose **+ New step** > **...More** > **Add a scope**.</span></span>

3. <span data-ttu-id="415e5-220">Now add the steps or drag existing steps that you want to run inside the scope.</span><span class="sxs-lookup"><span data-stu-id="415e5-220">Now add the steps or drag existing steps that you want to run inside the scope.</span></span> <span data-ttu-id="415e5-221">For this example, drag these actions into the scope:</span><span class="sxs-lookup"><span data-stu-id="415e5-221">For this example, drag these actions into the scope:</span></span>
      
   * <span data-ttu-id="415e5-222">**Get route**</span><span class="sxs-lookup"><span data-stu-id="415e5-222">**Get route**</span></span>
   * <span data-ttu-id="415e5-223">**If traffic time more than specified time**,  which includes both the **true** and **false** branches</span><span class="sxs-lookup"><span data-stu-id="415e5-223">**If traffic time more than specified time**,  which includes both the **true** and **false** branches</span></span>

   <span data-ttu-id="415e5-224">Your logic app now looks like this example:</span><span class="sxs-lookup"><span data-stu-id="415e5-224">Your logic app now looks like this example:</span></span>

   ![Scope added](./media/logic-apps-control-flow-run-steps-group-scopes/scope-added.png)

4. <span data-ttu-id="415e5-226">Under the scope, add a condition that checks the scope's status.</span><span class="sxs-lookup"><span data-stu-id="415e5-226">Under the scope, add a condition that checks the scope's status.</span></span> <span data-ttu-id="415e5-227">Rename the condition with this description: **If scope failed**</span><span class="sxs-lookup"><span data-stu-id="415e5-227">Rename the condition with this description: **If scope failed**</span></span>

   ![Add condition to check scope status](./media/logic-apps-control-flow-run-steps-group-scopes/add-condition-check-scope-status.png)
  
5. <span data-ttu-id="415e5-229">Build this expression that checks whether the scope's status is equal to `Failed` or `Aborted`.</span><span class="sxs-lookup"><span data-stu-id="415e5-229">Build this expression that checks whether the scope's status is equal to `Failed` or `Aborted`.</span></span>

   ![Add expression that checks the scope's status](./media/logic-apps-control-flow-run-steps-group-scopes/build-expression-check-scope-status.png)

   <span data-ttu-id="415e5-231">Or, to enter this expression as text, choose **Edit in advanced mode**.</span><span class="sxs-lookup"><span data-stu-id="415e5-231">Or, to enter this expression as text, choose **Edit in advanced mode**.</span></span>

   ```@equals('@result(''Scope'')[0][''status'']', 'Failed, Aborted')```

6. <span data-ttu-id="415e5-232">In the **If true** and **If false** branches, add the actions that you want to perform, for example, send email or a message.</span><span class="sxs-lookup"><span data-stu-id="415e5-232">In the **If true** and **If false** branches, add the actions that you want to perform, for example, send email or a message.</span></span>

   ![Add expression that checks the scope's status](./media/logic-apps-control-flow-run-steps-group-scopes/handle-true-false-branches.png)

7. <span data-ttu-id="415e5-234">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="415e5-234">Save your logic app.</span></span>

<span data-ttu-id="415e5-235">Your finished logic app now looks like this example with all the shapes expanded:</span><span class="sxs-lookup"><span data-stu-id="415e5-235">Your finished logic app now looks like this example with all the shapes expanded:</span></span>

![Finished logic app with scope](./media/logic-apps-control-flow-run-steps-group-scopes/scopes-overview.png)

## <a name="test-your-work"></a><span data-ttu-id="415e5-237">Test your work</span><span class="sxs-lookup"><span data-stu-id="415e5-237">Test your work</span></span>

<span data-ttu-id="415e5-238">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="415e5-238">On the designer toolbar, choose **Run**.</span></span> <span data-ttu-id="415e5-239">If all the scoped actions succeed, you get a "Scope succeeded" message.</span><span class="sxs-lookup"><span data-stu-id="415e5-239">If all the scoped actions succeed, you get a "Scope succeeded" message.</span></span> <span data-ttu-id="415e5-240">If any scoped actions don't succeed, you get a "Scope failed" message.</span><span class="sxs-lookup"><span data-stu-id="415e5-240">If any scoped actions don't succeed, you get a "Scope failed" message.</span></span> 

<a name="scopes-json"></a>

## <a name="json-definition"></a><span data-ttu-id="415e5-241">JSON definition</span><span class="sxs-lookup"><span data-stu-id="415e5-241">JSON definition</span></span>

<span data-ttu-id="415e5-242">If you're working in code view, you can define a scope structure in your logic app's JSON definition instead.</span><span class="sxs-lookup"><span data-stu-id="415e5-242">If you're working in code view, you can define a scope structure in your logic app's JSON definition instead.</span></span> <span data-ttu-id="415e5-243">For example, here is the JSON definition for trigger and actions in the previous logic app:</span><span class="sxs-lookup"><span data-stu-id="415e5-243">For example, here is the JSON definition for trigger and actions in the previous logic app:</span></span>

``` json
"triggers": {
  "Recurrence": {
    "type": "Recurrence",
    "recurrence": {
       "frequency": "Minute",
       "interval": 1
    },
  }
}
```

```json
"actions": {
  "If_scope_failed": {
    "type": "If",
    "actions": {
      "Scope_failed": {
        "type": "ApiConnection",
        "inputs": {
          "body": {
            "Body": "Scope failed",
            "Subject": "Scope failed",
            "To": "<your-email@domain.com>"
          },
          "host": {
            "connection": {
              "name": "@parameters('$connections')['outlook']['connectionId']"
            }
          },
          "method": "post",
          "path": "/Mail"
        },
        "runAfter": {}
      }
    },
    "else": {
      "actions": {
        "Scope_succeded": {
          "type": "ApiConnection",
          "inputs": {
            "body": {
              "Body": "None",
              "Subject": "Scope succeeded",
              "To": "<your-email@domain.com>"
            },
            "host": {
              "connection": {
               "name": "@parameters('$connections')['outlook']['connectionId']"
              }
            },
            "method": "post",
            "path": "/Mail"
          },
          "runAfter": {}
        }
      }
    },
    "expression": "@equals('@result(''Scope'')[0][''status'']', 'Failed, Aborted')",
    "runAfter": {
      "Scope": [
        "Succeeded"
      ]
    }
  },
  "Scope": {
    "type": "Scope",
    "actions": {
      "Get_route": {
        "type": "ApiConnection",
        "inputs": {
          "host": {
            "connection": {
              "name": "@parameters('$connections')['bingmaps']['connectionId']"
            }
          },
          "method": "get",
          "path": "/REST/V1/Routes/Driving",
          "queries": {
            "distanceUnit": "Mile",
            "optimize": "timeWithTraffic",
            "travelMode": "Driving",
            "wp.0": "<start>",
            "wp.1": "<end>"
          }
        },
        "runAfter": {}
      },
      "If_traffic_time_more_than_specified_time": {
        "type": "If",
        "actions": {
          "Send_mail_when_traffic_exceeds_10_minutes": {
            "type": "ApiConnection",
            "inputs": {
              "body": {
                 "Body": "Travel time:@{div(body('Get_route')?['travelDurationTraffic'], 60)} minutes",
                 "Subject": "Time to leave: Traffic more than 10 minutes",
                 "To": "<your-email@domain.com>"
              },
              "host": {
                "connection": {
                   "name": "@parameters('$connections')['outlook']['connectionId']"
                }
              },
              "method": "post",
              "path": "/Mail"
            },
            "runAfter": {}
          }
        },
        "expression": "@greater(body('Get_route')?['travelDurationTraffic'], 600)",
        "runAfter": {
          "Get_route": [
            "Succeeded"
          ]
        }
      }
    },
    "runAfter": {}
  }
}
```

## <a name="get-support"></a><span data-ttu-id="415e5-244">Get support</span><span class="sxs-lookup"><span data-stu-id="415e5-244">Get support</span></span>

* <span data-ttu-id="415e5-245">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="415e5-245">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="415e5-246">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="415e5-246">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="415e5-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="415e5-247">Next steps</span></span>

* [<span data-ttu-id="415e5-248">Run steps based on a condition (conditional statements)</span><span class="sxs-lookup"><span data-stu-id="415e5-248">Run steps based on a condition (conditional statements)</span></span>](../logic-apps/logic-apps-control-flow-conditional-statement.md)
* [<span data-ttu-id="415e5-249">Run steps based on different values (switch statements)</span><span class="sxs-lookup"><span data-stu-id="415e5-249">Run steps based on different values (switch statements)</span></span>](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [<span data-ttu-id="415e5-250">Run and repeat steps (loops)</span><span class="sxs-lookup"><span data-stu-id="415e5-250">Run and repeat steps (loops)</span></span>](../logic-apps/logic-apps-control-flow-loops.md)
* [<span data-ttu-id="415e5-251">Run or merge parallel steps (branches)</span><span class="sxs-lookup"><span data-stu-id="415e5-251">Run or merge parallel steps (branches)</span></span>](../logic-apps/logic-apps-control-flow-branches.md)
