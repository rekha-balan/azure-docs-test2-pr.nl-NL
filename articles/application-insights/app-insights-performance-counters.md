---
title: Performance counters in Application Insights | Microsoft Docs
description: Monitor system and custom .NET performance counters in Application Insights.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: awills
ms.openlocfilehash: 7cfef0507a143e4d8da512e7ad5f84dc01f732bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564190"
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="46a3a-103">System performance counters in Application Insights</span><span class="sxs-lookup"><span data-stu-id="46a3a-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="46a3a-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span><span class="sxs-lookup"><span data-stu-id="46a3a-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="46a3a-105">You can also define your own.</span><span class="sxs-lookup"><span data-stu-id="46a3a-105">You can also define your own.</span></span> <span data-ttu-id="46a3a-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span><span class="sxs-lookup"><span data-stu-id="46a3a-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="46a3a-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span><span class="sxs-lookup"><span data-stu-id="46a3a-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="46a3a-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span><span class="sxs-lookup"><span data-stu-id="46a3a-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Performance counters reported in Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="46a3a-110">(Performance counters aren't available for Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="46a3a-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="46a3a-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="46a3a-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="configure"></a><span data-ttu-id="46a3a-112">Configure</span><span class="sxs-lookup"><span data-stu-id="46a3a-112">Configure</span></span>
<span data-ttu-id="46a3a-113">If Application Insights Status Monitor isn't yet installed on your server machines, you need to install it to see performance counters.</span><span class="sxs-lookup"><span data-stu-id="46a3a-113">If Application Insights Status Monitor isn't yet installed on your server machines, you need to install it to see performance counters.</span></span>

<span data-ttu-id="46a3a-114">Download and run [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) on each server instance.</span><span class="sxs-lookup"><span data-stu-id="46a3a-114">Download and run [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) on each server instance.</span></span> <span data-ttu-id="46a3a-115">If it's already installed, you don't need to install it again.</span><span class="sxs-lookup"><span data-stu-id="46a3a-115">If it's already installed, you don't need to install it again.</span></span>

* <span data-ttu-id="46a3a-116">*I [installed the Application Insights SDK in my app](app-insights-asp-net.md) during development. Do I still need Status Monitor?*</span><span class="sxs-lookup"><span data-stu-id="46a3a-116">*I [installed the Application Insights SDK in my app](app-insights-asp-net.md) during development. Do I still need Status Monitor?*</span></span>
  
    <span data-ttu-id="46a3a-117">Yes, Status Monitor is required to collect performance counters for ASP.NET web apps.</span><span class="sxs-lookup"><span data-stu-id="46a3a-117">Yes, Status Monitor is required to collect performance counters for ASP.NET web apps.</span></span> <span data-ttu-id="46a3a-118">As you might already know, Status Monitor can also be used to [monitor web apps that are already live](app-insights-monitor-performance-live-website-now.md), without installing the SDK during development.</span><span class="sxs-lookup"><span data-stu-id="46a3a-118">As you might already know, Status Monitor can also be used to [monitor web apps that are already live](app-insights-monitor-performance-live-website-now.md), without installing the SDK during development.</span></span>

## <a name="view-counters"></a><span data-ttu-id="46a3a-119">View counters</span><span class="sxs-lookup"><span data-stu-id="46a3a-119">View counters</span></span>
<span data-ttu-id="46a3a-120">The Servers blade shows a default set of performance counters.</span><span class="sxs-lookup"><span data-stu-id="46a3a-120">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="46a3a-121">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span><span class="sxs-lookup"><span data-stu-id="46a3a-121">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="46a3a-122">The available counters are listed as metrics when you edit a chart.</span><span class="sxs-lookup"><span data-stu-id="46a3a-122">The available counters are listed as metrics when you edit a chart.</span></span>

