---
title: Monitor and manage pipelines by using the Azure portal and PowerShell | Microsoft Docs
description: Learn how to use the Azure portal and Azure PowerShell to monitor and manage the Azure data factories and pipelines that you have created.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/30/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 843b92c20b2ec930ce67659802a4287328a08650
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868946"
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="2adc1-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span><span class="sxs-lookup"><span data-stu-id="2adc1-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Using Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Using Monitoring and Management app](data-factory-monitor-manage-app.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [monitor and manage Data Factory pipelines in](../monitor-visually.md).

<span data-ttu-id="2adc1-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2adc1-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span>

> [!IMPORTANT]
> The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues. For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md). 

> [!IMPORTANT]
> Azure Data Factory version 1 now uses the new [Azure Monitor alerting infrastructure](../../monitoring-and-diagnostics/monitor-alerts-unified-usage.md). The old alerting infrastructure is deprecated. As a result, your existing alerts configured for version 1 data factories no longer work. Your existing alerts for v1 data factories are not migrated automatically. You have to recreate these alerts on the new alerting infrastructure. Log in to the Azure portal and select **Monitor** to create new alerts on metrics (such as failed runs or successful runs) for your version 1 data factories.

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="2adc1-117">Understand pipelines and activity states</span><span class="sxs-lookup"><span data-stu-id="2adc1-117">Understand pipelines and activity states</span></span>
<span data-ttu-id="2adc1-118">By using the Azure portal, you can:</span><span class="sxs-lookup"><span data-stu-id="2adc1-118">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="2adc1-119">View your data factory as a diagram.</span><span class="sxs-lookup"><span data-stu-id="2adc1-119">View your data factory as a diagram.</span></span>
* <span data-ttu-id="2adc1-120">View activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="2adc1-120">View activities in a pipeline.</span></span>
* <span data-ttu-id="2adc1-121">View input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="2adc1-121">View input and output datasets.</span></span>

