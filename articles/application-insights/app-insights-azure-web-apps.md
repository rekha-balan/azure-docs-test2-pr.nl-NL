---
title: Monitor Azure web app performance | Microsoft Docs
description: Application performance monitoring for Azure web apps. Chart load and response time, dependency information and set alerts on performance.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/30/2017
ms.author: awills
ms.openlocfilehash: 2521a4f6e51bcbb79c0d78169411b54d3ea4f160
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556128"
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="2ec25-104">Monitor Azure web app performance</span><span class="sxs-lookup"><span data-stu-id="2ec25-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="2ec25-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ec25-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="2ec25-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span><span class="sxs-lookup"><span data-stu-id="2ec25-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="2ec25-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span><span class="sxs-lookup"><span data-stu-id="2ec25-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="2ec25-108">Run time or build time</span><span class="sxs-lookup"><span data-stu-id="2ec25-108">Run time or build time</span></span>
<span data-ttu-id="2ec25-109">You can configure monitoring by instrumenting the app in either of two ways:</span><span class="sxs-lookup"><span data-stu-id="2ec25-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="2ec25-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span><span class="sxs-lookup"><span data-stu-id="2ec25-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="2ec25-111">It isn't necessary to rebuild or re-install your app.</span><span class="sxs-lookup"><span data-stu-id="2ec25-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="2ec25-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span><span class="sxs-lookup"><span data-stu-id="2ec25-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="2ec25-113">**Build time** - You can install a package in your app in development.</span><span class="sxs-lookup"><span data-stu-id="2ec25-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="2ec25-114">This option is more versatile.</span><span class="sxs-lookup"><span data-stu-id="2ec25-114">This option is more versatile.</span></span> <span data-ttu-id="2ec25-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span><span class="sxs-lookup"><span data-stu-id="2ec25-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="2ec25-116">You can log specific activities or record events according to the semantics of your app domain.</span><span class="sxs-lookup"><span data-stu-id="2ec25-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="2ec25-117">Run time instrumentation with Application Insights</span><span class="sxs-lookup"><span data-stu-id="2ec25-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="2ec25-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span><span class="sxs-lookup"><span data-stu-id="2ec25-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="2ec25-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="2ec25-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Analytics query language.</span></span> 

