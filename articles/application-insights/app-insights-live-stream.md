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
# <a name="live-metrics-stream-instant-metrics-for-close-monitoring"></a>Live Metrics Stream: instant metrics for close monitoring
Live Metrics Stream shows you your [Application Insights](app-insights-overview.md) metrics right at this very moment, with a near-real-time latency of one second. This immediate monitoring is very useful when you’re releasing a new build and want to make sure that everything is working as expected, or investigating an incident in real time.

Unlike [Metrics Explorer](app-insights-metrics-explorer.md), Live Metrics Stream displays a fixed set of metrics. The data persists only for as long as it's on the chart, and is then discarded.

Live Metrics Stream data is free: it doesn't add to your bill. It is available for ASP.NET and Java applications.

![Live Metrics Stream video](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/youtube.png) [Live Metrics Stream video](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

![In the Overview blade, click Live Stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream.png)



## <a name="live-failures"></a>Live failures

If any failures or exceptions are logged, Live Stream picks out a sample of them. Click **Pause** to hold a specific sample, and select an event to show its details.

![Sampled live failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream-failures.png)


Live Metrics Stream is available with the latest version of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).

## <a name="filter-by-server-instance"></a>Filter by server instance

If you want to monitor a particular server role instance, you can filter by server.

![Sampled live failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-live-stream/live-stream-filter.png)


## <a name="troubleshooting"></a>Troubleshooting

No data? Live Metrics Stream uses a different port than other Application Insights telemetry. Make sure [those ports](app-insights-ip-addresses.md) are open in your firewall.



## <a name="next-steps"></a>Next steps
* [Monitoring usage with Application Insights](app-insights-web-track-usage.md)
* [Using Diagnostic Search](app-insights-diagnostic-search.md)





