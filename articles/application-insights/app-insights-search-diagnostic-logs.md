---
title: Logs & diagnostics for ASP.NET in Azure Application Insights | Microsoft Docs
description: Diagnose issues in ASP.NET web apps by searching requests, exceptions and logs generated with Trace, NLog, or Log4Net.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 99860c53-0324-4a3a-9aa9-83f5dffba835
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/08/2016
ms.author: awills
ms.openlocfilehash: 7369edc270f4ef706e409fde2c25c868fe1b31ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562917"
---
# <a name="logs-exceptions-and-custom-diagnostics-for-aspnet-in-application-insights"></a><span data-ttu-id="112e6-103">Logs, exceptions and custom diagnostics for ASP.NET in Application Insights</span><span class="sxs-lookup"><span data-stu-id="112e6-103">Logs, exceptions and custom diagnostics for ASP.NET in Application Insights</span></span>
<span data-ttu-id="112e6-104">[Application Insights][start] includes a powerful [Diagnostic Search][diagnostic] tool that enables you to explore and drill in to telemetry sent by the Application Insights SDK from your application.</span><span class="sxs-lookup"><span data-stu-id="112e6-104">[Application Insights][start] includes a powerful [Diagnostic Search][diagnostic] tool that enables you to explore and drill in to telemetry sent by the Application Insights SDK from your application.</span></span> <span data-ttu-id="112e6-105">Many events such as user page views are automatically sent by the SDK.</span><span class="sxs-lookup"><span data-stu-id="112e6-105">Many events such as user page views are automatically sent by the SDK.</span></span>

<span data-ttu-id="112e6-106">You can also write code to send custom events, exception reports, and traces.</span><span class="sxs-lookup"><span data-stu-id="112e6-106">You can also write code to send custom events, exception reports, and traces.</span></span> <span data-ttu-id="112e6-107">And if you already use a logging framework such as log4J, log4net, NLog, or System.Diagnostics.Trace, you can capture those logs and include them in the search.</span><span class="sxs-lookup"><span data-stu-id="112e6-107">And if you already use a logging framework such as log4J, log4net, NLog, or System.Diagnostics.Trace, you can capture those logs and include them in the search.</span></span> <span data-ttu-id="112e6-108">This makes it easy to correlate log traces with user actions, exceptions and other events.</span><span class="sxs-lookup"><span data-stu-id="112e6-108">This makes it easy to correlate log traces with user actions, exceptions and other events.</span></span>

## <a name="send"></a><span data-ttu-id="112e6-109">Before you write custom telemetry</span><span class="sxs-lookup"><span data-stu-id="112e6-109">Before you write custom telemetry</span></span>
<span data-ttu-id="112e6-110">If you haven't yet [set up Application Insights for your project][start], do that now.</span><span class="sxs-lookup"><span data-stu-id="112e6-110">If you haven't yet [set up Application Insights for your project][start], do that now.</span></span>

<span data-ttu-id="112e6-111">When you run your application, it will send some telemetry that will show up in Diagnostic Search, including requests received by the server, page views logged at the client, and uncaught exceptions.</span><span class="sxs-lookup"><span data-stu-id="112e6-111">When you run your application, it will send some telemetry that will show up in Diagnostic Search, including requests received by the server, page views logged at the client, and uncaught exceptions.</span></span>

<span data-ttu-id="112e6-112">Open Diagnostic Search to see the telemetry that the SDK automatically sends.</span><span class="sxs-lookup"><span data-stu-id="112e6-112">Open Diagnostic Search to see the telemetry that the SDK automatically sends.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-45diagnostic.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-31search.png)

<span data-ttu-id="112e6-113">The details vary from one application type to another.</span><span class="sxs-lookup"><span data-stu-id="112e6-113">The details vary from one application type to another.</span></span> <span data-ttu-id="112e6-114">You can click through any individual event to get more detail.</span><span class="sxs-lookup"><span data-stu-id="112e6-114">You can click through any individual event to get more detail.</span></span>

