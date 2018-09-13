---
title: Diagnose failures and exceptions in web apps with Azure Application Insights | Microsoft Docs
description: Capture exceptions from ASP.NET apps along with request telemetry.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 454bf9596522458fb6e61b20fe1ec62ade617dad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550651"
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="aba24-103">Diagnose exceptions in your web apps with Application Insights</span><span class="sxs-lookup"><span data-stu-id="aba24-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="aba24-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aba24-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="aba24-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span><span class="sxs-lookup"><span data-stu-id="aba24-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="aba24-106">Set up exception reporting</span><span class="sxs-lookup"><span data-stu-id="aba24-106">Set up exception reporting</span></span>
* <span data-ttu-id="aba24-107">To have exceptions reported from your server app:</span><span class="sxs-lookup"><span data-stu-id="aba24-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="aba24-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span><span class="sxs-lookup"><span data-stu-id="aba24-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="aba24-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span><span class="sxs-lookup"><span data-stu-id="aba24-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="aba24-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="aba24-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="aba24-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="aba24-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="aba24-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span><span class="sxs-lookup"><span data-stu-id="aba24-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="aba24-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span><span class="sxs-lookup"><span data-stu-id="aba24-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="aba24-114">Web forms</span><span class="sxs-lookup"><span data-stu-id="aba24-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="aba24-115">MVC</span><span class="sxs-lookup"><span data-stu-id="aba24-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="aba24-116">Web API 1.\*</span><span class="sxs-lookup"><span data-stu-id="aba24-116">Web API 1.\*</span></span>](#web-api-1)
  * [<span data-ttu-id="aba24-117">Web API 2.\*</span><span class="sxs-lookup"><span data-stu-id="aba24-117">Web API 2.\*</span></span>](#web-api-2)
  * [<span data-ttu-id="aba24-118">WCF</span><span class="sxs-lookup"><span data-stu-id="aba24-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="aba24-119">Diagnosing exceptions using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aba24-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="aba24-120">Open the app solution in Visual Studio to help with debugging.</span><span class="sxs-lookup"><span data-stu-id="aba24-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="aba24-121">Run the app, either on your server or on your development machine by using F5.</span><span class="sxs-lookup"><span data-stu-id="aba24-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="aba24-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span><span class="sxs-lookup"><span data-stu-id="aba24-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="aba24-123">While you're debugging, you can do this just by clicking the Application Insights button.</span><span class="sxs-lookup"><span data-stu-id="aba24-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Right-click the project and choose Application Insights, Open.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="aba24-125">Notice that you can filter the report to show just exceptions.</span><span class="sxs-lookup"><span data-stu-id="aba24-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="aba24-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="aba24-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="aba24-127">Click an exception report to show its stack trace.</span><span class="sxs-lookup"><span data-stu-id="aba24-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="aba24-128">Click a line reference in the stack trace, to open the relevant code file.</span><span class="sxs-lookup"><span data-stu-id="aba24-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="aba24-129">In the code, notice that CodeLens shows data about the exceptions:</span><span class="sxs-lookup"><span data-stu-id="aba24-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![CodeLens notification of exceptions.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="aba24-131">Diagnosing failures using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="aba24-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="aba24-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span><span class="sxs-lookup"><span data-stu-id="aba24-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Select Settings, Failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="aba24-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span><span class="sxs-lookup"><span data-stu-id="aba24-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Select an instance of a failed request, and under exception details, get to instances of the exception.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="aba24-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span><span class="sxs-lookup"><span data-stu-id="aba24-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="aba24-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="aba24-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="aba24-138">Custom tracing and log data</span><span class="sxs-lookup"><span data-stu-id="aba24-138">Custom tracing and log data</span></span>
<span data-ttu-id="aba24-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span><span class="sxs-lookup"><span data-stu-id="aba24-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="aba24-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span><span class="sxs-lookup"><span data-stu-id="aba24-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="aba24-141">You have several options:</span><span class="sxs-lookup"><span data-stu-id="aba24-141">You have several options:</span></span>

* <span data-ttu-id="aba24-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span><span class="sxs-lookup"><span data-stu-id="aba24-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="aba24-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="aba24-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="aba24-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span><span class="sxs-lookup"><span data-stu-id="aba24-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="aba24-145">[TrackException()](#exceptions) sends stack traces.</span><span class="sxs-lookup"><span data-stu-id="aba24-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="aba24-146">[More about exceptions](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="aba24-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="aba24-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span><span class="sxs-lookup"><span data-stu-id="aba24-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="aba24-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span><span class="sxs-lookup"><span data-stu-id="aba24-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Drill through](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="aba24-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span><span class="sxs-lookup"><span data-stu-id="aba24-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="aba24-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span><span class="sxs-lookup"><span data-stu-id="aba24-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="aba24-152">Learn about sampling.</span><span class="sxs-lookup"><span data-stu-id="aba24-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="aba24-153">How to see request POST data</span><span class="sxs-lookup"><span data-stu-id="aba24-153">How to see request POST data</span></span>
<span data-ttu-id="aba24-154">Request details don't include the data sent to your app in a POST call.</span><span class="sxs-lookup"><span data-stu-id="aba24-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="aba24-155">To have this data reported:</span><span class="sxs-lookup"><span data-stu-id="aba24-155">To have this data reported:</span></span>

* <span data-ttu-id="aba24-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span><span class="sxs-lookup"><span data-stu-id="aba24-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="aba24-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="aba24-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="aba24-158">Send the POST data in the message parameter.</span><span class="sxs-lookup"><span data-stu-id="aba24-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="aba24-159">There is a limit to the permitted size, so you should try to send just the essential data.</span><span class="sxs-lookup"><span data-stu-id="aba24-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="aba24-160">When you investigate a failed request, find the associated traces.</span><span class="sxs-lookup"><span data-stu-id="aba24-160">When you investigate a failed request, find the associated traces.</span></span>  

![Drill through](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> <span data-ttu-id="aba24-162">Capturing exceptions and related diagnostic data</span><span class="sxs-lookup"><span data-stu-id="aba24-162">Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="aba24-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span><span class="sxs-lookup"><span data-stu-id="aba24-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="aba24-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span><span class="sxs-lookup"><span data-stu-id="aba24-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="aba24-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span><span class="sxs-lookup"><span data-stu-id="aba24-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="aba24-166">You can:</span><span class="sxs-lookup"><span data-stu-id="aba24-166">You can:</span></span>

* <span data-ttu-id="aba24-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span><span class="sxs-lookup"><span data-stu-id="aba24-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="aba24-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span><span class="sxs-lookup"><span data-stu-id="aba24-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="aba24-169">The necessary additions are different for different types of framework.</span><span class="sxs-lookup"><span data-stu-id="aba24-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="aba24-170">Reporting exceptions explicitly</span><span class="sxs-lookup"><span data-stu-id="aba24-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="aba24-171">The simplest way is to insert a call to TrackException() in an exception handler.</span><span class="sxs-lookup"><span data-stu-id="aba24-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="aba24-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="aba24-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="aba24-173">C#</span><span class="sxs-lookup"><span data-stu-id="aba24-173">C#</span></span>

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

<span data-ttu-id="aba24-174">VB</span><span class="sxs-lookup"><span data-stu-id="aba24-174">VB</span></span>

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

<span data-ttu-id="aba24-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span><span class="sxs-lookup"><span data-stu-id="aba24-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="aba24-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span><span class="sxs-lookup"><span data-stu-id="aba24-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="aba24-177">You can add as many items as you like to each dictionary.</span><span class="sxs-lookup"><span data-stu-id="aba24-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="aba24-178">Browser exceptions</span><span class="sxs-lookup"><span data-stu-id="aba24-178">Browser exceptions</span></span>
<span data-ttu-id="aba24-179">Most browser exceptions are reported.</span><span class="sxs-lookup"><span data-stu-id="aba24-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="aba24-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="aba24-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="aba24-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span><span class="sxs-lookup"><span data-stu-id="aba24-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="aba24-182">Web forms</span><span class="sxs-lookup"><span data-stu-id="aba24-182">Web forms</span></span>
<span data-ttu-id="aba24-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="aba24-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="aba24-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="aba24-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="aba24-185">(Add a Global.asax file if you don't already have one.)</span><span class="sxs-lookup"><span data-stu-id="aba24-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="aba24-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="aba24-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="aba24-187">MVC</span><span class="sxs-lookup"><span data-stu-id="aba24-187">MVC</span></span>
<span data-ttu-id="aba24-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span><span class="sxs-lookup"><span data-stu-id="aba24-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="aba24-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span><span class="sxs-lookup"><span data-stu-id="aba24-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="aba24-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="aba24-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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

#### <a name="mvc-2"></a><span data-ttu-id="aba24-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="aba24-191">MVC 2</span></span>
<span data-ttu-id="aba24-192">Replace the HandleError attribute with your new attribute in your controllers.</span><span class="sxs-lookup"><span data-stu-id="aba24-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="aba24-193">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="aba24-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="aba24-194">MVC 3</span></span>
<span data-ttu-id="aba24-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="aba24-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="aba24-196">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="aba24-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="aba24-197">MVC 4, MVC5</span></span>
<span data-ttu-id="aba24-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="aba24-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="aba24-199">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="aba24-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="aba24-200">Web API 1.x</span></span>
<span data-ttu-id="aba24-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="aba24-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="aba24-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span><span class="sxs-lookup"><span data-stu-id="aba24-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

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

[<span data-ttu-id="aba24-203">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="aba24-204">There are a number of cases that the exception filters cannot handle.</span><span class="sxs-lookup"><span data-stu-id="aba24-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="aba24-205">For example:</span><span class="sxs-lookup"><span data-stu-id="aba24-205">For example:</span></span>

* <span data-ttu-id="aba24-206">Exceptions thrown from controller constructors.</span><span class="sxs-lookup"><span data-stu-id="aba24-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="aba24-207">Exceptions thrown from message handlers.</span><span class="sxs-lookup"><span data-stu-id="aba24-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="aba24-208">Exceptions thrown during routing.</span><span class="sxs-lookup"><span data-stu-id="aba24-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="aba24-209">Exceptions thrown during response content serialization.</span><span class="sxs-lookup"><span data-stu-id="aba24-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="aba24-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="aba24-210">Web API 2.x</span></span>
<span data-ttu-id="aba24-211">Add an implementation of IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="aba24-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="aba24-212">Add this to the services in WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="aba24-212">Add this to the services in WebApiConfig:</span></span>

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
  <span data-ttu-id="aba24-213">}</span><span class="sxs-lookup"><span data-stu-id="aba24-213">}</span></span>

[<span data-ttu-id="aba24-214">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="aba24-215">As alternatives, you could:</span><span class="sxs-lookup"><span data-stu-id="aba24-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="aba24-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="aba24-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="aba24-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span><span class="sxs-lookup"><span data-stu-id="aba24-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="aba24-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span><span class="sxs-lookup"><span data-stu-id="aba24-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="aba24-219">WCF</span><span class="sxs-lookup"><span data-stu-id="aba24-219">WCF</span></span>
<span data-ttu-id="aba24-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="aba24-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="aba24-221">Add the attribute to the service implementations:</span><span class="sxs-lookup"><span data-stu-id="aba24-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="aba24-222">Sample</span><span class="sxs-lookup"><span data-stu-id="aba24-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="aba24-223">Exception performance counters</span><span class="sxs-lookup"><span data-stu-id="aba24-223">Exception performance counters</span></span>
<span data-ttu-id="aba24-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span><span class="sxs-lookup"><span data-stu-id="aba24-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="aba24-225">This includes both handled and unhandled .NET exceptions.</span><span class="sxs-lookup"><span data-stu-id="aba24-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="aba24-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span><span class="sxs-lookup"><span data-stu-id="aba24-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="aba24-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span><span class="sxs-lookup"><span data-stu-id="aba24-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="aba24-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span><span class="sxs-lookup"><span data-stu-id="aba24-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="aba24-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="aba24-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="aba24-230">Video</span><span class="sxs-lookup"><span data-stu-id="aba24-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="aba24-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="aba24-231">Next steps</span></span>
* [<span data-ttu-id="aba24-232">Monitor REST, SQL and other calls to dependencies</span><span class="sxs-lookup"><span data-stu-id="aba24-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="aba24-233">Monitor page load times, browser exceptions, and AJAX calls</span><span class="sxs-lookup"><span data-stu-id="aba24-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="aba24-234">Monitor performance counters</span><span class="sxs-lookup"><span data-stu-id="aba24-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)






