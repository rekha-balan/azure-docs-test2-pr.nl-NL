---
title: Using Analytics - the powerful search tool of Azure Application Insights | Microsoft Docs
description: 'Using the Analytics, the powerful diagnostic search tool of Application Insights. '
services: application-insights
documentationcenter: ''
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 0932538bc2bd3431b0a8cd056611ce96c6bc2298
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551653"
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="a6f11-103">Using Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6f11-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="a6f11-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6f11-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a6f11-105">These pages describe the Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="a6f11-105">These pages describe the Analytics query language.</span></span>

* <span data-ttu-id="a6f11-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="a6f11-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span><span class="sxs-lookup"><span data-stu-id="a6f11-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="a6f11-108">Open Analytics</span><span class="sxs-lookup"><span data-stu-id="a6f11-108">Open Analytics</span></span>
<span data-ttu-id="a6f11-109">From your app's home resource in Application Insights, click Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6f11-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Open portal.azure.com, open your Application Insights resource, and click Analytics.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/001.png)

<span data-ttu-id="a6f11-111">The inline tutorial gives you some ideas about what you can do.</span><span class="sxs-lookup"><span data-stu-id="a6f11-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="a6f11-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="a6f11-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="a6f11-113">Query your telemetry</span><span class="sxs-lookup"><span data-stu-id="a6f11-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="a6f11-114">Write a query</span><span class="sxs-lookup"><span data-stu-id="a6f11-114">Write a query</span></span>
![Schema display](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/150.png)

