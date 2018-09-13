---
title: Azure Application Insights for JavaScript web apps | Microsoft Docs
description: Get page view and session counts, web client data, and track usage patterns. Detect exceptions and performance issues in JavaScript web pages.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 36a95ce9be35e38465ea58ad00ae3bc3a26fb886
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564329"
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="d2f29-104">Application Insights for web pages</span><span class="sxs-lookup"><span data-stu-id="d2f29-104">Application Insights for web pages</span></span>
<span data-ttu-id="d2f29-105">Find out about the performance and usage of your web page or app.</span><span class="sxs-lookup"><span data-stu-id="d2f29-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="d2f29-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span><span class="sxs-lookup"><span data-stu-id="d2f29-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="d2f29-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span><span class="sxs-lookup"><span data-stu-id="d2f29-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="d2f29-108">You can set alerts on failure counts or slow page loading.</span><span class="sxs-lookup"><span data-stu-id="d2f29-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="d2f29-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span><span class="sxs-lookup"><span data-stu-id="d2f29-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="d2f29-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d2f29-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="d2f29-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span><span class="sxs-lookup"><span data-stu-id="d2f29-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![In portal.azure.com, open your app's resource and click Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/03.png)

<span data-ttu-id="d2f29-113">You need a subscription to [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2f29-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="d2f29-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span><span class="sxs-lookup"><span data-stu-id="d2f29-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="d2f29-115">Development and small-scale use won't cost anything.</span><span class="sxs-lookup"><span data-stu-id="d2f29-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="d2f29-116">Set up Application Insights for your web page</span><span class="sxs-lookup"><span data-stu-id="d2f29-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="d2f29-117">Add the loader code snippet to your web pages, as follows.</span><span class="sxs-lookup"><span data-stu-id="d2f29-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="d2f29-118">Open or create Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="d2f29-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="d2f29-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span><span class="sxs-lookup"><span data-stu-id="d2f29-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="d2f29-120">Sign into [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2f29-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d2f29-121">If you already set up monitoring for the server side of your app, you already have a resource:</span><span class="sxs-lookup"><span data-stu-id="d2f29-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Choose Browse, Developer Services, Application Insights.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/01-find.png)

<span data-ttu-id="d2f29-123">If you don't have one, create it:</span><span class="sxs-lookup"><span data-stu-id="d2f29-123">If you don't have one, create it:</span></span>

![Choose New, Developer Services, Application Insights.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/01-create.png)

<span data-ttu-id="d2f29-125">*Questions already?*</span><span class="sxs-lookup"><span data-stu-id="d2f29-125">*Questions already?*</span></span> <span data-ttu-id="d2f29-126">[More about creating a resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d2f29-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="d2f29-127">Add the SDK script to your app or web pages</span><span class="sxs-lookup"><span data-stu-id="d2f29-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="d2f29-128">In Quick Start, get the script for web pages:</span><span class="sxs-lookup"><span data-stu-id="d2f29-128">In Quick Start, get the script for web pages:</span></span>

![On your app overview blade, choose Quick Start, Get code to monitor my web pages.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="d2f29-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span><span class="sxs-lookup"><span data-stu-id="d2f29-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="d2f29-132">For example:</span><span class="sxs-lookup"><span data-stu-id="d2f29-132">For example:</span></span>

* <span data-ttu-id="d2f29-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="d2f29-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="d2f29-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d2f29-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="d2f29-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="d2f29-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="d2f29-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="d2f29-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="d2f29-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="d2f29-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="d2f29-138">Detailed configuration</span><span class="sxs-lookup"><span data-stu-id="d2f29-138">Detailed configuration</span></span>
<span data-ttu-id="d2f29-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span><span class="sxs-lookup"><span data-stu-id="d2f29-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="d2f29-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span><span class="sxs-lookup"><span data-stu-id="d2f29-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="d2f29-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span><span class="sxs-lookup"><span data-stu-id="d2f29-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="d2f29-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span><span class="sxs-lookup"><span data-stu-id="d2f29-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="d2f29-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span><span class="sxs-lookup"><span data-stu-id="d2f29-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a><span data-ttu-id="d2f29-144">Run your app</span><span class="sxs-lookup"><span data-stu-id="d2f29-144">Run your app</span></span>
<span data-ttu-id="d2f29-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span><span class="sxs-lookup"><span data-stu-id="d2f29-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="d2f29-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span><span class="sxs-lookup"><span data-stu-id="d2f29-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="d2f29-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span><span class="sxs-lookup"><span data-stu-id="d2f29-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="d2f29-148">Data is sent to dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="d2f29-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="d2f29-149">Explore your browser performance data</span><span class="sxs-lookup"><span data-stu-id="d2f29-149">Explore your browser performance data</span></span>
<span data-ttu-id="d2f29-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="d2f29-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![In portal.azure.com, open your app's resource and click Settings, Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/03.png)

<span data-ttu-id="d2f29-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="d2f29-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="d2f29-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span><span class="sxs-lookup"><span data-stu-id="d2f29-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="d2f29-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span><span class="sxs-lookup"><span data-stu-id="d2f29-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="d2f29-155">Click **Restore defaults** to get back to the original blade configuration.</span><span class="sxs-lookup"><span data-stu-id="d2f29-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="d2f29-156">Page load performance</span><span class="sxs-lookup"><span data-stu-id="d2f29-156">Page load performance</span></span>
<span data-ttu-id="d2f29-157">At the top is a segmented chart of page load times.</span><span class="sxs-lookup"><span data-stu-id="d2f29-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="d2f29-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="d2f29-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="d2f29-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span><span class="sxs-lookup"><span data-stu-id="d2f29-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="d2f29-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span><span class="sxs-lookup"><span data-stu-id="d2f29-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="d2f29-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="d2f29-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="d2f29-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span><span class="sxs-lookup"><span data-stu-id="d2f29-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="d2f29-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span><span class="sxs-lookup"><span data-stu-id="d2f29-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="d2f29-164">Slow loading?</span><span class="sxs-lookup"><span data-stu-id="d2f29-164">Slow loading?</span></span>
<span data-ttu-id="d2f29-165">Slow page loads are a major source of dissatisfaction for your users.</span><span class="sxs-lookup"><span data-stu-id="d2f29-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="d2f29-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span><span class="sxs-lookup"><span data-stu-id="d2f29-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="d2f29-167">The chart shows the average of all page loads in your app.</span><span class="sxs-lookup"><span data-stu-id="d2f29-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="d2f29-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span><span class="sxs-lookup"><span data-stu-id="d2f29-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="d2f29-169">Notice the page view count and standard deviation.</span><span class="sxs-lookup"><span data-stu-id="d2f29-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="d2f29-170">If the page count is very low, then the issue isn't affecting users much.</span><span class="sxs-lookup"><span data-stu-id="d2f29-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="d2f29-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span><span class="sxs-lookup"><span data-stu-id="d2f29-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="d2f29-172">**Zoom in on one URL and one page view.**</span><span class="sxs-lookup"><span data-stu-id="d2f29-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="d2f29-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span><span class="sxs-lookup"><span data-stu-id="d2f29-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/35.png)

<span data-ttu-id="d2f29-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span><span class="sxs-lookup"><span data-stu-id="d2f29-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="d2f29-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span><span class="sxs-lookup"><span data-stu-id="d2f29-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="d2f29-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span><span class="sxs-lookup"><span data-stu-id="d2f29-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="d2f29-177">**Page performance over time.**</span><span class="sxs-lookup"><span data-stu-id="d2f29-177">**Page performance over time.**</span></span> <span data-ttu-id="d2f29-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span><span class="sxs-lookup"><span data-stu-id="d2f29-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Click the head of the grid and select a new chart type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="d2f29-180">**Segment by other dimensions.**</span><span class="sxs-lookup"><span data-stu-id="d2f29-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="d2f29-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span><span class="sxs-lookup"><span data-stu-id="d2f29-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="d2f29-182">Add a new chart and experiment with the **Group-by** dimension.</span><span class="sxs-lookup"><span data-stu-id="d2f29-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="d2f29-183">AJAX Performance</span><span class="sxs-lookup"><span data-stu-id="d2f29-183">AJAX Performance</span></span>
<span data-ttu-id="d2f29-184">Make sure any AJAX calls in your web pages are performing well.</span><span class="sxs-lookup"><span data-stu-id="d2f29-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="d2f29-185">They are often used to fill parts of your page asynchronously.</span><span class="sxs-lookup"><span data-stu-id="d2f29-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="d2f29-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span><span class="sxs-lookup"><span data-stu-id="d2f29-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="d2f29-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span><span class="sxs-lookup"><span data-stu-id="d2f29-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="d2f29-188">There are summary charts in the upper part of the blade:</span><span class="sxs-lookup"><span data-stu-id="d2f29-188">There are summary charts in the upper part of the blade:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/31.png)

<span data-ttu-id="d2f29-189">and detailed grids lower down:</span><span class="sxs-lookup"><span data-stu-id="d2f29-189">and detailed grids lower down:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/33.png)

<span data-ttu-id="d2f29-190">Click any row for specific details.</span><span class="sxs-lookup"><span data-stu-id="d2f29-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="d2f29-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span><span class="sxs-lookup"><span data-stu-id="d2f29-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="d2f29-192">Click Restore Defaults to reconfigure the filter.</span><span class="sxs-lookup"><span data-stu-id="d2f29-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="d2f29-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span><span class="sxs-lookup"><span data-stu-id="d2f29-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/37.png)


<span data-ttu-id="d2f29-194">Click `...` for the full telemetry for an Ajax call.</span><span class="sxs-lookup"><span data-stu-id="d2f29-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="d2f29-195">No Ajax calls reported?</span><span class="sxs-lookup"><span data-stu-id="d2f29-195">No Ajax calls reported?</span></span>
<span data-ttu-id="d2f29-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span><span class="sxs-lookup"><span data-stu-id="d2f29-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="d2f29-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="d2f29-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="d2f29-198">Browser exceptions</span><span class="sxs-lookup"><span data-stu-id="d2f29-198">Browser exceptions</span></span>
<span data-ttu-id="d2f29-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span><span class="sxs-lookup"><span data-stu-id="d2f29-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/39.png)