![Performance counters reported in Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="46a3a-124">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span><span class="sxs-lookup"><span data-stu-id="46a3a-124">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="46a3a-125">Add counters</span><span class="sxs-lookup"><span data-stu-id="46a3a-125">Add counters</span></span>
<span data-ttu-id="46a3a-126">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span><span class="sxs-lookup"><span data-stu-id="46a3a-126">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="46a3a-127">You can configure it to do so.</span><span class="sxs-lookup"><span data-stu-id="46a3a-127">You can configure it to do so.</span></span>

1. <span data-ttu-id="46a3a-128">Find out what counters are available in your server by using this PowerShell command at the server:</span><span class="sxs-lookup"><span data-stu-id="46a3a-128">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="46a3a-129">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="46a3a-129">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="46a3a-130">Open ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="46a3a-130">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="46a3a-131">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span><span class="sxs-lookup"><span data-stu-id="46a3a-131">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="46a3a-132">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span><span class="sxs-lookup"><span data-stu-id="46a3a-132">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="46a3a-133">Update it there in each server instance.</span><span class="sxs-lookup"><span data-stu-id="46a3a-133">Update it there in each server instance.</span></span>
3. <span data-ttu-id="46a3a-134">Edit the performance collector directive:</span><span class="sxs-lookup"><span data-stu-id="46a3a-134">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="46a3a-135">You can capture both standard counters and those you have implemented yourself.</span><span class="sxs-lookup"><span data-stu-id="46a3a-135">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="46a3a-136">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span><span class="sxs-lookup"><span data-stu-id="46a3a-136">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="46a3a-137">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span><span class="sxs-lookup"><span data-stu-id="46a3a-137">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="46a3a-138">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="46a3a-138">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="46a3a-139">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span><span class="sxs-lookup"><span data-stu-id="46a3a-139">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="46a3a-140">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span><span class="sxs-lookup"><span data-stu-id="46a3a-140">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="46a3a-141">Collecting performance counters in code</span><span class="sxs-lookup"><span data-stu-id="46a3a-141">Collecting performance counters in code</span></span>
<span data-ttu-id="46a3a-142">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span><span class="sxs-lookup"><span data-stu-id="46a3a-142">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="46a3a-143">Or you can do the same thing with custom metrics you created:</span><span class="sxs-lookup"><span data-stu-id="46a3a-143">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="46a3a-144">Performance counters in Analytics</span><span class="sxs-lookup"><span data-stu-id="46a3a-144">Performance counters in Analytics</span></span>
<span data-ttu-id="46a3a-145">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="46a3a-145">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="46a3a-146">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span><span class="sxs-lookup"><span data-stu-id="46a3a-146">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="46a3a-147">In the telemetry for each application, you’ll see only the counters for that application.</span><span class="sxs-lookup"><span data-stu-id="46a3a-147">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="46a3a-148">For example, to see what counters are available:</span><span class="sxs-lookup"><span data-stu-id="46a3a-148">For example, to see what counters are available:</span></span> 

![Performance counters in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="46a3a-150">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span><span class="sxs-lookup"><span data-stu-id="46a3a-150">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="46a3a-151">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span><span class="sxs-lookup"><span data-stu-id="46a3a-151">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="46a3a-152">To get a chart of available memory over the recent period:</span><span class="sxs-lookup"><span data-stu-id="46a3a-152">To get a chart of available memory over the recent period:</span></span> 

![Memory timechart in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="46a3a-154">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span><span class="sxs-lookup"><span data-stu-id="46a3a-154">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="46a3a-155">For example, to compare the performance of your app on the different machines:</span><span class="sxs-lookup"><span data-stu-id="46a3a-155">For example, to compare the performance of your app on the different machines:</span></span> 

![Performance segmented by role instance in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="46a3a-157">ASP.NET and Application Insights counts</span><span class="sxs-lookup"><span data-stu-id="46a3a-157">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="46a3a-158">*What's the difference between the Exception rate and Exceptions metrics?*</span><span class="sxs-lookup"><span data-stu-id="46a3a-158">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="46a3a-159">*Exception rate* is a system performance counter.</span><span class="sxs-lookup"><span data-stu-id="46a3a-159">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="46a3a-160">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span><span class="sxs-lookup"><span data-stu-id="46a3a-160">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="46a3a-161">The Application Insights SDK collects this result and sends it to the portal.</span><span class="sxs-lookup"><span data-stu-id="46a3a-161">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="46a3a-162">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span><span class="sxs-lookup"><span data-stu-id="46a3a-162">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="46a3a-163">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="46a3a-163">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="46a3a-164">Alerts</span><span class="sxs-lookup"><span data-stu-id="46a3a-164">Alerts</span></span>
<span data-ttu-id="46a3a-165">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span><span class="sxs-lookup"><span data-stu-id="46a3a-165">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="46a3a-166">Open the Alerts blade and click Add Alert.</span><span class="sxs-lookup"><span data-stu-id="46a3a-166">Open the Alerts blade and click Add Alert.</span></span>

## <a name="next"></a><span data-ttu-id="46a3a-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="46a3a-167">Next steps</span></span>
* [<span data-ttu-id="46a3a-168">Dependency tracking</span><span class="sxs-lookup"><span data-stu-id="46a3a-168">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="46a3a-169">Exception tracking</span><span class="sxs-lookup"><span data-stu-id="46a3a-169">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)






