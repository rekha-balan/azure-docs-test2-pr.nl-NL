---
title: Troubleshoot Application Insights in a Java web project
description: Troubleshooting guide - monitoring live Java apps with Application Insights.
services: application-insights
documentationcenter: java
author: alancameronwills
manager: douge
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: awills
ms.openlocfilehash: caef2a6cafe8e10acc3888c8fc1cfb2e6d2c36eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662342"
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="2b762-103">Troubleshooting and Q and A for Application Insights for Java</span><span class="sxs-lookup"><span data-stu-id="2b762-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="2b762-104">Questions or problems with [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="2b762-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="2b762-105">Here are some tips.</span><span class="sxs-lookup"><span data-stu-id="2b762-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="2b762-106">Build errors</span><span class="sxs-lookup"><span data-stu-id="2b762-106">Build errors</span></span>
<span data-ttu-id="2b762-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span><span class="sxs-lookup"><span data-stu-id="2b762-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="2b762-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="2b762-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="2b762-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span><span class="sxs-lookup"><span data-stu-id="2b762-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="2b762-110">No data</span><span class="sxs-lookup"><span data-stu-id="2b762-110">No data</span></span>
<span data-ttu-id="2b762-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span><span class="sxs-lookup"><span data-stu-id="2b762-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="2b762-112">Wait a minute and click Refresh.</span><span class="sxs-lookup"><span data-stu-id="2b762-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="2b762-113">The charts refresh themselves periodically, but you can also refresh manually.</span><span class="sxs-lookup"><span data-stu-id="2b762-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="2b762-114">The refresh interval depends on the time range of the chart.</span><span class="sxs-lookup"><span data-stu-id="2b762-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="2b762-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span><span class="sxs-lookup"><span data-stu-id="2b762-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="2b762-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span><span class="sxs-lookup"><span data-stu-id="2b762-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="2b762-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="2b762-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com.</span></span> <span data-ttu-id="2b762-118">See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="2b762-118">See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="2b762-119">In the Microsoft Azure start board, look at the service status map.</span><span class="sxs-lookup"><span data-stu-id="2b762-119">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="2b762-120">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span><span class="sxs-lookup"><span data-stu-id="2b762-120">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="2b762-121">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span><span class="sxs-lookup"><span data-stu-id="2b762-121">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="2b762-122">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span><span class="sxs-lookup"><span data-stu-id="2b762-122">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="2b762-123">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span><span class="sxs-lookup"><span data-stu-id="2b762-123">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="2b762-124">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span><span class="sxs-lookup"><span data-stu-id="2b762-124">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="2b762-125">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span><span class="sxs-lookup"><span data-stu-id="2b762-125">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="2b762-126">I used to see data, but it has stopped</span><span class="sxs-lookup"><span data-stu-id="2b762-126">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="2b762-127">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="2b762-127">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="2b762-128">Have you hit your monthly quota of data points?</span><span class="sxs-lookup"><span data-stu-id="2b762-128">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="2b762-129">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span><span class="sxs-lookup"><span data-stu-id="2b762-129">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="2b762-130">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="2b762-130">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="2b762-131">I don't see all the data I'm expecting</span><span class="sxs-lookup"><span data-stu-id="2b762-131">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="2b762-132">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span><span class="sxs-lookup"><span data-stu-id="2b762-132">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="2b762-133">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span><span class="sxs-lookup"><span data-stu-id="2b762-133">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="2b762-134">This helps you keep within your monthly quota of telemetry.</span><span class="sxs-lookup"><span data-stu-id="2b762-134">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="2b762-135">No usage data</span><span class="sxs-lookup"><span data-stu-id="2b762-135">No usage data</span></span>
<span data-ttu-id="2b762-136">**I see data about requests and response times, but no page view, browser, or user data.**</span><span class="sxs-lookup"><span data-stu-id="2b762-136">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="2b762-137">You successfully set up your app to send telemetry from the server.</span><span class="sxs-lookup"><span data-stu-id="2b762-137">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="2b762-138">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span><span class="sxs-lookup"><span data-stu-id="2b762-138">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="2b762-139">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span><span class="sxs-lookup"><span data-stu-id="2b762-139">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="2b762-140">Use the same instrumentation key to set up both your client and server telemetry.</span><span class="sxs-lookup"><span data-stu-id="2b762-140">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="2b762-141">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span><span class="sxs-lookup"><span data-stu-id="2b762-141">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="2b762-142">Disabling telemetry</span><span class="sxs-lookup"><span data-stu-id="2b762-142">Disabling telemetry</span></span>
<span data-ttu-id="2b762-143">**How can I disable telemetry collection?**</span><span class="sxs-lookup"><span data-stu-id="2b762-143">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="2b762-144">In code:</span><span class="sxs-lookup"><span data-stu-id="2b762-144">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="2b762-145">**Or**</span><span class="sxs-lookup"><span data-stu-id="2b762-145">**Or**</span></span> 

