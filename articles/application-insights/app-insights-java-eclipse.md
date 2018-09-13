---
title: Get started with Azure Application Insights with Java in Eclipse | Microsoft docs
description: Use the Eclipse plug-in to add performance and usage monitoring to your Java website with Application Insights
services: application-insights
documentationcenter: java
author: alancameronwills
manager: douge
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: awills
ms.openlocfilehash: 7c670bc244584a62043a335d819bf39d10484ca9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556121"
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="068fe-103">Get started with Application Insights with Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="068fe-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="068fe-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span><span class="sxs-lookup"><span data-stu-id="068fe-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="068fe-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="068fe-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="068fe-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="068fe-106">Prerequisites</span></span>
<span data-ttu-id="068fe-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="068fe-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="068fe-108">([Add Application Insights to other types of Java project][java].)</span><span class="sxs-lookup"><span data-stu-id="068fe-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="068fe-109">You'll need:</span><span class="sxs-lookup"><span data-stu-id="068fe-109">You'll need:</span></span>

* <span data-ttu-id="068fe-110">Oracle JRE 1.6 or later</span><span class="sxs-lookup"><span data-stu-id="068fe-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="068fe-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="068fe-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="068fe-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span><span class="sxs-lookup"><span data-stu-id="068fe-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="068fe-113">Windows 7 or later, or Windows Server 2008 or later</span><span class="sxs-lookup"><span data-stu-id="068fe-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="068fe-114">Install the SDK on Eclipse (one time)</span><span class="sxs-lookup"><span data-stu-id="068fe-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="068fe-115">You only have to do this one time per machine.</span><span class="sxs-lookup"><span data-stu-id="068fe-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="068fe-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span><span class="sxs-lookup"><span data-stu-id="068fe-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="068fe-117">In Eclipse, click Help, Install New Software.</span><span class="sxs-lookup"><span data-stu-id="068fe-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Help, Install New Software](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="068fe-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="068fe-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="068fe-120">Uncheck **Contact all update sites...**</span><span class="sxs-lookup"><span data-stu-id="068fe-120">Uncheck **Contact all update sites...**</span></span>

    ![For Application Insights SDK, clear Contact all update sites](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="068fe-122">Follow the remaining steps for each Java project.</span><span class="sxs-lookup"><span data-stu-id="068fe-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="068fe-123">Create an Application Insights resource in Azure</span><span class="sxs-lookup"><span data-stu-id="068fe-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="068fe-124">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="068fe-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="068fe-125">Create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="068fe-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="068fe-126">Set the application type to Java web application.</span><span class="sxs-lookup"><span data-stu-id="068fe-126">Set the application type to Java web application.</span></span>  

    ![Click + and choose Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="068fe-128">Find the instrumentation key of the new resource.</span><span class="sxs-lookup"><span data-stu-id="068fe-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="068fe-129">You'll need to paste this into your code project shortly.</span><span class="sxs-lookup"><span data-stu-id="068fe-129">You'll need to paste this into your code project shortly.</span></span>  

    ![In the new resource overview, click Properties and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="068fe-131">Add Application Insights to your project</span><span class="sxs-lookup"><span data-stu-id="068fe-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="068fe-132">Add Application Insights from the context menu of your Java web project.</span><span class="sxs-lookup"><span data-stu-id="068fe-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![In the new resource overview, click Properties and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="068fe-134">Paste the instrumentation key that you got from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="068fe-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![In the new resource overview, click Properties and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="068fe-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span><span class="sxs-lookup"><span data-stu-id="068fe-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="068fe-137">Run the application and see metrics</span><span class="sxs-lookup"><span data-stu-id="068fe-137">Run the application and see metrics</span></span>
<span data-ttu-id="068fe-138">Run your application.</span><span class="sxs-lookup"><span data-stu-id="068fe-138">Run your application.</span></span>

<span data-ttu-id="068fe-139">Return to your Application Insights resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="068fe-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="068fe-140">HTTP requests data will appear on the overview blade.</span><span class="sxs-lookup"><span data-stu-id="068fe-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="068fe-141">(If it isn't there, wait a few seconds and then click Refresh.)</span><span class="sxs-lookup"><span data-stu-id="068fe-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="068fe-142">Server response, request counts, and failures</span><span class="sxs-lookup"><span data-stu-id="068fe-142">Server response, request counts, and failures</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="068fe-143">Click through any chart to see more detailed metrics.</span><span class="sxs-lookup"><span data-stu-id="068fe-143">Click through any chart to see more detailed metrics.</span></span>

![Request counts by name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="068fe-145">[Learn more about metrics.][metrics]</span><span class="sxs-lookup"><span data-stu-id="068fe-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="068fe-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span><span class="sxs-lookup"><span data-stu-id="068fe-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![All traces for this request](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="068fe-148">Client-side telemetry</span><span class="sxs-lookup"><span data-stu-id="068fe-148">Client-side telemetry</span></span>
<span data-ttu-id="068fe-149">From the QuickStart blade, click Get code to monitor my web pages:</span><span class="sxs-lookup"><span data-stu-id="068fe-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![On your app overview blade, choose Quick Start, Get code to monitor my web pages.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="068fe-152">Insert the code snippet in the head of your HTML files.</span><span class="sxs-lookup"><span data-stu-id="068fe-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="068fe-153">View client-side data</span><span class="sxs-lookup"><span data-stu-id="068fe-153">View client-side data</span></span>
<span data-ttu-id="068fe-154">Open your updated web pages and use them.</span><span class="sxs-lookup"><span data-stu-id="068fe-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="068fe-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span><span class="sxs-lookup"><span data-stu-id="068fe-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="068fe-156">(From the Overview blade, scroll down and click Usage.)</span><span class="sxs-lookup"><span data-stu-id="068fe-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="068fe-157">Page view, user, and session metrics will appear on the usage blade:</span><span class="sxs-lookup"><span data-stu-id="068fe-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sessions, users and page views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="068fe-159">[Learn more about setting up client-side telemetry.][usage]</span><span class="sxs-lookup"><span data-stu-id="068fe-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="068fe-160">Publish your application</span><span class="sxs-lookup"><span data-stu-id="068fe-160">Publish your application</span></span>
<span data-ttu-id="068fe-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span><span class="sxs-lookup"><span data-stu-id="068fe-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="068fe-162">Make sure your firewall allows your application to send telemetry to these ports:</span><span class="sxs-lookup"><span data-stu-id="068fe-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="068fe-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="068fe-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="068fe-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="068fe-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="068fe-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="068fe-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="068fe-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="068fe-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="068fe-167">On Windows servers, install:</span><span class="sxs-lookup"><span data-stu-id="068fe-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="068fe-168">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="068fe-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="068fe-169">(This enables performance counters.)</span><span class="sxs-lookup"><span data-stu-id="068fe-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="068fe-170">Exceptions and request failures</span><span class="sxs-lookup"><span data-stu-id="068fe-170">Exceptions and request failures</span></span>
<span data-ttu-id="068fe-171">Unhandled exceptions are automatically collected:</span><span class="sxs-lookup"><span data-stu-id="068fe-171">Unhandled exceptions are automatically collected:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="068fe-172">To collect data on other exceptions, you have two options:</span><span class="sxs-lookup"><span data-stu-id="068fe-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="068fe-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="068fe-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="068fe-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="068fe-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="068fe-175">You specify the methods you want to watch.</span><span class="sxs-lookup"><span data-stu-id="068fe-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="068fe-176">Monitor method calls and external dependencies</span><span class="sxs-lookup"><span data-stu-id="068fe-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="068fe-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span><span class="sxs-lookup"><span data-stu-id="068fe-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="068fe-178">Performance counters</span><span class="sxs-lookup"><span data-stu-id="068fe-178">Performance counters</span></span>
<span data-ttu-id="068fe-179">On your Overview blade, scroll down and click the  **Servers** tile.</span><span class="sxs-lookup"><span data-stu-id="068fe-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="068fe-180">You'll see a range of performance counters.</span><span class="sxs-lookup"><span data-stu-id="068fe-180">You'll see a range of performance counters.</span></span>

![Scroll down to click the Servers tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="068fe-182">Customize performance counter collection</span><span class="sxs-lookup"><span data-stu-id="068fe-182">Customize performance counter collection</span></span>
<span data-ttu-id="068fe-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span><span class="sxs-lookup"><span data-stu-id="068fe-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="068fe-184">Collect additional performance counters</span><span class="sxs-lookup"><span data-stu-id="068fe-184">Collect additional performance counters</span></span>
<span data-ttu-id="068fe-185">You can specify additional performance counters to be collected.</span><span class="sxs-lookup"><span data-stu-id="068fe-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="068fe-186">JMX counters (exposed by the Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="068fe-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="068fe-187">`displayName` – The name displayed in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="068fe-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="068fe-188">`objectName` – The JMX object name.</span><span class="sxs-lookup"><span data-stu-id="068fe-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="068fe-189">`attribute` – The attribute of the JMX object name to fetch</span><span class="sxs-lookup"><span data-stu-id="068fe-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="068fe-190">`type` (optional) - The type of JMX object’s attribute:</span><span class="sxs-lookup"><span data-stu-id="068fe-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="068fe-191">Default: a simple type such as int or long.</span><span class="sxs-lookup"><span data-stu-id="068fe-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="068fe-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="068fe-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="068fe-193">`tabular`: the perf counter data is in the format of a table row</span><span class="sxs-lookup"><span data-stu-id="068fe-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="068fe-194">Windows performance counters</span><span class="sxs-lookup"><span data-stu-id="068fe-194">Windows performance counters</span></span>
<span data-ttu-id="068fe-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span><span class="sxs-lookup"><span data-stu-id="068fe-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="068fe-196">Categories can either be global, or can have numbered or named instances.</span><span class="sxs-lookup"><span data-stu-id="068fe-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="068fe-197">displayName – The name displayed in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="068fe-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="068fe-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span><span class="sxs-lookup"><span data-stu-id="068fe-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="068fe-199">counterName – The name of the performance counter.</span><span class="sxs-lookup"><span data-stu-id="068fe-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="068fe-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span><span class="sxs-lookup"><span data-stu-id="068fe-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="068fe-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="068fe-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="068fe-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="068fe-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="068fe-203">Unix performance counters</span><span class="sxs-lookup"><span data-stu-id="068fe-203">Unix performance counters</span></span>
* <span data-ttu-id="068fe-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span><span class="sxs-lookup"><span data-stu-id="068fe-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="068fe-205">Availability web tests</span><span class="sxs-lookup"><span data-stu-id="068fe-205">Availability web tests</span></span>
<span data-ttu-id="068fe-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span><span class="sxs-lookup"><span data-stu-id="068fe-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="068fe-207">[To set up][availability], scroll down to click Availability.</span><span class="sxs-lookup"><span data-stu-id="068fe-207">[To set up][availability], scroll down to click Availability.</span></span>

![Scroll down, click Availability, then Add Web test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="068fe-209">You'll get charts of response times, plus email notifications if your site goes down.</span><span class="sxs-lookup"><span data-stu-id="068fe-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web test example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="068fe-211">[Learn more about availability web tests.][availability]</span><span class="sxs-lookup"><span data-stu-id="068fe-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="068fe-212">Diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="068fe-212">Diagnostic logs</span></span>
<span data-ttu-id="068fe-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span><span class="sxs-lookup"><span data-stu-id="068fe-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="068fe-214">[Learn more about diagnostic logs][javalogs]</span><span class="sxs-lookup"><span data-stu-id="068fe-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="068fe-215">Custom telemetry</span><span class="sxs-lookup"><span data-stu-id="068fe-215">Custom telemetry</span></span>
<span data-ttu-id="068fe-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span><span class="sxs-lookup"><span data-stu-id="068fe-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="068fe-217">You can insert code both in web page JavaScript and in the server-side Java.</span><span class="sxs-lookup"><span data-stu-id="068fe-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="068fe-218">[Learn about custom telemetry][track]</span><span class="sxs-lookup"><span data-stu-id="068fe-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="068fe-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="068fe-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="068fe-220">Detect and diagnose issues</span><span class="sxs-lookup"><span data-stu-id="068fe-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="068fe-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span><span class="sxs-lookup"><span data-stu-id="068fe-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="068fe-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span><span class="sxs-lookup"><span data-stu-id="068fe-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="068fe-223">[Search events and logs][diagnostic] to help diagnose problems.</span><span class="sxs-lookup"><span data-stu-id="068fe-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="068fe-224">[Capture Log4J or Logback traces][javalogs]</span><span class="sxs-lookup"><span data-stu-id="068fe-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="068fe-225">Track usage</span><span class="sxs-lookup"><span data-stu-id="068fe-225">Track usage</span></span>
* <span data-ttu-id="068fe-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span><span class="sxs-lookup"><span data-stu-id="068fe-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="068fe-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span><span class="sxs-lookup"><span data-stu-id="068fe-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
















