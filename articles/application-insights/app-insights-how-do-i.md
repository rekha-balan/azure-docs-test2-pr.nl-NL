---
title: How do I ... in Azure Application Insights | Microsoft Docs
description: FAQ in Application Insights.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 04/04/2017
ms.author: mbullwin
ms.openlocfilehash: 8cee346a45cd20e7dd677fd7f2efed5500175598
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783905"
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="60162-103">How do I ... in Application Insights?</span><span class="sxs-lookup"><span data-stu-id="60162-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="60162-104">Get an email when ...</span><span class="sxs-lookup"><span data-stu-id="60162-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="60162-105">Email if my site goes down</span><span class="sxs-lookup"><span data-stu-id="60162-105">Email if my site goes down</span></span>
<span data-ttu-id="60162-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="60162-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="60162-107">Email if my site is overloaded</span><span class="sxs-lookup"><span data-stu-id="60162-107">Email if my site is overloaded</span></span>
<span data-ttu-id="60162-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span><span class="sxs-lookup"><span data-stu-id="60162-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="60162-109">A threshold between 1 and 2 seconds should work.</span><span class="sxs-lookup"><span data-stu-id="60162-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="60162-110">Your app might also show signs of strain by returning failure codes.</span><span class="sxs-lookup"><span data-stu-id="60162-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="60162-111">Set an alert on **Failed requests**.</span><span class="sxs-lookup"><span data-stu-id="60162-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="60162-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span><span class="sxs-lookup"><span data-stu-id="60162-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="60162-113">Email on exceptions</span><span class="sxs-lookup"><span data-stu-id="60162-113">Email on exceptions</span></span>
1. [<span data-ttu-id="60162-114">Set up exception monitoring</span><span class="sxs-lookup"><span data-stu-id="60162-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="60162-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span><span class="sxs-lookup"><span data-stu-id="60162-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="60162-116">Email on an event in my app</span><span class="sxs-lookup"><span data-stu-id="60162-116">Email on an event in my app</span></span>
<span data-ttu-id="60162-117">Let's suppose you'd like to get an email when a specific event occurs.</span><span class="sxs-lookup"><span data-stu-id="60162-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="60162-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="60162-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="60162-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span><span class="sxs-lookup"><span data-stu-id="60162-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="60162-120">Write some code to increase a metric when the event occurs:</span><span class="sxs-lookup"><span data-stu-id="60162-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="60162-121">or:</span><span class="sxs-lookup"><span data-stu-id="60162-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="60162-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span><span class="sxs-lookup"><span data-stu-id="60162-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="60162-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span><span class="sxs-lookup"><span data-stu-id="60162-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="60162-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span><span class="sxs-lookup"><span data-stu-id="60162-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="60162-125">Set the averaging period to the minimum.</span><span class="sxs-lookup"><span data-stu-id="60162-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="60162-126">You'll get emails both when the metric goes above and below the threshold.</span><span class="sxs-lookup"><span data-stu-id="60162-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="60162-127">Some points to consider:</span><span class="sxs-lookup"><span data-stu-id="60162-127">Some points to consider:</span></span>

* <span data-ttu-id="60162-128">An alert has two states ("alert" and "healthy").</span><span class="sxs-lookup"><span data-stu-id="60162-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="60162-129">The state is evaluated only when a metric is received.</span><span class="sxs-lookup"><span data-stu-id="60162-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="60162-130">An email is sent only when the state changes.</span><span class="sxs-lookup"><span data-stu-id="60162-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="60162-131">This is why you have to send both high and low-value metrics.</span><span class="sxs-lookup"><span data-stu-id="60162-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="60162-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span><span class="sxs-lookup"><span data-stu-id="60162-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="60162-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span><span class="sxs-lookup"><span data-stu-id="60162-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="60162-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span><span class="sxs-lookup"><span data-stu-id="60162-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="60162-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span><span class="sxs-lookup"><span data-stu-id="60162-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="60162-136">Set up alerts automatically</span><span class="sxs-lookup"><span data-stu-id="60162-136">Set up alerts automatically</span></span>
[<span data-ttu-id="60162-137">Use PowerShell to create new alerts</span><span class="sxs-lookup"><span data-stu-id="60162-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="60162-138">Use PowerShell to Manage Application Insights</span><span class="sxs-lookup"><span data-stu-id="60162-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="60162-139">Create new resources</span><span class="sxs-lookup"><span data-stu-id="60162-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="60162-140">Create new alerts</span><span class="sxs-lookup"><span data-stu-id="60162-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="60162-141">Separate telemetry from different versions</span><span class="sxs-lookup"><span data-stu-id="60162-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="60162-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="60162-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="60162-143">Learn more</span><span class="sxs-lookup"><span data-stu-id="60162-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="60162-144">Separating development, test, and release versions: Use different Application Insights resources.</span><span class="sxs-lookup"><span data-stu-id="60162-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="60162-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="60162-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="60162-146">Reporting build versions: Add a property using a telemetry initializer.</span><span class="sxs-lookup"><span data-stu-id="60162-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="60162-147">Learn more</span><span class="sxs-lookup"><span data-stu-id="60162-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="60162-148">Monitor backend servers and desktop apps</span><span class="sxs-lookup"><span data-stu-id="60162-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="60162-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="60162-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="60162-150">Visualize data</span><span class="sxs-lookup"><span data-stu-id="60162-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="60162-151">Dashboard with metrics from multiple apps</span><span class="sxs-lookup"><span data-stu-id="60162-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="60162-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span><span class="sxs-lookup"><span data-stu-id="60162-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="60162-153">Pin it to the Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="60162-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="60162-154">Dashboard with data from other sources and Application Insights</span><span class="sxs-lookup"><span data-stu-id="60162-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="60162-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="60162-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="60162-156">Or</span><span class="sxs-lookup"><span data-stu-id="60162-156">Or</span></span>

* <span data-ttu-id="60162-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span><span class="sxs-lookup"><span data-stu-id="60162-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="60162-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="60162-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="60162-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span><span class="sxs-lookup"><span data-stu-id="60162-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="60162-160">Filter out anonymous or authenticated users</span><span class="sxs-lookup"><span data-stu-id="60162-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="60162-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span><span class="sxs-lookup"><span data-stu-id="60162-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="60162-162">You can then:</span><span class="sxs-lookup"><span data-stu-id="60162-162">You can then:</span></span>

* <span data-ttu-id="60162-163">Search on specific user ids</span><span class="sxs-lookup"><span data-stu-id="60162-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="60162-164">Filter metrics to either anonymous or authenticated users</span><span class="sxs-lookup"><span data-stu-id="60162-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="60162-165">Modify property names or values</span><span class="sxs-lookup"><span data-stu-id="60162-165">Modify property names or values</span></span>
<span data-ttu-id="60162-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="60162-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="60162-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60162-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="60162-168">List specific users and their usage</span><span class="sxs-lookup"><span data-stu-id="60162-168">List specific users and their usage</span></span>
<span data-ttu-id="60162-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="60162-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="60162-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span><span class="sxs-lookup"><span data-stu-id="60162-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="60162-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span><span class="sxs-lookup"><span data-stu-id="60162-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="60162-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span><span class="sxs-lookup"><span data-stu-id="60162-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="60162-173">To analyze page views, replace the standard JavaScript trackPageView call.</span><span class="sxs-lookup"><span data-stu-id="60162-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="60162-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span><span class="sxs-lookup"><span data-stu-id="60162-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="60162-175">You can then filter and segment metrics and searches on the user id.</span><span class="sxs-lookup"><span data-stu-id="60162-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="60162-176">Reduce traffic from my app to Application Insights</span><span class="sxs-lookup"><span data-stu-id="60162-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="60162-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span><span class="sxs-lookup"><span data-stu-id="60162-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="60162-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span><span class="sxs-lookup"><span data-stu-id="60162-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="60162-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span><span class="sxs-lookup"><span data-stu-id="60162-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="60162-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span><span class="sxs-lookup"><span data-stu-id="60162-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="60162-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span><span class="sxs-lookup"><span data-stu-id="60162-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="60162-182">There's an overload of TrackMetric() that provides for that.</span><span class="sxs-lookup"><span data-stu-id="60162-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="60162-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="60162-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="60162-184">Disable telemetry</span><span class="sxs-lookup"><span data-stu-id="60162-184">Disable telemetry</span></span>
<span data-ttu-id="60162-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span><span class="sxs-lookup"><span data-stu-id="60162-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="60162-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span><span class="sxs-lookup"><span data-stu-id="60162-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="60162-187">View system performance counters</span><span class="sxs-lookup"><span data-stu-id="60162-187">View system performance counters</span></span>
<span data-ttu-id="60162-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span><span class="sxs-lookup"><span data-stu-id="60162-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="60162-189">There's a predefined blade titled **Servers** that displays several of them.</span><span class="sxs-lookup"><span data-stu-id="60162-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Open your Application Insights resource and click Servers](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="60162-191">If you see no performance counter data</span><span class="sxs-lookup"><span data-stu-id="60162-191">If you see no performance counter data</span></span>
* <span data-ttu-id="60162-192">**IIS server** on your own machine or on a VM.</span><span class="sxs-lookup"><span data-stu-id="60162-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="60162-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="60162-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="60162-194">**Azure web site** - we don't support performance counters yet.</span><span class="sxs-lookup"><span data-stu-id="60162-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="60162-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span><span class="sxs-lookup"><span data-stu-id="60162-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="60162-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="60162-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="60162-197">To display more performance counters</span><span class="sxs-lookup"><span data-stu-id="60162-197">To display more performance counters</span></span>
* <span data-ttu-id="60162-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span><span class="sxs-lookup"><span data-stu-id="60162-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="60162-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="60162-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
