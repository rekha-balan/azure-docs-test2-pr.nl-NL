---
title: Live Metrics Stream in Azure Application Insights | Microsoft Docs
description: Monitor the performance of your web app in real time, to observe the effects of a release or other change.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: awills
ms.openlocfilehash: ba2778e63d2e9bf0dc46ff35791d7378722aaf2d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550349"
---
# <a name="live-metrics-stream-instant-metrics-for-close-monitoring"></a><span data-ttu-id="09603-103">Live Metrics Stream: instant metrics for close monitoring</span><span class="sxs-lookup"><span data-stu-id="09603-103">Live Metrics Stream: instant metrics for close monitoring</span></span>
<span data-ttu-id="09603-104">Live Metrics Stream shows you your [Application Insights](app-insights-overview.md) metrics right at this very moment, with a near-real-time latency of one second.</span><span class="sxs-lookup"><span data-stu-id="09603-104">Live Metrics Stream shows you your [Application Insights](app-insights-overview.md) metrics right at this very moment, with a near-real-time latency of one second.</span></span> <span data-ttu-id="09603-105">This immediate monitoring is very useful when you’re releasing a new build and want to make sure that everything is working as expected, or investigating an incident in real time.</span><span class="sxs-lookup"><span data-stu-id="09603-105">This immediate monitoring is very useful when you’re releasing a new build and want to make sure that everything is working as expected, or investigating an incident in real time.</span></span>

<span data-ttu-id="09603-106">Unlike [Metrics Explorer](app-insights-metrics-explorer.md), Live Metrics Stream displays a fixed set of metrics.</span><span class="sxs-lookup"><span data-stu-id="09603-106">Unlike [Metrics Explorer](app-insights-metrics-explorer.md), Live Metrics Stream displays a fixed set of metrics.</span></span> <span data-ttu-id="09603-107">The data persists only for as long as it's on the chart, and is then discarded.</span><span class="sxs-lookup"><span data-stu-id="09603-107">The data persists only for as long as it's on the chart, and is then discarded.</span></span>

<span data-ttu-id="09603-108">Live Metrics Stream data is free: it doesn't add to your bill.</span><span class="sxs-lookup"><span data-stu-id="09603-108">Live Metrics Stream data is free: it doesn't add to your bill.</span></span> <span data-ttu-id="09603-109">It is available for ASP.NET and Java applications.</span><span class="sxs-lookup"><span data-stu-id="09603-109">It is available for ASP.NET and Java applications.</span></span>

<span data-ttu-id="09603-110">![Live Metrics Stream video](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/youtube.png) [Live Metrics Stream video](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="09603-110">![Live Metrics Stream video](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/youtube.png) [Live Metrics Stream video](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

![In the Overview blade, click Live Stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream.png)



## <a name="live-failures"></a><span data-ttu-id="09603-112">Live failures</span><span class="sxs-lookup"><span data-stu-id="09603-112">Live failures</span></span>

<span data-ttu-id="09603-113">If any failures or exceptions are logged, Live Stream picks out a sample of them.</span><span class="sxs-lookup"><span data-stu-id="09603-113">If any failures or exceptions are logged, Live Stream picks out a sample of them.</span></span> <span data-ttu-id="09603-114">Click **Pause** to hold a specific sample, and select an event to show its details.</span><span class="sxs-lookup"><span data-stu-id="09603-114">Click **Pause** to hold a specific sample, and select an event to show its details.</span></span>

![Sampled live failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream-failures.png)


<span data-ttu-id="09603-116">Live Metrics Stream is available with the latest version of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="09603-116">Live Metrics Stream is available with the latest version of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span>

## <a name="filter-by-server-instance"></a><span data-ttu-id="09603-117">Filter by server instance</span><span class="sxs-lookup"><span data-stu-id="09603-117">Filter by server instance</span></span>

<span data-ttu-id="09603-118">If you want to monitor a particular server role instance, you can filter by server.</span><span class="sxs-lookup"><span data-stu-id="09603-118">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Sampled live failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream-filter.png)


## <a name="troubleshooting"></a><span data-ttu-id="09603-120">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="09603-120">Troubleshooting</span></span>

<span data-ttu-id="09603-121">No data?</span><span class="sxs-lookup"><span data-stu-id="09603-121">No data?</span></span> <span data-ttu-id="09603-122">Live Metrics Stream uses a different port than other Application Insights telemetry.</span><span class="sxs-lookup"><span data-stu-id="09603-122">Live Metrics Stream uses a different port than other Application Insights telemetry.</span></span> <span data-ttu-id="09603-123">Make sure [those ports](app-insights-ip-addresses.md) are open in your firewall.</span><span class="sxs-lookup"><span data-stu-id="09603-123">Make sure [those ports](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="09603-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="09603-124">Next steps</span></span>
* [<span data-ttu-id="09603-125">Monitoring usage with Application Insights</span><span class="sxs-lookup"><span data-stu-id="09603-125">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="09603-126">Using Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="09603-126">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)