<span data-ttu-id="2b762-146">Update ApplicationInsights.xml (in the resources folder in your project).</span><span class="sxs-lookup"><span data-stu-id="2b762-146">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="2b762-147">Add the following under the root node:</span><span class="sxs-lookup"><span data-stu-id="2b762-147">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="2b762-148">Using the XML method, you have to restart the application when you change the value.</span><span class="sxs-lookup"><span data-stu-id="2b762-148">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="2b762-149">Changing the target</span><span class="sxs-lookup"><span data-stu-id="2b762-149">Changing the target</span></span>
<span data-ttu-id="2b762-150">**How can I change which Azure resource my project sends data to?**</span><span class="sxs-lookup"><span data-stu-id="2b762-150">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="2b762-151">[Get the instrumentation key of the new resource.][java]</span><span class="sxs-lookup"><span data-stu-id="2b762-151">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="2b762-152">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span><span class="sxs-lookup"><span data-stu-id="2b762-152">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="2b762-153">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span><span class="sxs-lookup"><span data-stu-id="2b762-153">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="2b762-154">Debug data from the SDK</span><span class="sxs-lookup"><span data-stu-id="2b762-154">Debug data from the SDK</span></span>

<span data-ttu-id="2b762-155">**How can I find out what the SDK is doing?**</span><span class="sxs-lookup"><span data-stu-id="2b762-155">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="2b762-156">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span><span class="sxs-lookup"><span data-stu-id="2b762-156">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="2b762-157">You can also instruct the logger to output to a file:</span><span class="sxs-lookup"><span data-stu-id="2b762-157">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="File">
      <enabled>True</enabled>
      <uniqueprefix>JavaSDKLog</uniqueprefix>
    </SDKLogger>
```

<span data-ttu-id="2b762-158">The files can be found under `%temp%\javasdklogs`.</span><span class="sxs-lookup"><span data-stu-id="2b762-158">The files can be found under `%temp%\javasdklogs`.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="2b762-159">The Azure start screen</span><span class="sxs-lookup"><span data-stu-id="2b762-159">The Azure start screen</span></span>
<span data-ttu-id="2b762-160">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span><span class="sxs-lookup"><span data-stu-id="2b762-160">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="2b762-161">No, it shows the health of Azure servers around the world.</span><span class="sxs-lookup"><span data-stu-id="2b762-161">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="2b762-162">*From the Azure start board (home screen), how do I find data about my app?*</span><span class="sxs-lookup"><span data-stu-id="2b762-162">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="2b762-163">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span><span class="sxs-lookup"><span data-stu-id="2b762-163">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="2b762-164">To get there faster in future, you can pin your app to the start board.</span><span class="sxs-lookup"><span data-stu-id="2b762-164">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="2b762-165">Intranet servers</span><span class="sxs-lookup"><span data-stu-id="2b762-165">Intranet servers</span></span>
<span data-ttu-id="2b762-166">**Can I monitor a server on my intranet?**</span><span class="sxs-lookup"><span data-stu-id="2b762-166">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="2b762-167">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span><span class="sxs-lookup"><span data-stu-id="2b762-167">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="2b762-168">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="2b762-168">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="2b762-169">Data retention</span><span class="sxs-lookup"><span data-stu-id="2b762-169">Data retention</span></span>
<span data-ttu-id="2b762-170">**How long is data retained in the portal? Is it secure?**</span><span class="sxs-lookup"><span data-stu-id="2b762-170">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="2b762-171">See [Data retention and privacy][data].</span><span class="sxs-lookup"><span data-stu-id="2b762-171">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b762-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b762-172">Next steps</span></span>
<span data-ttu-id="2b762-173">**I set up Application Insights for my Java server app. What else can I do?**</span><span class="sxs-lookup"><span data-stu-id="2b762-173">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="2b762-174">[Monitor availability of your web pages][availability]</span><span class="sxs-lookup"><span data-stu-id="2b762-174">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="2b762-175">[Monitor web page usage][usage]</span><span class="sxs-lookup"><span data-stu-id="2b762-175">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="2b762-176">[Track usage and diagnose issues in your device apps][platforms]</span><span class="sxs-lookup"><span data-stu-id="2b762-176">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="2b762-177">[Write code to track usage of your app][track]</span><span class="sxs-lookup"><span data-stu-id="2b762-177">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="2b762-178">[Capture diagnostic logs][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2b762-178">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="2b762-179">Get help</span><span class="sxs-lookup"><span data-stu-id="2b762-179">Get help</span></span>
* [<span data-ttu-id="2b762-180">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="2b762-180">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

