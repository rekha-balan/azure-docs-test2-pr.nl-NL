---
title: Filter Azure Application Insights telemetry in your Java web app | Microsoft Docs
description: Reduce telemetry traffic by filtering out the events you don't need to monitor.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: awills
ms.openlocfilehash: cd09b7c5d45d07a3fbcc5d6f0c02400dcd36d61b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551246"
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="08461-103">Filter telemetry in your Java web app</span><span class="sxs-lookup"><span data-stu-id="08461-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="08461-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="08461-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="08461-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span><span class="sxs-lookup"><span data-stu-id="08461-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="08461-106">The out-of-the-box filters include:</span><span class="sxs-lookup"><span data-stu-id="08461-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="08461-107">Trace severity level</span><span class="sxs-lookup"><span data-stu-id="08461-107">Trace severity level</span></span>
* <span data-ttu-id="08461-108">Specific URLs, keywords or response codes</span><span class="sxs-lookup"><span data-stu-id="08461-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="08461-109">Fast responses - that is, requests to which your app responded to quickly</span><span class="sxs-lookup"><span data-stu-id="08461-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="08461-110">Specific event names</span><span class="sxs-lookup"><span data-stu-id="08461-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="08461-111">Filters skew the metrics of your app.</span><span class="sxs-lookup"><span data-stu-id="08461-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="08461-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span><span class="sxs-lookup"><span data-stu-id="08461-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="08461-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span><span class="sxs-lookup"><span data-stu-id="08461-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="08461-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span><span class="sxs-lookup"><span data-stu-id="08461-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="08461-115">Setting filters</span><span class="sxs-lookup"><span data-stu-id="08461-115">Setting filters</span></span>

<span data-ttu-id="08461-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span><span class="sxs-lookup"><span data-stu-id="08461-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want to see -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="08461-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="08461-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="08461-118">Built-in filters</span><span class="sxs-lookup"><span data-stu-id="08461-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="08461-119">Metric Telemetry filter</span><span class="sxs-lookup"><span data-stu-id="08461-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="08461-120">`NotNeeded` - Comma-separated list of custom metric names.</span><span class="sxs-lookup"><span data-stu-id="08461-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="08461-121">Page View Telemetry filter</span><span class="sxs-lookup"><span data-stu-id="08461-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="08461-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span><span class="sxs-lookup"><span data-stu-id="08461-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="08461-123">If this is set, pages that loaded faster than this time are not reported.</span><span class="sxs-lookup"><span data-stu-id="08461-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="08461-124">`NotNeededNames` - Comma-separated list of page names.</span><span class="sxs-lookup"><span data-stu-id="08461-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="08461-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span><span class="sxs-lookup"><span data-stu-id="08461-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="08461-126">For example, `"home"` filters out all pages that have "home" in the URL.</span><span class="sxs-lookup"><span data-stu-id="08461-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="08461-127">Request Telemetry Filter</span><span class="sxs-lookup"><span data-stu-id="08461-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="08461-128">Synthetic Source filter</span><span class="sxs-lookup"><span data-stu-id="08461-128">Synthetic Source filter</span></span>

<span data-ttu-id="08461-129">Filters out all telemetry that have values in the SyntheticSource property.</span><span class="sxs-lookup"><span data-stu-id="08461-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="08461-130">These include requests from bots, spiders and availability tests.</span><span class="sxs-lookup"><span data-stu-id="08461-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="08461-131">Filter out telemetry for all synthetic requests:</span><span class="sxs-lookup"><span data-stu-id="08461-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="08461-132">Filter out telemetry for specific synthetic sources:</span><span class="sxs-lookup"><span data-stu-id="08461-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="08461-133">`NotNeeded` - Comma-separated list of synthetic source names.</span><span class="sxs-lookup"><span data-stu-id="08461-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="08461-134">Telemetry Event filter</span><span class="sxs-lookup"><span data-stu-id="08461-134">Telemetry Event filter</span></span>

<span data-ttu-id="08461-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="08461-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="08461-136">`NotNeededNames` - Comma-separated list of event names.</span><span class="sxs-lookup"><span data-stu-id="08461-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="08461-137">Trace Telemetry filter</span><span class="sxs-lookup"><span data-stu-id="08461-137">Trace Telemetry filter</span></span>

<span data-ttu-id="08461-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="08461-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="08461-139">`FromSeverityLevel` valid values are:</span><span class="sxs-lookup"><span data-stu-id="08461-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="08461-140">OFF             - Filter out ALL traces</span><span class="sxs-lookup"><span data-stu-id="08461-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="08461-141">TRACE           - No filtering.</span><span class="sxs-lookup"><span data-stu-id="08461-141">TRACE           - No filtering.</span></span> <span data-ttu-id="08461-142">equals to Trace level</span><span class="sxs-lookup"><span data-stu-id="08461-142">equals to Trace level</span></span>
 *  <span data-ttu-id="08461-143">INFO            - Filter out TRACE level</span><span class="sxs-lookup"><span data-stu-id="08461-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="08461-144">WARN            - Filter out TRACE and INFO</span><span class="sxs-lookup"><span data-stu-id="08461-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="08461-145">ERROR           - Filter out WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="08461-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="08461-146">CRITICAL        - filter out all but CRITICAL</span><span class="sxs-lookup"><span data-stu-id="08461-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="08461-147">Custom filters</span><span class="sxs-lookup"><span data-stu-id="08461-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="08461-148">1. Code your filter</span><span class="sxs-lookup"><span data-stu-id="08461-148">1. Code your filter</span></span>

<span data-ttu-id="08461-149">In your code, create a class that implements `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="08461-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="08461-150">2. Invoke your filter in the configuration file</span><span class="sxs-lookup"><span data-stu-id="08461-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="08461-151">In ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="08461-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="08461-152">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="08461-152">Troubleshooting</span></span>

<span data-ttu-id="08461-153">*My filter isn't working.*</span><span class="sxs-lookup"><span data-stu-id="08461-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="08461-154">Check that you have provided valid parameter values.</span><span class="sxs-lookup"><span data-stu-id="08461-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="08461-155">For example, durations should be integers.</span><span class="sxs-lookup"><span data-stu-id="08461-155">For example, durations should be integers.</span></span> <span data-ttu-id="08461-156">Invalid values will cause the filter to be ignored.</span><span class="sxs-lookup"><span data-stu-id="08461-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="08461-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span><span class="sxs-lookup"><span data-stu-id="08461-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08461-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="08461-158">Next steps</span></span>

* <span data-ttu-id="08461-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span><span class="sxs-lookup"><span data-stu-id="08461-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
