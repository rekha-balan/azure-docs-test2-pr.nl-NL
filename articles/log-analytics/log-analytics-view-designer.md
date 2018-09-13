---
title: Create views to analyze data in OMS Log Analytics | Microsoft Docs
description: View Designer in Log Analytics allows you to create custom Views that are displayed in the OMS and Azure portal and contain different visualizations of data in the OMS repository. This article contains an overview of View Designer and procedures for creating and editing custom views.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: ''
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: bwren
ms.openlocfilehash: 771567df5634f7a8188d1fd6428652a8522ce83a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556604"
---
# <a name="use-view-designer-to-create-custom-views-in-log-analytics"></a><span data-ttu-id="dcd55-104">Use View Designer to create custom views in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dcd55-104">Use View Designer to create custom views in Log Analytics</span></span>
<span data-ttu-id="dcd55-105">The View Designer in [Log Analytics](log-analytics-overview.md) allows you to create custom views in the OMS console that contain different visualizations of data in the OMS repository.</span><span class="sxs-lookup"><span data-stu-id="dcd55-105">The View Designer in [Log Analytics](log-analytics-overview.md) allows you to create custom views in the OMS console that contain different visualizations of data in the OMS repository.</span></span> <span data-ttu-id="dcd55-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span><span class="sxs-lookup"><span data-stu-id="dcd55-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="dcd55-107">Other articles available for View Designer are:</span><span class="sxs-lookup"><span data-stu-id="dcd55-107">Other articles available for View Designer are:</span></span>

* <span data-ttu-id="dcd55-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of the settings for each of the tiles available to use in your custom views.</span><span class="sxs-lookup"><span data-stu-id="dcd55-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span> 
* <span data-ttu-id="dcd55-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of the settings for each of the tiles available to use in your custom views.</span><span class="sxs-lookup"><span data-stu-id="dcd55-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span> 

## <a name="concepts"></a><span data-ttu-id="dcd55-110">Concepts</span><span class="sxs-lookup"><span data-stu-id="dcd55-110">Concepts</span></span>
<span data-ttu-id="dcd55-111">Views created with the View Designer contain the elements in the following table.</span><span class="sxs-lookup"><span data-stu-id="dcd55-111">Views created with the View Designer contain the elements in the following table.</span></span>

| <span data-ttu-id="dcd55-112">Part</span><span class="sxs-lookup"><span data-stu-id="dcd55-112">Part</span></span> | <span data-ttu-id="dcd55-113">Description</span><span class="sxs-lookup"><span data-stu-id="dcd55-113">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dcd55-114">Tile</span><span class="sxs-lookup"><span data-stu-id="dcd55-114">Tile</span></span> |<span data-ttu-id="dcd55-115">Displayed on the main Log Analytics Overview dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-115">Displayed on the main Log Analytics Overview dashboard.</span></span>  <span data-ttu-id="dcd55-116">Includes a visual summarizing of the information contained in the custom View.</span><span class="sxs-lookup"><span data-stu-id="dcd55-116">Includes a visual summarizing of the information contained in the custom View.</span></span>  <span data-ttu-id="dcd55-117">Different Tile types provide different visualizations of records in the OMS repository.</span><span class="sxs-lookup"><span data-stu-id="dcd55-117">Different Tile types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="dcd55-118">Click on the Tile to open the Custom View.</span><span class="sxs-lookup"><span data-stu-id="dcd55-118">Click on the Tile to open the Custom View.</span></span> |
| <span data-ttu-id="dcd55-119">Custom View</span><span class="sxs-lookup"><span data-stu-id="dcd55-119">Custom View</span></span> |<span data-ttu-id="dcd55-120">Displayed when the user clicks on the Tile.</span><span class="sxs-lookup"><span data-stu-id="dcd55-120">Displayed when the user clicks on the Tile.</span></span>  <span data-ttu-id="dcd55-121">Contains one or more visualization parts.</span><span class="sxs-lookup"><span data-stu-id="dcd55-121">Contains one or more visualization parts.</span></span> |
| <span data-ttu-id="dcd55-122">Visualization Parts</span><span class="sxs-lookup"><span data-stu-id="dcd55-122">Visualization Parts</span></span> |<span data-ttu-id="dcd55-123">Visualization of data in the OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="dcd55-123">Visualization of data in the OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span></span>  <span data-ttu-id="dcd55-124">Most parts will include a Header that provides a high level visualization and a List of the top results.</span><span class="sxs-lookup"><span data-stu-id="dcd55-124">Most parts will include a Header that provides a high level visualization and a List of the top results.</span></span>  <span data-ttu-id="dcd55-125">Different part types provide different visualizations of records in the OMS repository.</span><span class="sxs-lookup"><span data-stu-id="dcd55-125">Different part types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="dcd55-126">Click on elements in the part to perform a log search providing detailed records.</span><span class="sxs-lookup"><span data-stu-id="dcd55-126">Click on elements in the part to perform a log search providing detailed records.</span></span> |

