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
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="532ac-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="532ac-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [Using Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Using Monitoring and Management app](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="532ac-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Azure Data Factory pipelines--and create alerts to get notified on failures.</span><span class="sxs-lookup"><span data-stu-id="532ac-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Azure Data Factory pipelines--and create alerts to get notified on failures.</span></span> <span data-ttu-id="532ac-107">You can also watch the following video to learn about using the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="532ac-107">You can also watch the following video to learn about using the Monitoring and Management app.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>
>

## <a name="open-the-monitoring-and-management-app"></a><span data-ttu-id="532ac-108">Open the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="532ac-108">Open the Monitoring and Management app</span></span>
<span data-ttu-id="532ac-109">To open the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span><span class="sxs-lookup"><span data-stu-id="532ac-109">To open the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Monitoring tile on the Data Factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="532ac-111">You should see the Monitoring and Management app open in a separate window.</span><span class="sxs-lookup"><span data-stu-id="532ac-111">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Monitoring and Management app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.

<span data-ttu-id="532ac-114">If you don't see activity windows in the list at the bottom, click the **Refresh** button on the toolbar to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="532ac-114">If you don't see activity windows in the list at the bottom, click the **Refresh** button on the toolbar to refresh the list.</span></span> <span data-ttu-id="532ac-115">In addition, set the right values for the **Start time** and **End time** filters.</span><span class="sxs-lookup"><span data-stu-id="532ac-115">In addition, set the right values for the **Start time** and **End time** filters.</span></span>  

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="532ac-116">Understand the Monitoring and Management app</span><span class="sxs-lookup"><span data-stu-id="532ac-116">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="532ac-117">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span><span class="sxs-lookup"><span data-stu-id="532ac-117">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="532ac-118">The first tab (**Resource Explorer**) is selected by default.</span><span class="sxs-lookup"><span data-stu-id="532ac-118">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="532ac-119">Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="532ac-119">Resource Explorer</span></span>
<span data-ttu-id="532ac-120">You see the following:</span><span class="sxs-lookup"><span data-stu-id="532ac-120">You see the following:</span></span>

* <span data-ttu-id="532ac-121">The Resource Explorer **tree view** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-121">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="532ac-122">The **Diagram View** at the top.</span><span class="sxs-lookup"><span data-stu-id="532ac-122">The **Diagram View** at the top.</span></span>
* <span data-ttu-id="532ac-123">The **Activity Windows** list at the bottom in the middle pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-123">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="532ac-124">The **Properties** and **Activity Window Explorer** tabs in the right pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-124">The **Properties** and **Activity Window Explorer** tabs in the right pane.</span></span>

<span data-ttu-id="532ac-125">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span><span class="sxs-lookup"><span data-stu-id="532ac-125">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="532ac-126">When you select an object in Resource Explorer:</span><span class="sxs-lookup"><span data-stu-id="532ac-126">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="532ac-127">The associated Data Factory entity is highlighted in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="532ac-127">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="532ac-128">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="532ac-128">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="532ac-129">The properties of the selected object are shown in the Properties window in the right pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-129">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="532ac-130">The JSON definition of the selected object is shown, if applicable.</span><span class="sxs-lookup"><span data-stu-id="532ac-130">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="532ac-131">For example: a linked service, a dataset, or a pipeline.</span><span class="sxs-lookup"><span data-stu-id="532ac-131">For example: a linked service, a dataset, or a pipeline.</span></span>

![Resource Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="532ac-133">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span><span class="sxs-lookup"><span data-stu-id="532ac-133">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="532ac-134">Diagram View</span><span class="sxs-lookup"><span data-stu-id="532ac-134">Diagram View</span></span>
<span data-ttu-id="532ac-135">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span><span class="sxs-lookup"><span data-stu-id="532ac-135">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="532ac-136">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span><span class="sxs-lookup"><span data-stu-id="532ac-136">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="532ac-137">The data factory entity is selected in the tree view.</span><span class="sxs-lookup"><span data-stu-id="532ac-137">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="532ac-138">The associated activity windows are highlighted in the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="532ac-138">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="532ac-139">The properties of the selected object are shown in the Properties window.</span><span class="sxs-lookup"><span data-stu-id="532ac-139">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="532ac-140">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span><span class="sxs-lookup"><span data-stu-id="532ac-140">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pipeline running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="532ac-142">There are three command bar buttons for the pipeline in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="532ac-142">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="532ac-143">You can use the second button to pause the pipeline.</span><span class="sxs-lookup"><span data-stu-id="532ac-143">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="532ac-144">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span><span class="sxs-lookup"><span data-stu-id="532ac-144">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="532ac-145">The third button pauses the pipeline and terminates its existing executing activities.</span><span class="sxs-lookup"><span data-stu-id="532ac-145">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="532ac-146">The first button resumes the pipeline.</span><span class="sxs-lookup"><span data-stu-id="532ac-146">The first button resumes the pipeline.</span></span> <span data-ttu-id="532ac-147">When your pipeline is paused, the color of the pipeline changes to yellow:</span><span class="sxs-lookup"><span data-stu-id="532ac-147">When your pipeline is paused, the color of the pipeline changes to yellow:</span></span>

![Pause/resume on tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnTile.png)

<span data-ttu-id="532ac-149">You can multiselect two or more pipelines by using the Ctrl key.</span><span class="sxs-lookup"><span data-stu-id="532ac-149">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="532ac-150">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span><span class="sxs-lookup"><span data-stu-id="532ac-150">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

![Pause/resume on the command bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

<span data-ttu-id="532ac-152">You can see all the activities in the pipeline by right-clicking the pipeline tile, and then clicking **Open pipeline**.</span><span class="sxs-lookup"><span data-stu-id="532ac-152">You can see all the activities in the pipeline by right-clicking the pipeline tile, and then clicking **Open pipeline**.</span></span>

![Open pipeline menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="532ac-154">In the opened pipeline view, you see all activities in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="532ac-154">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="532ac-155">In this example, there is only one activity: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="532ac-155">In this example, there is only one activity: Copy Activity.</span></span> <span data-ttu-id="532ac-156">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="532ac-156">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

![Opened pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="532ac-158">In the pipeline view, when you click an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span><span class="sxs-lookup"><span data-stu-id="532ac-158">In the pipeline view, when you click an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Activity Windows pop-up window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="532ac-160">You can click an activity window to see details for it in the **Properties** window in the right pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-160">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Activity window properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="532ac-162">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span><span class="sxs-lookup"><span data-stu-id="532ac-162">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="532ac-164">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span><span class="sxs-lookup"><span data-stu-id="532ac-164">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Resolved variables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="532ac-166">Switch to the **Script** tab to see the JSON script definition for the selected object.</span><span class="sxs-lookup"><span data-stu-id="532ac-166">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Script tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="532ac-168">You can see activity windows in three places:</span><span class="sxs-lookup"><span data-stu-id="532ac-168">You can see activity windows in three places:</span></span>

* <span data-ttu-id="532ac-169">The Activity Windows pop-up in the Diagram View (middle pane).</span><span class="sxs-lookup"><span data-stu-id="532ac-169">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="532ac-170">The Activity Window Explorer in the right pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-170">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="532ac-171">The Activity Windows list in the bottom pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-171">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="532ac-172">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span><span class="sxs-lookup"><span data-stu-id="532ac-172">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Activity Window Explorer left/right arrows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="532ac-174">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span><span class="sxs-lookup"><span data-stu-id="532ac-174">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="532ac-175">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="532ac-175">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="532ac-176">It's on by default.</span><span class="sxs-lookup"><span data-stu-id="532ac-176">It's on by default.</span></span> <span data-ttu-id="532ac-177">You can turn it off and move entities around in the diagram.</span><span class="sxs-lookup"><span data-stu-id="532ac-177">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="532ac-178">When you turn it off, you can use the last button to automatically position tables and pipelines.</span><span class="sxs-lookup"><span data-stu-id="532ac-178">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="532ac-179">You can also zoom in or out by using the mouse wheel.</span><span class="sxs-lookup"><span data-stu-id="532ac-179">You can also zoom in or out by using the mouse wheel.</span></span>

![Diagram View zoom commands](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="532ac-181">Activity Windows list</span><span class="sxs-lookup"><span data-stu-id="532ac-181">Activity Windows list</span></span>
<span data-ttu-id="532ac-182">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span><span class="sxs-lookup"><span data-stu-id="532ac-182">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="532ac-183">By default, the list is in descending order, which means that you see the latest activity window at the top.</span><span class="sxs-lookup"><span data-stu-id="532ac-183">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="532ac-185">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span><span class="sxs-lookup"><span data-stu-id="532ac-185">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="532ac-186">Activity windows can be in one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="532ac-186">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="532ac-187">Status</span><span class="sxs-lookup"><span data-stu-id="532ac-187">Status</span></span></th><th align="left"><span data-ttu-id="532ac-188">Substatus</span><span class="sxs-lookup"><span data-stu-id="532ac-188">Substatus</span></span></th><th align="left"><span data-ttu-id="532ac-189">Description</span><span class="sxs-lookup"><span data-stu-id="532ac-189">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="532ac-190">Waiting</span><span class="sxs-lookup"><span data-stu-id="532ac-190">Waiting</span></span></td><td><span data-ttu-id="532ac-191">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="532ac-191">ScheduleTime</span></span></td><td><span data-ttu-id="532ac-192">The time hasn't come for the activity window to run.</span><span class="sxs-lookup"><span data-stu-id="532ac-192">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-193">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="532ac-193">DatasetDependencies</span></span></td><td><span data-ttu-id="532ac-194">The upstream dependencies aren't ready.</span><span class="sxs-lookup"><span data-stu-id="532ac-194">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-195">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="532ac-195">ComputeResources</span></span></td><td><span data-ttu-id="532ac-196">The compute resources aren't available.</span><span class="sxs-lookup"><span data-stu-id="532ac-196">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-197">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="532ac-197">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="532ac-198">All the activity instances are busy running other activity windows.</span><span class="sxs-lookup"><span data-stu-id="532ac-198">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-199">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="532ac-199">ActivityResume</span></span></td><td><span data-ttu-id="532ac-200">The activity is paused and can't run the activity windows until it's resumed.</span><span class="sxs-lookup"><span data-stu-id="532ac-200">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-201">Retry</span><span class="sxs-lookup"><span data-stu-id="532ac-201">Retry</span></span></td><td><span data-ttu-id="532ac-202">The activity execution is being retried.</span><span class="sxs-lookup"><span data-stu-id="532ac-202">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-203">Validation</span><span class="sxs-lookup"><span data-stu-id="532ac-203">Validation</span></span></td><td><span data-ttu-id="532ac-204">Validation hasn't started yet.</span><span class="sxs-lookup"><span data-stu-id="532ac-204">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-205">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="532ac-205">ValidationRetry</span></span></td><td><span data-ttu-id="532ac-206">Validation is waiting to be retried.</span><span class="sxs-lookup"><span data-stu-id="532ac-206">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="532ac-207">InProgress</span><span class="sxs-lookup"><span data-stu-id="532ac-207">InProgress</span></span></td><td><span data-ttu-id="532ac-208">Validating</span><span class="sxs-lookup"><span data-stu-id="532ac-208">Validating</span></span></td><td><span data-ttu-id="532ac-209">Validation is in progress.</span><span class="sxs-lookup"><span data-stu-id="532ac-209">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="532ac-210">The activity window is being processed.</span><span class="sxs-lookup"><span data-stu-id="532ac-210">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="532ac-211">Failed</span><span class="sxs-lookup"><span data-stu-id="532ac-211">Failed</span></span></td><td><span data-ttu-id="532ac-212">TimedOut</span><span class="sxs-lookup"><span data-stu-id="532ac-212">TimedOut</span></span></td><td><span data-ttu-id="532ac-213">The activity execution took longer than what is allowed by the activity.</span><span class="sxs-lookup"><span data-stu-id="532ac-213">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-214">Canceled</span><span class="sxs-lookup"><span data-stu-id="532ac-214">Canceled</span></span></td><td><span data-ttu-id="532ac-215">The activity window was canceled by user action.</span><span class="sxs-lookup"><span data-stu-id="532ac-215">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-216">Validation</span><span class="sxs-lookup"><span data-stu-id="532ac-216">Validation</span></span></td><td><span data-ttu-id="532ac-217">Validation has failed.</span><span class="sxs-lookup"><span data-stu-id="532ac-217">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="532ac-218">The activity window failed to be generated or validated.</span><span class="sxs-lookup"><span data-stu-id="532ac-218">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="532ac-219">Ready</span><span class="sxs-lookup"><span data-stu-id="532ac-219">Ready</span></span></td><td>-</td><td><span data-ttu-id="532ac-220">The activity window is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="532ac-220">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-221">Skipped</span><span class="sxs-lookup"><span data-stu-id="532ac-221">Skipped</span></span></td><td>-</td><td><span data-ttu-id="532ac-222">The activity window wasn't processed.</span><span class="sxs-lookup"><span data-stu-id="532ac-222">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="532ac-223">None</span><span class="sxs-lookup"><span data-stu-id="532ac-223">None</span></span></td><td>-</td><td><span data-ttu-id="532ac-224">An activity window used to exist with a different status, but has been reset.</span><span class="sxs-lookup"><span data-stu-id="532ac-224">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="532ac-225">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span><span class="sxs-lookup"><span data-stu-id="532ac-225">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="532ac-227">Refresh activity windows</span><span class="sxs-lookup"><span data-stu-id="532ac-227">Refresh activity windows</span></span>
<span data-ttu-id="532ac-228">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span><span class="sxs-lookup"><span data-stu-id="532ac-228">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="532ac-229">Properties window</span><span class="sxs-lookup"><span data-stu-id="532ac-229">Properties window</span></span>
<span data-ttu-id="532ac-230">The Properties window is in the right-most pane of the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="532ac-230">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Properties window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="532ac-232">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="532ac-232">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="532ac-233">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="532ac-233">Activity Window Explorer</span></span>
<span data-ttu-id="532ac-234">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span><span class="sxs-lookup"><span data-stu-id="532ac-234">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="532ac-235">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="532ac-235">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Activity Window Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="532ac-237">You can switch to another activity window by clicking it in the calendar view at the top.</span><span class="sxs-lookup"><span data-stu-id="532ac-237">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="532ac-238">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span><span class="sxs-lookup"><span data-stu-id="532ac-238">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="532ac-239">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span><span class="sxs-lookup"><span data-stu-id="532ac-239">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="532ac-240">Script</span><span class="sxs-lookup"><span data-stu-id="532ac-240">Script</span></span>
<span data-ttu-id="532ac-241">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span><span class="sxs-lookup"><span data-stu-id="532ac-241">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Script tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="532ac-243">Use system views</span><span class="sxs-lookup"><span data-stu-id="532ac-243">Use system views</span></span>
<span data-ttu-id="532ac-244">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span><span class="sxs-lookup"><span data-stu-id="532ac-244">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="532ac-245">Switch to the **Monitoring Views** tab on the left by clicking it.</span><span class="sxs-lookup"><span data-stu-id="532ac-245">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Monitoring Views tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="532ac-247">Currently, there are three system views that are supported.</span><span class="sxs-lookup"><span data-stu-id="532ac-247">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="532ac-248">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span><span class="sxs-lookup"><span data-stu-id="532ac-248">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="532ac-249">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span><span class="sxs-lookup"><span data-stu-id="532ac-249">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="532ac-250">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span><span class="sxs-lookup"><span data-stu-id="532ac-250">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="532ac-251">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span><span class="sxs-lookup"><span data-stu-id="532ac-251">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="532ac-252">You can also download any logs for a failed activity window.</span><span class="sxs-lookup"><span data-stu-id="532ac-252">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="532ac-253">Sort and filter activity windows</span><span class="sxs-lookup"><span data-stu-id="532ac-253">Sort and filter activity windows</span></span>
<span data-ttu-id="532ac-254">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span><span class="sxs-lookup"><span data-stu-id="532ac-254">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="532ac-255">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span><span class="sxs-lookup"><span data-stu-id="532ac-255">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Start and end Times](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Currently, all times are in UTC format in the Monitoring and Management app.
>
>

<span data-ttu-id="532ac-258">In the **Activity Windows list**, click the name of a column (for example: Status).</span><span class="sxs-lookup"><span data-stu-id="532ac-258">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Activity Windows list column menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="532ac-260">You can do the following:</span><span class="sxs-lookup"><span data-stu-id="532ac-260">You can do the following:</span></span>

* <span data-ttu-id="532ac-261">Sort in ascending order.</span><span class="sxs-lookup"><span data-stu-id="532ac-261">Sort in ascending order.</span></span>
* <span data-ttu-id="532ac-262">Sort in descending order.</span><span class="sxs-lookup"><span data-stu-id="532ac-262">Sort in descending order.</span></span>
* <span data-ttu-id="532ac-263">Filter by one or more values (Ready, Waiting, and so on).</span><span class="sxs-lookup"><span data-stu-id="532ac-263">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="532ac-264">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span><span class="sxs-lookup"><span data-stu-id="532ac-264">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filter on a column of the Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="532ac-266">You can use the same pop-up window to clear filters.</span><span class="sxs-lookup"><span data-stu-id="532ac-266">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="532ac-267">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="532ac-267">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Clear all filters for the Activity Windows list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="532ac-269">Perform batch actions</span><span class="sxs-lookup"><span data-stu-id="532ac-269">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="532ac-270">Rerun selected activity windows</span><span class="sxs-lookup"><span data-stu-id="532ac-270">Rerun selected activity windows</span></span>
<span data-ttu-id="532ac-271">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span><span class="sxs-lookup"><span data-stu-id="532ac-271">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="532ac-272">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span><span class="sxs-lookup"><span data-stu-id="532ac-272">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="532ac-273">![Rerun an activity window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="532ac-273">![Rerun an activity window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="532ac-274">You can also select multiple activity windows in the list and rerun them at the same time.</span><span class="sxs-lookup"><span data-stu-id="532ac-274">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="532ac-275">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span><span class="sxs-lookup"><span data-stu-id="532ac-275">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="532ac-276">See the following section for details about filtering activity windows in the list.</span><span class="sxs-lookup"><span data-stu-id="532ac-276">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="532ac-277">Pause/resume multiple pipelines</span><span class="sxs-lookup"><span data-stu-id="532ac-277">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="532ac-278">You can multiselect two or more pipelines by using the Ctrl key.</span><span class="sxs-lookup"><span data-stu-id="532ac-278">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="532ac-279">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span><span class="sxs-lookup"><span data-stu-id="532ac-279">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Pause/resume on the command bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="532ac-281">Create alerts</span><span class="sxs-lookup"><span data-stu-id="532ac-281">Create alerts</span></span>
<span data-ttu-id="532ac-282">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span><span class="sxs-lookup"><span data-stu-id="532ac-282">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="532ac-283">You can also disable/enable an alert.</span><span class="sxs-lookup"><span data-stu-id="532ac-283">You can also disable/enable an alert.</span></span> <span data-ttu-id="532ac-284">To see the Alerts page, click the **Alerts** tab.</span><span class="sxs-lookup"><span data-stu-id="532ac-284">To see the Alerts page, click the **Alerts** tab.</span></span>

![Alerts tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="532ac-286">To create an alert</span><span class="sxs-lookup"><span data-stu-id="532ac-286">To create an alert</span></span>
1. <span data-ttu-id="532ac-287">Click **Add Alert** to add an alert.</span><span class="sxs-lookup"><span data-stu-id="532ac-287">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="532ac-288">You see the **Details** page.</span><span class="sxs-lookup"><span data-stu-id="532ac-288">You see the **Details** page.</span></span>

    ![Create Alerts - Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="532ac-290">Specify the **Name** and **Description** for the alert, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="532ac-290">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="532ac-291">You should see the **Filters** page.</span><span class="sxs-lookup"><span data-stu-id="532ac-291">You should see the **Filters** page.</span></span>

    ![Create Alerts - Filters page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="532ac-293">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="532ac-293">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="532ac-294">You should see the **Recipients** page.</span><span class="sxs-lookup"><span data-stu-id="532ac-294">You should see the **Recipients** page.</span></span>

    ![Create Alerts - Recipients page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="532ac-296">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="532ac-296">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="532ac-297">You should see the alert in the list.</span><span class="sxs-lookup"><span data-stu-id="532ac-297">You should see the alert in the list.</span></span>

    ![Alerts list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="532ac-299">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span><span class="sxs-lookup"><span data-stu-id="532ac-299">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="532ac-300">Event/status/substatus</span><span class="sxs-lookup"><span data-stu-id="532ac-300">Event/status/substatus</span></span>
<span data-ttu-id="532ac-301">The following table provides the list of available events and statuses (and substatuses).</span><span class="sxs-lookup"><span data-stu-id="532ac-301">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="532ac-302">Event name</span><span class="sxs-lookup"><span data-stu-id="532ac-302">Event name</span></span> | <span data-ttu-id="532ac-303">Status</span><span class="sxs-lookup"><span data-stu-id="532ac-303">Status</span></span> | <span data-ttu-id="532ac-304">Substatus</span><span class="sxs-lookup"><span data-stu-id="532ac-304">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="532ac-305">Activity Run Started</span><span class="sxs-lookup"><span data-stu-id="532ac-305">Activity Run Started</span></span> |<span data-ttu-id="532ac-306">Started</span><span class="sxs-lookup"><span data-stu-id="532ac-306">Started</span></span> |<span data-ttu-id="532ac-307">Starting</span><span class="sxs-lookup"><span data-stu-id="532ac-307">Starting</span></span> |
| <span data-ttu-id="532ac-308">Activity Run Finished</span><span class="sxs-lookup"><span data-stu-id="532ac-308">Activity Run Finished</span></span> |<span data-ttu-id="532ac-309">Succeeded</span><span class="sxs-lookup"><span data-stu-id="532ac-309">Succeeded</span></span> |<span data-ttu-id="532ac-310">Succeeded</span><span class="sxs-lookup"><span data-stu-id="532ac-310">Succeeded</span></span> |
| <span data-ttu-id="532ac-311">Activity Run Finished</span><span class="sxs-lookup"><span data-stu-id="532ac-311">Activity Run Finished</span></span> |<span data-ttu-id="532ac-312">Failed</span><span class="sxs-lookup"><span data-stu-id="532ac-312">Failed</span></span> |<span data-ttu-id="532ac-313">Failed Resource Allocation</span><span class="sxs-lookup"><span data-stu-id="532ac-313">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="532ac-314">Failed Execution</span><span class="sxs-lookup"><span data-stu-id="532ac-314">Failed Execution</span></span><br/><br/><span data-ttu-id="532ac-315">Timed Out</span><span class="sxs-lookup"><span data-stu-id="532ac-315">Timed Out</span></span><br/><br/><span data-ttu-id="532ac-316">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="532ac-316">Failed Validation</span></span><br/><br/><span data-ttu-id="532ac-317">Abandoned</span><span class="sxs-lookup"><span data-stu-id="532ac-317">Abandoned</span></span> |
| <span data-ttu-id="532ac-318">On-Demand HDI Cluster Create Started</span><span class="sxs-lookup"><span data-stu-id="532ac-318">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="532ac-319">Started</span><span class="sxs-lookup"><span data-stu-id="532ac-319">Started</span></span> |-|
| <span data-ttu-id="532ac-320">On-Demand HDI Cluster Created Successfully</span><span class="sxs-lookup"><span data-stu-id="532ac-320">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="532ac-321">Succeeded</span><span class="sxs-lookup"><span data-stu-id="532ac-321">Succeeded</span></span> |-|
| <span data-ttu-id="532ac-322">On-Demand HDI Cluster Deleted</span><span class="sxs-lookup"><span data-stu-id="532ac-322">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="532ac-323">Succeeded</span><span class="sxs-lookup"><span data-stu-id="532ac-323">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="532ac-324">To edit, delete, or disable an alert</span><span class="sxs-lookup"><span data-stu-id="532ac-324">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="532ac-325">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span><span class="sxs-lookup"><span data-stu-id="532ac-325">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Alerts buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-app/AlertButtons.png)

