## <a name="sampling"></a><span data-ttu-id="112e6-115">Sampling</span><span class="sxs-lookup"><span data-stu-id="112e6-115">Sampling</span></span>
<span data-ttu-id="112e6-116">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="112e6-116">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="112e6-117">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="112e6-117">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <a name="events"></a><span data-ttu-id="112e6-118">Custom events</span><span class="sxs-lookup"><span data-stu-id="112e6-118">Custom events</span></span>
<span data-ttu-id="112e6-119">Custom events show up both in [Diagnostic Search][diagnostic] and in [Metric Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="112e6-119">Custom events show up both in [Diagnostic Search][diagnostic] and in [Metric Explorer][metrics].</span></span> <span data-ttu-id="112e6-120">You can send them from devices, web pages and server applications.</span><span class="sxs-lookup"><span data-stu-id="112e6-120">You can send them from devices, web pages and server applications.</span></span> <span data-ttu-id="112e6-121">They can be used both for diagnostic purposes and to [understand usage patterns][track].</span><span class="sxs-lookup"><span data-stu-id="112e6-121">They can be used both for diagnostic purposes and to [understand usage patterns][track].</span></span>

<span data-ttu-id="112e6-122">A custom event has a name, and can also carry properties that you can filter on, together with numeric measurements.</span><span class="sxs-lookup"><span data-stu-id="112e6-122">A custom event has a name, and can also carry properties that you can filter on, together with numeric measurements.</span></span>

<span data-ttu-id="112e6-123">JavaScript at client</span><span class="sxs-lookup"><span data-stu-id="112e6-123">JavaScript at client</span></span>

    appInsights.trackEvent("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric measurements:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

<span data-ttu-id="112e6-124">C# at server</span><span class="sxs-lookup"><span data-stu-id="112e6-124">C# at server</span></span>

    // Set up some properties:
    var properties = new Dictionary <string, string> 
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var measurements = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, measurements);


<span data-ttu-id="112e6-125">VB at server</span><span class="sxs-lookup"><span data-stu-id="112e6-125">VB at server</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim measurements = New Dictionary (Of String, Double)
    measurements.Add("Score", currentGame.Score)
    measurements.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, measurements)

### <a name="run-your-app-and-view-the-results"></a><span data-ttu-id="112e6-126">Run your app and view the results.</span><span class="sxs-lookup"><span data-stu-id="112e6-126">Run your app and view the results.</span></span>
<span data-ttu-id="112e6-127">Open Diagnostic Search.</span><span class="sxs-lookup"><span data-stu-id="112e6-127">Open Diagnostic Search.</span></span>

<span data-ttu-id="112e6-128">Select Custom Event and select a particular event name.</span><span class="sxs-lookup"><span data-stu-id="112e6-128">Select Custom Event and select a particular event name.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-332filterCustom.png)

<span data-ttu-id="112e6-129">Filter the data more by entering a search term on a property value.</span><span class="sxs-lookup"><span data-stu-id="112e6-129">Filter the data more by entering a search term on a property value.</span></span>  

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-23-customevents-5.png)

<span data-ttu-id="112e6-130">Drill into an individual event to see its detailed properties.</span><span class="sxs-lookup"><span data-stu-id="112e6-130">Drill into an individual event to see its detailed properties.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-23-customevents-4.png)

## <a name="pages"></a> <span data-ttu-id="112e6-131">Page views</span><span class="sxs-lookup"><span data-stu-id="112e6-131">Page views</span></span>
<span data-ttu-id="112e6-132">Page view telemetry is sent by the trackPageView() call in [the JavaScript snippet you insert in your web pages][usage].</span><span class="sxs-lookup"><span data-stu-id="112e6-132">Page view telemetry is sent by the trackPageView() call in [the JavaScript snippet you insert in your web pages][usage].</span></span> <span data-ttu-id="112e6-133">Its main purpose is to contribute to the counts of page views that you see on the overview page.</span><span class="sxs-lookup"><span data-stu-id="112e6-133">Its main purpose is to contribute to the counts of page views that you see on the overview page.</span></span>

<span data-ttu-id="112e6-134">Usually it is called once in each HTML page, but you can insert more calls - for example, if you have a single-page app and you want to log a new page whenever the user gets more data.</span><span class="sxs-lookup"><span data-stu-id="112e6-134">Usually it is called once in each HTML page, but you can insert more calls - for example, if you have a single-page app and you want to log a new page whenever the user gets more data.</span></span>

    appInsights.trackPageView(pageSegmentName, "http://fabrikam.com/page.htm"); 

<span data-ttu-id="112e6-135">It's sometimes useful to attach properties that you can use as filters in diagnostic search:</span><span class="sxs-lookup"><span data-stu-id="112e6-135">It's sometimes useful to attach properties that you can use as filters in diagnostic search:</span></span>

    appInsights.trackPageView(pageSegmentName, "http://fabrikam.com/page.htm",
     {Game: currentGame.name, Difficulty: currentGame.difficulty});