![View Designer overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-to-your-workspace"></a><span data-ttu-id="dcd55-128">Add View Designer to your workspace</span><span class="sxs-lookup"><span data-stu-id="dcd55-128">Add View Designer to your workspace</span></span>
<span data-ttu-id="dcd55-129">While View Designer is in preview, you must add it to your workspace by selecting **Preview Features** in the **Settings** section of the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="dcd55-129">While View Designer is in preview, you must add it to your workspace by selecting **Preview Features** in the **Settings** section of the OMS portal.</span></span>

![Enable preview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a><span data-ttu-id="dcd55-131">Creating and editing views</span><span class="sxs-lookup"><span data-stu-id="dcd55-131">Creating and editing views</span></span>
### <a name="create-a-new-view"></a><span data-ttu-id="dcd55-132">Create a new view</span><span class="sxs-lookup"><span data-stu-id="dcd55-132">Create a new view</span></span>
<span data-ttu-id="dcd55-133">Open a new view in the **View Designer** by clicking on the View Designer tile in the main OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-133">Open a new view in the **View Designer** by clicking on the View Designer tile in the main OMS dashboard.</span></span>

![View Designer tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a><span data-ttu-id="dcd55-135">Edit an existing view</span><span class="sxs-lookup"><span data-stu-id="dcd55-135">Edit an existing view</span></span>
<span data-ttu-id="dcd55-136">To edit an existing view in the View Designer, open the view by clicking on its tile in the main OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-136">To edit an existing view in the View Designer, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="dcd55-137">Then click the **Edit** button to open the view in the View Designer.</span><span class="sxs-lookup"><span data-stu-id="dcd55-137">Then click the **Edit** button to open the view in the View Designer.</span></span>

![Edit a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a><span data-ttu-id="dcd55-139">Clone an existing view</span><span class="sxs-lookup"><span data-stu-id="dcd55-139">Clone an existing view</span></span>
<span data-ttu-id="dcd55-140">When you clone a view, it creates a new view and opens it in the View Designer.</span><span class="sxs-lookup"><span data-stu-id="dcd55-140">When you clone a view, it creates a new view and opens it in the View Designer.</span></span>  <span data-ttu-id="dcd55-141">The new view will have the same name as the original with "Copy" appended to the end of it.</span><span class="sxs-lookup"><span data-stu-id="dcd55-141">The new view will have the same name as the original with "Copy" appended to the end of it.</span></span>  <span data-ttu-id="dcd55-142">To clone a view, open the existing view by clicking on its tile in the main OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-142">To clone a view, open the existing view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="dcd55-143">Then click the **Clone** button to open the view in the View Designer.</span><span class="sxs-lookup"><span data-stu-id="dcd55-143">Then click the **Clone** button to open the view in the View Designer.</span></span>

![Clone a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a><span data-ttu-id="dcd55-145">Delete an existing view</span><span class="sxs-lookup"><span data-stu-id="dcd55-145">Delete an existing view</span></span>
<span data-ttu-id="dcd55-146">To delete an existing view, open the view by clicking on its tile in the main OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-146">To delete an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="dcd55-147">Then click the **Edit** button to open the view in the View Designer, and click **Delete View**.</span><span class="sxs-lookup"><span data-stu-id="dcd55-147">Then click the **Edit** button to open the view in the View Designer, and click **Delete View**.</span></span>

![Delete a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a><span data-ttu-id="dcd55-149">Export an existing view</span><span class="sxs-lookup"><span data-stu-id="dcd55-149">Export an existing view</span></span>
<span data-ttu-id="dcd55-150">You can export a view to a JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dcd55-150">You can export a view to a JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="dcd55-151">To export an existing view, open the view by clicking on its tile in the main OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="dcd55-151">To export an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="dcd55-152">Then click the **Export** button to create a file in the browser's download folder.</span><span class="sxs-lookup"><span data-stu-id="dcd55-152">Then click the **Export** button to create a file in the browser's download folder.</span></span>  <span data-ttu-id="dcd55-153">The name of the file will be the name of the view with the extension *omsview*.</span><span class="sxs-lookup"><span data-stu-id="dcd55-153">The name of the file will be the name of the view with the extension *omsview*.</span></span>

![Export a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a><span data-ttu-id="dcd55-155">Import an existing view</span><span class="sxs-lookup"><span data-stu-id="dcd55-155">Import an existing view</span></span>
<span data-ttu-id="dcd55-156">You can import an *omsview* file that you exported from another management group.</span><span class="sxs-lookup"><span data-stu-id="dcd55-156">You can import an *omsview* file that you exported from another management group.</span></span>  <span data-ttu-id="dcd55-157">To import an existing view, first create a new view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-157">To import an existing view, first create a new view.</span></span>  <span data-ttu-id="dcd55-158">Then click the **Import** button and select the *omsview* file.</span><span class="sxs-lookup"><span data-stu-id="dcd55-158">Then click the **Import** button and select the *omsview* file.</span></span>  <span data-ttu-id="dcd55-159">The configuration in the file will be copied into the existing view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-159">The configuration in the file will be copied into the existing view.</span></span>

![Export a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a><span data-ttu-id="dcd55-161">Working with View Designer</span><span class="sxs-lookup"><span data-stu-id="dcd55-161">Working with View Designer</span></span>
<span data-ttu-id="dcd55-162">The View Designer has three panes.</span><span class="sxs-lookup"><span data-stu-id="dcd55-162">The View Designer has three panes.</span></span>  <span data-ttu-id="dcd55-163">The **Design** pane represents the custom view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-163">The **Design** pane represents the custom view.</span></span>  <span data-ttu-id="dcd55-164">When you add tiles and parts from the **Control** pane to the **Design** pane they are added to the view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-164">When you add tiles and parts from the **Control** pane to the **Design** pane they are added to the view.</span></span>  <span data-ttu-id="dcd55-165">The **Properties** pane will display the properties for the tile or selected part.</span><span class="sxs-lookup"><span data-stu-id="dcd55-165">The **Properties** pane will display the properties for the tile or selected part.</span></span>

![View Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a><span data-ttu-id="dcd55-167">Configure view tile</span><span class="sxs-lookup"><span data-stu-id="dcd55-167">Configure view tile</span></span>
<span data-ttu-id="dcd55-168">A custom view can have only a single tile.</span><span class="sxs-lookup"><span data-stu-id="dcd55-168">A custom view can have only a single tile.</span></span>  <span data-ttu-id="dcd55-169">Select the **Tile** tab in the **Control** pane to view the current tile or select an alternate one.</span><span class="sxs-lookup"><span data-stu-id="dcd55-169">Select the **Tile** tab in the **Control** pane to view the current tile or select an alternate one.</span></span>  <span data-ttu-id="dcd55-170">The **Properties** pane will display the properties for the current tile.</span><span class="sxs-lookup"><span data-stu-id="dcd55-170">The **Properties** pane will display the properties for the current tile.</span></span>  <span data-ttu-id="dcd55-171">Configure the tile properties according to the detailed information in the [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** to save changes.</span><span class="sxs-lookup"><span data-stu-id="dcd55-171">Configure the tile properties according to the detailed information in the [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** to save changes.</span></span>

### <a name="configure-visualization-parts"></a><span data-ttu-id="dcd55-172">Configure visualization parts</span><span class="sxs-lookup"><span data-stu-id="dcd55-172">Configure visualization parts</span></span>
<span data-ttu-id="dcd55-173">A view can include any number of visualization parts.</span><span class="sxs-lookup"><span data-stu-id="dcd55-173">A view can include any number of visualization parts.</span></span>  <span data-ttu-id="dcd55-174">Select the **View** tab and then a visualization part to add to the view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-174">Select the **View** tab and then a visualization part to add to the view.</span></span>  <span data-ttu-id="dcd55-175">The **Properties** pane will display the properties for the selected part.</span><span class="sxs-lookup"><span data-stu-id="dcd55-175">The **Properties** pane will display the properties for the selected part.</span></span>  <span data-ttu-id="dcd55-176">Configure the view properties according to the detailed information in the [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** to save changes.</span><span class="sxs-lookup"><span data-stu-id="dcd55-176">Configure the view properties according to the detailed information in the [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** to save changes.</span></span>

### <a name="delete-a-visualization-part"></a><span data-ttu-id="dcd55-177">Delete a visualization part</span><span class="sxs-lookup"><span data-stu-id="dcd55-177">Delete a visualization part</span></span>
<span data-ttu-id="dcd55-178">You can remove a visualization part from the view by clicking the **X** button in the top right corner of the part.</span><span class="sxs-lookup"><span data-stu-id="dcd55-178">You can remove a visualization part from the view by clicking the **X** button in the top right corner of the part.</span></span>

### <a name="rearrange-visualization-parts"></a><span data-ttu-id="dcd55-179">Rearrange visualization parts</span><span class="sxs-lookup"><span data-stu-id="dcd55-179">Rearrange visualization parts</span></span>
<span data-ttu-id="dcd55-180">Views only have one row of visualization parts.</span><span class="sxs-lookup"><span data-stu-id="dcd55-180">Views only have one row of visualization parts.</span></span>  <span data-ttu-id="dcd55-181">Rearrange existing parts in a view by clicking and dragging them to a new location.</span><span class="sxs-lookup"><span data-stu-id="dcd55-181">Rearrange existing parts in a view by clicking and dragging them to a new location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcd55-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="dcd55-182">Next steps</span></span>
* <span data-ttu-id="dcd55-183">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-183">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span></span>
* <span data-ttu-id="dcd55-184">Add [Visualization Parts](log-analytics-view-designer-parts.md) to your custom view.</span><span class="sxs-lookup"><span data-stu-id="dcd55-184">Add [Visualization Parts](log-analytics-view-designer-parts.md) to your custom view.</span></span>










