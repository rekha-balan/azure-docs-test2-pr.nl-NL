---
title: Add loops that repeat actions or process arrays - Azure Logic Apps | Microsoft Docs
description: How to create loops that repeat workflow actions or process arrays in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.date: 03/05/2018
ms.topic: article
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 87595eeb0330a2d8210258c097c29b205b628cf4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866620"
---
# <a name="create-loops-that-repeat-workflow-actions-or-process-arrays-in-azure-logic-apps"></a><span data-ttu-id="4366e-103">Create loops that repeat workflow actions or process arrays in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4366e-103">Create loops that repeat workflow actions or process arrays in Azure Logic Apps</span></span>

<span data-ttu-id="4366e-104">To iterate through arrays in your logic app, you can use a ["Foreach" loop](#foreach-loop) or a [sequential "Foreach" loop](#sequential-foreach-loop).</span><span class="sxs-lookup"><span data-stu-id="4366e-104">To iterate through arrays in your logic app, you can use a ["Foreach" loop](#foreach-loop) or a [sequential "Foreach" loop](#sequential-foreach-loop).</span></span> <span data-ttu-id="4366e-105">The iterations for a standard "Foreach" loop run in parallel, while the iterations for a sequential "Foreach" loop run one at a time.</span><span class="sxs-lookup"><span data-stu-id="4366e-105">The iterations for a standard "Foreach" loop run in parallel, while the iterations for a sequential "Foreach" loop run one at a time.</span></span> <span data-ttu-id="4366e-106">For the maximum number of array items that "Foreach" loops can process in a single logic app run, see [Limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="4366e-106">For the maximum number of array items that "Foreach" loops can process in a single logic app run, see [Limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span></span> 

> [!TIP] 
> <span data-ttu-id="4366e-107">If you have a trigger that receives an array and want to run a workflow for each array item, you can *debatch* that array with the [**SplitOn** trigger property](../logic-apps/logic-apps-workflow-actions-triggers.md#split-on-debatch).</span><span class="sxs-lookup"><span data-stu-id="4366e-107">If you have a trigger that receives an array and want to run a workflow for each array item, you can *debatch* that array with the [**SplitOn** trigger property](../logic-apps/logic-apps-workflow-actions-triggers.md#split-on-debatch).</span></span> 
  
<span data-ttu-id="4366e-108">To repeat actions until a condition is met or some state has changed, use an ["Until" loop](#until-loop).</span><span class="sxs-lookup"><span data-stu-id="4366e-108">To repeat actions until a condition is met or some state has changed, use an ["Until" loop](#until-loop).</span></span> <span data-ttu-id="4366e-109">Your logic app first performs all the actions inside the loop and then checks the condition as the last step.</span><span class="sxs-lookup"><span data-stu-id="4366e-109">Your logic app first performs all the actions inside the loop and then checks the condition as the last step.</span></span> <span data-ttu-id="4366e-110">If the condition is met, the loop stops.</span><span class="sxs-lookup"><span data-stu-id="4366e-110">If the condition is met, the loop stops.</span></span> <span data-ttu-id="4366e-111">Otherwise, the loop repeats.</span><span class="sxs-lookup"><span data-stu-id="4366e-111">Otherwise, the loop repeats.</span></span> <span data-ttu-id="4366e-112">For the maximum number of "Until" loops in a single logic app run, see [Limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="4366e-112">For the maximum number of "Until" loops in a single logic app run, see [Limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4366e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4366e-113">Prerequisites</span></span>

* <span data-ttu-id="4366e-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4366e-114">An Azure subscription.</span></span> <span data-ttu-id="4366e-115">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4366e-115">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span> 

* <span data-ttu-id="4366e-116">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="4366e-116">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

<a name="foreach-loop"></a>

## <a name="foreach-loop"></a><span data-ttu-id="4366e-117">"Foreach" loop</span><span class="sxs-lookup"><span data-stu-id="4366e-117">"Foreach" loop</span></span>

<span data-ttu-id="4366e-118">To repeat actions for each item in an array, use a "Foreach" loop in your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="4366e-118">To repeat actions for each item in an array, use a "Foreach" loop in your logic app workflow.</span></span> <span data-ttu-id="4366e-119">You can include multiple actions in a "Foreach" loop, and you can nest "Foreach" loops inside each other.</span><span class="sxs-lookup"><span data-stu-id="4366e-119">You can include multiple actions in a "Foreach" loop, and you can nest "Foreach" loops inside each other.</span></span> <span data-ttu-id="4366e-120">By default, cycles in a standard "Foreach" loop run in parallel.</span><span class="sxs-lookup"><span data-stu-id="4366e-120">By default, cycles in a standard "Foreach" loop run in parallel.</span></span> <span data-ttu-id="4366e-121">For the maximum number of parallel cycles that "Foreach" loops can run, see [Limits and config](../logic-apps/logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="4366e-121">For the maximum number of parallel cycles that "Foreach" loops can run, see [Limits and config](../logic-apps/logic-apps-limits-and-config.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="4366e-122">A "Foreach" loop works only with an array, and actions in the loop use the `@item()` reference to process each item in the array.</span><span class="sxs-lookup"><span data-stu-id="4366e-122">A "Foreach" loop works only with an array, and actions in the loop use the `@item()` reference to process each item in the array.</span></span> <span data-ttu-id="4366e-123">If you specify data that's not in an array, the logic app workflow fails.</span><span class="sxs-lookup"><span data-stu-id="4366e-123">If you specify data that's not in an array, the logic app workflow fails.</span></span> 

<span data-ttu-id="4366e-124">For example, this logic app sends you a daily summary from a website's RSS feed.</span><span class="sxs-lookup"><span data-stu-id="4366e-124">For example, this logic app sends you a daily summary from a website's RSS feed.</span></span> <span data-ttu-id="4366e-125">The app uses a "Foreach" loop that sends an email for each new item found.</span><span class="sxs-lookup"><span data-stu-id="4366e-125">The app uses a "Foreach" loop that sends an email for each new item found.</span></span>

1. <span data-ttu-id="4366e-126">[Create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="4366e-126">[Create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span></span>

2. <span data-ttu-id="4366e-127">Between the RSS trigger and send email action, add a "Foreach" loop.</span><span class="sxs-lookup"><span data-stu-id="4366e-127">Between the RSS trigger and send email action, add a "Foreach" loop.</span></span> 

   <span data-ttu-id="4366e-128">To add a loop between steps, move the pointer over the arrow where you want to add the loop.</span><span class="sxs-lookup"><span data-stu-id="4366e-128">To add a loop between steps, move the pointer over the arrow where you want to add the loop.</span></span> 
   <span data-ttu-id="4366e-129">Choose the **plus sign** (**+**) that appears, then choose **Add a for each**.</span><span class="sxs-lookup"><span data-stu-id="4366e-129">Choose the **plus sign** (**+**) that appears, then choose **Add a for each**.</span></span>

   ![Add a "Foreach" loop between steps](media/logic-apps-control-flow-loops/add-for-each-loop.png)

3. <span data-ttu-id="4366e-131">Now build the loop.</span><span class="sxs-lookup"><span data-stu-id="4366e-131">Now build the loop.</span></span> <span data-ttu-id="4366e-132">Under **Select an output from previous steps** after the **Add dynamic content** list appears, select the **Feed links** array, which is output from the RSS trigger.</span><span class="sxs-lookup"><span data-stu-id="4366e-132">Under **Select an output from previous steps** after the **Add dynamic content** list appears, select the **Feed links** array, which is output from the RSS trigger.</span></span> 

   ![Select from dynamic content list](media/logic-apps-control-flow-loops/for-each-loop-dynamic-content-list.png)

   > [!NOTE] 
   > <span data-ttu-id="4366e-134">You can select *only* array outputs from the previous step.</span><span class="sxs-lookup"><span data-stu-id="4366e-134">You can select *only* array outputs from the previous step.</span></span>

   <span data-ttu-id="4366e-135">The selected array now appears here:</span><span class="sxs-lookup"><span data-stu-id="4366e-135">The selected array now appears here:</span></span>

   ![Select array](media/logic-apps-control-flow-loops/for-each-loop-select-array.png)

4. <span data-ttu-id="4366e-137">To perform an action on each array item, drag the **Send an email** action into the **For each** loop.</span><span class="sxs-lookup"><span data-stu-id="4366e-137">To perform an action on each array item, drag the **Send an email** action into the **For each** loop.</span></span> 

   <span data-ttu-id="4366e-138">Your logic app might look something like this example:</span><span class="sxs-lookup"><span data-stu-id="4366e-138">Your logic app might look something like this example:</span></span>

   ![Add steps to "Foreach" loop](media/logic-apps-control-flow-loops/for-each-loop-with-step.png)

5. <span data-ttu-id="4366e-140">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="4366e-140">Save your logic app.</span></span> <span data-ttu-id="4366e-141">To manually test your logic app, on the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="4366e-141">To manually test your logic app, on the designer toolbar, choose **Run**.</span></span>

<a name="for-each-json"></a>

## <a name="foreach-loop-definition-json"></a><span data-ttu-id="4366e-142">"Foreach" loop definition (JSON)</span><span class="sxs-lookup"><span data-stu-id="4366e-142">"Foreach" loop definition (JSON)</span></span>

<span data-ttu-id="4366e-143">If you're working in code view for your logic app, you can define the `Foreach` loop in your logic app's JSON definition instead, for example:</span><span class="sxs-lookup"><span data-stu-id="4366e-143">If you're working in code view for your logic app, you can define the `Foreach` loop in your logic app's JSON definition instead, for example:</span></span>

``` json
"actions": {
    "myForEachLoopName": {
        "type": "Foreach",
        "actions": {
            "Send_an_email": {
                "type": "ApiConnection",
                "inputs": {
                    "body": {
                        "Body": "@{item()}",
                        "Subject": "New CNN post @{triggerBody()?['publishDate']}",
                        "To": "me@contoso.com"
                    },
                    "host": {
                        "api": {
                            "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/office365"
                        },
                        "connection": {
                            "name": "@parameters('$connections')['office365']['connectionId']"
                        }
                    },
                    "method": "post",
                    "path": "/Mail"
                },
                "runAfter": {}
            }
        },
        "foreach": "@triggerBody()?['links']",
        "runAfter": {},
    }
},
```

<a name="sequential-foreach-loop"></a>

## <a name="foreach-loop-sequential"></a><span data-ttu-id="4366e-144">"Foreach" loop: Sequential</span><span class="sxs-lookup"><span data-stu-id="4366e-144">"Foreach" loop: Sequential</span></span>

<span data-ttu-id="4366e-145">By default, each cycle in a "Foreach" loop runs in parallel for each array item.</span><span class="sxs-lookup"><span data-stu-id="4366e-145">By default, each cycle in a "Foreach" loop runs in parallel for each array item.</span></span> <span data-ttu-id="4366e-146">To run each cycle sequentially, set the **Sequential** option in your "Foreach" loop.</span><span class="sxs-lookup"><span data-stu-id="4366e-146">To run each cycle sequentially, set the **Sequential** option in your "Foreach" loop.</span></span>

1. <span data-ttu-id="4366e-147">In the loop's upper right corner, choose **ellipses** (**...**) > **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4366e-147">In the loop's upper right corner, choose **ellipses** (**...**) > **Settings**.</span></span>

   ![On "Foreach" loop, choose "..." > "Settings"](media/logic-apps-control-flow-loops/for-each-loop-settings.png)

2. <span data-ttu-id="4366e-149">Turn on the **Sequential** setting, then choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="4366e-149">Turn on the **Sequential** setting, then choose **Done**.</span></span>

   ![Turn on "Foreach" loop's Sequential setting](media/logic-apps-control-flow-loops/for-each-loop-sequential-setting.png)

<span data-ttu-id="4366e-151">You can also set the **operationOptions** parameter to `Sequential` in your logic app's JSON definition.</span><span class="sxs-lookup"><span data-stu-id="4366e-151">You can also set the **operationOptions** parameter to `Sequential` in your logic app's JSON definition.</span></span> <span data-ttu-id="4366e-152">For example:</span><span class="sxs-lookup"><span data-stu-id="4366e-152">For example:</span></span>

``` json
"actions": {
    "myForEachLoopName": {
        "type": "Foreach",
        "actions": {
            "Send_an_email": {               
            }
        },
        "foreach": "@triggerBody()?['links']",
        "runAfter": {},
        "operationOptions": "Sequential"
    }
},
```

<a name="until-loop"></a>

## <a name="until-loop"></a><span data-ttu-id="4366e-153">"Until" loop</span><span class="sxs-lookup"><span data-stu-id="4366e-153">"Until" loop</span></span>
  
<span data-ttu-id="4366e-154">To repeat actions until a condition is met or some state has changed, use an "Until" loop in your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="4366e-154">To repeat actions until a condition is met or some state has changed, use an "Until" loop in your logic app workflow.</span></span> <span data-ttu-id="4366e-155">Here are some common use cases where you can use an "Until" loop:</span><span class="sxs-lookup"><span data-stu-id="4366e-155">Here are some common use cases where you can use an "Until" loop:</span></span>

* <span data-ttu-id="4366e-156">Call an endpoint until you get the response that you want.</span><span class="sxs-lookup"><span data-stu-id="4366e-156">Call an endpoint until you get the response that you want.</span></span>
* <span data-ttu-id="4366e-157">Create a record in a database, wait until a specific field in that record gets approved, and continue processing.</span><span class="sxs-lookup"><span data-stu-id="4366e-157">Create a record in a database, wait until a specific field in that record gets approved, and continue processing.</span></span> 

<span data-ttu-id="4366e-158">For example, at 8:00 AM each day, this logic app increments a variable until the variable's value equals 10.</span><span class="sxs-lookup"><span data-stu-id="4366e-158">For example, at 8:00 AM each day, this logic app increments a variable until the variable's value equals 10.</span></span> <span data-ttu-id="4366e-159">Then, the logic app sends an email that confirms the current value.</span><span class="sxs-lookup"><span data-stu-id="4366e-159">Then, the logic app sends an email that confirms the current value.</span></span> <span data-ttu-id="4366e-160">Although this example uses Office 365 Outlook, you can use any email provider supported by Logic Apps ([review the connectors list here](https://docs.microsoft.com/connectors/)).</span><span class="sxs-lookup"><span data-stu-id="4366e-160">Although this example uses Office 365 Outlook, you can use any email provider supported by Logic Apps ([review the connectors list here](https://docs.microsoft.com/connectors/)).</span></span> <span data-ttu-id="4366e-161">If you use another email account, the overall steps are the same, but your UI might slightly differ.</span><span class="sxs-lookup"><span data-stu-id="4366e-161">If you use another email account, the overall steps are the same, but your UI might slightly differ.</span></span> 

1. <span data-ttu-id="4366e-162">Create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="4366e-162">Create a blank logic app.</span></span> <span data-ttu-id="4366e-163">In Logic App Designer, search for "recurrence", and select this trigger: **Schedule - Recurrence**</span><span class="sxs-lookup"><span data-stu-id="4366e-163">In Logic App Designer, search for "recurrence", and select this trigger: **Schedule - Recurrence**</span></span> 

   ![Add "Schedule - Recurrence" trigger](./media/logic-apps-control-flow-loops/do-until-loop-add-trigger.png)

2. <span data-ttu-id="4366e-165">Specify when the trigger fires by setting the interval, frequency, and hour of the day.</span><span class="sxs-lookup"><span data-stu-id="4366e-165">Specify when the trigger fires by setting the interval, frequency, and hour of the day.</span></span> <span data-ttu-id="4366e-166">To set the hour, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="4366e-166">To set the hour, choose **Show advanced options**.</span></span>

   ![Add "Schedule - Recurrence" trigger](./media/logic-apps-control-flow-loops/do-until-loop-set-trigger-properties.png)

   | <span data-ttu-id="4366e-168">Property</span><span class="sxs-lookup"><span data-stu-id="4366e-168">Property</span></span> | <span data-ttu-id="4366e-169">Value</span><span class="sxs-lookup"><span data-stu-id="4366e-169">Value</span></span> |
   | -------- | ----- |
   | <span data-ttu-id="4366e-170">**Interval**</span><span class="sxs-lookup"><span data-stu-id="4366e-170">**Interval**</span></span> | <span data-ttu-id="4366e-171">1</span><span class="sxs-lookup"><span data-stu-id="4366e-171">1</span></span> | 
   | <span data-ttu-id="4366e-172">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="4366e-172">**Frequency**</span></span> | <span data-ttu-id="4366e-173">Day</span><span class="sxs-lookup"><span data-stu-id="4366e-173">Day</span></span> |
   | <span data-ttu-id="4366e-174">**At these hours**</span><span class="sxs-lookup"><span data-stu-id="4366e-174">**At these hours**</span></span> | <span data-ttu-id="4366e-175">8</span><span class="sxs-lookup"><span data-stu-id="4366e-175">8</span></span> |
   ||| 

3. <span data-ttu-id="4366e-176">Under the trigger, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="4366e-176">Under the trigger, choose **New step** > **Add an action**.</span></span> <span data-ttu-id="4366e-177">Search for "variables", and then select this action: **Variables - Initialize variable**</span><span class="sxs-lookup"><span data-stu-id="4366e-177">Search for "variables", and then select this action: **Variables - Initialize variable**</span></span>

   ![Add "Variables - Initialize variable" action](./media/logic-apps-control-flow-loops/do-until-loop-add-variable.png)

4. <span data-ttu-id="4366e-179">Set up your variable with these values:</span><span class="sxs-lookup"><span data-stu-id="4366e-179">Set up your variable with these values:</span></span>

   ![Set variable properties](./media/logic-apps-control-flow-loops/do-until-loop-set-variable-properties.png)

   | <span data-ttu-id="4366e-181">Property</span><span class="sxs-lookup"><span data-stu-id="4366e-181">Property</span></span> | <span data-ttu-id="4366e-182">Value</span><span class="sxs-lookup"><span data-stu-id="4366e-182">Value</span></span> | <span data-ttu-id="4366e-183">Description</span><span class="sxs-lookup"><span data-stu-id="4366e-183">Description</span></span> |
   | -------- | ----- | ----------- |
   | <span data-ttu-id="4366e-184">**Name**</span><span class="sxs-lookup"><span data-stu-id="4366e-184">**Name**</span></span> | <span data-ttu-id="4366e-185">Limit</span><span class="sxs-lookup"><span data-stu-id="4366e-185">Limit</span></span> | <span data-ttu-id="4366e-186">Your variable's name</span><span class="sxs-lookup"><span data-stu-id="4366e-186">Your variable's name</span></span> | 
   | <span data-ttu-id="4366e-187">**Type**</span><span class="sxs-lookup"><span data-stu-id="4366e-187">**Type**</span></span> | <span data-ttu-id="4366e-188">Integer</span><span class="sxs-lookup"><span data-stu-id="4366e-188">Integer</span></span> | <span data-ttu-id="4366e-189">Your variable's data type</span><span class="sxs-lookup"><span data-stu-id="4366e-189">Your variable's data type</span></span> | 
   | <span data-ttu-id="4366e-190">**Value**</span><span class="sxs-lookup"><span data-stu-id="4366e-190">**Value**</span></span> | <span data-ttu-id="4366e-191">0</span><span class="sxs-lookup"><span data-stu-id="4366e-191">0</span></span> | <span data-ttu-id="4366e-192">Your variable's starting value</span><span class="sxs-lookup"><span data-stu-id="4366e-192">Your variable's starting value</span></span> | 
   |||| 

5. <span data-ttu-id="4366e-193">Under the **Initialize variable** action, choose **New step** > **More**.</span><span class="sxs-lookup"><span data-stu-id="4366e-193">Under the **Initialize variable** action, choose **New step** > **More**.</span></span> <span data-ttu-id="4366e-194">Select this loop: **Add a do until**</span><span class="sxs-lookup"><span data-stu-id="4366e-194">Select this loop: **Add a do until**</span></span>

   ![Add "do until" loop](./media/logic-apps-control-flow-loops/do-until-loop-add-until-loop.png)

6. <span data-ttu-id="4366e-196">Build the loop's exit condition by selecting the **Limit** variable and the **is equal** operator.</span><span class="sxs-lookup"><span data-stu-id="4366e-196">Build the loop's exit condition by selecting the **Limit** variable and the **is equal** operator.</span></span> <span data-ttu-id="4366e-197">Enter **10** as the comparison value.</span><span class="sxs-lookup"><span data-stu-id="4366e-197">Enter **10** as the comparison value.</span></span>

   ![Build exit condition for stopping loop](./media/logic-apps-control-flow-loops/do-until-loop-settings.png)

7. <span data-ttu-id="4366e-199">Inside the loop, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="4366e-199">Inside the loop, choose **Add an action**.</span></span> <span data-ttu-id="4366e-200">Search for "variables", and then add this action: **Variables - Increment variable**</span><span class="sxs-lookup"><span data-stu-id="4366e-200">Search for "variables", and then add this action: **Variables - Increment variable**</span></span>

   ![Add action for incrementing variable](./media/logic-apps-control-flow-loops/do-until-loop-increment-variable.png)

8. <span data-ttu-id="4366e-202">For **Name**, select the **Limit** variable.</span><span class="sxs-lookup"><span data-stu-id="4366e-202">For **Name**, select the **Limit** variable.</span></span> <span data-ttu-id="4366e-203">For **Value**, enter "1".</span><span class="sxs-lookup"><span data-stu-id="4366e-203">For **Value**, enter "1".</span></span> 

   ![Increment "Limit" by 1](./media/logic-apps-control-flow-loops/do-until-loop-increment-variable-settings.png)

9. <span data-ttu-id="4366e-205">Under but outside the loop, add an action that sends email.</span><span class="sxs-lookup"><span data-stu-id="4366e-205">Under but outside the loop, add an action that sends email.</span></span> <span data-ttu-id="4366e-206">If prompted, sign in to your email account.</span><span class="sxs-lookup"><span data-stu-id="4366e-206">If prompted, sign in to your email account.</span></span>

   ![Add action that sends email](media/logic-apps-control-flow-loops/do-until-loop-send-email.png)

10. <span data-ttu-id="4366e-208">Set the email's properties.</span><span class="sxs-lookup"><span data-stu-id="4366e-208">Set the email's properties.</span></span> <span data-ttu-id="4366e-209">Add the **Limit** variable to the subject.</span><span class="sxs-lookup"><span data-stu-id="4366e-209">Add the **Limit** variable to the subject.</span></span> <span data-ttu-id="4366e-210">That way, you can confirm the variable's current value meets your specified condition, for example:</span><span class="sxs-lookup"><span data-stu-id="4366e-210">That way, you can confirm the variable's current value meets your specified condition, for example:</span></span>

    ![Set up email properties](./media/logic-apps-control-flow-loops/do-until-loop-send-email-settings.png)

    | <span data-ttu-id="4366e-212">Property</span><span class="sxs-lookup"><span data-stu-id="4366e-212">Property</span></span> | <span data-ttu-id="4366e-213">Value</span><span class="sxs-lookup"><span data-stu-id="4366e-213">Value</span></span> | <span data-ttu-id="4366e-214">Description</span><span class="sxs-lookup"><span data-stu-id="4366e-214">Description</span></span> |
    | -------- | ----- | ----------- | 
    | <span data-ttu-id="4366e-215">**To**</span><span class="sxs-lookup"><span data-stu-id="4366e-215">**To**</span></span> | *<email-address@domain>* | <span data-ttu-id="4366e-216">The recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="4366e-216">The recipient's email address.</span></span> <span data-ttu-id="4366e-217">For testing, use your own email address.</span><span class="sxs-lookup"><span data-stu-id="4366e-217">For testing, use your own email address.</span></span> | 
    | <span data-ttu-id="4366e-218">**Subject**</span><span class="sxs-lookup"><span data-stu-id="4366e-218">**Subject**</span></span> | <span data-ttu-id="4366e-219">Current value for "Limit" is **Limit**</span><span class="sxs-lookup"><span data-stu-id="4366e-219">Current value for "Limit" is **Limit**</span></span> | <span data-ttu-id="4366e-220">Specify the email subject.</span><span class="sxs-lookup"><span data-stu-id="4366e-220">Specify the email subject.</span></span> <span data-ttu-id="4366e-221">For this example, make sure that you include the **Limit** variable.</span><span class="sxs-lookup"><span data-stu-id="4366e-221">For this example, make sure that you include the **Limit** variable.</span></span> | 
    | <span data-ttu-id="4366e-222">**Body**</span><span class="sxs-lookup"><span data-stu-id="4366e-222">**Body**</span></span> | <span data-ttu-id="4366e-223"><*email-content*></span><span class="sxs-lookup"><span data-stu-id="4366e-223"><*email-content*></span></span> | <span data-ttu-id="4366e-224">Specify the email message content you want to send.</span><span class="sxs-lookup"><span data-stu-id="4366e-224">Specify the email message content you want to send.</span></span> <span data-ttu-id="4366e-225">For this example, enter whatever text you like.</span><span class="sxs-lookup"><span data-stu-id="4366e-225">For this example, enter whatever text you like.</span></span> | 
    |||| 

11. <span data-ttu-id="4366e-226">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="4366e-226">Save your logic app.</span></span> <span data-ttu-id="4366e-227">To manually test your logic app, on the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="4366e-227">To manually test your logic app, on the designer toolbar, choose **Run**.</span></span>

    <span data-ttu-id="4366e-228">After your logic starts running, you get an email with the content that you specified:</span><span class="sxs-lookup"><span data-stu-id="4366e-228">After your logic starts running, you get an email with the content that you specified:</span></span>

    ![Received email](./media/logic-apps-control-flow-loops/do-until-loop-sent-email.png)

## <a name="prevent-endless-loops"></a><span data-ttu-id="4366e-230">Prevent endless loops</span><span class="sxs-lookup"><span data-stu-id="4366e-230">Prevent endless loops</span></span>

<span data-ttu-id="4366e-231">An "Until" loop has default limits that stop execution if any of these conditions happen:</span><span class="sxs-lookup"><span data-stu-id="4366e-231">An "Until" loop has default limits that stop execution if any of these conditions happen:</span></span>

| <span data-ttu-id="4366e-232">Property</span><span class="sxs-lookup"><span data-stu-id="4366e-232">Property</span></span> | <span data-ttu-id="4366e-233">Default value</span><span class="sxs-lookup"><span data-stu-id="4366e-233">Default value</span></span> | <span data-ttu-id="4366e-234">Description</span><span class="sxs-lookup"><span data-stu-id="4366e-234">Description</span></span> | 
| -------- | ------------- | ----------- | 
| <span data-ttu-id="4366e-235">**Count**</span><span class="sxs-lookup"><span data-stu-id="4366e-235">**Count**</span></span> | <span data-ttu-id="4366e-236">60</span><span class="sxs-lookup"><span data-stu-id="4366e-236">60</span></span> | <span data-ttu-id="4366e-237">The maximum number of loops that run before the loop exits.</span><span class="sxs-lookup"><span data-stu-id="4366e-237">The maximum number of loops that run before the loop exits.</span></span> <span data-ttu-id="4366e-238">The default is 60 cycles.</span><span class="sxs-lookup"><span data-stu-id="4366e-238">The default is 60 cycles.</span></span> | 
| <span data-ttu-id="4366e-239">**Timeout**</span><span class="sxs-lookup"><span data-stu-id="4366e-239">**Timeout**</span></span> | <span data-ttu-id="4366e-240">PT1H</span><span class="sxs-lookup"><span data-stu-id="4366e-240">PT1H</span></span> | <span data-ttu-id="4366e-241">The maximum amount of time to run a loop before the loop exits.</span><span class="sxs-lookup"><span data-stu-id="4366e-241">The maximum amount of time to run a loop before the loop exits.</span></span> <span data-ttu-id="4366e-242">The default is one hour and is specified in ISO 8601 format.</span><span class="sxs-lookup"><span data-stu-id="4366e-242">The default is one hour and is specified in ISO 8601 format.</span></span> <p><span data-ttu-id="4366e-243">The timeout value is evaluated for each loop cycle.</span><span class="sxs-lookup"><span data-stu-id="4366e-243">The timeout value is evaluated for each loop cycle.</span></span> <span data-ttu-id="4366e-244">If any action in the loop takes longer than the timeout limit, the current cycle doesn't stop, but the next cycle doesn't start because the limit condition isn't met.</span><span class="sxs-lookup"><span data-stu-id="4366e-244">If any action in the loop takes longer than the timeout limit, the current cycle doesn't stop, but the next cycle doesn't start because the limit condition isn't met.</span></span> | 
|||| 

<span data-ttu-id="4366e-245">To change these default limits, choose **Show advanced options** in the loop action shape.</span><span class="sxs-lookup"><span data-stu-id="4366e-245">To change these default limits, choose **Show advanced options** in the loop action shape.</span></span>

<a name="until-json"></a>

## <a name="until-definition-json"></a><span data-ttu-id="4366e-246">"Until" definition (JSON)</span><span class="sxs-lookup"><span data-stu-id="4366e-246">"Until" definition (JSON)</span></span>

<span data-ttu-id="4366e-247">If you're working in code view for your logic app, you can define an `Until` loop in your logic app's JSON definition instead, for example:</span><span class="sxs-lookup"><span data-stu-id="4366e-247">If you're working in code view for your logic app, you can define an `Until` loop in your logic app's JSON definition instead, for example:</span></span>

``` json
"actions": {
    "Initialize_variable": {
        // Definition for initialize variable action
    },
    "Send_an_email": {
        // Definition for send email action
    },
    "Until": {
        "type": "Until",
        "actions": {
            "Increment_variable": {
                "type": "IncrementVariable",
                "inputs": {
                    "name": "Limit",
                    "value": 1
                },
                "runAfter": {}
            }
        },
        "expression": "@equals(variables('Limit'), 10)",
        // To prevent endless loops, an "Until" loop 
        // includes these default limits that stop the loop. 
        "limit": { 
            "count": 60,
            "timeout": "PT1H"
        },
        "runAfter": {
            "Initialize_variable": [
                "Succeeded"
            ]
        },
    }
},
```

<span data-ttu-id="4366e-248">In another example, this "Until" loop calls an HTTP endpoint that creates a resource and stops when the HTTP response body returns with "Completed" status.</span><span class="sxs-lookup"><span data-stu-id="4366e-248">In another example, this "Until" loop calls an HTTP endpoint that creates a resource and stops when the HTTP response body returns with "Completed" status.</span></span> <span data-ttu-id="4366e-249">To prevent endless loops, the loop also stops if any of these conditions happen:</span><span class="sxs-lookup"><span data-stu-id="4366e-249">To prevent endless loops, the loop also stops if any of these conditions happen:</span></span>

* <span data-ttu-id="4366e-250">The loop has run 10 times as specified by the `count` attribute.</span><span class="sxs-lookup"><span data-stu-id="4366e-250">The loop has run 10 times as specified by the `count` attribute.</span></span> <span data-ttu-id="4366e-251">The default is 60 times.</span><span class="sxs-lookup"><span data-stu-id="4366e-251">The default is 60 times.</span></span> 
* <span data-ttu-id="4366e-252">The loop has tried to run for two hours as specified by the `timeout` attribute in ISO 8601 format.</span><span class="sxs-lookup"><span data-stu-id="4366e-252">The loop has tried to run for two hours as specified by the `timeout` attribute in ISO 8601 format.</span></span> <span data-ttu-id="4366e-253">The default is one hour.</span><span class="sxs-lookup"><span data-stu-id="4366e-253">The default is one hour.</span></span>
  
``` json
"actions": {
    "myUntilLoopName": {
        "type": "Until",
        "actions": {
            "Create_new_resource": {
                "type": "Http",
                "inputs": {
                    "body": {
                        "resourceId": "@triggerBody()"
                    },
                    "url": "https://domain.com/provisionResource/create-resource",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                },
                "runAfter": {},
                "type": "ApiConnection"
            }
        },
        "expression": "@equals(triggerBody(), 'Completed')",
        "limit": {
            "count": 10,
            "timeout": "PT2H"
        },
        "runAfter": {}
    }
},
```

## <a name="get-support"></a><span data-ttu-id="4366e-254">Get support</span><span class="sxs-lookup"><span data-stu-id="4366e-254">Get support</span></span>

* <span data-ttu-id="4366e-255">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="4366e-255">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="4366e-256">To submit or vote on features and suggestions, [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="4366e-256">To submit or vote on features and suggestions, [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4366e-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="4366e-257">Next steps</span></span>

* [<span data-ttu-id="4366e-258">Run steps based on a condition (conditional statements)</span><span class="sxs-lookup"><span data-stu-id="4366e-258">Run steps based on a condition (conditional statements)</span></span>](../logic-apps/logic-apps-control-flow-conditional-statement.md)
* [<span data-ttu-id="4366e-259">Run steps based on different values (switch statements)</span><span class="sxs-lookup"><span data-stu-id="4366e-259">Run steps based on different values (switch statements)</span></span>](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [<span data-ttu-id="4366e-260">Run or merge parallel steps (branches)</span><span class="sxs-lookup"><span data-stu-id="4366e-260">Run or merge parallel steps (branches)</span></span>](../logic-apps/logic-apps-control-flow-branches.md)
* [<span data-ttu-id="4366e-261">Run steps based on grouped action status (scopes)</span><span class="sxs-lookup"><span data-stu-id="4366e-261">Run steps based on grouped action status (scopes)</span></span>](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
