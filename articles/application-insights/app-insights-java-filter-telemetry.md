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
# <a name="filter-telemetry-in-your-java-web-app"></a>Filter telemetry in your Java web app

Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md). There are some out-of-the-box filters that you can use, and you can also write your own custom filters.

The out-of-the-box filters include:

* Trace severity level
* Specific URLs, keywords or response codes
* Fast responses - that is, requests to which your app responded to quickly
* Specific event names

> [!NOTE]
> Filters skew the metrics of your app. For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times. But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.
> If this is a concern, use [Sampling](app-insights-sampling.md) instead.

## <a name="setting-filters"></a>Setting filters

In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:


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




[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Built-in filters

### <a name="metric-telemetry-filter"></a>Metric Telemetry filter

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` - Comma-separated list of custom metric names.


### <a name="page-view-telemetry-filter"></a>Page View Telemetry filter

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS` - Duration refers to the time taken to load the page. If this is set, pages that loaded faster than this time are not reported.
* `NotNeededNames` - Comma-separated list of page names.
* `NotNeededUrls` - Comma-separated list of URL fragments. For example, `"home"` filters out all pages that have "home" in the URL.


### <a name="request-telemetry-filter"></a>Request Telemetry Filter


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Synthetic Source filter

Filters out all telemetry that have values in the SyntheticSource property. These include requests from bots, spiders and availability tests.

Filter out telemetry for all synthetic requests:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Filter out telemetry for specific synthetic sources:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` - Comma-separated list of synthetic source names.

### <a name="telemetry-event-filter"></a>Telemetry Event filter

Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` - Comma-separated list of event names.


### <a name="trace-telemetry-filter"></a>Trace Telemetry filter

Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* `FromSeverityLevel` valid values are:
 *  OFF             - Filter out ALL traces
 *  TRACE           - No filtering. equals to Trace level
 *  INFO            - Filter out TRACE level
 *  WARN            - Filter out TRACE and INFO
 *  ERROR           - Filter out WARN, INFO, TRACE
 *  CRITICAL        - filter out all but CRITICAL


## <a name="custom-filters"></a>Custom filters

### <a name="1-code-your-filter"></a>1. Code your filter

In your code, create a class that implements `TelemetryProcessor`:

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


### <a name="2-invoke-your-filter-in-the-configuration-file"></a>2. Invoke your filter in the configuration file

In ApplicationInsights.xml:

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

## <a name="troubleshooting"></a>Troubleshooting

*My filter isn't working.*

* Check that you have provided valid parameter values. For example, durations should be integers. Invalid values will cause the filter to be ignored. If your custom filter throws an exception from a constructor or set method, it will be ignored.

## <a name="next-steps"></a>Next steps

* [Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.