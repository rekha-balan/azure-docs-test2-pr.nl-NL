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
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="ac33d-103">Exploring Metrics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="ac33d-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="ac33d-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span><span class="sxs-lookup"><span data-stu-id="ac33d-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="ac33d-105">They help you detect performance issues and watch trends in how your application is being used.</span><span class="sxs-lookup"><span data-stu-id="ac33d-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="ac33d-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span><span class="sxs-lookup"><span data-stu-id="ac33d-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="ac33d-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span><span class="sxs-lookup"><span data-stu-id="ac33d-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="ac33d-108">Here's a sample set of charts:</span><span class="sxs-lookup"><span data-stu-id="ac33d-108">Here's a sample set of charts:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="ac33d-109">You find metrics charts everywhere in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="ac33d-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="ac33d-110">In most cases, they can be customized, and you can add more charts to the blade.</span><span class="sxs-lookup"><span data-stu-id="ac33d-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="ac33d-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span><span class="sxs-lookup"><span data-stu-id="ac33d-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="ac33d-112">Time range</span><span class="sxs-lookup"><span data-stu-id="ac33d-112">Time range</span></span>
<span data-ttu-id="ac33d-113">You can change the Time range covered by the charts or grids on any blade.</span><span class="sxs-lookup"><span data-stu-id="ac33d-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Open the overview blade of your application in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="ac33d-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span><span class="sxs-lookup"><span data-stu-id="ac33d-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="ac33d-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span><span class="sxs-lookup"><span data-stu-id="ac33d-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="ac33d-117">It can take a while for data to come through the analysis pipeline onto a chart.</span><span class="sxs-lookup"><span data-stu-id="ac33d-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="ac33d-118">To zoom into part of a chart, drag over it:</span><span class="sxs-lookup"><span data-stu-id="ac33d-118">To zoom into part of a chart, drag over it:</span></span>

