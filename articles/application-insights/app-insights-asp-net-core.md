---
title: Azure Application Insights for ASP.NET Core | Microsoft Docs
description: Monitor web applications for availability, performance and usage.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 0dd516f26014e96786d2b3c4711d36ab9dd8fdc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549091"
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="65a1c-103">Application Insights for ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="65a1c-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="65a1c-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span><span class="sxs-lookup"><span data-stu-id="65a1c-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="65a1c-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span><span class="sxs-lookup"><span data-stu-id="65a1c-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="65a1c-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="65a1c-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="65a1c-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span><span class="sxs-lookup"><span data-stu-id="65a1c-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="65a1c-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="65a1c-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="65a1c-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="65a1c-110">Getting started</span></span>

* <span data-ttu-id="65a1c-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="65a1c-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="65a1c-112">[Learn more](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="65a1c-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="65a1c-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="65a1c-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="65a1c-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span><span class="sxs-lookup"><span data-stu-id="65a1c-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="65a1c-115">Using Application Insights</span><span class="sxs-lookup"><span data-stu-id="65a1c-115">Using Application Insights</span></span>
<span data-ttu-id="65a1c-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span><span class="sxs-lookup"><span data-stu-id="65a1c-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="65a1c-117">In a separate browser window, use your app for a while.</span><span class="sxs-lookup"><span data-stu-id="65a1c-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="65a1c-118">You'll see data appearing in the Application Insights charts.</span><span class="sxs-lookup"><span data-stu-id="65a1c-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="65a1c-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span><span class="sxs-lookup"><span data-stu-id="65a1c-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="65a1c-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span><span class="sxs-lookup"><span data-stu-id="65a1c-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="65a1c-121">Click any chart to see more charts and data.</span><span class="sxs-lookup"><span data-stu-id="65a1c-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="65a1c-122">Views in the portal fall into three main categories:</span><span class="sxs-lookup"><span data-stu-id="65a1c-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="65a1c-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="65a1c-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="65a1c-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span><span class="sxs-lookup"><span data-stu-id="65a1c-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="65a1c-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="65a1c-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="65a1c-126">Filter and search in the events, and navigate among related events to investigate issues.</span><span class="sxs-lookup"><span data-stu-id="65a1c-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="65a1c-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span><span class="sxs-lookup"><span data-stu-id="65a1c-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="65a1c-128">Alerts</span><span class="sxs-lookup"><span data-stu-id="65a1c-128">Alerts</span></span>
* <span data-ttu-id="65a1c-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span><span class="sxs-lookup"><span data-stu-id="65a1c-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="65a1c-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span><span class="sxs-lookup"><span data-stu-id="65a1c-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="65a1c-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span><span class="sxs-lookup"><span data-stu-id="65a1c-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="65a1c-132">Video</span><span class="sxs-lookup"><span data-stu-id="65a1c-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="65a1c-133">Open source</span><span class="sxs-lookup"><span data-stu-id="65a1c-133">Open source</span></span>
[<span data-ttu-id="65a1c-134">Read and contribute to the code</span><span class="sxs-lookup"><span data-stu-id="65a1c-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="65a1c-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="65a1c-135">Next steps</span></span>
* <span data-ttu-id="65a1c-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span><span class="sxs-lookup"><span data-stu-id="65a1c-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="65a1c-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span><span class="sxs-lookup"><span data-stu-id="65a1c-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="65a1c-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span><span class="sxs-lookup"><span data-stu-id="65a1c-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="65a1c-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span><span class="sxs-lookup"><span data-stu-id="65a1c-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 


