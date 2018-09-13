---
title: Working with Azure Application Insights on Visual Studio | Microsoft Docs
description: Web app performance analysis and diagnostics during debugging and in production.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2016
ms.author: awills
ms.openlocfilehash: a04ab4c00b403dff624933ed395a0728a1141502
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549257"
---
# <a name="working-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="6ee39-103">Working with Azure Application Insights in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ee39-103">Working with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="6ee39-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ee39-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="6ee39-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="6ee39-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="6ee39-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6ee39-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="6ee39-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span><span class="sxs-lookup"><span data-stu-id="6ee39-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="6ee39-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ee39-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="6ee39-109">You can use Visual Studio to analyze telemetry both from your production site and from debuggging runs on your development machine.</span><span class="sxs-lookup"><span data-stu-id="6ee39-109">You can use Visual Studio to analyze telemetry both from your production site and from debuggging runs on your development machine.</span></span> <span data-ttu-id="6ee39-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6ee39-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <a name="run"></a> <span data-ttu-id="6ee39-111">Debug your project</span><span class="sxs-lookup"><span data-stu-id="6ee39-111">Debug your project</span></span>
<span data-ttu-id="6ee39-112">Run your web app in local debug mode by using F5.</span><span class="sxs-lookup"><span data-stu-id="6ee39-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="6ee39-113">Open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="6ee39-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="6ee39-114">In Visual Studio, you'll see a count of the events that have been logged by the Application Insights module in your project.</span><span class="sxs-lookup"><span data-stu-id="6ee39-114">In Visual Studio, you'll see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![In Visual Studio, the Application Insights button shows during debugging.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="6ee39-116">Click this button to search your telemetry.</span><span class="sxs-lookup"><span data-stu-id="6ee39-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="6ee39-117">Application Insights search</span><span class="sxs-lookup"><span data-stu-id="6ee39-117">Application Insights search</span></span>
<span data-ttu-id="6ee39-118">The Application Insights Search window shows events that have been logged.</span><span class="sxs-lookup"><span data-stu-id="6ee39-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="6ee39-119">(If you signed in to Azure when you set up Application Insights, you'll be able to search the same events in the Azure portal.)</span><span class="sxs-lookup"><span data-stu-id="6ee39-119">(If you signed in to Azure when you set up Application Insights, you'll be able to search the same events in the Azure portal.)</span></span>

![Right-click the project and choose Application Insights, Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="6ee39-121">After you select or deselect filters, click the Search button at the end of the text search field.</span><span class="sxs-lookup"><span data-stu-id="6ee39-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="6ee39-122">The free text search works on any fields in the events.</span><span class="sxs-lookup"><span data-stu-id="6ee39-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="6ee39-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span><span class="sxs-lookup"><span data-stu-id="6ee39-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="6ee39-124">Click any event to see its detailed properties.</span><span class="sxs-lookup"><span data-stu-id="6ee39-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="6ee39-125">For requests to your web app, you can click through to the code.</span><span class="sxs-lookup"><span data-stu-id="6ee39-125">For requests to your web app, you can click through to the code.</span></span>

![Under Request Details, click through to the code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/31.png)

<span data-ttu-id="6ee39-127">You can also open related items to help diagnose failed requests or exceptions.</span><span class="sxs-lookup"><span data-stu-id="6ee39-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![Under Request Details, scroll down to related items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/41.png)

## <a name="exceptions-and-failed-requests"></a><span data-ttu-id="6ee39-129">Exceptions and failed requests</span><span class="sxs-lookup"><span data-stu-id="6ee39-129">Exceptions and failed requests</span></span>
<span data-ttu-id="6ee39-130">Exception reports show in the Search window.</span><span class="sxs-lookup"><span data-stu-id="6ee39-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="6ee39-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span><span class="sxs-lookup"><span data-stu-id="6ee39-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="6ee39-132">Click an exception to get a stack trace.</span><span class="sxs-lookup"><span data-stu-id="6ee39-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="6ee39-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span><span class="sxs-lookup"><span data-stu-id="6ee39-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Exception stack trace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/17.png)

## <a name="request-and-exception-summaries-in-the-code"></a><span data-ttu-id="6ee39-135">Request and exception summaries in the code</span><span class="sxs-lookup"><span data-stu-id="6ee39-135">Request and exception summaries in the code</span></span>
<span data-ttu-id="6ee39-136">In the Code Lens line above each handler method, you'll see a count of the requests and exceptions logged by Application Insights in the past 24h.</span><span class="sxs-lookup"><span data-stu-id="6ee39-136">In the Code Lens line above each handler method, you'll see a count of the requests and exceptions logged by Application Insights in the past 24h.</span></span>

![Exception stack trace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="6ee39-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6ee39-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="6ee39-139">More about Application Insights in Code Lens</span><span class="sxs-lookup"><span data-stu-id="6ee39-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="6ee39-140">Trends</span><span class="sxs-lookup"><span data-stu-id="6ee39-140">Trends</span></span>
<span data-ttu-id="6ee39-141">Trends is a tool for visualizing how your app behaves over time.</span><span class="sxs-lookup"><span data-stu-id="6ee39-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="6ee39-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span><span class="sxs-lookup"><span data-stu-id="6ee39-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="6ee39-143">Choose one of five common queries to get started.</span><span class="sxs-lookup"><span data-stu-id="6ee39-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="6ee39-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span><span class="sxs-lookup"><span data-stu-id="6ee39-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="6ee39-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span><span class="sxs-lookup"><span data-stu-id="6ee39-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="6ee39-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="6ee39-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Trends](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/51.png)

<span data-ttu-id="6ee39-148">[More about Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="6ee39-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="6ee39-149">Local monitoring</span><span class="sxs-lookup"><span data-stu-id="6ee39-149">Local monitoring</span></span>
<span data-ttu-id="6ee39-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window will display telemetry from your latest debugging session.</span><span class="sxs-lookup"><span data-stu-id="6ee39-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window will display telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="6ee39-151">This is desirable if you have already published a previous version of your app.</span><span class="sxs-lookup"><span data-stu-id="6ee39-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="6ee39-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span><span class="sxs-lookup"><span data-stu-id="6ee39-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="6ee39-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span><span class="sxs-lookup"><span data-stu-id="6ee39-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="6ee39-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="6ee39-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="6ee39-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span><span class="sxs-lookup"><span data-stu-id="6ee39-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="6ee39-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span><span class="sxs-lookup"><span data-stu-id="6ee39-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="whats-next"></a><span data-ttu-id="6ee39-157">What's next?</span><span class="sxs-lookup"><span data-stu-id="6ee39-157">What's next?</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="6ee39-158">**[Add more data](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="6ee39-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="6ee39-159">Monitor usage, availability, dependencies, exceptions.</span><span class="sxs-lookup"><span data-stu-id="6ee39-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="6ee39-160">Integrate traces from logging frameworks.</span><span class="sxs-lookup"><span data-stu-id="6ee39-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="6ee39-161">Write custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="6ee39-161">Write custom telemetry.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="6ee39-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="6ee39-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="6ee39-164">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span><span class="sxs-lookup"><span data-stu-id="6ee39-164">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio/62.png) |