![Drag across part of a chart.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="ac33d-120">Click the Undo Zoom button to restore it.</span><span class="sxs-lookup"><span data-stu-id="ac33d-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="ac33d-121">Granularity and point values</span><span class="sxs-lookup"><span data-stu-id="ac33d-121">Granularity and point values</span></span>
<span data-ttu-id="ac33d-122">Hover your mouse over the chart to display the values of the metrics at that point.</span><span class="sxs-lookup"><span data-stu-id="ac33d-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Hover the mouse over a chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="ac33d-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span><span class="sxs-lookup"><span data-stu-id="ac33d-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="ac33d-125">The sampling interval or "granularity" is shown at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="ac33d-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![The header of a blade.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="ac33d-127">You can adjust the granularity in the Time range blade:</span><span class="sxs-lookup"><span data-stu-id="ac33d-127">You can adjust the granularity in the Time range blade:</span></span>

![The header of a blade.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="ac33d-129">The granularities available depend on the time range you select.</span><span class="sxs-lookup"><span data-stu-id="ac33d-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="ac33d-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span><span class="sxs-lookup"><span data-stu-id="ac33d-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="ac33d-131">Editing charts and grids</span><span class="sxs-lookup"><span data-stu-id="ac33d-131">Editing charts and grids</span></span>
<span data-ttu-id="ac33d-132">To add a new chart to the blade:</span><span class="sxs-lookup"><span data-stu-id="ac33d-132">To add a new chart to the blade:</span></span>

![In Metrics Explorer, choose Add Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="ac33d-134">Select **Edit** on an existing or new chart to edit what it shows:</span><span class="sxs-lookup"><span data-stu-id="ac33d-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Select one or more metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="ac33d-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span><span class="sxs-lookup"><span data-stu-id="ac33d-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="ac33d-137">As soon as you choose one metric, some of the others are disabled.</span><span class="sxs-lookup"><span data-stu-id="ac33d-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="ac33d-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span><span class="sxs-lookup"><span data-stu-id="ac33d-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="ac33d-139">Segment your data</span><span class="sxs-lookup"><span data-stu-id="ac33d-139">Segment your data</span></span>
<span data-ttu-id="ac33d-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span><span class="sxs-lookup"><span data-stu-id="ac33d-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="ac33d-141">Select a chart or grid, switch on grouping and pick a property to group by:</span><span class="sxs-lookup"><span data-stu-id="ac33d-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Select Grouping On, then set select a property in Group By](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="ac33d-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span><span class="sxs-lookup"><span data-stu-id="ac33d-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="ac33d-144">This is suitable where the Aggregation method is Sum.</span><span class="sxs-lookup"><span data-stu-id="ac33d-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="ac33d-145">But where the aggregation type is Average, choose the Line or Grid display types.</span><span class="sxs-lookup"><span data-stu-id="ac33d-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="ac33d-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span><span class="sxs-lookup"><span data-stu-id="ac33d-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="ac33d-147">Is the chart too small for segmented data?</span><span class="sxs-lookup"><span data-stu-id="ac33d-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="ac33d-148">Adjust its height:</span><span class="sxs-lookup"><span data-stu-id="ac33d-148">Adjust its height:</span></span>

![Adjust the slider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="ac33d-150">Aggregation types</span><span class="sxs-lookup"><span data-stu-id="ac33d-150">Aggregation types</span></span>
<span data-ttu-id="ac33d-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span><span class="sxs-lookup"><span data-stu-id="ac33d-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="ac33d-152">If you hover over the chart, it shows the value at that point.</span><span class="sxs-lookup"><span data-stu-id="ac33d-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="ac33d-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span><span class="sxs-lookup"><span data-stu-id="ac33d-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="ac33d-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span><span class="sxs-lookup"><span data-stu-id="ac33d-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="ac33d-155">Metrics can be aggregated in different ways:</span><span class="sxs-lookup"><span data-stu-id="ac33d-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="ac33d-156">**Count** is a count of the events received in the sampling interval.</span><span class="sxs-lookup"><span data-stu-id="ac33d-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="ac33d-157">It is used for events such as requests.</span><span class="sxs-lookup"><span data-stu-id="ac33d-157">It is used for events such as requests.</span></span> <span data-ttu-id="ac33d-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span><span class="sxs-lookup"><span data-stu-id="ac33d-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="ac33d-159">But note that the numeric value changes when you change the sampling interval.</span><span class="sxs-lookup"><span data-stu-id="ac33d-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="ac33d-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span><span class="sxs-lookup"><span data-stu-id="ac33d-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="ac33d-161">**Average** divides the Sum by the number of data points received over the interval.</span><span class="sxs-lookup"><span data-stu-id="ac33d-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="ac33d-162">**Unique** counts are used for counts of users and accounts.</span><span class="sxs-lookup"><span data-stu-id="ac33d-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="ac33d-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span><span class="sxs-lookup"><span data-stu-id="ac33d-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="ac33d-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span><span class="sxs-lookup"><span data-stu-id="ac33d-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="ac33d-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span><span class="sxs-lookup"><span data-stu-id="ac33d-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Percentage aggregation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="ac33d-167">Change the aggregation type</span><span class="sxs-lookup"><span data-stu-id="ac33d-167">Change the aggregation type</span></span>

![Edit the chart and then select Aggregation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="ac33d-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span><span class="sxs-lookup"><span data-stu-id="ac33d-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Deselect all metrics to see the defaults](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="ac33d-171">Pin Y-axis</span><span class="sxs-lookup"><span data-stu-id="ac33d-171">Pin Y-axis</span></span> 
<span data-ttu-id="ac33d-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span><span class="sxs-lookup"><span data-stu-id="ac33d-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="ac33d-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span><span class="sxs-lookup"><span data-stu-id="ac33d-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="ac33d-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span><span class="sxs-lookup"><span data-stu-id="ac33d-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="ac33d-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span><span class="sxs-lookup"><span data-stu-id="ac33d-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Click Advanced Settings, select Custom range, and specify min max values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="ac33d-177">Filter your data</span><span class="sxs-lookup"><span data-stu-id="ac33d-177">Filter your data</span></span>
<span data-ttu-id="ac33d-178">To see just the metrics for a selected set of property values:</span><span class="sxs-lookup"><span data-stu-id="ac33d-178">To see just the metrics for a selected set of property values:</span></span>

![Click Filter, expand a property, and check some values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="ac33d-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span><span class="sxs-lookup"><span data-stu-id="ac33d-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="ac33d-181">Notice the counts of events alongside each property value.</span><span class="sxs-lookup"><span data-stu-id="ac33d-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="ac33d-182">When you select values of one property, the counts alongside other property values are adjusted.</span><span class="sxs-lookup"><span data-stu-id="ac33d-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="ac33d-183">Filters apply to all the charts on a blade.</span><span class="sxs-lookup"><span data-stu-id="ac33d-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="ac33d-184">If you want different filters applied to different charts, create and save different metrics blades.</span><span class="sxs-lookup"><span data-stu-id="ac33d-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="ac33d-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span><span class="sxs-lookup"><span data-stu-id="ac33d-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="ac33d-186">Remove bot and web test traffic</span><span class="sxs-lookup"><span data-stu-id="ac33d-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="ac33d-187">Use the filter **Real or synthetic traffic** and check **Real**.</span><span class="sxs-lookup"><span data-stu-id="ac33d-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="ac33d-188">You can also filter by **Source of synthetic traffic**.</span><span class="sxs-lookup"><span data-stu-id="ac33d-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="ac33d-189">To add properties to the filter list</span><span class="sxs-lookup"><span data-stu-id="ac33d-189">To add properties to the filter list</span></span>
<span data-ttu-id="ac33d-190">Would you like to filter telemetry on a category of your own choosing?</span><span class="sxs-lookup"><span data-stu-id="ac33d-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="ac33d-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span><span class="sxs-lookup"><span data-stu-id="ac33d-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="ac33d-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="ac33d-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="ac33d-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span><span class="sxs-lookup"><span data-stu-id="ac33d-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="ac33d-194">Edit the chart type</span><span class="sxs-lookup"><span data-stu-id="ac33d-194">Edit the chart type</span></span>
<span data-ttu-id="ac33d-195">Notice that you can switch between grids and graphs:</span><span class="sxs-lookup"><span data-stu-id="ac33d-195">Notice that you can switch between grids and graphs:</span></span>

![Select a grid or graph, then choose a chart type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="ac33d-197">Save your metrics blade</span><span class="sxs-lookup"><span data-stu-id="ac33d-197">Save your metrics blade</span></span>
<span data-ttu-id="ac33d-198">When you've created some charts, save them as a favorite.</span><span class="sxs-lookup"><span data-stu-id="ac33d-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="ac33d-199">You can choose whether to share it with other team members, if you use an organizational account.</span><span class="sxs-lookup"><span data-stu-id="ac33d-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Choose Favorite](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="ac33d-201">To see the blade again, **go to the overview blade** and open Favorites:</span><span class="sxs-lookup"><span data-stu-id="ac33d-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![In the Overview blade, choose Favorites](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="ac33d-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span><span class="sxs-lookup"><span data-stu-id="ac33d-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="ac33d-204">If you chose Absolute time range, it will show the same data every time.</span><span class="sxs-lookup"><span data-stu-id="ac33d-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="ac33d-205">Reset the blade</span><span class="sxs-lookup"><span data-stu-id="ac33d-205">Reset the blade</span></span>
<span data-ttu-id="ac33d-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span><span class="sxs-lookup"><span data-stu-id="ac33d-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![In the buttons at the top of Metric Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="ac33d-208">Live metrics stream</span><span class="sxs-lookup"><span data-stu-id="ac33d-208">Live metrics stream</span></span>

<span data-ttu-id="ac33d-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="ac33d-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="ac33d-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span><span class="sxs-lookup"><span data-stu-id="ac33d-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="ac33d-211">By contrast, live metrics are optimized for low latency.</span><span class="sxs-lookup"><span data-stu-id="ac33d-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="ac33d-212">Set alerts</span><span class="sxs-lookup"><span data-stu-id="ac33d-212">Set alerts</span></span>
<span data-ttu-id="ac33d-213">To be notified by email of unusual values of any metric, add an alert.</span><span class="sxs-lookup"><span data-stu-id="ac33d-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="ac33d-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span><span class="sxs-lookup"><span data-stu-id="ac33d-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![In Metrics Explorer, choose Alert rules, Add Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="ac33d-216">[Learn more about alerts][alerts].</span><span class="sxs-lookup"><span data-stu-id="ac33d-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="ac33d-217">Continuous Export</span><span class="sxs-lookup"><span data-stu-id="ac33d-217">Continuous Export</span></span>
<span data-ttu-id="ac33d-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="ac33d-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="ac33d-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="ac33d-219">Power BI</span></span>
<span data-ttu-id="ac33d-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac33d-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="ac33d-221">Analytics</span><span class="sxs-lookup"><span data-stu-id="ac33d-221">Analytics</span></span>
<span data-ttu-id="ac33d-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span><span class="sxs-lookup"><span data-stu-id="ac33d-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="ac33d-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span><span class="sxs-lookup"><span data-stu-id="ac33d-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="ac33d-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span><span class="sxs-lookup"><span data-stu-id="ac33d-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ac33d-225">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ac33d-225">Troubleshooting</span></span>
<span data-ttu-id="ac33d-226">*I don't see any data on my chart.*</span><span class="sxs-lookup"><span data-stu-id="ac33d-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="ac33d-227">Filters apply to all the charts on the blade.</span><span class="sxs-lookup"><span data-stu-id="ac33d-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="ac33d-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span><span class="sxs-lookup"><span data-stu-id="ac33d-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="ac33d-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span><span class="sxs-lookup"><span data-stu-id="ac33d-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="ac33d-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span><span class="sxs-lookup"><span data-stu-id="ac33d-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="ac33d-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span><span class="sxs-lookup"><span data-stu-id="ac33d-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="ac33d-232">Try clearing 'group by', or choose a different grouping property.</span><span class="sxs-lookup"><span data-stu-id="ac33d-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="ac33d-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ac33d-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="ac33d-234">It isn't available for Azure websites.</span><span class="sxs-lookup"><span data-stu-id="ac33d-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="ac33d-235">Video</span><span class="sxs-lookup"><span data-stu-id="ac33d-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="ac33d-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac33d-236">Next steps</span></span>
* [<span data-ttu-id="ac33d-237">Monitoring usage with Application Insights</span><span class="sxs-lookup"><span data-stu-id="ac33d-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="ac33d-238">Using Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="ac33d-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md




















