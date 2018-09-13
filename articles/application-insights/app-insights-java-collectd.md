---
title: Monitor Java web app performance on Linux - Azure | Microsoft Docs
description: Extended application performance monitoring of your Java website with the CollectD plug-in for Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: douge
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: awills
ms.openlocfilehash: 46116233e842d9dcd78ae270e8b8d44bc677393e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553885"
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="889a4-103">collectd: Linux performance metrics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="889a4-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="889a4-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span><span class="sxs-lookup"><span data-stu-id="889a4-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="889a4-105">This open-source solution gathers various system and network statistics.</span><span class="sxs-lookup"><span data-stu-id="889a4-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="889a4-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="889a4-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="889a4-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span><span class="sxs-lookup"><span data-stu-id="889a4-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![Sample charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="889a4-109">Get your instrumentation key</span><span class="sxs-lookup"><span data-stu-id="889a4-109">Get your instrumentation key</span></span>
<span data-ttu-id="889a4-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span><span class="sxs-lookup"><span data-stu-id="889a4-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="889a4-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="889a4-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="889a4-112">Take a copy of the instrumentation key, which identifies the resource.</span><span class="sxs-lookup"><span data-stu-id="889a4-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Browse all, open your resource, and then in the Essentials drop-down, select, and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="889a4-114">Install collectd and the plug-in</span><span class="sxs-lookup"><span data-stu-id="889a4-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="889a4-115">On your Linux server machines:</span><span class="sxs-lookup"><span data-stu-id="889a4-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="889a4-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span><span class="sxs-lookup"><span data-stu-id="889a4-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="889a4-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="889a4-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="889a4-118">Note the version number.</span><span class="sxs-lookup"><span data-stu-id="889a4-118">Note the version number.</span></span>
3. <span data-ttu-id="889a4-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="889a4-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="889a4-120">Edit `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="889a4-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="889a4-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span><span class="sxs-lookup"><span data-stu-id="889a4-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="889a4-122">Update the JVMArg for the java.class.path to include the following JAR.</span><span class="sxs-lookup"><span data-stu-id="889a4-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="889a4-123">Update the version number to match the one you downloaded:</span><span class="sxs-lookup"><span data-stu-id="889a4-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="889a4-124">Add this snippet, using the Instrumentation Key from your resource:</span><span class="sxs-lookup"><span data-stu-id="889a4-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="889a4-125">Here's part of a sample configuration file:</span><span class="sxs-lookup"><span data-stu-id="889a4-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="889a4-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span><span class="sxs-lookup"><span data-stu-id="889a4-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="889a4-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="889a4-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="889a4-128">View the data in Application Insights</span><span class="sxs-lookup"><span data-stu-id="889a4-128">View the data in Application Insights</span></span>
<span data-ttu-id="889a4-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span><span class="sxs-lookup"><span data-stu-id="889a4-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-collectd/result.png)

<span data-ttu-id="889a4-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span><span class="sxs-lookup"><span data-stu-id="889a4-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="889a4-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="889a4-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="889a4-132">To exclude upload of specific statistics</span><span class="sxs-lookup"><span data-stu-id="889a4-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="889a4-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span><span class="sxs-lookup"><span data-stu-id="889a4-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="889a4-134">To exclude data from specific plugins or data sources:</span><span class="sxs-lookup"><span data-stu-id="889a4-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="889a4-135">Edit the configuration file.</span><span class="sxs-lookup"><span data-stu-id="889a4-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="889a4-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span><span class="sxs-lookup"><span data-stu-id="889a4-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="889a4-137">Directive</span><span class="sxs-lookup"><span data-stu-id="889a4-137">Directive</span></span> | <span data-ttu-id="889a4-138">Effect</span><span class="sxs-lookup"><span data-stu-id="889a4-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="889a4-139">Exclude all data collected by the `disk` plugin</span><span class="sxs-lookup"><span data-stu-id="889a4-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="889a4-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span><span class="sxs-lookup"><span data-stu-id="889a4-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="889a4-141">Separate directives with a newline.</span><span class="sxs-lookup"><span data-stu-id="889a4-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="889a4-142">Problems?</span><span class="sxs-lookup"><span data-stu-id="889a4-142">Problems?</span></span>
<span data-ttu-id="889a4-143">*I don't see data in the portal*</span><span class="sxs-lookup"><span data-stu-id="889a4-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="889a4-144">Open [Search][diagnostic] to see if the raw events have arrived.</span><span class="sxs-lookup"><span data-stu-id="889a4-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="889a4-145">Sometimes they take longer to appear in metrics explorer.</span><span class="sxs-lookup"><span data-stu-id="889a4-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="889a4-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="889a4-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="889a4-147">Enable tracing in the Application Insights plugin.</span><span class="sxs-lookup"><span data-stu-id="889a4-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="889a4-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="889a4-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="889a4-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span><span class="sxs-lookup"><span data-stu-id="889a4-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="889a4-150">Known issue</span><span class="sxs-lookup"><span data-stu-id="889a4-150">Known issue</span></span>

<span data-ttu-id="889a4-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span><span class="sxs-lookup"><span data-stu-id="889a4-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="889a4-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span><span class="sxs-lookup"><span data-stu-id="889a4-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="889a4-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span><span class="sxs-lookup"><span data-stu-id="889a4-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="889a4-154">Workaround: Exclude data collected by the problem Write plugins.</span><span class="sxs-lookup"><span data-stu-id="889a4-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md





