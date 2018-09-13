---
title: Monitor and manage pipelines by using the Azure portal and PowerShell | Microsoft Docs
description: Learn how to use the Azure portal and Azure PowerShell to monitor and manage the Azure data factories and pipelines that you have created.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: spelluru
ms.openlocfilehash: 608d3c3d26f8b8932bf03a72f18aff043cb22475
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553773"
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="c8f37-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8f37-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Using Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Using Monitoring and Management app](data-factory-monitor-manage-app.md)


<span data-ttu-id="c8f37-106">Azure Data Factory provides a reliable and complete view of your storage, processing, and data movement services.</span><span class="sxs-lookup"><span data-stu-id="c8f37-106">Azure Data Factory provides a reliable and complete view of your storage, processing, and data movement services.</span></span> <span data-ttu-id="c8f37-107">The service provides you a monitoring dashboard that you can use to:</span><span class="sxs-lookup"><span data-stu-id="c8f37-107">The service provides you a monitoring dashboard that you can use to:</span></span>

* <span data-ttu-id="c8f37-108">Quickly assess end-to-end data pipeline health.</span><span class="sxs-lookup"><span data-stu-id="c8f37-108">Quickly assess end-to-end data pipeline health.</span></span>
* <span data-ttu-id="c8f37-109">Identify issues, and take corrective action if needed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-109">Identify issues, and take corrective action if needed.</span></span>
* <span data-ttu-id="c8f37-110">Track data lineage.</span><span class="sxs-lookup"><span data-stu-id="c8f37-110">Track data lineage.</span></span>
* <span data-ttu-id="c8f37-111">Track relationships between your data across any of your sources.</span><span class="sxs-lookup"><span data-stu-id="c8f37-111">Track relationships between your data across any of your sources.</span></span>
* <span data-ttu-id="c8f37-112">View full historical accounting of job execution, system health, and dependencies.</span><span class="sxs-lookup"><span data-stu-id="c8f37-112">View full historical accounting of job execution, system health, and dependencies.</span></span>

<span data-ttu-id="c8f37-113">This article describes how to monitor, manage, and debug your pipelines.</span><span class="sxs-lookup"><span data-stu-id="c8f37-113">This article describes how to monitor, manage, and debug your pipelines.</span></span> <span data-ttu-id="c8f37-114">It also provides information on how to create alerts and get notified about failures.</span><span class="sxs-lookup"><span data-stu-id="c8f37-114">It also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="c8f37-115">Understand pipelines and activity states</span><span class="sxs-lookup"><span data-stu-id="c8f37-115">Understand pipelines and activity states</span></span>
<span data-ttu-id="c8f37-116">By using the Azure portal, you can:</span><span class="sxs-lookup"><span data-stu-id="c8f37-116">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="c8f37-117">View your data factory as a diagram.</span><span class="sxs-lookup"><span data-stu-id="c8f37-117">View your data factory as a diagram.</span></span>
* <span data-ttu-id="c8f37-118">View activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8f37-118">View activities in a pipeline.</span></span>
* <span data-ttu-id="c8f37-119">View input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="c8f37-119">View input and output datasets.</span></span>

<span data-ttu-id="c8f37-120">This section also describes how a slice transitions from one state to another state.</span><span class="sxs-lookup"><span data-stu-id="c8f37-120">This section also describes how a slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="c8f37-121">Navigate to your data factory</span><span class="sxs-lookup"><span data-stu-id="c8f37-121">Navigate to your data factory</span></span>
1. <span data-ttu-id="c8f37-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8f37-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c8f37-123">Click **Data factories** on the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="c8f37-123">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="c8f37-124">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span><span class="sxs-lookup"><span data-stu-id="c8f37-124">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Browse all > Data factories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)

   <span data-ttu-id="c8f37-126">You should see all the data factories on the **Data factories** blade.</span><span class="sxs-lookup"><span data-stu-id="c8f37-126">You should see all the data factories on the **Data factories** blade.</span></span>
