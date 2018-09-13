---
title: Smart diagnostics of web app performance changes in Azure Application Insights| Microsoft Docs
description: Automatic diagnosis of spikes or steps in performance telemetry from your web app.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: awills
ms.openlocfilehash: 0523f3e911f4d47f003e732628a211ce113ea232
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564589"
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="ed9c2-103">Diagnose sudden changes in your app telemetry</span><span class="sxs-lookup"><span data-stu-id="ed9c2-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="ed9c2-104">*This feature is in preview.*</span><span class="sxs-lookup"><span data-stu-id="ed9c2-104">*This feature is in preview.*</span></span>

<span data-ttu-id="ed9c2-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span><span class="sxs-lookup"><span data-stu-id="ed9c2-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="ed9c2-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed9c2-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ed9c2-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="ed9c2-108">This helps you diagnose the problem quickly.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="ed9c2-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span><span class="sxs-lookup"><span data-stu-id="ed9c2-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![example analytics diagnostics result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="ed9c2-111">Diagnose data changes</span><span class="sxs-lookup"><span data-stu-id="ed9c2-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="ed9c2-112">Run a query in Analytics, and render it as a time chart.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="ed9c2-113">Click any highlighted peak point, if there is one.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![peak point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="ed9c2-115">Diagnostics takes a few seconds to discover a pattern.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="ed9c2-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="ed9c2-118">The text shows the dimension values that appear to correlate with the shift.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="ed9c2-119">In this example, it’s associated with a particular request and a particular browser version.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="ed9c2-120">Notice also the two components of the chart, with the filter true and false.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="ed9c2-121">The false component shows an unchanged trend.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="ed9c2-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="ed9c2-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="ed9c2-124">This shows that Diagnostics has found a combination of properties that explains the change.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="ed9c2-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![show all](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="ed9c2-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="ed9c2-128">At this point, you may change your query.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-128">At this point, you may change your query.</span></span> <span data-ttu-id="ed9c2-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="ed9c2-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="ed9c2-131">Try the demo</span><span class="sxs-lookup"><span data-stu-id="ed9c2-131">Try the demo</span></span>

<span data-ttu-id="ed9c2-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ed9c2-133">How it works</span><span class="sxs-lookup"><span data-stu-id="ed9c2-133">How it works</span></span>

<span data-ttu-id="ed9c2-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md#evaluate-diffpatterns) operation.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md#evaluate-diffpatterns) operation.</span></span> <span data-ttu-id="ed9c2-135">It looks for candidate patterns that might explain the data change.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="ed9c2-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="ed9c2-137">No diagnostic points?</span><span class="sxs-lookup"><span data-stu-id="ed9c2-137">No diagnostic points?</span></span>

<span data-ttu-id="ed9c2-138">Smart Diagnostics only works when the following criteria are satisfied:</span><span class="sxs-lookup"><span data-stu-id="ed9c2-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="ed9c2-139">Smart Diagnostics setting is switched on.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="ed9c2-140">Look under the Settings icon in Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="ed9c2-141">The Smart Diagnostics option in Analytics settings is selected.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="ed9c2-142">Time axis: The X-axis of the chart must be of type `datetime`.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="ed9c2-143">Line or area chart: Diagnostics only works these types of chart.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="ed9c2-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="ed9c2-145">Discontinuity: There must be a significant discontinuity in the data.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="ed9c2-146">Sufficient points to analyze.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="ed9c2-147">No more than one summarize clause in the query.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="ed9c2-148">No project clause that contains a name definition before the summarize clause.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="ed9c2-149">Related articles</span><span class="sxs-lookup"><span data-stu-id="ed9c2-149">Related articles</span></span>

 * [<span data-ttu-id="ed9c2-150">Analytics tutorial</span><span class="sxs-lookup"><span data-stu-id="ed9c2-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="ed9c2-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span><span class="sxs-lookup"><span data-stu-id="ed9c2-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>
<span data-ttu-id="ed9c2-152">S</span><span class="sxs-lookup"><span data-stu-id="ed9c2-152">S</span></span>



