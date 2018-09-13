---
title: Exploring Metrics in Azure Application Insights | Microsoft Docs
description: How to interpret charts on metric explorer, and how to customize metric explorer blades.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: awills
ms.openlocfilehash: 33c8f0d6efa20d8fa9b45e019b4bc52322ff9c79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553769"
---
# <a name="exploring-metrics-in-application-insights"></a>Exploring Metrics in Application Insights
Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application. They help you detect performance issues and watch trends in how your application is being used. There's a wide range of standard metrics, and you can also create your own custom metrics and events.

Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.

Here's a sample set of charts:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/01-overview.png)

You find metrics charts everywhere in the Application Insights portal. In most cases, they can be customized, and you can add more charts to the blade. From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.

## <a name="time-range"></a>Time range
You can change the Time range covered by the charts or grids on any blade.

![Open the overview blade of your application in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/03-range.png)

If you're expecting some data that hasn't appeared yet, click Refresh. Charts refresh themselves at intervals, but the intervals are longer for larger time ranges. It can take a while for data to come through the analysis pipeline onto a chart.

To zoom into part of a chart, drag over it:

![Drag across part of a chart.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/12-drag.png)

Click the Undo Zoom button to restore it.

## <a name="granularity-and-point-values"></a>Granularity and point values
Hover your mouse over the chart to display the values of the metrics at that point.

![Hover the mouse over a chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/02-focus.png)

The value of the metric at a particular point is aggregated over the preceding sampling interval.

The sampling interval or "granularity" is shown at the top of the blade.

![The header of a blade.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/11-grain.png)

You can adjust the granularity in the Time range blade:

![The header of a blade.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/grain.png)

The granularities available depend on the time range you select. The explicit granularities are alternatives to the "automatic" granularity for the time range.


## <a name="editing-charts-and-grids"></a>Editing charts and grids
To add a new chart to the blade:

![In Metrics Explorer, choose Add Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/04-add.png)

Select **Edit** on an existing or new chart to edit what it shows:

![Select one or more metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/08-select.png)

You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together. As soon as you choose one metric, some of the others are disabled.

If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.

## <a name="segment-your-data"></a>Segment your data
You can split a metric by property - for example, to compare page views on clients with different operating systems.

Select a chart or grid, switch on grouping and pick a property to group by:

![Select Grouping On, then set select a property in Group By](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> When you use grouping, the Area and Bar chart types provide a stacked display. This is suitable where the Aggregation method is Sum. But where the aggregation type is Average, choose the Line or Grid display types.
>
>

If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.

Is the chart too small for segmented data? Adjust its height:

![Adjust the slider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Aggregation types
The legend at the side by default usually shows the aggregated value over the period of the chart. If you hover over the chart, it shows the value at that point.

Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity". The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.

Metrics can be aggregated in different ways:

* **Count** is a count of the events received in the sampling interval. It is used for events such as requests. Variations in the height of the chart indicates variations in the rate at which the events occur. But note that the numeric value changes when you change the sampling interval.
* **Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.
* **Average** divides the Sum by the number of data points received over the interval.
* **Unique** counts are used for counts of users and accounts. Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.
* **%** - percentage versions of each aggregation are used only with segmented charts. The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.

    ![Percentage aggregation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a>Change the aggregation type

![Edit the chart and then select Aggregation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/05-aggregation.png)

The default method for each metric is shown when you create a new chart or when all metrics are deselected:

![Deselect all metrics to see the defaults](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Pin Y-axis 
By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values. But in some cases more than the quantum it might be interesting to visually inspect minor changes in values. For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.
Click on "Advanced Settings" check box to bring up the Y-axis range Settings

![Click Advanced Settings, select Custom range, and specify min max values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filter your data
To see just the metrics for a selected set of property values:

![Click Filter, expand a property, and check some values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/19-filter.png)

If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.

Notice the counts of events alongside each property value. When you select values of one property, the counts alongside other property values are adjusted.

Filters apply to all the charts on a blade. If you want different filters applied to different charts, create and save different metrics blades. If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.

### <a name="remove-bot-and-web-test-traffic"></a>Remove bot and web test traffic
Use the filter **Real or synthetic traffic** and check **Real**.

You can also filter by **Source of synthetic traffic**.

### <a name="to-add-properties-to-the-filter-list"></a>To add properties to the filter list
Would you like to filter telemetry on a category of your own choosing? For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.

[Create your own property](app-insights-api-custom-events-metrics.md#properties). Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.

## <a name="edit-the-chart-type"></a>Edit the chart type
Notice that you can switch between grids and graphs:

![Select a grid or graph, then choose a chart type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Save your metrics blade
When you've created some charts, save them as a favorite. You can choose whether to share it with other team members, if you use an organizational account.

![Choose Favorite](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/21-favorite-save.png)

To see the blade again, **go to the overview blade** and open Favorites:

![In the Overview blade, choose Favorites](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/22-favorite-get.png)

If you chose Relative time range when you saved, the blade will be updated with the latest metrics. If you chose Absolute time range, it will show the same data every time.

## <a name="reset-the-blade"></a>Reset the blade
If you edit a blade but then you'd like to get back to the original saved set, just click Reset.

![In the buttons at the top of Metric Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Live metrics stream

For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md). Most metrics take a few minutes to appear, because of the process of aggregation. By contrast, live metrics are optimized for low latency. 

## <a name="set-alerts"></a>Set alerts
To be notified by email of unusual values of any metric, add an alert. You can choose either to send the email to the account administrators, or to specific email addresses.

![In Metrics Explorer, choose Alert rules, Add Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Learn more about alerts][alerts].


## <a name="continuous-export"></a>Continuous Export
If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analytics
[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language. Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance. 

From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.

## <a name="troubleshooting"></a>Troubleshooting
*I don't see any data on my chart.*

* Filters apply to all the charts on the blade. Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.

    If you want to set different filters on different charts, create them in different blades, save them as separate favorites. If you want, you can pin them to the dashboard so that you can see them alongside each other.
* If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart. Try clearing 'group by', or choose a different grouping property.
* Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md). It isn't available for Azure websites.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Next steps
* [Monitoring usage with Application Insights](app-insights-web-track-usage.md)
* [Using Diagnostic Search](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md




















