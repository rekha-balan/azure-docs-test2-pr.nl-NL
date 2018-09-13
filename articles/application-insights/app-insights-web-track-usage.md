---
title: Usage analysis for web applications with Azure Application Insights | Microsoft docs
description: Overview of usage analysis with Application Insights
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: bbdb8e58-7115-48d8-93c0-f69a1beeea6e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: awills
ms.openlocfilehash: 2c3af2a063ddaf2d6006c4de37f1f94a960c6a77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556415"
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="df344-103">Usage analysis for web applications with Application Insights</span><span class="sxs-lookup"><span data-stu-id="df344-103">Usage analysis for web applications with Application Insights</span></span>
<span data-ttu-id="df344-104">Knowing how people use your application lets you focus your development work on the scenarios that are most important to your users, and gain insights into the goals that they find easier or more difficult to achieve.</span><span class="sxs-lookup"><span data-stu-id="df344-104">Knowing how people use your application lets you focus your development work on the scenarios that are most important to your users, and gain insights into the goals that they find easier or more difficult to achieve.</span></span>

<span data-ttu-id="df344-105">[Azure Application Insights](app-insights-overview.md) provides two levels of usage tracking:</span><span class="sxs-lookup"><span data-stu-id="df344-105">[Azure Application Insights](app-insights-overview.md) provides two levels of usage tracking:</span></span>

* <span data-ttu-id="df344-106">**User, session and page view data** - provided out of the box.</span><span class="sxs-lookup"><span data-stu-id="df344-106">**User, session and page view data** - provided out of the box.</span></span>  
* <span data-ttu-id="df344-107">**Custom telemetry** - You [write code](app-insights-api-custom-events-metrics.md) to trace your users through your app's user experience.</span><span class="sxs-lookup"><span data-stu-id="df344-107">**Custom telemetry** - You [write code](app-insights-api-custom-events-metrics.md) to trace your users through your app's user experience.</span></span> 


## <a name="get-started"></a><span data-ttu-id="df344-108">Get started</span><span class="sxs-lookup"><span data-stu-id="df344-108">Get started</span></span>

<span data-ttu-id="df344-109">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span><span class="sxs-lookup"><span data-stu-id="df344-109">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="df344-110">The client and server components of your app send telemetry back to the Azure portal for analysis.</span><span class="sxs-lookup"><span data-stu-id="df344-110">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="df344-111">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span><span class="sxs-lookup"><span data-stu-id="df344-111">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="df344-112">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="df344-112">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="df344-113">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span><span class="sxs-lookup"><span data-stu-id="df344-113">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copy the script into the head of your master web page.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/02-monitor-web-page.png)


3. <span data-ttu-id="df344-115">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="df344-115">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="df344-116">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span><span class="sxs-lookup"><span data-stu-id="df344-116">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="usage-analysis-out-of-the-box"></a><span data-ttu-id="df344-117">Usage analysis out of the box</span><span class="sxs-lookup"><span data-stu-id="df344-117">Usage analysis out of the box</span></span>
<span data-ttu-id="df344-118">Open the Usage blade.</span><span class="sxs-lookup"><span data-stu-id="df344-118">Open the Usage blade.</span></span>

![Users, sessions and page views charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/14-usage.png)

<span data-ttu-id="df344-120">Hover in the blank part above a graph to see the counts at a particular point.</span><span class="sxs-lookup"><span data-stu-id="df344-120">Hover in the blank part above a graph to see the counts at a particular point.</span></span> <span data-ttu-id="df344-121">Otherwise, the numbers show the value aggregated over the period, such as an average, a total, or a count of distinct users over the period.</span><span class="sxs-lookup"><span data-stu-id="df344-121">Otherwise, the numbers show the value aggregated over the period, such as an average, a total, or a count of distinct users over the period.</span></span>

<span data-ttu-id="df344-122">What do these charts show?</span><span class="sxs-lookup"><span data-stu-id="df344-122">What do these charts show?</span></span>

