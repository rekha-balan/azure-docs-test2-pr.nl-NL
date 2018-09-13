---
title: Monitor Azure Functions
description: Learn how to use Azure Application Insights with Azure Functions for monitoring function execution.
services: functions
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/15/2017
ms.author: glenga
ms.openlocfilehash: 9c39d621bfc8df338a4556fd412ae54489982074
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810159"
---
# <a name="monitor-azure-functions"></a><span data-ttu-id="4e8cf-104">Monitor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4e8cf-104">Monitor Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="4e8cf-105">Overview</span><span class="sxs-lookup"><span data-stu-id="4e8cf-105">Overview</span></span> 

<span data-ttu-id="4e8cf-106">[Azure Functions](functions-overview.md) offers built-in integration with [Azure Application Insights](../application-insights/app-insights-overview.md) for monitoring functions.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-106">[Azure Functions](functions-overview.md) offers built-in integration with [Azure Application Insights](../application-insights/app-insights-overview.md) for monitoring functions.</span></span> <span data-ttu-id="4e8cf-107">This article shows how to configure Functions to send telemetry data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-107">This article shows how to configure Functions to send telemetry data to Application Insights.</span></span>

![Application Insights Metrics Explorer](media/functions-monitoring/metrics-explorer.png)

<span data-ttu-id="4e8cf-109">Functions also has [built-in monitoring that doesn't use Application Insights](#monitoring-without-application-insights).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-109">Functions also has [built-in monitoring that doesn't use Application Insights](#monitoring-without-application-insights).</span></span> <span data-ttu-id="4e8cf-110">We recommend Application Insights because it offers more data and better ways to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-110">We recommend Application Insights because it offers more data and better ways to analyze the data.</span></span>

## <a name="application-insights-pricing-and-limits"></a><span data-ttu-id="4e8cf-111">Application Insights pricing and limits</span><span class="sxs-lookup"><span data-stu-id="4e8cf-111">Application Insights pricing and limits</span></span>

<span data-ttu-id="4e8cf-112">You can try out Application Insights integration with Function Apps for free.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-112">You can try out Application Insights integration with Function Apps for free.</span></span> <span data-ttu-id="4e8cf-113">However, there's a daily limit to how much data can be processed for free, and you might hit that limit during testing.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-113">However, there's a daily limit to how much data can be processed for free, and you might hit that limit during testing.</span></span> <span data-ttu-id="4e8cf-114">Azure provides portal and email notifications when the you're approaching your daily limit.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-114">Azure provides portal and email notifications when the you're approaching your daily limit.</span></span>  <span data-ttu-id="4e8cf-115">But if you miss those alerts and hit the limit, new logs won't appear in Application Insights queries.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-115">But if you miss those alerts and hit the limit, new logs won't appear in Application Insights queries.</span></span> <span data-ttu-id="4e8cf-116">So be aware of the limit to avoid unnecessary troubleshooting time.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-116">So be aware of the limit to avoid unnecessary troubleshooting time.</span></span> <span data-ttu-id="4e8cf-117">For more information, see [Manage pricing and data volume in Application Insights](../application-insights/app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-117">For more information, see [Manage pricing and data volume in Application Insights](../application-insights/app-insights-pricing.md).</span></span>

## <a name="enable-app-insights-integration"></a><span data-ttu-id="4e8cf-118">Enable App Insights integration</span><span class="sxs-lookup"><span data-stu-id="4e8cf-118">Enable App Insights integration</span></span>

<span data-ttu-id="4e8cf-119">For a function app to send data to Application Insights, it needs to know the instrumentation key of an Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-119">For a function app to send data to Application Insights, it needs to know the instrumentation key of an Application Insights resource.</span></span> <span data-ttu-id="4e8cf-120">The key has to be provided in an app setting named APPINSIGHTS_INSTRUMENTATIONKEY.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-120">The key has to be provided in an app setting named APPINSIGHTS_INSTRUMENTATIONKEY.</span></span>

<span data-ttu-id="4e8cf-121">You can set up this connection in the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="4e8cf-121">You can set up this connection in the [Azure portal](https://portal.azure.com):</span></span>

* [<span data-ttu-id="4e8cf-122">Automatically for a new function app</span><span class="sxs-lookup"><span data-stu-id="4e8cf-122">Automatically for a new function app</span></span>](#new-function-app)
* [<span data-ttu-id="4e8cf-123">Manually connect an App Insights resource</span><span class="sxs-lookup"><span data-stu-id="4e8cf-123">Manually connect an App Insights resource</span></span>](#manually-connect-an-app-insights-resource)

### <a name="new-function-app"></a><span data-ttu-id="4e8cf-124">New function app</span><span class="sxs-lookup"><span data-stu-id="4e8cf-124">New function app</span></span>

1. <span data-ttu-id="4e8cf-125">Go to the function app **Create** page.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-125">Go to the function app **Create** page.</span></span>

1. <span data-ttu-id="4e8cf-126">Set the **Application Insights** switch **On**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-126">Set the **Application Insights** switch **On**.</span></span>

2. <span data-ttu-id="4e8cf-127">Select an **Application Insights Location**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-127">Select an **Application Insights Location**.</span></span>

   <span data-ttu-id="4e8cf-128">Choose the region that is closest to your function app's region, in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want your data to be stored.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-128">Choose the region that is closest to your function app's region, in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want your data to be stored.</span></span>

   ![Enable Application Insights while creating a function app](media/functions-monitoring/enable-ai-new-function-app.png)

3. <span data-ttu-id="4e8cf-130">Enter the other required information.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-130">Enter the other required information.</span></span>

1. <span data-ttu-id="4e8cf-131">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-131">Select **Create**.</span></span>

<span data-ttu-id="4e8cf-132">The next step is to [disable built-in logging](#disable-built-in-logging).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-132">The next step is to [disable built-in logging](#disable-built-in-logging).</span></span>

### <a name="manually-connect-an-app-insights-resource"></a><span data-ttu-id="4e8cf-133">Manually connect an App Insights resource</span><span class="sxs-lookup"><span data-stu-id="4e8cf-133">Manually connect an App Insights resource</span></span> 

1. <span data-ttu-id="4e8cf-134">Create the Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-134">Create the Application Insights resource.</span></span> <span data-ttu-id="4e8cf-135">Set application type to **General**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-135">Set application type to **General**.</span></span>

   ![Create an Application Insights resource, type General](media/functions-monitoring/ai-general.png)

2. <span data-ttu-id="4e8cf-137">Copy the instrumentation key from the **Essentials** page of the Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-137">Copy the instrumentation key from the **Essentials** page of the Application Insights resource.</span></span> <span data-ttu-id="4e8cf-138">Hover over the end of the displayed key value to get a **Click to copy** button.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-138">Hover over the end of the displayed key value to get a **Click to copy** button.</span></span>

   ![Copy the Application Insights instrumentation key](media/functions-monitoring/copy-ai-key.png)

1. <span data-ttu-id="4e8cf-140">In the function app's **Application settings** page, [add an app setting](functions-how-to-use-azure-function-app-settings.md#settings) by clicking **Add new setting**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-140">In the function app's **Application settings** page, [add an app setting](functions-how-to-use-azure-function-app-settings.md#settings) by clicking **Add new setting**.</span></span> <span data-ttu-id="4e8cf-141">Name the new setting APPINSIGHTS_INSTRUMENTATIONKEY and paste the copied instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-141">Name the new setting APPINSIGHTS_INSTRUMENTATIONKEY and paste the copied instrumentation key.</span></span>

   ![Add instrumentation key to app settings](media/functions-monitoring/add-ai-key.png)

1. <span data-ttu-id="4e8cf-143">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-143">Click **Save**.</span></span>

## <a name="disable-built-in-logging"></a><span data-ttu-id="4e8cf-144">Disable built-in logging</span><span class="sxs-lookup"><span data-stu-id="4e8cf-144">Disable built-in logging</span></span>

<span data-ttu-id="4e8cf-145">If you enable Application Insights, we recommend that you disable the [built-in logging that uses Azure storage](#logging-to-storage).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-145">If you enable Application Insights, we recommend that you disable the [built-in logging that uses Azure storage](#logging-to-storage).</span></span> <span data-ttu-id="4e8cf-146">The built-in logging is useful for testing with light workloads but is not intended for high-load production use.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-146">The built-in logging is useful for testing with light workloads but is not intended for high-load production use.</span></span> <span data-ttu-id="4e8cf-147">For production monitoring, Application Insights is recommended.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-147">For production monitoring, Application Insights is recommended.</span></span> <span data-ttu-id="4e8cf-148">If built-in logging is used in production, the logging record may be incomplete due to throttling on Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-148">If built-in logging is used in production, the logging record may be incomplete due to throttling on Azure Storage.</span></span>

<span data-ttu-id="4e8cf-149">To disable built-in logging, delete the `AzureWebJobsDashboard` app setting.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-149">To disable built-in logging, delete the `AzureWebJobsDashboard` app setting.</span></span> <span data-ttu-id="4e8cf-150">For information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-150">For information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> <span data-ttu-id="4e8cf-151">Before deleting the app setting, make sure that no existing functions in the same function app use it for Azure Storage triggers or bindings.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-151">Before deleting the app setting, make sure that no existing functions in the same function app use it for Azure Storage triggers or bindings.</span></span>

## <a name="view-telemetry-in-monitor-tab"></a><span data-ttu-id="4e8cf-152">View telemetry in Monitor tab</span><span class="sxs-lookup"><span data-stu-id="4e8cf-152">View telemetry in Monitor tab</span></span>

<span data-ttu-id="4e8cf-153">After you have set up Application Insights integration as shown in the previous sections, you can view telemetry data in the **Monitor** tab.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-153">After you have set up Application Insights integration as shown in the previous sections, you can view telemetry data in the **Monitor** tab.</span></span>

1. <span data-ttu-id="4e8cf-154">In the function app page, select a function that has run at least once after Application Insights was configured, and then select the **Monitor** tab.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-154">In the function app page, select a function that has run at least once after Application Insights was configured, and then select the **Monitor** tab.</span></span>

   ![Select Monitor tab](media/functions-monitoring/monitor-tab.png)

2. <span data-ttu-id="4e8cf-156">Select **Refresh** periodically until the list of function invocations appears.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-156">Select **Refresh** periodically until the list of function invocations appears.</span></span>

   <span data-ttu-id="4e8cf-157">It may take up to 5 minutes for the list to appear, due to the way the telemetry client batches data for transmission to the server.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-157">It may take up to 5 minutes for the list to appear, due to the way the telemetry client batches data for transmission to the server.</span></span> <span data-ttu-id="4e8cf-158">(This delay doesn't apply to the [Live Metrics Stream](../application-insights/app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-158">(This delay doesn't apply to the [Live Metrics Stream](../application-insights/app-insights-live-stream.md).</span></span> <span data-ttu-id="4e8cf-159">That service connects to the Functions host when you load the page, so logs are streamed directly to the page.)</span><span class="sxs-lookup"><span data-stu-id="4e8cf-159">That service connects to the Functions host when you load the page, so logs are streamed directly to the page.)</span></span>

   ![Invocations list](media/functions-monitoring/monitor-tab-ai-invocations.png)

2. <span data-ttu-id="4e8cf-161">To see the logs for a particular function invocation, select the **Date** column link for that invocation.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-161">To see the logs for a particular function invocation, select the **Date** column link for that invocation.</span></span>

   ![Invocation details link](media/functions-monitoring/invocation-details-link-ai.png)

   <span data-ttu-id="4e8cf-163">The logging output for that invocation appears in a new page.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-163">The logging output for that invocation appears in a new page.</span></span>

   ![Invocation details](media/functions-monitoring/invocation-details-ai.png)

<span data-ttu-id="4e8cf-165">Both pages (invocation list and details) link to the Application Insights Analytics query that retrieves the data:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-165">Both pages (invocation list and details) link to the Application Insights Analytics query that retrieves the data:</span></span>

![Run in Application Insights](media/functions-monitoring/run-in-ai.png)

![Application Insights Analytics invocation list](media/functions-monitoring/ai-analytics-invocation-list.png)

<span data-ttu-id="4e8cf-168">From these queries, you can see that the invocation list is limited to the last 30 days, no more than 20 rows (`where timestamp > ago(30d) | take 20`) and the invocation details list is for the last 30 days with no limit.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-168">From these queries, you can see that the invocation list is limited to the last 30 days, no more than 20 rows (`where timestamp > ago(30d) | take 20`) and the invocation details list is for the last 30 days with no limit.</span></span>

<span data-ttu-id="4e8cf-169">For more information, see [Query telemetry data](#query-telemetry-data) later in this article.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-169">For more information, see [Query telemetry data](#query-telemetry-data) later in this article.</span></span>

## <a name="view-telemetry-in-app-insights"></a><span data-ttu-id="4e8cf-170">View telemetry in App Insights</span><span class="sxs-lookup"><span data-stu-id="4e8cf-170">View telemetry in App Insights</span></span>

<span data-ttu-id="4e8cf-171">To open Application Insights from a function app in the Azure portal, select the **Application Insights** link in the **Configured features** section of the function app's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-171">To open Application Insights from a function app in the Azure portal, select the **Application Insights** link in the **Configured features** section of the function app's **Overview** page.</span></span>

![Application Insights link on Overview page](media/functions-monitoring/ai-link.png)


<span data-ttu-id="4e8cf-173">For information about how to use Application Insights, see the [Application Insights documentation](https://docs.microsoft.com/azure/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-173">For information about how to use Application Insights, see the [Application Insights documentation](https://docs.microsoft.com/azure/application-insights/).</span></span> <span data-ttu-id="4e8cf-174">This section shows some examples of how to view data in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-174">This section shows some examples of how to view data in Application Insights.</span></span> <span data-ttu-id="4e8cf-175">If you are already familiar with Application Insights, you can go directly to [the sections about configuring and customizing the telemetry data](#configure-categories-and-log-levels).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-175">If you are already familiar with Application Insights, you can go directly to [the sections about configuring and customizing the telemetry data](#configure-categories-and-log-levels).</span></span>

<span data-ttu-id="4e8cf-176">In [Metrics Explorer](../application-insights/app-insights-metrics-explorer.md), you can create charts and alerts based on metrics such as number of function invocations, execution time, and success rate.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-176">In [Metrics Explorer](../application-insights/app-insights-metrics-explorer.md), you can create charts and alerts based on metrics such as number of function invocations, execution time, and success rate.</span></span>

![Metrics Explorer](media/functions-monitoring/metrics-explorer.png)

<span data-ttu-id="4e8cf-178">On the [Failures](../application-insights/app-insights-asp-net-exceptions.md) tab, you can create charts and alerts based on function failures and server exceptions.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-178">On the [Failures](../application-insights/app-insights-asp-net-exceptions.md) tab, you can create charts and alerts based on function failures and server exceptions.</span></span> <span data-ttu-id="4e8cf-179">The **Operation Name** is the function name.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-179">The **Operation Name** is the function name.</span></span> <span data-ttu-id="4e8cf-180">Failures in dependencies are not shown unless you implement [custom telemetry](#custom-telemetry-in-c-functions) for dependencies.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-180">Failures in dependencies are not shown unless you implement [custom telemetry](#custom-telemetry-in-c-functions) for dependencies.</span></span>

![Failures](media/functions-monitoring/failures.png)

<span data-ttu-id="4e8cf-182">On the [Performance](../application-insights/app-insights-performance-counters.md) tab, you can analyze performance issues.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-182">On the [Performance](../application-insights/app-insights-performance-counters.md) tab, you can analyze performance issues.</span></span>

![Performance](media/functions-monitoring/performance.png)

<span data-ttu-id="4e8cf-184">The **Servers** tab shows resource utilization and throughput per server.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-184">The **Servers** tab shows resource utilization and throughput per server.</span></span> <span data-ttu-id="4e8cf-185">This data can be useful for debugging scenarios where functions are bogging down your underlying resources.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-185">This data can be useful for debugging scenarios where functions are bogging down your underlying resources.</span></span> <span data-ttu-id="4e8cf-186">Servers are referred to as **Cloud role instances**.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-186">Servers are referred to as **Cloud role instances**.</span></span>

![Servers](media/functions-monitoring/servers.png)

<span data-ttu-id="4e8cf-188">The [Live Metrics Stream](../application-insights/app-insights-live-stream.md) tab shows metrics data as it is created in real time.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-188">The [Live Metrics Stream](../application-insights/app-insights-live-stream.md) tab shows metrics data as it is created in real time.</span></span>

![Live stream](media/functions-monitoring/live-stream.png)

## <a name="query-telemetry-data"></a><span data-ttu-id="4e8cf-190">Query telemetry data</span><span class="sxs-lookup"><span data-stu-id="4e8cf-190">Query telemetry data</span></span>

<span data-ttu-id="4e8cf-191">[Application Insights Analytics](../application-insights/app-insights-analytics.md) gives you access to all of the telemetry data in the form of tables in a database.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-191">[Application Insights Analytics](../application-insights/app-insights-analytics.md) gives you access to all of the telemetry data in the form of tables in a database.</span></span> <span data-ttu-id="4e8cf-192">Analytics provides a query language for extracting, manipulating, and visualizing the data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-192">Analytics provides a query language for extracting, manipulating, and visualizing the data.</span></span>

![Select Analytics](media/functions-monitoring/select-analytics.png)

![Analytics example](media/functions-monitoring/analytics-traces.png)

<span data-ttu-id="4e8cf-195">Here's a query example.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-195">Here's a query example.</span></span> <span data-ttu-id="4e8cf-196">This one shows the distribution of requests per worker over the last 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-196">This one shows the distribution of requests per worker over the last 30 minutes.</span></span>

```
requests
| where timestamp > ago(30m) 
| summarize count() by cloud_RoleInstance, bin(timestamp, 1m)
| render timechart
```

<span data-ttu-id="4e8cf-197">The tables that are available are shown in the **Schema** tab of the left pane.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-197">The tables that are available are shown in the **Schema** tab of the left pane.</span></span> <span data-ttu-id="4e8cf-198">You can find data generated by function invocations in the following tables:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-198">You can find data generated by function invocations in the following tables:</span></span>

* <span data-ttu-id="4e8cf-199">**traces** - Logs created by the runtime and by function code.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-199">**traces** - Logs created by the runtime and by function code.</span></span>
* <span data-ttu-id="4e8cf-200">**requests** - One for each function invocation.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-200">**requests** - One for each function invocation.</span></span>
* <span data-ttu-id="4e8cf-201">**exceptions** - Any exceptions thrown by the runtime.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-201">**exceptions** - Any exceptions thrown by the runtime.</span></span>
* <span data-ttu-id="4e8cf-202">**customMetrics** - Count of successful and failing invocations, success rate, duration.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-202">**customMetrics** - Count of successful and failing invocations, success rate, duration.</span></span>
* <span data-ttu-id="4e8cf-203">**customEvents** - Events tracked by the runtime, for example:  HTTP requests that trigger a function.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-203">**customEvents** - Events tracked by the runtime, for example:  HTTP requests that trigger a function.</span></span>
* <span data-ttu-id="4e8cf-204">**performanceCounters** - Info about the performance of the servers that the functions are running on.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-204">**performanceCounters** - Info about the performance of the servers that the functions are running on.</span></span>

<span data-ttu-id="4e8cf-205">The other tables are for availability tests and client/browser telemetry.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-205">The other tables are for availability tests and client/browser telemetry.</span></span> <span data-ttu-id="4e8cf-206">You can implement custom telemetry to add data to them.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-206">You can implement custom telemetry to add data to them.</span></span>

<span data-ttu-id="4e8cf-207">Within each table, some of the Functions-specific data is in a `customDimensions` field.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-207">Within each table, some of the Functions-specific data is in a `customDimensions` field.</span></span>  <span data-ttu-id="4e8cf-208">For example, the following query retrieves all traces that have log level `Error`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-208">For example, the following query retrieves all traces that have log level `Error`.</span></span>

```
traces 
| where customDimensions.LogLevel == "Error"
```

<span data-ttu-id="4e8cf-209">The runtime provides `customDimensions.LogLevel` and `customDimensions.Category`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-209">The runtime provides `customDimensions.LogLevel` and `customDimensions.Category`.</span></span> <span data-ttu-id="4e8cf-210">You can provide additional fields in logs you write in your function code.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-210">You can provide additional fields in logs you write in your function code.</span></span> <span data-ttu-id="4e8cf-211">See [Structured logging](#structured-logging) later in this article.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-211">See [Structured logging](#structured-logging) later in this article.</span></span>

## <a name="configure-categories-and-log-levels"></a><span data-ttu-id="4e8cf-212">Configure categories and log levels</span><span class="sxs-lookup"><span data-stu-id="4e8cf-212">Configure categories and log levels</span></span>

<span data-ttu-id="4e8cf-213">You can use Application Insights without any custom configuration, but the default configuration can result in high volumes of data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-213">You can use Application Insights without any custom configuration, but the default configuration can result in high volumes of data.</span></span> <span data-ttu-id="4e8cf-214">If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-214">If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights.</span></span> <span data-ttu-id="4e8cf-215">The remainder of this article shows how to configure and customize the data that your functions send to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-215">The remainder of this article shows how to configure and customize the data that your functions send to Application Insights.</span></span>

### <a name="categories"></a><span data-ttu-id="4e8cf-216">Categories</span><span class="sxs-lookup"><span data-stu-id="4e8cf-216">Categories</span></span>

<span data-ttu-id="4e8cf-217">The Azure Functions logger includes a *category* for every log.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-217">The Azure Functions logger includes a *category* for every log.</span></span> <span data-ttu-id="4e8cf-218">The category indicates which part of the runtime code or your function code wrote the log.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-218">The category indicates which part of the runtime code or your function code wrote the log.</span></span> 

<span data-ttu-id="4e8cf-219">The Functions runtime creates logs that have a category beginning with "Host".</span><span class="sxs-lookup"><span data-stu-id="4e8cf-219">The Functions runtime creates logs that have a category beginning with "Host".</span></span> <span data-ttu-id="4e8cf-220">For example, the "function started," "function executed," and "function completed" logs have category "Host.Executor".</span><span class="sxs-lookup"><span data-stu-id="4e8cf-220">For example, the "function started," "function executed," and "function completed" logs have category "Host.Executor".</span></span> 

<span data-ttu-id="4e8cf-221">If you write logs in your function code, their category is "Function".</span><span class="sxs-lookup"><span data-stu-id="4e8cf-221">If you write logs in your function code, their category is "Function".</span></span>

### <a name="log-levels"></a><span data-ttu-id="4e8cf-222">Log levels</span><span class="sxs-lookup"><span data-stu-id="4e8cf-222">Log levels</span></span>

<span data-ttu-id="4e8cf-223">The Azure functions logger also includes a *log level* with every log.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-223">The Azure functions logger also includes a *log level* with every log.</span></span> <span data-ttu-id="4e8cf-224">[LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel#Microsoft_Extensions_Logging_LogLevel) is an enumeration, and the integer code indicates relative importance:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-224">[LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel#Microsoft_Extensions_Logging_LogLevel) is an enumeration, and the integer code indicates relative importance:</span></span>

|<span data-ttu-id="4e8cf-225">LogLevel</span><span class="sxs-lookup"><span data-stu-id="4e8cf-225">LogLevel</span></span>    |<span data-ttu-id="4e8cf-226">Code</span><span class="sxs-lookup"><span data-stu-id="4e8cf-226">Code</span></span>|
|------------|---|
|<span data-ttu-id="4e8cf-227">Trace</span><span class="sxs-lookup"><span data-stu-id="4e8cf-227">Trace</span></span>       | <span data-ttu-id="4e8cf-228">0</span><span class="sxs-lookup"><span data-stu-id="4e8cf-228">0</span></span> |
|<span data-ttu-id="4e8cf-229">Debug</span><span class="sxs-lookup"><span data-stu-id="4e8cf-229">Debug</span></span>       | <span data-ttu-id="4e8cf-230">1</span><span class="sxs-lookup"><span data-stu-id="4e8cf-230">1</span></span> |
|<span data-ttu-id="4e8cf-231">Information</span><span class="sxs-lookup"><span data-stu-id="4e8cf-231">Information</span></span> | <span data-ttu-id="4e8cf-232">2</span><span class="sxs-lookup"><span data-stu-id="4e8cf-232">2</span></span> |
|<span data-ttu-id="4e8cf-233">Warning</span><span class="sxs-lookup"><span data-stu-id="4e8cf-233">Warning</span></span>     | <span data-ttu-id="4e8cf-234">3</span><span class="sxs-lookup"><span data-stu-id="4e8cf-234">3</span></span> |
|<span data-ttu-id="4e8cf-235">Error</span><span class="sxs-lookup"><span data-stu-id="4e8cf-235">Error</span></span>       | <span data-ttu-id="4e8cf-236">4</span><span class="sxs-lookup"><span data-stu-id="4e8cf-236">4</span></span> |
|<span data-ttu-id="4e8cf-237">Critical</span><span class="sxs-lookup"><span data-stu-id="4e8cf-237">Critical</span></span>    | <span data-ttu-id="4e8cf-238">5</span><span class="sxs-lookup"><span data-stu-id="4e8cf-238">5</span></span> |
|<span data-ttu-id="4e8cf-239">None</span><span class="sxs-lookup"><span data-stu-id="4e8cf-239">None</span></span>        | <span data-ttu-id="4e8cf-240">6</span><span class="sxs-lookup"><span data-stu-id="4e8cf-240">6</span></span> |

<span data-ttu-id="4e8cf-241">Log level `None` is explained in the next section.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-241">Log level `None` is explained in the next section.</span></span> 

### <a name="configure-logging-in-hostjson"></a><span data-ttu-id="4e8cf-242">Configure logging in host.json</span><span class="sxs-lookup"><span data-stu-id="4e8cf-242">Configure logging in host.json</span></span>

<span data-ttu-id="4e8cf-243">The *host.json* file configures how much logging a function app sends to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-243">The *host.json* file configures how much logging a function app sends to Application Insights.</span></span> <span data-ttu-id="4e8cf-244">For each category, you indicate the minimum log level to send.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-244">For each category, you indicate the minimum log level to send.</span></span> <span data-ttu-id="4e8cf-245">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-245">Here's an example:</span></span>

```json
{
  "logger": {
    "categoryFilter": {
      "defaultLevel": "Information",
      "categoryLevels": {
        "Host.Results": "Error",
        "Function": "Error",
        "Host.Aggregator": "Trace"
      }
    }
  }
}
```

<span data-ttu-id="4e8cf-246">This example sets up the following rules:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-246">This example sets up the following rules:</span></span>

1. <span data-ttu-id="4e8cf-247">For logs with category "Host.Results" or "Function", send only `Error` level and above to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-247">For logs with category "Host.Results" or "Function", send only `Error` level and above to Application Insights.</span></span> <span data-ttu-id="4e8cf-248">Logs for `Warning` level and below are ignored.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-248">Logs for `Warning` level and below are ignored.</span></span>
2. <span data-ttu-id="4e8cf-249">For logs with category Host.Aggregator, send all logs to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-249">For logs with category Host.Aggregator, send all logs to Application Insights.</span></span> <span data-ttu-id="4e8cf-250">The `Trace` log level is the same as what some loggers call `Verbose`, but use `Trace` in the *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-250">The `Trace` log level is the same as what some loggers call `Verbose`, but use `Trace` in the *host.json* file.</span></span>
3. <span data-ttu-id="4e8cf-251">For all other logs, send only `Information` level and above to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-251">For all other logs, send only `Information` level and above to Application Insights.</span></span>

<span data-ttu-id="4e8cf-252">The category value in *host.json* controls logging for all categories that begin with the same value.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-252">The category value in *host.json* controls logging for all categories that begin with the same value.</span></span> <span data-ttu-id="4e8cf-253">For example, "Host" in *host.json* controls logging for "Host.General", "Host.Executor", "Host.Results", and so forth.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-253">For example, "Host" in *host.json* controls logging for "Host.General", "Host.Executor", "Host.Results", and so forth.</span></span>

<span data-ttu-id="4e8cf-254">If *host.json* includes multiple categories that start with the same string, the longer ones are matched first.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-254">If *host.json* includes multiple categories that start with the same string, the longer ones are matched first.</span></span> <span data-ttu-id="4e8cf-255">For example, suppose you want everything from the runtime except "Host.Aggregator" to log at `Error` level, while "Host.Aggregator" logs at `Information` level:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-255">For example, suppose you want everything from the runtime except "Host.Aggregator" to log at `Error` level, while "Host.Aggregator" logs at `Information` level:</span></span>

```json
{
  "logger": {
    "categoryFilter": {
      "defaultLevel": "Information",
      "categoryLevels": {
        "Host": "Error",
        "Function": "Error",
        "Host.Aggregator": "Information"
      }
    }
  }
}
```

<span data-ttu-id="4e8cf-256">To suppress all logs for a category, you can use log level `None`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-256">To suppress all logs for a category, you can use log level `None`.</span></span> <span data-ttu-id="4e8cf-257">No logs are written with that category and there is no log level above it.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-257">No logs are written with that category and there is no log level above it.</span></span>

<span data-ttu-id="4e8cf-258">The following sections describe the main categories of logs that the runtime creates.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-258">The following sections describe the main categories of logs that the runtime creates.</span></span> 

### <a name="category-hostresults"></a><span data-ttu-id="4e8cf-259">Category Host.Results</span><span class="sxs-lookup"><span data-stu-id="4e8cf-259">Category Host.Results</span></span>

<span data-ttu-id="4e8cf-260">These logs show as "requests" in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-260">These logs show as "requests" in Application Insights.</span></span> <span data-ttu-id="4e8cf-261">They indicate success or failure of a function.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-261">They indicate success or failure of a function.</span></span>

![Requests chart](media/functions-monitoring/requests-chart.png)

<span data-ttu-id="4e8cf-263">All of these logs are written at `Information` level, so if you filter at `Warning` or above, you won't see any of this data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-263">All of these logs are written at `Information` level, so if you filter at `Warning` or above, you won't see any of this data.</span></span>

### <a name="category-hostaggregator"></a><span data-ttu-id="4e8cf-264">Category Host.Aggregator</span><span class="sxs-lookup"><span data-stu-id="4e8cf-264">Category Host.Aggregator</span></span>

<span data-ttu-id="4e8cf-265">These logs provide counts and averages of function invocations over a [configurable](#configure-the-aggregator) period of time.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-265">These logs provide counts and averages of function invocations over a [configurable](#configure-the-aggregator) period of time.</span></span> <span data-ttu-id="4e8cf-266">The default period is 30 seconds or 1,000 results, whichever comes first.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-266">The default period is 30 seconds or 1,000 results, whichever comes first.</span></span> 

<span data-ttu-id="4e8cf-267">The logs are available in the **customMetrics** table in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-267">The logs are available in the **customMetrics** table in Application Insights.</span></span> <span data-ttu-id="4e8cf-268">Examples are number of runs, success rate, and duration.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-268">Examples are number of runs, success rate, and duration.</span></span>

![customMetrics query](media/functions-monitoring/custom-metrics-query.png)

<span data-ttu-id="4e8cf-270">All of these logs are written at `Information` level, so if you filter at `Warning` or above, you won't see any of this data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-270">All of these logs are written at `Information` level, so if you filter at `Warning` or above, you won't see any of this data.</span></span>

### <a name="other-categories"></a><span data-ttu-id="4e8cf-271">Other categories</span><span class="sxs-lookup"><span data-stu-id="4e8cf-271">Other categories</span></span>

<span data-ttu-id="4e8cf-272">All logs for categories other than the ones already listed are available in the **traces** table in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-272">All logs for categories other than the ones already listed are available in the **traces** table in Application Insights.</span></span>

![traces query](media/functions-monitoring/analytics-traces.png)

<span data-ttu-id="4e8cf-274">All logs with categories that begin with "Host" are written by the Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-274">All logs with categories that begin with "Host" are written by the Functions runtime.</span></span> <span data-ttu-id="4e8cf-275">The "Function started" and "Function completed" logs have category "Host.Executor".</span><span class="sxs-lookup"><span data-stu-id="4e8cf-275">The "Function started" and "Function completed" logs have category "Host.Executor".</span></span> <span data-ttu-id="4e8cf-276">For successful runs, these logs are `Information` level; exceptions are logged at `Error` level.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-276">For successful runs, these logs are `Information` level; exceptions are logged at `Error` level.</span></span> <span data-ttu-id="4e8cf-277">The runtime also creates `Warning` level logs, for example: queue messages sent to the poison queue.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-277">The runtime also creates `Warning` level logs, for example: queue messages sent to the poison queue.</span></span>

<span data-ttu-id="4e8cf-278">Logs written by your function code have category "Function" and may be any log level.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-278">Logs written by your function code have category "Function" and may be any log level.</span></span>

## <a name="configure-the-aggregator"></a><span data-ttu-id="4e8cf-279">Configure the aggregator</span><span class="sxs-lookup"><span data-stu-id="4e8cf-279">Configure the aggregator</span></span>

<span data-ttu-id="4e8cf-280">As noted in the previous section, the runtime aggregates data about function executions over a period of time.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-280">As noted in the previous section, the runtime aggregates data about function executions over a period of time.</span></span> <span data-ttu-id="4e8cf-281">The default period is 30 seconds or 1,000 runs, whichever comes first.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-281">The default period is 30 seconds or 1,000 runs, whichever comes first.</span></span> <span data-ttu-id="4e8cf-282">You can configure this setting in the *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-282">You can configure this setting in the *host.json* file.</span></span>  <span data-ttu-id="4e8cf-283">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-283">Here's an example:</span></span>

```json
{
    "aggregator": {
      "batchSize": 1000,
      "flushTimeout": "00:00:30"
    }
}
```

## <a name="configure-sampling"></a><span data-ttu-id="4e8cf-284">Configure sampling</span><span class="sxs-lookup"><span data-stu-id="4e8cf-284">Configure sampling</span></span>

<span data-ttu-id="4e8cf-285">Application Insights has a [sampling](../application-insights/app-insights-sampling.md) feature that can protect you from producing too much telemetry data at times of peak load.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-285">Application Insights has a [sampling](../application-insights/app-insights-sampling.md) feature that can protect you from producing too much telemetry data at times of peak load.</span></span> <span data-ttu-id="4e8cf-286">When the number of telemetry items exceeds a specified rate, Application Insights starts to randomly ignore some of the incoming items.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-286">When the number of telemetry items exceeds a specified rate, Application Insights starts to randomly ignore some of the incoming items.</span></span> <span data-ttu-id="4e8cf-287">The default setting for maximum number of items per second is 5.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-287">The default setting for maximum number of items per second is 5.</span></span> <span data-ttu-id="4e8cf-288">You can configure sampling in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-288">You can configure sampling in *host.json*.</span></span>  <span data-ttu-id="4e8cf-289">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-289">Here's an example:</span></span>

```json
{
  "applicationInsights": {
    "sampling": {
      "isEnabled": true,
      "maxTelemetryItemsPerSecond" : 5
    }
  }
}
```

## <a name="write-logs-in-c-functions"></a><span data-ttu-id="4e8cf-290">Write logs in C# functions</span><span class="sxs-lookup"><span data-stu-id="4e8cf-290">Write logs in C# functions</span></span>

<span data-ttu-id="4e8cf-291">You can write logs in your function code that appear as traces in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-291">You can write logs in your function code that appear as traces in Application Insights.</span></span>

### <a name="ilogger"></a><span data-ttu-id="4e8cf-292">ILogger</span><span class="sxs-lookup"><span data-stu-id="4e8cf-292">ILogger</span></span>

<span data-ttu-id="4e8cf-293">Use an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) parameter in your functions instead of a `TraceWriter` parameter.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-293">Use an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) parameter in your functions instead of a `TraceWriter` parameter.</span></span> <span data-ttu-id="4e8cf-294">Logs created by using `TraceWriter` do go to Application Insights, but `ILogger` lets you do [structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-294">Logs created by using `TraceWriter` do go to Application Insights, but `ILogger` lets you do [structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="4e8cf-295">With an `ILogger` object you call `Log<level>` [extension methods on ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions#Methods_) to create logs.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-295">With an `ILogger` object you call `Log<level>` [extension methods on ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions#Methods_) to create logs.</span></span> <span data-ttu-id="4e8cf-296">For example, the following code writes `Information` logs with category "Function".</span><span class="sxs-lookup"><span data-stu-id="4e8cf-296">For example, the following code writes `Information` logs with category "Function".</span></span>

```cs
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger logger)
{
    logger.LogInformation("Request for item with key={itemKey}.", id);
```

### <a name="structured-logging"></a><span data-ttu-id="4e8cf-297">Structured logging</span><span class="sxs-lookup"><span data-stu-id="4e8cf-297">Structured logging</span></span>

<span data-ttu-id="4e8cf-298">The order of placeholders, not their names, determines which parameters are used in the log message.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-298">The order of placeholders, not their names, determines which parameters are used in the log message.</span></span> <span data-ttu-id="4e8cf-299">For example, suppose you have the following code:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-299">For example, suppose you have the following code:</span></span>

```csharp
string partitionKey = "partitionKey";
string rowKey = "rowKey";
logger.LogInformation("partitionKey={partitionKey}, rowKey={rowKey}", partitionKey, rowKey);
```

<span data-ttu-id="4e8cf-300">If you keep the same message string and reverse the order of the parameters, the resulting message text would have the values in the wrong places.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-300">If you keep the same message string and reverse the order of the parameters, the resulting message text would have the values in the wrong places.</span></span>

<span data-ttu-id="4e8cf-301">Placeholders are handled this way so that you can do structured logging.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-301">Placeholders are handled this way so that you can do structured logging.</span></span> <span data-ttu-id="4e8cf-302">Application Insights stores the parameter name-value pairs in addition to the message string.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-302">Application Insights stores the parameter name-value pairs in addition to the message string.</span></span> <span data-ttu-id="4e8cf-303">The result is that the message arguments become fields that you can query on.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-303">The result is that the message arguments become fields that you can query on.</span></span>

<span data-ttu-id="4e8cf-304">For example, if your logger method call looks like the previous example, you could query the field `customDimensions.prop__rowKey`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-304">For example, if your logger method call looks like the previous example, you could query the field `customDimensions.prop__rowKey`.</span></span> <span data-ttu-id="4e8cf-305">The `prop__` prefix is added to ensure that there are no collisions between fields the runtime adds and fields your function code adds.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-305">The `prop__` prefix is added to ensure that there are no collisions between fields the runtime adds and fields your function code adds.</span></span>

<span data-ttu-id="4e8cf-306">You can also query on the original message string by referencing the field `customDimensions.prop__{OriginalFormat}`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-306">You can also query on the original message string by referencing the field `customDimensions.prop__{OriginalFormat}`.</span></span>  

<span data-ttu-id="4e8cf-307">Here's a sample JSON representation of `customDimensions` data:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-307">Here's a sample JSON representation of `customDimensions` data:</span></span>

```json
{
  customDimensions: {
    "prop__{OriginalFormat}":"C# Queue trigger function processed: {message}",
    "Category":"Function",
    "LogLevel":"Information",
    "prop__message":"c9519cbf-b1e6-4b9b-bf24-cb7d10b1bb89"
  }
}
```

### <a name="logging-custom-metrics"></a><span data-ttu-id="4e8cf-308">Logging custom metrics</span><span class="sxs-lookup"><span data-stu-id="4e8cf-308">Logging custom metrics</span></span>  

<span data-ttu-id="4e8cf-309">In C# script functions, you can use the `LogMetric` extension method on `ILogger` to create custom metrics in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-309">In C# script functions, you can use the `LogMetric` extension method on `ILogger` to create custom metrics in Application Insights.</span></span> <span data-ttu-id="4e8cf-310">Here's a sample method call:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-310">Here's a sample method call:</span></span>

```csharp
logger.LogMetric("TestMetric", 1234); 
```

<span data-ttu-id="4e8cf-311">This code is an alternative to calling `TrackMetric` using [the Application Insights API for .NET](#custom-telemetry-in-c-functions).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-311">This code is an alternative to calling `TrackMetric` using [the Application Insights API for .NET](#custom-telemetry-in-c-functions).</span></span>

## <a name="write-logs-in-javascript-functions"></a><span data-ttu-id="4e8cf-312">Write logs in JavaScript functions</span><span class="sxs-lookup"><span data-stu-id="4e8cf-312">Write logs in JavaScript functions</span></span>

<span data-ttu-id="4e8cf-313">In Node.js functions, use `context.log` to write logs.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-313">In Node.js functions, use `context.log` to write logs.</span></span> <span data-ttu-id="4e8cf-314">Structured logging is not enabled.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-314">Structured logging is not enabled.</span></span>

```
context.log('JavaScript HTTP trigger function processed a request.' + context.invocationId);
```

### <a name="logging-custom-metrics"></a><span data-ttu-id="4e8cf-315">Logging custom metrics</span><span class="sxs-lookup"><span data-stu-id="4e8cf-315">Logging custom metrics</span></span>  

<span data-ttu-id="4e8cf-316">In Node.js functions, you can use the `context.log.metric` method to create custom metrics in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-316">In Node.js functions, you can use the `context.log.metric` method to create custom metrics in Application Insights.</span></span> <span data-ttu-id="4e8cf-317">Here's a sample method call:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-317">Here's a sample method call:</span></span>

```javascript
context.log.metric("TestMetric", 1234); 
```

<span data-ttu-id="4e8cf-318">This code is an alternative to calling `trackMetric` using [the Node.js SDK for Application Insights](#custom-telemetry-in-javascript-functions).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-318">This code is an alternative to calling `trackMetric` using [the Node.js SDK for Application Insights](#custom-telemetry-in-javascript-functions).</span></span>

## <a name="custom-telemetry-in-c-functions"></a><span data-ttu-id="4e8cf-319">Custom telemetry in C# functions</span><span class="sxs-lookup"><span data-stu-id="4e8cf-319">Custom telemetry in C# functions</span></span>

<span data-ttu-id="4e8cf-320">You can use the [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) NuGet package to send custom telemetry data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-320">You can use the [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) NuGet package to send custom telemetry data to Application Insights.</span></span>

<span data-ttu-id="4e8cf-321">Here's an example of C# code that uses the [custom telemetry API](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-321">Here's an example of C# code that uses the [custom telemetry API](../application-insights/app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="4e8cf-322">The example is for a .NET class library, but the Application Insights code is the same for C# script.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-322">The example is for a .NET class library, but the Application Insights code is the same for C# script.</span></span>

```cs
using System;
using System.Net;
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;
using Microsoft.ApplicationInsights.Extensibility;
using Microsoft.Azure.WebJobs;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
using System.Linq;

namespace functionapp0915
{
    public static class HttpTrigger2
    {
        private static string key = TelemetryConfiguration.Active.InstrumentationKey = 
            System.Environment.GetEnvironmentVariable(
                "APPINSIGHTS_INSTRUMENTATIONKEY", EnvironmentVariableTarget.Process);

        private static TelemetryClient telemetryClient = 
            new TelemetryClient() { InstrumentationKey = key };

        [FunctionName("HttpTrigger2")]
        public static async Task<HttpResponseMessage> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
            HttpRequestMessage req, ExecutionContext context, ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");
            DateTime start = DateTime.UtcNow;

            // parse query parameter
            string name = req.GetQueryNameValuePairs()
                .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
                .Value;

            // Get request body
            dynamic data = await req.Content.ReadAsAsync<object>();

            // Set name to query string or body data
            name = name ?? data?.name;
         
            // Track an Event
            var evt = new EventTelemetry("Function called");
            UpdateTelemetryContext(evt.Context, context, name);
            telemetryClient.TrackEvent(evt);
            
            // Track a Metric
            var metric = new MetricTelemetry("Test Metric", DateTime.Now.Millisecond);
            UpdateTelemetryContext(metric.Context, context, name);
            telemetryClient.TrackMetric(metric);
            
            // Track a Dependency
            var dependency = new DependencyTelemetry
                {
                    Name = "GET api/planets/1/",
                    Target = "swapi.co",
                    Data = "https://swapi.co/api/planets/1/",
                    Timestamp = start,
                    Duration = DateTime.UtcNow - start,
                    Success = true
                };
            UpdateTelemetryContext(dependency.Context, context, name);
            telemetryClient.TrackDependency(dependency);
            
            return name == null
                ? req.CreateResponse(HttpStatusCode.BadRequest, 
                    "Please pass a name on the query string or in the request body")
                : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
        }
        
        // This correllates all telemetry with the current Function invocation
        private static void UpdateTelemetryContext(TelemetryContext context, ExecutionContext functionContext, string userName)
        {
            context.Operation.Id = functionContext.InvocationId.ToString();
            context.Operation.ParentId = functionContext.InvocationId.ToString();
            context.Operation.Name = functionContext.FunctionName;
            context.User.Id = userName;
        }
    }    
}
```

<span data-ttu-id="4e8cf-323">Don't call `TrackRequest` or `StartOperation<RequestTelemetry>`, because you'll see duplicate requests for a function invocation.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-323">Don't call `TrackRequest` or `StartOperation<RequestTelemetry>`, because you'll see duplicate requests for a function invocation.</span></span>  <span data-ttu-id="4e8cf-324">The Functions runtime automatically tracks requests.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-324">The Functions runtime automatically tracks requests.</span></span>

<span data-ttu-id="4e8cf-325">Don't set `telemetryClient.Context.Operation.Id`.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-325">Don't set `telemetryClient.Context.Operation.Id`.</span></span> <span data-ttu-id="4e8cf-326">This is a global setting and will cause incorrect correllation when many functions are running simultaneously.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-326">This is a global setting and will cause incorrect correllation when many functions are running simultaneously.</span></span> <span data-ttu-id="4e8cf-327">Instead, create a new telemetry instance (`DependencyTelemetry`, `EventTelemetry`) and modify its `Context` property.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-327">Instead, create a new telemetry instance (`DependencyTelemetry`, `EventTelemetry`) and modify its `Context` property.</span></span> <span data-ttu-id="4e8cf-328">Then pass in the telemetry instance to the corresponding `Track` method on `TelemetryClient` (`TrackDependency()`, `TrackEvent()`).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-328">Then pass in the telemetry instance to the corresponding `Track` method on `TelemetryClient` (`TrackDependency()`, `TrackEvent()`).</span></span> <span data-ttu-id="4e8cf-329">This ensures that the telemetry has the correct correllation details for the current function invocation.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-329">This ensures that the telemetry has the correct correllation details for the current function invocation.</span></span>

## <a name="custom-telemetry-in-javascript-functions"></a><span data-ttu-id="4e8cf-330">Custom telemetry in JavaScript functions</span><span class="sxs-lookup"><span data-stu-id="4e8cf-330">Custom telemetry in JavaScript functions</span></span>

<span data-ttu-id="4e8cf-331">The [Application Insights Node.js SDK](https://www.npmjs.com/package/applicationinsights) is currently in beta.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-331">The [Application Insights Node.js SDK](https://www.npmjs.com/package/applicationinsights) is currently in beta.</span></span> <span data-ttu-id="4e8cf-332">Here's some sample code that sends custom telemetry to Application Insights:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-332">Here's some sample code that sends custom telemetry to Application Insights:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup();
const client = appInsights.defaultClient;

module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    client.trackEvent({name: "my custom event", tagOverrides:{"ai.operation.id": context.invocationId}, properties: {customProperty2: "custom property value"}});
    client.trackException({exception: new Error("handled exceptions can be logged with this method"), tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackMetric({name: "custom metric", value: 3, tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackTrace({message: "trace message", tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackDependency({target:"http://dbname", name:"select customers proc", data:"SELECT * FROM Customers", duration:231, resultCode:0, success: true, dependencyTypeName: "ZSQL", tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackRequest({name:"GET /customers", url:"http://myserver/customers", duration:309, resultCode:200, success:true, tagOverrides:{"ai.operation.id": context.invocationId}});

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```

<span data-ttu-id="4e8cf-333">The `tagOverrides` parameter sets `operation_Id` to the function's invocation ID.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-333">The `tagOverrides` parameter sets `operation_Id` to the function's invocation ID.</span></span> <span data-ttu-id="4e8cf-334">This setting enables you to correlate all of the automatically-generated and custom telemetry for a given function invocation.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-334">This setting enables you to correlate all of the automatically-generated and custom telemetry for a given function invocation.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4e8cf-335">Known issues</span><span class="sxs-lookup"><span data-stu-id="4e8cf-335">Known issues</span></span>

### <a name="dependencies"></a><span data-ttu-id="4e8cf-336">Dependencies</span><span class="sxs-lookup"><span data-stu-id="4e8cf-336">Dependencies</span></span>

<span data-ttu-id="4e8cf-337">Dependencies that the function has to other services don't show up automatically, but you can write custom code to show the dependencies.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-337">Dependencies that the function has to other services don't show up automatically, but you can write custom code to show the dependencies.</span></span> <span data-ttu-id="4e8cf-338">The sample code in the [C# custom telemetry section](#custom-telemetry-in-c-functions) shows how.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-338">The sample code in the [C# custom telemetry section](#custom-telemetry-in-c-functions) shows how.</span></span> <span data-ttu-id="4e8cf-339">The sample code results in an *application map* in Application Insights that looks like this:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-339">The sample code results in an *application map* in Application Insights that looks like this:</span></span>

![Application map](media/functions-monitoring/app-map.png)

### <a name="report-issues"></a><span data-ttu-id="4e8cf-341">Report issues</span><span class="sxs-lookup"><span data-stu-id="4e8cf-341">Report issues</span></span>

<span data-ttu-id="4e8cf-342">To report an issue with Application Insights integration in Functions, or to make a suggestion or request, [create an issue in GitHub](https://github.com/Azure/Azure-Functions/issues/new).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-342">To report an issue with Application Insights integration in Functions, or to make a suggestion or request, [create an issue in GitHub](https://github.com/Azure/Azure-Functions/issues/new).</span></span>

## <a name="monitoring-without-application-insights"></a><span data-ttu-id="4e8cf-343">Monitoring without Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e8cf-343">Monitoring without Application Insights</span></span>

<span data-ttu-id="4e8cf-344">We recommend Application Insights for monitoring functions because it offers more data and better ways to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-344">We recommend Application Insights for monitoring functions because it offers more data and better ways to analyze the data.</span></span> <span data-ttu-id="4e8cf-345">But if you prefer the built-in logging system that uses Azure Storage, you can continue to use that.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-345">But if you prefer the built-in logging system that uses Azure Storage, you can continue to use that.</span></span>

### <a name="logging-to-storage"></a><span data-ttu-id="4e8cf-346">Logging to storage</span><span class="sxs-lookup"><span data-stu-id="4e8cf-346">Logging to storage</span></span>

<span data-ttu-id="4e8cf-347">Built-in logging uses the storage account specified by the connection string in the `AzureWebJobsDashboard` app setting.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-347">Built-in logging uses the storage account specified by the connection string in the `AzureWebJobsDashboard` app setting.</span></span> <span data-ttu-id="4e8cf-348">In a function app page, select a function and then select the **Monitor** tab, and choose to keep it in classic view.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-348">In a function app page, select a function and then select the **Monitor** tab, and choose to keep it in classic view.</span></span>

![Switch to classic view](media/functions-monitoring/switch-to-classic-view.png)

 <span data-ttu-id="4e8cf-350">You get a list of function executions.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-350">You get a list of function executions.</span></span> <span data-ttu-id="4e8cf-351">Select a function execution to review the duration, input data, errors, and associated log files.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-351">Select a function execution to review the duration, input data, errors, and associated log files.</span></span>

<span data-ttu-id="4e8cf-352">If you enabled Application Insights earlier, but now you want to go back to built-in logging, disable Application Insights manually, and then select the **Monitor** tab. To disable Application Insights integration, delete the APPINSIGHTS_INSTRUMENTATIONKEY app setting.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-352">If you enabled Application Insights earlier, but now you want to go back to built-in logging, disable Application Insights manually, and then select the **Monitor** tab. To disable Application Insights integration, delete the APPINSIGHTS_INSTRUMENTATIONKEY app setting.</span></span>

<span data-ttu-id="4e8cf-353">Even if the **Monitor** tab shows Application Insights data, you can see log data in the file system if you haven't [disabled built-in logging](#disable-built-in-logging).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-353">Even if the **Monitor** tab shows Application Insights data, you can see log data in the file system if you haven't [disabled built-in logging](#disable-built-in-logging).</span></span> <span data-ttu-id="4e8cf-354">In the Storage resource, go to Files, select the file service for the function, and then go to `LogFiles > Application > Functions > Function > your_function` to see the log file.</span><span class="sxs-lookup"><span data-stu-id="4e8cf-354">In the Storage resource, go to Files, select the file service for the function, and then go to `LogFiles > Application > Functions > Function > your_function` to see the log file.</span></span>

### <a name="real-time-monitoring"></a><span data-ttu-id="4e8cf-355">Real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="4e8cf-355">Real-time monitoring</span></span>

<span data-ttu-id="4e8cf-356">You can stream log files to a command-line session on a local workstation using the [Azure Command Line Interface (CLI) 2.0](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-356">You can stream log files to a command-line session on a local workstation using the [Azure Command Line Interface (CLI) 2.0](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>  

<span data-ttu-id="4e8cf-357">For Azure CLI 2.0, use the following commands to sign in, choose your subscription, and stream log files:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-357">For Azure CLI 2.0, use the following commands to sign in, choose your subscription, and stream log files:</span></span>

```
az login
az account list
az account set <subscriptionNameOrId>
az webapp log tail --resource-group <resource group name> --name <function app name>
```

<span data-ttu-id="4e8cf-358">For Azure PowerShell, use the following commands to add your Azure account, choose your subscription, and stream log files:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-358">For Azure PowerShell, use the following commands to add your Azure account, choose your subscription, and stream log files:</span></span>

```
PS C:\> Add-AzureAccount
PS C:\> Get-AzureSubscription
PS C:\> Get-AzureSubscription -SubscriptionName "<subscription name>" | Select-AzureSubscription
PS C:\> Get-AzureWebSiteLog -Name <function app name> -Tail
```

<span data-ttu-id="4e8cf-359">For more information, see [How to stream logs](../app-service/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="4e8cf-359">For more information, see [How to stream logs](../app-service/web-sites-enable-diagnostic-log.md#streamlogs).</span></span>

### <a name="viewing-log-files-locally"></a><span data-ttu-id="4e8cf-360">Viewing log files locally</span><span class="sxs-lookup"><span data-stu-id="4e8cf-360">Viewing log files locally</span></span>

[!INCLUDE [functions-local-logs-location](../../includes/functions-local-logs-location.md)]

## <a name="next-steps"></a><span data-ttu-id="4e8cf-361">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e8cf-361">Next steps</span></span>

<span data-ttu-id="4e8cf-362">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="4e8cf-362">For more information, see the following resources:</span></span>

* [<span data-ttu-id="4e8cf-363">Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e8cf-363">Application Insights</span></span>](/azure/application-insights/)
* [<span data-ttu-id="4e8cf-364">ASP.NET Core logging</span><span class="sxs-lookup"><span data-stu-id="4e8cf-364">ASP.NET Core logging</span></span>](/aspnet/core/fundamentals/logging/)