## <a name="trace"></a> <span data-ttu-id="112e6-136">Trace telemetry</span><span class="sxs-lookup"><span data-stu-id="112e6-136">Trace telemetry</span></span>
<span data-ttu-id="112e6-137">Trace telemetry is code that you insert specifically to create diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="112e6-137">Trace telemetry is code that you insert specifically to create diagnostic logs.</span></span> 

<span data-ttu-id="112e6-138">For example, you could insert calls like this:</span><span class="sxs-lookup"><span data-stu-id="112e6-138">For example, you could insert calls like this:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");


#### <a name="install-an-adapter-for-your-logging-framework"></a><span data-ttu-id="112e6-139">Install an adapter for your logging framework</span><span class="sxs-lookup"><span data-stu-id="112e6-139">Install an adapter for your logging framework</span></span>
<span data-ttu-id="112e6-140">You can also search logs generated with a logging framework - log4Net, NLog or System.Diagnostics.Trace.</span><span class="sxs-lookup"><span data-stu-id="112e6-140">You can also search logs generated with a logging framework - log4Net, NLog or System.Diagnostics.Trace.</span></span> 

1. <span data-ttu-id="112e6-141">If you plan to use log4Net or NLog, install it in your project.</span><span class="sxs-lookup"><span data-stu-id="112e6-141">If you plan to use log4Net or NLog, install it in your project.</span></span> 
2. <span data-ttu-id="112e6-142">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="112e6-142">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="112e6-143">Select Online > All, select **Include Prerelease** and search for "Microsoft.ApplicationInsights"</span><span class="sxs-lookup"><span data-stu-id="112e6-143">Select Online > All, select **Include Prerelease** and search for "Microsoft.ApplicationInsights"</span></span>
   
    ![Get the prerelease version of the appropriate adapter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-36nuget.png)
4. <span data-ttu-id="112e6-145">Select the appropriate package - one of:</span><span class="sxs-lookup"><span data-stu-id="112e6-145">Select the appropriate package - one of:</span></span>
   
   * <span data-ttu-id="112e6-146">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span><span class="sxs-lookup"><span data-stu-id="112e6-146">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="112e6-147">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="112e6-147">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="112e6-148">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="112e6-148">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="112e6-149">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span><span class="sxs-lookup"><span data-stu-id="112e6-149">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

#### <a name="pepper"></a><span data-ttu-id="112e6-150">Insert diagnostic log calls</span><span class="sxs-lookup"><span data-stu-id="112e6-150">Insert diagnostic log calls</span></span>
<span data-ttu-id="112e6-151">If you use System.Diagnostics.Trace, a typical call would be:</span><span class="sxs-lookup"><span data-stu-id="112e6-151">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="112e6-152">If you prefer log4net or NLog:</span><span class="sxs-lookup"><span data-stu-id="112e6-152">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

<span data-ttu-id="112e6-153">Run your app in debug mode, or deploy it.</span><span class="sxs-lookup"><span data-stu-id="112e6-153">Run your app in debug mode, or deploy it.</span></span>

<span data-ttu-id="112e6-154">You'll see the messages in Diagnostic Search when you select the Trace filter.</span><span class="sxs-lookup"><span data-stu-id="112e6-154">You'll see the messages in Diagnostic Search when you select the Trace filter.</span></span>

### <a name="exceptions"></a><span data-ttu-id="112e6-155">Exceptions</span><span class="sxs-lookup"><span data-stu-id="112e6-155">Exceptions</span></span>
<span data-ttu-id="112e6-156">Getting exception reports in Application Insights provides a very powerful experience, especially since you can navigate between the failed requests and the exceptions, and read the exception stack.</span><span class="sxs-lookup"><span data-stu-id="112e6-156">Getting exception reports in Application Insights provides a very powerful experience, especially since you can navigate between the failed requests and the exceptions, and read the exception stack.</span></span>

<span data-ttu-id="112e6-157">In some cases, you need to [insert a few lines of code][exceptions] to make sure your exceptions are being caught automatically.</span><span class="sxs-lookup"><span data-stu-id="112e6-157">In some cases, you need to [insert a few lines of code][exceptions] to make sure your exceptions are being caught automatically.</span></span>

