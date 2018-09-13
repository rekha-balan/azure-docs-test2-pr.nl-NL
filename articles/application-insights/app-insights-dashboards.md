---
title: Dashboards and navigation in the Azure Application Insights | Microsoft Docs
description: Create views of your key APM charts and queries.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 13635761548e27bfe2a8d84c6e1528896253b5ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564100"
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="c93b6-103">Navigation and Dashboards in the Application Insights portal</span><span class="sxs-lookup"><span data-stu-id="c93b6-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="c93b6-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c93b6-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="c93b6-105">Find your telemetry</span><span class="sxs-lookup"><span data-stu-id="c93b6-105">Find your telemetry</span></span>
<span data-ttu-id="c93b6-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span><span class="sxs-lookup"><span data-stu-id="c93b6-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Click Browse, select Application Insights, then your app.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/00-start.png)

<span data-ttu-id="c93b6-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span><span class="sxs-lookup"><span data-stu-id="c93b6-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Major routes to view your telemetry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="c93b6-110">You can customize any of the charts and grids and pin them to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="c93b6-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="c93b6-112">Dashboards</span><span class="sxs-lookup"><span data-stu-id="c93b6-112">Dashboards</span></span>
<span data-ttu-id="c93b6-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="c93b6-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![A customized dashboard.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/31.png)

1. <span data-ttu-id="c93b6-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span><span class="sxs-lookup"><span data-stu-id="c93b6-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="c93b6-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span><span class="sxs-lookup"><span data-stu-id="c93b6-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="c93b6-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span><span class="sxs-lookup"><span data-stu-id="c93b6-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="c93b6-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span><span class="sxs-lookup"><span data-stu-id="c93b6-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="c93b6-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span><span class="sxs-lookup"><span data-stu-id="c93b6-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="c93b6-121">Add to a dashboard</span><span class="sxs-lookup"><span data-stu-id="c93b6-121">Add to a dashboard</span></span>
<span data-ttu-id="c93b6-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="c93b6-123">You'll see it next time you return there.</span><span class="sxs-lookup"><span data-stu-id="c93b6-123">You'll see it next time you return there.</span></span>

![To pin a chart, hover over it and then click "..." in the header.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/33.png)

1. <span data-ttu-id="c93b6-125">Pin chart to dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-125">Pin chart to dashboard.</span></span> <span data-ttu-id="c93b6-126">A copy of the chart appears on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="c93b6-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span><span class="sxs-lookup"><span data-stu-id="c93b6-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="c93b6-128">Click the top left corner to return to the current dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="c93b6-129">Then you can use the drop-down menu to return to the current view.</span><span class="sxs-lookup"><span data-stu-id="c93b6-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="c93b6-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span><span class="sxs-lookup"><span data-stu-id="c93b6-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="c93b6-131">You pin the whole tile to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="c93b6-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span><span class="sxs-lookup"><span data-stu-id="c93b6-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="c93b6-133">Time range up to 1 hour: Refresh every 5 minutes</span><span class="sxs-lookup"><span data-stu-id="c93b6-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="c93b6-134">Time range 1 - 24 hours: Refresh every 15 minutes</span><span class="sxs-lookup"><span data-stu-id="c93b6-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="c93b6-135">Time range above 24 hours: (Time range)/60.</span><span class="sxs-lookup"><span data-stu-id="c93b6-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="c93b6-136">Pin any query in Analytics</span><span class="sxs-lookup"><span data-stu-id="c93b6-136">Pin any query in Analytics</span></span>
<span data-ttu-id="c93b6-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="c93b6-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span><span class="sxs-lookup"><span data-stu-id="c93b6-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> <span data-ttu-id="c93b6-139">(There is a charge for this feature.)</span><span class="sxs-lookup"><span data-stu-id="c93b6-139">(There is a charge for this feature.)</span></span>