* <span data-ttu-id="df344-123">**Users:** The count of distinct active users over the time range of the chart.</span><span class="sxs-lookup"><span data-stu-id="df344-123">**Users:** The count of distinct active users over the time range of the chart.</span></span> <span data-ttu-id="df344-124">In web applications, users are counted by using cookies.</span><span class="sxs-lookup"><span data-stu-id="df344-124">In web applications, users are counted by using cookies.</span></span> <span data-ttu-id="df344-125">A person who uses several browsers, clears cookies, or uses the privacy feature will be counted several times.</span><span class="sxs-lookup"><span data-stu-id="df344-125">A person who uses several browsers, clears cookies, or uses the privacy feature will be counted several times.</span></span>
* <span data-ttu-id="df344-126">**Authenticated users** are counted if you have inserted a call to [setAuthenticatedUser()](app-insights-api-custom-events-metrics.md#authenticated-users) in your code.</span><span class="sxs-lookup"><span data-stu-id="df344-126">**Authenticated users** are counted if you have inserted a call to [setAuthenticatedUser()](app-insights-api-custom-events-metrics.md#authenticated-users) in your code.</span></span>
* <span data-ttu-id="df344-127">**Sessions:** The count of active sessions.</span><span class="sxs-lookup"><span data-stu-id="df344-127">**Sessions:** The count of active sessions.</span></span> <span data-ttu-id="df344-128">A web session is counted after 30 minutes of inactivity.</span><span class="sxs-lookup"><span data-stu-id="df344-128">A web session is counted after 30 minutes of inactivity.</span></span> 
* <span data-ttu-id="df344-129">**Page views** Counts the number of calls to trackPageView(), typically called once in each web page.</span><span class="sxs-lookup"><span data-stu-id="df344-129">**Page views** Counts the number of calls to trackPageView(), typically called once in each web page.</span></span>

<span data-ttu-id="df344-130">Click any of the charts to see more detail.</span><span class="sxs-lookup"><span data-stu-id="df344-130">Click any of the charts to see more detail.</span></span> <span data-ttu-id="df344-131">Notice that you can change the time range of the charts.</span><span class="sxs-lookup"><span data-stu-id="df344-131">Notice that you can change the time range of the charts.</span></span>

### <a name="where-do-my-users-live"></a><span data-ttu-id="df344-132">Where do my users live?</span><span class="sxs-lookup"><span data-stu-id="df344-132">Where do my users live?</span></span>
<span data-ttu-id="df344-133">Click a blank part of the Users chart to see open another blade that shows more detail:</span><span class="sxs-lookup"><span data-stu-id="df344-133">Click a blank part of the Users chart to see open another blade that shows more detail:</span></span>

![On the Usage blade, click the Users chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/02-sessions.png)

### <a name="what-browsers-or-operating-systems-do-they-use"></a><span data-ttu-id="df344-135">What browsers or operating systems do they use?</span><span class="sxs-lookup"><span data-stu-id="df344-135">What browsers or operating systems do they use?</span></span>

<span data-ttu-id="df344-136">Click **Edit** on the users chart, and Group (segment) data by a property such as Browser, Operating System, or City:</span><span class="sxs-lookup"><span data-stu-id="df344-136">Click **Edit** on the users chart, and Group (segment) data by a property such as Browser, Operating System, or City:</span></span> 

![Select a chart that shows a single metric, switch on Grouping, and choose a property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/03-browsers.png)

<span data-ttu-id="df344-138">To see the full set of counts, switch the chart type to **Grid**.</span><span class="sxs-lookup"><span data-stu-id="df344-138">To see the full set of counts, switch the chart type to **Grid**.</span></span> <span data-ttu-id="df344-139">You can also choose to display additional metrics:</span><span class="sxs-lookup"><span data-stu-id="df344-139">You can also choose to display additional metrics:</span></span>

![Multi-column grid chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/multi-column-grid.png)

<span data-ttu-id="df344-141">For graphical chart types, you can either group by a property, or select multiple metrics, but not both.</span><span class="sxs-lookup"><span data-stu-id="df344-141">For graphical chart types, you can either group by a property, or select multiple metrics, but not both.</span></span> <span data-ttu-id="df344-142">This chart compares two metrics, users and [authenticated users](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="df344-142">This chart compares two metrics, users and [authenticated users](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span> 

![Select a chart, search for and check or uncheck metrics.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/031-dual.png)



## <a name="page-views"></a><span data-ttu-id="df344-144">Page views</span><span class="sxs-lookup"><span data-stu-id="df344-144">Page views</span></span>
<span data-ttu-id="df344-145">From the Usage blade, click through the page views chart to get a more detailed version together with a breakdown of your most popular pages:</span><span class="sxs-lookup"><span data-stu-id="df344-145">From the Usage blade, click through the page views chart to get a more detailed version together with a breakdown of your most popular pages:</span></span>

![From the Overview blade, click the Page views chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/05-games.png)

<span data-ttu-id="df344-147">The example above is from a games web site.</span><span class="sxs-lookup"><span data-stu-id="df344-147">The example above is from a games web site.</span></span> <span data-ttu-id="df344-148">From the charts, we can instantly see:</span><span class="sxs-lookup"><span data-stu-id="df344-148">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="df344-149">Usage hasn't improved in the past week.</span><span class="sxs-lookup"><span data-stu-id="df344-149">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="df344-150">Maybe we should think about search engine optimization?</span><span class="sxs-lookup"><span data-stu-id="df344-150">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="df344-151">Tennis is the most popular game page.</span><span class="sxs-lookup"><span data-stu-id="df344-151">Tennis is the most popular game page.</span></span> <span data-ttu-id="df344-152">Let's focus on further improvements to this page.</span><span class="sxs-lookup"><span data-stu-id="df344-152">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="df344-153">On average, users visit the Tennis page about three times per week.</span><span class="sxs-lookup"><span data-stu-id="df344-153">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="df344-154">(There are about three times more sessions than users.)</span><span class="sxs-lookup"><span data-stu-id="df344-154">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="df344-155">Most users visit the site during the U.S. working week, and in working hours.</span><span class="sxs-lookup"><span data-stu-id="df344-155">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="df344-156">Perhaps we should provide a "quick hide" button on the web page.</span><span class="sxs-lookup"><span data-stu-id="df344-156">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="df344-157">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span><span class="sxs-lookup"><span data-stu-id="df344-157">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="df344-158">None of the recent deployments had a noticeable effect on usage.</span><span class="sxs-lookup"><span data-stu-id="df344-158">None of the recent deployments had a noticeable effect on usage.</span></span>

## <a name="custom-tracking"></a><span data-ttu-id="df344-159">Custom tracking</span><span class="sxs-lookup"><span data-stu-id="df344-159">Custom tracking</span></span>
<span data-ttu-id="df344-160">Let's suppose that instead of implementing each game in a separate web page, you decide to refactor them all into the same single-page app, with most of the functionality coded as Javascript in the web page.</span><span class="sxs-lookup"><span data-stu-id="df344-160">Let's suppose that instead of implementing each game in a separate web page, you decide to refactor them all into the same single-page app, with most of the functionality coded as Javascript in the web page.</span></span> <span data-ttu-id="df344-161">This allows the user to switch quickly between one game and another, or even have several games on one page.</span><span class="sxs-lookup"><span data-stu-id="df344-161">This allows the user to switch quickly between one game and another, or even have several games on one page.</span></span>

<span data-ttu-id="df344-162">But you'd still like Application Insights to log the number of times each game is opened, in exactly the same way as when they were on separate web pages.</span><span class="sxs-lookup"><span data-stu-id="df344-162">But you'd still like Application Insights to log the number of times each game is opened, in exactly the same way as when they were on separate web pages.</span></span> <span data-ttu-id="df344-163">That's easy: just insert a call to the telemetry module into your JavaScript where you want to record that a new 'page' has opened:</span><span class="sxs-lookup"><span data-stu-id="df344-163">That's easy: just insert a call to the telemetry module into your JavaScript where you want to record that a new 'page' has opened:</span></span>

```JavaScript
    telemetryClient.trackPageView(game.Name);
```
<span data-ttu-id="df344-164">This call simulates the telemetry that logs a page view.</span><span class="sxs-lookup"><span data-stu-id="df344-164">This call simulates the telemetry that logs a page view.</span></span>  <span data-ttu-id="df344-165">However, you don't always want to mix the messages up with page views.</span><span class="sxs-lookup"><span data-stu-id="df344-165">However, you don't always want to mix the messages up with page views.</span></span> <span data-ttu-id="df344-166">Instead, use custom events.</span><span class="sxs-lookup"><span data-stu-id="df344-166">Instead, use custom events.</span></span> <span data-ttu-id="df344-167">You can send them from web pages or a web server:</span><span class="sxs-lookup"><span data-stu-id="df344-167">You can send them from web pages or a web server:</span></span>


```JavaScript

    telemetryClient.trackEvent("GameEnd");
```

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("GameEnd");
```

```VB

    Dim tc = New Microsoft.ApplicationInsights.TelemetryClient()
    tc.TrackEvent("GameEnd")
```

<span data-ttu-id="df344-168">[Custom telemetry inserted into your web or server code](app-insights-api-custom-events-metrics.md#trackevent) can be used in many ways to understand how your application is being used.</span><span class="sxs-lookup"><span data-stu-id="df344-168">[Custom telemetry inserted into your web or server code](app-insights-api-custom-events-metrics.md#trackevent) can be used in many ways to understand how your application is being used.</span></span>

<span data-ttu-id="df344-169">To view events sent by TrackEvent(): Open Metrics Explorer, add a new chart, and then edit it.</span><span class="sxs-lookup"><span data-stu-id="df344-169">To view events sent by TrackEvent(): Open Metrics Explorer, add a new chart, and then edit it.</span></span> <span data-ttu-id="df344-170">Your metrics appear under Custom Metrics.</span><span class="sxs-lookup"><span data-stu-id="df344-170">Your metrics appear under Custom Metrics.</span></span> 

![A chart showing custom events.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/06-eventsSegment.png)

<span data-ttu-id="df344-172">If you set [property values](app-insights-api-custom-events-metrics.md#properties) (also called dimensions) in your events, you can group and filter by them.</span><span class="sxs-lookup"><span data-stu-id="df344-172">If you set [property values](app-insights-api-custom-events-metrics.md#properties) (also called dimensions) in your events, you can group and filter by them.</span></span>

<span data-ttu-id="df344-173">Create multiple charts to correlate changes in other metrics and events.</span><span class="sxs-lookup"><span data-stu-id="df344-173">Create multiple charts to correlate changes in other metrics and events.</span></span> <span data-ttu-id="df344-174">For example, at times when more games are played, you'd expect to see a rise in abandoned games as well.</span><span class="sxs-lookup"><span data-stu-id="df344-174">For example, at times when more games are played, you'd expect to see a rise in abandoned games as well.</span></span> <span data-ttu-id="df344-175">But the rise in abandoned games is disproportionate, you'd want to find out whether the high load is causing problems that users find unacceptable.</span><span class="sxs-lookup"><span data-stu-id="df344-175">But the rise in abandoned games is disproportionate, you'd want to find out whether the high load is causing problems that users find unacceptable.</span></span>

## <a name="drill-into-specific-events"></a><span data-ttu-id="df344-176">Drill into specific events</span><span class="sxs-lookup"><span data-stu-id="df344-176">Drill into specific events</span></span>
<span data-ttu-id="df344-177">To get a better understanding of how a typical session goes, you might want to focus on a specific user session that contains a particular type of event.</span><span class="sxs-lookup"><span data-stu-id="df344-177">To get a better understanding of how a typical session goes, you might want to focus on a specific user session that contains a particular type of event.</span></span>

<span data-ttu-id="df344-178">From a grid of events, click through the event of interest, and select a recent specific occurrence:</span><span class="sxs-lookup"><span data-stu-id="df344-178">From a grid of events, click through the event of interest, and select a recent specific occurrence:</span></span>

![In the list under the summary chart, click an event](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/08-searchEvents.png)

<span data-ttu-id="df344-180">Let's look at all the telemetry for the session in which that particular NoGame event occurred.</span><span class="sxs-lookup"><span data-stu-id="df344-180">Let's look at all the telemetry for the session in which that particular NoGame event occurred.</span></span>

![Click 'all telemetry for session'](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/09-relatedTelemetry.png)

<span data-ttu-id="df344-182">There were no exceptions, so the user wasn't prevented from playing by some failure.</span><span class="sxs-lookup"><span data-stu-id="df344-182">There were no exceptions, so the user wasn't prevented from playing by some failure.</span></span>

<span data-ttu-id="df344-183">We can filter out all types of telemetry except page views for this session:</span><span class="sxs-lookup"><span data-stu-id="df344-183">We can filter out all types of telemetry except page views for this session:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/10-filter.png)

<span data-ttu-id="df344-184">And now we can see that this user logged in simply to check the latest scores.</span><span class="sxs-lookup"><span data-stu-id="df344-184">And now we can see that this user logged in simply to check the latest scores.</span></span> <span data-ttu-id="df344-185">Maybe we should consider developing a user story that makes it easier to do that.</span><span class="sxs-lookup"><span data-stu-id="df344-185">Maybe we should consider developing a user story that makes it easier to do that.</span></span> <span data-ttu-id="df344-186">(And we should implement a custom event to report when this specific story occurs.)</span><span class="sxs-lookup"><span data-stu-id="df344-186">(And we should implement a custom event to report when this specific story occurs.)</span></span>

## <a name="filter-search-and-segment-your-data-with-properties"></a><span data-ttu-id="df344-187">Filter, search and segment your data with properties</span><span class="sxs-lookup"><span data-stu-id="df344-187">Filter, search and segment your data with properties</span></span>
<span data-ttu-id="df344-188">You can attach arbitrary tags and numeric values to events.</span><span class="sxs-lookup"><span data-stu-id="df344-188">You can attach arbitrary tags and numeric values to events.</span></span>

<span data-ttu-id="df344-189">*JavaScript in web page*</span><span class="sxs-lookup"><span data-stu-id="df344-189">*JavaScript in web page*</span></span>

```JavaScript

    appInsights.trackEvent("WinGame",
        // String properties:
        {Game: currentGame.name, Difficulty: currentGame.difficulty},
        // Numeric measurements:
        {Score: currentGame.score, Opponents: currentGame.opponentCount}
    );
```

<span data-ttu-id="df344-190">*C# at server*</span><span class="sxs-lookup"><span data-stu-id="df344-190">*C# at server*</span></span>

```C#

    // Set up some properties:
    var properties = new Dictionary <string, string>
        {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var measurements = new Dictionary <string, double>
        {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, measurements);
```

<span data-ttu-id="df344-191">*VB at server*</span><span class="sxs-lookup"><span data-stu-id="df344-191">*VB at server*</span></span>

```VB

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim measurements = New Dictionary (Of String, Double)
    measurements.Add("Score", currentGame.Score)
    measurements.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, measurements)
```

<span data-ttu-id="df344-192">Attach properties to page views in the same way:</span><span class="sxs-lookup"><span data-stu-id="df344-192">Attach properties to page views in the same way:</span></span>

<span data-ttu-id="df344-193">*JavaScript in web page*</span><span class="sxs-lookup"><span data-stu-id="df344-193">*JavaScript in web page*</span></span>

```JS

    appInsights.trackPageView("Win", 
        url,
        {Game: currentGame.Name}, 
        {Score: currentGame.Score});
```

<span data-ttu-id="df344-194">In Diagnostic Search, view the properties by clicking through an individual occurrence of an event.</span><span class="sxs-lookup"><span data-stu-id="df344-194">In Diagnostic Search, view the properties by clicking through an individual occurrence of an event.</span></span>

![In the list of events, open an event, and then click '...' to see more properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/11-details.png)

<span data-ttu-id="df344-196">Use the Search field to see event occurrences with a particular property value.</span><span class="sxs-lookup"><span data-stu-id="df344-196">Use the Search field to see event occurrences with a particular property value.</span></span>

![Type a value into the Search field](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/12-searchEvents.png)

## <a name="edit-and-create-queries-over-your-telemetry"></a><span data-ttu-id="df344-198">Edit and create queries over your telemetry</span><span class="sxs-lookup"><span data-stu-id="df344-198">Edit and create queries over your telemetry</span></span>

<span data-ttu-id="df344-199">Click the Azure Analytics icon on any chart to open an equivalent query that you can edit.</span><span class="sxs-lookup"><span data-stu-id="df344-199">Click the Azure Analytics icon on any chart to open an equivalent query that you can edit.</span></span>
<span data-ttu-id="df344-200">Scroll down to see if there is more than one generated query.</span><span class="sxs-lookup"><span data-stu-id="df344-200">Scroll down to see if there is more than one generated query.</span></span> <span data-ttu-id="df344-201">Place the cursor in any query and click **Go**.</span><span class="sxs-lookup"><span data-stu-id="df344-201">Place the cursor in any query and click **Go**.</span></span> 

<span data-ttu-id="df344-202">Alternatively, open Analytics from the icon on the Overview blade, and write your own queries, or try some of the sample queries on the Analytics Home tab.</span><span class="sxs-lookup"><span data-stu-id="df344-202">Alternatively, open Analytics from the icon on the Overview blade, and write your own queries, or try some of the sample queries on the Analytics Home tab.</span></span>


![Analytics window with generated query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-web-track-usage/open-analytics.png)

<span data-ttu-id="df344-204">[Learn more about the Azure Analytics query language](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="df344-204">[Learn more about the Azure Analytics query language](app-insights-analytics.md).</span></span>

<span data-ttu-id="df344-205">For usage analysis, you may be particularly interested in these tables:</span><span class="sxs-lookup"><span data-stu-id="df344-205">For usage analysis, you may be particularly interested in these tables:</span></span>

* <span data-ttu-id="df344-206">`customEvents` - Results of [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) calls.</span><span class="sxs-lookup"><span data-stu-id="df344-206">`customEvents` - Results of [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) calls.</span></span>
* <span data-ttu-id="df344-207">`pageViews` - Counts of pages opened in client browsers, or calls to [trackPageView()](app-insights-api-custom-events-metrics.md#page-views).</span><span class="sxs-lookup"><span data-stu-id="df344-207">`pageViews` - Counts of pages opened in client browsers, or calls to [trackPageView()](app-insights-api-custom-events-metrics.md#page-views).</span></span>


## <a name="a--b-testing"></a><span data-ttu-id="df344-208">A | B Testing</span><span class="sxs-lookup"><span data-stu-id="df344-208">A | B Testing</span></span>
<span data-ttu-id="df344-209">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span><span class="sxs-lookup"><span data-stu-id="df344-209">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="df344-210">Measure the success of each, and then move to a unified version.</span><span class="sxs-lookup"><span data-stu-id="df344-210">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="df344-211">For this technique, you attach distinct tags to all the telemetry that is sent by each version of your app.</span><span class="sxs-lookup"><span data-stu-id="df344-211">For this technique, you attach distinct tags to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="df344-212">You can do that by defining properties in the active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="df344-212">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="df344-213">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span><span class="sxs-lookup"><span data-stu-id="df344-213">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="df344-214">In the Application Insights portal, you'll then be able to filter and group (segment) your data on the tags, so as to compare the different versions.</span><span class="sxs-lookup"><span data-stu-id="df344-214">In the Application Insights portal, you'll then be able to filter and group (segment) your data on the tags, so as to compare the different versions.</span></span>


```C#

    using Microsoft.ApplicationInsights.DataContracts;

    var context = new TelemetryContext();
    context.Properties["Game"] = currentGame.Name;
    var telemetry = new TelemetryClient(context);
    // Now all telemetry will automatically be sent with the context property:
    telemetry.TrackEvent("WinGame");
```


```VB

    Dim context = New TelemetryContext
    context.Properties("Game") = currentGame.Name
    Dim telemetry = New TelemetryClient(context)
    ' Now all telemetry will automatically be sent with the context property:
    telemetry.TrackEvent("WinGame")
```

<span data-ttu-id="df344-215">Individual telemetry can override the default values.</span><span class="sxs-lookup"><span data-stu-id="df344-215">Individual telemetry can override the default values.</span></span>

<span data-ttu-id="df344-216">You can set up a universal initializer so that all new TelemetryClients automatically use your context.</span><span class="sxs-lookup"><span data-stu-id="df344-216">You can set up a universal initializer so that all new TelemetryClients automatically use your context.</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="df344-217">In the app initializer such as Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="df344-217">In the app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


## <a name="build---measure---learn"></a><span data-ttu-id="df344-218">Build - Measure - Learn</span><span class="sxs-lookup"><span data-stu-id="df344-218">Build - Measure - Learn</span></span>
<span data-ttu-id="df344-219">When you use analytics, it becomes an integrated part of your development cycle - not just something you think about to help solve problems.</span><span class="sxs-lookup"><span data-stu-id="df344-219">When you use analytics, it becomes an integrated part of your development cycle - not just something you think about to help solve problems.</span></span> <span data-ttu-id="df344-220">Here are some tips:</span><span class="sxs-lookup"><span data-stu-id="df344-220">Here are some tips:</span></span>

* <span data-ttu-id="df344-221">Determine the key metric of your application.</span><span class="sxs-lookup"><span data-stu-id="df344-221">Determine the key metric of your application.</span></span> <span data-ttu-id="df344-222">Do you want as many users as possible, or would you prefer a small set of very happy users?</span><span class="sxs-lookup"><span data-stu-id="df344-222">Do you want as many users as possible, or would you prefer a small set of very happy users?</span></span> <span data-ttu-id="df344-223">Do you want to maximize visits or sales?</span><span class="sxs-lookup"><span data-stu-id="df344-223">Do you want to maximize visits or sales?</span></span>
* <span data-ttu-id="df344-224">Plan to measure each story.</span><span class="sxs-lookup"><span data-stu-id="df344-224">Plan to measure each story.</span></span> <span data-ttu-id="df344-225">When you sketch a new user story or feature, or plan to update an existing one, always think about how you will measure the success of the change.</span><span class="sxs-lookup"><span data-stu-id="df344-225">When you sketch a new user story or feature, or plan to update an existing one, always think about how you will measure the success of the change.</span></span> <span data-ttu-id="df344-226">Before coding starts, ask "What effect will this have on our metrics, if it works?</span><span class="sxs-lookup"><span data-stu-id="df344-226">Before coding starts, ask "What effect will this have on our metrics, if it works?</span></span> <span data-ttu-id="df344-227">Should we track any new events?"</span><span class="sxs-lookup"><span data-stu-id="df344-227">Should we track any new events?"</span></span>
  <span data-ttu-id="df344-228">And of course, when the feature is live, make sure you look at the analytics and act on the results.</span><span class="sxs-lookup"><span data-stu-id="df344-228">And of course, when the feature is live, make sure you look at the analytics and act on the results.</span></span>
* <span data-ttu-id="df344-229">Relate other metrics to the key metric.</span><span class="sxs-lookup"><span data-stu-id="df344-229">Relate other metrics to the key metric.</span></span> <span data-ttu-id="df344-230">For example, if you add a 'favorites' feature, you'd like to know how often users add favorites.</span><span class="sxs-lookup"><span data-stu-id="df344-230">For example, if you add a 'favorites' feature, you'd like to know how often users add favorites.</span></span> <span data-ttu-id="df344-231">But it's perhaps more interesting to know how often they come back to their favorites.</span><span class="sxs-lookup"><span data-stu-id="df344-231">But it's perhaps more interesting to know how often they come back to their favorites.</span></span> <span data-ttu-id="df344-232">And, most importantly, do customers who use favorites ultimately buy more of your product?</span><span class="sxs-lookup"><span data-stu-id="df344-232">And, most importantly, do customers who use favorites ultimately buy more of your product?</span></span>
* <span data-ttu-id="df344-233">Canary testing.</span><span class="sxs-lookup"><span data-stu-id="df344-233">Canary testing.</span></span> <span data-ttu-id="df344-234">Set up a feature switch that allows you to make a new feature visible only to some users.</span><span class="sxs-lookup"><span data-stu-id="df344-234">Set up a feature switch that allows you to make a new feature visible only to some users.</span></span> <span data-ttu-id="df344-235">Use Application Insights to see whether the new feature is being used in the way you envisaged.</span><span class="sxs-lookup"><span data-stu-id="df344-235">Use Application Insights to see whether the new feature is being used in the way you envisaged.</span></span> <span data-ttu-id="df344-236">Make adjustments, then release it to a wider audience.</span><span class="sxs-lookup"><span data-stu-id="df344-236">Make adjustments, then release it to a wider audience.</span></span>
* <span data-ttu-id="df344-237">Talk to your users!</span><span class="sxs-lookup"><span data-stu-id="df344-237">Talk to your users!</span></span> <span data-ttu-id="df344-238">Analytics is not enough on its own, but complementary to maintaining a good customer relationship.</span><span class="sxs-lookup"><span data-stu-id="df344-238">Analytics is not enough on its own, but complementary to maintaining a good customer relationship.</span></span>

## <a name="learn-more"></a><span data-ttu-id="df344-239">Learn more</span><span class="sxs-lookup"><span data-stu-id="df344-239">Learn more</span></span>
* [<span data-ttu-id="df344-240">Detect, triage and diagnose crashes and performance issues in your app</span><span class="sxs-lookup"><span data-stu-id="df344-240">Detect, triage and diagnose crashes and performance issues in your app</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="df344-241">Get started with Application Insights on many platforms</span><span class="sxs-lookup"><span data-stu-id="df344-241">Get started with Application Insights on many platforms</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="df344-242">Using the API - overview</span><span class="sxs-lookup"><span data-stu-id="df344-242">Using the API - overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="df344-243">JavaScript API reference</span><span class="sxs-lookup"><span data-stu-id="df344-243">JavaScript API reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
















