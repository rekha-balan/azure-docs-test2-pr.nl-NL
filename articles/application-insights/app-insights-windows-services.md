---
title: Azure Application Insights for Windows server and worker roles | Microsoft Docs
description: Manually add the Application Insights SDK to your ASP.NET application to analyze usage, availability and performance.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/15/2017
ms.author: mbullwin
ms.openlocfilehash: 461b1f4e72f0a47da4ccb560bfb4cfb7d0f3ccd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776067"
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="ee3f0-103">Manually configure Application Insights for .NET applications</span><span class="sxs-lookup"><span data-stu-id="ee3f0-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="ee3f0-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="ee3f0-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="ee3f0-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Example performance monitoring charts](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="ee3f0-108">Before you start</span><span class="sxs-lookup"><span data-stu-id="ee3f0-108">Before you start</span></span>

<span data-ttu-id="ee3f0-109">You need:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-109">You need:</span></span>

* <span data-ttu-id="ee3f0-110">A subscription to [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="ee3f0-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="ee3f0-112">Visual Studio 2013 or later.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-112">Visual Studio 2013 or later.</span></span>

## <a name="add"></a><span data-ttu-id="ee3f0-113">1. Choose an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="ee3f0-113">1. Choose an Application Insights resource</span></span>

<span data-ttu-id="ee3f0-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="ee3f0-115">You need to decide whether to create a new one, or share an existing one.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="ee3f0-116">Part of a larger app: Use existing resource</span><span class="sxs-lookup"><span data-stu-id="ee3f0-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="ee3f0-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="ee3f0-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="ee3f0-119">So, if you're already monitoring other components of this app, then just use the same resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="ee3f0-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="ee3f0-121">Self-contained app: Create a new resource</span><span class="sxs-lookup"><span data-stu-id="ee3f0-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="ee3f0-122">If the new app is unrelated to other applications, then it should have its own resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="ee3f0-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="ee3f0-124">Choose ASP.NET as the application type.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-124">Choose ASP.NET as the application type.</span></span>

![Click New, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="ee3f0-126">The choice of application type sets the default content of the resource blades.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="ee3f0-127">2. Copy the Instrumentation Key</span><span class="sxs-lookup"><span data-stu-id="ee3f0-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="ee3f0-128">The key identifies the resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-128">The key identifies the resource.</span></span> <span data-ttu-id="ee3f0-129">You'll install it soon in the SDK, in order to direct data to the resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![Click Properties, select the key, and press ctrl+C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a><span data-ttu-id="ee3f0-131">3. Install the Application Insights package in your application</span><span class="sxs-lookup"><span data-stu-id="ee3f0-131">3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="ee3f0-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="ee3f0-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Right-click the project and select Manage Nuget Packages](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="ee3f0-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span><span class="sxs-lookup"><span data-stu-id="ee3f0-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Search for "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="ee3f0-137">*Which version?*</span><span class="sxs-lookup"><span data-stu-id="ee3f0-137">*Which version?*</span></span>

    <span data-ttu-id="ee3f0-138">Check **Include prerelease** if you want to try our latest features.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="ee3f0-139">The relevant documents or blogs note whether you need a prerelease version.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="ee3f0-140">*Can I use other packages?*</span><span class="sxs-lookup"><span data-stu-id="ee3f0-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="ee3f0-141">Yes.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-141">Yes.</span></span> <span data-ttu-id="ee3f0-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="ee3f0-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="ee3f0-144">To upgrade to future package versions</span><span class="sxs-lookup"><span data-stu-id="ee3f0-144">To upgrade to future package versions</span></span>
<span data-ttu-id="ee3f0-145">We release a new version of the SDK from time to time.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="ee3f0-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="ee3f0-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="ee3f0-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="ee3f0-149">4. Send telemetry</span><span class="sxs-lookup"><span data-stu-id="ee3f0-149">4. Send telemetry</span></span>
<span data-ttu-id="ee3f0-150">**If you installed only the API package:**</span><span class="sxs-lookup"><span data-stu-id="ee3f0-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="ee3f0-151">Set the instrumentation key in code, for example in `main()`:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="ee3f0-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span><span class="sxs-lookup"><span data-stu-id="ee3f0-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="ee3f0-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="ee3f0-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="ee3f0-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="ee3f0-156">Insert this just before the closing tag:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="ee3f0-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ee3f0-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="ee3f0-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="ee3f0-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="ee3f0-160">If you set the key in code, you don't have to set it in the `.config` file.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <a name="run"></a> <span data-ttu-id="ee3f0-161">Run your project</span><span class="sxs-lookup"><span data-stu-id="ee3f0-161">Run your project</span></span>
<span data-ttu-id="ee3f0-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="ee3f0-163">In Visual Studio, you'll see a count of the events that have been sent.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Event count in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> <span data-ttu-id="ee3f0-165">View your telemetry</span><span class="sxs-lookup"><span data-stu-id="ee3f0-165">View your telemetry</span></span>
<span data-ttu-id="ee3f0-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="ee3f0-167">Look for data in the Overview charts.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="ee3f0-168">At first, you'll just see one or two points.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="ee3f0-169">For example:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-169">For example:</span></span>

![Click through to more data](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="ee3f0-171">Click through any chart to see more detailed metrics.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="ee3f0-172">Learn more about metrics.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="ee3f0-173">No data?</span><span class="sxs-lookup"><span data-stu-id="ee3f0-173">No data?</span></span>
* <span data-ttu-id="ee3f0-174">Use the application, opening different pages so that it generates some telemetry.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="ee3f0-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="ee3f0-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="ee3f0-177">Wait a few seconds and click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="ee3f0-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="ee3f0-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="ee3f0-180">Publish your app</span><span class="sxs-lookup"><span data-stu-id="ee3f0-180">Publish your app</span></span>
<span data-ttu-id="ee3f0-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Use Visual Studio to publish your app](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="ee3f0-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="ee3f0-184">When you deploy your app in Release configuration, data accumulates more slowly.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="ee3f0-185">No data after you publish to your server?</span><span class="sxs-lookup"><span data-stu-id="ee3f0-185">No data after you publish to your server?</span></span>
<span data-ttu-id="ee3f0-186">Open ports for outgoing traffic in your server's firewall.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="ee3f0-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span><span class="sxs-lookup"><span data-stu-id="ee3f0-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="ee3f0-188">Trouble on your build server?</span><span class="sxs-lookup"><span data-stu-id="ee3f0-188">Trouble on your build server?</span></span>
<span data-ttu-id="ee3f0-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="ee3f0-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="ee3f0-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="ee3f0-192">[Learn about sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="ee3f0-193">Video</span><span class="sxs-lookup"><span data-stu-id="ee3f0-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="ee3f0-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee3f0-194">Next steps</span></span>
* <span data-ttu-id="ee3f0-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

