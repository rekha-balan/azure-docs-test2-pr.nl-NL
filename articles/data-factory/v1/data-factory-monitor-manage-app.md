---
title: Monitor and manage data pipelines - Azure | Microsoft Docs
description: Learn how to use the Monitoring and Management app to monitor and manage Azure data factories and pipelines.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 3f234e49f1a28fd0881e47ede13ae72483ed31f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871238"
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="d3a80-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="d3a80-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [Using Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Using Monitoring and Management app](data-factory-monitor-manage-app.md)
>
>

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [monitor and manage Data Factory pipelines in](../monitor-visually.md).

<span data-ttu-id="d3a80-108">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="d3a80-108">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="d3a80-109">You can get started with using the application by watching the following video:</span><span class="sxs-lookup"><span data-stu-id="d3a80-109">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> The user interface shown in the video may not exactly match what you see in the portal. It's slightly older, but concepts remain the same. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="d3a80-112">Launch the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="d3a80-112">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="d3a80-113">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span><span class="sxs-lookup"><span data-stu-id="d3a80-113">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Monitoring tile on the Data Factory home page](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="d3a80-115">You should see the Monitoring and Management app open in a separate window.</span><span class="sxs-lookup"><span data-stu-id="d3a80-115">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Monitoring and Management app](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.


<span data-ttu-id="d3a80-118">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span><span class="sxs-lookup"><span data-stu-id="d3a80-118">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="d3a80-119">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span><span class="sxs-lookup"><span data-stu-id="d3a80-119">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="d3a80-120">If you don't see activity windows in the list at the bottom, do the following:</span><span class="sxs-lookup"><span data-stu-id="d3a80-120">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="d3a80-121">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span><span class="sxs-lookup"><span data-stu-id="d3a80-121">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="d3a80-122">The Activity Windows list is not automatically refreshed.</span><span class="sxs-lookup"><span data-stu-id="d3a80-122">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="d3a80-123">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-123">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="d3a80-124">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d3a80-124">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="d3a80-125">Understand the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="d3a80-125">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="d3a80-126">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span><span class="sxs-lookup"><span data-stu-id="d3a80-126">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="d3a80-127">The first tab (**Resource Explorer**) is selected by default.</span><span class="sxs-lookup"><span data-stu-id="d3a80-127">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="d3a80-128">Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="d3a80-128">Resource Explorer</span></span>
<span data-ttu-id="d3a80-129">You see the following:</span><span class="sxs-lookup"><span data-stu-id="d3a80-129">You see the following:</span></span>

* <span data-ttu-id="d3a80-130">The Resource Explorer **tree view** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-130">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="d3a80-131">The **Diagram View** at the top in the middle pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-131">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="d3a80-132">The **Activity Windows** list at the bottom in the middle pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-132">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="d3a80-133">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-133">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="d3a80-134">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span><span class="sxs-lookup"><span data-stu-id="d3a80-134">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="d3a80-135">When you select an object in Resource Explorer:</span><span class="sxs-lookup"><span data-stu-id="d3a80-135">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="d3a80-136">The associated Data Factory entity is highlighted in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="d3a80-136">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="d3a80-137">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d3a80-137">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="d3a80-138">The properties of the selected object are shown in the Properties window in the right pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-138">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="d3a80-139">The JSON definition of the selected object is shown, if applicable.</span><span class="sxs-lookup"><span data-stu-id="d3a80-139">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="d3a80-140">For example: a linked service, a dataset, or a pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-140">For example: a linked service, a dataset, or a pipeline.</span></span>

![Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="d3a80-142">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span><span class="sxs-lookup"><span data-stu-id="d3a80-142">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="d3a80-143">Diagram View</span><span class="sxs-lookup"><span data-stu-id="d3a80-143">Diagram View</span></span>
<span data-ttu-id="d3a80-144">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span><span class="sxs-lookup"><span data-stu-id="d3a80-144">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="d3a80-145">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span><span class="sxs-lookup"><span data-stu-id="d3a80-145">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="d3a80-146">The data factory entity is selected in the tree view.</span><span class="sxs-lookup"><span data-stu-id="d3a80-146">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="d3a80-147">The associated activity windows are highlighted in the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-147">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="d3a80-148">The properties of the selected object are shown in the Properties window.</span><span class="sxs-lookup"><span data-stu-id="d3a80-148">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="d3a80-149">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span><span class="sxs-lookup"><span data-stu-id="d3a80-149">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline running](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="d3a80-151">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span><span class="sxs-lookup"><span data-stu-id="d3a80-151">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Pause/resume on the command bar](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="d3a80-153">There are three command bar buttons for the pipeline in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="d3a80-153">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="d3a80-154">You can use the second button to pause the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-154">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="d3a80-155">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span><span class="sxs-lookup"><span data-stu-id="d3a80-155">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="d3a80-156">The third button pauses the pipeline and terminates its existing executing activities.</span><span class="sxs-lookup"><span data-stu-id="d3a80-156">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="d3a80-157">The first button resumes the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-157">The first button resumes the pipeline.</span></span> <span data-ttu-id="d3a80-158">When your pipeline is paused, the color of the pipeline changes.</span><span class="sxs-lookup"><span data-stu-id="d3a80-158">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="d3a80-159">For example, a paused pipeline looks like in the following image:</span><span class="sxs-lookup"><span data-stu-id="d3a80-159">For example, a paused pipeline looks like in the following image:</span></span> 

![Pipeline paused](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="d3a80-161">You can multi-select two or more pipelines by using the Ctrl key.</span><span class="sxs-lookup"><span data-stu-id="d3a80-161">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="d3a80-162">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span><span class="sxs-lookup"><span data-stu-id="d3a80-162">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="d3a80-163">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-163">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Context menu for pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="d3a80-165">Click the **Open pipeline** option to see all the activities in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-165">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Open pipeline menu](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="d3a80-167">In the opened pipeline view, you see all activities in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3a80-167">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="d3a80-168">In this example, there is only one activity: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="d3a80-168">In this example, there is only one activity: Copy Activity.</span></span> 

![Opened pipeline](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="d3a80-170">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="d3a80-170">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="d3a80-171">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span><span class="sxs-lookup"><span data-stu-id="d3a80-171">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Activity Windows pop-up window](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="d3a80-173">You can click an activity window to see details for it in the **Properties** window in the right pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-173">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Activity window properties](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="d3a80-175">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span><span class="sxs-lookup"><span data-stu-id="d3a80-175">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="d3a80-177">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span><span class="sxs-lookup"><span data-stu-id="d3a80-177">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Resolved variables](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="d3a80-179">Switch to the **Script** tab to see the JSON script definition for the selected object.</span><span class="sxs-lookup"><span data-stu-id="d3a80-179">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Script tab](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="d3a80-181">You can see activity windows in three places:</span><span class="sxs-lookup"><span data-stu-id="d3a80-181">You can see activity windows in three places:</span></span>

* <span data-ttu-id="d3a80-182">The Activity Windows pop-up in the Diagram View (middle pane).</span><span class="sxs-lookup"><span data-stu-id="d3a80-182">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="d3a80-183">The Activity Window Explorer in the right pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-183">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="d3a80-184">The Activity Windows list in the bottom pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-184">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="d3a80-185">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span><span class="sxs-lookup"><span data-stu-id="d3a80-185">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Activity Window Explorer left/right arrows](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="d3a80-187">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span><span class="sxs-lookup"><span data-stu-id="d3a80-187">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="d3a80-188">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="d3a80-188">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="d3a80-189">It's on by default.</span><span class="sxs-lookup"><span data-stu-id="d3a80-189">It's on by default.</span></span> <span data-ttu-id="d3a80-190">You can turn it off and move entities around in the diagram.</span><span class="sxs-lookup"><span data-stu-id="d3a80-190">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="d3a80-191">When you turn it off, you can use the last button to automatically position tables and pipelines.</span><span class="sxs-lookup"><span data-stu-id="d3a80-191">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="d3a80-192">You can also zoom in or out by using the mouse wheel.</span><span class="sxs-lookup"><span data-stu-id="d3a80-192">You can also zoom in or out by using the mouse wheel.</span></span>

![Diagram View zoom commands](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="d3a80-194">Activity Windows list</span><span class="sxs-lookup"><span data-stu-id="d3a80-194">Activity Windows list</span></span>
<span data-ttu-id="d3a80-195">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="d3a80-195">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="d3a80-196">By default, the list is in descending order, which means that you see the latest activity window at the top.</span><span class="sxs-lookup"><span data-stu-id="d3a80-196">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Activity Windows list](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="d3a80-198">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span><span class="sxs-lookup"><span data-stu-id="d3a80-198">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="d3a80-199">Activity windows can be in one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="d3a80-199">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="d3a80-200">Status</span><span class="sxs-lookup"><span data-stu-id="d3a80-200">Status</span></span></th><th align="left"><span data-ttu-id="d3a80-201">Substatus</span><span class="sxs-lookup"><span data-stu-id="d3a80-201">Substatus</span></span></th><th align="left"><span data-ttu-id="d3a80-202">Description</span><span class="sxs-lookup"><span data-stu-id="d3a80-202">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="d3a80-203">Waiting</span><span class="sxs-lookup"><span data-stu-id="d3a80-203">Waiting</span></span></td><td><span data-ttu-id="d3a80-204">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="d3a80-204">ScheduleTime</span></span></td><td><span data-ttu-id="d3a80-205">The time hasn't come for the activity window to run.</span><span class="sxs-lookup"><span data-stu-id="d3a80-205">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-206">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="d3a80-206">DatasetDependencies</span></span></td><td><span data-ttu-id="d3a80-207">The upstream dependencies aren't ready.</span><span class="sxs-lookup"><span data-stu-id="d3a80-207">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-208">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="d3a80-208">ComputeResources</span></span></td><td><span data-ttu-id="d3a80-209">The compute resources aren't available.</span><span class="sxs-lookup"><span data-stu-id="d3a80-209">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-210">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="d3a80-210">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="d3a80-211">All the activity instances are busy running other activity windows.</span><span class="sxs-lookup"><span data-stu-id="d3a80-211">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-212">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="d3a80-212">ActivityResume</span></span></td><td><span data-ttu-id="d3a80-213">The activity is paused and can't run the activity windows until it's resumed.</span><span class="sxs-lookup"><span data-stu-id="d3a80-213">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-214">Retry</span><span class="sxs-lookup"><span data-stu-id="d3a80-214">Retry</span></span></td><td><span data-ttu-id="d3a80-215">The activity execution is being retried.</span><span class="sxs-lookup"><span data-stu-id="d3a80-215">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-216">Validation</span><span class="sxs-lookup"><span data-stu-id="d3a80-216">Validation</span></span></td><td><span data-ttu-id="d3a80-217">Validation hasn't started yet.</span><span class="sxs-lookup"><span data-stu-id="d3a80-217">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-218">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="d3a80-218">ValidationRetry</span></span></td><td><span data-ttu-id="d3a80-219">Validation is waiting to be retried.</span><span class="sxs-lookup"><span data-stu-id="d3a80-219">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="d3a80-220">InProgress</span><span class="sxs-lookup"><span data-stu-id="d3a80-220">InProgress</span></span></td><td><span data-ttu-id="d3a80-221">Validating</span><span class="sxs-lookup"><span data-stu-id="d3a80-221">Validating</span></span></td><td><span data-ttu-id="d3a80-222">Validation is in progress.</span><span class="sxs-lookup"><span data-stu-id="d3a80-222">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="d3a80-223">The activity window is being processed.</span><span class="sxs-lookup"><span data-stu-id="d3a80-223">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="d3a80-224">Failed</span><span class="sxs-lookup"><span data-stu-id="d3a80-224">Failed</span></span></td><td><span data-ttu-id="d3a80-225">TimedOut</span><span class="sxs-lookup"><span data-stu-id="d3a80-225">TimedOut</span></span></td><td><span data-ttu-id="d3a80-226">The activity execution took longer than what is allowed by the activity.</span><span class="sxs-lookup"><span data-stu-id="d3a80-226">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-227">Canceled</span><span class="sxs-lookup"><span data-stu-id="d3a80-227">Canceled</span></span></td><td><span data-ttu-id="d3a80-228">The activity window was canceled by user action.</span><span class="sxs-lookup"><span data-stu-id="d3a80-228">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-229">Validation</span><span class="sxs-lookup"><span data-stu-id="d3a80-229">Validation</span></span></td><td><span data-ttu-id="d3a80-230">Validation has failed.</span><span class="sxs-lookup"><span data-stu-id="d3a80-230">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="d3a80-231">The activity window failed to be generated or validated.</span><span class="sxs-lookup"><span data-stu-id="d3a80-231">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="d3a80-232">Ready</span><span class="sxs-lookup"><span data-stu-id="d3a80-232">Ready</span></span></td><td>-</td><td><span data-ttu-id="d3a80-233">The activity window is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="d3a80-233">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-234">Skipped</span><span class="sxs-lookup"><span data-stu-id="d3a80-234">Skipped</span></span></td><td>-</td><td><span data-ttu-id="d3a80-235">The activity window wasn't processed.</span><span class="sxs-lookup"><span data-stu-id="d3a80-235">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d3a80-236">None</span><span class="sxs-lookup"><span data-stu-id="d3a80-236">None</span></span></td><td>-</td><td><span data-ttu-id="d3a80-237">An activity window used to exist with a different status, but has been reset.</span><span class="sxs-lookup"><span data-stu-id="d3a80-237">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="d3a80-238">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span><span class="sxs-lookup"><span data-stu-id="d3a80-238">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="d3a80-240">Refresh activity windows</span><span class="sxs-lookup"><span data-stu-id="d3a80-240">Refresh activity windows</span></span>
<span data-ttu-id="d3a80-241">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-241">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="d3a80-242">Properties window</span><span class="sxs-lookup"><span data-stu-id="d3a80-242">Properties window</span></span>
<span data-ttu-id="d3a80-243">The Properties window is in the right-most pane of the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="d3a80-243">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Properties window](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="d3a80-245">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-245">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="d3a80-246">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="d3a80-246">Activity Window Explorer</span></span>
<span data-ttu-id="d3a80-247">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="d3a80-247">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="d3a80-248">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-248">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="d3a80-250">You can switch to another activity window by clicking it in the calendar view at the top.</span><span class="sxs-lookup"><span data-stu-id="d3a80-250">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="d3a80-251">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span><span class="sxs-lookup"><span data-stu-id="d3a80-251">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="d3a80-252">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span><span class="sxs-lookup"><span data-stu-id="d3a80-252">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="d3a80-253">Script</span><span class="sxs-lookup"><span data-stu-id="d3a80-253">Script</span></span>
<span data-ttu-id="d3a80-254">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span><span class="sxs-lookup"><span data-stu-id="d3a80-254">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Script tab](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="d3a80-256">Use system views</span><span class="sxs-lookup"><span data-stu-id="d3a80-256">Use system views</span></span>
<span data-ttu-id="d3a80-257">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span><span class="sxs-lookup"><span data-stu-id="d3a80-257">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="d3a80-258">Switch to the **Monitoring Views** tab on the left by clicking it.</span><span class="sxs-lookup"><span data-stu-id="d3a80-258">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Monitoring Views tab](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="d3a80-260">Currently, there are three system views that are supported.</span><span class="sxs-lookup"><span data-stu-id="d3a80-260">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="d3a80-261">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span><span class="sxs-lookup"><span data-stu-id="d3a80-261">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="d3a80-262">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span><span class="sxs-lookup"><span data-stu-id="d3a80-262">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="d3a80-263">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-263">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="d3a80-264">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d3a80-264">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="d3a80-265">You can also download any logs for a failed activity window.</span><span class="sxs-lookup"><span data-stu-id="d3a80-265">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="d3a80-266">Sort and filter activity windows</span><span class="sxs-lookup"><span data-stu-id="d3a80-266">Sort and filter activity windows</span></span>
<span data-ttu-id="d3a80-267">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span><span class="sxs-lookup"><span data-stu-id="d3a80-267">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="d3a80-268">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-268">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Start and end Times](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Currently, all times are in UTC format in the Monitoring and Management app.
>
>

<span data-ttu-id="d3a80-271">In the **Activity Windows list**, click the name of a column (for example: Status).</span><span class="sxs-lookup"><span data-stu-id="d3a80-271">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Activity Windows list column menu](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="d3a80-273">You can do the following:</span><span class="sxs-lookup"><span data-stu-id="d3a80-273">You can do the following:</span></span>

* <span data-ttu-id="d3a80-274">Sort in ascending order.</span><span class="sxs-lookup"><span data-stu-id="d3a80-274">Sort in ascending order.</span></span>
* <span data-ttu-id="d3a80-275">Sort in descending order.</span><span class="sxs-lookup"><span data-stu-id="d3a80-275">Sort in descending order.</span></span>
* <span data-ttu-id="d3a80-276">Filter by one or more values (Ready, Waiting, and so on).</span><span class="sxs-lookup"><span data-stu-id="d3a80-276">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="d3a80-277">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span><span class="sxs-lookup"><span data-stu-id="d3a80-277">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filter on a column of the Activity Windows list](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="d3a80-279">You can use the same pop-up window to clear filters.</span><span class="sxs-lookup"><span data-stu-id="d3a80-279">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="d3a80-280">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="d3a80-280">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Clear all filters for the Activity Windows list](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="d3a80-282">Perform batch actions</span><span class="sxs-lookup"><span data-stu-id="d3a80-282">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="d3a80-283">Rerun selected activity windows</span><span class="sxs-lookup"><span data-stu-id="d3a80-283">Rerun selected activity windows</span></span>
<span data-ttu-id="d3a80-284">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span><span class="sxs-lookup"><span data-stu-id="d3a80-284">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="d3a80-285">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span><span class="sxs-lookup"><span data-stu-id="d3a80-285">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="d3a80-286">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="d3a80-286">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="d3a80-287">You can also select multiple activity windows in the list and rerun them at the same time.</span><span class="sxs-lookup"><span data-stu-id="d3a80-287">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="d3a80-288">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span><span class="sxs-lookup"><span data-stu-id="d3a80-288">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="d3a80-289">See the following section for details about filtering activity windows in the list.</span><span class="sxs-lookup"><span data-stu-id="d3a80-289">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="d3a80-290">Pause/resume multiple pipelines</span><span class="sxs-lookup"><span data-stu-id="d3a80-290">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="d3a80-291">You can multiselect two or more pipelines by using the Ctrl key.</span><span class="sxs-lookup"><span data-stu-id="d3a80-291">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="d3a80-292">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span><span class="sxs-lookup"><span data-stu-id="d3a80-292">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Pause/resume on the command bar](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
