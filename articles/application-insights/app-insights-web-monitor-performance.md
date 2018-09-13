---
title: Monitor your app's health and usage with Application Insights
description: Get started with Application Insights. Analyze usage, availability and performance of your on-premises or Microsoft Azure applications.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: awills
ms.openlocfilehash: 57db3c5b4142905a4a39cc63afa5030859302676
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669008"
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="4736b-104">Monitor performance in web applications</span><span class="sxs-lookup"><span data-stu-id="4736b-104">Monitor performance in web applications</span></span>


<span data-ttu-id="4736b-105">Make sure your application is performing well, and find out quickly about any failures.</span><span class="sxs-lookup"><span data-stu-id="4736b-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="4736b-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span><span class="sxs-lookup"><span data-stu-id="4736b-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="4736b-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span><span class="sxs-lookup"><span data-stu-id="4736b-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="4736b-108">They can be hosted on-premise, on virtual machines, or as Microsoft Azure websites.</span><span class="sxs-lookup"><span data-stu-id="4736b-108">They can be hosted on-premise, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="4736b-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span><span class="sxs-lookup"><span data-stu-id="4736b-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

## <a name="setup"></a><span data-ttu-id="4736b-110">Set up performance monitoring</span><span class="sxs-lookup"><span data-stu-id="4736b-110">Set up performance monitoring</span></span>
<span data-ttu-id="4736b-111">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span><span class="sxs-lookup"><span data-stu-id="4736b-111">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="4736b-112">ASP.NET web apps</span><span class="sxs-lookup"><span data-stu-id="4736b-112">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="4736b-113">Add exception monitoring</span><span class="sxs-lookup"><span data-stu-id="4736b-113">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="4736b-114">Add dependency monitoring</span><span class="sxs-lookup"><span data-stu-id="4736b-114">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="4736b-115">J2EE web apps</span><span class="sxs-lookup"><span data-stu-id="4736b-115">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="4736b-116">Add dependency monitoring</span><span class="sxs-lookup"><span data-stu-id="4736b-116">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <a name="view"></a><span data-ttu-id="4736b-117">Exploring performance metrics</span><span class="sxs-lookup"><span data-stu-id="4736b-117">Exploring performance metrics</span></span>
<span data-ttu-id="4736b-118">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span><span class="sxs-lookup"><span data-stu-id="4736b-118">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="4736b-119">The overview blade shows basic performance data:</span><span class="sxs-lookup"><span data-stu-id="4736b-119">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="4736b-120">Click any chart to see more detail, and to see results for a longer period.</span><span class="sxs-lookup"><span data-stu-id="4736b-120">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="4736b-121">For example, click the Requests tile and then select a time range:</span><span class="sxs-lookup"><span data-stu-id="4736b-121">For example, click the Requests tile and then select a time range:</span></span>

