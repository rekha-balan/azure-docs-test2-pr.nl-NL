---
title: Monitor and manage data pipelines - Azure | Microsoft Docs
description: Learn how to use the Monitoring and Management app to monitor and manage Azure data factories and pipelines.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: spelluru
ms.openlocfilehash: a39a90aa8d3dc9b9d305071e026efe6e49780fa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552333"
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a>Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app
> [!div class="op_single_selector"]
> * [Using Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Using Monitoring and Management app](data-factory-monitor-manage-app.md)
>
>

This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Azure Data Factory pipelines--and create alerts to get notified on failures. You can also watch the following video to learn about using the Monitoring and Management app.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>
>

## <a name="open-the-monitoring-and-management-app"></a>Open the Monitoring and Management app
To open the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.

![Monitoring tile on the Data Factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/MonitoringAppTile.png)

You should see the Monitoring and Management app open in a separate window.  

![Monitoring and Management app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.

If you don't see activity windows in the list at the bottom, click the **Refresh** button on the toolbar to refresh the list. In addition, set the right values for the **Start time** and **End time** filters.  

## <a name="understand-the-monitoring-and-management-app"></a>Understand the Monitoring and Management app
There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**. The first tab (**Resource Explorer**) is selected by default.

### <a name="resource-explorer"></a>Resource Explorer
You see the following:

* The Resource Explorer **tree view** in the left pane.
* The **Diagram View** at the top.
* The **Activity Windows** list at the bottom in the middle pane.
* The **Properties** and **Activity Window Explorer** tabs in the right pane.

In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view. When you select an object in Resource Explorer:

* The associated Data Factory entity is highlighted in the Diagram View.
* [Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.  
* The properties of the selected object are shown in the Properties window in the right pane.
* The JSON definition of the selected object is shown, if applicable. For example: a linked service, a dataset, or a pipeline.

![Resource Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ResourceExplorer.png)

See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.

### <a name="diagram-view"></a>Diagram View
The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets. When you select a Data Factory entity (dataset/pipeline) in the Diagram View:

* The data factory entity is selected in the tree view.
* The associated activity windows are highlighted in the Activity Windows list.
* The properties of the selected object are shown in the Properties window.

When the pipeline is enabled (not in a paused state), it's shown with a green line:

![Pipeline running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/PipelineRunning.png)

There are three command bar buttons for the pipeline in the Diagram View. You can use the second button to pause the pipeline. Pausing doesn't terminate the currently running activities and lets them proceed to completion. The third button pauses the pipeline and terminates its existing executing activities. The first button resumes the pipeline. When your pipeline is paused, the color of the pipeline changes to yellow:

![Pause/resume on tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnTile.png)

You can multiselect two or more pipelines by using the Ctrl key. You can use the command bar buttons to pause/resume multiple pipelines at a time.

![Pause/resume on the command bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

You can see all the activities in the pipeline by right-clicking the pipeline tile, and then clicking **Open pipeline**.

![Open pipeline menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

In the opened pipeline view, you see all activities in the pipeline. In this example, there is only one activity: Copy Activity. To go back to the previous view, click the data factory name in the breadcrumb menu at the top.

![Opened pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/OpenedPipeline.png)

In the pipeline view, when you click an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.

![Activity Windows pop-up window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

You can click an activity window to see details for it in the **Properties** window in the right pane.

![Activity window properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

In the right pane, switch to the **Activity Window Explorer** tab to see more details.

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.

![Resolved variables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Switch to the **Script** tab to see the JSON script definition for the selected object.   

![Script tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ScriptTab.png)

You can see activity windows in three places:

* The Activity Windows pop-up in the Diagram View (middle pane).
* The Activity Window Explorer in the right pane.
* The Activity Windows list in the bottom pane.

In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.

![Activity Window Explorer left/right arrows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout. The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View. It's on by default. You can turn it off and move entities around in the diagram. When you turn it off, you can use the last button to automatically position tables and pipelines. You can also zoom in or out by using the mouse wheel.

![Diagram View zoom commands](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Activity Windows list
The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View. By default, the list is in descending order, which means that you see the latest activity window at the top.

![Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsList.png)

This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.  

Activity windows can be in one of the following statuses:

<table>
<tr>
    <th align="left">Status</th><th align="left">Substatus</th><th align="left">Description</th>
</tr>
<tr>
    <td rowspan="8">Waiting</td><td>ScheduleTime</td><td>The time hasn't come for the activity window to run.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>The upstream dependencies aren't ready.</td>
</tr>
<tr>
<td>ComputeResources</td><td>The compute resources aren't available.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>All the activity instances are busy running other activity windows.</td>
</tr>
<tr>
<td>ActivityResume</td><td>The activity is paused and can't run the activity windows until it's resumed.</td>
</tr>
<tr>
<td>Retry</td><td>The activity execution is being retried.</td>
</tr>
<tr>
<td>Validation</td><td>Validation hasn't started yet.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Validation is waiting to be retried.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>Validation is in progress.</td>
</tr>
<td>-</td>
<td>The activity window is being processed.</td>
</tr>
<tr>
<td rowspan="4">Failed</td><td>TimedOut</td><td>The activity execution took longer than what is allowed by the activity.</td>
</tr>
<tr>
<td>Canceled</td><td>The activity window was canceled by user action.</td>
</tr>
<tr>
<td>Validation</td><td>Validation has failed.</td>
</tr>
<tr>
<td>-</td><td>The activity window failed to be generated or validated.</td>
</tr>
<td>Ready</td><td>-</td><td>The activity window is ready for consumption.</td>
</tr>
<tr>
<td>Skipped</td><td>-</td><td>The activity window wasn't processed.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>An activity window used to exist with a different status, but has been reset.</td>
</tr>
</table>


When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Refresh activity windows
The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.  

### <a name="properties-window"></a>Properties window
The Properties window is in the right-most pane of the Monitoring and Management app.

![Properties window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/PropertiesWindow.png)

It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.

### <a name="activity-window-explorer"></a>Activity Window Explorer
The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app. It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

You can switch to another activity window by clicking it in the calendar view at the top. You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.

You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.

### <a name="script"></a>Script
You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).

![Script tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Use system views
The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.

Switch to the **Monitoring Views** tab on the left by clicking it.

![Monitoring Views tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Currently, there are three system views that are supported. Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).

When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.

You can use the **Failed activity windows** view to see all failed activity windows in the list. Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**. You can also download any logs for a failed activity window.

## <a name="sort-and-filter-activity-windows"></a>Sort and filter activity windows
Change the **start time** and **end time** settings in the command bar to filter activity windows. After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.

![Start and end Times](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Currently, all times are in UTC format in the Monitoring and Management app.
>
>

In the **Activity Windows list**, click the name of a column (for example: Status).

![Activity Windows list column menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

You can do the following:

* Sort in ascending order.
* Sort in descending order.
* Filter by one or more values (Ready, Waiting, and so on).

When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.

![Filter on a column of the Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

You can use the same pop-up window to clear filters. To clear all filters for the Activity Windows list, click the clear filter button on the command bar.

![Clear all filters for the Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Perform batch actions
### <a name="rerun-selected-activity-windows"></a>Rerun selected activity windows
Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**. When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.
    ![Rerun an activity window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ReRunSlice.png)

You can also select multiple activity windows in the list and rerun them at the same time. You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail. See the following section for details about filtering activity windows in the list.  

### <a name="pauseresume-multiple-pipelines"></a>Pause/resume multiple pipelines
You can multiselect two or more pipelines by using the Ctrl key. You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.

![Pause/resume on the command bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Create alerts
The **Alerts** page lets you create an alert and view/edit/delete existing alerts. You can also disable/enable an alert. To see the Alerts page, click the **Alerts** tab.

![Alerts tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a>To create an alert
1. Click **Add Alert** to add an alert. You see the **Details** page.

    ![Create Alerts - Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Specify the **Name** and **Description** for the alert, and click **Next**. You should see the **Filters** page.

    ![Create Alerts - Filters page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**. You should see the **Recipients** page.

    ![Create Alerts - Recipients page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**. You should see the alert in the list.

    ![Alerts list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertsList.png)

In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.

### <a name="eventstatussubstatus"></a>Event/status/substatus
The following table provides the list of available events and statuses (and substatuses).

| Event name | Status | Substatus |
| --- | --- | --- |
| Activity Run Started |Started |Starting |
| Activity Run Finished |Succeeded |Succeeded |
| Activity Run Finished |Failed |Failed Resource Allocation<br/><br/>Failed Execution<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| On-Demand HDI Cluster Create Started |Started |-|
| On-Demand HDI Cluster Created Successfully |Succeeded |-|
| On-Demand HDI Cluster Deleted |Succeeded |-|

### <a name="to-edit-delete-or-disable-an-alert"></a>To edit, delete, or disable an alert

Use the following buttons (highlighted in red) to edit, delete, or disable an alert.

![Alerts buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertButtons.png)

































