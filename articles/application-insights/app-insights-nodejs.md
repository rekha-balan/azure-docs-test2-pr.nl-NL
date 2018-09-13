---
title: Monitor Node.js services with Azure Application Insights | Microsoft Docs
description: Monitor performance and diagnose problems in Node.js services with Application Insights.
services: application-insights
documentationcenter: nodejs
author: mrbullwinkle
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/01/2017
ms.author: mbullwin
ms.openlocfilehash: 28be3a1734639ac175e4d18d9e9f21b83b9a7e7c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821280"
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="aedc0-103">Monitor your Node.js services and apps with Application Insights</span><span class="sxs-lookup"><span data-stu-id="aedc0-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="aedc0-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after deployment, to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="aedc0-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after deployment, to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="aedc0-105">You can use Application Insights for Node.js services that are hosted in your datacenter, in Azure VMs and web apps, and even in other public clouds.</span><span class="sxs-lookup"><span data-stu-id="aedc0-105">You can use Application Insights for Node.js services that are hosted in your datacenter, in Azure VMs and web apps, and even in other public clouds.</span></span>

<span data-ttu-id="aedc0-106">To receive, store, and explore your monitoring data, include the SDK in your code, and then set up a corresponding Application Insights resource in Azure.</span><span class="sxs-lookup"><span data-stu-id="aedc0-106">To receive, store, and explore your monitoring data, include the SDK in your code, and then set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="aedc0-107">The SDK sends data to that resource for further analysis and exploration.</span><span class="sxs-lookup"><span data-stu-id="aedc0-107">The SDK sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="aedc0-108">The Node.js SDK can automatically monitor incoming and outgoing HTTP requests, exceptions, and some system metrics.</span><span class="sxs-lookup"><span data-stu-id="aedc0-108">The Node.js SDK can automatically monitor incoming and outgoing HTTP requests, exceptions, and some system metrics.</span></span> <span data-ttu-id="aedc0-109">Beginning in version 0.20, the SDK also can monitor some common third-party packages, like MongoDB, MySQL, and Redis.</span><span class="sxs-lookup"><span data-stu-id="aedc0-109">Beginning in version 0.20, the SDK also can monitor some common third-party packages, like MongoDB, MySQL, and Redis.</span></span> <span data-ttu-id="aedc0-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="aedc0-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="aedc0-111">You can use the TelemetryClient API to manually instrument and monitor additional aspects of your app and system.</span><span class="sxs-lookup"><span data-stu-id="aedc0-111">You can use the TelemetryClient API to manually instrument and monitor additional aspects of your app and system.</span></span> <span data-ttu-id="aedc0-112">We describe the TelemetryClient API in more detail later in this article.</span><span class="sxs-lookup"><span data-stu-id="aedc0-112">We describe the TelemetryClient API in more detail later in this article.</span></span>

![Example performance monitoring charts](./media/app-insights-nodejs/10-perf.png)

## <a name="get-started"></a><span data-ttu-id="aedc0-114">Get started</span><span class="sxs-lookup"><span data-stu-id="aedc0-114">Get started</span></span>

<span data-ttu-id="aedc0-115">Complete the following tasks to set up monitoring for an app or service.</span><span class="sxs-lookup"><span data-stu-id="aedc0-115">Complete the following tasks to set up monitoring for an app or service.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aedc0-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aedc0-116">Prerequisites</span></span>

