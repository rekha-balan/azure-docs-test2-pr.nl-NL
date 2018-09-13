---
title: What is Azure Application Insights? | Microsoft Docs
description: Application Performance Management and usage tracking of your live web application.  Detect, triage and diagnose problems, understand how people use your app.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/07/2017
ms.author: awills
ms.openlocfilehash: bd742ec16b48b7b79c97f762f2ff02f1a03bb3c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552307"
---
# <a name="what-is-application-insights"></a>What is Application Insights?
Application Insights is an extensible Application Performance Management (APM) service for web developers on multiple platforms. Use it to monitor your live web application. It will automatically detect performance anomalies. It includes powerful analytics tools to help you diagnose issues and to understand what users actually do with your app.  It's designed to help you continuously improve  performance and usability. It works for apps on a wide variety of platforms including .NET, Node.js and J2EE, hosted on-premises or in the cloud. It  integrates with your devOps process, and has connection points to a variety of development tools.

![Chart user activity statistics, or drill into specific events.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/00-sample.png)

[Take a look at the intro animation](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>How does Application Insights work?
You install a small instrumentation package in your application, and set up an Application Insights resource in the Microsoft Azure portal. The instrumentation monitors your app and sends telemetry data to the portal. (The application can run anywhere - it doesn't have to be hosted in Azure.)

You can instrument not only the web service application, but also any background components, and the JavaScript in the web pages themselves. 

![Application Insights instrumentation in your app sends telemetry to your Application Insights resource.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/01-scheme.png)


In addition, you can pull in telemetry from the host environments such as performance counters, Azure diagnostics, or Docker logs. You can also set up web tests that periodically send synthetic requests to your web service.

All these telemetry streams are integrated in the Azure portal, where you can apply powerful analytic and search tools to the raw data.


### <a name="whats-the-overhead"></a>What's the overhead?
The impact on your app's performance is very small. Tracking calls are non-blocking, and are batched and sent in a separate thread.

## <a name="what-does-application-insights-monitor"></a>What does Application Insights monitor?

Application Insights is aimed at the development team, to help you understand how your app is performing and how it's being used. It monitors:

* **Request rates, response times, and failure rates** - Find out which pages are most popular, at what times of day, and where your users are. See which pages perform best. If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem. 
* **Dependency rates, response times, and failure rates** - Find out whether external services are slowing you down.
* **Exceptions** - Analyse the aggregated statistics, or pick specific instances and drill into the stack trace and related requests. Both server and browser exceptions are reported.
* **Page views and load performance** - reported by your users' browsers.
* **AJAX calls** from web pages - rates, response times, and failure rates.
* **User and session counts**.
* **Performance counters** from your Windows or Linux server machines, such as CPU, memory, and network usage. 
* **Host diagnostics** from Docker or Azure. 
* **Diagnostic trace logs** from your app - so that you can correlate trace events with requests.
* **Custom events and metrics** that you write yourself in the client or server code, to track business events such as items sold or games won.

## <a name="where-do-i-see-my-telemetry"></a>Where do I see my telemetry?

There are plenty of ways to explore your data. Check out these articles:

|  |  |
| --- | --- |
| [**Application map**](app-insights-app-map.md)<br/>The components of your app, with key metrics and alerts. |![Application map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/appmap-tn.png)  |
| [**Diagnostic search for instance data**](app-insights-diagnostic-search.md)<br/>Search and filter events such as requests, exceptions, dependency calls, log traces, and page views.  |![Search telemetry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/search-tn.png) |
| [**Metrics Explorer for aggregated data**](app-insights-metrics-explorer.md)<br/>Explore, filter, and segment aggregated data such as rates of requests, failures, and exceptions; response times, page load times. |![Metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/metrics-tn.png) |
| [**Dashboards**](app-insights-dashboards.md#dashboards)<br/>Mash up data from multiple resources and share with others. Great for multi-component applications, and for continuous display in the team room. |![Dashboards sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/dashboard-tn.png) |
| [**Live Metrics Stream**](app-insights-live-stream.md)<br/>When you deploy a new build, watch these near-real-time performance indicators to make sure everything works as expected. |![Live metrics sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/live-metrics-tn.png) |
| [**Analytics**](app-insights-analytics.md)<br/>Answer tough questions about your app's performance and usage by using this powerful query language. |![Analytics sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/analytics-tn.png) |
| [**Automatic and manual alerts**](app-insights-alerts.md)<br/>Automatic alerts adapt to your app's normal patterns of telemetry and trigger when there's something outside the usual pattern. You can also set alerts on particular levels of custom or standard metrics. |![Alert sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/alerts-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>See performance data in the code. Go to code from stack traces.|![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/visual-studio-tn.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Integrate usage metrics with other business intelligence.| ![Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/power-bi.png)|
| [**REST API**](https://dev.applicationinsights.io/)<br/>Write code to run queries over your metrics and raw data.| ![REST API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/rest-tn.png) |
| [**Continuous export**](app-insights-export-telemetry.md)<br/>Bulk export of raw data to storage as soon as it arrives. |![Export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>How do I use Application Insights?

### <a name="monitor"></a>Monitor
Install Application Insights in your app, set up [availability web tests](app-insights-monitor-web-app-availability.md), and:

* Set up a [dashboard](app-insights-dashboards.md) for your team room to keep an eye on load, responsiveness, and the performance of your dependencies, page loads, and AJAX calls.
* Discover which are the slowest and most failing requests.
* Watch [Live Stream](app-insights-live-stream.md) when you deploy a new release, to know immediately about any degradation.

### <a name="detect-diagnose"></a>Detect, Diagnose
When you receive an alert or discover a problem:

* Assess how many users are affected.
* Correlate failures with exceptions, dependency calls and traces.
* Examine stack dumps and trace logs.

### <a name="build-measure-learn"></a>Build, Measure, Learn
Measure the effectiveness of each new feature that you deploy.

* Plan to measure how customers use new UX or business features.
* Write custom telemetry into your code.
* Base the next development cycle on hard evidence from your telemetry.

## <a name="get-started"></a>Get started
Application Insights is one of the many services hosted within Microsoft Azure, and telemetry is sent there for analysis and presentation. So before you do anything else, you'll need a subscription to [Microsoft Azure](http://azure.com). It's free to sign up, and if you choose the basic [pricing plan](https://azure.microsoft.com/pricing/details/application-insights/) of Application Insights, there's no charge until your application has grown to have substantial usage. If your organization already has a subscription, they could add your Microsoft account to it.

There are several ways to get started. Begin with whichever works best for you. You can add the others later.

* **At run time: instrument your web app on the server.** Avoids any update to the code. You need admin access to your server.
  * [**IIS on-premises or on a VM**](app-insights-monitor-performance-live-website-now.md)
  * [**Azure web app or VM**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **At development time: add Application Insights to your code.** Allows you to write custom telemetry and to instrument back-end and desktop apps.
  * [Visual Studio](app-insights-asp-net.md) 2013 update 2 or later.
  * Java in [Eclipse](app-insights-java-eclipse.md) or [other tools](app-insights-java-get-started.md)
  * [Node.js](app-insights-nodejs.md)
  * [Other platforms](app-insights-platforms.md)
* **[Instrument your web pages](app-insights-javascript.md)** for page view, AJAX and other client-side telemetry.
* **[Availability tests](app-insights-monitor-web-app-availability.md)** - ping your website regularly from our servers.


## <a name="next-steps"></a>Next steps
Get started at runtime with:

* [IIS server](app-insights-monitor-performance-live-website-now.md)
* [J2EE server](app-insights-java-live.md)

Get started at development time with:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Support and feedback
* Questions and Issues:
  * [Troubleshooting][qna]
  * [MSDN Forum](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [StackOverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Your suggestions:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Application Insights blog](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Videos

[![Animated introduction](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md













