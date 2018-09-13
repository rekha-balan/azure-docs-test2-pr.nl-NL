---
title: Dependency Tracking in Azure Application Insights | Microsoft Docs
description: Analyze usage, availability and performance of your on-premises or Microsoft Azure web application with Application Insights.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: ecc3286cfe71f4d9a7e32b931f8672e92fc81cd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554667"
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="8fc2d-103">Set up Application Insights: Dependency tracking</span><span class="sxs-lookup"><span data-stu-id="8fc2d-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="8fc2d-104">A *dependency* is an external component that is called by your app.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="8fc2d-105">It's typically a service called using HTTP, or a database, or a file system.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="8fc2d-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="8fc2d-107">You can investigate specific calls, and relate them to requests and exceptions.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![sample charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="8fc2d-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="8fc2d-110">Server</span><span class="sxs-lookup"><span data-stu-id="8fc2d-110">Server</span></span>
  * <span data-ttu-id="8fc2d-111">SQL databases</span><span class="sxs-lookup"><span data-stu-id="8fc2d-111">SQL databases</span></span>
  * <span data-ttu-id="8fc2d-112">ASP.NET web and WCF services that use HTTP-based bindings</span><span class="sxs-lookup"><span data-stu-id="8fc2d-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="8fc2d-113">Local or remote HTTP calls</span><span class="sxs-lookup"><span data-stu-id="8fc2d-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="8fc2d-114">Azure DocumentDb, table, blob storage, and queue</span><span class="sxs-lookup"><span data-stu-id="8fc2d-114">Azure DocumentDb, table, blob storage, and queue</span></span>
* <span data-ttu-id="8fc2d-115">Web pages</span><span class="sxs-lookup"><span data-stu-id="8fc2d-115">Web pages</span></span>
  * <span data-ttu-id="8fc2d-116">AJAX calls</span><span class="sxs-lookup"><span data-stu-id="8fc2d-116">AJAX calls</span></span>

<span data-ttu-id="8fc2d-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="8fc2d-118">Performance overhead is minimal.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="8fc2d-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="8fc2d-120">Set up dependency monitoring</span><span class="sxs-lookup"><span data-stu-id="8fc2d-120">Set up dependency monitoring</span></span>
<span data-ttu-id="8fc2d-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="8fc2d-122">To get complete data, install the appropriate agent for the host server.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="8fc2d-123">Platform</span><span class="sxs-lookup"><span data-stu-id="8fc2d-123">Platform</span></span> | <span data-ttu-id="8fc2d-124">Install</span><span class="sxs-lookup"><span data-stu-id="8fc2d-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="8fc2d-125">IIS Server</span><span class="sxs-lookup"><span data-stu-id="8fc2d-125">IIS Server</span></span> |<span data-ttu-id="8fc2d-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="8fc2d-127">Azure Web App</span><span class="sxs-lookup"><span data-stu-id="8fc2d-127">Azure Web App</span></span> |<span data-ttu-id="8fc2d-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="8fc2d-129">Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="8fc2d-129">Azure Cloud Service</span></span> |<span data-ttu-id="8fc2d-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="8fc2d-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="8fc2d-131">Where to find dependency data</span><span class="sxs-lookup"><span data-stu-id="8fc2d-131">Where to find dependency data</span></span>
* <span data-ttu-id="8fc2d-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="8fc2d-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="8fc2d-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="8fc2d-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="8fc2d-136">[Analytics](#analytics) can be used to query dependency data.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="8fc2d-137">Application Map</span><span class="sxs-lookup"><span data-stu-id="8fc2d-137">Application Map</span></span>
<span data-ttu-id="8fc2d-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="8fc2d-139">It is automatically generated from the telemetry from your app.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="8fc2d-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Application Map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="8fc2d-142">**Navigate from the boxes** to relevant dependency and other charts.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="8fc2d-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="8fc2d-144">[Learn more](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="8fc2d-145">Performance and failure blades</span><span class="sxs-lookup"><span data-stu-id="8fc2d-145">Performance and failure blades</span></span>
<span data-ttu-id="8fc2d-146">The performance blade shows the duration of dependency calls made by the server app.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="8fc2d-147">There's a summary chart and a table segmented by call.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-147">There's a summary chart and a table segmented by call.</span></span>

![Performance blade dependency charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="8fc2d-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Dependency call instances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="8fc2d-151">**Failure counts** are shown on the **Failures** blade.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="8fc2d-152">A failure is any return code that is not in the range 200-399, or unknown.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc2d-153">**100% failures?**</span><span class="sxs-lookup"><span data-stu-id="8fc2d-153">**100% failures?**</span></span> <span data-ttu-id="8fc2d-154">- This probably indicates that you are only getting partial dependency data.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="8fc2d-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="8fc2d-156">AJAX Calls</span><span class="sxs-lookup"><span data-stu-id="8fc2d-156">AJAX Calls</span></span>
<span data-ttu-id="8fc2d-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="8fc2d-158">They are shown as Dependencies.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-158">They are shown as Dependencies.</span></span>

## <a name="diagnosis"></a> <span data-ttu-id="8fc2d-159">Diagnose slow requests</span><span class="sxs-lookup"><span data-stu-id="8fc2d-159">Diagnose slow requests</span></span>
<span data-ttu-id="8fc2d-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="8fc2d-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="8fc2d-162">Let's walk through an example of that.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="8fc2d-163">Tracing from requests to dependencies</span><span class="sxs-lookup"><span data-stu-id="8fc2d-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="8fc2d-164">Open the Performance blade, and look at the grid of requests:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-164">Open the Performance blade, and look at the grid of requests:</span></span>

![List of requests with averages and counts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="8fc2d-166">The top one is taking very long.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-166">The top one is taking very long.</span></span> <span data-ttu-id="8fc2d-167">Let's see if we can find out where the time is spent.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="8fc2d-168">Click that row to see individual request events:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-168">Click that row to see individual request events:</span></span>

![List of request occurrences](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="8fc2d-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Find Calls to Remote Dependencies, identify unusual Duration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="8fc2d-172">It looks like most of the time servicing this request was spent in a call to a local service.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="8fc2d-173">Select that row to get more information:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-173">Select that row to get more information:</span></span>

![Click through that remote dependency to identify the culprit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="8fc2d-175">Looks like this is where the problem is.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="8fc2d-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="8fc2d-177">Request timeline</span><span class="sxs-lookup"><span data-stu-id="8fc2d-177">Request timeline</span></span>
<span data-ttu-id="8fc2d-178">In a different case, there is no dependency call that is particularly long.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="8fc2d-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Find Calls to Remote Dependencies, identify unusual Duration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="8fc2d-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profiling-your-live-site"></a><span data-ttu-id="8fc2d-182">Profiling your live site</span><span class="sxs-lookup"><span data-stu-id="8fc2d-182">Profiling your live site</span></span>

<span data-ttu-id="8fc2d-183">No idea where the time goes?</span><span class="sxs-lookup"><span data-stu-id="8fc2d-183">No idea where the time goes?</span></span> <span data-ttu-id="8fc2d-184">The Application Insights profiler will trace HTTP calls to your live site and show you which functions in your code took the longest time.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-184">The Application Insights profiler will trace HTTP calls to your live site and show you which functions in your code took the longest time.</span></span> <span data-ttu-id="8fc2d-185">The profiler is currently in limited preview - you can [sign up to try it](https://aka.ms/AIProfilerPreview).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-185">The profiler is currently in limited preview - you can [sign up to try it](https://aka.ms/AIProfilerPreview).</span></span>

## <a name="failed-requests"></a><span data-ttu-id="8fc2d-186">Failed requests</span><span class="sxs-lookup"><span data-stu-id="8fc2d-186">Failed requests</span></span>
<span data-ttu-id="8fc2d-187">Failed requests might also be associated with failed calls to dependencies.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-187">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="8fc2d-188">Again, we can click through to track down the problem.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-188">Again, we can click through to track down the problem.</span></span>

![Click the failed requests chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="8fc2d-190">Click through to an occurrence of a failed request, and look at its associated events.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-190">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Click a request type, click the instance to get to a different view of the same instance, click it to get exception details.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="8fc2d-192">Analytics</span><span class="sxs-lookup"><span data-stu-id="8fc2d-192">Analytics</span></span>
<span data-ttu-id="8fc2d-193">You can track dependencies in the [Analytics query language](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-193">You can track dependencies in the [Analytics query language](app-insights-analytics.md).</span></span> <span data-ttu-id="8fc2d-194">Here are some examples.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-194">Here are some examples.</span></span>

* <span data-ttu-id="8fc2d-195">Find any failed dependency calls:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-195">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="8fc2d-196">Find AJAX calls:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-196">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="8fc2d-197">Find dependency calls associated with requests:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-197">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="8fc2d-198">Find AJAX calls associated with page views:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-198">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="8fc2d-199">Custom dependency tracking</span><span class="sxs-lookup"><span data-stu-id="8fc2d-199">Custom dependency tracking</span></span>
<span data-ttu-id="8fc2d-200">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-200">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="8fc2d-201">But you might want some additional components to be treated in the same way.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-201">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="8fc2d-202">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-202">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="8fc2d-203">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-203">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="8fc2d-204">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-204">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

<span data-ttu-id="8fc2d-205">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2d-205">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8fc2d-206">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="8fc2d-206">Troubleshooting</span></span>
<span data-ttu-id="8fc2d-207">*Dependency success flag always shows either true or false.*</span><span class="sxs-lookup"><span data-stu-id="8fc2d-207">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="8fc2d-208">*SQL query not shown in full.*</span><span class="sxs-lookup"><span data-stu-id="8fc2d-208">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="8fc2d-209">Upgrade to the latest version of the SDK.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-209">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="8fc2d-210">If your .NET version is less than 4.6:</span><span class="sxs-lookup"><span data-stu-id="8fc2d-210">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="8fc2d-211">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-211">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="8fc2d-212">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fc2d-212">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="8fc2d-213">Video</span><span class="sxs-lookup"><span data-stu-id="8fc2d-213">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="8fc2d-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fc2d-214">Next steps</span></span>
* [<span data-ttu-id="8fc2d-215">Exceptions</span><span class="sxs-lookup"><span data-stu-id="8fc2d-215">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="8fc2d-216">User & page data</span><span class="sxs-lookup"><span data-stu-id="8fc2d-216">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="8fc2d-217">Availability</span><span class="sxs-lookup"><span data-stu-id="8fc2d-217">Availability</span></span>](app-insights-monitor-web-app-availability.md)











