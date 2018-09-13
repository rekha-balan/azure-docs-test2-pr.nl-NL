---
title: Check status, set up logging, and get alerts - Azure Logic Apps | Microsoft Docs
description: Monitor status, log diagnostics data, and set up alerts for Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.date: 07/21/2017
ms.openlocfilehash: a08cd6289fc85b79ccec731126a33a9549d60546
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803509"
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="4120f-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4120f-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="4120f-104">After you [create and run a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), you can check its runs history, trigger history, status, and performance.</span><span class="sxs-lookup"><span data-stu-id="4120f-104">After you [create and run a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="4120f-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="4120f-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span><span class="sxs-lookup"><span data-stu-id="4120f-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="4120f-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4120f-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="4120f-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="4120f-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="4120f-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span><span class="sxs-lookup"><span data-stu-id="4120f-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="4120f-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="4120f-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="4120f-111">View runs and trigger history for your logic app</span><span class="sxs-lookup"><span data-stu-id="4120f-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="4120f-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **All services**.</span><span class="sxs-lookup"><span data-stu-id="4120f-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **All services**.</span></span> <span data-ttu-id="4120f-113">In the search box, type "logic apps", and choose **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="4120f-113">In the search box, type "logic apps", and choose **Logic apps**.</span></span>

   ![Find your logic app](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="4120f-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4120f-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="4120f-116">Select your logic app, then choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="4120f-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="4120f-117">The Azure portal shows the runs history and trigger history for your logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="4120f-118">For example:</span><span class="sxs-lookup"><span data-stu-id="4120f-118">For example:</span></span>

   ![Logic app runs history and trigger history](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="4120f-120">**Runs history** shows all the runs for your logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="4120f-121">**Trigger History** shows all the trigger activity for your logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="4120f-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="4120f-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4120f-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="4120f-124">To view the steps from a specific run, under **Runs history**, select that run.</span><span class="sxs-lookup"><span data-stu-id="4120f-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="4120f-125">The monitor view shows each step in that run.</span><span class="sxs-lookup"><span data-stu-id="4120f-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="4120f-126">For example:</span><span class="sxs-lookup"><span data-stu-id="4120f-126">For example:</span></span>

   ![Actions for a specific run](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="4120f-128">To get more details about the run, choose **Run Details**.</span><span class="sxs-lookup"><span data-stu-id="4120f-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="4120f-129">This information summarizes the steps, status, inputs, and outputs for the run.</span><span class="sxs-lookup"><span data-stu-id="4120f-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Choose "Run Details"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="4120f-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="4120f-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="4120f-132">To get details about a specific step, choose that step.</span><span class="sxs-lookup"><span data-stu-id="4120f-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="4120f-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span><span class="sxs-lookup"><span data-stu-id="4120f-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="4120f-134">For example:</span><span class="sxs-lookup"><span data-stu-id="4120f-134">For example:</span></span>

   ![Step details](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="4120f-136">All runtime details and events are encrypted within the Logic Apps service.</span><span class="sxs-lookup"><span data-stu-id="4120f-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="4120f-137">They are decrypted only when a user requests to view that data.</span><span class="sxs-lookup"><span data-stu-id="4120f-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="4120f-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span></span>

6. <span data-ttu-id="4120f-139">To get details about a specific trigger event, go back to the **Overview** pane.</span><span class="sxs-lookup"><span data-stu-id="4120f-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="4120f-140">Under **Trigger history**, select the trigger event.</span><span class="sxs-lookup"><span data-stu-id="4120f-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="4120f-141">You can now review details like inputs and outputs, for example:</span><span class="sxs-lookup"><span data-stu-id="4120f-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Trigger event output details](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="4120f-143">Turn on diagnostics logging for your logic app</span><span class="sxs-lookup"><span data-stu-id="4120f-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="4120f-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="4120f-145">Log Analytics is a service in Azure that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span><span class="sxs-lookup"><span data-stu-id="4120f-145">Log Analytics is a service in Azure that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="4120f-146">Before you start, you need to have a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="4120f-146">Before you start, you need to have a Log Analytics workspace.</span></span> <span data-ttu-id="4120f-147">Learn [how to create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-147">Learn [how to create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span></span>

1. <span data-ttu-id="4120f-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="4120f-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span><span class="sxs-lookup"><span data-stu-id="4120f-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Go to Monitoring, Diagnostics, Diagnostic Settings](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="4120f-151">Under **Diagnostics settings**, choose **On**.</span><span class="sxs-lookup"><span data-stu-id="4120f-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Turn on diagnostic logs](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="4120f-153">Now select the Log Analytics workspace and event category for logging as shown:</span><span class="sxs-lookup"><span data-stu-id="4120f-153">Now select the Log Analytics workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="4120f-154">Select **Send to Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4120f-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="4120f-155">Under **Log Analytics**, choose **Configure**.</span><span class="sxs-lookup"><span data-stu-id="4120f-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="4120f-156">Under **OMS Workspaces**, select the Log Analytics workspace to use for logging.</span><span class="sxs-lookup"><span data-stu-id="4120f-156">Under **OMS Workspaces**, select the Log Analytics workspace to use for logging.</span></span>
   4. <span data-ttu-id="4120f-157">Under **Log**, select the **WorkflowRuntime** category.</span><span class="sxs-lookup"><span data-stu-id="4120f-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="4120f-158">Choose the metric interval.</span><span class="sxs-lookup"><span data-stu-id="4120f-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="4120f-159">When you're done, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="4120f-159">When you're done, choose **Save**.</span></span>

   ![Select Log Analytics workspace and data for logging](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="4120f-161">Now, you can find events and other data for trigger events, run events, and action events.</span><span class="sxs-lookup"><span data-stu-id="4120f-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="4120f-162">Find events and data for your logic app</span><span class="sxs-lookup"><span data-stu-id="4120f-162">Find events and data for your logic app</span></span>

<span data-ttu-id="4120f-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="4120f-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="4120f-164">In the [Azure portal](https://portal.azure.com), choose **All Services**.</span><span class="sxs-lookup"><span data-stu-id="4120f-164">In the [Azure portal](https://portal.azure.com), choose **All Services**.</span></span> <span data-ttu-id="4120f-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span><span class="sxs-lookup"><span data-stu-id="4120f-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Choose "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="4120f-167">Under **Log Analytics**, find and select your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="4120f-167">Under **Log Analytics**, find and select your Log Analytics workspace.</span></span> 

   ![Select your Log Analytics workspace](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="4120f-169">Under **Management**, choose **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="4120f-169">Under **Management**, choose **Log Search**.</span></span>

   ![Choose "Log Search"](media/logic-apps-monitor-your-logic-apps/log-search.png)

4. <span data-ttu-id="4120f-171">In the search box, specify a field that you want to find, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4120f-171">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="4120f-172">When you start typing, you see possible matches and operations that you can use.</span><span class="sxs-lookup"><span data-stu-id="4120f-172">When you start typing, you see possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="4120f-173">For example, to find the top 10 events that happened, enter and select this search query: **search Category == "WorkflowRuntime" | limit 10**</span><span class="sxs-lookup"><span data-stu-id="4120f-173">For example, to find the top 10 events that happened, enter and select this search query: **search Category == "WorkflowRuntime" | limit 10**</span></span>

   ![Enter search string](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="4120f-175">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-175">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

5. <span data-ttu-id="4120f-176">On the results page, in the left bar, choose the timeframe that you want to view.</span><span class="sxs-lookup"><span data-stu-id="4120f-176">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="4120f-177">To refine your query by adding a filter, choose **+Add**.</span><span class="sxs-lookup"><span data-stu-id="4120f-177">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Choose timeframe for query results](media/logic-apps-monitor-your-logic-apps/query-results.png)

6. <span data-ttu-id="4120f-179">Under **Add Filters**, enter the filter name so you can find the filter you want.</span><span class="sxs-lookup"><span data-stu-id="4120f-179">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="4120f-180">Select the filter, and choose **+Add**.</span><span class="sxs-lookup"><span data-stu-id="4120f-180">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="4120f-181">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="4120f-181">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="4120f-182">Here the filter for **status_s** is already selected.</span><span class="sxs-lookup"><span data-stu-id="4120f-182">Here the filter for **status_s** is already selected.</span></span>

   ![Select filter](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

7. <span data-ttu-id="4120f-184">In the left bar, select the filter value that you want to use, and choose **Apply**.</span><span class="sxs-lookup"><span data-stu-id="4120f-184">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Select filter value, choose "Apply"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

8. <span data-ttu-id="4120f-186">Now return to the query that you're building.</span><span class="sxs-lookup"><span data-stu-id="4120f-186">Now return to the query that you're building.</span></span> <span data-ttu-id="4120f-187">Your query is updated with your selected filter and value.</span><span class="sxs-lookup"><span data-stu-id="4120f-187">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="4120f-188">Your previous results are now filtered too.</span><span class="sxs-lookup"><span data-stu-id="4120f-188">Your previous results are now filtered too.</span></span>

   ![Return to your query with filtered results](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

9. <span data-ttu-id="4120f-190">To save your query for future use, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="4120f-190">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="4120f-191">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="4120f-191">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="4120f-192">Extend how and where you use diagnostic data with other services</span><span class="sxs-lookup"><span data-stu-id="4120f-192">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="4120f-193">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span><span class="sxs-lookup"><span data-stu-id="4120f-193">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="4120f-194">Archive Azure Diagnostics Logs in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4120f-194">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="4120f-195">Stream Azure Diagnostics Logs to Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4120f-195">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="4120f-196">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-196">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="4120f-197">For example:</span><span class="sxs-lookup"><span data-stu-id="4120f-197">For example:</span></span>

* [<span data-ttu-id="4120f-198">Stream data from Event Hubs to Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4120f-198">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="4120f-199">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span><span class="sxs-lookup"><span data-stu-id="4120f-199">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="4120f-200">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-200">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="4120f-201">Then select the options for where you want to send diagnostic data:</span><span class="sxs-lookup"><span data-stu-id="4120f-201">Then select the options for where you want to send diagnostic data:</span></span>

![Send data to Azure storage account or event hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="4120f-203">Retention periods apply only when you choose to use a storage account.</span><span class="sxs-lookup"><span data-stu-id="4120f-203">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="4120f-204">Set up alerts for your logic app</span><span class="sxs-lookup"><span data-stu-id="4120f-204">Set up alerts for your logic app</span></span>

<span data-ttu-id="4120f-205">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-205">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="4120f-206">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4120f-206">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="4120f-207">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span><span class="sxs-lookup"><span data-stu-id="4120f-207">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="4120f-208">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span><span class="sxs-lookup"><span data-stu-id="4120f-208">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="4120f-209">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span><span class="sxs-lookup"><span data-stu-id="4120f-209">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Add an alert for your logic app](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="4120f-211">On the **Add an alert rule** blade, create your alert as shown:</span><span class="sxs-lookup"><span data-stu-id="4120f-211">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="4120f-212">Under **Resource**, select your logic app, if not already selected.</span><span class="sxs-lookup"><span data-stu-id="4120f-212">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="4120f-213">Give a name and description for your alert.</span><span class="sxs-lookup"><span data-stu-id="4120f-213">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="4120f-214">Select a **Metric** or event that you want to track.</span><span class="sxs-lookup"><span data-stu-id="4120f-214">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="4120f-215">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span><span class="sxs-lookup"><span data-stu-id="4120f-215">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="4120f-216">Select whether to send mail for the alert.</span><span class="sxs-lookup"><span data-stu-id="4120f-216">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="4120f-217">Specify any other email addresses for sending the alert.</span><span class="sxs-lookup"><span data-stu-id="4120f-217">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="4120f-218">You can also specify a webhook URL where you want to send the alert.</span><span class="sxs-lookup"><span data-stu-id="4120f-218">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="4120f-219">For example, this rule sends an alert when five or more runs fail in an hour:</span><span class="sxs-lookup"><span data-stu-id="4120f-219">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Create metric alert rule](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="4120f-221">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span><span class="sxs-lookup"><span data-stu-id="4120f-221">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="4120f-222">Post to Slack</span><span class="sxs-lookup"><span data-stu-id="4120f-222">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="4120f-223">Send a text</span><span class="sxs-lookup"><span data-stu-id="4120f-223">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="4120f-224">Add a message to a queue</span><span class="sxs-lookup"><span data-stu-id="4120f-224">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="4120f-225">Azure Diagnostics event settings and details</span><span class="sxs-lookup"><span data-stu-id="4120f-225">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="4120f-226">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span><span class="sxs-lookup"><span data-stu-id="4120f-226">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="4120f-227">To programmatically set up monitoring, tracking, and logging, you can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="4120f-227">To programmatically set up monitoring, tracking, and logging, you can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="4120f-228">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span><span class="sxs-lookup"><span data-stu-id="4120f-228">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="4120f-229">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span><span class="sxs-lookup"><span data-stu-id="4120f-229">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="4120f-230">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span><span class="sxs-lookup"><span data-stu-id="4120f-230">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="4120f-231">You can use a request trigger, HTTP trigger, or webhook trigger.</span><span class="sxs-lookup"><span data-stu-id="4120f-231">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="4120f-232">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span><span class="sxs-lookup"><span data-stu-id="4120f-232">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="4120f-233">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span><span class="sxs-lookup"><span data-stu-id="4120f-233">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="4120f-234">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span><span class="sxs-lookup"><span data-stu-id="4120f-234">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="4120f-235">For example, suppose you want to track data like an "order ID" in your telemetry:</span><span class="sxs-lookup"><span data-stu-id="4120f-235">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="4120f-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="4120f-236">Next steps</span></span>

* [<span data-ttu-id="4120f-237">Create templates for logic app deployment and release management</span><span class="sxs-lookup"><span data-stu-id="4120f-237">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="4120f-238">B2B scenarios with Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="4120f-238">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="4120f-239">Monitor B2B messages</span><span class="sxs-lookup"><span data-stu-id="4120f-239">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
