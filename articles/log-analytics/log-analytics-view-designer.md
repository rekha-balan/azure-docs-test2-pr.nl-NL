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
# <a name="use-view-designer-to-create-custom-views-in-log-analytics"></a>Use View Designer to create custom views in Log Analytics
The View Designer in [Log Analytics](log-analytics-overview.md) allows you to create custom views in the OMS console that contain different visualizations of data in the OMS repository. This article contains an overview of View Designer and procedures for creating and editing custom views.

Other articles available for View Designer are:

* [Tile reference](log-analytics-view-designer-tiles.md) - Reference of the settings for each of the tiles available to use in your custom views. 
* [Visualization part reference](log-analytics-view-designer-parts.md) - Reference of the settings for each of the tiles available to use in your custom views. 

## <a name="concepts"></a>Concepts
Views created with the View Designer contain the elements in the following table.

| Part | Description |
|:--- |:--- |
| Tile |Displayed on the main Log Analytics Overview dashboard.  Includes a visual summarizing of the information contained in the custom View.  Different Tile types provide different visualizations of records in the OMS repository.  Click on the Tile to open the Custom View. |
| Custom View |Displayed when the user clicks on the Tile.  Contains one or more visualization parts. |
| Visualization Parts |Visualization of data in the OMS repository based on one or more [log searches](log-analytics-log-searches.md).  Most parts will include a Header that provides a high level visualization and a List of the top results.  Different part types provide different visualizations of records in the OMS repository.  Click on elements in the part to perform a log search providing detailed records. |

![View Designer overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-to-your-workspace"></a>Add View Designer to your workspace
While View Designer is in preview, you must add it to your workspace by selecting **Preview Features** in the **Settings** section of the OMS portal.

![Enable preview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Creating and editing views
### <a name="create-a-new-view"></a>Create a new view
Open a new view in the **View Designer** by clicking on the View Designer tile in the main OMS dashboard.

![View Designer tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Edit an existing view
To edit an existing view in the View Designer, open the view by clicking on its tile in the main OMS dashboard.  Then click the **Edit** button to open the view in the View Designer.

![Edit a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Clone an existing view
When you clone a view, it creates a new view and opens it in the View Designer.  The new view will have the same name as the original with "Copy" appended to the end of it.  To clone a view, open the existing view by clicking on its tile in the main OMS dashboard.  Then click the **Clone** button to open the view in the View Designer.

![Clone a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Delete an existing view
To delete an existing view, open the view by clicking on its tile in the main OMS dashboard.  Then click the **Edit** button to open the view in the View Designer, and click **Delete View**.

![Delete a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Export an existing view
You can export a view to a JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).  To export an existing view, open the view by clicking on its tile in the main OMS dashboard.  Then click the **Export** button to create a file in the browser's download folder.  The name of the file will be the name of the view with the extension *omsview*.

![Export a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Import an existing view
You can import an *omsview* file that you exported from another management group.  To import an existing view, first create a new view.  Then click the **Import** button and select the *omsview* file.  The configuration in the file will be copied into the existing view.

![Export a view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Working with View Designer
The View Designer has three panes.  The **Design** pane represents the custom view.  When you add tiles and parts from the **Control** pane to the **Design** pane they are added to the view.  The **Properties** pane will display the properties for the tile or selected part.

![View Designer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Configure view tile
A custom view can have only a single tile.  Select the **Tile** tab in the **Control** pane to view the current tile or select an alternate one.  The **Properties** pane will display the properties for the current tile.  Configure the tile properties according to the detailed information in the [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** to save changes.

### <a name="configure-visualization-parts"></a>Configure visualization parts
A view can include any number of visualization parts.  Select the **View** tab and then a visualization part to add to the view.  The **Properties** pane will display the properties for the selected part.  Configure the view properties according to the detailed information in the [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** to save changes.

### <a name="delete-a-visualization-part"></a>Delete a visualization part
You can remove a visualization part from the view by clicking the **X** button in the top right corner of the part.

### <a name="rearrange-visualization-parts"></a>Rearrange visualization parts
Views only have one row of visualization parts.  Rearrange existing parts in a view by clicking and dragging them to a new location.

## <a name="next-steps"></a>Next steps
* Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.
* Add [Visualization Parts](log-analytics-view-designer-parts.md) to your custom view.










