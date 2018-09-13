---
title: Application Insights API for custom events and metrics | Microsoft Docs
description: Insert a few lines of code in your device or desktop app, webpage, or service, to track usage and diagnose issues.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/31/2017
ms.author: awills
ms.openlocfilehash: 633d7b4cf5fb06f6673abad6f1694e8a050553fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553471"
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="1f9ce-103">Application Insights API for custom events and metrics</span><span class="sxs-lookup"><span data-stu-id="1f9ce-103">Application Insights API for custom events and metrics</span></span>


<span data-ttu-id="1f9ce-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="1f9ce-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="1f9ce-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="1f9ce-107">This API is the same API that the standard Application Insights data collectors use.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="1f9ce-108">API summary</span><span class="sxs-lookup"><span data-stu-id="1f9ce-108">API summary</span></span>
<span data-ttu-id="1f9ce-109">The API is uniform across all platforms, apart from a few small variations.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="1f9ce-110">Method</span><span class="sxs-lookup"><span data-stu-id="1f9ce-110">Method</span></span> | <span data-ttu-id="1f9ce-111">Used for</span><span class="sxs-lookup"><span data-stu-id="1f9ce-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="1f9ce-112">Pages, screens, blades, or forms.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="1f9ce-113">User actions and other events.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-113">User actions and other events.</span></span> <span data-ttu-id="1f9ce-114">Used to track user behavior or to monitor performance.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#send-metrics) |<span data-ttu-id="1f9ce-115">Performance measurements such as queue lengths not related to specific events.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="1f9ce-116">Logging exceptions for diagnosis.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="1f9ce-117">Trace where they occur in relation to other events and examine stack traces.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="1f9ce-118">Logging the frequency and duration of server requests for performance analysis.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="1f9ce-119">Diagnostic log messages.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-119">Diagnostic log messages.</span></span> <span data-ttu-id="1f9ce-120">You can also capture third-party logs.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="1f9ce-121">Logging the duration and frequency of calls to external components that your app depends on.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="1f9ce-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <a name="prep"></a><span data-ttu-id="1f9ce-123">Before you start</span><span class="sxs-lookup"><span data-stu-id="1f9ce-123">Before you start</span></span>
<span data-ttu-id="1f9ce-124">If you haven't done these yet:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-124">If you haven't done these yet:</span></span>

* <span data-ttu-id="1f9ce-125">Add the Application Insights SDK to your project:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="1f9ce-126">ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="1f9ce-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="1f9ce-127">Java project</span><span class="sxs-lookup"><span data-stu-id="1f9ce-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="1f9ce-128">JavaScript in each webpage</span><span class="sxs-lookup"><span data-stu-id="1f9ce-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="1f9ce-129">In your device or web server code, include:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="1f9ce-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="1f9ce-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="1f9ce-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="1f9ce-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="1f9ce-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="1f9ce-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="1f9ce-133">Constructing a TelemetryClient instance</span><span class="sxs-lookup"><span data-stu-id="1f9ce-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="1f9ce-134">Construct an instance of TelemetryClient (except in JavaScript in webpages):</span><span class="sxs-lookup"><span data-stu-id="1f9ce-134">Construct an instance of TelemetryClient (except in JavaScript in webpages):</span></span>

<span data-ttu-id="1f9ce-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="1f9ce-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="1f9ce-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="1f9ce-138">TelemetryClient is thread-safe.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="1f9ce-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="1f9ce-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="1f9ce-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="1f9ce-142">This information is attached to all events that the instance sends.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="1f9ce-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="1f9ce-143">TrackEvent</span></span>
<span data-ttu-id="1f9ce-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="1f9ce-145">(It isn't related to MVC or other framework "events.")</span><span class="sxs-lookup"><span data-stu-id="1f9ce-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="1f9ce-146">Insert TrackEvent calls in your code to count how often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-146">Insert TrackEvent calls in your code to count how often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="1f9ce-147">For example, in a game app, send an event whenever a user wins the game:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-147">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="1f9ce-148">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-148">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="1f9ce-149">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-149">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="1f9ce-150">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-150">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="1f9ce-151">*Java*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-151">*Java*</span></span>

    telemetry.trackEvent("WinGame");