<span data-ttu-id="d2f29-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="d2f29-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="d2f29-201">Inspect individual page view events</span><span class="sxs-lookup"><span data-stu-id="d2f29-201">Inspect individual page view events</span></span>

<span data-ttu-id="d2f29-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span><span class="sxs-lookup"><span data-stu-id="d2f29-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="d2f29-203">But for debugging purposes, you can also look at individual page view events.</span><span class="sxs-lookup"><span data-stu-id="d2f29-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="d2f29-204">In the Diagnostic Search blade, set Filters to Page View.</span><span class="sxs-lookup"><span data-stu-id="d2f29-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="d2f29-205">Select any event to see more detail.</span><span class="sxs-lookup"><span data-stu-id="d2f29-205">Select any event to see more detail.</span></span> <span data-ttu-id="d2f29-206">In the details page, click "..." to see even more detail.</span><span class="sxs-lookup"><span data-stu-id="d2f29-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="d2f29-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span><span class="sxs-lookup"><span data-stu-id="d2f29-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="d2f29-208">You can also use the powerful [Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span><span class="sxs-lookup"><span data-stu-id="d2f29-208">You can also use the powerful [Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="d2f29-209">Page view properties</span><span class="sxs-lookup"><span data-stu-id="d2f29-209">Page view properties</span></span>
* <span data-ttu-id="d2f29-210">**Page view duration**</span><span class="sxs-lookup"><span data-stu-id="d2f29-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="d2f29-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span><span class="sxs-lookup"><span data-stu-id="d2f29-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="d2f29-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="d2f29-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="d2f29-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span><span class="sxs-lookup"><span data-stu-id="d2f29-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="d2f29-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span><span class="sxs-lookup"><span data-stu-id="d2f29-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="d2f29-215">Custom page counts</span><span class="sxs-lookup"><span data-stu-id="d2f29-215">Custom page counts</span></span>
<span data-ttu-id="d2f29-216">By default, a page count occurs each time a new page loads into the client browser.</span><span class="sxs-lookup"><span data-stu-id="d2f29-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="d2f29-217">But you might want to count additional page views.</span><span class="sxs-lookup"><span data-stu-id="d2f29-217">But you might want to count additional page views.</span></span> <span data-ttu-id="d2f29-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span><span class="sxs-lookup"><span data-stu-id="d2f29-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="d2f29-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span><span class="sxs-lookup"><span data-stu-id="d2f29-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="d2f29-220">Insert a JavaScript call like this at the appropriate point in your client code:</span><span class="sxs-lookup"><span data-stu-id="d2f29-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="d2f29-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span><span class="sxs-lookup"><span data-stu-id="d2f29-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="d2f29-222">Usage tracking</span><span class="sxs-lookup"><span data-stu-id="d2f29-222">Usage tracking</span></span>
<span data-ttu-id="d2f29-223">Want to find out what your users do with your app?</span><span class="sxs-lookup"><span data-stu-id="d2f29-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="d2f29-224">Learn about usage tracking</span><span class="sxs-lookup"><span data-stu-id="d2f29-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="d2f29-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d2f29-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <a name="video"></a> <span data-ttu-id="d2f29-226">Video</span><span class="sxs-lookup"><span data-stu-id="d2f29-226">Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> <span data-ttu-id="d2f29-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2f29-227">Next steps</span></span>
* [<span data-ttu-id="d2f29-228">Track usage</span><span class="sxs-lookup"><span data-stu-id="d2f29-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="d2f29-229">Custom events and metrics</span><span class="sxs-lookup"><span data-stu-id="d2f29-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="d2f29-230">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="d2f29-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)
















