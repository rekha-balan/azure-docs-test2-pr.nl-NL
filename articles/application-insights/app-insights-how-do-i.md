---
title: How do I ... in Azure Application Insights | Microsoft Docs
description: FAQ in Application Insights.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: awills
ms.openlocfilehash: 0c239814089734b1a4cba76254a1bdb025375f72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552300"
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="456a4-103">How do I ... in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="456a4-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="456a4-104">Get an email when ...</span><span class="sxs-lookup"><span data-stu-id="456a4-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="456a4-105">Email if my site goes down</span><span class="sxs-lookup"><span data-stu-id="456a4-105">Email if my site goes down</span></span>
<span data-ttu-id="456a4-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="456a4-107">Email if my site is overloaded</span><span class="sxs-lookup"><span data-stu-id="456a4-107">Email if my site is overloaded</span></span>
<span data-ttu-id="456a4-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span><span class="sxs-lookup"><span data-stu-id="456a4-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="456a4-109">A threshold between 1 and 2 seconds should work.</span><span class="sxs-lookup"><span data-stu-id="456a4-109">A threshold between 1 and 2 seconds should work.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="456a4-110">Your app might also show signs of strain by returning failure codes.</span><span class="sxs-lookup"><span data-stu-id="456a4-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="456a4-111">Set an alert on **Failed requests**.</span><span class="sxs-lookup"><span data-stu-id="456a4-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="456a4-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span><span class="sxs-lookup"><span data-stu-id="456a4-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="456a4-113">Email on exceptions</span><span class="sxs-lookup"><span data-stu-id="456a4-113">Email on exceptions</span></span>
1. [<span data-ttu-id="456a4-114">Set up exception monitoring</span><span class="sxs-lookup"><span data-stu-id="456a4-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="456a4-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span><span class="sxs-lookup"><span data-stu-id="456a4-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="456a4-116">Email on an event in my app</span><span class="sxs-lookup"><span data-stu-id="456a4-116">Email on an event in my app</span></span>
<span data-ttu-id="456a4-117">Let's suppose you'd like to get an email when a specific event occurs.</span><span class="sxs-lookup"><span data-stu-id="456a4-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="456a4-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="456a4-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span><span class="sxs-lookup"><span data-stu-id="456a4-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="456a4-120">Write some code to increase a metric when the event occurs:</span><span class="sxs-lookup"><span data-stu-id="456a4-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="456a4-121">or:</span><span class="sxs-lookup"><span data-stu-id="456a4-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="456a4-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span><span class="sxs-lookup"><span data-stu-id="456a4-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="456a4-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span><span class="sxs-lookup"><span data-stu-id="456a4-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="456a4-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span><span class="sxs-lookup"><span data-stu-id="456a4-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="456a4-125">Set the averaging period to the minimum.</span><span class="sxs-lookup"><span data-stu-id="456a4-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="456a4-126">You'll get emails both when the metric goes above and below the threshold.</span><span class="sxs-lookup"><span data-stu-id="456a4-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="456a4-127">Some points to consider:</span><span class="sxs-lookup"><span data-stu-id="456a4-127">Some points to consider:</span></span>

* <span data-ttu-id="456a4-128">An alert has two states ("alert" and "healthy").</span><span class="sxs-lookup"><span data-stu-id="456a4-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="456a4-129">The state is evaluated only when a metric is received.</span><span class="sxs-lookup"><span data-stu-id="456a4-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="456a4-130">An email is sent only when the state changes.</span><span class="sxs-lookup"><span data-stu-id="456a4-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="456a4-131">This is why you have to send both high and low-value metrics.</span><span class="sxs-lookup"><span data-stu-id="456a4-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="456a4-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span><span class="sxs-lookup"><span data-stu-id="456a4-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="456a4-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span><span class="sxs-lookup"><span data-stu-id="456a4-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="456a4-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span><span class="sxs-lookup"><span data-stu-id="456a4-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="456a4-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span><span class="sxs-lookup"><span data-stu-id="456a4-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="456a4-136">Set up alerts automatically</span><span class="sxs-lookup"><span data-stu-id="456a4-136">Set up alerts automatically</span></span>
[<span data-ttu-id="456a4-137">Use PowerShell to create new alerts</span><span class="sxs-lookup"><span data-stu-id="456a4-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="456a4-138">Use PowerShell to Manage Application Insights</span><span class="sxs-lookup"><span data-stu-id="456a4-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="456a4-139">Create new resources</span><span class="sxs-lookup"><span data-stu-id="456a4-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="456a4-140">Create new alerts</span><span class="sxs-lookup"><span data-stu-id="456a4-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="application-versions-and-stamps"></a><span data-ttu-id="456a4-141">Application versions and stamps</span><span class="sxs-lookup"><span data-stu-id="456a4-141">Application versions and stamps</span></span>
### <a name="separate-the-results-from-dev-test-and-prod"></a><span data-ttu-id="456a4-142">Separate the results from dev, test and prod</span><span class="sxs-lookup"><span data-stu-id="456a4-142">Separate the results from dev, test and prod</span></span>
* <span data-ttu-id="456a4-143">For different environmnents, set up different ikeys</span><span class="sxs-lookup"><span data-stu-id="456a4-143">For different environmnents, set up different ikeys</span></span>
* <span data-ttu-id="456a4-144">For different stamps (dev, test, prod) tag the telemetry with different property values</span><span class="sxs-lookup"><span data-stu-id="456a4-144">For different stamps (dev, test, prod) tag the telemetry with different property values</span></span>

[<span data-ttu-id="456a4-145">Learn more</span><span class="sxs-lookup"><span data-stu-id="456a4-145">Learn more</span></span>](app-insights-separate-resources.md)

### <a name="filter-on-build-number"></a><span data-ttu-id="456a4-146">Filter on build number</span><span class="sxs-lookup"><span data-stu-id="456a4-146">Filter on build number</span></span>
<span data-ttu-id="456a4-147">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span><span class="sxs-lookup"><span data-stu-id="456a4-147">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="456a4-148">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span><span class="sxs-lookup"><span data-stu-id="456a4-148">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/050-filter.png)

<span data-ttu-id="456a4-149">There are several different methods of setting the Application Version property.</span><span class="sxs-lookup"><span data-stu-id="456a4-149">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="456a4-150">Set directly:</span><span class="sxs-lookup"><span data-stu-id="456a4-150">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="456a4-151">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span><span class="sxs-lookup"><span data-stu-id="456a4-151">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="456a4-152">[ASP.NET] Set the version in `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="456a4-152">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="456a4-153">The web module will pick up the version from the BuildLabel node.</span><span class="sxs-lookup"><span data-stu-id="456a4-153">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="456a4-154">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="456a4-154">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="456a4-155">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span><span class="sxs-lookup"><span data-stu-id="456a4-155">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="456a4-156">To do this, add a few lines to your .csproj file:</span><span class="sxs-lookup"><span data-stu-id="456a4-156">To do this, add a few lines to your .csproj file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="456a4-157">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="456a4-157">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="456a4-158">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="456a4-158">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="456a4-159">But when built with MSBuild, it is populated with the correct version number.</span><span class="sxs-lookup"><span data-stu-id="456a4-159">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="456a4-160">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="456a4-160">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="456a4-161">Monitor backend servers and desktop apps</span><span class="sxs-lookup"><span data-stu-id="456a4-161">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="456a4-162">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-162">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="456a4-163">Visualize data</span><span class="sxs-lookup"><span data-stu-id="456a4-163">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="456a4-164">Dashboard with metrics from multiple apps</span><span class="sxs-lookup"><span data-stu-id="456a4-164">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="456a4-165">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span><span class="sxs-lookup"><span data-stu-id="456a4-165">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="456a4-166">Pin it to the Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="456a4-166">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="456a4-167">Dashboard with data from other sources and Application Insights</span><span class="sxs-lookup"><span data-stu-id="456a4-167">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="456a4-168">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-168">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="456a4-169">Or</span><span class="sxs-lookup"><span data-stu-id="456a4-169">Or</span></span>

* <span data-ttu-id="456a4-170">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span><span class="sxs-lookup"><span data-stu-id="456a4-170">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="456a4-171">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-171">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="456a4-172">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span><span class="sxs-lookup"><span data-stu-id="456a4-172">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="456a4-173">Filter out anonymous or authenticated users</span><span class="sxs-lookup"><span data-stu-id="456a4-173">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="456a4-174">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span><span class="sxs-lookup"><span data-stu-id="456a4-174">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="456a4-175">You can then:</span><span class="sxs-lookup"><span data-stu-id="456a4-175">You can then:</span></span>

* <span data-ttu-id="456a4-176">Search on specific user ids</span><span class="sxs-lookup"><span data-stu-id="456a4-176">Search on specific user ids</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="456a4-177">Filter metrics to either anonymous or authenticated users</span><span class="sxs-lookup"><span data-stu-id="456a4-177">Filter metrics to either anonymous or authenticated users</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="456a4-178">Modify property names or values</span><span class="sxs-lookup"><span data-stu-id="456a4-178">Modify property names or values</span></span>
<span data-ttu-id="456a4-179">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="456a4-179">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="456a4-180">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="456a4-180">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="456a4-181">List specific users and their usage</span><span class="sxs-lookup"><span data-stu-id="456a4-181">List specific users and their usage</span></span>
<span data-ttu-id="456a4-182">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="456a4-182">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="456a4-183">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span><span class="sxs-lookup"><span data-stu-id="456a4-183">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="456a4-184">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span><span class="sxs-lookup"><span data-stu-id="456a4-184">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="456a4-185">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span><span class="sxs-lookup"><span data-stu-id="456a4-185">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="456a4-186">To analyze page views, replace the standard JavaScript trackPageView call.</span><span class="sxs-lookup"><span data-stu-id="456a4-186">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="456a4-187">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span><span class="sxs-lookup"><span data-stu-id="456a4-187">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="456a4-188">You can then filter and segment metrics and searches on the user id.</span><span class="sxs-lookup"><span data-stu-id="456a4-188">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="456a4-189">Reduce traffic from my app to Application Insights</span><span class="sxs-lookup"><span data-stu-id="456a4-189">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="456a4-190">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span><span class="sxs-lookup"><span data-stu-id="456a4-190">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="456a4-191">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span><span class="sxs-lookup"><span data-stu-id="456a4-191">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="456a4-192">In your web pages, Limit the number of Ajax calls reported for every page view.</span><span class="sxs-lookup"><span data-stu-id="456a4-192">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="456a4-193">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span><span class="sxs-lookup"><span data-stu-id="456a4-193">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="456a4-194">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span><span class="sxs-lookup"><span data-stu-id="456a4-194">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="456a4-195">There's an overload of TrackMetric() that provides for that.</span><span class="sxs-lookup"><span data-stu-id="456a4-195">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="456a4-196">Learn more about [pricing and quotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-196">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="456a4-197">Disable telemetry</span><span class="sxs-lookup"><span data-stu-id="456a4-197">Disable telemetry</span></span>
<span data-ttu-id="456a4-198">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span><span class="sxs-lookup"><span data-stu-id="456a4-198">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="456a4-199">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span><span class="sxs-lookup"><span data-stu-id="456a4-199">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="456a4-200">View system performance counters</span><span class="sxs-lookup"><span data-stu-id="456a4-200">View system performance counters</span></span>
<span data-ttu-id="456a4-201">Among the metrics you can show in metrics explorer are a set of system performance counters.</span><span class="sxs-lookup"><span data-stu-id="456a4-201">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="456a4-202">There's a predefined blade titled **Servers** that displays several of them.</span><span class="sxs-lookup"><span data-stu-id="456a4-202">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Open your Application Insights resource and click Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="456a4-204">If you see no performance counter data</span><span class="sxs-lookup"><span data-stu-id="456a4-204">If you see no performance counter data</span></span>
* <span data-ttu-id="456a4-205">**IIS server** on your own machine or on a VM.</span><span class="sxs-lookup"><span data-stu-id="456a4-205">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="456a4-206">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-206">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="456a4-207">**Azure web site** - we don't support performance counters yet.</span><span class="sxs-lookup"><span data-stu-id="456a4-207">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="456a4-208">There are several metrics you can get as a standard part of the Azure web site control panel.</span><span class="sxs-lookup"><span data-stu-id="456a4-208">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="456a4-209">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="456a4-209">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="456a4-210">To display more performance counters</span><span class="sxs-lookup"><span data-stu-id="456a4-210">To display more performance counters</span></span>
* <span data-ttu-id="456a4-211">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span><span class="sxs-lookup"><span data-stu-id="456a4-211">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="456a4-212">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-212">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="456a4-213">Version and release tracking</span><span class="sxs-lookup"><span data-stu-id="456a4-213">Version and release tracking</span></span>
<span data-ttu-id="456a4-214">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span><span class="sxs-lookup"><span data-stu-id="456a4-214">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="456a4-215">In your .csproj file, add:</span><span class="sxs-lookup"><span data-stu-id="456a4-215">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="456a4-216">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span><span class="sxs-lookup"><span data-stu-id="456a4-216">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="456a4-217">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="456a4-217">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="456a4-218">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="456a4-218">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="456a4-219">Release annotations</span><span class="sxs-lookup"><span data-stu-id="456a4-219">Release annotations</span></span>
<span data-ttu-id="456a4-220">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span><span class="sxs-lookup"><span data-stu-id="456a4-220">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="456a4-221">The following image shows how this marker appears.</span><span class="sxs-lookup"><span data-stu-id="456a4-221">The following image shows how this marker appears.</span></span>

![Screenshot of sample release annotation on a chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/release-annotation.png)