### <a name="view-your-events-in-the-azure-portal"></a><span data-ttu-id="1f9ce-152">View your events in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1f9ce-152">View your events in the Azure portal</span></span>
<span data-ttu-id="1f9ce-153">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-153">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![See a count of custom events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="1f9ce-155">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-155">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Set the chart type and grouping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="1f9ce-157">On the grid, click through an event name to see individual occurrences of that event.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-157">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="1f9ce-158">Click any occurrence to see more detail.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-158">Click any occurrence to see more detail.</span></span>

![Drill through the events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="1f9ce-160">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-160">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Open Filters, expand Event name, and select one or more values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/06-filter.png)


## <a name="send-metrics"></a><span data-ttu-id="1f9ce-162">Send metrics</span><span class="sxs-lookup"><span data-stu-id="1f9ce-162">Send metrics</span></span>

<span data-ttu-id="1f9ce-163">Application Insights can chart metrics that are not attached to particular events.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-163">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="1f9ce-164">For example, you could monitor a queue length at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-164">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="1f9ce-165">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-165">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="1f9ce-166">There are two ways to send metrics:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-166">There are two ways to send metrics:</span></span>

* <span data-ttu-id="1f9ce-167">**MetricManager** is recommended as a convenient way to send metrics while reducing bandwidth.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-167">**MetricManager** is recommended as a convenient way to send metrics while reducing bandwidth.</span></span> <span data-ttu-id="1f9ce-168">It aggregates your metrics in your app, sending the aggregated statistics to the portal at intervals of one minute.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-168">It aggregates your metrics in your app, sending the aggregated statistics to the portal at intervals of one minute.</span></span> <span data-ttu-id="1f9ce-169">MetricManager is available from version 2.4 of the Application Insights SDK for ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-169">MetricManager is available from version 2.4 of the Application Insights SDK for ASP.NET.</span></span>
* <span data-ttu-id="1f9ce-170">**TrackMetric** sends metric statistics to the portal.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-170">**TrackMetric** sends metric statistics to the portal.</span></span> <span data-ttu-id="1f9ce-171">You can either send single metric values, or perform your own aggregation and use TrackMetric to send the statistics.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-171">You can either send single metric values, or perform your own aggregation and use TrackMetric to send the statistics.</span></span>

### <a name="metricmanager"></a><span data-ttu-id="1f9ce-172">MetricManager</span><span class="sxs-lookup"><span data-stu-id="1f9ce-172">MetricManager</span></span>

<span data-ttu-id="1f9ce-173">(Application Insights for ASP.NET v2.4.0+)</span><span class="sxs-lookup"><span data-stu-id="1f9ce-173">(Application Insights for ASP.NET v2.4.0+)</span></span>

<span data-ttu-id="1f9ce-174">Create an instance of MetricManager and then use it as a factory for metrics:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-174">Create an instance of MetricManager and then use it as a factory for metrics:</span></span>

<span data-ttu-id="1f9ce-175">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-175">*C#*</span></span>
```C#
    // Initially:
    var manager = new Microsoft.ApplicationInsights.Extensibility.MetricManager(telemetryClient);

    // For each metric that you want to use:
    var metric1 = mgr.CreateMetric("m1", dimensions);

    // Each time you want to record a measurement:
    metric1.Track(value);

```

<span data-ttu-id="1f9ce-176">`dimensions` is an optional string dictionary.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-176">`dimensions` is an optional string dictionary.</span></span> <span data-ttu-id="1f9ce-177">Use it if you want to attach [properties](#properties) to your metric so that you can segment by different property values.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-177">Use it if you want to attach [properties](#properties) to your metric so that you can segment by different property values.</span></span> 

### <a name="trackmetric"></a><span data-ttu-id="1f9ce-178">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="1f9ce-178">TrackMetric</span></span>

<span data-ttu-id="1f9ce-179">TrackMetric is the basic method for sending aggregated metrics.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-179">TrackMetric is the basic method for sending aggregated metrics.</span></span> 

<span data-ttu-id="1f9ce-180">To send a single metric value:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-180">To send a single metric value:</span></span>

<span data-ttu-id="1f9ce-181">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-181">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="1f9ce-182">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-182">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

<span data-ttu-id="1f9ce-183">However, it is recommended to aggregate metrics before sending them from your app, to reduce bandwidth.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-183">However, it is recommended to aggregate metrics before sending them from your app, to reduce bandwidth.</span></span>
<span data-ttu-id="1f9ce-184">If you are using the latest version of the SDK for ASP.NET, you can use [`MetricManager`](#metricmanager) to do this.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-184">If you are using the latest version of the SDK for ASP.NET, you can use [`MetricManager`](#metricmanager) to do this.</span></span> <span data-ttu-id="1f9ce-185">Otherwise, here is an example of aggregating code:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-185">Otherwise, here is an example of aggregating code:</span></span>

<span data-ttu-id="1f9ce-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-186">*C#*</span></span>

```C#
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
    class MetricAggregator
    {
        private List<double> measurements = new List<double>();
        private string name;
        private TelemetryClient telemetryClient;
        private BackgroundWorker thread;
        private Boolean stop = false;
        public void TrackMetric (double value)
        {
            lock (this)
            {
                measurements.Add(value);
            }
        }
        public MetricTelemetry Aggregate()
        {
            lock (this)
            {
                var sample = new MetricTelemetry();
                sample.Name = "metric name";
                sample.Count = measurements.Count;
                sample.Max = measurements.Max();
                sample.Min = measurements.Min();
                sample.Sum = measurements.Sum();
                var mean = sample.Sum / measurements.Count;
                sample.StandardDeviation = Math.Sqrt(measurements.Sum(v => { var diff = v - mean; return diff * diff; }) / measurements.Count);
                sample.Timestamp = DateTime.Now;
                measurements.Clear();
                return sample;
            }
        }
        public MetricAggregator(string Name)
        {
            name = Name;
            thread = new BackgroundWorker();
            thread.DoWork += async (o, e) => {
                while (!stop)
                {
                    await Task.Delay(60000);
                    telemetryClient.TrackMetric(this.Aggregate());
                }
            };
            thread.RunWorkerAsync();
        }
    }
```
### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="1f9ce-187">Custom metrics in Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="1f9ce-187">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="1f9ce-188">To see the results, open Metrics Explorer and add a new chart.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-188">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="1f9ce-189">Edit the chart to show your metric.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-189">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="1f9ce-190">Your custom metric might take several minutes to appear in the list of available metrics.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-190">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Add a new chart or select a chart, and under Custom, select your metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="1f9ce-192">Custom metrics in Analytics</span><span class="sxs-lookup"><span data-stu-id="1f9ce-192">Custom metrics in Analytics</span></span>

<span data-ttu-id="1f9ce-193">The telemetry is available in the customMetrics table.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-193">The telemetry is available in the customMetrics table.</span></span> <span data-ttu-id="1f9ce-194">Each row represents a call to trackMetric() in your app.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-194">Each row represents a call to trackMetric() in your app.</span></span> <span data-ttu-id="1f9ce-195">Therefore, if you have used MetricManager or your own aggregation code, each row will not represent a single measurement.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-195">Therefore, if you have used MetricManager or your own aggregation code, each row will not represent a single measurement.</span></span> 

* <span data-ttu-id="1f9ce-196">`valueSum` - This is the sum of the measurements.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-196">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="1f9ce-197">To get the mean value, divide by `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-197">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="1f9ce-198">`valueCount` - The number of measurements that were aggregated into this trackMetric call.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-198">`valueCount` - The number of measurements that were aggregated into this trackMetric call.</span></span>



## <a name="page-views"></a><span data-ttu-id="1f9ce-199">Page views</span><span class="sxs-lookup"><span data-stu-id="1f9ce-199">Page views</span></span>
<span data-ttu-id="1f9ce-200">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-200">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="1f9ce-201">But you can change that to track page views at additional or different times.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-201">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="1f9ce-202">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-202">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Usage lens on Overview blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="1f9ce-204">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-204">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="1f9ce-205">Custom page views</span><span class="sxs-lookup"><span data-stu-id="1f9ce-205">Custom page views</span></span>
<span data-ttu-id="1f9ce-206">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-206">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="1f9ce-207">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-207">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="1f9ce-208">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-208">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="1f9ce-209">If you have several tabs within different HTML pages, you can specify the URL too:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-209">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="1f9ce-210">Timing page views</span><span class="sxs-lookup"><span data-stu-id="1f9ce-210">Timing page views</span></span>
<span data-ttu-id="1f9ce-211">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-211">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="1f9ce-212">Instead, you can either:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-212">Instead, you can either:</span></span>

* <span data-ttu-id="1f9ce-213">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-213">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="1f9ce-214">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-214">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="1f9ce-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-215">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="1f9ce-216">...</span><span class="sxs-lookup"><span data-stu-id="1f9ce-216">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="1f9ce-217">The name that you use as the first parameter associates the start and stop calls.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-217">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="1f9ce-218">It defaults to the current page name.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-218">It defaults to the current page name.</span></span>

<span data-ttu-id="1f9ce-219">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-219">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="1f9ce-220">It's up to you what interval you actually time.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-220">It's up to you what interval you actually time.</span></span>

## <a name="trackrequest"></a><span data-ttu-id="1f9ce-221">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="1f9ce-221">TrackRequest</span></span>
<span data-ttu-id="1f9ce-222">The server SDK uses TrackRequest to log HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-222">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="1f9ce-223">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-223">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="1f9ce-224">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-224">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="1f9ce-225">Operation context</span><span class="sxs-lookup"><span data-stu-id="1f9ce-225">Operation context</span></span>
<span data-ttu-id="1f9ce-226">You can associate telemetry items together by attaching to them a common operation ID.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-226">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="1f9ce-227">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-227">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="1f9ce-228">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-228">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="1f9ce-229">The easiest way to set the ID is to set an operation context by using this pattern:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-229">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="1f9ce-230">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-230">*C#*</span></span>

```C#

    // Establish an operation context and associated telemetry item:
    using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
    {
        // Telemetry sent in here will use the same operation ID.
        ...
        telemetry.TrackEvent(...); // or other Track* calls
        ...
        // Set properties of containing telemetry item--for example:
        operation.Telemetry.ResponseCode = "200";

        // Optional: explicitly send telemetry item:
        telemetry.StopOperation(operation);

    } // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="1f9ce-231">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-231">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="1f9ce-232">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-232">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="1f9ce-233">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-233">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="1f9ce-234">Operation contexts can't be nested.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-234">Operation contexts can't be nested.</span></span> <span data-ttu-id="1f9ce-235">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-235">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="1f9ce-236">In Search, the operation context is used to create the **Related Items** list:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-236">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Related items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/21.png)

## <a name="trackexception"></a><span data-ttu-id="1f9ce-238">TrackException</span><span class="sxs-lookup"><span data-stu-id="1f9ce-238">TrackException</span></span>
<span data-ttu-id="1f9ce-239">Send exceptions to Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-239">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="1f9ce-240">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-240">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="1f9ce-241">To [examine individual occurrences](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-241">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="1f9ce-242">The reports include the stack traces.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-242">The reports include the stack traces.</span></span>

<span data-ttu-id="1f9ce-243">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-243">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="1f9ce-244">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-244">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="1f9ce-245">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-245">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="1f9ce-246">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-246">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="1f9ce-247">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-247">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="1f9ce-248">JavaScript: Exceptions are caught automatically.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-248">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="1f9ce-249">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-249">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

## <a name="tracktrace"></a><span data-ttu-id="1f9ce-250">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="1f9ce-250">TrackTrace</span></span>
<span data-ttu-id="1f9ce-251">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-251">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="1f9ce-252">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-252">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="1f9ce-253">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-253">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="1f9ce-254">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-254">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="1f9ce-255">You can search on message content, but (unlike property values) you can't filter on it.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-255">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="1f9ce-256">The size limit on `message` is much higher than the limit on properties.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-256">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="1f9ce-257">An advantage of TrackTrace is that you can put relatively long data in the message.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-257">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="1f9ce-258">For example, you can encode POST data there.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-258">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="1f9ce-259">In addition, you can add a severity level to your message.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-259">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="1f9ce-260">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-260">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="1f9ce-261">For example:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-261">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="1f9ce-262">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-262">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="1f9ce-263">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="1f9ce-263">TrackDependency</span></span>
<span data-ttu-id="1f9ce-264">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-264">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="1f9ce-265">The results appear in the dependency charts in the portal.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-265">The results appear in the dependency charts in the portal.</span></span>

```C#

            var success = false;
            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

<span data-ttu-id="1f9ce-266">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-266">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="1f9ce-267">You have to install an agent on your server to make the module work.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-267">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="1f9ce-268">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-268">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="1f9ce-269">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-269">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

## <a name="flushing-data"></a><span data-ttu-id="1f9ce-270">Flushing data</span><span class="sxs-lookup"><span data-stu-id="1f9ce-270">Flushing data</span></span>
<span data-ttu-id="1f9ce-271">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-271">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="1f9ce-272">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-272">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="1f9ce-273">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-273">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="1f9ce-274">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-274">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="1f9ce-275">Authenticated users</span><span class="sxs-lookup"><span data-stu-id="1f9ce-275">Authenticated users</span></span>
<span data-ttu-id="1f9ce-276">In a web app, users are (by default) identified by cookies.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-276">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="1f9ce-277">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-277">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="1f9ce-278">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-278">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="1f9ce-279">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-279">*JavaScript*</span></span>

```JS
    // Called when my app has identified the user.
    function Authenticated(signInId) {
      var validatedId = signInId.replace(/[,;=| ]+/g, "_");
      appInsights.setAuthenticatedUserContext(validatedId);
      ...
    }
```

<span data-ttu-id="1f9ce-280">In an ASP.NET web MVC application, for example:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-280">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="1f9ce-281">*Razor*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-281">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="1f9ce-282">It isn't necessary to use the user's actual sign-in name.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-282">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="1f9ce-283">It only has to be an ID that is unique to that user.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-283">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="1f9ce-284">It must not include spaces or any of the characters `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-284">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="1f9ce-285">The user ID is also set in a session cookie and sent to the server.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-285">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="1f9ce-286">If the server SDK is installed, the authenticated user ID will be sent as part of the context properties of both client and server telemetry.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-286">If the server SDK is installed, the authenticated user ID will be sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="1f9ce-287">You can then filter and search on it.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-287">You can then filter and search on it.</span></span>

<span data-ttu-id="1f9ce-288">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-288">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="1f9ce-289">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated** and **User accounts**.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-289">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated** and **User accounts**.</span></span>

<span data-ttu-id="1f9ce-290">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-290">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <a name="properties"></a><span data-ttu-id="1f9ce-291">Filtering, searching, and segmenting your data by using properties</span><span class="sxs-lookup"><span data-stu-id="1f9ce-291">Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="1f9ce-292">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-292">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="1f9ce-293">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-293">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="1f9ce-294">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-294">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="1f9ce-295">There's a limit of 8192 on the string length.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-295">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="1f9ce-296">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="1f9ce-296">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="1f9ce-297">*Metrics* are numeric values that can be presented graphically.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-297">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="1f9ce-298">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-298">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="1f9ce-299">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-299">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="1f9ce-300">For metric values to be correctly displayed, they should be greater than or equal to 0.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-300">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="1f9ce-301">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-301">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="1f9ce-302">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-302">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="1f9ce-303">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-303">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="1f9ce-304">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-304">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="1f9ce-305">*Java*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-305">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="1f9ce-306">Take care not to log personally identifiable information in properties.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-306">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="1f9ce-307">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-307">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Open Metrics Explorer, select the chart, and select the metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="1f9ce-309">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-309">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="1f9ce-310">Metrics can sometimes take an hour to be aggregated through the pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-310">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="1f9ce-311">*If you used properties and metrics*, segment the metric by the property:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-311">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Set grouping, and then select the property under Group by](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="1f9ce-313">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-313">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Select an instance, and then select "..."](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="1f9ce-315">Use the **Search** field to see event occurrences that have a particular property value.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-315">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Type a term into Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="1f9ce-317">[Learn more about search expressions](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-317">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="1f9ce-318">Alternative way to set properties and metrics</span><span class="sxs-lookup"><span data-stu-id="1f9ce-318">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="1f9ce-319">If it's more convenient, you can collect the parameters of an event in a separate object:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-319">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="1f9ce-320">Don't reuse the same telemetry item instance (`event` in this example) to call Track\*() multiple times.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-320">Don't reuse the same telemetry item instance (`event` in this example) to call Track\*() multiple times.</span></span> <span data-ttu-id="1f9ce-321">This may cause telemetry to be sent with incorrect configuration.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-321">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

## <a name="timed"></a> <span data-ttu-id="1f9ce-322">Timing events</span><span class="sxs-lookup"><span data-stu-id="1f9ce-322">Timing events</span></span>
<span data-ttu-id="1f9ce-323">Sometimes you want to chart how long it takes to perform an action.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-323">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="1f9ce-324">For example, you might want to know how long users take to consider choices in a game.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-324">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="1f9ce-325">You can use the measurement parameter for this.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-325">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="1f9ce-326">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-326">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a><span data-ttu-id="1f9ce-327">Default properties for custom telemetry</span><span class="sxs-lookup"><span data-stu-id="1f9ce-327">Default properties for custom telemetry</span></span>
<span data-ttu-id="1f9ce-328">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-328">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="1f9ce-329">They are attached to every telemetry item that's sent from that client.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-329">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="1f9ce-330">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-330">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="1f9ce-331">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-331">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="1f9ce-332">*Java*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-332">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="1f9ce-333">Individual telemetry calls can override the default values in their property dictionaries.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-333">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="1f9ce-334">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-334">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="1f9ce-335">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-335">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="1f9ce-336">Sampling, filtering, and processing telemetry</span><span class="sxs-lookup"><span data-stu-id="1f9ce-336">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="1f9ce-337">You can write code to process your telemetry before it's sent from the SDK.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-337">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="1f9ce-338">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-338">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="1f9ce-339">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-339">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="1f9ce-340">For example, you can add version numbers or values that are calculated from other properties.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-340">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="1f9ce-341">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-341">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="1f9ce-342">You control what is sent or discarded, but you have to account for the effect on your metrics.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-342">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="1f9ce-343">Depending on how you discard items, you might lose the ability to navigate between related items.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-343">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="1f9ce-344">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-344">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="1f9ce-345">It does so without affecting the displayed metrics.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-345">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="1f9ce-346">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-346">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="1f9ce-347">[Learn more](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-347">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="1f9ce-348">Disabling telemetry</span><span class="sxs-lookup"><span data-stu-id="1f9ce-348">Disabling telemetry</span></span>
<span data-ttu-id="1f9ce-349">To *dynamically stop and start* the collection and transmission of telemetry:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-349">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="1f9ce-350">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-350">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="1f9ce-351">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-351">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="debug"></a><span data-ttu-id="1f9ce-352">Developer mode</span><span class="sxs-lookup"><span data-stu-id="1f9ce-352">Developer mode</span></span>
<span data-ttu-id="1f9ce-353">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-353">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="1f9ce-354">You also get additional messages that help you trace any problems with the telemetry.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-354">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="1f9ce-355">Switch it off in production, because it may slow down your app.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-355">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="1f9ce-356">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-356">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="1f9ce-357">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-357">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a> <span data-ttu-id="1f9ce-358">Setting the instrumentation key for selected custom telemetry</span><span class="sxs-lookup"><span data-stu-id="1f9ce-358">Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="1f9ce-359">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-359">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> <span data-ttu-id="1f9ce-360">Dynamic instrumentation key</span><span class="sxs-lookup"><span data-stu-id="1f9ce-360">Dynamic instrumentation key</span></span>
<span data-ttu-id="1f9ce-361">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-361">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="1f9ce-362">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-362">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="1f9ce-363">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-363">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="1f9ce-364">*C#*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-364">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="1f9ce-365">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-365">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="1f9ce-366">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-366">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="1f9ce-367">For example, in a webpage generated in an ASP.NET app:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-367">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="1f9ce-368">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-368">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="1f9ce-369">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="1f9ce-369">TelemetryContext</span></span>
<span data-ttu-id="1f9ce-370">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-370">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="1f9ce-371">They are normally set by the standard telemetry modules, but you can also set them yourself.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-371">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="1f9ce-372">For example:</span><span class="sxs-lookup"><span data-stu-id="1f9ce-372">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="1f9ce-373">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-373">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="1f9ce-374">**Component**: The app and its version.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-374">**Component**: The app and its version.</span></span>
* <span data-ttu-id="1f9ce-375">**Device**: Data about the device where the app is running.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-375">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="1f9ce-376">(In web apps, this is the server or client device that the telemetry is sent from.)</span><span class="sxs-lookup"><span data-stu-id="1f9ce-376">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="1f9ce-377">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry will appear.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-377">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry will appear.</span></span> <span data-ttu-id="1f9ce-378">It's usually picked up from ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-378">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="1f9ce-379">**Location**: The geographic location of the device.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-379">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="1f9ce-380">**Operation**: In web apps, the current HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-380">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="1f9ce-381">In other app types, you can set this to group events together.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-381">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="1f9ce-382">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-382">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="1f9ce-383">**Name**: An identifier, usually the URL of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-383">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="1f9ce-384">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-384">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="1f9ce-385">By default, it will be excluded from calculations in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-385">By default, it will be excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="1f9ce-386">**Properties**: Properties that are sent with all telemetry data.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-386">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="1f9ce-387">It can be overridden in individual Track\* calls.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-387">It can be overridden in individual Track\* calls.</span></span>
* <span data-ttu-id="1f9ce-388">**Session**: The user's session.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-388">**Session**: The user's session.</span></span> <span data-ttu-id="1f9ce-389">The ID is set to a generated value, which is changed when the user has not been active for a while.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-389">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="1f9ce-390">**User**: User information.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-390">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="1f9ce-391">Limits</span><span class="sxs-lookup"><span data-stu-id="1f9ce-391">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="1f9ce-392">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-392">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="1f9ce-393">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-393">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="1f9ce-394">Reference docs</span><span class="sxs-lookup"><span data-stu-id="1f9ce-394">Reference docs</span></span>
* [<span data-ttu-id="1f9ce-395">ASP.NET reference</span><span class="sxs-lookup"><span data-stu-id="1f9ce-395">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="1f9ce-396">Java reference</span><span class="sxs-lookup"><span data-stu-id="1f9ce-396">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="1f9ce-397">JavaScript reference</span><span class="sxs-lookup"><span data-stu-id="1f9ce-397">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="1f9ce-398">Android SDK</span><span class="sxs-lookup"><span data-stu-id="1f9ce-398">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="1f9ce-399">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="1f9ce-399">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="1f9ce-400">SDK code</span><span class="sxs-lookup"><span data-stu-id="1f9ce-400">SDK code</span></span>
* [<span data-ttu-id="1f9ce-401">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="1f9ce-401">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="1f9ce-402">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="1f9ce-402">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="1f9ce-403">Windows Server packages</span><span class="sxs-lookup"><span data-stu-id="1f9ce-403">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="1f9ce-404">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1f9ce-404">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="1f9ce-405">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="1f9ce-405">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="1f9ce-406">All platforms</span><span class="sxs-lookup"><span data-stu-id="1f9ce-406">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="1f9ce-407">Questions</span><span class="sxs-lookup"><span data-stu-id="1f9ce-407">Questions</span></span>
* <span data-ttu-id="1f9ce-408">*What exceptions might Track_() calls throw?*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-408">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="1f9ce-409">None.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-409">None.</span></span> <span data-ttu-id="1f9ce-410">You don't need to wrap them in try-catch clauses.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-410">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="1f9ce-411">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span><span class="sxs-lookup"><span data-stu-id="1f9ce-411">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="1f9ce-412">*Is there a REST API to get data from the portal?*</span><span class="sxs-lookup"><span data-stu-id="1f9ce-412">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="1f9ce-413">Yes, the [data access API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-413">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="1f9ce-414">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ce-414">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <a name="next"></a><span data-ttu-id="1f9ce-415">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f9ce-415">Next steps</span></span>
* [<span data-ttu-id="1f9ce-416">Search events and logs</span><span class="sxs-lookup"><span data-stu-id="1f9ce-416">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="1f9ce-417">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1f9ce-417">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)














