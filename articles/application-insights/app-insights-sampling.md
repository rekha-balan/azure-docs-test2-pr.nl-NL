---
title: Telemetry sampling in Azure Application Insights | Microsoft Docs
description: How to keep the volume of telemetry under control.
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: awills
ms.openlocfilehash: 6d5ddb557cb1fc31279223e4793f78497d7c9c52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550820"
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="d7d76-103">Sampling in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d7d76-103">Sampling in Application Insights</span></span>


<span data-ttu-id="d7d76-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7d76-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d7d76-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span><span class="sxs-lookup"><span data-stu-id="d7d76-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="d7d76-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span><span class="sxs-lookup"><span data-stu-id="d7d76-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="d7d76-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span><span class="sxs-lookup"><span data-stu-id="d7d76-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="d7d76-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="d7d76-109">In brief:</span><span class="sxs-lookup"><span data-stu-id="d7d76-109">In brief:</span></span>
* <span data-ttu-id="d7d76-110">Sampling retains 1 in *n* records and discards the rest.</span><span class="sxs-lookup"><span data-stu-id="d7d76-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="d7d76-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span><span class="sxs-lookup"><span data-stu-id="d7d76-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="d7d76-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span><span class="sxs-lookup"><span data-stu-id="d7d76-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="d7d76-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span><span class="sxs-lookup"><span data-stu-id="d7d76-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="d7d76-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span><span class="sxs-lookup"><span data-stu-id="d7d76-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="d7d76-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span><span class="sxs-lookup"><span data-stu-id="d7d76-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="d7d76-116">When sampling is not in operation, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="d7d76-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="d7d76-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="d7d76-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="d7d76-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="d7d76-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="d7d76-119">Types of sampling</span><span class="sxs-lookup"><span data-stu-id="d7d76-119">Types of sampling</span></span>
<span data-ttu-id="d7d76-120">There are three alternative sampling methods:</span><span class="sxs-lookup"><span data-stu-id="d7d76-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="d7d76-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span><span class="sxs-lookup"><span data-stu-id="d7d76-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="d7d76-122">Default from SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="d7d76-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="d7d76-123">Currently available for ASP.NET server-side telemetry only.</span><span class="sxs-lookup"><span data-stu-id="d7d76-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="d7d76-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="d7d76-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="d7d76-125">You set the rate.</span><span class="sxs-lookup"><span data-stu-id="d7d76-125">You set the rate.</span></span> <span data-ttu-id="d7d76-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span><span class="sxs-lookup"><span data-stu-id="d7d76-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="d7d76-127">**Ingestion sampling** works in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7d76-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="d7d76-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span><span class="sxs-lookup"><span data-stu-id="d7d76-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="d7d76-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span><span class="sxs-lookup"><span data-stu-id="d7d76-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="d7d76-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span><span class="sxs-lookup"><span data-stu-id="d7d76-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="d7d76-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span><span class="sxs-lookup"><span data-stu-id="d7d76-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="d7d76-132">Ingestion sampling</span><span class="sxs-lookup"><span data-stu-id="d7d76-132">Ingestion sampling</span></span>
<span data-ttu-id="d7d76-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span><span class="sxs-lookup"><span data-stu-id="d7d76-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="d7d76-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d7d76-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="d7d76-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="d7d76-136">Set the sampling rate in the Quotas and Pricing blade:</span><span class="sxs-lookup"><span data-stu-id="d7d76-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![From the application Overview blade, click Settings, Quota, Samples, then select a sampling rate, and click Update.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sampling/04.png)

