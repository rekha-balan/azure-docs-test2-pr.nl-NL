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
# <a name="smart-detection-in-application-insights"></a>Smart Detection in Application Insights
 Smart Detection automatically warns you of potential performance problems in your web application. It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md). If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert. This feature needs no configuration. It operates if your application sends enough telemetry.

You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.

## <a name="review-your-smart-detections"></a>Review your Smart Detections
You can discover detections in two ways:

* **You receive an email** from Application Insights. Here's a typical example:
  
    ![Email alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-proactive-diagnostics/03.png)
  
    Click the big button to open more detail in the portal.
* **The Smart Detection tile** on your app's overview blade shows a count of recent alerts. Click the tile to see a list of recent alerts.

![View recent detections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-proactive-diagnostics/04.png)

Select an alert to see its details.

## <a name="what-problems-are-detected"></a>What problems are detected?
There are three kinds of detection:

* [Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md). We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors. If the failure rate goes outside the expected envelope, we send an alert.
* [Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md). We search for anomalous patterns in response times and failure rates every day. We correlate these issues with properties such as location, browser, client OS, server instance, and time of day.
* [Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.

(The help links in each notification take you to the relevant articles.)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Next steps
These diagnostic tools help you inspect the telemetry from your app:

* [Metric explorer](app-insights-metrics-explorer.md)
* [Search explorer](app-insights-diagnostic-search.md)
* [Analytics - powerful query language](app-insights-analytics-tour.md)

Smart Detection is completely automatic. But maybe you'd like to set up some more alerts?

* [Manually configured metric alerts](app-insights-alerts.md)
* [Availability web tests](app-insights-monitor-web-app-availability.md) 



