---
title: Create views to analyze data in Azure Log Analytics | Microsoft Docs
description: By using View Designer in Log Analytics, you can create custom views that are displayed in the Azure portal and contain a variety of data visualizations in the Log Analytics workspace. This article contains an overview of View Designer and presents procedures for creating and editing custom views.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 362d19c489dfa0eda33036052ac9626414ef0933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818628"
---
# <a name="create-custom-views-by-using-view-designer-in-log-analytics"></a><span data-ttu-id="6dd30-104">Create custom views by using View Designer in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6dd30-104">Create custom views by using View Designer in Log Analytics</span></span>
<span data-ttu-id="6dd30-105">By using View Designer in [Azure Log Analytics](log-analytics-overview.md), you can create a variety of custom views in the Azure portal that can help you visualize data in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-105">By using View Designer in [Azure Log Analytics](log-analytics-overview.md), you can create a variety of custom views in the Azure portal that can help you visualize data in your Log Analytics workspace.</span></span> <span data-ttu-id="6dd30-106">This article presents an overview of View Designer and procedures for creating and editing custom views.</span><span class="sxs-lookup"><span data-stu-id="6dd30-106">This article presents an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="6dd30-107">For more information about View Designer, see:</span><span class="sxs-lookup"><span data-stu-id="6dd30-107">For more information about View Designer, see:</span></span>

* <span data-ttu-id="6dd30-108">[Tile reference](log-analytics-view-designer-tiles.md): Provides a reference guide to the settings for each of the available tiles in your custom views.</span><span class="sxs-lookup"><span data-stu-id="6dd30-108">[Tile reference](log-analytics-view-designer-tiles.md): Provides a reference guide to the settings for each of the available tiles in your custom views.</span></span>
* <span data-ttu-id="6dd30-109">[Visualization part reference](log-analytics-view-designer-parts.md): Provides a reference guide to the settings for the visualization parts that are available in your custom views.</span><span class="sxs-lookup"><span data-stu-id="6dd30-109">[Visualization part reference](log-analytics-view-designer-parts.md): Provides a reference guide to the settings for the visualization parts that are available in your custom views.</span></span>


## <a name="concepts"></a><span data-ttu-id="6dd30-110">Concepts</span><span class="sxs-lookup"><span data-stu-id="6dd30-110">Concepts</span></span>
<span data-ttu-id="6dd30-111">Views are displayed on the **Overview** page of your Log Analytics workspace in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6dd30-111">Views are displayed on the **Overview** page of your Log Analytics workspace in the Azure portal.</span></span> <span data-ttu-id="6dd30-112">The tiles in each custom view are displayed alphabetically, and the tiles for the solutions are installed the same workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-112">The tiles in each custom view are displayed alphabetically, and the tiles for the solutions are installed the same workspace.</span></span>

![Overview page](media/log-analytics-view-designer/overview-page.png)

<span data-ttu-id="6dd30-114">The views that you create with View Designer contain the elements that are described in the following table:</span><span class="sxs-lookup"><span data-stu-id="6dd30-114">The views that you create with View Designer contain the elements that are described in the following table:</span></span>