![Click through to more data and select a time range](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="4736b-123">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span><span class="sxs-lookup"><span data-stu-id="4736b-123">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Click a graph to choose metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="4736b-125">**Uncheck all the metrics** to see the full selection that is available.</span><span class="sxs-lookup"><span data-stu-id="4736b-125">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="4736b-126">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span><span class="sxs-lookup"><span data-stu-id="4736b-126">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="4736b-127">What does it all mean?</span><span class="sxs-lookup"><span data-stu-id="4736b-127">What does it all mean?</span></span> <span data-ttu-id="4736b-128">Performance tiles and reports</span><span class="sxs-lookup"><span data-stu-id="4736b-128">Performance tiles and reports</span></span>
<span data-ttu-id="4736b-129">There's a variety of performance metrics you can get.</span><span class="sxs-lookup"><span data-stu-id="4736b-129">There's a variety of performance metrics you can get.</span></span> <span data-ttu-id="4736b-130">Let's start with those that appear by default on the application blade.</span><span class="sxs-lookup"><span data-stu-id="4736b-130">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="4736b-131">Requests</span><span class="sxs-lookup"><span data-stu-id="4736b-131">Requests</span></span>
<span data-ttu-id="4736b-132">The number of HTTP requests received in a specified period.</span><span class="sxs-lookup"><span data-stu-id="4736b-132">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="4736b-133">Compare this with the results on other reports to see how your app behaves as the load varies.</span><span class="sxs-lookup"><span data-stu-id="4736b-133">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="4736b-134">HTTP requests include all GET or POST requests for pages, data and images.</span><span class="sxs-lookup"><span data-stu-id="4736b-134">HTTP requests include all GET or POST requests for pages, data and images.</span></span>

<span data-ttu-id="4736b-135">Click on the tile to get counts for specific URLs.</span><span class="sxs-lookup"><span data-stu-id="4736b-135">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="4736b-136">Average response time</span><span class="sxs-lookup"><span data-stu-id="4736b-136">Average response time</span></span>
<span data-ttu-id="4736b-137">Measures the time between a web request entering your application and the response being returned.</span><span class="sxs-lookup"><span data-stu-id="4736b-137">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="4736b-138">The points show a moving average.</span><span class="sxs-lookup"><span data-stu-id="4736b-138">The points show a moving average.</span></span> <span data-ttu-id="4736b-139">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span><span class="sxs-lookup"><span data-stu-id="4736b-139">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="4736b-140">Look for unusual peaks.</span><span class="sxs-lookup"><span data-stu-id="4736b-140">Look for unusual peaks.</span></span> <span data-ttu-id="4736b-141">In general, expect response time to rise with a rise in requests.</span><span class="sxs-lookup"><span data-stu-id="4736b-141">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="4736b-142">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span><span class="sxs-lookup"><span data-stu-id="4736b-142">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="4736b-143">Click on the tile to get times for specific URLs.</span><span class="sxs-lookup"><span data-stu-id="4736b-143">Click on the tile to get times for specific URLs.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="4736b-144">Slowest requests</span><span class="sxs-lookup"><span data-stu-id="4736b-144">Slowest requests</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="4736b-145">Shows which requests might need performance tuning.</span><span class="sxs-lookup"><span data-stu-id="4736b-145">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="4736b-146">Failed requests</span><span class="sxs-lookup"><span data-stu-id="4736b-146">Failed requests</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="4736b-147">A count of requests that threw uncaught exceptions.</span><span class="sxs-lookup"><span data-stu-id="4736b-147">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="4736b-148">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span><span class="sxs-lookup"><span data-stu-id="4736b-148">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="4736b-149">Only a representative sample of failures is retained for individual inspection.</span><span class="sxs-lookup"><span data-stu-id="4736b-149">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="4736b-150">Other metrics</span><span class="sxs-lookup"><span data-stu-id="4736b-150">Other metrics</span></span>
<span data-ttu-id="4736b-151">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span><span class="sxs-lookup"><span data-stu-id="4736b-151">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="4736b-152">Click (i) to see each metric's definition.</span><span class="sxs-lookup"><span data-stu-id="4736b-152">Click (i) to see each metric's definition.</span></span>

![Deselect all metrics to see the whole set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="4736b-154">Selecting any metric will disable the others that can't appear on the same chart.</span><span class="sxs-lookup"><span data-stu-id="4736b-154">Selecting any metric will disable the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="4736b-155">Set alerts</span><span class="sxs-lookup"><span data-stu-id="4736b-155">Set alerts</span></span>
<span data-ttu-id="4736b-156">To be notified by email of unusual values of any metric, add an alert.</span><span class="sxs-lookup"><span data-stu-id="4736b-156">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="4736b-157">You can choose either to send the email to the account administrators, or to specific email addresses.</span><span class="sxs-lookup"><span data-stu-id="4736b-157">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="4736b-158">Set the resource before the other properties.</span><span class="sxs-lookup"><span data-stu-id="4736b-158">Set the resource before the other properties.</span></span> <span data-ttu-id="4736b-159">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span><span class="sxs-lookup"><span data-stu-id="4736b-159">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="4736b-160">Be careful to note the units in which you're asked to enter the threshold value.</span><span class="sxs-lookup"><span data-stu-id="4736b-160">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="4736b-161">*I don't see the Add Alert button.*</span><span class="sxs-lookup"><span data-stu-id="4736b-161">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="4736b-162">- Is this a group account to which you have read-only access?</span><span class="sxs-lookup"><span data-stu-id="4736b-162">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="4736b-163">Check with the account administrator.</span><span class="sxs-lookup"><span data-stu-id="4736b-163">Check with the account administrator.</span></span>

## <a name="diagnosis"></a><span data-ttu-id="4736b-164">Diagnosing issues</span><span class="sxs-lookup"><span data-stu-id="4736b-164">Diagnosing issues</span></span>
<span data-ttu-id="4736b-165">Here are a few tips for finding and diagnosing performance issues:</span><span class="sxs-lookup"><span data-stu-id="4736b-165">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="4736b-166">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span><span class="sxs-lookup"><span data-stu-id="4736b-166">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="4736b-167">Compare the Request count with other metrics to see if failures or slow response are related to load.</span><span class="sxs-lookup"><span data-stu-id="4736b-167">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="4736b-168">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span><span class="sxs-lookup"><span data-stu-id="4736b-168">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>

## <a name="next"></a><span data-ttu-id="4736b-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="4736b-169">Next steps</span></span>
<span data-ttu-id="4736b-170">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span><span class="sxs-lookup"><span data-stu-id="4736b-170">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="4736b-171">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span><span class="sxs-lookup"><span data-stu-id="4736b-171">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="4736b-172">[Usage tracking][usage] - Find out how people use your application.</span><span class="sxs-lookup"><span data-stu-id="4736b-172">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="4736b-173">[Troubleshooting][qna] - and Q & A</span><span class="sxs-lookup"><span data-stu-id="4736b-173">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md









