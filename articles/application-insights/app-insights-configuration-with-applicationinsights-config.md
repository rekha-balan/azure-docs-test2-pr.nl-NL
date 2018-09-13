---
title: ApplicationInsights.config reference - Azure | Microsoft Docs
description: Enable or disable data collection modules, and add performance counters and other parameters.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/05/2018
ms.reviewer: olegan
ms.author: mbullwin
ms.openlocfilehash: 9e53fa896f1d958e505d26af430b262be9195605
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44786973"
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="f8a3f-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span><span class="sxs-lookup"><span data-stu-id="f8a3f-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="f8a3f-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="f8a3f-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="f8a3f-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="f8a3f-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="f8a3f-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="f8a3f-109">It is automatically added to your project when you [install most versions of the SDK][start].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="f8a3f-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Application Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Application Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="f8a3f-111">There isn't an equivalent file to control the [SDK in a web page][client].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="f8a3f-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a3f-113">ApplicationInsights.config and .xml instructions do not apply to the .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-113">ApplicationInsights.config and .xml instructions do not apply to the .NET Core SDK.</span></span> <span data-ttu-id="f8a3f-114">For changes to a .NET Core application we typically use the appsettings.json file.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-114">For changes to a .NET Core application we typically use the appsettings.json file.</span></span> <span data-ttu-id="f8a3f-115">An example of this can be found in the [Snapshot Debugger documentation.](https://docs.microsoft.com/azure/application-insights/app-insights-snapshot-debugger#configure-snapshot-collection-for-aspnet-core-20-applications)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-115">An example of this can be found in the [Snapshot Debugger documentation.](https://docs.microsoft.com/azure/application-insights/app-insights-snapshot-debugger#configure-snapshot-collection-for-aspnet-core-20-applications)</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="f8a3f-116">Telemetry Modules (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-116">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="f8a3f-117">Each telemetry module collects a specific type of data and uses the core API to send the data.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-117">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="f8a3f-118">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-118">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="f8a3f-119">There's a node in the configuration file for each module.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-119">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="f8a3f-120">To disable a module, delete the node or comment it out.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-120">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="f8a3f-121">Dependency Tracking</span><span class="sxs-lookup"><span data-stu-id="f8a3f-121">Dependency Tracking</span></span>
<span data-ttu-id="f8a3f-122">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-122">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="f8a3f-123">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-123">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="f8a3f-124">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-124">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="f8a3f-125">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-125">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="f8a3f-126">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-126">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="f8a3f-127">Performance collector</span><span class="sxs-lookup"><span data-stu-id="f8a3f-127">Performance collector</span></span>
<span data-ttu-id="f8a3f-128">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory, and network load from IIS installations.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-128">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory, and network load from IIS installations.</span></span> <span data-ttu-id="f8a3f-129">You can specify which counters to collect, including performance counters you have set up yourself.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-129">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="f8a3f-130">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-130">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="f8a3f-131">Application Insights Diagnostics Telemetry</span><span class="sxs-lookup"><span data-stu-id="f8a3f-131">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="f8a3f-132">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-132">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="f8a3f-133">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-133">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="f8a3f-134">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-134">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="f8a3f-135">Sends diagnostic data to dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-135">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="f8a3f-136">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-136">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="f8a3f-137">If you only install this package, the ApplicationInsights.config file is not automatically created.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-137">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="f8a3f-138">Developer Mode</span><span class="sxs-lookup"><span data-stu-id="f8a3f-138">Developer Mode</span></span>
<span data-ttu-id="f8a3f-139">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-139">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="f8a3f-140">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-140">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="f8a3f-141">It causes significant overhead in CPU and network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-141">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="f8a3f-142">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span><span class="sxs-lookup"><span data-stu-id="f8a3f-142">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="f8a3f-143">Web Request Tracking</span><span class="sxs-lookup"><span data-stu-id="f8a3f-143">Web Request Tracking</span></span>
<span data-ttu-id="f8a3f-144">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-144">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="f8a3f-145">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span><span class="sxs-lookup"><span data-stu-id="f8a3f-145">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="f8a3f-146">Exception tracking</span><span class="sxs-lookup"><span data-stu-id="f8a3f-146">Exception tracking</span></span>
<span data-ttu-id="f8a3f-147">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-147">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="f8a3f-148">See [Failures and exceptions][exceptions].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-148">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="f8a3f-149">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span><span class="sxs-lookup"><span data-stu-id="f8a3f-149">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="f8a3f-150">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-150">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="f8a3f-151">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-151">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="f8a3f-152">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-152">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="f8a3f-153">EventSource Tracking</span><span class="sxs-lookup"><span data-stu-id="f8a3f-153">EventSource Tracking</span></span>
<span data-ttu-id="f8a3f-154">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-154">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="f8a3f-155">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-155">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="f8a3f-156">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="f8a3f-156">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="f8a3f-157">ETW Event Tracking</span><span class="sxs-lookup"><span data-stu-id="f8a3f-157">ETW Event Tracking</span></span>
<span data-ttu-id="f8a3f-158">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-158">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="f8a3f-159">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-159">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="f8a3f-160">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="f8a3f-160">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="f8a3f-161">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="f8a3f-161">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="f8a3f-162">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-162">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="f8a3f-163">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-163">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="f8a3f-164">No entry in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-164">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="f8a3f-165">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-165">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="f8a3f-166">If you just install this NuGet, no .config file is generated.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-166">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="f8a3f-167">Telemetry Channel</span><span class="sxs-lookup"><span data-stu-id="f8a3f-167">Telemetry Channel</span></span>
<span data-ttu-id="f8a3f-168">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-168">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="f8a3f-169">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-169">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="f8a3f-170">It buffers data in memory.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-170">It buffers data in memory.</span></span>
* <span data-ttu-id="f8a3f-171">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-171">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="f8a3f-172">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-172">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="f8a3f-173">Telemetry Initializers (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-173">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="f8a3f-174">Telemetry initializers set context properties that are sent along with every item of telemetry.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-174">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="f8a3f-175">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-175">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="f8a3f-176">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-176">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="f8a3f-177">`AccountIdTelemetryInitializer` sets the AccountId property.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-177">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="f8a3f-178">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-178">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="f8a3f-179">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-179">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="f8a3f-180">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-180">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="f8a3f-181">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-181">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="f8a3f-182">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-182">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="f8a3f-183">`Type` is set to "PC"</span><span class="sxs-lookup"><span data-stu-id="f8a3f-183">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="f8a3f-184">`Id` is set to the domain name of the computer where the web application is running.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-184">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="f8a3f-185">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-185">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="f8a3f-186">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-186">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="f8a3f-187">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-187">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="f8a3f-188">`Language` is set to the name of the `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-188">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="f8a3f-189">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-189">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="f8a3f-190">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-190">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="f8a3f-191">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-191">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="f8a3f-192">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-192">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="f8a3f-193">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session`, and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-193">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session`, and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="f8a3f-194">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-194">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="f8a3f-195">The `<Filters>` set identifying properties of the requests.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-195">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="f8a3f-196">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-196">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="f8a3f-197">`WebTestTelemetryInitializer` sets the user id, session id, and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-197">`WebTestTelemetryInitializer` sets the user id, session id, and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="f8a3f-198">The `<Filters>` set identifying properties of the requests.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-198">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="f8a3f-199">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-199">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="f8a3f-200">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-200">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="f8a3f-201">For more information, see the [GitHub page](https://github.com/Microsoft/ApplicationInsights-ServiceFabric/blob/master/README.md) about the properties added by this NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-201">For more information, see the [GitHub page](https://github.com/Microsoft/ApplicationInsights-ServiceFabric/blob/master/README.md) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="f8a3f-202">Telemetry Processors (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-202">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="f8a3f-203">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-203">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="f8a3f-204">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-204">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="f8a3f-205">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-205">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="f8a3f-206">This is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-206">This is enabled by default.</span></span> <span data-ttu-id="f8a3f-207">If your app sends a lot of telemetry, this processor removes some of it.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-207">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="f8a3f-208">The parameter provides the target that the algorithm tries to achieve.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-208">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="f8a3f-209">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-209">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="f8a3f-210">[Learn more about sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-210">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="f8a3f-211">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-211">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="f8a3f-212">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="f8a3f-212">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="f8a3f-213">Channel parameters (Java)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-213">Channel parameters (Java)</span></span>
<span data-ttu-id="f8a3f-214">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-214">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="f8a3f-215">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="f8a3f-215">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="f8a3f-216">The number of telemetry items that can be stored in the SDK's in-memory storage.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-216">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="f8a3f-217">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-217">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="f8a3f-218">Min: 1</span><span class="sxs-lookup"><span data-stu-id="f8a3f-218">Min: 1</span></span>
* <span data-ttu-id="f8a3f-219">Max: 1000</span><span class="sxs-lookup"><span data-stu-id="f8a3f-219">Max: 1000</span></span>
* <span data-ttu-id="f8a3f-220">Default: 500</span><span class="sxs-lookup"><span data-stu-id="f8a3f-220">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="f8a3f-221">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="f8a3f-221">FlushIntervalInSeconds</span></span>
<span data-ttu-id="f8a3f-222">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span><span class="sxs-lookup"><span data-stu-id="f8a3f-222">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="f8a3f-223">Min: 1</span><span class="sxs-lookup"><span data-stu-id="f8a3f-223">Min: 1</span></span>
* <span data-ttu-id="f8a3f-224">Max: 300</span><span class="sxs-lookup"><span data-stu-id="f8a3f-224">Max: 300</span></span>
* <span data-ttu-id="f8a3f-225">Default: 5</span><span class="sxs-lookup"><span data-stu-id="f8a3f-225">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="f8a3f-226">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="f8a3f-226">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="f8a3f-227">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-227">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="f8a3f-228">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-228">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="f8a3f-229">When the storage size has been met, new telemetry items will be discarded.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-229">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="f8a3f-230">Min: 1</span><span class="sxs-lookup"><span data-stu-id="f8a3f-230">Min: 1</span></span>
* <span data-ttu-id="f8a3f-231">Max: 100</span><span class="sxs-lookup"><span data-stu-id="f8a3f-231">Max: 100</span></span>
* <span data-ttu-id="f8a3f-232">Default: 10</span><span class="sxs-lookup"><span data-stu-id="f8a3f-232">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="f8a3f-233">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="f8a3f-233">InstrumentationKey</span></span>
<span data-ttu-id="f8a3f-234">This determines the Application Insights resource in which your data appears.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-234">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="f8a3f-235">Typically you create a separate resource, with a separate key, for each of your applications.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-235">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="f8a3f-236">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-236">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="f8a3f-237">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-237">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="f8a3f-238">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-238">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```csharp

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="f8a3f-239">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-239">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```csharp

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="f8a3f-240">To get a new key, [create a new resource in the Application Insights portal][new].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-240">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>



## <a name="applicationid-provider"></a><span data-ttu-id="f8a3f-241">ApplicationId Provider</span><span class="sxs-lookup"><span data-stu-id="f8a3f-241">ApplicationId Provider</span></span>

<span data-ttu-id="f8a3f-242">_Available starting in v2.6.0_</span><span class="sxs-lookup"><span data-stu-id="f8a3f-242">_Available starting in v2.6.0_</span></span>

<span data-ttu-id="f8a3f-243">The purpose of this provider is to lookup an Application ID based on an Instrumentation Key.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-243">The purpose of this provider is to lookup an Application ID based on an Instrumentation Key.</span></span> <span data-ttu-id="f8a3f-244">The Application ID is included in RequestTelemetry and DependencyTelemetry and used to determine Correlation in the Portal.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-244">The Application ID is included in RequestTelemetry and DependencyTelemetry and used to determine Correlation in the Portal.</span></span>

<span data-ttu-id="f8a3f-245">This is available by setting `TelemetryConfiguration.ApplicationIdProvider` either in code or in config.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-245">This is available by setting `TelemetryConfiguration.ApplicationIdProvider` either in code or in config.</span></span>

### <a name="interface-iapplicationidprovider"></a><span data-ttu-id="f8a3f-246">Interface: IApplicationIdProvider</span><span class="sxs-lookup"><span data-stu-id="f8a3f-246">Interface: IApplicationIdProvider</span></span>

```csharp
public interface IApplicationIdProvider
{
    bool TryGetApplicationId(string instrumentationKey, out string applicationId);
}
```


<span data-ttu-id="f8a3f-247">We provide two implementations in the [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights) sdk: `ApplicationInsightsApplicationIdProvider` and `DictionaryApplicationIdProvider`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-247">We provide two implementations in the [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights) sdk: `ApplicationInsightsApplicationIdProvider` and `DictionaryApplicationIdProvider`.</span></span>

### <a name="applicationinsightsapplicationidprovider"></a><span data-ttu-id="f8a3f-248">ApplicationInsightsApplicationIdProvider</span><span class="sxs-lookup"><span data-stu-id="f8a3f-248">ApplicationInsightsApplicationIdProvider</span></span>

<span data-ttu-id="f8a3f-249">This is a wrapper around our Profile API.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-249">This is a wrapper around our Profile API.</span></span> <span data-ttu-id="f8a3f-250">It will throttle requests and cache results.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-250">It will throttle requests and cache results.</span></span>

<span data-ttu-id="f8a3f-251">This provider is added to your config file when you install either [Microsoft.ApplicationInsights.DependencyCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) or [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)</span><span class="sxs-lookup"><span data-stu-id="f8a3f-251">This provider is added to your config file when you install either [Microsoft.ApplicationInsights.DependencyCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) or [Microsoft.ApplicationInsights.Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)</span></span>

<span data-ttu-id="f8a3f-252">This class has an optional property `ProfileQueryEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-252">This class has an optional property `ProfileQueryEndpoint`.</span></span>
<span data-ttu-id="f8a3f-253">By default this is set to `https://dc.services.visualstudio.com/api/profiles/{0}/appId`.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-253">By default this is set to `https://dc.services.visualstudio.com/api/profiles/{0}/appId`.</span></span>
<span data-ttu-id="f8a3f-254">If you need to configure a proxy for this configuration, we recommend proxying the base address and including "/api/profiles/{0}/appId".</span><span class="sxs-lookup"><span data-stu-id="f8a3f-254">If you need to configure a proxy for this configuration, we recommend proxying the base address and including "/api/profiles/{0}/appId".</span></span> <span data-ttu-id="f8a3f-255">Note that '{0}' is substituted at runtime per request with the Instrumentation Key.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-255">Note that '{0}' is substituted at runtime per request with the Instrumentation Key.</span></span>

#### <a name="example-configuration-via-applicationinsightsconfig"></a><span data-ttu-id="f8a3f-256">Example Configuration via ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-256">Example Configuration via ApplicationInsights.config:</span></span>
```xml
<ApplicationInsights>
    ...
    <ApplicationIdProvider Type="Microsoft.ApplicationInsights.Extensibility.Implementation.ApplicationId.ApplicationInsightsApplicationIdProvider, Microsoft.ApplicationInsights">
        <ProfileQueryEndpoint>https://dc.services.visualstudio.com/api/profiles/{0}/appId</ProfileQueryEndpoint>
    </ApplicationIdProvider>
    ...
</ApplicationInsights>
```

#### <a name="example-configuration-via-code"></a><span data-ttu-id="f8a3f-257">Example Configuration via code:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-257">Example Configuration via code:</span></span>
```csharp
TelemetryConfiguration.Active.ApplicationIdProvider = new ApplicationInsightsApplicationIdProvider();
```

### <a name="dictionaryapplicationidprovider"></a><span data-ttu-id="f8a3f-258">DictionaryApplicationIdProvider</span><span class="sxs-lookup"><span data-stu-id="f8a3f-258">DictionaryApplicationIdProvider</span></span>

<span data-ttu-id="f8a3f-259">This is a static provider, which will rely on your configured Instrumentation Key / Application ID pairs.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-259">This is a static provider, which will rely on your configured Instrumentation Key / Application ID pairs.</span></span>

<span data-ttu-id="f8a3f-260">This class has a property `Defined`, which is a Dictionary<string,string> of Instrumentation Key to Application ID pairs.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-260">This class has a property `Defined`, which is a Dictionary<string,string> of Instrumentation Key to Application ID pairs.</span></span>

<span data-ttu-id="f8a3f-261">This class has an optional property `Next` which can be used to configure another provider to use when an Instrumentation Key is requested that does not exist in your configuration.</span><span class="sxs-lookup"><span data-stu-id="f8a3f-261">This class has an optional property `Next` which can be used to configure another provider to use when an Instrumentation Key is requested that does not exist in your configuration.</span></span>

#### <a name="example-configuration-via-applicationinsightsconfig"></a><span data-ttu-id="f8a3f-262">Example Configuration via ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-262">Example Configuration via ApplicationInsights.config:</span></span>
```xml
<ApplicationInsights>
    ...
    <ApplicationIdProvider Type="Microsoft.ApplicationInsights.Extensibility.Implementation.ApplicationId.DictionaryApplicationIdProvider, Microsoft.ApplicationInsights">
        <Defined>
            <Type key="InstrumentationKey_1" value="ApplicationId_1"/>
            <Type key="InstrumentationKey_2" value="ApplicationId_2"/>
        </Defined>
        <Next Type="Microsoft.ApplicationInsights.Extensibility.Implementation.ApplicationId.ApplicationInsightsApplicationIdProvider, Microsoft.ApplicationInsights" />
    </ApplicationIdProvider>
    ...
</ApplicationInsights>
```

#### <a name="example-configuration-via-code"></a><span data-ttu-id="f8a3f-263">Example Configuration via code:</span><span class="sxs-lookup"><span data-stu-id="f8a3f-263">Example Configuration via code:</span></span>
```csharp
TelemetryConfiguration.Active.ApplicationIdProvider = new DictionaryApplicationIdProvider{
 Defined = new Dictionary<string, string>
    {
        {"InstrumentationKey_1", "ApplicationId_1"},
        {"InstrumentationKey_2", "ApplicationId_2"}
    }
};
```




## <a name="next-steps"></a><span data-ttu-id="f8a3f-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8a3f-264">Next steps</span></span>
<span data-ttu-id="f8a3f-265">[Learn more about the API][api].</span><span class="sxs-lookup"><span data-stu-id="f8a3f-265">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
