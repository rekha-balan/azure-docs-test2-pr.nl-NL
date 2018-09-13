---
title: Monitor your Node.js app with Azure Application Insights  | Microsoft Docs
description: Analyze usage, availability and performance of your on-premises or Microsoft Azure web application by using Application Insights.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 33bbe9741ea59c5684a68a127ab13c6276952b5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670154"
---
# <a name="add-application-insights-sdk-to-monitor-your-nodejs-app"></a><span data-ttu-id="a62e8-103">Add Application Insights SDK to monitor your Node.js app</span><span class="sxs-lookup"><span data-stu-id="a62e8-103">Add Application Insights SDK to monitor your Node.js app</span></span>


<span data-ttu-id="a62e8-104">[Azure Application Insights](app-insights-overview.md) monitors your live application to help you [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [discover how your app is used](app-insights-web-track-usage.md).</span><span class="sxs-lookup"><span data-stu-id="a62e8-104">[Azure Application Insights](app-insights-overview.md) monitors your live application to help you [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [discover how your app is used](app-insights-web-track-usage.md).</span></span> <span data-ttu-id="a62e8-105">It works for apps that are hosted on your own on-premises IIS servers or on Azure VMs, as well as Azure web apps.</span><span class="sxs-lookup"><span data-stu-id="a62e8-105">It works for apps that are hosted on your own on-premises IIS servers or on Azure VMs, as well as Azure web apps.</span></span>

<span data-ttu-id="a62e8-106">The SDK provides automatic collection of incoming HTTP request rates and responses, performance counters (CPU, memory, RPS), and unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="a62e8-106">The SDK provides automatic collection of incoming HTTP request rates and responses, performance counters (CPU, memory, RPS), and unhandled exceptions.</span></span> <span data-ttu-id="a62e8-107">In addition, you can add custom calls to track dependencies, metrics, or other events.</span><span class="sxs-lookup"><span data-stu-id="a62e8-107">In addition, you can add custom calls to track dependencies, metrics, or other events.</span></span>

![Example performance monitoring charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-nodejs/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="a62e8-109">Before you start</span><span class="sxs-lookup"><span data-stu-id="a62e8-109">Before you start</span></span>
<span data-ttu-id="a62e8-110">You need:</span><span class="sxs-lookup"><span data-stu-id="a62e8-110">You need:</span></span>

* <span data-ttu-id="a62e8-111">A subscription to [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a62e8-111">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="a62e8-112">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="a62e8-112">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>

## <a name="add"></a><span data-ttu-id="a62e8-113">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="a62e8-113">Create an Application Insights resource</span></span>
<span data-ttu-id="a62e8-114">Sign in to the [Azure portal][portal], and create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="a62e8-114">Sign in to the [Azure portal][portal], and create a new Application Insights resource.</span></span> <span data-ttu-id="a62e8-115">A [resource][roles] in Azure is an instance of a service.</span><span class="sxs-lookup"><span data-stu-id="a62e8-115">A [resource][roles] in Azure is an instance of a service.</span></span> <span data-ttu-id="a62e8-116">This resource is where telemetry from your app will be analyzed and presented to you.</span><span class="sxs-lookup"><span data-stu-id="a62e8-116">This resource is where telemetry from your app will be analyzed and presented to you.</span></span>

![Click New, Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-nodejs/01-new-asp.png)

<span data-ttu-id="a62e8-118">Choose General as the application type.</span><span class="sxs-lookup"><span data-stu-id="a62e8-118">Choose General as the application type.</span></span> <span data-ttu-id="a62e8-119">The choice of application type sets the default content of the resource blades and the properties visible in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="a62e8-119">The choice of application type sets the default content of the resource blades and the properties visible in [Metrics Explorer][metrics].</span></span>

#### <a name="copy-the-instrumentation-key"></a><span data-ttu-id="a62e8-120">Copy the Instrumentation Key</span><span class="sxs-lookup"><span data-stu-id="a62e8-120">Copy the Instrumentation Key</span></span>
<span data-ttu-id="a62e8-121">The key identifies the resource, and you'll install it soon in the SDK to direct data to the resource.</span><span class="sxs-lookup"><span data-stu-id="a62e8-121">The key identifies the resource, and you'll install it soon in the SDK to direct data to the resource.</span></span>

![Click Properties, select the key, and press ctrl+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-nodejs/02-props-asp.png)

## <a name="sdk"></a> <span data-ttu-id="a62e8-123">Install the SDK in your application</span><span class="sxs-lookup"><span data-stu-id="a62e8-123">Install the SDK in your application</span></span>
```
npm install applicationinsights --save
```

## <a name="usage"></a><span data-ttu-id="a62e8-124">Usage</span><span class="sxs-lookup"><span data-stu-id="a62e8-124">Usage</span></span>
<span data-ttu-id="a62e8-125">This will enable request monitoring, unhandled exception tracking, and system performance monitoring (CPU/Memory/RPS).</span><span class="sxs-lookup"><span data-stu-id="a62e8-125">This will enable request monitoring, unhandled exception tracking, and system performance monitoring (CPU/Memory/RPS).</span></span>

```javascript

var appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>").start();
```

<span data-ttu-id="a62e8-126">The instrumentation key can also be set in the environment variable APPINSIGHTS_INSTRUMENTATIONKEY.</span><span class="sxs-lookup"><span data-stu-id="a62e8-126">The instrumentation key can also be set in the environment variable APPINSIGHTS_INSTRUMENTATIONKEY.</span></span> <span data-ttu-id="a62e8-127">If this is done, no argument is required when calling `appInsights.setup()` or `appInsights.getClient()`.</span><span class="sxs-lookup"><span data-stu-id="a62e8-127">If this is done, no argument is required when calling `appInsights.setup()` or `appInsights.getClient()`.</span></span>

<span data-ttu-id="a62e8-128">You can try the SDK without sending telemetry: set the instrumentation key to a non-empty string.</span><span class="sxs-lookup"><span data-stu-id="a62e8-128">You can try the SDK without sending telemetry: set the instrumentation key to a non-empty string.</span></span>

## <a name="run"></a> <span data-ttu-id="a62e8-129">Run your project</span><span class="sxs-lookup"><span data-stu-id="a62e8-129">Run your project</span></span>
<span data-ttu-id="a62e8-130">Run your application and try it out: open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="a62e8-130">Run your application and try it out: open different pages to generate some telemetry.</span></span>

## <a name="monitor"></a> <span data-ttu-id="a62e8-131">View your telemetry</span><span class="sxs-lookup"><span data-stu-id="a62e8-131">View your telemetry</span></span>
<span data-ttu-id="a62e8-132">Return to the [Azure portal](https://portal.azure.com) and browse to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="a62e8-132">Return to the [Azure portal](https://portal.azure.com) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="a62e8-133">Look for data in the Overview page.</span><span class="sxs-lookup"><span data-stu-id="a62e8-133">Look for data in the Overview page.</span></span> <span data-ttu-id="a62e8-134">At first, you'll just see one or two points.</span><span class="sxs-lookup"><span data-stu-id="a62e8-134">At first, you'll just see one or two points.</span></span> <span data-ttu-id="a62e8-135">For example:</span><span class="sxs-lookup"><span data-stu-id="a62e8-135">For example:</span></span>

![Click through to more data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="a62e8-137">Click through any chart to see more detailed metrics.</span><span class="sxs-lookup"><span data-stu-id="a62e8-137">Click through any chart to see more detailed metrics.</span></span> <span data-ttu-id="a62e8-138">[Learn more about metrics.][perf]</span><span class="sxs-lookup"><span data-stu-id="a62e8-138">[Learn more about metrics.][perf]</span></span>

#### <a name="no-data"></a><span data-ttu-id="a62e8-139">No data?</span><span class="sxs-lookup"><span data-stu-id="a62e8-139">No data?</span></span>
* <span data-ttu-id="a62e8-140">Use the application, opening different pages so that it generates some telemetry.</span><span class="sxs-lookup"><span data-stu-id="a62e8-140">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="a62e8-141">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span><span class="sxs-lookup"><span data-stu-id="a62e8-141">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="a62e8-142">Sometimes it takes events a little while longer to get through the metrics pipeline.</span><span class="sxs-lookup"><span data-stu-id="a62e8-142">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="a62e8-143">Wait a few seconds and click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="a62e8-143">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="a62e8-144">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span><span class="sxs-lookup"><span data-stu-id="a62e8-144">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="a62e8-145">See [Troubleshooting][qna].</span><span class="sxs-lookup"><span data-stu-id="a62e8-145">See [Troubleshooting][qna].</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a62e8-146">Publish your app</span><span class="sxs-lookup"><span data-stu-id="a62e8-146">Publish your app</span></span>
<span data-ttu-id="a62e8-147">Now deploy your application to IIS or to Azure and watch the data accumulate.</span><span class="sxs-lookup"><span data-stu-id="a62e8-147">Now deploy your application to IIS or to Azure and watch the data accumulate.</span></span>

#### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="a62e8-148">No data after you publish to your server?</span><span class="sxs-lookup"><span data-stu-id="a62e8-148">No data after you publish to your server?</span></span>
<span data-ttu-id="a62e8-149">Check that [the necessary firewall ports are open](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="a62e8-149">Check that [the necessary firewall ports are open](app-insights-ip-addresses.md).</span></span>

#### <a name="trouble-on-your-build-server"></a><span data-ttu-id="a62e8-150">Trouble on your build server?</span><span class="sxs-lookup"><span data-stu-id="a62e8-150">Trouble on your build server?</span></span>
<span data-ttu-id="a62e8-151">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="a62e8-151">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

## <a name="customized-usage"></a><span data-ttu-id="a62e8-152">Customized Usage</span><span class="sxs-lookup"><span data-stu-id="a62e8-152">Customized Usage</span></span>
### <a name="disabling-auto-collection"></a><span data-ttu-id="a62e8-153">Disabling auto-collection</span><span class="sxs-lookup"><span data-stu-id="a62e8-153">Disabling auto-collection</span></span>
```javascript
import appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoCollectRequests(false)
    .setAutoCollectPerformance(false)
    .setAutoCollectExceptions(false)
    // no telemetry will be sent until .start() is called
    .start();
```

### <a name="custom-monitoring"></a><span data-ttu-id="a62e8-154">Custom monitoring</span><span class="sxs-lookup"><span data-stu-id="a62e8-154">Custom monitoring</span></span>
```javascript
import appInsights = require("applicationinsights");
var client = appInsights.getClient();

client.trackEvent("custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");
```

<span data-ttu-id="a62e8-155">[Learn more about the telemetry API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a62e8-155">[Learn more about the telemetry API](app-insights-api-custom-events-metrics.md).</span></span>

### <a name="using-multiple-instrumentation-keys"></a><span data-ttu-id="a62e8-156">Using multiple instrumentation keys</span><span class="sxs-lookup"><span data-stu-id="a62e8-156">Using multiple instrumentation keys</span></span>
```javascript
import appInsights = require("applicationinsights");

// configure auto-collection with one instrumentation key
appInsights.setup("<instrumentation_key>").start();

// get a client for another instrumentation key
var otherClient = appInsights.getClient("<other_instrumentation_key>");
otherClient.trackEvent("custom event");
```

## <a name="examples"></a><span data-ttu-id="a62e8-157">Examples</span><span class="sxs-lookup"><span data-stu-id="a62e8-157">Examples</span></span>
### <a name="tracking-dependency"></a><span data-ttu-id="a62e8-158">Tracking dependency</span><span class="sxs-lookup"><span data-stu-id="a62e8-158">Tracking dependency</span></span>
```javascript
import appInsights = require("applicationinsights");
var client = appInsights.getClient();

var startTime = Date.now();
// execute dependency call
var endTime = Date.now();

var elapsedTime = endTime - startTime;
var success = true;
client.trackDependency("dependency name", "command name", elapsedTime, success);
```



### <a name="manual-request-tracking-of-all-get-requests"></a><span data-ttu-id="a62e8-159">Manual request tracking of all "GET" requests</span><span class="sxs-lookup"><span data-stu-id="a62e8-159">Manual request tracking of all "GET" requests</span></span>
```javascript
var http = require("http");
var appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoCollectRequests(false) // disable auto-collection of requests for this example
    .start();

// assign common properties to all telemetry sent from the default client
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};

// track a system startup event
appInsights.client.trackEvent("server start");

// create server
var port = process.env.port || 1337
var server = http.createServer(function (req, res) {
    // track all "GET" requests
    if(req.method === "GET") {
        appInsights.client.trackRequest(req, res);
    }

    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello World\n");
}).listen(port);

// track startup time of the server as a custom metric
var start = +new Date;
server.on("listening", () => {
    var end = +new Date;
    var duration = end - start;
    appInsights.client.trackMetric("StartupTime", duration);
});
```

## <a name="video"></a><span data-ttu-id="a62e8-160">Video</span><span class="sxs-lookup"><span data-stu-id="a62e8-160">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="a62e8-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="a62e8-161">Next steps</span></span>
* [<span data-ttu-id="a62e8-162">Monitor your telemetry in the portal</span><span class="sxs-lookup"><span data-stu-id="a62e8-162">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="a62e8-163">Write Analytics queries over your telemetry</span><span class="sxs-lookup"><span data-stu-id="a62e8-163">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--Link references-->

[knowUsers]: app-insights-web-track-usage.md
[metrics]: app-insights-metrics-explorer.md
[perf]: app-insights-web-monitor-performance.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md




