---
title: Call an Azure function from Microsoft Flow | Microsoft Docs
description: Create a custom connector then call a function using that connector.
services: functions
keywords: cloud apps, cloud services, Microsoft Flow, business processes, business application
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.topic: conceptual
ms.date: 12/14/2017
ms.author: glenga
ms.reviewer: sunayv
ms.custom: ''
ms.openlocfilehash: 662c78fc7074b0dafc53c393962aa4b578779095
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865075"
---
# <a name="call-a-function-from-microsoft-flow"></a><span data-ttu-id="f5c64-104">Call a function from Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="f5c64-104">Call a function from Microsoft Flow</span></span>

<span data-ttu-id="f5c64-105">[Microsoft Flow](https://flow.microsoft.com/) makes it easy to automate workflows and business processes between your favorite apps and services.</span><span class="sxs-lookup"><span data-stu-id="f5c64-105">[Microsoft Flow](https://flow.microsoft.com/) makes it easy to automate workflows and business processes between your favorite apps and services.</span></span> <span data-ttu-id="f5c64-106">Professional developers can use Azure Functions to extend the capabilities of Microsoft Flow, while shielding flow builders from the technical details.</span><span class="sxs-lookup"><span data-stu-id="f5c64-106">Professional developers can use Azure Functions to extend the capabilities of Microsoft Flow, while shielding flow builders from the technical details.</span></span>

<span data-ttu-id="f5c64-107">You build a flow in this topic based on a maintenance scenario for wind turbines.</span><span class="sxs-lookup"><span data-stu-id="f5c64-107">You build a flow in this topic based on a maintenance scenario for wind turbines.</span></span> <span data-ttu-id="f5c64-108">This topic shows you how to call the function that you defined in [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span><span class="sxs-lookup"><span data-stu-id="f5c64-108">This topic shows you how to call the function that you defined in [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span></span> <span data-ttu-id="f5c64-109">The function determines if an emergency repair on a wind turbine is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="f5c64-109">The function determines if an emergency repair on a wind turbine is cost-effective.</span></span> <span data-ttu-id="f5c64-110">If it is cost-effective, the flow sends an email to recommend the repair.</span><span class="sxs-lookup"><span data-stu-id="f5c64-110">If it is cost-effective, the flow sends an email to recommend the repair.</span></span>

<span data-ttu-id="f5c64-111">For information on calling the same function from PowerApps, see [Call a function from PowerApps](functions-powerapps-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="f5c64-111">For information on calling the same function from PowerApps, see [Call a function from PowerApps](functions-powerapps-scenario.md).</span></span>

<span data-ttu-id="f5c64-112">In this topic, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f5c64-112">In this topic, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5c64-113">Create a list in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5c64-113">Create a list in SharePoint.</span></span>
> * <span data-ttu-id="f5c64-114">Export an API definition.</span><span class="sxs-lookup"><span data-stu-id="f5c64-114">Export an API definition.</span></span>
> * <span data-ttu-id="f5c64-115">Add a connection to the API.</span><span class="sxs-lookup"><span data-stu-id="f5c64-115">Add a connection to the API.</span></span>
> * <span data-ttu-id="f5c64-116">Create a flow to send email if a repair is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="f5c64-116">Create a flow to send email if a repair is cost-effective.</span></span>
> * <span data-ttu-id="f5c64-117">Run the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-117">Run the flow.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5c64-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5c64-118">Prerequisites</span></span>

+ <span data-ttu-id="f5c64-119">An active [Microsoft Flow account](https://flow.microsoft.com/documentation/sign-up-sign-in/) with the same sign in credentials as your Azure account.</span><span class="sxs-lookup"><span data-stu-id="f5c64-119">An active [Microsoft Flow account](https://flow.microsoft.com/documentation/sign-up-sign-in/) with the same sign in credentials as your Azure account.</span></span> 
+ <span data-ttu-id="f5c64-120">SharePoint, which you use as a data source for this flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-120">SharePoint, which you use as a data source for this flow.</span></span> <span data-ttu-id="f5c64-121">Sign up for [an Office 365 trial](https://signup.microsoft.com/Signup?OfferId=467eab54-127b-42d3-b046-3844b860bebf&dl=O365_BUSINESS_PREMIUM&ali=1) if you don't already have SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5c64-121">Sign up for [an Office 365 trial](https://signup.microsoft.com/Signup?OfferId=467eab54-127b-42d3-b046-3844b860bebf&dl=O365_BUSINESS_PREMIUM&ali=1) if you don't already have SharePoint.</span></span>
+ <span data-ttu-id="f5c64-122">Complete the tutorial [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span><span class="sxs-lookup"><span data-stu-id="f5c64-122">Complete the tutorial [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span></span>

## <a name="create-a-sharepoint-list"></a><span data-ttu-id="f5c64-123">Create a SharePoint list</span><span class="sxs-lookup"><span data-stu-id="f5c64-123">Create a SharePoint list</span></span>
<span data-ttu-id="f5c64-124">You start off by creating a list that you use as a data source for the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-124">You start off by creating a list that you use as a data source for the flow.</span></span> <span data-ttu-id="f5c64-125">The list has the following columns.</span><span class="sxs-lookup"><span data-stu-id="f5c64-125">The list has the following columns.</span></span>

| <span data-ttu-id="f5c64-126">List Column</span><span class="sxs-lookup"><span data-stu-id="f5c64-126">List Column</span></span>     | <span data-ttu-id="f5c64-127">Data Type</span><span class="sxs-lookup"><span data-stu-id="f5c64-127">Data Type</span></span>           | <span data-ttu-id="f5c64-128">Notes</span><span class="sxs-lookup"><span data-stu-id="f5c64-128">Notes</span></span>                                    |
|-----------------|---------------------|------------------------------------------|
| <span data-ttu-id="f5c64-129">**Title**</span><span class="sxs-lookup"><span data-stu-id="f5c64-129">**Title**</span></span>           | <span data-ttu-id="f5c64-130">Single line of text</span><span class="sxs-lookup"><span data-stu-id="f5c64-130">Single line of text</span></span> | <span data-ttu-id="f5c64-131">Name of the turbine</span><span class="sxs-lookup"><span data-stu-id="f5c64-131">Name of the turbine</span></span>                      |
| <span data-ttu-id="f5c64-132">**LastServiceDate**</span><span class="sxs-lookup"><span data-stu-id="f5c64-132">**LastServiceDate**</span></span> | <span data-ttu-id="f5c64-133">Date</span><span class="sxs-lookup"><span data-stu-id="f5c64-133">Date</span></span>                |                                          |
| <span data-ttu-id="f5c64-134">**MaxOutput**</span><span class="sxs-lookup"><span data-stu-id="f5c64-134">**MaxOutput**</span></span>       | <span data-ttu-id="f5c64-135">Number</span><span class="sxs-lookup"><span data-stu-id="f5c64-135">Number</span></span>              | <span data-ttu-id="f5c64-136">Output of the turbine, in KwH</span><span class="sxs-lookup"><span data-stu-id="f5c64-136">Output of the turbine, in KwH</span></span>            |
| <span data-ttu-id="f5c64-137">**ServiceRequired**</span><span class="sxs-lookup"><span data-stu-id="f5c64-137">**ServiceRequired**</span></span> | <span data-ttu-id="f5c64-138">Yes/No</span><span class="sxs-lookup"><span data-stu-id="f5c64-138">Yes/No</span></span>              |                                          |
| <span data-ttu-id="f5c64-139">**EstimatedEffort**</span><span class="sxs-lookup"><span data-stu-id="f5c64-139">**EstimatedEffort**</span></span> | <span data-ttu-id="f5c64-140">Number</span><span class="sxs-lookup"><span data-stu-id="f5c64-140">Number</span></span>              | <span data-ttu-id="f5c64-141">Estimated time for the repair, in hours</span><span class="sxs-lookup"><span data-stu-id="f5c64-141">Estimated time for the repair, in hours</span></span> |

1. <span data-ttu-id="f5c64-142">In your SharePoint site, click or tap **New**, then **List**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-142">In your SharePoint site, click or tap **New**, then **List**.</span></span>

    ![Create new SharePoint list](./media/functions-flow-scenario/new-list.png)

2. <span data-ttu-id="f5c64-144">Enter the name `Turbines`, then click or tap **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-144">Enter the name `Turbines`, then click or tap **Create**.</span></span>

    ![Specify name for new list](./media/functions-flow-scenario/create-list.png)

    <span data-ttu-id="f5c64-146">The **Turbines** list is created, with the default **Title** field.</span><span class="sxs-lookup"><span data-stu-id="f5c64-146">The **Turbines** list is created, with the default **Title** field.</span></span>

    ![Turbines list](./media/functions-flow-scenario/initial-list.png)

3. <span data-ttu-id="f5c64-148">Click or tap ![New item icon](./media/functions-flow-scenario/icon-new.png) then **Date**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-148">Click or tap ![New item icon](./media/functions-flow-scenario/icon-new.png) then **Date**.</span></span>

    ![Add single line of text field](./media/functions-flow-scenario/add-column.png)

4. <span data-ttu-id="f5c64-150">Enter the name `LastServiceDate`, then click or tap **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-150">Enter the name `LastServiceDate`, then click or tap **Create**.</span></span>

    ![Create LastServiceDate column](./media/functions-flow-scenario/date-column.png)

5. <span data-ttu-id="f5c64-152">Repeat the last two steps for the other three columns in the list:</span><span class="sxs-lookup"><span data-stu-id="f5c64-152">Repeat the last two steps for the other three columns in the list:</span></span>

    1. <span data-ttu-id="f5c64-153">**Number** > "MaxOutput"</span><span class="sxs-lookup"><span data-stu-id="f5c64-153">**Number** > "MaxOutput"</span></span>

    2. <span data-ttu-id="f5c64-154">**Yes/No** > "ServiceRequired"</span><span class="sxs-lookup"><span data-stu-id="f5c64-154">**Yes/No** > "ServiceRequired"</span></span>

    3. <span data-ttu-id="f5c64-155">**Number** > "EstimatedEffort"</span><span class="sxs-lookup"><span data-stu-id="f5c64-155">**Number** > "EstimatedEffort"</span></span>

<span data-ttu-id="f5c64-156">That's it for now - you should have an empty list that looks like the following image.</span><span class="sxs-lookup"><span data-stu-id="f5c64-156">That's it for now - you should have an empty list that looks like the following image.</span></span> <span data-ttu-id="f5c64-157">You add data to the list after you create the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-157">You add data to the list after you create the flow.</span></span>

![Empty list](media/functions-flow-scenario/empty-list.png)

[!INCLUDE [Export an API definition](../../includes/functions-export-api-definition.md)]

## <a name="add-a-connection-to-the-api"></a><span data-ttu-id="f5c64-159">Add a connection to the API</span><span class="sxs-lookup"><span data-stu-id="f5c64-159">Add a connection to the API</span></span>
<span data-ttu-id="f5c64-160">The custom API (also known as a custom connector) is available in Microsoft Flow, but you must make a connection to the API before you can use it in a flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-160">The custom API (also known as a custom connector) is available in Microsoft Flow, but you must make a connection to the API before you can use it in a flow.</span></span>

1. <span data-ttu-id="f5c64-161">In [flow.microsoft.com](https://flow.microsoft.com), click the gear icon (in the upper right), then click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-161">In [flow.microsoft.com](https://flow.microsoft.com), click the gear icon (in the upper right), then click **Connections**.</span></span>

    ![Flow connections](media/functions-flow-scenario/flow-connections.png)

1. <span data-ttu-id="f5c64-163">Click **Create Connection**, scroll down to the **Turbine Repair** connector, and click it.</span><span class="sxs-lookup"><span data-stu-id="f5c64-163">Click **Create Connection**, scroll down to the **Turbine Repair** connector, and click it.</span></span>

    ![Create connection](media/functions-flow-scenario/create-connection.png)

1. <span data-ttu-id="f5c64-165">Enter the API Key, and click **Create connection**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-165">Enter the API Key, and click **Create connection**.</span></span>

    ![Enter API key and create](media/functions-flow-scenario/api-key.png)

> [!NOTE]
> <span data-ttu-id="f5c64-167">If you share your flow with others, each person who works on or uses the flow must also enter the API key to connect to the API.</span><span class="sxs-lookup"><span data-stu-id="f5c64-167">If you share your flow with others, each person who works on or uses the flow must also enter the API key to connect to the API.</span></span> <span data-ttu-id="f5c64-168">This behavior might change in the future, and we will update this topic to reflect that.</span><span class="sxs-lookup"><span data-stu-id="f5c64-168">This behavior might change in the future, and we will update this topic to reflect that.</span></span>


## <a name="create-a-flow"></a><span data-ttu-id="f5c64-169">Create a flow</span><span class="sxs-lookup"><span data-stu-id="f5c64-169">Create a flow</span></span>

<span data-ttu-id="f5c64-170">Now you're ready to create a flow that uses the custom connector and the SharePoint list you created.</span><span class="sxs-lookup"><span data-stu-id="f5c64-170">Now you're ready to create a flow that uses the custom connector and the SharePoint list you created.</span></span>

### <a name="add-a-trigger-and-specify-a-condition"></a><span data-ttu-id="f5c64-171">Add a trigger and specify a condition</span><span class="sxs-lookup"><span data-stu-id="f5c64-171">Add a trigger and specify a condition</span></span>

<span data-ttu-id="f5c64-172">You first create a flow from blank (without a template), and add a *trigger* that fires when an item is created in the SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f5c64-172">You first create a flow from blank (without a template), and add a *trigger* that fires when an item is created in the SharePoint list.</span></span> <span data-ttu-id="f5c64-173">You then add a *condition* to determine what happens next.</span><span class="sxs-lookup"><span data-stu-id="f5c64-173">You then add a *condition* to determine what happens next.</span></span>

1. <span data-ttu-id="f5c64-174">In [flow.microsoft.com](https://flow.microsoft.com), click **My Flows**, then **Create from blank**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-174">In [flow.microsoft.com](https://flow.microsoft.com), click **My Flows**, then **Create from blank**.</span></span>

    ![Create from blank](media/functions-flow-scenario/create-from-blank.png)

2. <span data-ttu-id="f5c64-176">Click the SharePoint trigger **When an item is created**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-176">Click the SharePoint trigger **When an item is created**.</span></span>

    ![Choose a trigger](media/functions-flow-scenario/choose-trigger.png)

    <span data-ttu-id="f5c64-178">If you're not already signed into SharePoint, you will be prompted to do so.</span><span class="sxs-lookup"><span data-stu-id="f5c64-178">If you're not already signed into SharePoint, you will be prompted to do so.</span></span>

3. <span data-ttu-id="f5c64-179">For **Site Address**, enter your SharePoint site name, and for **List Name**, enter the list that contains the turbine data.</span><span class="sxs-lookup"><span data-stu-id="f5c64-179">For **Site Address**, enter your SharePoint site name, and for **List Name**, enter the list that contains the turbine data.</span></span>

    ![Choose a trigger](media/functions-flow-scenario/site-list.png)

4. <span data-ttu-id="f5c64-181">Click **New step**, then **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-181">Click **New step**, then **Add a condition**.</span></span>

    ![Add a condition](media/functions-flow-scenario/add-condition.png)

    <span data-ttu-id="f5c64-183">Microsoft Flow adds two branches to the flow: **If yes** and **If no**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-183">Microsoft Flow adds two branches to the flow: **If yes** and **If no**.</span></span> <span data-ttu-id="f5c64-184">You add steps to one or both branches after you define the condition that you want to match.</span><span class="sxs-lookup"><span data-stu-id="f5c64-184">You add steps to one or both branches after you define the condition that you want to match.</span></span>

    ![Condition branches](media/functions-flow-scenario/condition-branches.png)

5. <span data-ttu-id="f5c64-186">On the **Condition** card, click the first box, then select **ServiceRequired** from the **Dynamic content** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f5c64-186">On the **Condition** card, click the first box, then select **ServiceRequired** from the **Dynamic content** dialog box.</span></span>

    ![Select field for condition](media/functions-flow-scenario/condition1-field.png)

6. <span data-ttu-id="f5c64-188">Enter a value of `True` for the condition.</span><span class="sxs-lookup"><span data-stu-id="f5c64-188">Enter a value of `True` for the condition.</span></span>

    ![Enter true for condition](media/functions-flow-scenario/condition1-yes.png)

    <span data-ttu-id="f5c64-190">The value is displayed as `Yes` or `No` in the SharePoint list, but it is stored as a *boolean*, either `True` or `False`.</span><span class="sxs-lookup"><span data-stu-id="f5c64-190">The value is displayed as `Yes` or `No` in the SharePoint list, but it is stored as a *boolean*, either `True` or `False`.</span></span> 

7. <span data-ttu-id="f5c64-191">Click **Create flow** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="f5c64-191">Click **Create flow** at the top of the page.</span></span> <span data-ttu-id="f5c64-192">Be sure to click **Update Flow** periodically.</span><span class="sxs-lookup"><span data-stu-id="f5c64-192">Be sure to click **Update Flow** periodically.</span></span>

<span data-ttu-id="f5c64-193">For any items created in the list, the flow checks if the **ServiceRequired** field is set to `Yes`, then goes to the **If yes** branch or the **If no** branch as appropriate.</span><span class="sxs-lookup"><span data-stu-id="f5c64-193">For any items created in the list, the flow checks if the **ServiceRequired** field is set to `Yes`, then goes to the **If yes** branch or the **If no** branch as appropriate.</span></span> <span data-ttu-id="f5c64-194">To save time, in this topic you only specify actions for the **If yes** branch.</span><span class="sxs-lookup"><span data-stu-id="f5c64-194">To save time, in this topic you only specify actions for the **If yes** branch.</span></span>

### <a name="add-the-custom-connector"></a><span data-ttu-id="f5c64-195">Add the custom connector</span><span class="sxs-lookup"><span data-stu-id="f5c64-195">Add the custom connector</span></span>

<span data-ttu-id="f5c64-196">You now add the custom connector that calls the function in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c64-196">You now add the custom connector that calls the function in Azure.</span></span> <span data-ttu-id="f5c64-197">You add the custom connector to the flow just like a standard connector.</span><span class="sxs-lookup"><span data-stu-id="f5c64-197">You add the custom connector to the flow just like a standard connector.</span></span> 

1. <span data-ttu-id="f5c64-198">In the **If yes** branch, click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-198">In the **If yes** branch, click **Add an action**.</span></span>

    ![Add an action](media/functions-flow-scenario/condition1-yes-add-action.png)

2. <span data-ttu-id="f5c64-200">In the **Choose an action** dialog box, search for `Turbine Repair`, then select the action **Turbine Repair - Calculates costs**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-200">In the **Choose an action** dialog box, search for `Turbine Repair`, then select the action **Turbine Repair - Calculates costs**.</span></span>

    ![Choose an action](media/functions-flow-scenario/choose-turbine-repair.png)

    <span data-ttu-id="f5c64-202">The following image shows the card that is added to the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-202">The following image shows the card that is added to the flow.</span></span> <span data-ttu-id="f5c64-203">The fields and descriptions come from the OpenAPI definition for the connector.</span><span class="sxs-lookup"><span data-stu-id="f5c64-203">The fields and descriptions come from the OpenAPI definition for the connector.</span></span>

    ![Calculates costs defaults](media/functions-flow-scenario/calculates-costs-default.png)

3. <span data-ttu-id="f5c64-205">On the **Calculates costs** card, use the **Dynamic content** dialog box to select inputs for the function.</span><span class="sxs-lookup"><span data-stu-id="f5c64-205">On the **Calculates costs** card, use the **Dynamic content** dialog box to select inputs for the function.</span></span> <span data-ttu-id="f5c64-206">Microsoft Flow shows numeric fields but not the date field, because the OpenAPI definition specifies that **Hours** and **Capacity** are numeric.</span><span class="sxs-lookup"><span data-stu-id="f5c64-206">Microsoft Flow shows numeric fields but not the date field, because the OpenAPI definition specifies that **Hours** and **Capacity** are numeric.</span></span>

    <span data-ttu-id="f5c64-207">For **Hours**, select **EstimatedEffort**, and for **Capacity**, select **MaxOutput**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-207">For **Hours**, select **EstimatedEffort**, and for **Capacity**, select **MaxOutput**.</span></span>

    ![Choose an action](media/functions-flow-scenario/calculates-costs-fields.png)

     <span data-ttu-id="f5c64-209">Now you add another condition based on the output of the function.</span><span class="sxs-lookup"><span data-stu-id="f5c64-209">Now you add another condition based on the output of the function.</span></span>

4. <span data-ttu-id="f5c64-210">At the bottom of the **If yes** branch, click **More**, then **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-210">At the bottom of the **If yes** branch, click **More**, then **Add a condition**.</span></span>

    ![Add a condition](media/functions-flow-scenario/condition2-add.png)

5. <span data-ttu-id="f5c64-212">On the **Condition 2** card, click the first box, then select **Message** from the **Dynamic content** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f5c64-212">On the **Condition 2** card, click the first box, then select **Message** from the **Dynamic content** dialog box.</span></span>

    ![Select field for condition](media/functions-flow-scenario/condition2-field.png)

6. <span data-ttu-id="f5c64-214">Enter a value of `Yes`.</span><span class="sxs-lookup"><span data-stu-id="f5c64-214">Enter a value of `Yes`.</span></span> <span data-ttu-id="f5c64-215">The flow goes to the next **If yes** branch or **If no** branch based on whether the message returned by the function is yes (make the repair) or no (don't make the repair).</span><span class="sxs-lookup"><span data-stu-id="f5c64-215">The flow goes to the next **If yes** branch or **If no** branch based on whether the message returned by the function is yes (make the repair) or no (don't make the repair).</span></span> 

    ![Enter yes for condition](media/functions-flow-scenario/condition2-yes.png)

<span data-ttu-id="f5c64-217">The flow should now look like the following image.</span><span class="sxs-lookup"><span data-stu-id="f5c64-217">The flow should now look like the following image.</span></span>

![Enter yes for condition](media/functions-flow-scenario/flow-checkpoint1.png)

### <a name="send-email-based-on-function-results"></a><span data-ttu-id="f5c64-219">Send email based on function results</span><span class="sxs-lookup"><span data-stu-id="f5c64-219">Send email based on function results</span></span>

<span data-ttu-id="f5c64-220">At this point in the flow, the function has returned a **Message** value of `Yes` or `No` from the function, as well as other information on costs and potential revenue.</span><span class="sxs-lookup"><span data-stu-id="f5c64-220">At this point in the flow, the function has returned a **Message** value of `Yes` or `No` from the function, as well as other information on costs and potential revenue.</span></span> <span data-ttu-id="f5c64-221">In the **If yes** branch of the second condition, you will send an email, but you could do any number of things, like writing back to the SharePoint list or starting an [approval process](https://flow.microsoft.com/documentation/modern-approvals/).</span><span class="sxs-lookup"><span data-stu-id="f5c64-221">In the **If yes** branch of the second condition, you will send an email, but you could do any number of things, like writing back to the SharePoint list or starting an [approval process](https://flow.microsoft.com/documentation/modern-approvals/).</span></span>

1. <span data-ttu-id="f5c64-222">In the **If yes** branch of the second condition, click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-222">In the **If yes** branch of the second condition, click **Add an action**.</span></span>

    ![Add an action](media/functions-flow-scenario/condition2-yes-add-action.png)

2. <span data-ttu-id="f5c64-224">In the **Choose an action** dialog box, search for `email`, then select a send email action based on the email system you use (in this case Outlook).</span><span class="sxs-lookup"><span data-stu-id="f5c64-224">In the **Choose an action** dialog box, search for `email`, then select a send email action based on the email system you use (in this case Outlook).</span></span>

    ![Outlook send an email](media/functions-flow-scenario/outlook-send-email.png)

3. <span data-ttu-id="f5c64-226">On the **Send an email** card, compose an email.</span><span class="sxs-lookup"><span data-stu-id="f5c64-226">On the **Send an email** card, compose an email.</span></span> <span data-ttu-id="f5c64-227">Enter a valid name in your organization for the **To** field.</span><span class="sxs-lookup"><span data-stu-id="f5c64-227">Enter a valid name in your organization for the **To** field.</span></span> <span data-ttu-id="f5c64-228">In the image below you can see the other fields are a combination of text and tokens from the **Dynamic content** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f5c64-228">In the image below you can see the other fields are a combination of text and tokens from the **Dynamic content** dialog box.</span></span> 

    ![Email fields](media/functions-flow-scenario/email-fields.png)

    <span data-ttu-id="f5c64-230">The **Title** token comes from the SharePoint list, and **CostToFix** and **RevenueOpportunity** are returned by the function.</span><span class="sxs-lookup"><span data-stu-id="f5c64-230">The **Title** token comes from the SharePoint list, and **CostToFix** and **RevenueOpportunity** are returned by the function.</span></span>

    <span data-ttu-id="f5c64-231">The completed flow should look like the following image (we left out the first **If no** branch to save space).</span><span class="sxs-lookup"><span data-stu-id="f5c64-231">The completed flow should look like the following image (we left out the first **If no** branch to save space).</span></span>

    ![Complete flow](media/functions-flow-scenario/complete-flow.png)

4. <span data-ttu-id="f5c64-233">Click **Update Flow** at the top of the page, then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-233">Click **Update Flow** at the top of the page, then click **Done**.</span></span>

## <a name="run-the-flow"></a><span data-ttu-id="f5c64-234">Run the flow</span><span class="sxs-lookup"><span data-stu-id="f5c64-234">Run the flow</span></span>

<span data-ttu-id="f5c64-235">Now that the flow is completed, you add a row to the SharePoint list and see how the flow responds.</span><span class="sxs-lookup"><span data-stu-id="f5c64-235">Now that the flow is completed, you add a row to the SharePoint list and see how the flow responds.</span></span>

1. <span data-ttu-id="f5c64-236">Go back to the SharePoint list, and click **Quick Edit**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-236">Go back to the SharePoint list, and click **Quick Edit**.</span></span>

    ![Quick edit](media/functions-flow-scenario/quick-edit.png)

2. <span data-ttu-id="f5c64-238">Enter the following values in the edit grid.</span><span class="sxs-lookup"><span data-stu-id="f5c64-238">Enter the following values in the edit grid.</span></span>

    | <span data-ttu-id="f5c64-239">List Column</span><span class="sxs-lookup"><span data-stu-id="f5c64-239">List Column</span></span>     | <span data-ttu-id="f5c64-240">Value</span><span class="sxs-lookup"><span data-stu-id="f5c64-240">Value</span></span>           |
    |-----------------|---------------------|
    | <span data-ttu-id="f5c64-241">**Title**</span><span class="sxs-lookup"><span data-stu-id="f5c64-241">**Title**</span></span>           | <span data-ttu-id="f5c64-242">Turbine 60</span><span class="sxs-lookup"><span data-stu-id="f5c64-242">Turbine 60</span></span> |
    | <span data-ttu-id="f5c64-243">**LastServiceDate**</span><span class="sxs-lookup"><span data-stu-id="f5c64-243">**LastServiceDate**</span></span> | <span data-ttu-id="f5c64-244">08/04/2017</span><span class="sxs-lookup"><span data-stu-id="f5c64-244">08/04/2017</span></span> |
    | <span data-ttu-id="f5c64-245">**MaxOutput**</span><span class="sxs-lookup"><span data-stu-id="f5c64-245">**MaxOutput**</span></span>       | <span data-ttu-id="f5c64-246">2500</span><span class="sxs-lookup"><span data-stu-id="f5c64-246">2500</span></span> |
    | <span data-ttu-id="f5c64-247">**ServiceRequired**</span><span class="sxs-lookup"><span data-stu-id="f5c64-247">**ServiceRequired**</span></span> | <span data-ttu-id="f5c64-248">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c64-248">Yes</span></span> |
    | <span data-ttu-id="f5c64-249">**EstimatedEffort**</span><span class="sxs-lookup"><span data-stu-id="f5c64-249">**EstimatedEffort**</span></span> | <span data-ttu-id="f5c64-250">10</span><span class="sxs-lookup"><span data-stu-id="f5c64-250">10</span></span> |

3. <span data-ttu-id="f5c64-251">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="f5c64-251">Click **Done**.</span></span>

    ![Quick edit done](media/functions-flow-scenario/quick-edit-done.png)

    <span data-ttu-id="f5c64-253">When you add the item, it triggers the flow, which you take a look at next.</span><span class="sxs-lookup"><span data-stu-id="f5c64-253">When you add the item, it triggers the flow, which you take a look at next.</span></span>

4. <span data-ttu-id="f5c64-254">In [flow.microsoft.com](https://flow.microsoft.com), click **My Flows**, then click the flow you created.</span><span class="sxs-lookup"><span data-stu-id="f5c64-254">In [flow.microsoft.com](https://flow.microsoft.com), click **My Flows**, then click the flow you created.</span></span>

    ![My flows](media/functions-flow-scenario/my-flows.png)

5. <span data-ttu-id="f5c64-256">Under **RUN HISTORY**, click the flow run.</span><span class="sxs-lookup"><span data-stu-id="f5c64-256">Under **RUN HISTORY**, click the flow run.</span></span>

    ![Run history](media/functions-flow-scenario/run-history.png)

    <span data-ttu-id="f5c64-258">If the run was successful, you can review the flow operations on the next page.</span><span class="sxs-lookup"><span data-stu-id="f5c64-258">If the run was successful, you can review the flow operations on the next page.</span></span> <span data-ttu-id="f5c64-259">If the run failed for any reason, the next page provides troubleshooting information.</span><span class="sxs-lookup"><span data-stu-id="f5c64-259">If the run failed for any reason, the next page provides troubleshooting information.</span></span>

6. <span data-ttu-id="f5c64-260">Expand the cards to see what occurred during the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-260">Expand the cards to see what occurred during the flow.</span></span> <span data-ttu-id="f5c64-261">For example, expand the **Calculates costs** card to see the inputs to and outputs from the function.</span><span class="sxs-lookup"><span data-stu-id="f5c64-261">For example, expand the **Calculates costs** card to see the inputs to and outputs from the function.</span></span> 

    ![Calculates costs inputs and outputs](media/functions-flow-scenario/calculates-costs-outputs.png)

7. <span data-ttu-id="f5c64-263">Check the email account for the person you specified in the **To** field of the **Send an email** card.</span><span class="sxs-lookup"><span data-stu-id="f5c64-263">Check the email account for the person you specified in the **To** field of the **Send an email** card.</span></span> <span data-ttu-id="f5c64-264">The email sent from the flow should look like the following image.</span><span class="sxs-lookup"><span data-stu-id="f5c64-264">The email sent from the flow should look like the following image.</span></span>

    ![Flow email](media/functions-flow-scenario/flow-email.png)

    <span data-ttu-id="f5c64-266">You can see how the tokens have been replaced with the correct values from the SharePoint list and the function.</span><span class="sxs-lookup"><span data-stu-id="f5c64-266">You can see how the tokens have been replaced with the correct values from the SharePoint list and the function.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c64-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5c64-267">Next steps</span></span>
<span data-ttu-id="f5c64-268">In this topic, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f5c64-268">In this topic, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5c64-269">Create a list in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5c64-269">Create a list in SharePoint.</span></span>
> * <span data-ttu-id="f5c64-270">Export an API definition.</span><span class="sxs-lookup"><span data-stu-id="f5c64-270">Export an API definition.</span></span>
> * <span data-ttu-id="f5c64-271">Add a connection to the API.</span><span class="sxs-lookup"><span data-stu-id="f5c64-271">Add a connection to the API.</span></span>
> * <span data-ttu-id="f5c64-272">Create a flow to send email if a repair is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="f5c64-272">Create a flow to send email if a repair is cost-effective.</span></span>
> * <span data-ttu-id="f5c64-273">Run the flow.</span><span class="sxs-lookup"><span data-stu-id="f5c64-273">Run the flow.</span></span>

<span data-ttu-id="f5c64-274">To learn more about Microsoft Flow, see [Get started with Microsoft Flow](https://flow.microsoft.com/documentation/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="f5c64-274">To learn more about Microsoft Flow, see [Get started with Microsoft Flow](https://flow.microsoft.com/documentation/getting-started/).</span></span>

<span data-ttu-id="f5c64-275">To learn about other interesting scenarios that use Azure Functions, see [Call a function from PowerApps](functions-powerapps-scenario.md) and [Create a function that integrates with Azure Logic Apps](functions-twitter-email.md).</span><span class="sxs-lookup"><span data-stu-id="f5c64-275">To learn about other interesting scenarios that use Azure Functions, see [Call a function from PowerApps](functions-powerapps-scenario.md) and [Create a function that integrates with Azure Logic Apps](functions-twitter-email.md).</span></span>
