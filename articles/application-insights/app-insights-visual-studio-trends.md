---
title: Analyzing Trends in Visual Studio | Microsoft Docs
description: Analyze, visualize, and explore trends in your Application Insights telemetry in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: douge
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: daviste
ms.openlocfilehash: 768bb2aa6d4aec34c0dacae72e2e3a273b1efbdc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564578"
---
# <a name="analyzing-trends-in-visual-studio"></a><span data-ttu-id="bfdb0-103">Analyzing Trends in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfdb0-103">Analyzing Trends in Visual Studio</span></span>
<span data-ttu-id="bfdb0-104">The Application Insights Trends tool visualizes how your web application's important telemetry events change over time, helping you quickly identify problems and anomalies.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-104">The Application Insights Trends tool visualizes how your web application's important telemetry events change over time, helping you quickly identify problems and anomalies.</span></span> <span data-ttu-id="bfdb0-105">By linking you to more detailed diagnostic information, Trends can help you improve your app's performance, track down the causes of exceptions, and uncover insights from your custom events.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-105">By linking you to more detailed diagnostic information, Trends can help you improve your app's performance, track down the causes of exceptions, and uncover insights from your custom events.</span></span>

![Example Trends window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a><span data-ttu-id="bfdb0-107">Configure your web app for Application Insights</span><span class="sxs-lookup"><span data-stu-id="bfdb0-107">Configure your web app for Application Insights</span></span>

<span data-ttu-id="bfdb0-108">If you haven't done this already, [configure your web app for Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfdb0-108">If you haven't done this already, [configure your web app for Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="bfdb0-109">This allows it to send telemetry to the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-109">This allows it to send telemetry to the Application Insights portal.</span></span> <span data-ttu-id="bfdb0-110">The Trends tool reads the telemetry from there.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-110">The Trends tool reads the telemetry from there.</span></span>

<span data-ttu-id="bfdb0-111">Application Insights Trends is available in Visual Studio 2015 Update 3 and later.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-111">Application Insights Trends is available in Visual Studio 2015 Update 3 and later.</span></span>

## <a name="open-application-insights-trends"></a><span data-ttu-id="bfdb0-112">Open Application Insights Trends</span><span class="sxs-lookup"><span data-stu-id="bfdb0-112">Open Application Insights Trends</span></span>
<span data-ttu-id="bfdb0-113">To open the Application Insights Trends window:</span><span class="sxs-lookup"><span data-stu-id="bfdb0-113">To open the Application Insights Trends window:</span></span>

* <span data-ttu-id="bfdb0-114">From the Application Insights toolbar button, choose **Explore Telemetry Trends**, or</span><span class="sxs-lookup"><span data-stu-id="bfdb0-114">From the Application Insights toolbar button, choose **Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="bfdb0-115">From the project context menu, choose **Application Insights > Explore Telemetry Trends**, or</span><span class="sxs-lookup"><span data-stu-id="bfdb0-115">From the project context menu, choose **Application Insights > Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="bfdb0-116">From the Visual Studio menu bar, choose **View > Other Windows > Application Insights Trends**.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-116">From the Visual Studio menu bar, choose **View > Other Windows > Application Insights Trends**.</span></span>

<span data-ttu-id="bfdb0-117">You may see a prompt to select a resource.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-117">You may see a prompt to select a resource.</span></span> <span data-ttu-id="bfdb0-118">Click **Select a resource**, sign in with an Azure subscription, then choose an Application Insights resource from the list for which you'd like to analyze telemetry trends.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-118">Click **Select a resource**, sign in with an Azure subscription, then choose an Application Insights resource from the list for which you'd like to analyze telemetry trends.</span></span>

## <a name="choose-a-trend-analysis"></a><span data-ttu-id="bfdb0-119">Choose a trend analysis</span><span class="sxs-lookup"><span data-stu-id="bfdb0-119">Choose a trend analysis</span></span>
![Menu of common types of trend analysis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

<span data-ttu-id="bfdb0-121">Get started by choosing from one of five common trend analyses, each analyzing data from the last 24 hours:</span><span class="sxs-lookup"><span data-stu-id="bfdb0-121">Get started by choosing from one of five common trend analyses, each analyzing data from the last 24 hours:</span></span>

* <span data-ttu-id="bfdb0-122">**Investigate performance issues with your server requests** - Requests made to your service, grouped by response times</span><span class="sxs-lookup"><span data-stu-id="bfdb0-122">**Investigate performance issues with your server requests** - Requests made to your service, grouped by response times</span></span>
* <span data-ttu-id="bfdb0-123">**Analyze errors in your server requests** - Requests made to your service, grouped by HTTP response code</span><span class="sxs-lookup"><span data-stu-id="bfdb0-123">**Analyze errors in your server requests** - Requests made to your service, grouped by HTTP response code</span></span>
* <span data-ttu-id="bfdb0-124">**Examine the exceptions in your application** - Exceptions from your service, grouped by exception type</span><span class="sxs-lookup"><span data-stu-id="bfdb0-124">**Examine the exceptions in your application** - Exceptions from your service, grouped by exception type</span></span>
* <span data-ttu-id="bfdb0-125">**Check the performance of your application's dependencies** - Services called by your service, grouped by response times</span><span class="sxs-lookup"><span data-stu-id="bfdb0-125">**Check the performance of your application's dependencies** - Services called by your service, grouped by response times</span></span>
* <span data-ttu-id="bfdb0-126">**Inspect your custom events** - Custom events you've set up for your service, grouped by event type.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-126">**Inspect your custom events** - Custom events you've set up for your service, grouped by event type.</span></span>

<span data-ttu-id="bfdb0-127">These pre-built analyses are available later from the **View common types of telemetry analysis** button in the upper-left corner of the Trends window.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-127">These pre-built analyses are available later from the **View common types of telemetry analysis** button in the upper-left corner of the Trends window.</span></span>

## <a name="visualize-trends-in-your-application"></a><span data-ttu-id="bfdb0-128">Visualize trends in your application</span><span class="sxs-lookup"><span data-stu-id="bfdb0-128">Visualize trends in your application</span></span>
<span data-ttu-id="bfdb0-129">Application Insights Trends creates a time series visualization from your app's telemetry.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-129">Application Insights Trends creates a time series visualization from your app's telemetry.</span></span> <span data-ttu-id="bfdb0-130">Each time series visualization displays one type of telemetry, grouped by one property of that telemetry, over some time range.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-130">Each time series visualization displays one type of telemetry, grouped by one property of that telemetry, over some time range.</span></span> <span data-ttu-id="bfdb0-131">For example, you might want to view server requests, grouped by the country from which they originated, over the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-131">For example, you might want to view server requests, grouped by the country from which they originated, over the last 24 hours.</span></span> <span data-ttu-id="bfdb0-132">In this example, each bubble on the visualization would represent a count of the server requests for some country/region during one hour.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-132">In this example, each bubble on the visualization would represent a count of the server requests for some country/region during one hour.</span></span>

<span data-ttu-id="bfdb0-133">Use the controls at the top of the window to adjust what types of telemetry you view.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-133">Use the controls at the top of the window to adjust what types of telemetry you view.</span></span> <span data-ttu-id="bfdb0-134">First, choose the telemetry types in which you're interested:</span><span class="sxs-lookup"><span data-stu-id="bfdb0-134">First, choose the telemetry types in which you're interested:</span></span>

* <span data-ttu-id="bfdb0-135">**Telemetry Type** - Server requests, exceptions, depdendencies, or custom events</span><span class="sxs-lookup"><span data-stu-id="bfdb0-135">**Telemetry Type** - Server requests, exceptions, depdendencies, or custom events</span></span>
* <span data-ttu-id="bfdb0-136">**Time Range** - Anywhere from the last 30 minutes to the last 3 days</span><span class="sxs-lookup"><span data-stu-id="bfdb0-136">**Time Range** - Anywhere from the last 30 minutes to the last 3 days</span></span>
* <span data-ttu-id="bfdb0-137">**Group By** - Exception type, problem ID, country/region, and more.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-137">**Group By** - Exception type, problem ID, country/region, and more.</span></span>

<span data-ttu-id="bfdb0-138">Then, click **Analyze Telemetry** to run the query.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-138">Then, click **Analyze Telemetry** to run the query.</span></span>

<span data-ttu-id="bfdb0-139">To navigate between bubbles in the visualization:</span><span class="sxs-lookup"><span data-stu-id="bfdb0-139">To navigate between bubbles in the visualization:</span></span>

* <span data-ttu-id="bfdb0-140">Click to select a bubble, which updates the filters at the bottom of the window, summarizing just the events that occurred during a specific time period</span><span class="sxs-lookup"><span data-stu-id="bfdb0-140">Click to select a bubble, which updates the filters at the bottom of the window, summarizing just the events that occurred during a specific time period</span></span>
* <span data-ttu-id="bfdb0-141">Double-click a bubble to navigate to the Search tool and see all of the individual telemetry events that occured during that time period</span><span class="sxs-lookup"><span data-stu-id="bfdb0-141">Double-click a bubble to navigate to the Search tool and see all of the individual telemetry events that occured during that time period</span></span>
* <span data-ttu-id="bfdb0-142">Ctrl-click a bubble to de-select it in the visualization.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-142">Ctrl-click a bubble to de-select it in the visualization.</span></span>

> [!TIP]
> <span data-ttu-id="bfdb0-143">The Trends and Search tools work together to help you pinpoint the causes of issues in your service among thousands of telemetry events.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-143">The Trends and Search tools work together to help you pinpoint the causes of issues in your service among thousands of telemetry events.</span></span> <span data-ttu-id="bfdb0-144">For example, if one afternoon your customers notice your app is being less responsive, start with Trends.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-144">For example, if one afternoon your customers notice your app is being less responsive, start with Trends.</span></span> <span data-ttu-id="bfdb0-145">Analyze requests made to your service over the past several hours, grouped by response time.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-145">Analyze requests made to your service over the past several hours, grouped by response time.</span></span> <span data-ttu-id="bfdb0-146">See if there's an unusually large cluster of slow requests.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-146">See if there's an unusually large cluster of slow requests.</span></span> <span data-ttu-id="bfdb0-147">Then double click that bubble to go to the Search tool, filtered to those request events.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-147">Then double click that bubble to go to the Search tool, filtered to those request events.</span></span> <span data-ttu-id="bfdb0-148">From Search, you can explore the contents of those requests and navigate to the code involved to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-148">From Search, you can explore the contents of those requests and navigate to the code involved to resolve the issue.</span></span>
> 
> 

## <a name="filter"></a><span data-ttu-id="bfdb0-149">Filter</span><span class="sxs-lookup"><span data-stu-id="bfdb0-149">Filter</span></span>
<span data-ttu-id="bfdb0-150">Discover more specific trends with the filter controls at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-150">Discover more specific trends with the filter controls at the bottom of the window.</span></span> <span data-ttu-id="bfdb0-151">To apply a filter, click on its name.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-151">To apply a filter, click on its name.</span></span> <span data-ttu-id="bfdb0-152">You can quickly switch between different filters to discover trends that may be hiding in a particular dimension of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-152">You can quickly switch between different filters to discover trends that may be hiding in a particular dimension of your telemetry.</span></span> <span data-ttu-id="bfdb0-153">If you apply a filter in one dimension, like Exception Type, filters in other dimensions remain clickable even though they appear grayed-out. To un-apply a filter, click it again.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-153">If you apply a filter in one dimension, like Exception Type, filters in other dimensions remain clickable even though they appear grayed-out. To un-apply a filter, click it again.</span></span> <span data-ttu-id="bfdb0-154">Ctrl-click to select multiple filters in the same dimension.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-154">Ctrl-click to select multiple filters in the same dimension.</span></span>

![Trend filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

<span data-ttu-id="bfdb0-156">What if you want to apply multiple filters?</span><span class="sxs-lookup"><span data-stu-id="bfdb0-156">What if you want to apply multiple filters?</span></span> 

1. <span data-ttu-id="bfdb0-157">Apply the first filter.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-157">Apply the first filter.</span></span> 
2. <span data-ttu-id="bfdb0-158">Click the **Apply selected filters and query again** button by the name of the dimension of your first filter.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-158">Click the **Apply selected filters and query again** button by the name of the dimension of your first filter.</span></span> <span data-ttu-id="bfdb0-159">This will re-query your telemetry for only events that match the first filter.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-159">This will re-query your telemetry for only events that match the first filter.</span></span> 
3. <span data-ttu-id="bfdb0-160">Apply a second filter.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-160">Apply a second filter.</span></span> 
4. <span data-ttu-id="bfdb0-161">Repeat the process to find trends in specific subsets of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-161">Repeat the process to find trends in specific subsets of your telemetry.</span></span> <span data-ttu-id="bfdb0-162">For example, server requests named "GET Home/Index" *and* that came from Germany *and* that received a 500 response code.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-162">For example, server requests named "GET Home/Index" *and* that came from Germany *and* that received a 500 response code.</span></span> 

<span data-ttu-id="bfdb0-163">To un-apply one of these filters, click the **Remove selected filters and query again** button for the dimension.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-163">To un-apply one of these filters, click the **Remove selected filters and query again** button for the dimension.</span></span>

![Multiple filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a><span data-ttu-id="bfdb0-165">Find anomalies</span><span class="sxs-lookup"><span data-stu-id="bfdb0-165">Find anomalies</span></span>
<span data-ttu-id="bfdb0-166">The Trends tool can highlight bubbles of events that are anomalous compared to other bubbles in the same time series.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-166">The Trends tool can highlight bubbles of events that are anomalous compared to other bubbles in the same time series.</span></span> <span data-ttu-id="bfdb0-167">In the View Type dropdown, choose **Counts in time bucket (highlight anomalies)** or **Percentages in time bucket (highlight anomalies)**.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-167">In the View Type dropdown, choose **Counts in time bucket (highlight anomalies)** or **Percentages in time bucket (highlight anomalies)**.</span></span> <span data-ttu-id="bfdb0-168">Red bubbles are anomalous.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-168">Red bubbles are anomalous.</span></span> <span data-ttu-id="bfdb0-169">Anomalies are defined as bubbles with counts/percentages exceeding 2.1 times the standard deviation of the counts/percentages that occured in the past two time periods (48 hours if you're viewing the last 24 hours, etc.).</span><span class="sxs-lookup"><span data-stu-id="bfdb0-169">Anomalies are defined as bubbles with counts/percentages exceeding 2.1 times the standard deviation of the counts/percentages that occured in the past two time periods (48 hours if you're viewing the last 24 hours, etc.).</span></span>

![Colored dots indicate anomalies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> <span data-ttu-id="bfdb0-171">Highlighting anomalies is especially helpful for finding outliers in time series of small bubbles that may otherwise look similarly sized.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-171">Highlighting anomalies is especially helpful for finding outliers in time series of small bubbles that may otherwise look similarly sized.</span></span>  
> 
> 

## <a name="next"></a><span data-ttu-id="bfdb0-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfdb0-172">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="bfdb0-173">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="bfdb0-173">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="bfdb0-174">Search telemetry, see data in CodeLens, and configure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-174">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="bfdb0-175">All within Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-175">All within Visual Studio.</span></span> |![Right-click the project and choose Application Insights, Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/34.png) |
| <span data-ttu-id="bfdb0-177">**[Add more data](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="bfdb0-177">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="bfdb0-178">Monitor usage, availability, dependencies, exceptions.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-178">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="bfdb0-179">Integrate traces from logging frameworks.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-179">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="bfdb0-180">Write custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-180">Write custom telemetry.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/64.png) |
| <span data-ttu-id="bfdb0-182">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="bfdb0-182">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="bfdb0-183">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span><span class="sxs-lookup"><span data-stu-id="bfdb0-183">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-trends/62.png) |