3. <span data-ttu-id="c8f37-127">On the **Data factories** blade, select the data factory that you're interested in.</span><span class="sxs-lookup"><span data-stu-id="c8f37-127">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Select data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="c8f37-129">You should see the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-129">You should see the home page for the data factory.</span></span>

   ![Data factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="c8f37-131">Diagram view of your data factory</span><span class="sxs-lookup"><span data-stu-id="c8f37-131">Diagram view of your data factory</span></span>
<span data-ttu-id="c8f37-132">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span><span class="sxs-lookup"><span data-stu-id="c8f37-132">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span>

<span data-ttu-id="c8f37-133">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-133">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Diagram view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="c8f37-135">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and tables.</span><span class="sxs-lookup"><span data-stu-id="c8f37-135">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and tables.</span></span> <span data-ttu-id="c8f37-136">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span><span class="sxs-lookup"><span data-stu-id="c8f37-136">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="c8f37-137">Activities inside a pipeline</span><span class="sxs-lookup"><span data-stu-id="c8f37-137">Activities inside a pipeline</span></span>
1. <span data-ttu-id="c8f37-138">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span><span class="sxs-lookup"><span data-stu-id="c8f37-138">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="c8f37-139">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8f37-139">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Open pipeline menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="c8f37-141">In the following example, you see a copy activity in the pipeline with an input and an output.</span><span class="sxs-lookup"><span data-stu-id="c8f37-141">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Activities inside a pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="c8f37-143">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span><span class="sxs-lookup"><span data-stu-id="c8f37-143">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Navigate back to data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="c8f37-145">View the state of each activity inside a pipeline</span><span class="sxs-lookup"><span data-stu-id="c8f37-145">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="c8f37-146">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span><span class="sxs-lookup"><span data-stu-id="c8f37-146">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="c8f37-147">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8f37-147">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="c8f37-148">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="c8f37-148">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![State of the pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="c8f37-150">The dataset slices in the data factory can have one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="c8f37-150">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="c8f37-151">State</span><span class="sxs-lookup"><span data-stu-id="c8f37-151">State</span></span></th><th align="left"><span data-ttu-id="c8f37-152">Substate</span><span class="sxs-lookup"><span data-stu-id="c8f37-152">Substate</span></span></th><th align="left"><span data-ttu-id="c8f37-153">Description</span><span class="sxs-lookup"><span data-stu-id="c8f37-153">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="c8f37-154">Waiting</span><span class="sxs-lookup"><span data-stu-id="c8f37-154">Waiting</span></span></td><td><span data-ttu-id="c8f37-155">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="c8f37-155">ScheduleTime</span></span></td><td><span data-ttu-id="c8f37-156">The time hasn't come for the slice to run.</span><span class="sxs-lookup"><span data-stu-id="c8f37-156">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-157">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="c8f37-157">DatasetDependencies</span></span></td><td><span data-ttu-id="c8f37-158">The upstream dependencies aren't ready.</span><span class="sxs-lookup"><span data-stu-id="c8f37-158">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-159">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="c8f37-159">ComputeResources</span></span></td><td><span data-ttu-id="c8f37-160">The compute resources aren't available.</span><span class="sxs-lookup"><span data-stu-id="c8f37-160">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-161">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="c8f37-161">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="c8f37-162">All the activity instances are busy running other slices.</span><span class="sxs-lookup"><span data-stu-id="c8f37-162">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-163">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="c8f37-163">ActivityResume</span></span></td><td><span data-ttu-id="c8f37-164">The activity is paused and can't run the slices until the activity is resumed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-164">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-165">Retry</span><span class="sxs-lookup"><span data-stu-id="c8f37-165">Retry</span></span></td><td><span data-ttu-id="c8f37-166">Activity execution is being retried.</span><span class="sxs-lookup"><span data-stu-id="c8f37-166">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-167">Validation</span><span class="sxs-lookup"><span data-stu-id="c8f37-167">Validation</span></span></td><td><span data-ttu-id="c8f37-168">Validation hasn't started yet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-168">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-169">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="c8f37-169">ValidationRetry</span></span></td><td><span data-ttu-id="c8f37-170">Validation is waiting to be retried.</span><span class="sxs-lookup"><span data-stu-id="c8f37-170">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="c8f37-171">InProgress</span><span class="sxs-lookup"><span data-stu-id="c8f37-171">InProgress</span></span></td><td><span data-ttu-id="c8f37-172">Validating</span><span class="sxs-lookup"><span data-stu-id="c8f37-172">Validating</span></span></td><td><span data-ttu-id="c8f37-173">Validation is in progress.</span><span class="sxs-lookup"><span data-stu-id="c8f37-173">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="c8f37-174">The slice is being processed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-174">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="c8f37-175">Failed</span><span class="sxs-lookup"><span data-stu-id="c8f37-175">Failed</span></span></td><td><span data-ttu-id="c8f37-176">TimedOut</span><span class="sxs-lookup"><span data-stu-id="c8f37-176">TimedOut</span></span></td><td><span data-ttu-id="c8f37-177">The activity execution took longer than what is allowed by the activity.</span><span class="sxs-lookup"><span data-stu-id="c8f37-177">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-178">Canceled</span><span class="sxs-lookup"><span data-stu-id="c8f37-178">Canceled</span></span></td><td><span data-ttu-id="c8f37-179">The slice was canceled by user action.</span><span class="sxs-lookup"><span data-stu-id="c8f37-179">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-180">Validation</span><span class="sxs-lookup"><span data-stu-id="c8f37-180">Validation</span></span></td><td><span data-ttu-id="c8f37-181">Validation has failed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-181">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="c8f37-182">The slice failed to be generated and/or validated.</span><span class="sxs-lookup"><span data-stu-id="c8f37-182">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="c8f37-183">Ready</span><span class="sxs-lookup"><span data-stu-id="c8f37-183">Ready</span></span></td><td>-</td><td><span data-ttu-id="c8f37-184">The slice is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="c8f37-184">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-185">Skipped</span><span class="sxs-lookup"><span data-stu-id="c8f37-185">Skipped</span></span></td><td><span data-ttu-id="c8f37-186">None</span><span class="sxs-lookup"><span data-stu-id="c8f37-186">None</span></span></td><td><span data-ttu-id="c8f37-187">The slice isn't being processed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-187">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c8f37-188">None</span><span class="sxs-lookup"><span data-stu-id="c8f37-188">None</span></span></td><td>-</td><td><span data-ttu-id="c8f37-189">A slice used to exist with a different status, but it has been reset.</span><span class="sxs-lookup"><span data-stu-id="c8f37-189">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="c8f37-190">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span><span class="sxs-lookup"><span data-stu-id="c8f37-190">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Slice details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="c8f37-192">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span><span class="sxs-lookup"><span data-stu-id="c8f37-192">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="c8f37-193">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span><span class="sxs-lookup"><span data-stu-id="c8f37-193">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="c8f37-194">The list shows all the log files, along with an error message if there is one.</span><span class="sxs-lookup"><span data-stu-id="c8f37-194">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="c8f37-195">This feature is useful to view and debug logs without having to leave your data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-195">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Activity run details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="c8f37-197">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span><span class="sxs-lookup"><span data-stu-id="c8f37-197">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="c8f37-198">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span><span class="sxs-lookup"><span data-stu-id="c8f37-198">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Upstream slices that are not ready](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="c8f37-200">Dataset state diagram</span><span class="sxs-lookup"><span data-stu-id="c8f37-200">Dataset state diagram</span></span>
<span data-ttu-id="c8f37-201">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span><span class="sxs-lookup"><span data-stu-id="c8f37-201">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="c8f37-202">Currently, the slice status follows the following state diagram:</span><span class="sxs-lookup"><span data-stu-id="c8f37-202">Currently, the slice status follows the following state diagram:</span></span>

![State diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="c8f37-204">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-204">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="c8f37-205">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span><span class="sxs-lookup"><span data-stu-id="c8f37-205">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="c8f37-206">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span><span class="sxs-lookup"><span data-stu-id="c8f37-206">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="c8f37-207">The activity execution might succeed or fail.</span><span class="sxs-lookup"><span data-stu-id="c8f37-207">The activity execution might succeed or fail.</span></span> <span data-ttu-id="c8f37-208">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span><span class="sxs-lookup"><span data-stu-id="c8f37-208">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="c8f37-209">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span><span class="sxs-lookup"><span data-stu-id="c8f37-209">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="c8f37-210">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span><span class="sxs-lookup"><span data-stu-id="c8f37-210">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="manage-pipelines"></a><span data-ttu-id="c8f37-211">Manage pipelines</span><span class="sxs-lookup"><span data-stu-id="c8f37-211">Manage pipelines</span></span>
<span data-ttu-id="c8f37-212">You can manage your pipelines by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8f37-212">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="c8f37-213">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c8f37-213">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span>

### <a name="pause-and-resume-pipelines"></a><span data-ttu-id="c8f37-214">Pause and resume pipelines</span><span class="sxs-lookup"><span data-stu-id="c8f37-214">Pause and resume pipelines</span></span>
<span data-ttu-id="c8f37-215">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-215">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="c8f37-216">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-216">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span>

<span data-ttu-id="c8f37-217">For example, in the following screenshot, an issue has been identified with the **PartitionProductsUsagePipeline** in the **productrecgamalbox1dev** data factory, and we want to suspend the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8f37-217">For example, in the following screenshot, an issue has been identified with the **PartitionProductsUsagePipeline** in the **productrecgamalbox1dev** data factory, and we want to suspend the pipeline.</span></span>

![Pipeline to be suspended](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/pipeline-to-be-suspended.png)

<span data-ttu-id="c8f37-219">To suspend a pipeline, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="c8f37-219">To suspend a pipeline, run the following PowerShell command:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="c8f37-220">For example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-220">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="c8f37-221">After the issue has been fixed with the **PartitionProductsUsagePipeline**, you can resume the suspended pipeline by running the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="c8f37-221">After the issue has been fixed with the **PartitionProductsUsagePipeline**, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="c8f37-222">For example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-222">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```
## <a name="debug-pipelines"></a><span data-ttu-id="c8f37-223">Debug pipelines</span><span class="sxs-lookup"><span data-stu-id="c8f37-223">Debug pipelines</span></span>
<span data-ttu-id="c8f37-224">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8f37-224">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="c8f37-225">Find errors in a pipeline</span><span class="sxs-lookup"><span data-stu-id="c8f37-225">Find errors in a pipeline</span></span>
<span data-ttu-id="c8f37-226">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span><span class="sxs-lookup"><span data-stu-id="c8f37-226">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="c8f37-227">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span><span class="sxs-lookup"><span data-stu-id="c8f37-227">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="c8f37-228">Use the Azure portal to debug an error</span><span class="sxs-lookup"><span data-stu-id="c8f37-228">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="c8f37-229">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span><span class="sxs-lookup"><span data-stu-id="c8f37-229">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Table blade with problem slice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="c8f37-231">On the **Data slice** blade, click the activity run that failed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-231">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Data slice with an error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="c8f37-233">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span><span class="sxs-lookup"><span data-stu-id="c8f37-233">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="c8f37-234">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span><span class="sxs-lookup"><span data-stu-id="c8f37-234">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Activity run details blade with error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="c8f37-236">Use PowerShell to debug an error</span><span class="sxs-lookup"><span data-stu-id="c8f37-236">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="c8f37-237">Start **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c8f37-237">Start **Azure PowerShell**.</span></span>
2. <span data-ttu-id="c8f37-238">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span><span class="sxs-lookup"><span data-stu-id="c8f37-238">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="c8f37-239">You should see a slice with the status of **Failed**.</span><span class="sxs-lookup"><span data-stu-id="c8f37-239">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="c8f37-240">For example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-240">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="c8f37-241">Replace **StartDateTime** with the the StartDateTime value that you specified for the Set-AzureRmDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="c8f37-241">Replace **StartDateTime** with the the StartDateTime value that you specified for the Set-AzureRmDataFactoryPipelineActivePeriod.</span></span>
3. <span data-ttu-id="c8f37-242">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span><span class="sxs-lookup"><span data-stu-id="c8f37-242">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="c8f37-243">For example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-243">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="c8f37-244">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span><span class="sxs-lookup"><span data-stu-id="c8f37-244">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="c8f37-245">The date-time should be enclosed in double quotes.</span><span class="sxs-lookup"><span data-stu-id="c8f37-245">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="c8f37-246">You should see output with details about the error that is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="c8f37-246">You should see output with details about the error that is similar to the following:</span></span>

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
5. <span data-ttu-id="c8f37-247">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-247">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="c8f37-248">Rerun failures in a pipeline</span><span class="sxs-lookup"><span data-stu-id="c8f37-248">Rerun failures in a pipeline</span></span>
### <a name="use-the-azure-portal"></a><span data-ttu-id="c8f37-249">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8f37-249">Use the Azure portal</span></span>
<span data-ttu-id="c8f37-250">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="c8f37-250">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Rerun a failed slice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="c8f37-252">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="c8f37-252">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>
<span data-ttu-id="c8f37-253">![Fix errors and validate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)</span><span class="sxs-lookup"><span data-stu-id="c8f37-253">![Fix errors and validate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)</span></span>

### <a name="use-azure-powershell"></a><span data-ttu-id="c8f37-254">Use Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8f37-254">Use Azure PowerShell</span></span>
<span data-ttu-id="c8f37-255">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-255">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="c8f37-256">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-256">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="c8f37-257">**Example:**</span><span class="sxs-lookup"><span data-stu-id="c8f37-257">**Example:**</span></span>

<span data-ttu-id="c8f37-258">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="c8f37-258">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="c8f37-259">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="c8f37-259">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="c8f37-260">The other possible value for this parameter is 'Individual'.</span><span class="sxs-lookup"><span data-stu-id="c8f37-260">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="c8f37-261">Create alerts</span><span class="sxs-lookup"><span data-stu-id="c8f37-261">Create alerts</span></span>
<span data-ttu-id="c8f37-262">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span><span class="sxs-lookup"><span data-stu-id="c8f37-262">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="c8f37-263">You can create alerts on these events.</span><span class="sxs-lookup"><span data-stu-id="c8f37-263">You can create alerts on these events.</span></span> <span data-ttu-id="c8f37-264">You can use Data Factory to capture various metrics and create alerts on metrics.</span><span class="sxs-lookup"><span data-stu-id="c8f37-264">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="c8f37-265">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span><span class="sxs-lookup"><span data-stu-id="c8f37-265">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="c8f37-266">Alerts on events</span><span class="sxs-lookup"><span data-stu-id="c8f37-266">Alerts on events</span></span>
<span data-ttu-id="c8f37-267">Azure events provide useful insights into what is happening in your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c8f37-267">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="c8f37-268">When you're using Azure Data Factory, events are generated when:</span><span class="sxs-lookup"><span data-stu-id="c8f37-268">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="c8f37-269">A data factory is created, updated, or deleted.</span><span class="sxs-lookup"><span data-stu-id="c8f37-269">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="c8f37-270">Data processing (as "runs") has started or completed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-270">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="c8f37-271">An on-demand HDInsight cluster is created or removed.</span><span class="sxs-lookup"><span data-stu-id="c8f37-271">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="c8f37-272">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span><span class="sxs-lookup"><span data-stu-id="c8f37-272">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="c8f37-273">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span><span class="sxs-lookup"><span data-stu-id="c8f37-273">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="c8f37-274">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-274">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> Currently, the portal doesn't show alerts on events. Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="c8f37-277">Specify an alert definition</span><span class="sxs-lookup"><span data-stu-id="c8f37-277">Specify an alert definition</span></span>
<span data-ttu-id="c8f37-278">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span><span class="sxs-lookup"><span data-stu-id="c8f37-278">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="c8f37-279">In the following example, the alert sends an email notification for the RunFinished operation.</span><span class="sxs-lookup"><span data-stu-id="c8f37-279">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="c8f37-280">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="c8f37-280">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="c8f37-281">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span><span class="sxs-lookup"><span data-stu-id="c8f37-281">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="c8f37-282">This example sets up the alert for all data factories in your subscription.</span><span class="sxs-lookup"><span data-stu-id="c8f37-282">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="c8f37-283">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="c8f37-283">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="c8f37-284">The following table provides the list of available operations and statuses (and substatuses).</span><span class="sxs-lookup"><span data-stu-id="c8f37-284">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="c8f37-285">Operation name</span><span class="sxs-lookup"><span data-stu-id="c8f37-285">Operation name</span></span> | <span data-ttu-id="c8f37-286">Status</span><span class="sxs-lookup"><span data-stu-id="c8f37-286">Status</span></span> | <span data-ttu-id="c8f37-287">Substatus</span><span class="sxs-lookup"><span data-stu-id="c8f37-287">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8f37-288">RunStarted</span><span class="sxs-lookup"><span data-stu-id="c8f37-288">RunStarted</span></span> |<span data-ttu-id="c8f37-289">Started</span><span class="sxs-lookup"><span data-stu-id="c8f37-289">Started</span></span> |<span data-ttu-id="c8f37-290">Starting</span><span class="sxs-lookup"><span data-stu-id="c8f37-290">Starting</span></span> |
| <span data-ttu-id="c8f37-291">RunFinished</span><span class="sxs-lookup"><span data-stu-id="c8f37-291">RunFinished</span></span> |<span data-ttu-id="c8f37-292">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="c8f37-292">Failed / Succeeded</span></span> |<span data-ttu-id="c8f37-293">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="c8f37-293">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="c8f37-294">Succeeded</span><span class="sxs-lookup"><span data-stu-id="c8f37-294">Succeeded</span></span><br/><br/><span data-ttu-id="c8f37-295">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="c8f37-295">FailedExecution</span></span><br/><br/><span data-ttu-id="c8f37-296">TimedOut</span><span class="sxs-lookup"><span data-stu-id="c8f37-296">TimedOut</span></span><br/><br/><span data-ttu-id="c8f37-297"><Canceled</span><span class="sxs-lookup"><span data-stu-id="c8f37-297"><Canceled</span></span><br/><br/><span data-ttu-id="c8f37-298">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="c8f37-298">FailedValidation</span></span><br/><br/><span data-ttu-id="c8f37-299">Abandoned</span><span class="sxs-lookup"><span data-stu-id="c8f37-299">Abandoned</span></span> |
| <span data-ttu-id="c8f37-300">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="c8f37-300">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="c8f37-301">Started</span><span class="sxs-lookup"><span data-stu-id="c8f37-301">Started</span></span> | |
| <span data-ttu-id="c8f37-302">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="c8f37-302">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="c8f37-303">Succeeded</span><span class="sxs-lookup"><span data-stu-id="c8f37-303">Succeeded</span></span> | |
| <span data-ttu-id="c8f37-304">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="c8f37-304">OnDemandClusterDeleted</span></span> |<span data-ttu-id="c8f37-305">Succeeded</span><span class="sxs-lookup"><span data-stu-id="c8f37-305">Succeeded</span></span> | |

<span data-ttu-id="c8f37-306">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span><span class="sxs-lookup"><span data-stu-id="c8f37-306">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="c8f37-307">Deploy the alert</span><span class="sxs-lookup"><span data-stu-id="c8f37-307">Deploy the alert</span></span>
<span data-ttu-id="c8f37-308">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-308">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="c8f37-309">After the resource group deployment has finished successfully, you see the following messages:</span><span class="sxs-lookup"><span data-stu-id="c8f37-309">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule. The JSON payload is similar to the JSON example.  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="c8f37-312">Retrieve the list of Azure resource group deployments</span><span class="sxs-lookup"><span data-stu-id="c8f37-312">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="c8f37-313">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-313">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="c8f37-314">Troubleshoot user events</span><span class="sxs-lookup"><span data-stu-id="c8f37-314">Troubleshoot user events</span></span>
1. <span data-ttu-id="c8f37-315">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span><span class="sxs-lookup"><span data-stu-id="c8f37-315">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Metrics and operations tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="c8f37-317">Click the **Events** tile to see the events.</span><span class="sxs-lookup"><span data-stu-id="c8f37-317">Click the **Events** tile to see the events.</span></span>

    ![Events tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="c8f37-319">On the **Events** blade, you can see details about events, filtered events, and so on.</span><span class="sxs-lookup"><span data-stu-id="c8f37-319">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Events blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="c8f37-321">Click an **Operation** in the operations list that causes an error.</span><span class="sxs-lookup"><span data-stu-id="c8f37-321">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Select an operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="c8f37-323">Click an **Error** event to see details about the error.</span><span class="sxs-lookup"><span data-stu-id="c8f37-323">Click an **Error** event to see details about the error.</span></span>

    ![Event error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="c8f37-325">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span><span class="sxs-lookup"><span data-stu-id="c8f37-325">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="c8f37-326">Here are a few examples of using the **Get-AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c8f37-326">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of the data slices for the Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="c8f37-327">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8f37-327">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="c8f37-328">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span><span class="sxs-lookup"><span data-stu-id="c8f37-328">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="c8f37-329">The alert emails might have been blocked by your email settings.</span><span class="sxs-lookup"><span data-stu-id="c8f37-329">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="c8f37-330">Alerts on metrics</span><span class="sxs-lookup"><span data-stu-id="c8f37-330">Alerts on metrics</span></span>
<span data-ttu-id="c8f37-331">In Data Factory, you can capture various metrics and create alerts on metrics.</span><span class="sxs-lookup"><span data-stu-id="c8f37-331">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="c8f37-332">You can monitor and create alerts on the following metrics for the slices in your data factory:</span><span class="sxs-lookup"><span data-stu-id="c8f37-332">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="c8f37-333">**Failed Runs**</span><span class="sxs-lookup"><span data-stu-id="c8f37-333">**Failed Runs**</span></span>
* <span data-ttu-id="c8f37-334">**Successful Runs**</span><span class="sxs-lookup"><span data-stu-id="c8f37-334">**Successful Runs**</span></span>

<span data-ttu-id="c8f37-335">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-335">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="c8f37-336">Metrics are emitted every time there is a slice run.</span><span class="sxs-lookup"><span data-stu-id="c8f37-336">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="c8f37-337">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span><span class="sxs-lookup"><span data-stu-id="c8f37-337">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="c8f37-338">To enable metrics, set up a storage account.</span><span class="sxs-lookup"><span data-stu-id="c8f37-338">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="c8f37-339">Enable metrics</span><span class="sxs-lookup"><span data-stu-id="c8f37-339">Enable metrics</span></span>
<span data-ttu-id="c8f37-340">To enable metrics, click the following from the **Data Factory** blade:</span><span class="sxs-lookup"><span data-stu-id="c8f37-340">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="c8f37-341">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="c8f37-341">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Diagnostics link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="c8f37-343">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8f37-343">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Diagnostics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="c8f37-345">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span><span class="sxs-lookup"><span data-stu-id="c8f37-345">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="c8f37-346">Set up an alert on metrics</span><span class="sxs-lookup"><span data-stu-id="c8f37-346">Set up an alert on metrics</span></span>
<span data-ttu-id="c8f37-347">Click the **Data Factory metrics** tile:</span><span class="sxs-lookup"><span data-stu-id="c8f37-347">Click the **Data Factory metrics** tile:</span></span>

![Data factory metrics tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="c8f37-349">On the **Metric** blade, click **+ Add alert** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="c8f37-349">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="c8f37-350">![Data factory metric blade > Add alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="c8f37-350">![Data factory metric blade > Add alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="c8f37-351">On the **Add an alert rule** page, do the following steps, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8f37-351">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="c8f37-352">Enter a name for the alert (example: "failed alert").</span><span class="sxs-lookup"><span data-stu-id="c8f37-352">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="c8f37-353">Enter a description for the alert (example: "send an email when a failure occurs").</span><span class="sxs-lookup"><span data-stu-id="c8f37-353">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="c8f37-354">Select a metric ("Failed Runs" vs. "Successful Runs").</span><span class="sxs-lookup"><span data-stu-id="c8f37-354">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="c8f37-355">Specify a condition and a threshold value.</span><span class="sxs-lookup"><span data-stu-id="c8f37-355">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="c8f37-356">Specify the period of time.</span><span class="sxs-lookup"><span data-stu-id="c8f37-356">Specify the period of time.</span></span>
* <span data-ttu-id="c8f37-357">Specify whether an email should be sent to owners, contributors, and readers.</span><span class="sxs-lookup"><span data-stu-id="c8f37-357">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Data factory metric blade > Add alert rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="c8f37-359">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span><span class="sxs-lookup"><span data-stu-id="c8f37-359">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Data factory metric blade > New alert added](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="c8f37-361">You should also see the number of alerts in the **Alert rules** tile.</span><span class="sxs-lookup"><span data-stu-id="c8f37-361">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="c8f37-362">Click the **Alert rules** tile.</span><span class="sxs-lookup"><span data-stu-id="c8f37-362">Click the **Alert rules** tile.</span></span>

![Data factory metric blade - Alert rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="c8f37-364">On the **Alerts rules** blade, you see any existing alerts.</span><span class="sxs-lookup"><span data-stu-id="c8f37-364">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="c8f37-365">To add an alert, click **Add alert** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="c8f37-365">To add an alert, click **Add alert** on the toolbar.</span></span>

![Alert rules blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="c8f37-367">Alert notifications</span><span class="sxs-lookup"><span data-stu-id="c8f37-367">Alert notifications</span></span>
<span data-ttu-id="c8f37-368">After the alert rule matches the condition, you should get an email that says the alert is activated.</span><span class="sxs-lookup"><span data-stu-id="c8f37-368">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="c8f37-369">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span><span class="sxs-lookup"><span data-stu-id="c8f37-369">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="c8f37-370">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span><span class="sxs-lookup"><span data-stu-id="c8f37-370">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="c8f37-371">Deploy alerts by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8f37-371">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="c8f37-372">You can deploy alerts for metrics the same way that you do for events.</span><span class="sxs-lookup"><span data-stu-id="c8f37-372">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="c8f37-373">**Alert definition**</span><span class="sxs-lookup"><span data-stu-id="c8f37-373">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="c8f37-374">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span><span class="sxs-lookup"><span data-stu-id="c8f37-374">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="c8f37-375">*metricName* currently supports two values:</span><span class="sxs-lookup"><span data-stu-id="c8f37-375">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="c8f37-376">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="c8f37-376">FailedRuns</span></span>
* <span data-ttu-id="c8f37-377">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="c8f37-377">SuccessfulRuns</span></span>

<span data-ttu-id="c8f37-378">**Deploy the alert**</span><span class="sxs-lookup"><span data-stu-id="c8f37-378">**Deploy the alert**</span></span>

<span data-ttu-id="c8f37-379">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c8f37-379">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="c8f37-380">You should see following message after a successful deployment:</span><span class="sxs-lookup"><span data-stu-id="c8f37-380">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="c8f37-381">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span><span class="sxs-lookup"><span data-stu-id="c8f37-381">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="c8f37-382">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span><span class="sxs-lookup"><span data-stu-id="c8f37-382">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="c8f37-383">Move a data factory to a different resource group or subscription</span><span class="sxs-lookup"><span data-stu-id="c8f37-383">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="c8f37-384">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-384">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Move data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="c8f37-386">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span><span class="sxs-lookup"><span data-stu-id="c8f37-386">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Move resources dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-monitor-manage-pipelines/MoveResources.png)

