1. <span data-ttu-id="2ec25-120">**Select Application Insights** in the Azure control panel for your web app.</span><span class="sxs-lookup"><span data-stu-id="2ec25-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![Under Monitoring, choose Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="2ec25-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span><span class="sxs-lookup"><span data-stu-id="2ec25-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="2ec25-123">**Instrument your web app** after Application Insights has been installed.</span><span class="sxs-lookup"><span data-stu-id="2ec25-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrument your web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/restart-web-app-for-insights.png)
3. <span data-ttu-id="2ec25-125">**Monitor your app**.</span><span class="sxs-lookup"><span data-stu-id="2ec25-125">**Monitor your app**.</span></span>  <span data-ttu-id="2ec25-126">[Expore the data](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="2ec25-126">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="2ec25-127">Later, you can build and redeploy the app with Application Insights if you want.</span><span class="sxs-lookup"><span data-stu-id="2ec25-127">Later, you can build and redeploy the app with Application Insights if you want.</span></span>

<span data-ttu-id="2ec25-128">*How do I remove Application Insights, or switch to sending to another resource?*</span><span class="sxs-lookup"><span data-stu-id="2ec25-128">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="2ec25-129">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="2ec25-129">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="2ec25-130">Delete the Application Insights extension.</span><span class="sxs-lookup"><span data-stu-id="2ec25-130">Delete the Application Insights extension.</span></span> <span data-ttu-id="2ec25-131">Then under Monitoring, choose Application Insights and create or select the resource you want.</span><span class="sxs-lookup"><span data-stu-id="2ec25-131">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="2ec25-132">Build the app with Application Insights</span><span class="sxs-lookup"><span data-stu-id="2ec25-132">Build the app with Application Insights</span></span>
<span data-ttu-id="2ec25-133">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span><span class="sxs-lookup"><span data-stu-id="2ec25-133">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="2ec25-134">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span><span class="sxs-lookup"><span data-stu-id="2ec25-134">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="2ec25-135">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span><span class="sxs-lookup"><span data-stu-id="2ec25-135">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="2ec25-136">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2ec25-136">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Right-click the web project and choose Add or Configure Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="2ec25-138">If you're asked to sign in, use the credentials for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="2ec25-138">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="2ec25-139">The operation has two effects:</span><span class="sxs-lookup"><span data-stu-id="2ec25-139">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="2ec25-140">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span><span class="sxs-lookup"><span data-stu-id="2ec25-140">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="2ec25-141">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span><span class="sxs-lookup"><span data-stu-id="2ec25-141">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="2ec25-142">**Test the telemetry** by running the app in your development machine (F5).</span><span class="sxs-lookup"><span data-stu-id="2ec25-142">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="2ec25-143">**Publish the app** to Azure in the usual way.</span><span class="sxs-lookup"><span data-stu-id="2ec25-143">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="2ec25-144">*How do I switch to sending to a different Application Insights resource?*</span><span class="sxs-lookup"><span data-stu-id="2ec25-144">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="2ec25-145">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span><span class="sxs-lookup"><span data-stu-id="2ec25-145">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="2ec25-146">You get the option to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="2ec25-146">You get the option to create a new resource.</span></span> <span data-ttu-id="2ec25-147">Rebuild and redeploy.</span><span class="sxs-lookup"><span data-stu-id="2ec25-147">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="2ec25-148">Explore the data</span><span class="sxs-lookup"><span data-stu-id="2ec25-148">Explore the data</span></span>
1. <span data-ttu-id="2ec25-149">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span><span class="sxs-lookup"><span data-stu-id="2ec25-149">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="2ec25-150">It's very useful display when you're republishing your app - you can see any problems immediately.</span><span class="sxs-lookup"><span data-stu-id="2ec25-150">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="2ec25-151">Click through to the full Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="2ec25-151">Click through to the full Application Insights resource.</span></span>

    ![Click through](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="2ec25-153">You can also go there either directly from Azure resource navigation.</span><span class="sxs-lookup"><span data-stu-id="2ec25-153">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="2ec25-154">Click through any chart to get more detail:</span><span class="sxs-lookup"><span data-stu-id="2ec25-154">Click through any chart to get more detail:</span></span>
   
    ![On the Application Insights overview blade, click a chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="2ec25-156">You can [customize metrics blades](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="2ec25-156">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="2ec25-157">Click through further to see individual events and their properties:</span><span class="sxs-lookup"><span data-stu-id="2ec25-157">Click through further to see individual events and their properties:</span></span>
   
    ![Click an event type to open a search filtered on that type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="2ec25-159">Notice the "..." link to open all properties.</span><span class="sxs-lookup"><span data-stu-id="2ec25-159">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="2ec25-160">You can [customize searches](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="2ec25-160">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="2ec25-161">For more powerful searches over your telemetry, use the [Analytics query language](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="2ec25-161">For more powerful searches over your telemetry, use the [Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="2ec25-162">More telemetry</span><span class="sxs-lookup"><span data-stu-id="2ec25-162">More telemetry</span></span>

* [<span data-ttu-id="2ec25-163">Web page load data</span><span class="sxs-lookup"><span data-stu-id="2ec25-163">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="2ec25-164">Custom telemetry</span><span class="sxs-lookup"><span data-stu-id="2ec25-164">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="2ec25-165">Video</span><span class="sxs-lookup"><span data-stu-id="2ec25-165">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="2ec25-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ec25-166">Next steps</span></span>
* <span data-ttu-id="2ec25-167">[Run the profiler on your live app](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="2ec25-167">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="2ec25-168">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2ec25-168">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="2ec25-169">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="2ec25-169">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="2ec25-170">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span><span class="sxs-lookup"><span data-stu-id="2ec25-170">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="2ec25-171">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span><span class="sxs-lookup"><span data-stu-id="2ec25-171">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="2ec25-172">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span><span class="sxs-lookup"><span data-stu-id="2ec25-172">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>