<span data-ttu-id="d7d76-138">Like other types of sampling, the algorithm retains related telemetry items.</span><span class="sxs-lookup"><span data-stu-id="d7d76-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d7d76-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span><span class="sxs-lookup"><span data-stu-id="d7d76-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="d7d76-140">Metric counts such as request rate and exception rate are correctly retained.</span><span class="sxs-lookup"><span data-stu-id="d7d76-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="d7d76-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="d7d76-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="d7d76-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span><span class="sxs-lookup"><span data-stu-id="d7d76-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="d7d76-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span><span class="sxs-lookup"><span data-stu-id="d7d76-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="d7d76-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="d7d76-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span><span class="sxs-lookup"><span data-stu-id="d7d76-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="d7d76-146">Adaptive sampling at your web server</span><span class="sxs-lookup"><span data-stu-id="d7d76-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="d7d76-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="d7d76-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="d7d76-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="d7d76-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="d7d76-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span><span class="sxs-lookup"><span data-stu-id="d7d76-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="d7d76-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span><span class="sxs-lookup"><span data-stu-id="d7d76-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="d7d76-151">To achieve the target volume, some of the telemetry generated is discarded.</span><span class="sxs-lookup"><span data-stu-id="d7d76-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="d7d76-152">But like other types of sampling, the algorithm retains related telemetry items.</span><span class="sxs-lookup"><span data-stu-id="d7d76-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d7d76-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span><span class="sxs-lookup"><span data-stu-id="d7d76-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="d7d76-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7d76-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="d7d76-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d7d76-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="d7d76-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span><span class="sxs-lookup"><span data-stu-id="d7d76-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="d7d76-157">The figures shown are the default values:</span><span class="sxs-lookup"><span data-stu-id="d7d76-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="d7d76-158">The target rate that the adaptive algorithm aims for **on each server host**.</span><span class="sxs-lookup"><span data-stu-id="d7d76-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="d7d76-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="d7d76-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="d7d76-160">The interval at which the current rate of telemetry is re-evaluated.</span><span class="sxs-lookup"><span data-stu-id="d7d76-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="d7d76-161">Evaluation is performed as a moving average.</span><span class="sxs-lookup"><span data-stu-id="d7d76-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="d7d76-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span><span class="sxs-lookup"><span data-stu-id="d7d76-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="d7d76-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span><span class="sxs-lookup"><span data-stu-id="d7d76-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="d7d76-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span><span class="sxs-lookup"><span data-stu-id="d7d76-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="d7d76-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span><span class="sxs-lookup"><span data-stu-id="d7d76-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="d7d76-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span><span class="sxs-lookup"><span data-stu-id="d7d76-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="d7d76-167">In the calculation of the moving average, the weight assigned to the most recent value.</span><span class="sxs-lookup"><span data-stu-id="d7d76-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="d7d76-168">Use a value equal to or less than 1.</span><span class="sxs-lookup"><span data-stu-id="d7d76-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="d7d76-169">Smaller values make the algorithm less reactive to sudden changes.</span><span class="sxs-lookup"><span data-stu-id="d7d76-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="d7d76-170">The value assigned when the app has just started.</span><span class="sxs-lookup"><span data-stu-id="d7d76-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="d7d76-171">Don't reduce this while you're debugging.</span><span class="sxs-lookup"><span data-stu-id="d7d76-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="d7d76-172">A semi-colon delimited list of types that you do not want to be sampled.</span><span class="sxs-lookup"><span data-stu-id="d7d76-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="d7d76-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="d7d76-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d7d76-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span><span class="sxs-lookup"><span data-stu-id="d7d76-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="d7d76-175">A semi-colon delimited list of types that you want to be sampled.</span><span class="sxs-lookup"><span data-stu-id="d7d76-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="d7d76-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="d7d76-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d7d76-177">The specified types are sampled; all instances of the other types will always be transmitted.</span><span class="sxs-lookup"><span data-stu-id="d7d76-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="d7d76-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="d7d76-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="d7d76-179">Alternative: configure adaptive sampling in code</span><span class="sxs-lookup"><span data-stu-id="d7d76-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="d7d76-180">Instead of adjusting sampling in the .config file, you can use code.</span><span class="sxs-lookup"><span data-stu-id="d7d76-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="d7d76-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span><span class="sxs-lookup"><span data-stu-id="d7d76-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="d7d76-182">You could use this, for example, to find out what sampling rate is being used.</span><span class="sxs-lookup"><span data-stu-id="d7d76-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="d7d76-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span><span class="sxs-lookup"><span data-stu-id="d7d76-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="d7d76-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="d7d76-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d7d76-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d7d76-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="d7d76-186">Sampling for web pages with JavaScript</span><span class="sxs-lookup"><span data-stu-id="d7d76-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="d7d76-187">You can configure web pages for fixed-rate sampling from any server.</span><span class="sxs-lookup"><span data-stu-id="d7d76-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="d7d76-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="d7d76-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="d7d76-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span><span class="sxs-lookup"><span data-stu-id="d7d76-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="d7d76-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span><span class="sxs-lookup"><span data-stu-id="d7d76-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d7d76-191">Currently sampling doesn't support other values.</span><span class="sxs-lookup"><span data-stu-id="d7d76-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="d7d76-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span><span class="sxs-lookup"><span data-stu-id="d7d76-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="d7d76-193">Fixed-rate sampling for ASP.NET web sites</span><span class="sxs-lookup"><span data-stu-id="d7d76-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="d7d76-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span><span class="sxs-lookup"><span data-stu-id="d7d76-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="d7d76-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span><span class="sxs-lookup"><span data-stu-id="d7d76-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="d7d76-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span><span class="sxs-lookup"><span data-stu-id="d7d76-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="d7d76-197">The sampling algorithm retains related items.</span><span class="sxs-lookup"><span data-stu-id="d7d76-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="d7d76-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span><span class="sxs-lookup"><span data-stu-id="d7d76-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="d7d76-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span><span class="sxs-lookup"><span data-stu-id="d7d76-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="d7d76-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d7d76-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="d7d76-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d7d76-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="d7d76-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span><span class="sxs-lookup"><span data-stu-id="d7d76-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="d7d76-203">**Enable the fixed-rate sampling module.**</span><span class="sxs-lookup"><span data-stu-id="d7d76-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="d7d76-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="d7d76-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="d7d76-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span><span class="sxs-lookup"><span data-stu-id="d7d76-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d7d76-206">Currently sampling doesn't support other values.</span><span class="sxs-lookup"><span data-stu-id="d7d76-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="d7d76-207">Alternative: enable fixed-rate sampling in your server code</span><span class="sxs-lookup"><span data-stu-id="d7d76-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="d7d76-208">Instead of setting the sampling parameter in the .config file, you can use code.</span><span class="sxs-lookup"><span data-stu-id="d7d76-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="d7d76-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="d7d76-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d7d76-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d7d76-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="d7d76-211">When to use sampling?</span><span class="sxs-lookup"><span data-stu-id="d7d76-211">When to use sampling?</span></span>
<span data-ttu-id="d7d76-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span><span class="sxs-lookup"><span data-stu-id="d7d76-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d7d76-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span><span class="sxs-lookup"><span data-stu-id="d7d76-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="d7d76-214">You don’t need sampling for most small and medium size applications.</span><span class="sxs-lookup"><span data-stu-id="d7d76-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="d7d76-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span><span class="sxs-lookup"><span data-stu-id="d7d76-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="d7d76-216">The main advantages of sampling are:</span><span class="sxs-lookup"><span data-stu-id="d7d76-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="d7d76-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span><span class="sxs-lookup"><span data-stu-id="d7d76-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="d7d76-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span><span class="sxs-lookup"><span data-stu-id="d7d76-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="d7d76-219">To reduce network traffic from the collection of telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="d7d76-220">Which type of sampling should I use?</span><span class="sxs-lookup"><span data-stu-id="d7d76-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="d7d76-221">**Use ingestion sampling if:**</span><span class="sxs-lookup"><span data-stu-id="d7d76-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="d7d76-222">You often go through your monthly quota of telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="d7d76-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span><span class="sxs-lookup"><span data-stu-id="d7d76-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="d7d76-224">You're getting a lot of telemetry from your users' web browsers.</span><span class="sxs-lookup"><span data-stu-id="d7d76-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="d7d76-225">**Use fixed-rate sampling if:**</span><span class="sxs-lookup"><span data-stu-id="d7d76-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="d7d76-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span><span class="sxs-lookup"><span data-stu-id="d7d76-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="d7d76-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span><span class="sxs-lookup"><span data-stu-id="d7d76-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="d7d76-228">You are confident of the appropriate sampling percentage for your app.</span><span class="sxs-lookup"><span data-stu-id="d7d76-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="d7d76-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span><span class="sxs-lookup"><span data-stu-id="d7d76-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="d7d76-230">**Use adaptive sampling:**</span><span class="sxs-lookup"><span data-stu-id="d7d76-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="d7d76-231">Otherwise, we recommend adaptive sampling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="d7d76-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span><span class="sxs-lookup"><span data-stu-id="d7d76-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d7d76-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span><span class="sxs-lookup"><span data-stu-id="d7d76-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="d7d76-234">How do I know whether sampling is in operation?</span><span class="sxs-lookup"><span data-stu-id="d7d76-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="d7d76-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span><span class="sxs-lookup"><span data-stu-id="d7d76-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="d7d76-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span><span class="sxs-lookup"><span data-stu-id="d7d76-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="d7d76-237">How does sampling work?</span><span class="sxs-lookup"><span data-stu-id="d7d76-237">How does sampling work?</span></span>
<span data-ttu-id="d7d76-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span><span class="sxs-lookup"><span data-stu-id="d7d76-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="d7d76-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="d7d76-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span><span class="sxs-lookup"><span data-stu-id="d7d76-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="d7d76-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span><span class="sxs-lookup"><span data-stu-id="d7d76-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="d7d76-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="d7d76-243">It either keeps or drops them all together.</span><span class="sxs-lookup"><span data-stu-id="d7d76-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="d7d76-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span><span class="sxs-lookup"><span data-stu-id="d7d76-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="d7d76-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span><span class="sxs-lookup"><span data-stu-id="d7d76-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="d7d76-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span><span class="sxs-lookup"><span data-stu-id="d7d76-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="d7d76-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span><span class="sxs-lookup"><span data-stu-id="d7d76-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="d7d76-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span><span class="sxs-lookup"><span data-stu-id="d7d76-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="d7d76-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span><span class="sxs-lookup"><span data-stu-id="d7d76-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="d7d76-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span><span class="sxs-lookup"><span data-stu-id="d7d76-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="d7d76-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span><span class="sxs-lookup"><span data-stu-id="d7d76-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="d7d76-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="d7d76-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span><span class="sxs-lookup"><span data-stu-id="d7d76-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="d7d76-254">Adaptive sampling</span><span class="sxs-lookup"><span data-stu-id="d7d76-254">Adaptive sampling</span></span>
<span data-ttu-id="d7d76-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span><span class="sxs-lookup"><span data-stu-id="d7d76-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="d7d76-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span><span class="sxs-lookup"><span data-stu-id="d7d76-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="d7d76-257">Sampling and the JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="d7d76-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="d7d76-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span><span class="sxs-lookup"><span data-stu-id="d7d76-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="d7d76-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span><span class="sxs-lookup"><span data-stu-id="d7d76-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="d7d76-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span><span class="sxs-lookup"><span data-stu-id="d7d76-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="d7d76-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span><span class="sxs-lookup"><span data-stu-id="d7d76-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="d7d76-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span><span class="sxs-lookup"><span data-stu-id="d7d76-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="d7d76-263">Verify that you enabled fixed-rate sampling both on server and client.</span><span class="sxs-lookup"><span data-stu-id="d7d76-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="d7d76-264">Make sure that the SDK version is 2.0 or above.</span><span class="sxs-lookup"><span data-stu-id="d7d76-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="d7d76-265">Check that you set the same sampling percentage in both the client and server.</span><span class="sxs-lookup"><span data-stu-id="d7d76-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d7d76-266">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="d7d76-266">Frequently Asked Questions</span></span>
<span data-ttu-id="d7d76-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="d7d76-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d7d76-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="d7d76-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span><span class="sxs-lookup"><span data-stu-id="d7d76-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="d7d76-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span><span class="sxs-lookup"><span data-stu-id="d7d76-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="d7d76-271">*Can the sampling percentage change over time?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="d7d76-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="d7d76-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="d7d76-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span><span class="sxs-lookup"><span data-stu-id="d7d76-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="d7d76-275">Otherwise, you have to guess.</span><span class="sxs-lookup"><span data-stu-id="d7d76-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="d7d76-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="d7d76-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="d7d76-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span><span class="sxs-lookup"><span data-stu-id="d7d76-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="d7d76-279">*What happens if I configure sampling percentage too low?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="d7d76-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span><span class="sxs-lookup"><span data-stu-id="d7d76-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="d7d76-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span><span class="sxs-lookup"><span data-stu-id="d7d76-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="d7d76-282">*What happens if I configure sampling percentage too high?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="d7d76-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span><span class="sxs-lookup"><span data-stu-id="d7d76-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="d7d76-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span><span class="sxs-lookup"><span data-stu-id="d7d76-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="d7d76-285">*On what platforms can I use sampling?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="d7d76-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span><span class="sxs-lookup"><span data-stu-id="d7d76-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="d7d76-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d7d76-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="d7d76-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span><span class="sxs-lookup"><span data-stu-id="d7d76-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="d7d76-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span><span class="sxs-lookup"><span data-stu-id="d7d76-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="d7d76-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span><span class="sxs-lookup"><span data-stu-id="d7d76-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="d7d76-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span><span class="sxs-lookup"><span data-stu-id="d7d76-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="d7d76-292">Use that to send your rare events.</span><span class="sxs-lookup"><span data-stu-id="d7d76-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7d76-293">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7d76-293">Next steps</span></span>
* <span data-ttu-id="d7d76-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span><span class="sxs-lookup"><span data-stu-id="d7d76-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>