<span data-ttu-id="c93b6-140">Results are automatically recalculated every hour.</span><span class="sxs-lookup"><span data-stu-id="c93b6-140">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="c93b6-141">Click the Refresh icon on the chart to recalculate immediately.</span><span class="sxs-lookup"><span data-stu-id="c93b6-141">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="c93b6-142">(Browser refresh doesn't recalculate.)</span><span class="sxs-lookup"><span data-stu-id="c93b6-142">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="c93b6-143">Adjust a tile on the dashboard</span><span class="sxs-lookup"><span data-stu-id="c93b6-143">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="c93b6-144">Once a tile is on the dashboard, you can adjust it.</span><span class="sxs-lookup"><span data-stu-id="c93b6-144">Once a tile is on the dashboard, you can adjust it.</span></span>

![Hover over a chart in order to edit it.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/36.png)

1. <span data-ttu-id="c93b6-146">Add a chart to the tile.</span><span class="sxs-lookup"><span data-stu-id="c93b6-146">Add a chart to the tile.</span></span>
2. <span data-ttu-id="c93b6-147">Set the metric, group-by dimension and style (table, graph) of a chart.</span><span class="sxs-lookup"><span data-stu-id="c93b6-147">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="c93b6-148">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span><span class="sxs-lookup"><span data-stu-id="c93b6-148">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="c93b6-149">Set tile title.</span><span class="sxs-lookup"><span data-stu-id="c93b6-149">Set tile title.</span></span>

<span data-ttu-id="c93b6-150">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span><span class="sxs-lookup"><span data-stu-id="c93b6-150">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="c93b6-151">The original tile that you pinned isn't affected by your edits.</span><span class="sxs-lookup"><span data-stu-id="c93b6-151">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="c93b6-152">Switch between dashboards</span><span class="sxs-lookup"><span data-stu-id="c93b6-152">Switch between dashboards</span></span>
<span data-ttu-id="c93b6-153">You can save more than one dashboard and switch between them.</span><span class="sxs-lookup"><span data-stu-id="c93b6-153">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="c93b6-154">When you pin a chart or blade, they're added to the current dashboard.</span><span class="sxs-lookup"><span data-stu-id="c93b6-154">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![To switch between dashboards, click Dashboard and select a saved dashboard.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/32.png)

<span data-ttu-id="c93b6-158">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span><span class="sxs-lookup"><span data-stu-id="c93b6-158">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="c93b6-159">On the dashboard, a blade appears as a tile: click it to go to the blade.</span><span class="sxs-lookup"><span data-stu-id="c93b6-159">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="c93b6-160">A chart replicates the chart in its original location.</span><span class="sxs-lookup"><span data-stu-id="c93b6-160">A chart replicates the chart in its original location.</span></span>

![Click a tile to open the blade it represents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="c93b6-162">Share dashboards</span><span class="sxs-lookup"><span data-stu-id="c93b6-162">Share dashboards</span></span>
<span data-ttu-id="c93b6-163">When you've created a dashboard, you can share it with other users.</span><span class="sxs-lookup"><span data-stu-id="c93b6-163">When you've created a dashboard, you can share it with other users.</span></span>

![In the dashboard header, click Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/41.png)

<span data-ttu-id="c93b6-165">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-165">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="c93b6-166">App navigation</span><span class="sxs-lookup"><span data-stu-id="c93b6-166">App navigation</span></span>
<span data-ttu-id="c93b6-167">The overview blade is the gateway to more information about your app.</span><span class="sxs-lookup"><span data-stu-id="c93b6-167">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="c93b6-168">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span><span class="sxs-lookup"><span data-stu-id="c93b6-168">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="c93b6-169">Overview blade buttons</span><span class="sxs-lookup"><span data-stu-id="c93b6-169">Overview blade buttons</span></span>
![Overview blade top navigation bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="c93b6-171">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span><span class="sxs-lookup"><span data-stu-id="c93b6-171">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="c93b6-172">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span><span class="sxs-lookup"><span data-stu-id="c93b6-172">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="c93b6-173">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span><span class="sxs-lookup"><span data-stu-id="c93b6-173">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="c93b6-174">**Time range** - Adjust the range displayed by all the charts on the blade.</span><span class="sxs-lookup"><span data-stu-id="c93b6-174">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="c93b6-175">**Delete** - Delete the Application Insights resource for this app.</span><span class="sxs-lookup"><span data-stu-id="c93b6-175">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="c93b6-176">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="c93b6-176">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="c93b6-177">Essentials tab</span><span class="sxs-lookup"><span data-stu-id="c93b6-177">Essentials tab</span></span>
* <span data-ttu-id="c93b6-178">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span><span class="sxs-lookup"><span data-stu-id="c93b6-178">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="c93b6-179">Pricing - Make features available and set volume caps.</span><span class="sxs-lookup"><span data-stu-id="c93b6-179">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="c93b6-180">App navigation bar</span><span class="sxs-lookup"><span data-stu-id="c93b6-180">App navigation bar</span></span>
![Left navigation bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="c93b6-182">**Overview** - Return to the app overview blade.</span><span class="sxs-lookup"><span data-stu-id="c93b6-182">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="c93b6-183">**Activity log** - Alerts and Azure administrative events.</span><span class="sxs-lookup"><span data-stu-id="c93b6-183">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="c93b6-184">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span><span class="sxs-lookup"><span data-stu-id="c93b6-184">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="c93b6-185">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span><span class="sxs-lookup"><span data-stu-id="c93b6-185">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="c93b6-186">INVESTIGATE</span><span class="sxs-lookup"><span data-stu-id="c93b6-186">INVESTIGATE</span></span>

* <span data-ttu-id="c93b6-187">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span><span class="sxs-lookup"><span data-stu-id="c93b6-187">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="c93b6-188">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span><span class="sxs-lookup"><span data-stu-id="c93b6-188">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="c93b6-189">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span><span class="sxs-lookup"><span data-stu-id="c93b6-189">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="c93b6-190">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.\*</span><span class="sxs-lookup"><span data-stu-id="c93b6-190">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.\*</span></span>
* <span data-ttu-id="c93b6-191">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-191">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="c93b6-192">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span><span class="sxs-lookup"><span data-stu-id="c93b6-192">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="c93b6-193">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span><span class="sxs-lookup"><span data-stu-id="c93b6-193">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="c93b6-194">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-194">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="c93b6-195">**Browser** - Page view and AJAX performance.</span><span class="sxs-lookup"><span data-stu-id="c93b6-195">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="c93b6-196">Available if you [instrument your web pages](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-196">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="c93b6-197">**Usage** - Page view, user, and session counts.</span><span class="sxs-lookup"><span data-stu-id="c93b6-197">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="c93b6-198">Available if you [instrument your web pages](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-198">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="c93b6-199">CONFIGURE</span><span class="sxs-lookup"><span data-stu-id="c93b6-199">CONFIGURE</span></span>

* <span data-ttu-id="c93b6-200">**Getting started** - inline tutorial.</span><span class="sxs-lookup"><span data-stu-id="c93b6-200">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="c93b6-201">**Properties** - instrumentation key, subscription and resource id.</span><span class="sxs-lookup"><span data-stu-id="c93b6-201">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="c93b6-202">[Alerts](app-insights-alerts.md) - metric alert configuration.</span><span class="sxs-lookup"><span data-stu-id="c93b6-202">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="c93b6-203">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c93b6-203">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="c93b6-204">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span><span class="sxs-lookup"><span data-stu-id="c93b6-204">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="c93b6-205">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c93b6-205">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="c93b6-206">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span><span class="sxs-lookup"><span data-stu-id="c93b6-206">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="c93b6-207">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span><span class="sxs-lookup"><span data-stu-id="c93b6-207">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="c93b6-208">SETTINGS</span><span class="sxs-lookup"><span data-stu-id="c93b6-208">SETTINGS</span></span>

* <span data-ttu-id="c93b6-209">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span><span class="sxs-lookup"><span data-stu-id="c93b6-209">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="c93b6-210">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span><span class="sxs-lookup"><span data-stu-id="c93b6-210">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="c93b6-211">Video</span><span class="sxs-lookup"><span data-stu-id="c93b6-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="c93b6-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="c93b6-212">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="c93b6-213">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="c93b6-213">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="c93b6-214">Filter and segment metrics</span><span class="sxs-lookup"><span data-stu-id="c93b6-214">Filter and segment metrics</span></span> |![Search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="c93b6-216">Diagnostic search</span><span class="sxs-lookup"><span data-stu-id="c93b6-216">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="c93b6-217">Find and inspect events, related events, and create bugs</span><span class="sxs-lookup"><span data-stu-id="c93b6-217">Find and inspect events, related events, and create bugs</span></span> |![Search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="c93b6-219">Analytics</span><span class="sxs-lookup"><span data-stu-id="c93b6-219">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="c93b6-220">Powerful query language</span><span class="sxs-lookup"><span data-stu-id="c93b6-220">Powerful query language</span></span> |![Search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-dashboards/63.png) |