| <span data-ttu-id="6dd30-115">Part</span><span class="sxs-lookup"><span data-stu-id="6dd30-115">Part</span></span> | <span data-ttu-id="6dd30-116">Description</span><span class="sxs-lookup"><span data-stu-id="6dd30-116">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6dd30-117">Tiles</span><span class="sxs-lookup"><span data-stu-id="6dd30-117">Tiles</span></span> | <span data-ttu-id="6dd30-118">Are displayed on your Log Analytics workspace **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="6dd30-118">Are displayed on your Log Analytics workspace **Overview** page.</span></span> <span data-ttu-id="6dd30-119">Each tile displays a visual summary of the custom view it represents.</span><span class="sxs-lookup"><span data-stu-id="6dd30-119">Each tile displays a visual summary of the custom view it represents.</span></span> <span data-ttu-id="6dd30-120">Each tile type provides a different visualization of your records.</span><span class="sxs-lookup"><span data-stu-id="6dd30-120">Each tile type provides a different visualization of your records.</span></span> <span data-ttu-id="6dd30-121">You select a tile to display a custom view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-121">You select a tile to display a custom view.</span></span> |
| <span data-ttu-id="6dd30-122">Custom view</span><span class="sxs-lookup"><span data-stu-id="6dd30-122">Custom view</span></span> | <span data-ttu-id="6dd30-123">Displayed when you select a tile.</span><span class="sxs-lookup"><span data-stu-id="6dd30-123">Displayed when you select a tile.</span></span> <span data-ttu-id="6dd30-124">Each view contains one or more visualization parts.</span><span class="sxs-lookup"><span data-stu-id="6dd30-124">Each view contains one or more visualization parts.</span></span> |
| <span data-ttu-id="6dd30-125">Visualization parts</span><span class="sxs-lookup"><span data-stu-id="6dd30-125">Visualization parts</span></span> | <span data-ttu-id="6dd30-126">Present a visualization of data in the Log Analytics workspace based on one or more [log searches](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="6dd30-126">Present a visualization of data in the Log Analytics workspace based on one or more [log searches](log-analytics-log-searches.md).</span></span> <span data-ttu-id="6dd30-127">Most parts include a header, which provides a high-level visualization, and a list, which displays the top results.</span><span class="sxs-lookup"><span data-stu-id="6dd30-127">Most parts include a header, which provides a high-level visualization, and a list, which displays the top results.</span></span> <span data-ttu-id="6dd30-128">Each part type provides a different visualization of the records in the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-128">Each part type provides a different visualization of the records in the Log Analytics workspace.</span></span> <span data-ttu-id="6dd30-129">You select elements in the part to perform a log search that provides detailed records.</span><span class="sxs-lookup"><span data-stu-id="6dd30-129">You select elements in the part to perform a log search that provides detailed records.</span></span> |


## <a name="work-with-an-existing-view"></a><span data-ttu-id="6dd30-130">Work with an existing view</span><span class="sxs-lookup"><span data-stu-id="6dd30-130">Work with an existing view</span></span>
<span data-ttu-id="6dd30-131">Views that were created with View Designer display the following options:</span><span class="sxs-lookup"><span data-stu-id="6dd30-131">Views that were created with View Designer display the following options:</span></span>

![Overview menu](media/log-analytics-view-designer/overview-menu.png)

<span data-ttu-id="6dd30-133">The options are described in the following table:</span><span class="sxs-lookup"><span data-stu-id="6dd30-133">The options are described in the following table:</span></span>

| <span data-ttu-id="6dd30-134">Option</span><span class="sxs-lookup"><span data-stu-id="6dd30-134">Option</span></span> | <span data-ttu-id="6dd30-135">Description</span><span class="sxs-lookup"><span data-stu-id="6dd30-135">Description</span></span> |
|:--|:--|
| <span data-ttu-id="6dd30-136">Refresh</span><span class="sxs-lookup"><span data-stu-id="6dd30-136">Refresh</span></span>   | <span data-ttu-id="6dd30-137">Refreshes the view with the latest data.</span><span class="sxs-lookup"><span data-stu-id="6dd30-137">Refreshes the view with the latest data.</span></span> | 
| <span data-ttu-id="6dd30-138">Analytics</span><span class="sxs-lookup"><span data-stu-id="6dd30-138">Analytics</span></span> | <span data-ttu-id="6dd30-139">Opens the [Advanced Analytics portal](log-analytics-log-search-portals.md) to analyze data with log queries.</span><span class="sxs-lookup"><span data-stu-id="6dd30-139">Opens the [Advanced Analytics portal](log-analytics-log-search-portals.md) to analyze data with log queries.</span></span> |
| <span data-ttu-id="6dd30-140">Edit</span><span class="sxs-lookup"><span data-stu-id="6dd30-140">Edit</span></span>       | <span data-ttu-id="6dd30-141">Opens the view in View Designer to edit its contents and configuration.</span><span class="sxs-lookup"><span data-stu-id="6dd30-141">Opens the view in View Designer to edit its contents and configuration.</span></span>  |
| <span data-ttu-id="6dd30-142">Clone</span><span class="sxs-lookup"><span data-stu-id="6dd30-142">Clone</span></span>      | <span data-ttu-id="6dd30-143">Creates a new view and opens it in View Designer.</span><span class="sxs-lookup"><span data-stu-id="6dd30-143">Creates a new view and opens it in View Designer.</span></span> <span data-ttu-id="6dd30-144">The name of the new view is the same as the original name, but with *Copy* appended to it.</span><span class="sxs-lookup"><span data-stu-id="6dd30-144">The name of the new view is the same as the original name, but with *Copy* appended to it.</span></span> |
| <span data-ttu-id="6dd30-145">Date range</span><span class="sxs-lookup"><span data-stu-id="6dd30-145">Date range</span></span> | <span data-ttu-id="6dd30-146">Set the date and time range filter for the data that's included in the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-146">Set the date and time range filter for the data that's included in the view.</span></span> <span data-ttu-id="6dd30-147">This date range is applied before any date ranges set in queries in the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-147">This date range is applied before any date ranges set in queries in the view.</span></span>  |
| +          | <span data-ttu-id="6dd30-148">Define a custom filter that's defined for the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-148">Define a custom filter that's defined for the view.</span></span> |


## <a name="create-a-new-view"></a><span data-ttu-id="6dd30-149">Create a new view</span><span class="sxs-lookup"><span data-stu-id="6dd30-149">Create a new view</span></span>
<span data-ttu-id="6dd30-150">You can create a new view in View Designer by selecting **View Designer** in the menu of your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-150">You can create a new view in View Designer by selecting **View Designer** in the menu of your Log Analytics workspace.</span></span>

![View Designer tile](media/log-analytics-view-designer/view-designer-tile.png)


## <a name="work-with-view-designer"></a><span data-ttu-id="6dd30-152">Work with View Designer</span><span class="sxs-lookup"><span data-stu-id="6dd30-152">Work with View Designer</span></span>
<span data-ttu-id="6dd30-153">You use View Designer to create new views or edit existing ones.</span><span class="sxs-lookup"><span data-stu-id="6dd30-153">You use View Designer to create new views or edit existing ones.</span></span> 

<span data-ttu-id="6dd30-154">View Designer has three panes:</span><span class="sxs-lookup"><span data-stu-id="6dd30-154">View Designer has three panes:</span></span> 
* <span data-ttu-id="6dd30-155">**Design**: Contains the custom view that you're creating or editing.</span><span class="sxs-lookup"><span data-stu-id="6dd30-155">**Design**: Contains the custom view that you're creating or editing.</span></span> 
* <span data-ttu-id="6dd30-156">**Controls**: Contains the tiles and parts that you add to the **Design** pane.</span><span class="sxs-lookup"><span data-stu-id="6dd30-156">**Controls**: Contains the tiles and parts that you add to the **Design** pane.</span></span> 
* <span data-ttu-id="6dd30-157">**Properties**: Displays the properties of the tiles or selected parts.</span><span class="sxs-lookup"><span data-stu-id="6dd30-157">**Properties**: Displays the properties of the tiles or selected parts.</span></span>

![View Designer](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-the-view-tile"></a><span data-ttu-id="6dd30-159">Configure the view tile</span><span class="sxs-lookup"><span data-stu-id="6dd30-159">Configure the view tile</span></span>
<span data-ttu-id="6dd30-160">A custom view can have only a single tile.</span><span class="sxs-lookup"><span data-stu-id="6dd30-160">A custom view can have only a single tile.</span></span> <span data-ttu-id="6dd30-161">To view the current tile or select an alternate one, select the **Tile** tab in the **Control** pane.</span><span class="sxs-lookup"><span data-stu-id="6dd30-161">To view the current tile or select an alternate one, select the **Tile** tab in the **Control** pane.</span></span> <span data-ttu-id="6dd30-162">The **Properties** pane displays the properties of the current tile.</span><span class="sxs-lookup"><span data-stu-id="6dd30-162">The **Properties** pane displays the properties of the current tile.</span></span> 

<span data-ttu-id="6dd30-163">You can configure the tile properties according to the information in the [Tile reference](log-analytics-view-designer-tiles.md) and then click **Apply** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="6dd30-163">You can configure the tile properties according to the information in the [Tile reference](log-analytics-view-designer-tiles.md) and then click **Apply** to save the changes.</span></span>

### <a name="configure-the-visualization-parts"></a><span data-ttu-id="6dd30-164">Configure the visualization parts</span><span class="sxs-lookup"><span data-stu-id="6dd30-164">Configure the visualization parts</span></span>
<span data-ttu-id="6dd30-165">A view can include any number of visualization parts.</span><span class="sxs-lookup"><span data-stu-id="6dd30-165">A view can include any number of visualization parts.</span></span> <span data-ttu-id="6dd30-166">To add parts to a view, select the **View** tab, and then select a visualization part.</span><span class="sxs-lookup"><span data-stu-id="6dd30-166">To add parts to a view, select the **View** tab, and then select a visualization part.</span></span> <span data-ttu-id="6dd30-167">The **Properties** pane displays the properties of the selected part.</span><span class="sxs-lookup"><span data-stu-id="6dd30-167">The **Properties** pane displays the properties of the selected part.</span></span> 

<span data-ttu-id="6dd30-168">You can configure the view properties according to the information in the [Visualization part reference](log-analytics-view-designer-parts.md) and then click **Apply** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="6dd30-168">You can configure the view properties according to the information in the [Visualization part reference](log-analytics-view-designer-parts.md) and then click **Apply** to save the changes.</span></span>

<span data-ttu-id="6dd30-169">Views have only one row of visualization parts.</span><span class="sxs-lookup"><span data-stu-id="6dd30-169">Views have only one row of visualization parts.</span></span> <span data-ttu-id="6dd30-170">You can rearrange the existing parts by dragging them to a new location.</span><span class="sxs-lookup"><span data-stu-id="6dd30-170">You can rearrange the existing parts by dragging them to a new location.</span></span>

<span data-ttu-id="6dd30-171">You can remove a visualization part from the view by selecting the **X** at the top right of the part.</span><span class="sxs-lookup"><span data-stu-id="6dd30-171">You can remove a visualization part from the view by selecting the **X** at the top right of the part.</span></span>


### <a name="menu-options"></a><span data-ttu-id="6dd30-172">Menu options</span><span class="sxs-lookup"><span data-stu-id="6dd30-172">Menu options</span></span>
<span data-ttu-id="6dd30-173">The options for working with views in edit mode are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="6dd30-173">The options for working with views in edit mode are described in the following table.</span></span>

![Edit menu](media/log-analytics-view-designer/edit-menu.png)

| <span data-ttu-id="6dd30-175">Option</span><span class="sxs-lookup"><span data-stu-id="6dd30-175">Option</span></span> | <span data-ttu-id="6dd30-176">Description</span><span class="sxs-lookup"><span data-stu-id="6dd30-176">Description</span></span> |
|:--|:--|
| <span data-ttu-id="6dd30-177">Save</span><span class="sxs-lookup"><span data-stu-id="6dd30-177">Save</span></span>        | <span data-ttu-id="6dd30-178">Saves your changes and closes the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-178">Saves your changes and closes the view.</span></span> |
| <span data-ttu-id="6dd30-179">Cancel</span><span class="sxs-lookup"><span data-stu-id="6dd30-179">Cancel</span></span>      | <span data-ttu-id="6dd30-180">Discards your changes and closes the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-180">Discards your changes and closes the view.</span></span> |
| <span data-ttu-id="6dd30-181">Delete View</span><span class="sxs-lookup"><span data-stu-id="6dd30-181">Delete View</span></span> | <span data-ttu-id="6dd30-182">Deletes the view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-182">Deletes the view.</span></span> |
| <span data-ttu-id="6dd30-183">Export</span><span class="sxs-lookup"><span data-stu-id="6dd30-183">Export</span></span>      | <span data-ttu-id="6dd30-184">Exports the view to an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) that you can import into another workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-184">Exports the view to an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) that you can import into another workspace.</span></span> <span data-ttu-id="6dd30-185">The name of the file is the name of the view, and it has an *omsview* extension.</span><span class="sxs-lookup"><span data-stu-id="6dd30-185">The name of the file is the name of the view, and it has an *omsview* extension.</span></span> |
| <span data-ttu-id="6dd30-186">Import</span><span class="sxs-lookup"><span data-stu-id="6dd30-186">Import</span></span>      | <span data-ttu-id="6dd30-187">Imports the *omsview* file that you exported from another workspace.</span><span class="sxs-lookup"><span data-stu-id="6dd30-187">Imports the *omsview* file that you exported from another workspace.</span></span> <span data-ttu-id="6dd30-188">This action overwrites the configuration of the existing view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-188">This action overwrites the configuration of the existing view.</span></span> |
| <span data-ttu-id="6dd30-189">Clone</span><span class="sxs-lookup"><span data-stu-id="6dd30-189">Clone</span></span>       | <span data-ttu-id="6dd30-190">Creates a new view and opens it in View Designer.</span><span class="sxs-lookup"><span data-stu-id="6dd30-190">Creates a new view and opens it in View Designer.</span></span> <span data-ttu-id="6dd30-191">The name of the new view is the same as the original name, but with *Copy* appended to it.</span><span class="sxs-lookup"><span data-stu-id="6dd30-191">The name of the new view is the same as the original name, but with *Copy* appended to it.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6dd30-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="6dd30-192">Next steps</span></span>
* <span data-ttu-id="6dd30-193">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-193">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span></span>
* <span data-ttu-id="6dd30-194">Add [Visualization parts](log-analytics-view-designer-parts.md) to your custom view.</span><span class="sxs-lookup"><span data-stu-id="6dd30-194">Add [Visualization parts](log-analytics-view-designer-parts.md) to your custom view.</span></span>
