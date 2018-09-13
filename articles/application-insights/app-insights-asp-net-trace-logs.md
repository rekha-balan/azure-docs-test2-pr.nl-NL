---
title: Explore .NET trace logs in Application Insights
description: Search logs generated with Trace, NLog, or Log4Net.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: douge
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: awills
ms.openlocfilehash: e222d1eb0986794e1db0c47d0b2475f3da4e1950
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554354"
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="2ede6-103">Explore .NET trace logs in Application Insights</span><span class="sxs-lookup"><span data-stu-id="2ede6-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="2ede6-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span><span class="sxs-lookup"><span data-stu-id="2ede6-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="2ede6-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span><span class="sxs-lookup"><span data-stu-id="2ede6-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="2ede6-106">Do you need the log capture module?</span><span class="sxs-lookup"><span data-stu-id="2ede6-106">Do you need the log capture module?</span></span> <span data-ttu-id="2ede6-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span><span class="sxs-lookup"><span data-stu-id="2ede6-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="2ede6-108">Install logging on your app</span><span class="sxs-lookup"><span data-stu-id="2ede6-108">Install logging on your app</span></span>
<span data-ttu-id="2ede6-109">Install your chosen logging framework in your project.</span><span class="sxs-lookup"><span data-stu-id="2ede6-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="2ede6-110">This should result in an entry in app.config or web.config.</span><span class="sxs-lookup"><span data-stu-id="2ede6-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="2ede6-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span><span class="sxs-lookup"><span data-stu-id="2ede6-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```

## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="2ede6-112">Configure Application Insights to collect logs</span><span class="sxs-lookup"><span data-stu-id="2ede6-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="2ede6-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span><span class="sxs-lookup"><span data-stu-id="2ede6-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="2ede6-114">You'll see an option to include the log collector.</span><span class="sxs-lookup"><span data-stu-id="2ede6-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="2ede6-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="2ede6-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="2ede6-116">Select the option to **Configure trace collection**.</span><span class="sxs-lookup"><span data-stu-id="2ede6-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="2ede6-117">*No Application Insights menu or log collector option?*</span><span class="sxs-lookup"><span data-stu-id="2ede6-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="2ede6-118">Try [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="2ede6-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="2ede6-119">Manual installation</span><span class="sxs-lookup"><span data-stu-id="2ede6-119">Manual installation</span></span>
<span data-ttu-id="2ede6-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span><span class="sxs-lookup"><span data-stu-id="2ede6-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="2ede6-121">If you plan to use log4Net or NLog, install it in your project.</span><span class="sxs-lookup"><span data-stu-id="2ede6-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="2ede6-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="2ede6-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="2ede6-123">Search for "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="2ede6-123">Search for "Application Insights"</span></span>

    ![Get the prerelease version of the appropriate adapter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-trace-logs/appinsights-36nuget.png)
4. <span data-ttu-id="2ede6-125">Select the appropriate package - one of:</span><span class="sxs-lookup"><span data-stu-id="2ede6-125">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="2ede6-126">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span><span class="sxs-lookup"><span data-stu-id="2ede6-126">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="2ede6-127">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="2ede6-127">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="2ede6-128">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="2ede6-128">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="2ede6-129">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span><span class="sxs-lookup"><span data-stu-id="2ede6-129">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="2ede6-130">Insert diagnostic log calls</span><span class="sxs-lookup"><span data-stu-id="2ede6-130">Insert diagnostic log calls</span></span>
<span data-ttu-id="2ede6-131">If you use System.Diagnostics.Trace, a typical call would be:</span><span class="sxs-lookup"><span data-stu-id="2ede6-131">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="2ede6-132">If you prefer log4net or NLog:</span><span class="sxs-lookup"><span data-stu-id="2ede6-132">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");


## <a name="using-the-trace-api-directly"></a><span data-ttu-id="2ede6-133">Using the Trace API directly</span><span class="sxs-lookup"><span data-stu-id="2ede6-133">Using the Trace API directly</span></span>
<span data-ttu-id="2ede6-134">You can call the Application Insights trace API directly.</span><span class="sxs-lookup"><span data-stu-id="2ede6-134">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="2ede6-135">The logging adapters use this API.</span><span class="sxs-lookup"><span data-stu-id="2ede6-135">The logging adapters use this API.</span></span>

<span data-ttu-id="2ede6-136">For example:</span><span class="sxs-lookup"><span data-stu-id="2ede6-136">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="2ede6-137">An advantage of TrackTrace is that you can put relatively long data in the message.</span><span class="sxs-lookup"><span data-stu-id="2ede6-137">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="2ede6-138">For example, you could encode POST data there.</span><span class="sxs-lookup"><span data-stu-id="2ede6-138">For example, you could encode POST data there.</span></span>

<span data-ttu-id="2ede6-139">In addition, you can add a severity level to your message.</span><span class="sxs-lookup"><span data-stu-id="2ede6-139">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="2ede6-140">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span><span class="sxs-lookup"><span data-stu-id="2ede6-140">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="2ede6-141">For example:</span><span class="sxs-lookup"><span data-stu-id="2ede6-141">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="2ede6-142">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span><span class="sxs-lookup"><span data-stu-id="2ede6-142">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="2ede6-143">Explore your logs</span><span class="sxs-lookup"><span data-stu-id="2ede6-143">Explore your logs</span></span>
<span data-ttu-id="2ede6-144">Run your app, either in debug mode or deploy it live.</span><span class="sxs-lookup"><span data-stu-id="2ede6-144">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="2ede6-145">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="2ede6-145">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![In Application Insights, choose Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="2ede6-148">You can, for example:</span><span class="sxs-lookup"><span data-stu-id="2ede6-148">You can, for example:</span></span>

* <span data-ttu-id="2ede6-149">Filter on log traces, or on items with specific properties</span><span class="sxs-lookup"><span data-stu-id="2ede6-149">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="2ede6-150">Inspect a specific item in detail.</span><span class="sxs-lookup"><span data-stu-id="2ede6-150">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="2ede6-151">Find other telemetry relating to the same user request (that is, with the same OperationId)</span><span class="sxs-lookup"><span data-stu-id="2ede6-151">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="2ede6-152">Save the configuration of this page as a Favorite</span><span class="sxs-lookup"><span data-stu-id="2ede6-152">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="2ede6-153">**Sampling.**</span><span class="sxs-lookup"><span data-stu-id="2ede6-153">**Sampling.**</span></span> <span data-ttu-id="2ede6-154">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="2ede6-154">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="2ede6-155">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="2ede6-155">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="2ede6-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ede6-156">Next steps</span></span>
<span data-ttu-id="2ede6-157">[Diagnose failures and exceptions in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="2ede6-157">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="2ede6-158">[Learn more about Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="2ede6-158">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2ede6-159">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2ede6-159">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="2ede6-160">How do I do this for Java?</span><span class="sxs-lookup"><span data-stu-id="2ede6-160">How do I do this for Java?</span></span>
<span data-ttu-id="2ede6-161">Use the [Java log adapters](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2ede6-161">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="2ede6-162">There's no Application Insights option on the project context menu</span><span class="sxs-lookup"><span data-stu-id="2ede6-162">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="2ede6-163">Check Application Insights tools is installed on this development machine.</span><span class="sxs-lookup"><span data-stu-id="2ede6-163">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="2ede6-164">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="2ede6-164">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="2ede6-165">If it isn't in the Installed tab, open the Online tab and install it.</span><span class="sxs-lookup"><span data-stu-id="2ede6-165">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="2ede6-166">This might be a type of project not supported by Application Insights tools.</span><span class="sxs-lookup"><span data-stu-id="2ede6-166">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="2ede6-167">Use [manual installation](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="2ede6-167">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="2ede6-168">No log adapter option in the configuration tool</span><span class="sxs-lookup"><span data-stu-id="2ede6-168">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="2ede6-169">You need to install the logging framework first.</span><span class="sxs-lookup"><span data-stu-id="2ede6-169">You need to install the logging framework first.</span></span>
* <span data-ttu-id="2ede6-170">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ede6-170">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="2ede6-171">Have you got the latest version of Application Insights?</span><span class="sxs-lookup"><span data-stu-id="2ede6-171">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="2ede6-172">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span><span class="sxs-lookup"><span data-stu-id="2ede6-172">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <a name="emptykey"></a><span data-ttu-id="2ede6-173">I get an error "Instrumentation key cannot be empty"</span><span class="sxs-lookup"><span data-stu-id="2ede6-173">I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="2ede6-174">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2ede6-174">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="2ede6-175">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2ede6-175">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="2ede6-176">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span><span class="sxs-lookup"><span data-stu-id="2ede6-176">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="2ede6-177">That should fix it.</span><span class="sxs-lookup"><span data-stu-id="2ede6-177">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="2ede6-178">I can see traces in diagnostic search, but not the other events</span><span class="sxs-lookup"><span data-stu-id="2ede6-178">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="2ede6-179">It can sometimes take a while for all the events and requests to get through the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2ede6-179">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <a name="limits"></a><span data-ttu-id="2ede6-180">How much data is retained?</span><span class="sxs-lookup"><span data-stu-id="2ede6-180">How much data is retained?</span></span>
<span data-ttu-id="2ede6-181">Up to 500 events per second from each application.</span><span class="sxs-lookup"><span data-stu-id="2ede6-181">Up to 500 events per second from each application.</span></span> <span data-ttu-id="2ede6-182">Events are retained for seven days.</span><span class="sxs-lookup"><span data-stu-id="2ede6-182">Events are retained for seven days.</span></span>

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="2ede6-183">I'm not seeing some of the log entries that I expect</span><span class="sxs-lookup"><span data-stu-id="2ede6-183">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="2ede6-184">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="2ede6-184">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="2ede6-185">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="2ede6-185">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <a name="add"></a><span data-ttu-id="2ede6-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ede6-186">Next steps</span></span>
* <span data-ttu-id="2ede6-187">[Set up availability and responsiveness tests][availability]</span><span class="sxs-lookup"><span data-stu-id="2ede6-187">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="2ede6-188">[Troubleshooting][qna]</span><span class="sxs-lookup"><span data-stu-id="2ede6-188">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md