<span data-ttu-id="a6f11-116">Begin with the names of any of the tables listed on the left (or the [range](app-insights-analytics-reference.md#range-operator) or [union](app-insights-analytics-reference.md#union-operator) operators).</span><span class="sxs-lookup"><span data-stu-id="a6f11-116">Begin with the names of any of the tables listed on the left (or the [range](app-insights-analytics-reference.md#range-operator) or [union](app-insights-analytics-reference.md#union-operator) operators).</span></span> <span data-ttu-id="a6f11-117">Use `|` to create a pipeline of [operators](app-insights-analytics-reference.md#queries-and-operators).</span><span class="sxs-lookup"><span data-stu-id="a6f11-117">Use `|` to create a pipeline of [operators](app-insights-analytics-reference.md#queries-and-operators).</span></span> 

<span data-ttu-id="a6f11-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span><span class="sxs-lookup"><span data-stu-id="a6f11-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="a6f11-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span><span class="sxs-lookup"><span data-stu-id="a6f11-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="a6f11-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a6f11-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="a6f11-121">Run a query</span><span class="sxs-lookup"><span data-stu-id="a6f11-121">Run a query</span></span>
![Running a query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="a6f11-123">You can use single line breaks in a query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="a6f11-124">Put the cursor inside or at the end of the query you want to run.</span><span class="sxs-lookup"><span data-stu-id="a6f11-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="a6f11-125">Check the time range of your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-125">Check the time range of your query.</span></span> <span data-ttu-id="a6f11-126">(You can change it, or override it by including your own [`where...timestamp...`](app-insights-analytics-tour.md#time-range) clause in your query.)</span><span class="sxs-lookup"><span data-stu-id="a6f11-126">(You can change it, or override it by including your own [`where...timestamp...`](app-insights-analytics-tour.md#time-range) clause in your query.)</span></span>
3. <span data-ttu-id="a6f11-127">Click Go to run the query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="a6f11-128">Don't put blank lines in your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="a6f11-129">You can keep several separated queries in one query tab by separating them with blank lines.</span><span class="sxs-lookup"><span data-stu-id="a6f11-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="a6f11-130">Only the query that has the cursor runs.</span><span class="sxs-lookup"><span data-stu-id="a6f11-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="a6f11-131">Save a query</span><span class="sxs-lookup"><span data-stu-id="a6f11-131">Save a query</span></span>
![Saving a query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="a6f11-133">Save the current query file.</span><span class="sxs-lookup"><span data-stu-id="a6f11-133">Save the current query file.</span></span>
2. <span data-ttu-id="a6f11-134">Open a saved query file.</span><span class="sxs-lookup"><span data-stu-id="a6f11-134">Open a saved query file.</span></span>
3. <span data-ttu-id="a6f11-135">Create a new query file.</span><span class="sxs-lookup"><span data-stu-id="a6f11-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="a6f11-136">See the details</span><span class="sxs-lookup"><span data-stu-id="a6f11-136">See the details</span></span>
<span data-ttu-id="a6f11-137">Expand any row in the results to see its complete list of properties.</span><span class="sxs-lookup"><span data-stu-id="a6f11-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="a6f11-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span><span class="sxs-lookup"><span data-stu-id="a6f11-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Expand a row](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="a6f11-140">Arrange the results</span><span class="sxs-lookup"><span data-stu-id="a6f11-140">Arrange the results</span></span>
<span data-ttu-id="a6f11-141">You can sort, filter, paginate, and group the results returned from your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f11-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="a6f11-143">They only rearrange the results that were returned by your last query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="a6f11-144">To perform these tasks in the server before the results are returned, write your query with the [sort](app-insights-analytics-reference.md#sort-operator), [summarize](app-insights-analytics-reference.md#summarize-operator) and [where](app-insights-analytics-reference.md#where-operator) operators.</span><span class="sxs-lookup"><span data-stu-id="a6f11-144">To perform these tasks in the server before the results are returned, write your query with the [sort](app-insights-analytics-reference.md#sort-operator), [summarize](app-insights-analytics-reference.md#summarize-operator) and [where](app-insights-analytics-reference.md#where-operator) operators.</span></span>
> 
> 

<span data-ttu-id="a6f11-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span><span class="sxs-lookup"><span data-stu-id="a6f11-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Arrange columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="a6f11-147">Sort and filter items</span><span class="sxs-lookup"><span data-stu-id="a6f11-147">Sort and filter items</span></span>
<span data-ttu-id="a6f11-148">Sort your results by clicking the head of a column.</span><span class="sxs-lookup"><span data-stu-id="a6f11-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="a6f11-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="a6f11-150">Use the filter icon to narrow your search.</span><span class="sxs-lookup"><span data-stu-id="a6f11-150">Use the filter icon to narrow your search.</span></span>

![Sort and filter columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="a6f11-152">Group items</span><span class="sxs-lookup"><span data-stu-id="a6f11-152">Group items</span></span>
<span data-ttu-id="a6f11-153">To sort by more than one column, use grouping.</span><span class="sxs-lookup"><span data-stu-id="a6f11-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="a6f11-154">First enable it, and then drag column headers into the space above the table.</span><span class="sxs-lookup"><span data-stu-id="a6f11-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="a6f11-156">Missing some results?</span><span class="sxs-lookup"><span data-stu-id="a6f11-156">Missing some results?</span></span>

<span data-ttu-id="a6f11-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span><span class="sxs-lookup"><span data-stu-id="a6f11-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="a6f11-158">**Time range filter**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-158">**Time range filter**.</span></span> <span data-ttu-id="a6f11-159">By default, you will only see results from the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="a6f11-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="a6f11-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span><span class="sxs-lookup"><span data-stu-id="a6f11-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="a6f11-161">However, you can change the time range filter by using the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="a6f11-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="a6f11-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](app-insights-analytics-reference.md#where-operator) into your query.</span><span class="sxs-lookup"><span data-stu-id="a6f11-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](app-insights-analytics-reference.md#where-operator) into your query.</span></span> <span data-ttu-id="a6f11-163">For example:</span><span class="sxs-lookup"><span data-stu-id="a6f11-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="a6f11-164">**Results limit**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-164">**Results limit**.</span></span> <span data-ttu-id="a6f11-165">There's a limit of about 10k rows on the results returned from the portal.</span><span class="sxs-lookup"><span data-stu-id="a6f11-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="a6f11-166">A warning shows if you go over the limit.</span><span class="sxs-lookup"><span data-stu-id="a6f11-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="a6f11-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span><span class="sxs-lookup"><span data-stu-id="a6f11-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="a6f11-168">It's good practice to avoid hitting the limit.</span><span class="sxs-lookup"><span data-stu-id="a6f11-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="a6f11-169">Use the time range filter, or use operators such as:</span><span class="sxs-lookup"><span data-stu-id="a6f11-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="a6f11-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="a6f11-170">top 100 by timestamp</span></span>](app-insights-analytics-reference.md#top-operator) 
  * [<span data-ttu-id="a6f11-171">take 100</span><span class="sxs-lookup"><span data-stu-id="a6f11-171">take 100</span></span>](app-insights-analytics-reference.md#take-operator)
  * [<span data-ttu-id="a6f11-172">summarize </span><span class="sxs-lookup"><span data-stu-id="a6f11-172">summarize </span></span>](app-insights-analytics-reference.md#summarize-operator) 
  * [<span data-ttu-id="a6f11-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="a6f11-173">where timestamp > ago(3d)</span></span>](app-insights-analytics-reference.md#where-operator)

<span data-ttu-id="a6f11-174">(Want more than 10k rows?</span><span class="sxs-lookup"><span data-stu-id="a6f11-174">(Want more than 10k rows?</span></span> <span data-ttu-id="a6f11-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span><span class="sxs-lookup"><span data-stu-id="a6f11-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="a6f11-176">Analytics is designed for analysis, rather than retrieving raw data.)</span><span class="sxs-lookup"><span data-stu-id="a6f11-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="a6f11-177">Diagrams</span><span class="sxs-lookup"><span data-stu-id="a6f11-177">Diagrams</span></span>
<span data-ttu-id="a6f11-178">Select the type of diagram you'd like:</span><span class="sxs-lookup"><span data-stu-id="a6f11-178">Select the type of diagram you'd like:</span></span>

![Select a diagram type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/230.png)

<span data-ttu-id="a6f11-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span><span class="sxs-lookup"><span data-stu-id="a6f11-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="a6f11-181">By default, results are initially displayed as a table, and you select the diagram manually.</span><span class="sxs-lookup"><span data-stu-id="a6f11-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="a6f11-182">But you can use the [render directive](app-insights-analytics-reference.md#render-directive) at the end of a query to select a diagram.</span><span class="sxs-lookup"><span data-stu-id="a6f11-182">But you can use the [render directive](app-insights-analytics-reference.md#render-directive) at the end of a query to select a diagram.</span></span>

## <a name="pin-to-dashboard"></a><span data-ttu-id="a6f11-183">Pin to dashboard</span><span class="sxs-lookup"><span data-stu-id="a6f11-183">Pin to dashboard</span></span>
<span data-ttu-id="a6f11-184">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span><span class="sxs-lookup"><span data-stu-id="a6f11-184">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="a6f11-185">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span><span class="sxs-lookup"><span data-stu-id="a6f11-185">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Click the pin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="a6f11-187">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span><span class="sxs-lookup"><span data-stu-id="a6f11-187">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="a6f11-188">You can pin a table to the dashboard, if it has four or fewer columns.</span><span class="sxs-lookup"><span data-stu-id="a6f11-188">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="a6f11-189">Only the top seven rows are displayed.</span><span class="sxs-lookup"><span data-stu-id="a6f11-189">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="a6f11-190">Dashboard refresh</span><span class="sxs-lookup"><span data-stu-id="a6f11-190">Dashboard refresh</span></span>
<span data-ttu-id="a6f11-191">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span><span class="sxs-lookup"><span data-stu-id="a6f11-191">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="a6f11-192">You can also click the Refresh button.</span><span class="sxs-lookup"><span data-stu-id="a6f11-192">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="a6f11-193">Automatic simplifications</span><span class="sxs-lookup"><span data-stu-id="a6f11-193">Automatic simplifications</span></span>

<span data-ttu-id="a6f11-194">Certain simplifications are applied to a chart when you pin it to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="a6f11-194">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="a6f11-195">**Time restriction:** Queries are automatically limited to the past 14 days.</span><span class="sxs-lookup"><span data-stu-id="a6f11-195">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="a6f11-196">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="a6f11-196">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="a6f11-197">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span><span class="sxs-lookup"><span data-stu-id="a6f11-197">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="a6f11-198">For example, this query:</span><span class="sxs-lookup"><span data-stu-id="a6f11-198">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="a6f11-199">looks like this in Analytics:</span><span class="sxs-lookup"><span data-stu-id="a6f11-199">looks like this in Analytics:</span></span>

![Chart with long tail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="a6f11-201">but when you pin it to a dashboard, it looks like this:</span><span class="sxs-lookup"><span data-stu-id="a6f11-201">but when you pin it to a dashboard, it looks like this:</span></span>

![Chart with limited bins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="a6f11-203">Export to Excel</span><span class="sxs-lookup"><span data-stu-id="a6f11-203">Export to Excel</span></span>
<span data-ttu-id="a6f11-204">After you've run a query, you can download a .csv file.</span><span class="sxs-lookup"><span data-stu-id="a6f11-204">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="a6f11-205">Click **Export,  Excel**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-205">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="a6f11-206">Export to Power BI</span><span class="sxs-lookup"><span data-stu-id="a6f11-206">Export to Power BI</span></span>
<span data-ttu-id="a6f11-207">Put the cursor in a query and choose **Export, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-207">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Export from Analytics to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-using/240.png)

<span data-ttu-id="a6f11-209">You run the query in Power BI.</span><span class="sxs-lookup"><span data-stu-id="a6f11-209">You run the query in Power BI.</span></span> <span data-ttu-id="a6f11-210">You can set it to refresh on a schedule.</span><span class="sxs-lookup"><span data-stu-id="a6f11-210">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="a6f11-211">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span><span class="sxs-lookup"><span data-stu-id="a6f11-211">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="a6f11-212">Learn more about export to Power BI</span><span class="sxs-lookup"><span data-stu-id="a6f11-212">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="a6f11-213">Deep link</span><span class="sxs-lookup"><span data-stu-id="a6f11-213">Deep link</span></span>

<span data-ttu-id="a6f11-214">Get a link under **Export, Share link** that you can send to another user.</span><span class="sxs-lookup"><span data-stu-id="a6f11-214">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="a6f11-215">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span><span class="sxs-lookup"><span data-stu-id="a6f11-215">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="a6f11-216">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span><span class="sxs-lookup"><span data-stu-id="a6f11-216">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="a6f11-217">You could write code to generate deep links that you provide to users.</span><span class="sxs-lookup"><span data-stu-id="a6f11-217">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="a6f11-218">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="a6f11-218">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="a6f11-219">Automation</span><span class="sxs-lookup"><span data-stu-id="a6f11-219">Automation</span></span>

<span data-ttu-id="a6f11-220">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="a6f11-220">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="a6f11-221">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span><span class="sxs-lookup"><span data-stu-id="a6f11-221">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="a6f11-222">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span><span class="sxs-lookup"><span data-stu-id="a6f11-222">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="a6f11-223">Remember to add your own where-clause, to avoid getting huge responses.</span><span class="sxs-lookup"><span data-stu-id="a6f11-223">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="a6f11-224">Import data</span><span class="sxs-lookup"><span data-stu-id="a6f11-224">Import data</span></span>

<span data-ttu-id="a6f11-225">You can import data from a CSV file.</span><span class="sxs-lookup"><span data-stu-id="a6f11-225">You can import data from a CSV file.</span></span> <span data-ttu-id="a6f11-226">A typical usage is to import static data that you can join with tables from your telemetry.</span><span class="sxs-lookup"><span data-stu-id="a6f11-226">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="a6f11-227">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span><span class="sxs-lookup"><span data-stu-id="a6f11-227">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="a6f11-228">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span><span class="sxs-lookup"><span data-stu-id="a6f11-228">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="a6f11-229">Define your data schema</span><span class="sxs-lookup"><span data-stu-id="a6f11-229">Define your data schema</span></span>

1. <span data-ttu-id="a6f11-230">Click **Settings** (at top left) and then **Data Sources**.</span><span class="sxs-lookup"><span data-stu-id="a6f11-230">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="a6f11-231">Add a data source, following the instructions.</span><span class="sxs-lookup"><span data-stu-id="a6f11-231">Add a data source, following the instructions.</span></span> <span data-ttu-id="a6f11-232">You are asked to supply a sample of the data, which should include at least ten rows.</span><span class="sxs-lookup"><span data-stu-id="a6f11-232">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="a6f11-233">You then correct the schema.</span><span class="sxs-lookup"><span data-stu-id="a6f11-233">You then correct the schema.</span></span>

<span data-ttu-id="a6f11-234">This defines a data source, which you can then use to import individual tables.</span><span class="sxs-lookup"><span data-stu-id="a6f11-234">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="a6f11-235">Import a table</span><span class="sxs-lookup"><span data-stu-id="a6f11-235">Import a table</span></span>

1. <span data-ttu-id="a6f11-236">Open your data source definition from the list.</span><span class="sxs-lookup"><span data-stu-id="a6f11-236">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="a6f11-237">Click "Upload" and follow the instructions to upload the table.</span><span class="sxs-lookup"><span data-stu-id="a6f11-237">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="a6f11-238">This involves a call to a REST API, and so it is easy to automate.</span><span class="sxs-lookup"><span data-stu-id="a6f11-238">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="a6f11-239">Your table is now available for use in Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="a6f11-239">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="a6f11-240">It will appear in Analytics</span><span class="sxs-lookup"><span data-stu-id="a6f11-240">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="a6f11-241">Use the table</span><span class="sxs-lookup"><span data-stu-id="a6f11-241">Use the table</span></span>

<span data-ttu-id="a6f11-242">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="a6f11-242">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="a6f11-243">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span><span class="sxs-lookup"><span data-stu-id="a6f11-243">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="a6f11-244">The resulting table of requests has an additional column, `realName`.</span><span class="sxs-lookup"><span data-stu-id="a6f11-244">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="a6f11-245">Import from LogStash</span><span class="sxs-lookup"><span data-stu-id="a6f11-245">Import from LogStash</span></span>

<span data-ttu-id="a6f11-246">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span><span class="sxs-lookup"><span data-stu-id="a6f11-246">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="a6f11-247">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="a6f11-247">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="a6f11-248">Video</span><span class="sxs-lookup"><span data-stu-id="a6f11-248">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]














