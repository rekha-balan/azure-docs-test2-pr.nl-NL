---
title: Call a function from PowerApps | Microsoft Docs
description: Create a custom connector then call a function using that connector.
services: functions
keywords: cloud apps, cloud services, PowerApps, business processes, business application
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.topic: conceptual
ms.date: 12/14/2017
ms.author: glenga
ms.reviewer: sunayv
ms.custom: ''
ms.openlocfilehash: 55de3cd8830834a2af512661d5389952d927ef9f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857218"
---
# <a name="call-a-function-from-powerapps"></a><span data-ttu-id="9abb4-104">Call a function from PowerApps</span><span class="sxs-lookup"><span data-stu-id="9abb4-104">Call a function from PowerApps</span></span>
<span data-ttu-id="9abb4-105">The [PowerApps](https://powerapps.microsoft.com) platform is designed for business experts to build apps without traditional application code.</span><span class="sxs-lookup"><span data-stu-id="9abb4-105">The [PowerApps](https://powerapps.microsoft.com) platform is designed for business experts to build apps without traditional application code.</span></span> <span data-ttu-id="9abb4-106">Professional developers can use Azure Functions to extend the capabilities of PowerApps, while shielding PowerApps app builders from the technical details.</span><span class="sxs-lookup"><span data-stu-id="9abb4-106">Professional developers can use Azure Functions to extend the capabilities of PowerApps, while shielding PowerApps app builders from the technical details.</span></span>

<span data-ttu-id="9abb4-107">You build an app in this topic based on a maintenance scenario for wind turbines.</span><span class="sxs-lookup"><span data-stu-id="9abb4-107">You build an app in this topic based on a maintenance scenario for wind turbines.</span></span> <span data-ttu-id="9abb4-108">This topic shows you how to call the function that you defined in [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span><span class="sxs-lookup"><span data-stu-id="9abb4-108">This topic shows you how to call the function that you defined in [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span></span> <span data-ttu-id="9abb4-109">The function determines if an emergency repair on a wind turbine is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="9abb4-109">The function determines if an emergency repair on a wind turbine is cost-effective.</span></span>

![Finished app in PowerApps](media/functions-powerapps-scenario/finished-app.png)

<span data-ttu-id="9abb4-111">For information on calling the same function from Microsoft Flow, see [Call a function from Microsoft Flow](functions-flow-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="9abb4-111">For information on calling the same function from Microsoft Flow, see [Call a function from Microsoft Flow](functions-flow-scenario.md).</span></span>

<span data-ttu-id="9abb4-112">In this topic, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="9abb4-112">In this topic, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9abb4-113">Prepare sample data in Excel.</span><span class="sxs-lookup"><span data-stu-id="9abb4-113">Prepare sample data in Excel.</span></span>
> * <span data-ttu-id="9abb4-114">Export an API definition.</span><span class="sxs-lookup"><span data-stu-id="9abb4-114">Export an API definition.</span></span>
> * <span data-ttu-id="9abb4-115">Add a connection to the API.</span><span class="sxs-lookup"><span data-stu-id="9abb4-115">Add a connection to the API.</span></span>
> * <span data-ttu-id="9abb4-116">Create an app and add data sources.</span><span class="sxs-lookup"><span data-stu-id="9abb4-116">Create an app and add data sources.</span></span>
> * <span data-ttu-id="9abb4-117">Add controls to view data in the app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-117">Add controls to view data in the app.</span></span>
> * <span data-ttu-id="9abb4-118">Add controls to call the function and display data.</span><span class="sxs-lookup"><span data-stu-id="9abb4-118">Add controls to call the function and display data.</span></span>
> * <span data-ttu-id="9abb4-119">Run the app to determine whether a repair is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="9abb4-119">Run the app to determine whether a repair is cost-effective.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9abb4-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9abb4-120">Prerequisites</span></span>

+ <span data-ttu-id="9abb4-121">An active [PowerApps account](https://docs.microsoft.com/en-us/powerapps/maker/signup-for-powerapps) with the same sign in credentials as your Azure account.</span><span class="sxs-lookup"><span data-stu-id="9abb4-121">An active [PowerApps account](https://docs.microsoft.com/en-us/powerapps/maker/signup-for-powerapps) with the same sign in credentials as your Azure account.</span></span> 
+ <span data-ttu-id="9abb4-122">Excel and the [Excel sample file](https://procsi.blob.core.windows.net/docs/turbine-data.xlsx) that you will use as a data source for your app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-122">Excel and the [Excel sample file](https://procsi.blob.core.windows.net/docs/turbine-data.xlsx) that you will use as a data source for your app.</span></span>
+ <span data-ttu-id="9abb4-123">Complete the tutorial [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span><span class="sxs-lookup"><span data-stu-id="9abb4-123">Complete the tutorial [Create an OpenAPI definition for a function](functions-openapi-definition.md).</span></span>

[!INCLUDE [Export an API definition](../../includes/functions-export-api-definition.md)]

## <a name="add-a-connection-to-the-api"></a><span data-ttu-id="9abb4-124">Add a connection to the API</span><span class="sxs-lookup"><span data-stu-id="9abb4-124">Add a connection to the API</span></span>
<span data-ttu-id="9abb4-125">The custom API (also known as a custom connector) is available in PowerApps, but you must make a connection to the API before you can use it in an app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-125">The custom API (also known as a custom connector) is available in PowerApps, but you must make a connection to the API before you can use it in an app.</span></span>

1. <span data-ttu-id="9abb4-126">In [web.powerapps.com](https://web.powerapps.com), click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-126">In [web.powerapps.com](https://web.powerapps.com), click **Connections**.</span></span>

    ![PowerApps connections](media/functions-powerapps-scenario/powerapps-connections.png)

1. <span data-ttu-id="9abb4-128">Click **New Connection**, scroll down to the **Turbine Repair** connector, and click it.</span><span class="sxs-lookup"><span data-stu-id="9abb4-128">Click **New Connection**, scroll down to the **Turbine Repair** connector, and click it.</span></span>

    ![New connection](media/functions-powerapps-scenario/new-connection.png)

1. <span data-ttu-id="9abb4-130">Enter the API Key, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-130">Enter the API Key, and click **Create**.</span></span>

    ![Create connection](media/functions-powerapps-scenario/create-connection.png)

> [!NOTE]
> <span data-ttu-id="9abb4-132">If you share your app with others, each person who works on or uses the app must also enter the API key to connect to the API.</span><span class="sxs-lookup"><span data-stu-id="9abb4-132">If you share your app with others, each person who works on or uses the app must also enter the API key to connect to the API.</span></span> <span data-ttu-id="9abb4-133">This behavior might change in the future, and we will update this topic to reflect that.</span><span class="sxs-lookup"><span data-stu-id="9abb4-133">This behavior might change in the future, and we will update this topic to reflect that.</span></span>

## <a name="create-an-app-and-add-data-sources"></a><span data-ttu-id="9abb4-134">Create an app and add data sources</span><span class="sxs-lookup"><span data-stu-id="9abb4-134">Create an app and add data sources</span></span>
<span data-ttu-id="9abb4-135">Now you're ready to create the app in PowerApps, and add the Excel data and the custom API as data sources for the app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-135">Now you're ready to create the app in PowerApps, and add the Excel data and the custom API as data sources for the app.</span></span>

1. <span data-ttu-id="9abb4-136">In [web.powerapps.com](https://web.powerapps.com), choose **Start from blank** > ![Phone app icon](media/functions-powerapps-scenario/icon-phone-app.png) (phone) > **Make this app**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-136">In [web.powerapps.com](https://web.powerapps.com), choose **Start from blank** > ![Phone app icon](media/functions-powerapps-scenario/icon-phone-app.png) (phone) > **Make this app**.</span></span>

    ![Start from blank - phone app](media/functions-powerapps-scenario/create-phone-app.png)

    <span data-ttu-id="9abb4-138">The app opens in PowerApps Studio for web.</span><span class="sxs-lookup"><span data-stu-id="9abb4-138">The app opens in PowerApps Studio for web.</span></span> <span data-ttu-id="9abb4-139">The following image shows the different parts of PowerApps Studio.</span><span class="sxs-lookup"><span data-stu-id="9abb4-139">The following image shows the different parts of PowerApps Studio.</span></span>

    ![PowerApps Studio](media/functions-powerapps-scenario/powerapps-studio.png)

    <span data-ttu-id="9abb4-141">**(A) Left navigation bar**, in which you see a hierarchical view of all the controls on each screen</span><span class="sxs-lookup"><span data-stu-id="9abb4-141">**(A) Left navigation bar**, in which you see a hierarchical view of all the controls on each screen</span></span>

    <span data-ttu-id="9abb4-142">**(B) Middle pane**, which shows the screen that you're working on</span><span class="sxs-lookup"><span data-stu-id="9abb4-142">**(B) Middle pane**, which shows the screen that you're working on</span></span>

    <span data-ttu-id="9abb4-143">**(C) Right pane**, where you set options such as layout and data sources</span><span class="sxs-lookup"><span data-stu-id="9abb4-143">**(C) Right pane**, where you set options such as layout and data sources</span></span>

    <span data-ttu-id="9abb4-144">**(D) Property** drop-down list, where you select the properties that formulas apply to</span><span class="sxs-lookup"><span data-stu-id="9abb4-144">**(D) Property** drop-down list, where you select the properties that formulas apply to</span></span>

    <span data-ttu-id="9abb4-145">**(E) Formula bar**, where you add formulas (as in Excel) that define app behavior</span><span class="sxs-lookup"><span data-stu-id="9abb4-145">**(E) Formula bar**, where you add formulas (as in Excel) that define app behavior</span></span>
    
    <span data-ttu-id="9abb4-146">**(F) Ribbon**, where you add controls and customize design elements</span><span class="sxs-lookup"><span data-stu-id="9abb4-146">**(F) Ribbon**, where you add controls and customize design elements</span></span>

1. <span data-ttu-id="9abb4-147">Add the Excel file as a data source.</span><span class="sxs-lookup"><span data-stu-id="9abb4-147">Add the Excel file as a data source.</span></span>

    <span data-ttu-id="9abb4-148">The data you will import looks like the following:</span><span class="sxs-lookup"><span data-stu-id="9abb4-148">The data you will import looks like the following:</span></span>

    ![Excel data to import](media/functions-powerapps-scenario/excel-table.png)

    1. <span data-ttu-id="9abb4-150">On the app canvas, choose **connect to data**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-150">On the app canvas, choose **connect to data**.</span></span>

    1. <span data-ttu-id="9abb4-151">On the **Data** panel, click **Add static data to your app**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-151">On the **Data** panel, click **Add static data to your app**.</span></span>

        ![Add data source](media/functions-powerapps-scenario/add-static-data.png)

        <span data-ttu-id="9abb4-153">Normally you would read and write data from an external source, but you're adding the Excel data as static data because this is a sample.</span><span class="sxs-lookup"><span data-stu-id="9abb4-153">Normally you would read and write data from an external source, but you're adding the Excel data as static data because this is a sample.</span></span>

    1. <span data-ttu-id="9abb4-154">Navigate to the Excel file you saved, select the **Turbines** table, and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-154">Navigate to the Excel file you saved, select the **Turbines** table, and click **Connect**.</span></span>

        ![Add data source](media/functions-powerapps-scenario/choose-table.png)


1. <span data-ttu-id="9abb4-156">Add the custom API as a data source.</span><span class="sxs-lookup"><span data-stu-id="9abb4-156">Add the custom API as a data source.</span></span>

    1. <span data-ttu-id="9abb4-157">On the **Data** panel, click **Add data source**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-157">On the **Data** panel, click **Add data source**.</span></span>

    1. <span data-ttu-id="9abb4-158">Click **Turbine Repair**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-158">Click **Turbine Repair**.</span></span>

        ![Turbine repair connector](media/functions-powerapps-scenario/turbine-connector.png)

## <a name="add-controls-to-view-data-in-the-app"></a><span data-ttu-id="9abb4-160">Add controls to view data in the app</span><span class="sxs-lookup"><span data-stu-id="9abb4-160">Add controls to view data in the app</span></span>
<span data-ttu-id="9abb4-161">Now that the data sources are available in the app, you add a screen to your app so you can view the turbine data.</span><span class="sxs-lookup"><span data-stu-id="9abb4-161">Now that the data sources are available in the app, you add a screen to your app so you can view the turbine data.</span></span>

1. <span data-ttu-id="9abb4-162">On the **Home** tab, click **New screen** > **List screen**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-162">On the **Home** tab, click **New screen** > **List screen**.</span></span>

    ![List screen](media/functions-powerapps-scenario/list-screen.png)

    <span data-ttu-id="9abb4-164">PowerApps adds a screen that contains a *gallery* to display items, and other controls that enable searching, sorting, and filtering.</span><span class="sxs-lookup"><span data-stu-id="9abb4-164">PowerApps adds a screen that contains a *gallery* to display items, and other controls that enable searching, sorting, and filtering.</span></span>

1. <span data-ttu-id="9abb4-165">Change the title bar to `Turbine Repair`, and resize the gallery so there's room for more controls under it.</span><span class="sxs-lookup"><span data-stu-id="9abb4-165">Change the title bar to `Turbine Repair`, and resize the gallery so there's room for more controls under it.</span></span>

    ![Change title and resize gallery](media/functions-powerapps-scenario/gallery-title.png)

1. <span data-ttu-id="9abb4-167">With the gallery selected, in the right pane, under **Properties**, click **CustomGallerySample**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-167">With the gallery selected, in the right pane, under **Properties**, click **CustomGallerySample**.</span></span>

    ![Change data source](media/functions-powerapps-scenario/change-data-source.png)

1. <span data-ttu-id="9abb4-169">In the **Data** panel, select **Turbines** from the list.</span><span class="sxs-lookup"><span data-stu-id="9abb4-169">In the **Data** panel, select **Turbines** from the list.</span></span>

    ![Select data source](media/functions-powerapps-scenario/select-data-source.png)

    <span data-ttu-id="9abb4-171">The data set doesn't contain an image, so next you change the layout to better fit the data.</span><span class="sxs-lookup"><span data-stu-id="9abb4-171">The data set doesn't contain an image, so next you change the layout to better fit the data.</span></span> 

1. <span data-ttu-id="9abb4-172">Still in the **Data** panel, change **Layout** to **Title, subtitle, and body**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-172">Still in the **Data** panel, change **Layout** to **Title, subtitle, and body**.</span></span>

    ![Change gallery layout](media/functions-powerapps-scenario/change-layout.png)

1. <span data-ttu-id="9abb4-174">As the last step in the **Data** panel, change the fields that are displayed in the gallery.</span><span class="sxs-lookup"><span data-stu-id="9abb4-174">As the last step in the **Data** panel, change the fields that are displayed in the gallery.</span></span>

    ![Change gallery fields](media/functions-powerapps-scenario/change-fields.png)
    
    + <span data-ttu-id="9abb4-176">**Body1** = LastServiceDate</span><span class="sxs-lookup"><span data-stu-id="9abb4-176">**Body1** = LastServiceDate</span></span>
    + <span data-ttu-id="9abb4-177">**Subtitle2** = ServiceRequired</span><span class="sxs-lookup"><span data-stu-id="9abb4-177">**Subtitle2** = ServiceRequired</span></span>
    + <span data-ttu-id="9abb4-178">**Title2** = Title</span><span class="sxs-lookup"><span data-stu-id="9abb4-178">**Title2** = Title</span></span> 

1. <span data-ttu-id="9abb4-179">With the gallery selected, set the **TemplateFill** property to the following formula: `If(ThisItem.IsSelected, Orange, White)`.</span><span class="sxs-lookup"><span data-stu-id="9abb4-179">With the gallery selected, set the **TemplateFill** property to the following formula: `If(ThisItem.IsSelected, Orange, White)`.</span></span>

    ![Template fill formula](media/functions-powerapps-scenario/formula-fill.png)

    <span data-ttu-id="9abb4-181">Now it's easier to see which gallery item is selected.</span><span class="sxs-lookup"><span data-stu-id="9abb4-181">Now it's easier to see which gallery item is selected.</span></span>

    ![Selected item](media/functions-powerapps-scenario/selected-item.png)

1. <span data-ttu-id="9abb4-183">You don't need the original screen in the app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-183">You don't need the original screen in the app.</span></span> <span data-ttu-id="9abb4-184">In the left pane, hover over **Screen1**, click **. . .**, and **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-184">In the left pane, hover over **Screen1**, click **. . .**, and **Delete**.</span></span>

    ![Delete screen](media/functions-powerapps-scenario/delete-screen.png)

1. <span data-ttu-id="9abb4-186">Click **File**, and name the app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-186">Click **File**, and name the app.</span></span> <span data-ttu-id="9abb4-187">Click **Save** on the left menu, then click **Save** in the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="9abb4-187">Click **Save** on the left menu, then click **Save** in the bottom right corner.</span></span>

<span data-ttu-id="9abb4-188">There's a lot of other formatting you would typically do in a production app, but we'll move on to the important part for this scenario - calling the function.</span><span class="sxs-lookup"><span data-stu-id="9abb4-188">There's a lot of other formatting you would typically do in a production app, but we'll move on to the important part for this scenario - calling the function.</span></span>

## <a name="add-controls-to-call-the-function-and-display-data"></a><span data-ttu-id="9abb4-189">Add controls to call the function and display data</span><span class="sxs-lookup"><span data-stu-id="9abb4-189">Add controls to call the function and display data</span></span>
<span data-ttu-id="9abb4-190">You have an app that displays summary data for each turbine, so now it's time to add controls that call the function you created, and display the data that is returned.</span><span class="sxs-lookup"><span data-stu-id="9abb4-190">You have an app that displays summary data for each turbine, so now it's time to add controls that call the function you created, and display the data that is returned.</span></span> <span data-ttu-id="9abb4-191">You access the function based on the way you name it in the OpenAPI definition; in this case it's `TurbineRepair.CalculateCosts()`.</span><span class="sxs-lookup"><span data-stu-id="9abb4-191">You access the function based on the way you name it in the OpenAPI definition; in this case it's `TurbineRepair.CalculateCosts()`.</span></span>

1. <span data-ttu-id="9abb4-192">In the ribbon, on the **Insert** tab, click **Button**.</span><span class="sxs-lookup"><span data-stu-id="9abb4-192">In the ribbon, on the **Insert** tab, click **Button**.</span></span> <span data-ttu-id="9abb4-193">Then on the same tab, click **Label**</span><span class="sxs-lookup"><span data-stu-id="9abb4-193">Then on the same tab, click **Label**</span></span>

    ![Insert button and label](media/functions-powerapps-scenario/insert-controls.png)

1. <span data-ttu-id="9abb4-195">Drag the button and the label below the gallery, and resize the label.</span><span class="sxs-lookup"><span data-stu-id="9abb4-195">Drag the button and the label below the gallery, and resize the label.</span></span> 

1. <span data-ttu-id="9abb4-196">Select the button text, and change it to `Calculate costs`.</span><span class="sxs-lookup"><span data-stu-id="9abb4-196">Select the button text, and change it to `Calculate costs`.</span></span> <span data-ttu-id="9abb4-197">The app should look like the following image.</span><span class="sxs-lookup"><span data-stu-id="9abb4-197">The app should look like the following image.</span></span>

    ![App with button](media/functions-powerapps-scenario/move-button-label.png)

1. <span data-ttu-id="9abb4-199">Select the button, and enter the following formula for the button's **OnSelect** property.</span><span class="sxs-lookup"><span data-stu-id="9abb4-199">Select the button, and enter the following formula for the button's **OnSelect** property.</span></span>

    ```
    If (BrowseGallery1.Selected.ServiceRequired="Yes", ClearCollect(DetermineRepair, TurbineRepair.CalculateCosts({hours: BrowseGallery1.Selected.EstimatedEffort, capacity: BrowseGallery1.Selected.MaxOutput})))
    ```
    <span data-ttu-id="9abb4-200">This formula executes when the button is clicked, and it does the following if the selected gallery item has a **ServiceRequired** value of `Yes`:</span><span class="sxs-lookup"><span data-stu-id="9abb4-200">This formula executes when the button is clicked, and it does the following if the selected gallery item has a **ServiceRequired** value of `Yes`:</span></span>

    + <span data-ttu-id="9abb4-201">Clears the *collection* `DetermineRepair` to remove data from previous calls.</span><span class="sxs-lookup"><span data-stu-id="9abb4-201">Clears the *collection* `DetermineRepair` to remove data from previous calls.</span></span> <span data-ttu-id="9abb4-202">A collection is a tabular variable.</span><span class="sxs-lookup"><span data-stu-id="9abb4-202">A collection is a tabular variable.</span></span>

    + <span data-ttu-id="9abb4-203">Assigns to the collection the data returned by calling the function `TurbineRepair.CalculateCosts()`.</span><span class="sxs-lookup"><span data-stu-id="9abb4-203">Assigns to the collection the data returned by calling the function `TurbineRepair.CalculateCosts()`.</span></span> 
    
        <span data-ttu-id="9abb4-204">The values passed to the function come from the **EstimatedEffort** and **MaxOutput** fields for the item selected in the gallery.</span><span class="sxs-lookup"><span data-stu-id="9abb4-204">The values passed to the function come from the **EstimatedEffort** and **MaxOutput** fields for the item selected in the gallery.</span></span> <span data-ttu-id="9abb4-205">These fields aren't displayed in the gallery, but they're still available to use in formulas.</span><span class="sxs-lookup"><span data-stu-id="9abb4-205">These fields aren't displayed in the gallery, but they're still available to use in formulas.</span></span>

1. <span data-ttu-id="9abb4-206">Select the label, and enter the following formula for the label's **Text** property.</span><span class="sxs-lookup"><span data-stu-id="9abb4-206">Select the label, and enter the following formula for the label's **Text** property.</span></span>

    ```
    "Repair decision: " & First(DetermineRepair).message & " | Cost: " & First(DetermineRepair).costToFix & " | Revenue: " & First(DetermineRepair).revenueOpportunity
    ```
    <span data-ttu-id="9abb4-207">This formula uses the `First()` function to access the first (and only) row of the `DetermineRepair` collection.</span><span class="sxs-lookup"><span data-stu-id="9abb4-207">This formula uses the `First()` function to access the first (and only) row of the `DetermineRepair` collection.</span></span> <span data-ttu-id="9abb4-208">It then displays the three values that the function returns: `message`, `costToFix`, and `revenueOpportunity`.</span><span class="sxs-lookup"><span data-stu-id="9abb4-208">It then displays the three values that the function returns: `message`, `costToFix`, and `revenueOpportunity`.</span></span> <span data-ttu-id="9abb4-209">These values are blank before the app runs for the first time.</span><span class="sxs-lookup"><span data-stu-id="9abb4-209">These values are blank before the app runs for the first time.</span></span>

    <span data-ttu-id="9abb4-210">The completed app should look like the following image.</span><span class="sxs-lookup"><span data-stu-id="9abb4-210">The completed app should look like the following image.</span></span>

    ![Finished app before run](media/functions-powerapps-scenario/finished-app-before-run.png)


## <a name="run-the-app"></a><span data-ttu-id="9abb4-212">Run the app</span><span class="sxs-lookup"><span data-stu-id="9abb4-212">Run the app</span></span>
<span data-ttu-id="9abb4-213">You have a complete app!</span><span class="sxs-lookup"><span data-stu-id="9abb4-213">You have a complete app!</span></span> <span data-ttu-id="9abb4-214">Now it's time to run it and see the function calls in action.</span><span class="sxs-lookup"><span data-stu-id="9abb4-214">Now it's time to run it and see the function calls in action.</span></span>

1. <span data-ttu-id="9abb4-215">In the upper right corner of PowerApps Studio, click the run button:</span><span class="sxs-lookup"><span data-stu-id="9abb4-215">In the upper right corner of PowerApps Studio, click the run button:</span></span> ![Run app button](media/functions-powerapps-scenario/f5-arrow-sm.png)<span data-ttu-id="9abb4-217">.</span><span class="sxs-lookup"><span data-stu-id="9abb4-217">.</span></span>

1. <span data-ttu-id="9abb4-218">Select a turbine with a value of `Yes` for **ServiceRequired**, then click the **Calculate costs** button.</span><span class="sxs-lookup"><span data-stu-id="9abb4-218">Select a turbine with a value of `Yes` for **ServiceRequired**, then click the **Calculate costs** button.</span></span> <span data-ttu-id="9abb4-219">You should see a result like the following image.</span><span class="sxs-lookup"><span data-stu-id="9abb4-219">You should see a result like the following image.</span></span>

    ![Finished app in PowerApps](media/functions-powerapps-scenario/finished-app.png)

1. <span data-ttu-id="9abb4-221">Try the other turbines to see what's returned by the function each time.</span><span class="sxs-lookup"><span data-stu-id="9abb4-221">Try the other turbines to see what's returned by the function each time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abb4-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="9abb4-222">Next steps</span></span>
<span data-ttu-id="9abb4-223">In this topic, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="9abb4-223">In this topic, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9abb4-224">Prepare sample data in Excel.</span><span class="sxs-lookup"><span data-stu-id="9abb4-224">Prepare sample data in Excel.</span></span>
> * <span data-ttu-id="9abb4-225">Export an API definition.</span><span class="sxs-lookup"><span data-stu-id="9abb4-225">Export an API definition.</span></span>
> * <span data-ttu-id="9abb4-226">Add a connection to the API.</span><span class="sxs-lookup"><span data-stu-id="9abb4-226">Add a connection to the API.</span></span>
> * <span data-ttu-id="9abb4-227">Create an app and add data sources.</span><span class="sxs-lookup"><span data-stu-id="9abb4-227">Create an app and add data sources.</span></span>
> * <span data-ttu-id="9abb4-228">Add controls to view data in the app.</span><span class="sxs-lookup"><span data-stu-id="9abb4-228">Add controls to view data in the app.</span></span>
> * <span data-ttu-id="9abb4-229">Add controls to call the function and display data</span><span class="sxs-lookup"><span data-stu-id="9abb4-229">Add controls to call the function and display data</span></span>
> * <span data-ttu-id="9abb4-230">Run the app to determine whether a repair is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="9abb4-230">Run the app to determine whether a repair is cost-effective.</span></span>

<span data-ttu-id="9abb4-231">To learn more about PowerApps, see [Introduction to PowerApps](https://powerapps.microsoft.com/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="9abb4-231">To learn more about PowerApps, see [Introduction to PowerApps](https://powerapps.microsoft.com/tutorials/getting-started/).</span></span>

<span data-ttu-id="9abb4-232">To learn about other interesting scenarios that use Azure Functions, see [Call a function from Microsoft Flow](functions-flow-scenario.md) and [Create a function that integrates with Azure Logic Apps](functions-twitter-email.md).</span><span class="sxs-lookup"><span data-stu-id="9abb4-232">To learn about other interesting scenarios that use Azure Functions, see [Call a function from Microsoft Flow](functions-flow-scenario.md) and [Create a function that integrates with Azure Logic Apps](functions-twitter-email.md).</span></span>
