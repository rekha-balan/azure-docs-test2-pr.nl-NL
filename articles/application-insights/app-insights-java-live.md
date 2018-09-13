---
title: Application Insights for Java web apps that are already live
description: Start monitoring a web application that is already running on your server
services: application-insights
documentationcenter: java
author: harelbr
manager: douge
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: awills
ms.openlocfilehash: f48c940cf60ce45aa22b26d0184155dc51991963
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554817"
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="2c948-103">Application Insights for Java web apps that are already live</span><span class="sxs-lookup"><span data-stu-id="2c948-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="2c948-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span><span class="sxs-lookup"><span data-stu-id="2c948-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="2c948-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span><span class="sxs-lookup"><span data-stu-id="2c948-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="2c948-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c948-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="2c948-107">The procedure on this page adds the SDK to your web app at runtime.</span><span class="sxs-lookup"><span data-stu-id="2c948-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="2c948-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span><span class="sxs-lookup"><span data-stu-id="2c948-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="2c948-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span><span class="sxs-lookup"><span data-stu-id="2c948-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="2c948-110">That gives you more options such as writing code to track user activity.</span><span class="sxs-lookup"><span data-stu-id="2c948-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="2c948-111">1. Get an Application Insights instrumentation key</span><span class="sxs-lookup"><span data-stu-id="2c948-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="2c948-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="2c948-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="2c948-113">Create a new Application Insights resource and set the application type to Java web application.</span><span class="sxs-lookup"><span data-stu-id="2c948-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Fill a name, choose Java web app, and click Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-live/02-create.png)

    <span data-ttu-id="2c948-115">The resource is created in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="2c948-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="2c948-116">Open the new resource and get its instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="2c948-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="2c948-117">You'll need to paste this key into your code project shortly.</span><span class="sxs-lookup"><span data-stu-id="2c948-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![In the new resource overview, click Properties and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="2c948-119">2. Download the SDK</span><span class="sxs-lookup"><span data-stu-id="2c948-119">2. Download the SDK</span></span>
1. <span data-ttu-id="2c948-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="2c948-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="2c948-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span><span class="sxs-lookup"><span data-stu-id="2c948-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="2c948-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="2c948-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="2c948-123">Note that you need to repeat this on each server instance, and for each app.</span><span class="sxs-lookup"><span data-stu-id="2c948-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="2c948-124">3. Add an Application Insights xml file</span><span class="sxs-lookup"><span data-stu-id="2c948-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="2c948-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span><span class="sxs-lookup"><span data-stu-id="2c948-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="2c948-126">Put into it the following XML.</span><span class="sxs-lookup"><span data-stu-id="2c948-126">Put into it the following XML.</span></span>

<span data-ttu-id="2c948-127">Substitute the instrumentation key that you got from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2c948-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="2c948-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span><span class="sxs-lookup"><span data-stu-id="2c948-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="2c948-129">The HTTP Request component is optional.</span><span class="sxs-lookup"><span data-stu-id="2c948-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="2c948-130">It automatically sends telemetry about requests and response times to the portal.</span><span class="sxs-lookup"><span data-stu-id="2c948-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="2c948-131">Events correlation is an addition to the HTTP request component.</span><span class="sxs-lookup"><span data-stu-id="2c948-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="2c948-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="2c948-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="2c948-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="2c948-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="2c948-134">4. Add an HTTP filter</span><span class="sxs-lookup"><span data-stu-id="2c948-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="2c948-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span><span class="sxs-lookup"><span data-stu-id="2c948-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="2c948-136">To get the most accurate results, the filter should be mapped before all other filters.</span><span class="sxs-lookup"><span data-stu-id="2c948-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="2c948-137">5. Check firewall exceptions</span><span class="sxs-lookup"><span data-stu-id="2c948-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="2c948-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="2c948-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="2c948-139">6. Restart your web app</span><span class="sxs-lookup"><span data-stu-id="2c948-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="2c948-140">7. View your telemetry in Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c948-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="2c948-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c948-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="2c948-142">Telemetry about HTTP requests appears on the overview blade.</span><span class="sxs-lookup"><span data-stu-id="2c948-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="2c948-143">(If it isn't there, wait a few seconds and then click Refresh.)</span><span class="sxs-lookup"><span data-stu-id="2c948-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-live/5-results.png)

<span data-ttu-id="2c948-145">Click through any chart to see more detailed metrics.</span><span class="sxs-lookup"><span data-stu-id="2c948-145">Click through any chart to see more detailed metrics.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="2c948-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span><span class="sxs-lookup"><span data-stu-id="2c948-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="2c948-147">Learn more about metrics.</span><span class="sxs-lookup"><span data-stu-id="2c948-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="2c948-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c948-148">Next steps</span></span>
* <span data-ttu-id="2c948-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span><span class="sxs-lookup"><span data-stu-id="2c948-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="2c948-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span><span class="sxs-lookup"><span data-stu-id="2c948-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="2c948-151">Capture log traces</span><span class="sxs-lookup"><span data-stu-id="2c948-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="2c948-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span><span class="sxs-lookup"><span data-stu-id="2c948-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>






