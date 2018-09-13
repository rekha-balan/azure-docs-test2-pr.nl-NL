---
title: Explore .NET trace logs in Application Insights
description: Search logs generated with Trace, NLog, or Log4Net.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/03/2017
ms.author: mbullwin
ms.openlocfilehash: b1cd2e8d7649de48f34efb0c7d839e17906a29bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819291"
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="b9147-103">Explore .NET trace logs in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b9147-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="b9147-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span><span class="sxs-lookup"><span data-stu-id="b9147-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="b9147-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span><span class="sxs-lookup"><span data-stu-id="b9147-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="b9147-106">Do you need the log capture module?</span><span class="sxs-lookup"><span data-stu-id="b9147-106">Do you need the log capture module?</span></span> <span data-ttu-id="b9147-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span><span class="sxs-lookup"><span data-stu-id="b9147-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="b9147-108">Install logging on your app</span><span class="sxs-lookup"><span data-stu-id="b9147-108">Install logging on your app</span></span>
<span data-ttu-id="b9147-109">Install your chosen logging framework in your project.</span><span class="sxs-lookup"><span data-stu-id="b9147-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="b9147-110">This should result in an entry in app.config or web.config.</span><span class="sxs-lookup"><span data-stu-id="b9147-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="b9147-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span><span class="sxs-lookup"><span data-stu-id="b9147-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

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
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="b9147-112">Configure Application Insights to collect logs</span><span class="sxs-lookup"><span data-stu-id="b9147-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="b9147-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span><span class="sxs-lookup"><span data-stu-id="b9147-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="b9147-114">You'll see an option to include the log collector.</span><span class="sxs-lookup"><span data-stu-id="b9147-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="b9147-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="b9147-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="b9147-116">Select the option to **Configure trace collection**.</span><span class="sxs-lookup"><span data-stu-id="b9147-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="b9147-117">*No Application Insights menu or log collector option?*</span><span class="sxs-lookup"><span data-stu-id="b9147-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="b9147-118">Try [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b9147-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="b9147-119">Manual installation</span><span class="sxs-lookup"><span data-stu-id="b9147-119">Manual installation</span></span>
<span data-ttu-id="b9147-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span><span class="sxs-lookup"><span data-stu-id="b9147-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="b9147-121">If you plan to use log4Net or NLog, install it in your project.</span><span class="sxs-lookup"><span data-stu-id="b9147-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="b9147-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="b9147-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="b9147-123">Search for "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="b9147-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="b9147-124">Select the appropriate package - one of:</span><span class="sxs-lookup"><span data-stu-id="b9147-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="b9147-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span><span class="sxs-lookup"><span data-stu-id="b9147-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="b9147-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span><span class="sxs-lookup"><span data-stu-id="b9147-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="b9147-127">Microsoft.ApplicationInsights.EtwCollector (to capture ETW events)</span><span class="sxs-lookup"><span data-stu-id="b9147-127">Microsoft.ApplicationInsights.EtwCollector (to capture ETW events)</span></span>
   * <span data-ttu-id="b9147-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="b9147-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="b9147-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="b9147-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="b9147-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span><span class="sxs-lookup"><span data-stu-id="b9147-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="b9147-131">Insert diagnostic log calls</span><span class="sxs-lookup"><span data-stu-id="b9147-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="b9147-132">If you use System.Diagnostics.Trace, a typical call would be:</span><span class="sxs-lookup"><span data-stu-id="b9147-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="b9147-133">If you prefer log4net or NLog:</span><span class="sxs-lookup"><span data-stu-id="b9147-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="b9147-134">Using EventSource events</span><span class="sxs-lookup"><span data-stu-id="b9147-134">Using EventSource events</span></span>
<span data-ttu-id="b9147-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span><span class="sxs-lookup"><span data-stu-id="b9147-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="b9147-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span><span class="sxs-lookup"><span data-stu-id="b9147-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="b9147-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="b9147-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="b9147-138">For each source, you can set the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b9147-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="b9147-139">`Name` specifies the name of the EventSource to collect.</span><span class="sxs-lookup"><span data-stu-id="b9147-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="b9147-140">`Level` specifies the logging level to collect.</span><span class="sxs-lookup"><span data-stu-id="b9147-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="b9147-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="b9147-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="b9147-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span><span class="sxs-lookup"><span data-stu-id="b9147-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="b9147-143">Using DiagnosticSource events</span><span class="sxs-lookup"><span data-stu-id="b9147-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="b9147-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span><span class="sxs-lookup"><span data-stu-id="b9147-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="b9147-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="b9147-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="b9147-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="b9147-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnosticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="b9147-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="b9147-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="b9147-148">Using ETW events</span><span class="sxs-lookup"><span data-stu-id="b9147-148">Using ETW events</span></span>
<span data-ttu-id="b9147-149">You can configure ETW events to be sent to Application Insights as traces.</span><span class="sxs-lookup"><span data-stu-id="b9147-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="b9147-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span><span class="sxs-lookup"><span data-stu-id="b9147-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="b9147-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="b9147-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="b9147-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span><span class="sxs-lookup"><span data-stu-id="b9147-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="b9147-153">For each source, you can set the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b9147-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="b9147-154">`ProviderName` is the name of the ETW provider to collect.</span><span class="sxs-lookup"><span data-stu-id="b9147-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="b9147-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="b9147-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="b9147-156">`Level` sets the logging level to collect.</span><span class="sxs-lookup"><span data-stu-id="b9147-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="b9147-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="b9147-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="b9147-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span><span class="sxs-lookup"><span data-stu-id="b9147-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="b9147-159">Using the Trace API directly</span><span class="sxs-lookup"><span data-stu-id="b9147-159">Using the Trace API directly</span></span>
<span data-ttu-id="b9147-160">You can call the Application Insights trace API directly.</span><span class="sxs-lookup"><span data-stu-id="b9147-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="b9147-161">The logging adapters use this API.</span><span class="sxs-lookup"><span data-stu-id="b9147-161">The logging adapters use this API.</span></span>

<span data-ttu-id="b9147-162">For example:</span><span class="sxs-lookup"><span data-stu-id="b9147-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="b9147-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span><span class="sxs-lookup"><span data-stu-id="b9147-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="b9147-164">For example, you could encode POST data there.</span><span class="sxs-lookup"><span data-stu-id="b9147-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="b9147-165">In addition, you can add a severity level to your message.</span><span class="sxs-lookup"><span data-stu-id="b9147-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="b9147-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span><span class="sxs-lookup"><span data-stu-id="b9147-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="b9147-167">For example:</span><span class="sxs-lookup"><span data-stu-id="b9147-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="b9147-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span><span class="sxs-lookup"><span data-stu-id="b9147-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="b9147-169">Explore your logs</span><span class="sxs-lookup"><span data-stu-id="b9147-169">Explore your logs</span></span>
<span data-ttu-id="b9147-170">Run your app, either in debug mode or deploy it live.</span><span class="sxs-lookup"><span data-stu-id="b9147-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="b9147-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="b9147-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![In Application Insights, choose Search](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Search](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="b9147-174">You can, for example:</span><span class="sxs-lookup"><span data-stu-id="b9147-174">You can, for example:</span></span>

* <span data-ttu-id="b9147-175">Filter on log traces, or on items with specific properties</span><span class="sxs-lookup"><span data-stu-id="b9147-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="b9147-176">Inspect a specific item in detail.</span><span class="sxs-lookup"><span data-stu-id="b9147-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="b9147-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span><span class="sxs-lookup"><span data-stu-id="b9147-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="b9147-178">Save the configuration of this page as a Favorite</span><span class="sxs-lookup"><span data-stu-id="b9147-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="b9147-179">**Sampling.**</span><span class="sxs-lookup"><span data-stu-id="b9147-179">**Sampling.**</span></span> <span data-ttu-id="b9147-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="b9147-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="b9147-181">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="b9147-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="b9147-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9147-182">Next steps</span></span>
<span data-ttu-id="b9147-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="b9147-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="b9147-184">[Learn more about Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="b9147-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b9147-185">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b9147-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="b9147-186">How do I do this for Java?</span><span class="sxs-lookup"><span data-stu-id="b9147-186">How do I do this for Java?</span></span>
<span data-ttu-id="b9147-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b9147-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="b9147-188">There's no Application Insights option on the project context menu</span><span class="sxs-lookup"><span data-stu-id="b9147-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="b9147-189">Check Application Insights tools is installed on this development machine.</span><span class="sxs-lookup"><span data-stu-id="b9147-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="b9147-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="b9147-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="b9147-191">If it isn't in the Installed tab, open the Online tab and install it.</span><span class="sxs-lookup"><span data-stu-id="b9147-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="b9147-192">This might be a type of project not supported by Application Insights tools.</span><span class="sxs-lookup"><span data-stu-id="b9147-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="b9147-193">Use [manual installation](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="b9147-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="b9147-194">No log adapter option in the configuration tool</span><span class="sxs-lookup"><span data-stu-id="b9147-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="b9147-195">You need to install the logging framework first.</span><span class="sxs-lookup"><span data-stu-id="b9147-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="b9147-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9147-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="b9147-197">Have you got the latest version of Application Insights?</span><span class="sxs-lookup"><span data-stu-id="b9147-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="b9147-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span><span class="sxs-lookup"><span data-stu-id="b9147-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <a name="emptykey"></a><span data-ttu-id="b9147-199">I get an error "Instrumentation key cannot be empty"</span><span class="sxs-lookup"><span data-stu-id="b9147-199">I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="b9147-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b9147-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="b9147-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="b9147-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="b9147-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span><span class="sxs-lookup"><span data-stu-id="b9147-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="b9147-203">That should fix it.</span><span class="sxs-lookup"><span data-stu-id="b9147-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="b9147-204">I can see traces in diagnostic search, but not the other events</span><span class="sxs-lookup"><span data-stu-id="b9147-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="b9147-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span><span class="sxs-lookup"><span data-stu-id="b9147-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <a name="limits"></a><span data-ttu-id="b9147-206">How much data is retained?</span><span class="sxs-lookup"><span data-stu-id="b9147-206">How much data is retained?</span></span>
<span data-ttu-id="b9147-207">Several factors impact the amount of data retained.</span><span class="sxs-lookup"><span data-stu-id="b9147-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="b9147-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span><span class="sxs-lookup"><span data-stu-id="b9147-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="b9147-209">I'm not seeing some of the log entries that I expect</span><span class="sxs-lookup"><span data-stu-id="b9147-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="b9147-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="b9147-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="b9147-211">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="b9147-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <a name="add"></a><span data-ttu-id="b9147-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9147-212">Next steps</span></span>
* <span data-ttu-id="b9147-213">[Set up availability and responsiveness tests][availability]</span><span class="sxs-lookup"><span data-stu-id="b9147-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="b9147-214">[Troubleshooting][qna]</span><span class="sxs-lookup"><span data-stu-id="b9147-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
