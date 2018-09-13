---
title: Analytics - the powerful search tool of Azure Application Insights | Microsoft Docs
description: 'Overview of Analytics, the powerful diagnostic search tool of Application Insights. '
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 22e46ece63160b04ae21d7ace0d3266befa7e75e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661486"
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="e96a7-103">Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e96a7-103">Analytics in Application Insights</span></span>
<span data-ttu-id="e96a7-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e96a7-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e96a7-105">These pages describe the Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="e96a7-105">These pages describe the Analytics query language.</span></span> 

* <span data-ttu-id="e96a7-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="e96a7-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="e96a7-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span><span class="sxs-lookup"><span data-stu-id="e96a7-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="e96a7-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span><span class="sxs-lookup"><span data-stu-id="e96a7-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="e96a7-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="e96a7-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="e96a7-110">Queries in Analytics</span><span class="sxs-lookup"><span data-stu-id="e96a7-110">Queries in Analytics</span></span>
<span data-ttu-id="e96a7-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span><span class="sxs-lookup"><span data-stu-id="e96a7-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="e96a7-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span><span class="sxs-lookup"><span data-stu-id="e96a7-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="e96a7-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="e96a7-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL

    requests      // Table of events that log HTTP requests.
    | where timestamp > ago(7d) and client_City == "Hyderabad"
    | summarize clients = dcount(client_IP) 
      by tod_UTC=bin(timestamp % 1d, 1h), resultCode
    | extend local_hour = (tod_UTC + 5h + 30min) % 24h + datetime("2001-01-01") 
```

<span data-ttu-id="e96a7-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span><span class="sxs-lookup"><span data-stu-id="e96a7-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

<span data-ttu-id="e96a7-115">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span><span class="sxs-lookup"><span data-stu-id="e96a7-115">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Choose bar chart, x and y axes, then segmentation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics/020.png)

<span data-ttu-id="e96a7-117">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="e96a7-117">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="e96a7-118">(And we should investigate those 500 codes.)</span><span class="sxs-lookup"><span data-stu-id="e96a7-118">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="e96a7-119">There are also powerful statistical operations:</span><span class="sxs-lookup"><span data-stu-id="e96a7-119">There are also powerful statistical operations:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics/025.png)

<span data-ttu-id="e96a7-120">The language has many attractive features:</span><span class="sxs-lookup"><span data-stu-id="e96a7-120">The language has many attractive features:</span></span>


* <span data-ttu-id="e96a7-121">[Filter](app-insights-analytics-reference.md#where-operator) your raw app telemetry by any fields, including your custom properties and metrics.</span><span class="sxs-lookup"><span data-stu-id="e96a7-121">[Filter](app-insights-analytics-reference.md#where-operator) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="e96a7-122">[Join](app-insights-analytics-reference.md#join-operator) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span><span class="sxs-lookup"><span data-stu-id="e96a7-122">[Join](app-insights-analytics-reference.md#join-operator) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="e96a7-123">Powerful statistical [aggregations](app-insights-analytics-reference.md#aggregations).</span><span class="sxs-lookup"><span data-stu-id="e96a7-123">Powerful statistical [aggregations](app-insights-analytics-reference.md#aggregations).</span></span>
* <span data-ttu-id="e96a7-124">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span><span class="sxs-lookup"><span data-stu-id="e96a7-124">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="e96a7-125">Immediate and powerful visualizations.</span><span class="sxs-lookup"><span data-stu-id="e96a7-125">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="e96a7-126">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="e96a7-126">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="e96a7-127">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="e96a7-127">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="e96a7-128">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span><span class="sxs-lookup"><span data-stu-id="e96a7-128">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="e96a7-129">Connect to your Application Insights data</span><span class="sxs-lookup"><span data-stu-id="e96a7-129">Connect to your Application Insights data</span></span>
<span data-ttu-id="e96a7-130">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="e96a7-130">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Open portal.azure.com, open your Application Insights resource, and click Analytics.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="e96a7-132">Video</span><span class="sxs-lookup"><span data-stu-id="e96a7-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]


## <a name="next-steps"></a><span data-ttu-id="e96a7-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="e96a7-133">Next steps</span></span>
* <span data-ttu-id="e96a7-134">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="e96a7-134">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 

### <a name="query-examples"></a><span data-ttu-id="e96a7-135">Query examples</span><span class="sxs-lookup"><span data-stu-id="e96a7-135">Query examples</span></span>

* <span data-ttu-id="e96a7-136">Try these walkthroughs to illustrate the power of using Analytics:</span><span class="sxs-lookup"><span data-stu-id="e96a7-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>
 1. [<span data-ttu-id="e96a7-137">Automatic diagnostics of spikes and step jumps in requests durations</span><span class="sxs-lookup"><span data-stu-id="e96a7-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 2. [<span data-ttu-id="e96a7-138">Analyzing performance degradations with time series analysis</span><span class="sxs-lookup"><span data-stu-id="e96a7-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 3. [<span data-ttu-id="e96a7-139">Analyzing application failures with autocluster and diffpatterns</span><span class="sxs-lookup"><span data-stu-id="e96a7-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 4. [<span data-ttu-id="e96a7-140">Advanced shape detections with time series analysis</span><span class="sxs-lookup"><span data-stu-id="e96a7-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 5. [<span data-ttu-id="e96a7-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span><span class="sxs-lookup"><span data-stu-id="e96a7-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 6. <span data-ttu-id="e96a7-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="e96a7-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 7. <span data-ttu-id="e96a7-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="e96a7-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 8. <span data-ttu-id="e96a7-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="e96a7-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 9. <span data-ttu-id="e96a7-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="e96a7-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>





