---
title: Troubleshoot Application Insights in a Java web project
description: Troubleshooting guide - monitoring live Java apps with Application Insights.
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 04/02/2018
ms.author: mbullwin
ms.openlocfilehash: 26899ea62b8caa872b6c99b94976c87f84ba7176
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826657"
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="70513-103">Troubleshooting and Q and A for Application Insights for Java</span><span class="sxs-lookup"><span data-stu-id="70513-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="70513-104">Questions or problems with [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="70513-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="70513-105">Here are some tips.</span><span class="sxs-lookup"><span data-stu-id="70513-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="70513-106">Build errors</span><span class="sxs-lookup"><span data-stu-id="70513-106">Build errors</span></span>
<span data-ttu-id="70513-107">**In Eclipse or Intellij Idea, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span><span class="sxs-lookup"><span data-stu-id="70513-107">**In Eclipse or Intellij Idea, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="70513-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[2.0,)</version>` or (Gradle) `version:'2.0.+'`), try specifying a specific version instead like `2.0.1`.</span><span class="sxs-lookup"><span data-stu-id="70513-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[2.0,)</version>` or (Gradle) `version:'2.0.+'`), try specifying a specific version instead like `2.0.1`.</span></span> <span data-ttu-id="70513-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java/releases) for the latest version.</span><span class="sxs-lookup"><span data-stu-id="70513-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java/releases) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="70513-110">No data</span><span class="sxs-lookup"><span data-stu-id="70513-110">No data</span></span>
<span data-ttu-id="70513-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span><span class="sxs-lookup"><span data-stu-id="70513-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="70513-112">Wait a minute and click Refresh.</span><span class="sxs-lookup"><span data-stu-id="70513-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="70513-113">The charts refresh themselves periodically, but you can also refresh manually.</span><span class="sxs-lookup"><span data-stu-id="70513-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="70513-114">The refresh interval depends on the time range of the chart.</span><span class="sxs-lookup"><span data-stu-id="70513-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="70513-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project) or configured as Environment variable.</span><span class="sxs-lookup"><span data-stu-id="70513-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project) or configured as Environment variable.</span></span>
* <span data-ttu-id="70513-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span><span class="sxs-lookup"><span data-stu-id="70513-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="70513-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="70513-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com.</span></span> <span data-ttu-id="70513-118">See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="70513-118">See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="70513-119">In the Microsoft Azure start board, look at the service status map.</span><span class="sxs-lookup"><span data-stu-id="70513-119">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="70513-120">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span><span class="sxs-lookup"><span data-stu-id="70513-120">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="70513-121">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with AI: INFO/WARN/ERROR for any suspicious logs.</span><span class="sxs-lookup"><span data-stu-id="70513-121">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with AI: INFO/WARN/ERROR for any suspicious logs.</span></span>
* <span data-ttu-id="70513-122">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span><span class="sxs-lookup"><span data-stu-id="70513-122">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="70513-123">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span><span class="sxs-lookup"><span data-stu-id="70513-123">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="70513-124">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span><span class="sxs-lookup"><span data-stu-id="70513-124">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="70513-125">For example: in Tomcat, this would mean the WEB-INF/classes folder.</span><span class="sxs-lookup"><span data-stu-id="70513-125">For example: in Tomcat, this would mean the WEB-INF/classes folder.</span></span> <span data-ttu-id="70513-126">During developement you can place ApplicationInsights.xml in resources folder of your web project.</span><span class="sxs-lookup"><span data-stu-id="70513-126">During developement you can place ApplicationInsights.xml in resources folder of your web project.</span></span>
* <span data-ttu-id="70513-127">Please also look at [GitHub issues page](https://github.com/Microsoft/ApplicationInsights-Java/issues) for known issues with the SDK.</span><span class="sxs-lookup"><span data-stu-id="70513-127">Please also look at [GitHub issues page](https://github.com/Microsoft/ApplicationInsights-Java/issues) for known issues with the SDK.</span></span>
* <span data-ttu-id="70513-128">Please ensure to use same version of Application Insights core, web, agent and logging appenders to avoid any version conflict issues.</span><span class="sxs-lookup"><span data-stu-id="70513-128">Please ensure to use same version of Application Insights core, web, agent and logging appenders to avoid any version conflict issues.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="70513-129">I used to see data, but it has stopped</span><span class="sxs-lookup"><span data-stu-id="70513-129">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="70513-130">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="70513-130">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="70513-131">Have you hit your monthly quota of data points?</span><span class="sxs-lookup"><span data-stu-id="70513-131">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="70513-132">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span><span class="sxs-lookup"><span data-stu-id="70513-132">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="70513-133">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="70513-133">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>
* <span data-ttu-id="70513-134">Have you recently upgraded your SDK?</span><span class="sxs-lookup"><span data-stu-id="70513-134">Have you recently upgraded your SDK?</span></span> <span data-ttu-id="70513-135">Please ensure that only Unique SDK jars are present inside the project directory.</span><span class="sxs-lookup"><span data-stu-id="70513-135">Please ensure that only Unique SDK jars are present inside the project directory.</span></span> <span data-ttu-id="70513-136">There should not be two different versions of SDK present.</span><span class="sxs-lookup"><span data-stu-id="70513-136">There should not be two different versions of SDK present.</span></span>
* <span data-ttu-id="70513-137">Are you looking at the correct AI resource?</span><span class="sxs-lookup"><span data-stu-id="70513-137">Are you looking at the correct AI resource?</span></span> <span data-ttu-id="70513-138">Please match the iKey of your application to the resource where you are expecting telemetry.</span><span class="sxs-lookup"><span data-stu-id="70513-138">Please match the iKey of your application to the resource where you are expecting telemetry.</span></span> <span data-ttu-id="70513-139">They should be the same.</span><span class="sxs-lookup"><span data-stu-id="70513-139">They should be the same.</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="70513-140">I don't see all the data I'm expecting</span><span class="sxs-lookup"><span data-stu-id="70513-140">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="70513-141">Open the Usage and estimated cost page and check whether [sampling](app-insights-sampling.md) is in operation.</span><span class="sxs-lookup"><span data-stu-id="70513-141">Open the Usage and estimated cost page and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="70513-142">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span><span class="sxs-lookup"><span data-stu-id="70513-142">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="70513-143">This helps you keep within your monthly quota of telemetry.</span><span class="sxs-lookup"><span data-stu-id="70513-143">This helps you keep within your monthly quota of telemetry.</span></span> 
* <span data-ttu-id="70513-144">Do you have SDK Sampling turned on?</span><span class="sxs-lookup"><span data-stu-id="70513-144">Do you have SDK Sampling turned on?</span></span> <span data-ttu-id="70513-145">If yes, data would be sampled at the rate specified for all the applicable types.</span><span class="sxs-lookup"><span data-stu-id="70513-145">If yes, data would be sampled at the rate specified for all the applicable types.</span></span>
* <span data-ttu-id="70513-146">Are you running an older version of Java SDK?</span><span class="sxs-lookup"><span data-stu-id="70513-146">Are you running an older version of Java SDK?</span></span> <span data-ttu-id="70513-147">Starting with version 2.0.1, we have introduced fault tolerance mechanism to handle intermittent network and backend failures as well as data persistence on local drives.</span><span class="sxs-lookup"><span data-stu-id="70513-147">Starting with version 2.0.1, we have introduced fault tolerance mechanism to handle intermittent network and backend failures as well as data persistence on local drives.</span></span>
* <span data-ttu-id="70513-148">Are you getting throttled due to excessive telemetry?</span><span class="sxs-lookup"><span data-stu-id="70513-148">Are you getting throttled due to excessive telemetry?</span></span> <span data-ttu-id="70513-149">If you turn on INFO logging, you will see a log message "App is throttled".</span><span class="sxs-lookup"><span data-stu-id="70513-149">If you turn on INFO logging, you will see a log message "App is throttled".</span></span> <span data-ttu-id="70513-150">Our current limit is 32k telemetry items/second.</span><span class="sxs-lookup"><span data-stu-id="70513-150">Our current limit is 32k telemetry items/second.</span></span>

### <a name="java-agent-cannot-capture-dependency-data"></a><span data-ttu-id="70513-151">Java Agent cannot capture dependency data</span><span class="sxs-lookup"><span data-stu-id="70513-151">Java Agent cannot capture dependency data</span></span>
* <span data-ttu-id="70513-152">Have you configured Java agent by following [Configure Java Agent](app-insights-java-agent.md) ?</span><span class="sxs-lookup"><span data-stu-id="70513-152">Have you configured Java agent by following [Configure Java Agent](app-insights-java-agent.md) ?</span></span>
* <span data-ttu-id="70513-153">Make sure both the java agent jar and the AI-Agent.xml file are placed in the same folder.</span><span class="sxs-lookup"><span data-stu-id="70513-153">Make sure both the java agent jar and the AI-Agent.xml file are placed in the same folder.</span></span>
* <span data-ttu-id="70513-154">Make sure that the dependency you are trying to auto-collect is supported for auto collection.</span><span class="sxs-lookup"><span data-stu-id="70513-154">Make sure that the dependency you are trying to auto-collect is supported for auto collection.</span></span> <span data-ttu-id="70513-155">Currently we only support MySQL, MsSQL, Oracle DB and Redis Cache dependency collection.</span><span class="sxs-lookup"><span data-stu-id="70513-155">Currently we only support MySQL, MsSQL, Oracle DB and Redis Cache dependency collection.</span></span>
* <span data-ttu-id="70513-156">Are you using JDK 1.7 or 1.8?</span><span class="sxs-lookup"><span data-stu-id="70513-156">Are you using JDK 1.7 or 1.8?</span></span> <span data-ttu-id="70513-157">Currently we do not support dependency collection in JDK 9.</span><span class="sxs-lookup"><span data-stu-id="70513-157">Currently we do not support dependency collection in JDK 9.</span></span>

## <a name="no-usage-data"></a><span data-ttu-id="70513-158">No usage data</span><span class="sxs-lookup"><span data-stu-id="70513-158">No usage data</span></span>
<span data-ttu-id="70513-159">**I see data about requests and response times, but no page view, browser, or user data.**</span><span class="sxs-lookup"><span data-stu-id="70513-159">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="70513-160">You successfully set up your app to send telemetry from the server.</span><span class="sxs-lookup"><span data-stu-id="70513-160">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="70513-161">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span><span class="sxs-lookup"><span data-stu-id="70513-161">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="70513-162">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span><span class="sxs-lookup"><span data-stu-id="70513-162">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="70513-163">Use the same instrumentation key to set up both your client and server telemetry.</span><span class="sxs-lookup"><span data-stu-id="70513-163">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="70513-164">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span><span class="sxs-lookup"><span data-stu-id="70513-164">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="70513-165">Disabling telemetry</span><span class="sxs-lookup"><span data-stu-id="70513-165">Disabling telemetry</span></span>
<span data-ttu-id="70513-166">**How can I disable telemetry collection?**</span><span class="sxs-lookup"><span data-stu-id="70513-166">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="70513-167">In code:</span><span class="sxs-lookup"><span data-stu-id="70513-167">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="70513-168">**Or**</span><span class="sxs-lookup"><span data-stu-id="70513-168">**Or**</span></span> 

<span data-ttu-id="70513-169">Update ApplicationInsights.xml (in the resources folder in your project).</span><span class="sxs-lookup"><span data-stu-id="70513-169">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="70513-170">Add the following under the root node:</span><span class="sxs-lookup"><span data-stu-id="70513-170">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="70513-171">Using the XML method, you have to restart the application when you change the value.</span><span class="sxs-lookup"><span data-stu-id="70513-171">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="70513-172">Changing the target</span><span class="sxs-lookup"><span data-stu-id="70513-172">Changing the target</span></span>
<span data-ttu-id="70513-173">**How can I change which Azure resource my project sends data to?**</span><span class="sxs-lookup"><span data-stu-id="70513-173">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="70513-174">[Get the instrumentation key of the new resource.][java]</span><span class="sxs-lookup"><span data-stu-id="70513-174">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="70513-175">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span><span class="sxs-lookup"><span data-stu-id="70513-175">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="70513-176">If you had configured the Instrumentation Key as environment variable please update the value of the environment variable with new iKey.</span><span class="sxs-lookup"><span data-stu-id="70513-176">If you had configured the Instrumentation Key as environment variable please update the value of the environment variable with new iKey.</span></span>
* <span data-ttu-id="70513-177">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span><span class="sxs-lookup"><span data-stu-id="70513-177">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="70513-178">Debug data from the SDK</span><span class="sxs-lookup"><span data-stu-id="70513-178">Debug data from the SDK</span></span>

<span data-ttu-id="70513-179">**How can I find out what the SDK is doing?**</span><span class="sxs-lookup"><span data-stu-id="70513-179">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="70513-180">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span><span class="sxs-lookup"><span data-stu-id="70513-180">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="70513-181">You can also instruct the logger to output to a file:</span><span class="sxs-lookup"><span data-stu-id="70513-181">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="70513-182">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span><span class="sxs-lookup"><span data-stu-id="70513-182">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="70513-183">The Azure start screen</span><span class="sxs-lookup"><span data-stu-id="70513-183">The Azure start screen</span></span>
<span data-ttu-id="70513-184">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span><span class="sxs-lookup"><span data-stu-id="70513-184">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="70513-185">No, it shows the health of Azure servers around the world.</span><span class="sxs-lookup"><span data-stu-id="70513-185">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="70513-186">*From the Azure start board (home screen), how do I find data about my app?*</span><span class="sxs-lookup"><span data-stu-id="70513-186">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="70513-187">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span><span class="sxs-lookup"><span data-stu-id="70513-187">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="70513-188">To get there faster in future, you can pin your app to the start board.</span><span class="sxs-lookup"><span data-stu-id="70513-188">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="70513-189">Intranet servers</span><span class="sxs-lookup"><span data-stu-id="70513-189">Intranet servers</span></span>
<span data-ttu-id="70513-190">**Can I monitor a server on my intranet?**</span><span class="sxs-lookup"><span data-stu-id="70513-190">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="70513-191">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span><span class="sxs-lookup"><span data-stu-id="70513-191">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="70513-192">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="70513-192">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="70513-193">Data retention</span><span class="sxs-lookup"><span data-stu-id="70513-193">Data retention</span></span>
<span data-ttu-id="70513-194">**How long is data retained in the portal? Is it secure?**</span><span class="sxs-lookup"><span data-stu-id="70513-194">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="70513-195">See [Data retention and privacy][data].</span><span class="sxs-lookup"><span data-stu-id="70513-195">See [Data retention and privacy][data].</span></span>

## <a name="debug-logging"></a><span data-ttu-id="70513-196">Debug logging</span><span class="sxs-lookup"><span data-stu-id="70513-196">Debug logging</span></span>
<span data-ttu-id="70513-197">Application Insights uses `org.apache.http`.</span><span class="sxs-lookup"><span data-stu-id="70513-197">Application Insights uses `org.apache.http`.</span></span> <span data-ttu-id="70513-198">This is relocated within Application Insights core jars under the namespace `com.microsoft.applicationinsights.core.dependencies.http`.</span><span class="sxs-lookup"><span data-stu-id="70513-198">This is relocated within Application Insights core jars under the namespace `com.microsoft.applicationinsights.core.dependencies.http`.</span></span> <span data-ttu-id="70513-199">This enables Application Insights to handle scenarios where different versions of the same `org.apache.http` exist in one code base.</span><span class="sxs-lookup"><span data-stu-id="70513-199">This enables Application Insights to handle scenarios where different versions of the same `org.apache.http` exist in one code base.</span></span> 

>[!NOTE]
><span data-ttu-id="70513-200">If you enable DEBUG level logging for all namespaces in the app, it will be honored by all executing modules including `org.apache.http` renamed as `com.microsoft.applicationinsights.core.dependencies.http`.</span><span class="sxs-lookup"><span data-stu-id="70513-200">If you enable DEBUG level logging for all namespaces in the app, it will be honored by all executing modules including `org.apache.http` renamed as `com.microsoft.applicationinsights.core.dependencies.http`.</span></span> <span data-ttu-id="70513-201">Application Insights will not be able to apply filtering for these calls because the log call is being made by the Apache library.</span><span class="sxs-lookup"><span data-stu-id="70513-201">Application Insights will not be able to apply filtering for these calls because the log call is being made by the Apache library.</span></span> <span data-ttu-id="70513-202">DEBUG level logging produce a considerable amount of log data and is not recommended for live production instances.</span><span class="sxs-lookup"><span data-stu-id="70513-202">DEBUG level logging produce a considerable amount of log data and is not recommended for live production instances.</span></span>


## <a name="next-steps"></a><span data-ttu-id="70513-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="70513-203">Next steps</span></span>
<span data-ttu-id="70513-204">**I set up Application Insights for my Java server app. What else can I do?**</span><span class="sxs-lookup"><span data-stu-id="70513-204">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="70513-205">[Monitor availability of your web pages][availability]</span><span class="sxs-lookup"><span data-stu-id="70513-205">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="70513-206">[Monitor web page usage][usage]</span><span class="sxs-lookup"><span data-stu-id="70513-206">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="70513-207">[Track usage and diagnose issues in your device apps][platforms]</span><span class="sxs-lookup"><span data-stu-id="70513-207">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="70513-208">[Write code to track usage of your app][track]</span><span class="sxs-lookup"><span data-stu-id="70513-208">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="70513-209">[Capture diagnostic logs][javalogs]</span><span class="sxs-lookup"><span data-stu-id="70513-209">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="70513-210">Get help</span><span class="sxs-lookup"><span data-stu-id="70513-210">Get help</span></span>
* [<span data-ttu-id="70513-211">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="70513-211">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)
* [<span data-ttu-id="70513-212">File an issue on GitHub</span><span class="sxs-lookup"><span data-stu-id="70513-212">File an issue on GitHub</span></span>](https://github.com/Microsoft/ApplicationInsights-Java/issues)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

