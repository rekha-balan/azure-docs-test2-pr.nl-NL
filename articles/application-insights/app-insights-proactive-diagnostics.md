---
title: Smart Detection in Azure Application Insights | Microsoft Docs
description: Application Insights performs automatic deep analysis of your app telemetry and warns you of potential problems.
services: application-insights
documentationcenter: windows
author: rakefetj
manager: douge
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: awills
ms.openlocfilehash: 99a260343557489a5d08a75ed21856208d6254c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552819"
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="6ac94-103">Smart Detection in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6ac94-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="6ac94-104">Smart Detection automatically warns you of potential performance problems in your web application.</span><span class="sxs-lookup"><span data-stu-id="6ac94-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="6ac94-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ac94-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6ac94-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span><span class="sxs-lookup"><span data-stu-id="6ac94-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="6ac94-107">This feature needs no configuration.</span><span class="sxs-lookup"><span data-stu-id="6ac94-107">This feature needs no configuration.</span></span> <span data-ttu-id="6ac94-108">It operates if your application sends enough telemetry.</span><span class="sxs-lookup"><span data-stu-id="6ac94-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="6ac94-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span><span class="sxs-lookup"><span data-stu-id="6ac94-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="6ac94-110">Review your Smart Detections</span><span class="sxs-lookup"><span data-stu-id="6ac94-110">Review your Smart Detections</span></span>
<span data-ttu-id="6ac94-111">You can discover detections in two ways:</span><span class="sxs-lookup"><span data-stu-id="6ac94-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="6ac94-112">**You receive an email** from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6ac94-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="6ac94-113">Here's a typical example:</span><span class="sxs-lookup"><span data-stu-id="6ac94-113">Here's a typical example:</span></span>
  
    ![Email alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="6ac94-115">Click the big button to open more detail in the portal.</span><span class="sxs-lookup"><span data-stu-id="6ac94-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="6ac94-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span><span class="sxs-lookup"><span data-stu-id="6ac94-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="6ac94-117">Click the tile to see a list of recent alerts.</span><span class="sxs-lookup"><span data-stu-id="6ac94-117">Click the tile to see a list of recent alerts.</span></span>

![View recent detections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="6ac94-119">Select an alert to see its details.</span><span class="sxs-lookup"><span data-stu-id="6ac94-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="6ac94-120">What problems are detected?</span><span class="sxs-lookup"><span data-stu-id="6ac94-120">What problems are detected?</span></span>
<span data-ttu-id="6ac94-121">There are three kinds of detection:</span><span class="sxs-lookup"><span data-stu-id="6ac94-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="6ac94-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6ac94-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="6ac94-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span><span class="sxs-lookup"><span data-stu-id="6ac94-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="6ac94-124">If the failure rate goes outside the expected envelope, we send an alert.</span><span class="sxs-lookup"><span data-stu-id="6ac94-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="6ac94-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6ac94-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="6ac94-126">We search for anomalous patterns in response times and failure rates every day.</span><span class="sxs-lookup"><span data-stu-id="6ac94-126">We search for anomalous patterns in response times and failure rates every day.</span></span> <span data-ttu-id="6ac94-127">We correlate these issues with properties such as location, browser, client OS, server instance, and time of day.</span><span class="sxs-lookup"><span data-stu-id="6ac94-127">We correlate these issues with properties such as location, browser, client OS, server instance, and time of day.</span></span>
* <span data-ttu-id="6ac94-128">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="6ac94-128">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="6ac94-129">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span><span class="sxs-lookup"><span data-stu-id="6ac94-129">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="6ac94-130">(The help links in each notification take you to the relevant articles.)</span><span class="sxs-lookup"><span data-stu-id="6ac94-130">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="6ac94-131">Video</span><span class="sxs-lookup"><span data-stu-id="6ac94-131">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="6ac94-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ac94-132">Next steps</span></span>
<span data-ttu-id="6ac94-133">These diagnostic tools help you inspect the telemetry from your app:</span><span class="sxs-lookup"><span data-stu-id="6ac94-133">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="6ac94-134">Metric explorer</span><span class="sxs-lookup"><span data-stu-id="6ac94-134">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="6ac94-135">Search explorer</span><span class="sxs-lookup"><span data-stu-id="6ac94-135">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="6ac94-136">Analytics - powerful query language</span><span class="sxs-lookup"><span data-stu-id="6ac94-136">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="6ac94-137">Smart Detection is completely automatic.</span><span class="sxs-lookup"><span data-stu-id="6ac94-137">Smart Detection is completely automatic.</span></span> <span data-ttu-id="6ac94-138">But maybe you'd like to set up some more alerts?</span><span class="sxs-lookup"><span data-stu-id="6ac94-138">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="6ac94-139">Manually configured metric alerts</span><span class="sxs-lookup"><span data-stu-id="6ac94-139">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="6ac94-140">Availability web tests</span><span class="sxs-lookup"><span data-stu-id="6ac94-140">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 