<span data-ttu-id="112e6-158">You can also write explicit code to send exception telemetry:</span><span class="sxs-lookup"><span data-stu-id="112e6-158">You can also write explicit code to send exception telemetry:</span></span>

<span data-ttu-id="112e6-159">JavaScript</span><span class="sxs-lookup"><span data-stu-id="112e6-159">JavaScript</span></span>

    try 
    { ...
    }
    catch (ex)
    {
      appInsights.TrackException(ex, "handler loc",
        {Game: currentGame.Name, 
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="112e6-160">C#</span><span class="sxs-lookup"><span data-stu-id="112e6-160">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try 
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string> 
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="112e6-161">VB</span><span class="sxs-lookup"><span data-stu-id="112e6-161">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="112e6-162">The properties and measurements parameters are optional, but are useful for filtering and adding extra information.</span><span class="sxs-lookup"><span data-stu-id="112e6-162">The properties and measurements parameters are optional, but are useful for filtering and adding extra information.</span></span> <span data-ttu-id="112e6-163">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span><span class="sxs-lookup"><span data-stu-id="112e6-163">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="112e6-164">You can add as many items as you like to each dictionary.</span><span class="sxs-lookup"><span data-stu-id="112e6-164">You can add as many items as you like to each dictionary.</span></span>

#### <a name="viewing-exceptions"></a><span data-ttu-id="112e6-165">Viewing exceptions</span><span class="sxs-lookup"><span data-stu-id="112e6-165">Viewing exceptions</span></span>
<span data-ttu-id="112e6-166">You'll see a summary of exceptions reported on the Overview blade, and you can click through to see more details.</span><span class="sxs-lookup"><span data-stu-id="112e6-166">You'll see a summary of exceptions reported on the Overview blade, and you can click through to see more details.</span></span> <span data-ttu-id="112e6-167">For example:</span><span class="sxs-lookup"><span data-stu-id="112e6-167">For example:</span></span>

<span data-ttu-id="112e6-168">![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-039-1exceptions.png)[]</span><span class="sxs-lookup"><span data-stu-id="112e6-168">![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-039-1exceptions.png)[]</span></span>

<span data-ttu-id="112e6-169">Click on any exception type to see specific occurrences:</span><span class="sxs-lookup"><span data-stu-id="112e6-169">Click on any exception type to see specific occurrences:</span></span>

<span data-ttu-id="112e6-170">![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-333facets.png)[]</span><span class="sxs-lookup"><span data-stu-id="112e6-170">![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-search-diagnostic-logs/appinsights-333facets.png)[]</span></span>

<span data-ttu-id="112e6-171">You can also open Diagnostic Search directly, filter on exceptions, and choose the exception type that you want to see.</span><span class="sxs-lookup"><span data-stu-id="112e6-171">You can also open Diagnostic Search directly, filter on exceptions, and choose the exception type that you want to see.</span></span>

### <a name="reporting-unhandled-exceptions"></a><span data-ttu-id="112e6-172">Reporting unhandled exceptions</span><span class="sxs-lookup"><span data-stu-id="112e6-172">Reporting unhandled exceptions</span></span>
<span data-ttu-id="112e6-173">Application Insights reports unhandled exceptions where it can, from devices, [web browsers][usage], or web servers, whether instrumented by [Status Monitor][redfield] or [Application Insights SDK][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="112e6-173">Application Insights reports unhandled exceptions where it can, from devices, [web browsers][usage], or web servers, whether instrumented by [Status Monitor][redfield] or [Application Insights SDK][greenbrown].</span></span> 

<span data-ttu-id="112e6-174">However, it isn't always able to do this in some cases because the .NET framework catches the exceptions.</span><span class="sxs-lookup"><span data-stu-id="112e6-174">However, it isn't always able to do this in some cases because the .NET framework catches the exceptions.</span></span>  <span data-ttu-id="112e6-175">To make sure you see all exceptions, you therefore have to write a small exception handler.</span><span class="sxs-lookup"><span data-stu-id="112e6-175">To make sure you see all exceptions, you therefore have to write a small exception handler.</span></span> <span data-ttu-id="112e6-176">The best procedure varies with the technology.</span><span class="sxs-lookup"><span data-stu-id="112e6-176">The best procedure varies with the technology.</span></span> <span data-ttu-id="112e6-177">See [Exception telemetry for ASP.NET][exceptions] for details.</span><span class="sxs-lookup"><span data-stu-id="112e6-177">See [Exception telemetry for ASP.NET][exceptions] for details.</span></span> 

### <a name="correlating-with-a-build"></a><span data-ttu-id="112e6-178">Correlating with a build</span><span class="sxs-lookup"><span data-stu-id="112e6-178">Correlating with a build</span></span>
<span data-ttu-id="112e6-179">When you read diagnostic logs, it's likely that your source code will have changed since the live code was deployed.</span><span class="sxs-lookup"><span data-stu-id="112e6-179">When you read diagnostic logs, it's likely that your source code will have changed since the live code was deployed.</span></span>

<span data-ttu-id="112e6-180">It's therefore useful to put build information, such as the URL of the current version, into a property along with each exception or trace.</span><span class="sxs-lookup"><span data-stu-id="112e6-180">It's therefore useful to put build information, such as the URL of the current version, into a property along with each exception or trace.</span></span> 

<span data-ttu-id="112e6-181">Instead of adding the property separately to every exception call, you can set the information in the default context.</span><span class="sxs-lookup"><span data-stu-id="112e6-181">Instead of adding the property separately to every exception call, you can set the information in the default context.</span></span> 

    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }

<span data-ttu-id="112e6-182">In the app initializer such as Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="112e6-182">In the app initializer such as Global.asax.cs:</span></span>

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }

### <a name="requests"></a> <span data-ttu-id="112e6-183">Server Web Requests</span><span class="sxs-lookup"><span data-stu-id="112e6-183">Server Web Requests</span></span>
<span data-ttu-id="112e6-184">Request telemetry is sent automatically when you [install Status Monitor on your web server][redfield], or when you [add Application Insights to your web project][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="112e6-184">Request telemetry is sent automatically when you [install Status Monitor on your web server][redfield], or when you [add Application Insights to your web project][greenbrown].</span></span> <span data-ttu-id="112e6-185">It also feeds into the request and response time charts in Metric Explorer and on the Overview page.</span><span class="sxs-lookup"><span data-stu-id="112e6-185">It also feeds into the request and response time charts in Metric Explorer and on the Overview page.</span></span>

<span data-ttu-id="112e6-186">If you want to send additional events, you can use the TrackRequest() API.</span><span class="sxs-lookup"><span data-stu-id="112e6-186">If you want to send additional events, you can use the TrackRequest() API.</span></span>

## <a name="questions"></a><span data-ttu-id="112e6-187">Q & A</span><span class="sxs-lookup"><span data-stu-id="112e6-187">Q & A</span></span>
### <a name="emptykey"></a><span data-ttu-id="112e6-188">I get an error "Instrumentation key cannot be empty"</span><span class="sxs-lookup"><span data-stu-id="112e6-188">I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="112e6-189">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span><span class="sxs-lookup"><span data-stu-id="112e6-189">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="112e6-190">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="112e6-190">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="112e6-191">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span><span class="sxs-lookup"><span data-stu-id="112e6-191">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="112e6-192">That should fix it.</span><span class="sxs-lookup"><span data-stu-id="112e6-192">That should fix it.</span></span>

### <a name="limits"></a><span data-ttu-id="112e6-193">How much data is retained?</span><span class="sxs-lookup"><span data-stu-id="112e6-193">How much data is retained?</span></span>
<span data-ttu-id="112e6-194">Up to 500 events per second from each application.</span><span class="sxs-lookup"><span data-stu-id="112e6-194">Up to 500 events per second from each application.</span></span> <span data-ttu-id="112e6-195">Events are retained for seven days.</span><span class="sxs-lookup"><span data-stu-id="112e6-195">Events are retained for seven days.</span></span>

### <a name="some-of-my-events-or-traces-dont-appear"></a><span data-ttu-id="112e6-196">Some of my events or traces don't appear</span><span class="sxs-lookup"><span data-stu-id="112e6-196">Some of my events or traces don't appear</span></span>
<span data-ttu-id="112e6-197">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="112e6-197">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="112e6-198">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="112e6-198">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <a name="add"></a><span data-ttu-id="112e6-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="112e6-199">Next steps</span></span>
* <span data-ttu-id="112e6-200">[Set up availability and responsiveness tests][availability]</span><span class="sxs-lookup"><span data-stu-id="112e6-200">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="112e6-201">[Troubleshooting][qna]</span><span class="sxs-lookup"><span data-stu-id="112e6-201">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[greenbrown]: app-insights-asp-net.md
[metrics]: app-insights-metrics-explorer.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md