<span data-ttu-id="aedc0-117">Before you begin, make sure that you have an Azure subscription, or [get a new one for free][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="aedc0-117">Before you begin, make sure that you have an Azure subscription, or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="aedc0-118">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span><span class="sxs-lookup"><span data-stu-id="aedc0-118">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/free/
[add-aad-user]: https://docs.microsoft.com/azure/active-directory/active-directory-users-create-azure-portal


### <a name="resource"></a> <span data-ttu-id="aedc0-119">Set up an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="aedc0-119">Set up an Application Insights resource</span></span>


1. <span data-ttu-id="aedc0-120">Sign in to the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="aedc0-120">Sign in to the [Azure portal][portal].</span></span>
2. <span data-ttu-id="aedc0-121">Select **Create a resource** > **Developer tools** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="aedc0-121">Select **Create a resource** > **Developer tools** > **Application Insights**.</span></span> <span data-ttu-id="aedc0-122">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span><span class="sxs-lookup"><span data-stu-id="aedc0-122">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

  ![Create an Application Insights resource](./media/app-insights-nodejs/03-new_appinsights_resource.png)

3. <span data-ttu-id="aedc0-124">On the resource creation page, in the **Application Type** box, select **Node.js Application**.</span><span class="sxs-lookup"><span data-stu-id="aedc0-124">On the resource creation page, in the **Application Type** box, select **Node.js Application**.</span></span> <span data-ttu-id="aedc0-125">The app type determines the default dashboards and reports that are created.</span><span class="sxs-lookup"><span data-stu-id="aedc0-125">The app type determines the default dashboards and reports that are created.</span></span> <span data-ttu-id="aedc0-126">(Any Application Insights resource can collect data from any language and platform.)</span><span class="sxs-lookup"><span data-stu-id="aedc0-126">(Any Application Insights resource can collect data from any language and platform.)</span></span>

  ![New Application Insights resource form](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="sdk"></a> <span data-ttu-id="aedc0-128">Set up the Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="aedc0-128">Set up the Node.js SDK</span></span>

<span data-ttu-id="aedc0-129">Include the SDK in your app, so it can gather data.</span><span class="sxs-lookup"><span data-stu-id="aedc0-129">Include the SDK in your app, so it can gather data.</span></span> 

1. <span data-ttu-id="aedc0-130">Copy your resource's Instrumentation Key (also called an *ikey*) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aedc0-130">Copy your resource's Instrumentation Key (also called an *ikey*) from the Azure portal.</span></span> <span data-ttu-id="aedc0-131">Application Insights uses the ikey to map data to your Azure resource.</span><span class="sxs-lookup"><span data-stu-id="aedc0-131">Application Insights uses the ikey to map data to your Azure resource.</span></span> <span data-ttu-id="aedc0-132">Before the SDK can use your ikey, you must specify the ikey in an environment variable or in your code.</span><span class="sxs-lookup"><span data-stu-id="aedc0-132">Before the SDK can use your ikey, you must specify the ikey in an environment variable or in your code.</span></span>  

  ![Copy instrumentation key](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

2. <span data-ttu-id="aedc0-134">Add the Node.js SDK library to your app's dependencies via package.json.</span><span class="sxs-lookup"><span data-stu-id="aedc0-134">Add the Node.js SDK library to your app's dependencies via package.json.</span></span> <span data-ttu-id="aedc0-135">From the root folder of your app, run:</span><span class="sxs-lookup"><span data-stu-id="aedc0-135">From the root folder of your app, run:</span></span>

  ```bash
  npm install applicationinsights --save
  ```

3. <span data-ttu-id="aedc0-136">Explicitly load the library in your code.</span><span class="sxs-lookup"><span data-stu-id="aedc0-136">Explicitly load the library in your code.</span></span> <span data-ttu-id="aedc0-137">Because the SDK injects instrumentation into many other libraries, load the library as early as possible, even before other `require` statements.</span><span class="sxs-lookup"><span data-stu-id="aedc0-137">Because the SDK injects instrumentation into many other libraries, load the library as early as possible, even before other `require` statements.</span></span> 

  <span data-ttu-id="aedc0-138">At the top of your first .js file, add the following code.</span><span class="sxs-lookup"><span data-stu-id="aedc0-138">At the top of your first .js file, add the following code.</span></span> <span data-ttu-id="aedc0-139">The `setup` method configures the ikey (and thus, the Azure resource) to be used by default for all tracked items.</span><span class="sxs-lookup"><span data-stu-id="aedc0-139">The `setup` method configures the ikey (and thus, the Azure resource) to be used by default for all tracked items.</span></span>

  ```javascript
  const appInsights = require("applicationinsights");
  appInsights.setup("<instrumentation_key>");
  appInsights.start();
  ```
   
  <span data-ttu-id="aedc0-140">You also can provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY, instead of passing it manually to  `setup()` or `new appInsights.TelemetryClient()`.</span><span class="sxs-lookup"><span data-stu-id="aedc0-140">You also can provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY, instead of passing it manually to  `setup()` or `new appInsights.TelemetryClient()`.</span></span> <span data-ttu-id="aedc0-141">This practice lets you keep ikeys out of committed source code, and you can specify different ikeys for different environments.</span><span class="sxs-lookup"><span data-stu-id="aedc0-141">This practice lets you keep ikeys out of committed source code, and you can specify different ikeys for different environments.</span></span>

  <span data-ttu-id="aedc0-142">For additional configuration options, see the following sections.</span><span class="sxs-lookup"><span data-stu-id="aedc0-142">For additional configuration options, see the following sections.</span></span>

  <span data-ttu-id="aedc0-143">You can try the SDK without sending telemetry by setting `appInsights.defaultClient.config.disableAppInsights = true`.</span><span class="sxs-lookup"><span data-stu-id="aedc0-143">You can try the SDK without sending telemetry by setting `appInsights.defaultClient.config.disableAppInsights = true`.</span></span>

### <a name="monitor"></a> <span data-ttu-id="aedc0-144">Monitor your app</span><span class="sxs-lookup"><span data-stu-id="aedc0-144">Monitor your app</span></span>

<span data-ttu-id="aedc0-145">The SDK automatically gathers telemetry about the Node.js runtime and about some common third-party modules.</span><span class="sxs-lookup"><span data-stu-id="aedc0-145">The SDK automatically gathers telemetry about the Node.js runtime and about some common third-party modules.</span></span> <span data-ttu-id="aedc0-146">Use your application to generate some of this data.</span><span class="sxs-lookup"><span data-stu-id="aedc0-146">Use your application to generate some of this data.</span></span>

<span data-ttu-id="aedc0-147">Then, in the [Azure portal][portal] go to the Application Insights resource that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="aedc0-147">Then, in the [Azure portal][portal] go to the Application Insights resource that you created earlier.</span></span> <span data-ttu-id="aedc0-148">In the **Overview timeline**, look for your first few data points.</span><span class="sxs-lookup"><span data-stu-id="aedc0-148">In the **Overview timeline**, look for your first few data points.</span></span> <span data-ttu-id="aedc0-149">To see more detailed data, select different components in the charts.</span><span class="sxs-lookup"><span data-stu-id="aedc0-149">To see more detailed data, select different components in the charts.</span></span>

![First data points](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="aedc0-151">To view the topology that is discovered for your app, select the **Application map** button.</span><span class="sxs-lookup"><span data-stu-id="aedc0-151">To view the topology that is discovered for your app, select the **Application map** button.</span></span> <span data-ttu-id="aedc0-152">Select components in the map to see more details.</span><span class="sxs-lookup"><span data-stu-id="aedc0-152">Select components in the map to see more details.</span></span>

![Simple app map](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="aedc0-154">To learn more about your app, and to troubleshoot problems, in the **INVESTIGATE** section, select the other views that are available.</span><span class="sxs-lookup"><span data-stu-id="aedc0-154">To learn more about your app, and to troubleshoot problems, in the **INVESTIGATE** section, select the other views that are available.</span></span>

![Investigate section](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="aedc0-156">No data?</span><span class="sxs-lookup"><span data-stu-id="aedc0-156">No data?</span></span>

<span data-ttu-id="aedc0-157">Because the SDK batches data for submission, there might be a delay before items are displayed in the portal.</span><span class="sxs-lookup"><span data-stu-id="aedc0-157">Because the SDK batches data for submission, there might be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="aedc0-158">If you don't see data in your resource, try some of the following fixes:</span><span class="sxs-lookup"><span data-stu-id="aedc0-158">If you don't see data in your resource, try some of the following fixes:</span></span>

* <span data-ttu-id="aedc0-159">Continue to use the application.</span><span class="sxs-lookup"><span data-stu-id="aedc0-159">Continue to use the application.</span></span> <span data-ttu-id="aedc0-160">Take more actions to generate more telemetry.</span><span class="sxs-lookup"><span data-stu-id="aedc0-160">Take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="aedc0-161">Click **Refresh** in the portal resource view.</span><span class="sxs-lookup"><span data-stu-id="aedc0-161">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="aedc0-162">Charts periodically refresh on their own, but manually refreshing forces them to refresh immediately.</span><span class="sxs-lookup"><span data-stu-id="aedc0-162">Charts periodically refresh on their own, but manually refreshing forces them to refresh immediately.</span></span>
* <span data-ttu-id="aedc0-163">Verify that [required outgoing ports](app-insights-ip-addresses.md) are open.</span><span class="sxs-lookup"><span data-stu-id="aedc0-163">Verify that [required outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="aedc0-164">Use [Search](app-insights-diagnostic-search.md) to look for specific events.</span><span class="sxs-lookup"><span data-stu-id="aedc0-164">Use [Search](app-insights-diagnostic-search.md) to look for specific events.</span></span>
* <span data-ttu-id="aedc0-165">Check the [FAQ][FAQ].</span><span class="sxs-lookup"><span data-stu-id="aedc0-165">Check the [FAQ][FAQ].</span></span>


## <a name="sdk-configuration"></a><span data-ttu-id="aedc0-166">SDK configuration</span><span class="sxs-lookup"><span data-stu-id="aedc0-166">SDK configuration</span></span>

<span data-ttu-id="aedc0-167">The SDK's configuration methods and default values are listed in the following code example.</span><span class="sxs-lookup"><span data-stu-id="aedc0-167">The SDK's configuration methods and default values are listed in the following code example.</span></span>

<span data-ttu-id="aedc0-168">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="aedc0-168">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="aedc0-169">With this option set, the SDK can track context across asynchronous callbacks in Node.js.</span><span class="sxs-lookup"><span data-stu-id="aedc0-169">With this option set, the SDK can track context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(true)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .setAutoCollectConsole(true)
    .setUseDiskRetryCaching(true)
    .start();
```

## <a name="telemetryclient-api"></a><span data-ttu-id="aedc0-170">TelemetryClient API</span><span class="sxs-lookup"><span data-stu-id="aedc0-170">TelemetryClient API</span></span>

<span data-ttu-id="aedc0-171">For a full description of the TelemetryClient API, see [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="aedc0-171">For a full description of the TelemetryClient API, see [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="aedc0-172">You can track any request, event, metric, or exception by using the Application Insights Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="aedc0-172">You can track any request, event, metric, or exception by using the Application Insights Node.js SDK.</span></span> <span data-ttu-id="aedc0-173">The following code example demonstrates some of the APIs that you can use:</span><span class="sxs-lookup"><span data-stu-id="aedc0-173">The following code example demonstrates some of the APIs that you can use:</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey is in env var
let client = appInsights.defaultClient;

client.trackEvent({name: "my custom event", properties: {customProperty: "custom property value"}});
client.trackException({exception: new Error("handled exceptions can be logged with this method")});
client.trackMetric({name: "custom metric", value: 3});
client.trackTrace({message: "trace message"});
client.trackDependency({target:"http://dbname", name:"select customers proc", data:"SELECT * FROM Customers", duration:231, resultCode:0, success: true, dependencyTypeName: "ZSQL"});
client.trackRequest({name:"GET /customers", url:"http://myserver/customers", duration:309, resultCode:200, success:true});

let http = require("http");
http.createServer( (req, res) => {
  client.trackNodeHttpRequest({request: req, response: res}); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="aedc0-174">Track your dependencies</span><span class="sxs-lookup"><span data-stu-id="aedc0-174">Track your dependencies</span></span>

<span data-ttu-id="aedc0-175">Use the following code to track your dependencies:</span><span class="sxs-lookup"><span data-stu-id="aedc0-175">Use the following code to track your dependencies:</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.defaultClient;

var success = false;
let startTime = Date.now();
// Execute dependency call here...
let duration = Date.now() - startTime;
success = true;

client.trackDependency({dependencyTypeName: "dependency name", name: "command name", duration: duration, success: success});
```

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="aedc0-176">Add a custom property to all events</span><span class="sxs-lookup"><span data-stu-id="aedc0-176">Add a custom property to all events</span></span>

<span data-ttu-id="aedc0-177">Use the following code to add a custom property to all events:</span><span class="sxs-lookup"><span data-stu-id="aedc0-177">Use the following code to add a custom property to all events:</span></span>

```javascript
appInsights.defaultClient.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="aedc0-178">Track HTTP GET requests</span><span class="sxs-lookup"><span data-stu-id="aedc0-178">Track HTTP GET requests</span></span>

<span data-ttu-id="aedc0-179">Use the following code to track HTTP GET requests:</span><span class="sxs-lookup"><span data-stu-id="aedc0-179">Use the following code to track HTTP GET requests:</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.defaultClient.trackNodeHttpRequest({request: req, response: res});
    }
    // Other work here...
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="aedc0-180">Track server startup time</span><span class="sxs-lookup"><span data-stu-id="aedc0-180">Track server startup time</span></span>

<span data-ttu-id="aedc0-181">Use the following code to track server startup time:</span><span class="sxs-lookup"><span data-stu-id="aedc0-181">Use the following code to track server startup time:</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.defaultClient.trackMetric({name: "server startup time", value: duration});
});
```

## <a name="next-steps"></a><span data-ttu-id="aedc0-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="aedc0-182">Next steps</span></span>

* [<span data-ttu-id="aedc0-183">Monitor your telemetry in the portal</span><span class="sxs-lookup"><span data-stu-id="aedc0-183">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="aedc0-184">Write Analytics queries over your telemetry</span><span class="sxs-lookup"><span data-stu-id="aedc0-184">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md

