---
title: Using Search in Azure Application Insights | Microsoft Docs
description: Search and filter raw telemetry sent by your web app.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: abef6f2c012141c2c92b65c2b942bb642f460c74
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564572"
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="bcfdc-103">Using Search in Application Insights</span><span class="sxs-lookup"><span data-stu-id="bcfdc-103">Using Search in Application Insights</span></span>
<span data-ttu-id="bcfdc-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="bcfdc-105">And you can view log traces and events that you have coded.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="bcfdc-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="bcfdc-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="bcfdc-107">Where do you see Search?</span><span class="sxs-lookup"><span data-stu-id="bcfdc-107">Where do you see Search?</span></span>
### <a name="in-the-azure-portal"></a><span data-ttu-id="bcfdc-108">In the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bcfdc-108">In the Azure portal</span></span>
<span data-ttu-id="bcfdc-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span></span>

![Open diagnostic search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="bcfdc-111">It also opens when you click through some charts and grid items.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="bcfdc-112">In this case, its filters are pre-set to focus on the type of item you selected.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-112">In this case, its filters are pre-set to focus on the type of item you selected.</span></span> 

<span data-ttu-id="bcfdc-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="bcfdc-114">Click through a performance range to see a list of individual requests in that response time range:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-114">Click through a performance range to see a list of individual requests in that response time range:</span></span>

![Click through request performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="bcfdc-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="bcfdc-117">At the top of the list is a summary chart showing counts of events over time.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-117">At the top of the list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="bcfdc-118">Click Refresh to get new events.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-118">Click Refresh to get new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="bcfdc-119">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcfdc-119">In Visual Studio</span></span>

<span data-ttu-id="bcfdc-120">In Visual Studio, there's also an Application Insights Search window.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="bcfdc-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span></span> <span data-ttu-id="bcfdc-122">But it can also show the events collected from your published app at the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-122">But it can also show the events collected from your published app at the Azure portal.</span></span>

<span data-ttu-id="bcfdc-123">Open the Search window in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-123">Open the Search window in Visual Studio:</span></span>

![Visual Studio open Application Insights search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="bcfdc-125">The Search window has features similar to the web portal:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-125">The Search window has features similar to the web portal:</span></span>

![Visual Studio Application Insights search window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="bcfdc-127">The Track Operation tab is available when you open a request or a page view.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-127">The Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="bcfdc-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span></span> <span data-ttu-id="bcfdc-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="bcfdc-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="bcfdc-131">Inspect individual items</span><span class="sxs-lookup"><span data-stu-id="bcfdc-131">Inspect individual items</span></span>
<span data-ttu-id="bcfdc-132">Select any telemetry item to see key fields and related items.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-132">Select any telemetry item to see key fields and related items.</span></span> <span data-ttu-id="bcfdc-133">If you want to see the full set of fields, click "...".</span><span class="sxs-lookup"><span data-stu-id="bcfdc-133">If you want to see the full set of fields, click "...".</span></span> 

![Click New Work Item, edit the fields, and then click OK.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="bcfdc-135">Filter event types</span><span class="sxs-lookup"><span data-stu-id="bcfdc-135">Filter event types</span></span>
<span data-ttu-id="bcfdc-136">Open the Filter blade and choose the event types you want to see.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-136">Open the Filter blade and choose the event types you want to see.</span></span> <span data-ttu-id="bcfdc-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span><span class="sxs-lookup"><span data-stu-id="bcfdc-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span></span>

![Choose Filter and select telemetry types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="bcfdc-139">The event types are:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-139">The event types are:</span></span>

* <span data-ttu-id="bcfdc-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="bcfdc-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="bcfdc-142">These events are used to create the request and response overview charts.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-142">These events are used to create the request and response overview charts.</span></span>
* <span data-ttu-id="bcfdc-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span></span> 
* <span data-ttu-id="bcfdc-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="bcfdc-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span><span class="sxs-lookup"><span data-stu-id="bcfdc-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="bcfdc-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="bcfdc-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="bcfdc-148">Filter on property values</span><span class="sxs-lookup"><span data-stu-id="bcfdc-148">Filter on property values</span></span>
<span data-ttu-id="bcfdc-149">You can filter events on the values of their properties.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-149">You can filter events on the values of their properties.</span></span> <span data-ttu-id="bcfdc-150">The available properties depend on the event types you selected.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-150">The available properties depend on the event types you selected.</span></span> 

<span data-ttu-id="bcfdc-151">For example, pick out requests with a specific response code.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-151">For example, pick out requests with a specific response code.</span></span> 

![Expand a property and choose a value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="bcfdc-153">Choosing no values of a particular property has the same effect as choosing all values.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-153">Choosing no values of a particular property has the same effect as choosing all values.</span></span> <span data-ttu-id="bcfdc-154">It switches off filtering on that property.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="bcfdc-155">Narrow your search</span><span class="sxs-lookup"><span data-stu-id="bcfdc-155">Narrow your search</span></span>
<span data-ttu-id="bcfdc-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span></span> 

<span data-ttu-id="bcfdc-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span></span>

![Expand a property and choose a value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-the-same-property"></a><span data-ttu-id="bcfdc-159">Find events with the same property</span><span class="sxs-lookup"><span data-stu-id="bcfdc-159">Find events with the same property</span></span>
<span data-ttu-id="bcfdc-160">Find all the items with the same property value:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-160">Find all the items with the same property value:</span></span>

![Right-click a property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-the-data"></a><span data-ttu-id="bcfdc-162">Search the data</span><span class="sxs-lookup"><span data-stu-id="bcfdc-162">Search the data</span></span>

> [!NOTE]
> <span data-ttu-id="bcfdc-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span></span>
> 

<span data-ttu-id="bcfdc-164">You can search for terms in any of the property values.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-164">You can search for terms in any of the property values.</span></span> <span data-ttu-id="bcfdc-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="bcfdc-166">You might want to set a time range, as searches over a shorter range are faster.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-166">You might want to set a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostic search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="bcfdc-168">Search for complete words, not substrings.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="bcfdc-169">Use quotation marks to enclose special characters.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-169">Use quotation marks to enclose special characters.</span></span>

| <span data-ttu-id="bcfdc-170">string</span><span class="sxs-lookup"><span data-stu-id="bcfdc-170">string</span></span> | <span data-ttu-id="bcfdc-171">is *not* found by</span><span class="sxs-lookup"><span data-stu-id="bcfdc-171">is *not* found by</span></span> | <span data-ttu-id="bcfdc-172">but these do find it</span><span class="sxs-lookup"><span data-stu-id="bcfdc-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bcfdc-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="bcfdc-173">HomeController.About</span></span> |<span data-ttu-id="bcfdc-174">home</span><span class="sxs-lookup"><span data-stu-id="bcfdc-174">home</span></span><br/><span data-ttu-id="bcfdc-175">controller</span><span class="sxs-lookup"><span data-stu-id="bcfdc-175">controller</span></span><br/><span data-ttu-id="bcfdc-176">out</span><span class="sxs-lookup"><span data-stu-id="bcfdc-176">out</span></span> | <span data-ttu-id="bcfdc-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="bcfdc-177">homecontroller</span></span><br/><span data-ttu-id="bcfdc-178">about</span><span class="sxs-lookup"><span data-stu-id="bcfdc-178">about</span></span><br/><span data-ttu-id="bcfdc-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="bcfdc-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="bcfdc-180">United States</span><span class="sxs-lookup"><span data-stu-id="bcfdc-180">United States</span></span>|<span data-ttu-id="bcfdc-181">Uni</span><span class="sxs-lookup"><span data-stu-id="bcfdc-181">Uni</span></span><br/><span data-ttu-id="bcfdc-182">ted</span><span class="sxs-lookup"><span data-stu-id="bcfdc-182">ted</span></span>|<span data-ttu-id="bcfdc-183">united</span><span class="sxs-lookup"><span data-stu-id="bcfdc-183">united</span></span><br/><span data-ttu-id="bcfdc-184">states</span><span class="sxs-lookup"><span data-stu-id="bcfdc-184">states</span></span><br/><span data-ttu-id="bcfdc-185">united AND states</span><span class="sxs-lookup"><span data-stu-id="bcfdc-185">united AND states</span></span><br/><span data-ttu-id="bcfdc-186">"united states"</span><span class="sxs-lookup"><span data-stu-id="bcfdc-186">"united states"</span></span>

<span data-ttu-id="bcfdc-187">Here are the search expressions you can use:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-187">Here are the search expressions you can use:</span></span>

| <span data-ttu-id="bcfdc-188">Sample query</span><span class="sxs-lookup"><span data-stu-id="bcfdc-188">Sample query</span></span> | <span data-ttu-id="bcfdc-189">Effect</span><span class="sxs-lookup"><span data-stu-id="bcfdc-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="bcfdc-190">Find all events in the time range whose fields include the word "apple"</span><span class="sxs-lookup"><span data-stu-id="bcfdc-190">Find all events in the time range whose fields include the word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="bcfdc-191">Find events that contain both words.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-191">Find events that contain both words.</span></span> <span data-ttu-id="bcfdc-192">Use capital "AND", not "and".</span><span class="sxs-lookup"><span data-stu-id="bcfdc-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="bcfdc-193">Find events that contain either word.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-193">Find events that contain either word.</span></span> <span data-ttu-id="bcfdc-194">Use "OR", not "or".</span><span class="sxs-lookup"><span data-stu-id="bcfdc-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="bcfdc-195">Short form.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="bcfdc-196">Find events that contain one word but not the other.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-196">Find events that contain one word but not the other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="bcfdc-197">Sampling</span><span class="sxs-lookup"><span data-stu-id="bcfdc-197">Sampling</span></span>
<span data-ttu-id="bcfdc-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="bcfdc-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="bcfdc-200">[Learn about sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="bcfdc-201">Create work item</span><span class="sxs-lookup"><span data-stu-id="bcfdc-201">Create work item</span></span>
<span data-ttu-id="bcfdc-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span></span> 

![Click New Work Item, edit the fields, and then click OK.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="bcfdc-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span></span>

![Fill the URL of your Team Services server and the Project name, and click Authorize](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="bcfdc-206">(You can also configure the link on the Work Items blade.)</span><span class="sxs-lookup"><span data-stu-id="bcfdc-206">(You can also configure the link on the Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="bcfdc-207">Save your search</span><span class="sxs-lookup"><span data-stu-id="bcfdc-207">Save your search</span></span>
<span data-ttu-id="bcfdc-208">When you've set all the filters you want, you can save the search as a favorite.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-208">When you've set all the filters you want, you can save the search as a favorite.</span></span> <span data-ttu-id="bcfdc-209">If you work in an organizational account, you can choose whether to share it with other team members.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-209">If you work in an organizational account, you can choose whether to share it with other team members.</span></span>

![Click Favorite, set the name, and click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="bcfdc-211">To see the search again, **go to the overview blade** and open Favorites:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-211">To see the search again, **go to the overview blade** and open Favorites:</span></span>

![Favorites tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="bcfdc-213">If you saved with Relative time range, the re-opened blade has the latest data.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-213">If you saved with Relative time range, the re-opened blade has the latest data.</span></span> <span data-ttu-id="bcfdc-214">If you saved with Absolute time range, you see the same data every time.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-214">If you saved with Absolute time range, you see the same data every time.</span></span> <span data-ttu-id="bcfdc-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span><span class="sxs-lookup"><span data-stu-id="bcfdc-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-to-application-insights"></a><span data-ttu-id="bcfdc-216">Send more telemetry to Application Insights</span><span class="sxs-lookup"><span data-stu-id="bcfdc-216">Send more telemetry to Application Insights</span></span>
<span data-ttu-id="bcfdc-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span><span class="sxs-lookup"><span data-stu-id="bcfdc-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="bcfdc-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="bcfdc-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="bcfdc-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="bcfdc-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="questions"></a><span data-ttu-id="bcfdc-222">Q & A</span><span class="sxs-lookup"><span data-stu-id="bcfdc-222">Q & A</span></span>
### <a name="limits"></a><span data-ttu-id="bcfdc-223">How much data is retained?</span><span class="sxs-lookup"><span data-stu-id="bcfdc-223">How much data is retained?</span></span>

<span data-ttu-id="bcfdc-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="bcfdc-225">How can I see POST data in my server requests?</span><span class="sxs-lookup"><span data-stu-id="bcfdc-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="bcfdc-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bcfdc-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="bcfdc-227">Put the POST data in the message parameter.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-227">Put the POST data in the message parameter.</span></span> <span data-ttu-id="bcfdc-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span><span class="sxs-lookup"><span data-stu-id="bcfdc-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="bcfdc-229">Video</span><span class="sxs-lookup"><span data-stu-id="bcfdc-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a><span data-ttu-id="bcfdc-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="bcfdc-230">Next steps</span></span>
* [<span data-ttu-id="bcfdc-231">Write complex queries in Analytics</span><span class="sxs-lookup"><span data-stu-id="bcfdc-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="bcfdc-232">Send logs and custom telemetry to Application Insights</span><span class="sxs-lookup"><span data-stu-id="bcfdc-232">Send logs and custom telemetry to Application Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="bcfdc-233">Set up availability and responsiveness tests</span><span class="sxs-lookup"><span data-stu-id="bcfdc-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="bcfdc-234">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="bcfdc-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)














