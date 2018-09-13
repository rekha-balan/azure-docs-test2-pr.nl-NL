---
title: Monitor Docker applications in Azure Application Insights | Microsoft Docs
description: Docker perf counters, events and exceptions can be displayed on Application Insights, along with the telemetry from the containerized apps.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 7ac0becb2b22046799503bb5af7b40b17388ec56
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555212"
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="e18c2-103">Monitor Docker applications in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e18c2-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="e18c2-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e18c2-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="e18c2-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span><span class="sxs-lookup"><span data-stu-id="e18c2-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="e18c2-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span><span class="sxs-lookup"><span data-stu-id="e18c2-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="e18c2-107">They'll run on any host machine that runs a Docker Engine.</span><span class="sxs-lookup"><span data-stu-id="e18c2-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="e18c2-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span><span class="sxs-lookup"><span data-stu-id="e18c2-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="e18c2-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span><span class="sxs-lookup"><span data-stu-id="e18c2-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="e18c2-110">Performance counters for all the containers.</span><span class="sxs-lookup"><span data-stu-id="e18c2-110">Performance counters for all the containers.</span></span> <span data-ttu-id="e18c2-111">CPU, memory, network usage, and more.</span><span class="sxs-lookup"><span data-stu-id="e18c2-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="e18c2-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span><span class="sxs-lookup"><span data-stu-id="e18c2-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="e18c2-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span><span class="sxs-lookup"><span data-stu-id="e18c2-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="e18c2-115">Set up your Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="e18c2-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="e18c2-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e18c2-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="e18c2-117">*Which resource should I use?*</span><span class="sxs-lookup"><span data-stu-id="e18c2-117">*Which resource should I use?*</span></span> <span data-ttu-id="e18c2-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e18c2-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="e18c2-119">This is where you view and analyze the telemetry.</span><span class="sxs-lookup"><span data-stu-id="e18c2-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="e18c2-120">(Select 'General' for the app type.)</span><span class="sxs-lookup"><span data-stu-id="e18c2-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="e18c2-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span><span class="sxs-lookup"><span data-stu-id="e18c2-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="e18c2-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span><span class="sxs-lookup"><span data-stu-id="e18c2-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="e18c2-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span><span class="sxs-lookup"><span data-stu-id="e18c2-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="e18c2-124">In that case, you probably also want to create a separate resource for the Docker data.</span><span class="sxs-lookup"><span data-stu-id="e18c2-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="e18c2-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="e18c2-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/03.png)
3. <span data-ttu-id="e18c2-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span><span class="sxs-lookup"><span data-stu-id="e18c2-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="e18c2-128">You use this to tell the SDK where to send its telemetry.</span><span class="sxs-lookup"><span data-stu-id="e18c2-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/02-props.png)

<span data-ttu-id="e18c2-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span><span class="sxs-lookup"><span data-stu-id="e18c2-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="e18c2-131">Run the Application Insights monitor on your host</span><span class="sxs-lookup"><span data-stu-id="e18c2-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="e18c2-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span><span class="sxs-lookup"><span data-stu-id="e18c2-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="e18c2-133">Connect to your Docker host.</span><span class="sxs-lookup"><span data-stu-id="e18c2-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="e18c2-134">Edit your instrumentation key into this command, and then run it:</span><span class="sxs-lookup"><span data-stu-id="e18c2-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="e18c2-135">Only one Application Insights image is required per Docker host.</span><span class="sxs-lookup"><span data-stu-id="e18c2-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="e18c2-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span><span class="sxs-lookup"><span data-stu-id="e18c2-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="e18c2-137">Update your app</span><span class="sxs-lookup"><span data-stu-id="e18c2-137">Update your app</span></span>
<span data-ttu-id="e18c2-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span><span class="sxs-lookup"><span data-stu-id="e18c2-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="e18c2-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span><span class="sxs-lookup"><span data-stu-id="e18c2-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="e18c2-140">View your telemetry</span><span class="sxs-lookup"><span data-stu-id="e18c2-140">View your telemetry</span></span>
<span data-ttu-id="e18c2-141">Go back to your Application Insights resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e18c2-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="e18c2-142">Click through the Docker tile.</span><span class="sxs-lookup"><span data-stu-id="e18c2-142">Click through the Docker tile.</span></span>

<span data-ttu-id="e18c2-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span><span class="sxs-lookup"><span data-stu-id="e18c2-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="e18c2-144">Here are some of the views you can get.</span><span class="sxs-lookup"><span data-stu-id="e18c2-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="e18c2-145">Perf counters by host, activity by image</span><span class="sxs-lookup"><span data-stu-id="e18c2-145">Perf counters by host, activity by image</span></span>
![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/10.png)

![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/11.png)

<span data-ttu-id="e18c2-148">Click any host or image name for more detail.</span><span class="sxs-lookup"><span data-stu-id="e18c2-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="e18c2-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span><span class="sxs-lookup"><span data-stu-id="e18c2-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="e18c2-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e18c2-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="e18c2-151">Docker container events</span><span class="sxs-lookup"><span data-stu-id="e18c2-151">Docker container events</span></span>
![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/13.png)

<span data-ttu-id="e18c2-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e18c2-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="e18c2-154">Search and filter to find the events you want.</span><span class="sxs-lookup"><span data-stu-id="e18c2-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="e18c2-155">Click any event to get more detail.</span><span class="sxs-lookup"><span data-stu-id="e18c2-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="e18c2-156">Exceptions by container name</span><span class="sxs-lookup"><span data-stu-id="e18c2-156">Exceptions by container name</span></span>
![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="e18c2-158">Docker context added to app telemetry</span><span class="sxs-lookup"><span data-stu-id="e18c2-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="e18c2-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span><span class="sxs-lookup"><span data-stu-id="e18c2-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/16.png)

<span data-ttu-id="e18c2-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span><span class="sxs-lookup"><span data-stu-id="e18c2-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="e18c2-163">Q & A</span><span class="sxs-lookup"><span data-stu-id="e18c2-163">Q & A</span></span>
<span data-ttu-id="e18c2-164">*What does Application Insights give me that I can't get from Docker?*</span><span class="sxs-lookup"><span data-stu-id="e18c2-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="e18c2-165">Detailed breakdown of performance counters by container and image.</span><span class="sxs-lookup"><span data-stu-id="e18c2-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="e18c2-166">Integrate container and app data in one dashboard.</span><span class="sxs-lookup"><span data-stu-id="e18c2-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="e18c2-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span><span class="sxs-lookup"><span data-stu-id="e18c2-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="e18c2-168">*How do I get telemetry from the app itself?*</span><span class="sxs-lookup"><span data-stu-id="e18c2-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="e18c2-169">Install the Application Insights SDK in the app.</span><span class="sxs-lookup"><span data-stu-id="e18c2-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="e18c2-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e18c2-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="e18c2-171">Video</span><span class="sxs-lookup"><span data-stu-id="e18c2-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e18c2-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="e18c2-172">Next steps</span></span>

* [<span data-ttu-id="e18c2-173">Application Insights for Java</span><span class="sxs-lookup"><span data-stu-id="e18c2-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="e18c2-174">Application Insights for Node.js</span><span class="sxs-lookup"><span data-stu-id="e18c2-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="e18c2-175">Application Insights for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e18c2-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)