<span data-ttu-id="2adc1-122">This section also describes how a dataset slice transitions from one state to another state.</span><span class="sxs-lookup"><span data-stu-id="2adc1-122">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="2adc1-123">Navigate to your data factory</span><span class="sxs-lookup"><span data-stu-id="2adc1-123">Navigate to your data factory</span></span>
1. <span data-ttu-id="2adc1-124">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2adc1-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2adc1-125">Click **Data factories** on the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="2adc1-125">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="2adc1-126">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span><span class="sxs-lookup"><span data-stu-id="2adc1-126">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Browse all > Data factories](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="2adc1-128">On the **Data factories** blade, select the data factory that you're interested in.</span><span class="sxs-lookup"><span data-stu-id="2adc1-128">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Select data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="2adc1-130">You should see the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="2adc1-130">You should see the home page for the data factory.</span></span>

   ![Data factory blade](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="2adc1-132">Diagram view of your data factory</span><span class="sxs-lookup"><span data-stu-id="2adc1-132">Diagram view of your data factory</span></span>
<span data-ttu-id="2adc1-133">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span><span class="sxs-lookup"><span data-stu-id="2adc1-133">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="2adc1-134">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="2adc1-134">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Diagram view](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="2adc1-136">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span><span class="sxs-lookup"><span data-stu-id="2adc1-136">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="2adc1-137">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span><span class="sxs-lookup"><span data-stu-id="2adc1-137">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="2adc1-138">Activities inside a pipeline</span><span class="sxs-lookup"><span data-stu-id="2adc1-138">Activities inside a pipeline</span></span>
1. <span data-ttu-id="2adc1-139">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span><span class="sxs-lookup"><span data-stu-id="2adc1-139">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="2adc1-140">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span><span class="sxs-lookup"><span data-stu-id="2adc1-140">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Open pipeline menu](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="2adc1-142">In the following example, you see a copy activity in the pipeline with an input and an output.</span><span class="sxs-lookup"><span data-stu-id="2adc1-142">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Activities inside a pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="2adc1-144">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span><span class="sxs-lookup"><span data-stu-id="2adc1-144">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Navigate back to data factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="2adc1-146">View the state of each activity inside a pipeline</span><span class="sxs-lookup"><span data-stu-id="2adc1-146">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="2adc1-147">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span><span class="sxs-lookup"><span data-stu-id="2adc1-147">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="2adc1-148">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span><span class="sxs-lookup"><span data-stu-id="2adc1-148">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="2adc1-149">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="2adc1-149">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![State of the pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="2adc1-151">The dataset slices in the data factory can have one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="2adc1-151">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="2adc1-152">State</span><span class="sxs-lookup"><span data-stu-id="2adc1-152">State</span></span></th><th align="left"><span data-ttu-id="2adc1-153">Substate</span><span class="sxs-lookup"><span data-stu-id="2adc1-153">Substate</span></span></th><th align="left"><span data-ttu-id="2adc1-154">Description</span><span class="sxs-lookup"><span data-stu-id="2adc1-154">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="2adc1-155">Waiting</span><span class="sxs-lookup"><span data-stu-id="2adc1-155">Waiting</span></span></td><td><span data-ttu-id="2adc1-156">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="2adc1-156">ScheduleTime</span></span></td><td><span data-ttu-id="2adc1-157">The time hasn't come for the slice to run.</span><span class="sxs-lookup"><span data-stu-id="2adc1-157">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-158">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="2adc1-158">DatasetDependencies</span></span></td><td><span data-ttu-id="2adc1-159">The upstream dependencies aren't ready.</span><span class="sxs-lookup"><span data-stu-id="2adc1-159">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-160">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="2adc1-160">ComputeResources</span></span></td><td><span data-ttu-id="2adc1-161">The compute resources aren't available.</span><span class="sxs-lookup"><span data-stu-id="2adc1-161">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-162">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="2adc1-162">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="2adc1-163">All the activity instances are busy running other slices.</span><span class="sxs-lookup"><span data-stu-id="2adc1-163">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-164">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="2adc1-164">ActivityResume</span></span></td><td><span data-ttu-id="2adc1-165">The activity is paused and can't run the slices until the activity is resumed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-165">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-166">Retry</span><span class="sxs-lookup"><span data-stu-id="2adc1-166">Retry</span></span></td><td><span data-ttu-id="2adc1-167">Activity execution is being retried.</span><span class="sxs-lookup"><span data-stu-id="2adc1-167">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-168">Validation</span><span class="sxs-lookup"><span data-stu-id="2adc1-168">Validation</span></span></td><td><span data-ttu-id="2adc1-169">Validation hasn't started yet.</span><span class="sxs-lookup"><span data-stu-id="2adc1-169">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-170">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="2adc1-170">ValidationRetry</span></span></td><td><span data-ttu-id="2adc1-171">Validation is waiting to be retried.</span><span class="sxs-lookup"><span data-stu-id="2adc1-171">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="2adc1-172">InProgress</span><span class="sxs-lookup"><span data-stu-id="2adc1-172">InProgress</span></span></td><td><span data-ttu-id="2adc1-173">Validating</span><span class="sxs-lookup"><span data-stu-id="2adc1-173">Validating</span></span></td><td><span data-ttu-id="2adc1-174">Validation is in progress.</span><span class="sxs-lookup"><span data-stu-id="2adc1-174">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="2adc1-175">The slice is being processed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-175">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="2adc1-176">Failed</span><span class="sxs-lookup"><span data-stu-id="2adc1-176">Failed</span></span></td><td><span data-ttu-id="2adc1-177">TimedOut</span><span class="sxs-lookup"><span data-stu-id="2adc1-177">TimedOut</span></span></td><td><span data-ttu-id="2adc1-178">The activity execution took longer than what is allowed by the activity.</span><span class="sxs-lookup"><span data-stu-id="2adc1-178">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-179">Canceled</span><span class="sxs-lookup"><span data-stu-id="2adc1-179">Canceled</span></span></td><td><span data-ttu-id="2adc1-180">The slice was canceled by user action.</span><span class="sxs-lookup"><span data-stu-id="2adc1-180">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-181">Validation</span><span class="sxs-lookup"><span data-stu-id="2adc1-181">Validation</span></span></td><td><span data-ttu-id="2adc1-182">Validation has failed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-182">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="2adc1-183">The slice failed to be generated and/or validated.</span><span class="sxs-lookup"><span data-stu-id="2adc1-183">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="2adc1-184">Ready</span><span class="sxs-lookup"><span data-stu-id="2adc1-184">Ready</span></span></td><td>-</td><td><span data-ttu-id="2adc1-185">The slice is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="2adc1-185">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-186">Skipped</span><span class="sxs-lookup"><span data-stu-id="2adc1-186">Skipped</span></span></td><td><span data-ttu-id="2adc1-187">None</span><span class="sxs-lookup"><span data-stu-id="2adc1-187">None</span></span></td><td><span data-ttu-id="2adc1-188">The slice isn't being processed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-188">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="2adc1-189">None</span><span class="sxs-lookup"><span data-stu-id="2adc1-189">None</span></span></td><td>-</td><td><span data-ttu-id="2adc1-190">A slice used to exist with a different status, but it has been reset.</span><span class="sxs-lookup"><span data-stu-id="2adc1-190">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="2adc1-191">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span><span class="sxs-lookup"><span data-stu-id="2adc1-191">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Slice details](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="2adc1-193">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span><span class="sxs-lookup"><span data-stu-id="2adc1-193">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="2adc1-194">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span><span class="sxs-lookup"><span data-stu-id="2adc1-194">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="2adc1-195">The list shows all the log files, along with an error message if there is one.</span><span class="sxs-lookup"><span data-stu-id="2adc1-195">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="2adc1-196">This feature is useful to view and debug logs without having to leave your data factory.</span><span class="sxs-lookup"><span data-stu-id="2adc1-196">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Activity run details](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="2adc1-198">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span><span class="sxs-lookup"><span data-stu-id="2adc1-198">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="2adc1-199">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span><span class="sxs-lookup"><span data-stu-id="2adc1-199">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Upstream slices that are not ready](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="2adc1-201">Dataset state diagram</span><span class="sxs-lookup"><span data-stu-id="2adc1-201">Dataset state diagram</span></span>
<span data-ttu-id="2adc1-202">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span><span class="sxs-lookup"><span data-stu-id="2adc1-202">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="2adc1-203">Currently, the slice status follows the following state diagram:</span><span class="sxs-lookup"><span data-stu-id="2adc1-203">Currently, the slice status follows the following state diagram:</span></span>

![State diagram](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="2adc1-205">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-205">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="2adc1-206">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span><span class="sxs-lookup"><span data-stu-id="2adc1-206">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="2adc1-207">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span><span class="sxs-lookup"><span data-stu-id="2adc1-207">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="2adc1-208">The activity execution might succeed or fail.</span><span class="sxs-lookup"><span data-stu-id="2adc1-208">The activity execution might succeed or fail.</span></span> <span data-ttu-id="2adc1-209">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span><span class="sxs-lookup"><span data-stu-id="2adc1-209">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="2adc1-210">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span><span class="sxs-lookup"><span data-stu-id="2adc1-210">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="2adc1-211">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span><span class="sxs-lookup"><span data-stu-id="2adc1-211">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="2adc1-212">Pause and resume pipelines</span><span class="sxs-lookup"><span data-stu-id="2adc1-212">Pause and resume pipelines</span></span>
<span data-ttu-id="2adc1-213">You can manage your pipelines by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2adc1-213">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="2adc1-214">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2adc1-214">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> The diagram view does not support pausing and resuming pipelines. If you want to use an user interface, use the monitoring and managing application. For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article. 

<span data-ttu-id="2adc1-218">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2adc1-218">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="2adc1-219">This cmdlet is useful when you don't want to run your pipelines until an issue is fixed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-219">This cmdlet is useful when you don't want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="2adc1-220">For example:</span><span class="sxs-lookup"><span data-stu-id="2adc1-220">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="2adc1-221">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="2adc1-221">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="2adc1-222">For example:</span><span class="sxs-lookup"><span data-stu-id="2adc1-222">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="2adc1-223">Debug pipelines</span><span class="sxs-lookup"><span data-stu-id="2adc1-223">Debug pipelines</span></span>
<span data-ttu-id="2adc1-224">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2adc1-224">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> [!NOTE] 
> It is much easier to troubleshot errors using the Monitoring & Management App. For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article. 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="2adc1-227">Find errors in a pipeline</span><span class="sxs-lookup"><span data-stu-id="2adc1-227">Find errors in a pipeline</span></span>
<span data-ttu-id="2adc1-228">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span><span class="sxs-lookup"><span data-stu-id="2adc1-228">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="2adc1-229">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span><span class="sxs-lookup"><span data-stu-id="2adc1-229">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="2adc1-230">Use the Azure portal to debug an error</span><span class="sxs-lookup"><span data-stu-id="2adc1-230">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="2adc1-231">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-231">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Table blade with problem slice](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="2adc1-233">On the **Data slice** blade, click the activity run that failed.</span><span class="sxs-lookup"><span data-stu-id="2adc1-233">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Data slice with an error](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="2adc1-235">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span><span class="sxs-lookup"><span data-stu-id="2adc1-235">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="2adc1-236">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span><span class="sxs-lookup"><span data-stu-id="2adc1-236">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Activity run details blade with error](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="2adc1-238">Use PowerShell to debug an error</span><span class="sxs-lookup"><span data-stu-id="2adc1-238">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="2adc1-239">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-239">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="2adc1-240">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span><span class="sxs-lookup"><span data-stu-id="2adc1-240">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="2adc1-241">You should see a slice with the status of **Failed**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-241">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="2adc1-242">For example:</span><span class="sxs-lookup"><span data-stu-id="2adc1-242">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="2adc1-243">Replace **StartDateTime** with start time of your pipeline.</span><span class="sxs-lookup"><span data-stu-id="2adc1-243">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="2adc1-244">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span><span class="sxs-lookup"><span data-stu-id="2adc1-244">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="2adc1-245">For example:</span><span class="sxs-lookup"><span data-stu-id="2adc1-245">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="2adc1-246">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span><span class="sxs-lookup"><span data-stu-id="2adc1-246">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="2adc1-247">The date-time should be enclosed in double quotes.</span><span class="sxs-lookup"><span data-stu-id="2adc1-247">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="2adc1-248">You should see output with details about the error that is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2adc1-248">You should see output with details about the error that is similar to the following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="2adc1-249">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2adc1-249">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="2adc1-250">Rerun failures in a pipeline</span><span class="sxs-lookup"><span data-stu-id="2adc1-250">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App. For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md). 

### <a name="use-the-azure-portal"></a><span data-ttu-id="2adc1-253">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2adc1-253">Use the Azure portal</span></span>
<span data-ttu-id="2adc1-254">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="2adc1-254">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Rerun a failed slice](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="2adc1-256">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="2adc1-256">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Fix errors and validate](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="2adc1-258">Use Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2adc1-258">Use Azure PowerShell</span></span>
<span data-ttu-id="2adc1-259">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2adc1-259">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="2adc1-260">See the [Set-AzureRmDataFactorySliceStatus](https://docs.microsoft.com/powershell/module/azurerm.datafactories/set-azurermdatafactoryslicestatus) topic for syntax and other details about the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2adc1-260">See the [Set-AzureRmDataFactorySliceStatus](https://docs.microsoft.com/powershell/module/azurerm.datafactories/set-azurermdatafactoryslicestatus) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="2adc1-261">**Example:**</span><span class="sxs-lookup"><span data-stu-id="2adc1-261">**Example:**</span></span>

<span data-ttu-id="2adc1-262">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="2adc1-262">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="2adc1-263">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="2adc1-263">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="2adc1-264">The other possible value for this parameter is 'Individual'.</span><span class="sxs-lookup"><span data-stu-id="2adc1-264">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```
## <a name="create-alerts-in-the-azure-portal"></a><span data-ttu-id="2adc1-265">Create alerts in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2adc1-265">Create alerts in the Azure portal</span></span>

1.  <span data-ttu-id="2adc1-266">Log in to the Azure portal and select **Monitor -> Alerts** to open the Alerts page.</span><span class="sxs-lookup"><span data-stu-id="2adc1-266">Log in to the Azure portal and select **Monitor -> Alerts** to open the Alerts page.</span></span>

    ![Open the Alerts page.](media/data-factory-monitor-manage-pipelines/v1alerts-image1.png)

2.  <span data-ttu-id="2adc1-268">Select **+ New Alert rule** to create a new alert.</span><span class="sxs-lookup"><span data-stu-id="2adc1-268">Select **+ New Alert rule** to create a new alert.</span></span>

    ![Create a new alert](media/data-factory-monitor-manage-pipelines/v1alerts-image2.png)

3.  <span data-ttu-id="2adc1-270">Define the **Alert condition**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-270">Define the **Alert condition**.</span></span> <span data-ttu-id="2adc1-271">(Make sure to select **Data factories** in the **Filter by resource type** field.) You can also specify values for **Dimensions**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-271">(Make sure to select **Data factories** in the **Filter by resource type** field.) You can also specify values for **Dimensions**.</span></span>

    ![Define the Alert Condition - Select target](media/data-factory-monitor-manage-pipelines/v1alerts-image3.png)

    ![Define the Alert Condition - Add alert criteria](media/data-factory-monitor-manage-pipelines/v1alerts-image4.png)

    ![Define the Alert Condition - Add alert logic](media/data-factory-monitor-manage-pipelines/v1alerts-image5.png)

4.  <span data-ttu-id="2adc1-275">Define the **Alert details**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-275">Define the **Alert details**.</span></span>

    ![Define the Alert Details](media/data-factory-monitor-manage-pipelines/v1alerts-image6.png)

5.  <span data-ttu-id="2adc1-277">Define the **Action group**.</span><span class="sxs-lookup"><span data-stu-id="2adc1-277">Define the **Action group**.</span></span>

    ![Define the Action Group - create a new Action group](media/data-factory-monitor-manage-pipelines/v1alerts-image7.png)

    ![Define the Action Group - set properties](media/data-factory-monitor-manage-pipelines/v1alerts-image8.png)

    ![Define the Action Group - new action group created](media/data-factory-monitor-manage-pipelines/v1alerts-image9.png)

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="2adc1-281">Move a data factory to a different resource group or subscription</span><span class="sxs-lookup"><span data-stu-id="2adc1-281">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="2adc1-282">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="2adc1-282">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Move data factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="2adc1-284">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span><span class="sxs-lookup"><span data-stu-id="2adc1-284">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Move resources dialog box](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
