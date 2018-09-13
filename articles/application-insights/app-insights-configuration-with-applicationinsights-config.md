---
title: ApplicationInsights.config reference - Azure | Microsoft Docs
description: Enable or disable data collection modules, and add performance counters and other parameters.
services: application-insights
documentationcenter: ''
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: douge
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/12/2016
ms.author: awills
ms.openlocfilehash: a43eca9878881731f54dc1ec3bc8a9cd15bf2c5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670170"
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="626b6-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span><span class="sxs-lookup"><span data-stu-id="626b6-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="626b6-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="626b6-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="626b6-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span><span class="sxs-lookup"><span data-stu-id="626b6-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="626b6-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span><span class="sxs-lookup"><span data-stu-id="626b6-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="626b6-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span><span class="sxs-lookup"><span data-stu-id="626b6-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="626b6-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span><span class="sxs-lookup"><span data-stu-id="626b6-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="626b6-109">It is automatically added to your project when you [install most versions of the SDK][start].</span><span class="sxs-lookup"><span data-stu-id="626b6-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="626b6-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="626b6-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="626b6-111">There isn't an equivalent file to control the [SDK in a web page][client].</span><span class="sxs-lookup"><span data-stu-id="626b6-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="626b6-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span><span class="sxs-lookup"><span data-stu-id="626b6-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="626b6-113">Telemetry Modules (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="626b6-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="626b6-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span><span class="sxs-lookup"><span data-stu-id="626b6-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="626b6-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span><span class="sxs-lookup"><span data-stu-id="626b6-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="626b6-116">There's a node in the configuration file for each module.</span><span class="sxs-lookup"><span data-stu-id="626b6-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="626b6-117">To disable a module, delete the node or comment it out.</span><span class="sxs-lookup"><span data-stu-id="626b6-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="626b6-118">Dependency Tracking</span><span class="sxs-lookup"><span data-stu-id="626b6-118">Dependency Tracking</span></span>
<span data-ttu-id="626b6-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span><span class="sxs-lookup"><span data-stu-id="626b6-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="626b6-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="626b6-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="626b6-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="626b6-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="626b6-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="626b6-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="626b6-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="626b6-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="626b6-124">Performance collector</span><span class="sxs-lookup"><span data-stu-id="626b6-124">Performance collector</span></span>
<span data-ttu-id="626b6-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span><span class="sxs-lookup"><span data-stu-id="626b6-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="626b6-126">You can specify which counters to collect, including performance counters you have set up yourself.</span><span class="sxs-lookup"><span data-stu-id="626b6-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="626b6-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="626b6-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="626b6-128">Application Insights Diagnostics Telemetry</span><span class="sxs-lookup"><span data-stu-id="626b6-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="626b6-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span><span class="sxs-lookup"><span data-stu-id="626b6-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="626b6-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span><span class="sxs-lookup"><span data-stu-id="626b6-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="626b6-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="626b6-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="626b6-132">Sends diagnostic data to dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="626b6-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="626b6-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="626b6-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="626b6-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span><span class="sxs-lookup"><span data-stu-id="626b6-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="626b6-135">Developer Mode</span><span class="sxs-lookup"><span data-stu-id="626b6-135">Developer Mode</span></span>
<span data-ttu-id="626b6-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span><span class="sxs-lookup"><span data-stu-id="626b6-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="626b6-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="626b6-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="626b6-138">It causes significant overhead in CPU and network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="626b6-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="626b6-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span><span class="sxs-lookup"><span data-stu-id="626b6-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="626b6-140">Web Request Tracking</span><span class="sxs-lookup"><span data-stu-id="626b6-140">Web Request Tracking</span></span>
<span data-ttu-id="626b6-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="626b6-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="626b6-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span><span class="sxs-lookup"><span data-stu-id="626b6-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="626b6-143">Exception tracking</span><span class="sxs-lookup"><span data-stu-id="626b6-143">Exception tracking</span></span>
<span data-ttu-id="626b6-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span><span class="sxs-lookup"><span data-stu-id="626b6-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="626b6-145">See [Failures and exceptions][exceptions].</span><span class="sxs-lookup"><span data-stu-id="626b6-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="626b6-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span><span class="sxs-lookup"><span data-stu-id="626b6-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="626b6-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="626b6-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="626b6-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span><span class="sxs-lookup"><span data-stu-id="626b6-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="626b6-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="626b6-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="626b6-150">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="626b6-150">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="626b6-151">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span><span class="sxs-lookup"><span data-stu-id="626b6-151">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="626b6-152">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="626b6-152">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="626b6-153">No entry in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="626b6-153">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="626b6-154">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="626b6-154">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="626b6-155">If you just install this NuGet, no .config file is generated.</span><span class="sxs-lookup"><span data-stu-id="626b6-155">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="626b6-156">Telemetry Channel</span><span class="sxs-lookup"><span data-stu-id="626b6-156">Telemetry Channel</span></span>
<span data-ttu-id="626b6-157">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="626b6-157">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="626b6-158">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span><span class="sxs-lookup"><span data-stu-id="626b6-158">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="626b6-159">It buffers data in memory.</span><span class="sxs-lookup"><span data-stu-id="626b6-159">It buffers data in memory.</span></span>
* <span data-ttu-id="626b6-160">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span><span class="sxs-lookup"><span data-stu-id="626b6-160">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="626b6-161">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span><span class="sxs-lookup"><span data-stu-id="626b6-161">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="626b6-162">Telemetry Initializers (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="626b6-162">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="626b6-163">Telemetry initializers set context properties that are sent along with every item of telemetry.</span><span class="sxs-lookup"><span data-stu-id="626b6-163">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="626b6-164">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span><span class="sxs-lookup"><span data-stu-id="626b6-164">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="626b6-165">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="626b6-165">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="626b6-166">`AccountIdTelemetryInitializer` sets the AccountId property.</span><span class="sxs-lookup"><span data-stu-id="626b6-166">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="626b6-167">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="626b6-167">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="626b6-168">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span><span class="sxs-lookup"><span data-stu-id="626b6-168">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="626b6-169">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span><span class="sxs-lookup"><span data-stu-id="626b6-169">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="626b6-170">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span><span class="sxs-lookup"><span data-stu-id="626b6-170">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="626b6-171">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span><span class="sxs-lookup"><span data-stu-id="626b6-171">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="626b6-172">`Type` is set to "PC"</span><span class="sxs-lookup"><span data-stu-id="626b6-172">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="626b6-173">`Id` is set to the domain name of the computer where the web application is running.</span><span class="sxs-lookup"><span data-stu-id="626b6-173">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="626b6-174">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span><span class="sxs-lookup"><span data-stu-id="626b6-174">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="626b6-175">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span><span class="sxs-lookup"><span data-stu-id="626b6-175">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="626b6-176">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="626b6-176">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="626b6-177">`Language` is set to the name of the `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="626b6-177">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="626b6-178">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span><span class="sxs-lookup"><span data-stu-id="626b6-178">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="626b6-179">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span><span class="sxs-lookup"><span data-stu-id="626b6-179">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="626b6-180">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="626b6-180">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="626b6-181">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span><span class="sxs-lookup"><span data-stu-id="626b6-181">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="626b6-182">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span><span class="sxs-lookup"><span data-stu-id="626b6-182">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="626b6-183">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span><span class="sxs-lookup"><span data-stu-id="626b6-183">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="626b6-184">The `<Filters>` set identifying properties of the requests.</span><span class="sxs-lookup"><span data-stu-id="626b6-184">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="626b6-185">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span><span class="sxs-lookup"><span data-stu-id="626b6-185">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="626b6-186">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span><span class="sxs-lookup"><span data-stu-id="626b6-186">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="626b6-187">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="626b6-187">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="626b6-188">The `<Filters>` set identifying properties of the requests.</span><span class="sxs-lookup"><span data-stu-id="626b6-188">The `<Filters>` set identifying properties of the requests.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="626b6-189">Telemetry Processors (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="626b6-189">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="626b6-190">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span><span class="sxs-lookup"><span data-stu-id="626b6-190">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="626b6-191">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="626b6-191">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="626b6-192">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="626b6-192">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="626b6-193">This is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="626b6-193">This is enabled by default.</span></span> <span data-ttu-id="626b6-194">If your app sends a lot of telemetry, this processor removes some of it.</span><span class="sxs-lookup"><span data-stu-id="626b6-194">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="626b6-195">The parameter provides the target that the algorithm tries to achieve.</span><span class="sxs-lookup"><span data-stu-id="626b6-195">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="626b6-196">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span><span class="sxs-lookup"><span data-stu-id="626b6-196">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="626b6-197">[Learn more about sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="626b6-197">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="626b6-198">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="626b6-198">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="626b6-199">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="626b6-199">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="626b6-200">Channel parameters (Java)</span><span class="sxs-lookup"><span data-stu-id="626b6-200">Channel parameters (Java)</span></span>
<span data-ttu-id="626b6-201">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span><span class="sxs-lookup"><span data-stu-id="626b6-201">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="626b6-202">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="626b6-202">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="626b6-203">The number of telemetry items that can be stored in the SDK's in-memory storage.</span><span class="sxs-lookup"><span data-stu-id="626b6-203">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="626b6-204">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span><span class="sxs-lookup"><span data-stu-id="626b6-204">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="626b6-205">Min: 1</span><span class="sxs-lookup"><span data-stu-id="626b6-205">Min: 1</span></span>
* <span data-ttu-id="626b6-206">Max: 1000</span><span class="sxs-lookup"><span data-stu-id="626b6-206">Max: 1000</span></span>
* <span data-ttu-id="626b6-207">Default: 500</span><span class="sxs-lookup"><span data-stu-id="626b6-207">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="626b6-208">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="626b6-208">FlushIntervalInSeconds</span></span>
<span data-ttu-id="626b6-209">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span><span class="sxs-lookup"><span data-stu-id="626b6-209">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="626b6-210">Min: 1</span><span class="sxs-lookup"><span data-stu-id="626b6-210">Min: 1</span></span>
* <span data-ttu-id="626b6-211">Max: 300</span><span class="sxs-lookup"><span data-stu-id="626b6-211">Max: 300</span></span>
* <span data-ttu-id="626b6-212">Default: 5</span><span class="sxs-lookup"><span data-stu-id="626b6-212">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="626b6-213">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="626b6-213">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="626b6-214">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span><span class="sxs-lookup"><span data-stu-id="626b6-214">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="626b6-215">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span><span class="sxs-lookup"><span data-stu-id="626b6-215">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="626b6-216">When the storage size has been met, new telemetry items will be discarded.</span><span class="sxs-lookup"><span data-stu-id="626b6-216">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="626b6-217">Min: 1</span><span class="sxs-lookup"><span data-stu-id="626b6-217">Min: 1</span></span>
* <span data-ttu-id="626b6-218">Max: 100</span><span class="sxs-lookup"><span data-stu-id="626b6-218">Max: 100</span></span>
* <span data-ttu-id="626b6-219">Default: 10</span><span class="sxs-lookup"><span data-stu-id="626b6-219">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="626b6-220">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="626b6-220">InstrumentationKey</span></span>
<span data-ttu-id="626b6-221">This determines the Application Insights resource in which your data appears.</span><span class="sxs-lookup"><span data-stu-id="626b6-221">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="626b6-222">Typically you create a separate resource, with a separate key, for each of your applications.</span><span class="sxs-lookup"><span data-stu-id="626b6-222">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="626b6-223">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span><span class="sxs-lookup"><span data-stu-id="626b6-223">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="626b6-224">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="626b6-224">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="626b6-225">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span><span class="sxs-lookup"><span data-stu-id="626b6-225">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="626b6-226">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span><span class="sxs-lookup"><span data-stu-id="626b6-226">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="626b6-227">To get a new key, [create a new resource in the Application Insights portal][new].</span><span class="sxs-lookup"><span data-stu-id="626b6-227">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="626b6-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="626b6-228">Next steps</span></span>
<span data-ttu-id="626b6-229">[Learn more about the API][api].</span><span class="sxs-lookup"><span data-stu-id="626b6-229">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
