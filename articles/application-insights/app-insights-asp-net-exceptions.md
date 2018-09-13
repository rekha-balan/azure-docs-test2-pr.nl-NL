---
title: Diagnose failures and exceptions in web apps with Azure Application Insights | Microsoft Docs
description: Capture exceptions from ASP.NET apps along with request telemetry.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 09/19/2017
ms.author: mbullwin
ms.openlocfilehash: a3dcf4211df5d40c4b174fd9a818d3268ffaa3a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830518"
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="203f8-103">Diagnose exceptions in your web apps with Application Insights</span><span class="sxs-lookup"><span data-stu-id="203f8-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="203f8-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="203f8-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="203f8-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span><span class="sxs-lookup"><span data-stu-id="203f8-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="203f8-106">Set up exception reporting</span><span class="sxs-lookup"><span data-stu-id="203f8-106">Set up exception reporting</span></span>
* <span data-ttu-id="203f8-107">To have exceptions reported from your server app:</span><span class="sxs-lookup"><span data-stu-id="203f8-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="203f8-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span><span class="sxs-lookup"><span data-stu-id="203f8-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="203f8-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span><span class="sxs-lookup"><span data-stu-id="203f8-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="203f8-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="203f8-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="203f8-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="203f8-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="203f8-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="203f8-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span><span class="sxs-lookup"><span data-stu-id="203f8-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="203f8-114">Web forms</span><span class="sxs-lookup"><span data-stu-id="203f8-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="203f8-115">MVC</span><span class="sxs-lookup"><span data-stu-id="203f8-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="203f8-116">Web API 1.\*</span><span class="sxs-lookup"><span data-stu-id="203f8-116">Web API 1.\*</span></span>](#web-api-1x)
  * [<span data-ttu-id="203f8-117">Web API 2.\*</span><span class="sxs-lookup"><span data-stu-id="203f8-117">Web API 2.\*</span></span>](#web-api-2x)
  * [<span data-ttu-id="203f8-118">WCF</span><span class="sxs-lookup"><span data-stu-id="203f8-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="203f8-119">Diagnosing exceptions using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="203f8-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="203f8-120">Open the app solution in Visual Studio to help with debugging.</span><span class="sxs-lookup"><span data-stu-id="203f8-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="203f8-121">Run the app, either on your server or on your development machine by using F5.</span><span class="sxs-lookup"><span data-stu-id="203f8-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="203f8-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span><span class="sxs-lookup"><span data-stu-id="203f8-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="203f8-123">While you're debugging, you can do this just by clicking the Application Insights button.</span><span class="sxs-lookup"><span data-stu-id="203f8-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Right-click the project and choose Application Insights, Open.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="203f8-125">Notice that you can filter the report to show just exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="203f8-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="203f8-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="203f8-127">Click an exception report to show its stack trace.</span><span class="sxs-lookup"><span data-stu-id="203f8-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="203f8-128">Click a line reference in the stack trace, to open the relevant code file.</span><span class="sxs-lookup"><span data-stu-id="203f8-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="203f8-129">In the code, notice that CodeLens shows data about the exceptions:</span><span class="sxs-lookup"><span data-stu-id="203f8-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![CodeLens notification of exceptions.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="203f8-131">Diagnosing failures using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="203f8-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="203f8-132">Application Insights comes with a curated APM experience to help you diagnose failures in your monitored applications.</span><span class="sxs-lookup"><span data-stu-id="203f8-132">Application Insights comes with a curated APM experience to help you diagnose failures in your monitored applications.</span></span> <span data-ttu-id="203f8-133">To start, click on the Failures option in the Application Insights resource menu located in the Investigate section.</span><span class="sxs-lookup"><span data-stu-id="203f8-133">To start, click on the Failures option in the Application Insights resource menu located in the Investigate section.</span></span> <span data-ttu-id="203f8-134">You should see a full-screen view that shows you the failure rate trends for your requests, how many of them are failing, and how many users are impacted.</span><span class="sxs-lookup"><span data-stu-id="203f8-134">You should see a full-screen view that shows you the failure rate trends for your requests, how many of them are failing, and how many users are impacted.</span></span> <span data-ttu-id="203f8-135">On the right you'll see some of the most useful distributions specific to the selected failing operation, including top 3 response codes, top 3 exception types, and top 3 failing dependency types.</span><span class="sxs-lookup"><span data-stu-id="203f8-135">On the right you'll see some of the most useful distributions specific to the selected failing operation, including top 3 response codes, top 3 exception types, and top 3 failing dependency types.</span></span> 

![Failures triage view (operations tab)](./media/app-insights-asp-net-exceptions/FailuresTriageView.png)

<span data-ttu-id="203f8-137">In a single click you can then review representative samples for each of these subsets of operations.</span><span class="sxs-lookup"><span data-stu-id="203f8-137">In a single click you can then review representative samples for each of these subsets of operations.</span></span> <span data-ttu-id="203f8-138">In particular, to diagnose exceptions, you can click on the count of a particular exception to be presented with an Exceptions details blade, such as this one:</span><span class="sxs-lookup"><span data-stu-id="203f8-138">In particular, to diagnose exceptions, you can click on the count of a particular exception to be presented with an Exceptions details blade, such as this one:</span></span>

![Exception details blade](./media/app-insights-asp-net-exceptions/ExceptionDetailsBlade.png)

<span data-ttu-id="203f8-140">**Alternatively,** instead of looking at exceptions of a specific failing operation, you can start from the overall view of exceptions, by switching to the Exceptions tab:</span><span class="sxs-lookup"><span data-stu-id="203f8-140">**Alternatively,** instead of looking at exceptions of a specific failing operation, you can start from the overall view of exceptions, by switching to the Exceptions tab:</span></span>

![Failures triage view (exceptions tab)](./media/app-insights-asp-net-exceptions/FailuresTriageView_Exceptions.png)

<span data-ttu-id="203f8-142">Here you can see all the exceptions collected for your monitored app.</span><span class="sxs-lookup"><span data-stu-id="203f8-142">Here you can see all the exceptions collected for your monitored app.</span></span>

<span data-ttu-id="203f8-143">*No exceptions showing? See [Capture exceptions](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="203f8-143">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="203f8-144">Custom tracing and log data</span><span class="sxs-lookup"><span data-stu-id="203f8-144">Custom tracing and log data</span></span>
<span data-ttu-id="203f8-145">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span><span class="sxs-lookup"><span data-stu-id="203f8-145">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="203f8-146">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span><span class="sxs-lookup"><span data-stu-id="203f8-146">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="203f8-147">You have several options:</span><span class="sxs-lookup"><span data-stu-id="203f8-147">You have several options:</span></span>

* <span data-ttu-id="203f8-148">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span><span class="sxs-lookup"><span data-stu-id="203f8-148">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="203f8-149">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="203f8-149">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="203f8-150">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span><span class="sxs-lookup"><span data-stu-id="203f8-150">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="203f8-151">[TrackException()](#exceptions) sends stack traces.</span><span class="sxs-lookup"><span data-stu-id="203f8-151">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="203f8-152">[More about exceptions](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="203f8-152">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="203f8-153">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span><span class="sxs-lookup"><span data-stu-id="203f8-153">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="203f8-154">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span><span class="sxs-lookup"><span data-stu-id="203f8-154">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drill through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="203f8-156">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span><span class="sxs-lookup"><span data-stu-id="203f8-156">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="203f8-157">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span><span class="sxs-lookup"><span data-stu-id="203f8-157">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="203f8-158">Learn about sampling.</span><span class="sxs-lookup"><span data-stu-id="203f8-158">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="203f8-159">How to see request POST data</span><span class="sxs-lookup"><span data-stu-id="203f8-159">How to see request POST data</span></span>
<span data-ttu-id="203f8-160">Request details don't include the data sent to your app in a POST call.</span><span class="sxs-lookup"><span data-stu-id="203f8-160">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="203f8-161">To have this data reported:</span><span class="sxs-lookup"><span data-stu-id="203f8-161">To have this data reported:</span></span>

* <span data-ttu-id="203f8-162">[Install the SDK](app-insights-asp-net.md) in your application project.</span><span class="sxs-lookup"><span data-stu-id="203f8-162">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="203f8-163">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="203f8-163">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="203f8-164">Send the POST data in the message parameter.</span><span class="sxs-lookup"><span data-stu-id="203f8-164">Send the POST data in the message parameter.</span></span> <span data-ttu-id="203f8-165">There is a limit to the permitted size, so you should try to send just the essential data.</span><span class="sxs-lookup"><span data-stu-id="203f8-165">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="203f8-166">When you investigate a failed request, find the associated traces.</span><span class="sxs-lookup"><span data-stu-id="203f8-166">When you investigate a failed request, find the associated traces.</span></span>  

![Drill through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> <span data-ttu-id="203f8-168">Capturing exceptions and related diagnostic data</span><span class="sxs-lookup"><span data-stu-id="203f8-168">Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="203f8-169">At first, you won't see in the portal all the exceptions that cause failures in your app.</span><span class="sxs-lookup"><span data-stu-id="203f8-169">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="203f8-170">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span><span class="sxs-lookup"><span data-stu-id="203f8-170">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="203f8-171">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span><span class="sxs-lookup"><span data-stu-id="203f8-171">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="203f8-172">You can:</span><span class="sxs-lookup"><span data-stu-id="203f8-172">You can:</span></span>

* <span data-ttu-id="203f8-173">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-173">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="203f8-174">**Capture exceptions automatically** by configuring your ASP.NET framework.</span><span class="sxs-lookup"><span data-stu-id="203f8-174">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="203f8-175">The necessary additions are different for different types of framework.</span><span class="sxs-lookup"><span data-stu-id="203f8-175">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="203f8-176">Reporting exceptions explicitly</span><span class="sxs-lookup"><span data-stu-id="203f8-176">Reporting exceptions explicitly</span></span>
<span data-ttu-id="203f8-177">The simplest way is to insert a call to TrackException() in an exception handler.</span><span class="sxs-lookup"><span data-stu-id="203f8-177">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

```javascript
    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }
```

```csharp
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
```

```VB
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
```

<span data-ttu-id="203f8-178">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span><span class="sxs-lookup"><span data-stu-id="203f8-178">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="203f8-179">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span><span class="sxs-lookup"><span data-stu-id="203f8-179">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="203f8-180">You can add as many items as you like to each dictionary.</span><span class="sxs-lookup"><span data-stu-id="203f8-180">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="203f8-181">Browser exceptions</span><span class="sxs-lookup"><span data-stu-id="203f8-181">Browser exceptions</span></span>
<span data-ttu-id="203f8-182">Most browser exceptions are reported.</span><span class="sxs-lookup"><span data-stu-id="203f8-182">Most browser exceptions are reported.</span></span>

<span data-ttu-id="203f8-183">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="203f8-183">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="203f8-184">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span><span class="sxs-lookup"><span data-stu-id="203f8-184">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="203f8-185">Web forms</span><span class="sxs-lookup"><span data-stu-id="203f8-185">Web forms</span></span>
<span data-ttu-id="203f8-186">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="203f8-186">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="203f8-187">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="203f8-187">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="203f8-188">(Add a Global.asax file if you don't already have one.)</span><span class="sxs-lookup"><span data-stu-id="203f8-188">(Add a Global.asax file if you don't already have one.)</span></span>

```csharp
    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }
```

## <a name="mvc"></a><span data-ttu-id="203f8-189">MVC</span><span class="sxs-lookup"><span data-stu-id="203f8-189">MVC</span></span>
<span data-ttu-id="203f8-190">Starting with Application Insights Web SDK version 2.6 (beta3 and later), Application Insights collects unhandled exceptions thrown in the MVC 5+ controllers methods automatically.</span><span class="sxs-lookup"><span data-stu-id="203f8-190">Starting with Application Insights Web SDK version 2.6 (beta3 and later), Application Insights collects unhandled exceptions thrown in the MVC 5+ controllers methods automatically.</span></span> <span data-ttu-id="203f8-191">If you have previously added a custom handler to track such exceptions (as described in following examples), you may remove it to prevent double tracking of exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-191">If you have previously added a custom handler to track such exceptions (as described in following examples), you may remove it to prevent double tracking of exceptions.</span></span>

<span data-ttu-id="203f8-192">There are a number of cases that the exception filters cannot handle.</span><span class="sxs-lookup"><span data-stu-id="203f8-192">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="203f8-193">For example:</span><span class="sxs-lookup"><span data-stu-id="203f8-193">For example:</span></span>

* <span data-ttu-id="203f8-194">Exceptions thrown from controller constructors.</span><span class="sxs-lookup"><span data-stu-id="203f8-194">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="203f8-195">Exceptions thrown from message handlers.</span><span class="sxs-lookup"><span data-stu-id="203f8-195">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="203f8-196">Exceptions thrown during routing.</span><span class="sxs-lookup"><span data-stu-id="203f8-196">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="203f8-197">Exceptions thrown during response content serialization.</span><span class="sxs-lookup"><span data-stu-id="203f8-197">Exceptions thrown during response content serialization.</span></span>
* <span data-ttu-id="203f8-198">Exception thrown during application start-up.</span><span class="sxs-lookup"><span data-stu-id="203f8-198">Exception thrown during application start-up.</span></span>
* <span data-ttu-id="203f8-199">Exception thrown in background tasks.</span><span class="sxs-lookup"><span data-stu-id="203f8-199">Exception thrown in background tasks.</span></span>

<span data-ttu-id="203f8-200">All exceptions *handled* by application still need to be tracked manually.</span><span class="sxs-lookup"><span data-stu-id="203f8-200">All exceptions *handled* by application still need to be tracked manually.</span></span> <span data-ttu-id="203f8-201">Unhandled exceptions originating from controllers typically result in 500 "Internal Server Error" response.</span><span class="sxs-lookup"><span data-stu-id="203f8-201">Unhandled exceptions originating from controllers typically result in 500 "Internal Server Error" response.</span></span> <span data-ttu-id="203f8-202">If such response is manually constructed as a result of handled exception (or no exception at all) it is tracked in corresponding request telemetry with `ResultCode` 500, however Application Insights SDK is unable to track corresponding exception.</span><span class="sxs-lookup"><span data-stu-id="203f8-202">If such response is manually constructed as a result of handled exception (or no exception at all) it is tracked in corresponding request telemetry with `ResultCode` 500, however Application Insights SDK is unable to track corresponding exception.</span></span>

### <a name="prior-versions-support"></a><span data-ttu-id="203f8-203">Prior versions support</span><span class="sxs-lookup"><span data-stu-id="203f8-203">Prior versions support</span></span>
<span data-ttu-id="203f8-204">If you use MVC 4 (and prior) of Application Insights Web SDK 2.5 (and prior), refer to the following examples to track exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-204">If you use MVC 4 (and prior) of Application Insights Web SDK 2.5 (and prior), refer to the following examples to track exceptions.</span></span>

<span data-ttu-id="203f8-205">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span><span class="sxs-lookup"><span data-stu-id="203f8-205">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="203f8-206">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span><span class="sxs-lookup"><span data-stu-id="203f8-206">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="203f8-207">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="203f8-207">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

```csharp
    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }
```

#### <a name="mvc-2"></a><span data-ttu-id="203f8-208">MVC 2</span><span class="sxs-lookup"><span data-stu-id="203f8-208">MVC 2</span></span>
<span data-ttu-id="203f8-209">Replace the HandleError attribute with your new attribute in your controllers.</span><span class="sxs-lookup"><span data-stu-id="203f8-209">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

```csharp
    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...
```

[<span data-ttu-id="203f8-210">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-210">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="203f8-211">MVC 3</span><span class="sxs-lookup"><span data-stu-id="203f8-211">MVC 3</span></span>
<span data-ttu-id="203f8-212">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="203f8-212">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

```csharp
    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...
```

[<span data-ttu-id="203f8-213">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-213">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="203f8-214">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="203f8-214">MVC 4, MVC5</span></span>
<span data-ttu-id="203f8-215">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="203f8-215">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

```csharp
    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }
```

[<span data-ttu-id="203f8-216">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-216">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api"></a><span data-ttu-id="203f8-217">Web API</span><span class="sxs-lookup"><span data-stu-id="203f8-217">Web API</span></span>
<span data-ttu-id="203f8-218">Starting with Application Insights Web SDK version 2.6 (beta3 and later), Application Insights collects unhandled exceptions thrown in the controller methods automatically for WebAPI 2+.</span><span class="sxs-lookup"><span data-stu-id="203f8-218">Starting with Application Insights Web SDK version 2.6 (beta3 and later), Application Insights collects unhandled exceptions thrown in the controller methods automatically for WebAPI 2+.</span></span> <span data-ttu-id="203f8-219">If you have previously added a custom handler to track such exceptions (as described in following examples), you may remove it to prevent double tracking of exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-219">If you have previously added a custom handler to track such exceptions (as described in following examples), you may remove it to prevent double tracking of exceptions.</span></span>

<span data-ttu-id="203f8-220">There are a number of cases that the exception filters cannot handle.</span><span class="sxs-lookup"><span data-stu-id="203f8-220">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="203f8-221">For example:</span><span class="sxs-lookup"><span data-stu-id="203f8-221">For example:</span></span>

* <span data-ttu-id="203f8-222">Exceptions thrown from controller constructors.</span><span class="sxs-lookup"><span data-stu-id="203f8-222">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="203f8-223">Exceptions thrown from message handlers.</span><span class="sxs-lookup"><span data-stu-id="203f8-223">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="203f8-224">Exceptions thrown during routing.</span><span class="sxs-lookup"><span data-stu-id="203f8-224">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="203f8-225">Exceptions thrown during response content serialization.</span><span class="sxs-lookup"><span data-stu-id="203f8-225">Exceptions thrown during response content serialization.</span></span>
* <span data-ttu-id="203f8-226">Exception thrown during application start-up.</span><span class="sxs-lookup"><span data-stu-id="203f8-226">Exception thrown during application start-up.</span></span>
* <span data-ttu-id="203f8-227">Exception thrown in background tasks.</span><span class="sxs-lookup"><span data-stu-id="203f8-227">Exception thrown in background tasks.</span></span>

<span data-ttu-id="203f8-228">All exceptions *handled* by application still need to be tracked manually.</span><span class="sxs-lookup"><span data-stu-id="203f8-228">All exceptions *handled* by application still need to be tracked manually.</span></span> <span data-ttu-id="203f8-229">Unhandled exceptions originating from controllers typically result in 500 "Internal Server Error" response.</span><span class="sxs-lookup"><span data-stu-id="203f8-229">Unhandled exceptions originating from controllers typically result in 500 "Internal Server Error" response.</span></span> <span data-ttu-id="203f8-230">If such response is manually constructed as a result of handled exception (or no exception at all) it is tracked in a corresponding request telemetry with `ResultCode` 500, however Application Insights SDK is unable to track corresponding exception.</span><span class="sxs-lookup"><span data-stu-id="203f8-230">If such response is manually constructed as a result of handled exception (or no exception at all) it is tracked in a corresponding request telemetry with `ResultCode` 500, however Application Insights SDK is unable to track corresponding exception.</span></span>

### <a name="prior-versions-support"></a><span data-ttu-id="203f8-231">Prior versions support</span><span class="sxs-lookup"><span data-stu-id="203f8-231">Prior versions support</span></span>
<span data-ttu-id="203f8-232">If you use WebAPI 1 (and prior) of Application Insights Web SDK 2.5 (and prior), refer to the following examples to track exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-232">If you use WebAPI 1 (and prior) of Application Insights Web SDK 2.5 (and prior), refer to the following examples to track exceptions.</span></span>

#### <a name="web-api-1x"></a><span data-ttu-id="203f8-233">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="203f8-233">Web API 1.x</span></span>
<span data-ttu-id="203f8-234">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="203f8-234">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

```csharp
    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }
```

<span data-ttu-id="203f8-235">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span><span class="sxs-lookup"><span data-stu-id="203f8-235">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

```csharp
    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }
```

[<span data-ttu-id="203f8-236">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-236">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

#### <a name="web-api-2x"></a><span data-ttu-id="203f8-237">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="203f8-237">Web API 2.x</span></span>
<span data-ttu-id="203f8-238">Add an implementation of IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="203f8-238">Add an implementation of IExceptionLogger:</span></span>

```csharp
    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }
```

<span data-ttu-id="203f8-239">Add this to the services in WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="203f8-239">Add this to the services in WebApiConfig:</span></span>

```csharp
    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
     }
```

[<span data-ttu-id="203f8-240">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-240">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="203f8-241">As alternatives, you could:</span><span class="sxs-lookup"><span data-stu-id="203f8-241">As alternatives, you could:</span></span>

1. <span data-ttu-id="203f8-242">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="203f8-242">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="203f8-243">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span><span class="sxs-lookup"><span data-stu-id="203f8-243">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="203f8-244">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span><span class="sxs-lookup"><span data-stu-id="203f8-244">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="203f8-245">WCF</span><span class="sxs-lookup"><span data-stu-id="203f8-245">WCF</span></span>
<span data-ttu-id="203f8-246">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="203f8-246">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Add the attribute to the service implementations:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...
```

[<span data-ttu-id="203f8-247">Sample</span><span class="sxs-lookup"><span data-stu-id="203f8-247">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="203f8-248">Exception performance counters</span><span class="sxs-lookup"><span data-stu-id="203f8-248">Exception performance counters</span></span>
<span data-ttu-id="203f8-249">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span><span class="sxs-lookup"><span data-stu-id="203f8-249">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="203f8-250">This includes both handled and unhandled .NET exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-250">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="203f8-251">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span><span class="sxs-lookup"><span data-stu-id="203f8-251">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="203f8-252">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span><span class="sxs-lookup"><span data-stu-id="203f8-252">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="203f8-253">This is different from the 'Exceptions' count calculated by the Application Insights portal counting TrackException reports.</span><span class="sxs-lookup"><span data-stu-id="203f8-253">This is different from the 'Exceptions' count calculated by the Application Insights portal counting TrackException reports.</span></span> <span data-ttu-id="203f8-254">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="203f8-254">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="203f8-255">Video</span><span class="sxs-lookup"><span data-stu-id="203f8-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="203f8-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="203f8-256">Next steps</span></span>
* [<span data-ttu-id="203f8-257">Monitor REST, SQL, and other calls to dependencies</span><span class="sxs-lookup"><span data-stu-id="203f8-257">Monitor REST, SQL, and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="203f8-258">Monitor page load times, browser exceptions, and AJAX calls</span><span class="sxs-lookup"><span data-stu-id="203f8-258">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="203f8-259">Monitor performance counters</span><span class="sxs-lookup"><span data-stu-id="203f8-259">Monitor performance counters</span></span>](app-insights-performance-counters.md)
