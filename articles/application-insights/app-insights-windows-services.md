---
title: Azure Application Insights for Windows server and worker roles | Microsoft Docs
description: Manually add the Application Insights SDK to your ASP.NET application to analyze usage, availability and performance.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: douge
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/01/2016
ms.author: awills
ms.openlocfilehash: 64f5793e31b8d7a4bcf3d48cec7df14d5e67af03
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552820"
---
# <a name="manually-configure-application-insights-for-aspnet-applications"></a><span data-ttu-id="9a5e8-103">Manually configure Application Insights for ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="9a5e8-103">Manually configure Application Insights for ASP.NET applications</span></span>
<span data-ttu-id="9a5e8-104">[Application Insights](app-insights-overview.md) is an extensible tool for web developers to monitor the performance and usage of your live application.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-104">[Application Insights](app-insights-overview.md) is an extensible tool for web developers to monitor the performance and usage of your live application.</span></span> <span data-ttu-id="9a5e8-105">You can manually configure it to monitor Windows server, worker roles, and other ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-105">You can manually configure it to monitor Windows server, worker roles, and other ASP.NET applications.</span></span> <span data-ttu-id="9a5e8-106">For web apps, manual configuration is an alternative to the [automatic set-up](app-insights-asp-net.md) offered by Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-106">For web apps, manual configuration is an alternative to the [automatic set-up](app-insights-asp-net.md) offered by Visual Studio.</span></span>

![Example performance monitoring charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="9a5e8-108">Before you start</span><span class="sxs-lookup"><span data-stu-id="9a5e8-108">Before you start</span></span>
<span data-ttu-id="9a5e8-109">You need:</span><span class="sxs-lookup"><span data-stu-id="9a5e8-109">You need:</span></span>

* <span data-ttu-id="9a5e8-110">A subscription to [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="9a5e8-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="9a5e8-112">Visual Studio 2013 or later.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-112">Visual Studio 2013 or later.</span></span>

## <a name="add"></a><span data-ttu-id="9a5e8-113">1. Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="9a5e8-113">1. Create an Application Insights resource</span></span>
<span data-ttu-id="9a5e8-114">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-114">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="9a5e8-115">Choose ASP.NET as the application type.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-115">Choose ASP.NET as the application type.</span></span>

![Click New, Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="9a5e8-117">A [resource](app-insights-resources-roles-access-control.md) in Azure is an instance of a service.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-117">A [resource](app-insights-resources-roles-access-control.md) in Azure is an instance of a service.</span></span> <span data-ttu-id="9a5e8-118">This resource is where telemetry from your app will be analyzed and presented to you.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-118">This resource is where telemetry from your app will be analyzed and presented to you.</span></span>

<span data-ttu-id="9a5e8-119">The choice of application type sets the default content of the resource blades and the properties visible in [Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-119">The choice of application type sets the default content of the resource blades and the properties visible in [Metrics Explorer](app-insights-metrics-explorer.md).</span></span>

#### <a name="copy-the-instrumentation-key"></a><span data-ttu-id="9a5e8-120">Copy the Instrumentation Key</span><span class="sxs-lookup"><span data-stu-id="9a5e8-120">Copy the Instrumentation Key</span></span>
<span data-ttu-id="9a5e8-121">The key identifies the resource, and you'll install it soon in the SDK to direct data to the resource.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-121">The key identifies the resource, and you'll install it soon in the SDK to direct data to the resource.</span></span>

![Click Properties, select the key, and press ctrl+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/02-props-asp.png)

<span data-ttu-id="9a5e8-123">The steps you've just done to create a new resource are a good way to start monitoring any application.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-123">The steps you've just done to create a new resource are a good way to start monitoring any application.</span></span> <span data-ttu-id="9a5e8-124">Now you can send data to it.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-124">Now you can send data to it.</span></span>

## <a name="sdk"></a><span data-ttu-id="9a5e8-125">2. Install the Application Insights package in your application</span><span class="sxs-lookup"><span data-stu-id="9a5e8-125">2. Install the Application Insights package in your application</span></span>
<span data-ttu-id="9a5e8-126">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-126">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> <span data-ttu-id="9a5e8-127">For ASP.NET apps, it's easy.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-127">For ASP.NET apps, it's easy.</span></span>

1. <span data-ttu-id="9a5e8-128">In Visual Studio, edit the NuGet packages of your web app project.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-128">In Visual Studio, edit the NuGet packages of your web app project.</span></span>
   
    ![Right-click the project and select Manage Nuget Packages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="9a5e8-130">Install Application Insights package for Windows server apps.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-130">Install Application Insights package for Windows server apps.</span></span>
   
    ![Search for "Application Insights"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="9a5e8-132">*Can I use other packages?*</span><span class="sxs-lookup"><span data-stu-id="9a5e8-132">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="9a5e8-133">Yes.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-133">Yes.</span></span> <span data-ttu-id="9a5e8-134">Choose the Core API (Microsoft.ApplicationInsights) if you only want to use the API to send your own telemetry.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-134">Choose the Core API (Microsoft.ApplicationInsights) if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="9a5e8-135">The Windows Server package automatically includes the Core API plus a number of other packages such as performance counter collection and dependency monitoring.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-135">The Windows Server package automatically includes the Core API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

#### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="9a5e8-136">To upgrade to future package versions</span><span class="sxs-lookup"><span data-stu-id="9a5e8-136">To upgrade to future package versions</span></span>
<span data-ttu-id="9a5e8-137">We release a new version of the SDK from time to time.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-137">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="9a5e8-138">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-138">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="9a5e8-139">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-139">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="9a5e8-140">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-140">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="3-send-telemetry"></a><span data-ttu-id="9a5e8-141">3. Send telemetry</span><span class="sxs-lookup"><span data-stu-id="9a5e8-141">3. Send telemetry</span></span>
<span data-ttu-id="9a5e8-142">**If you installed only the core API package:**</span><span class="sxs-lookup"><span data-stu-id="9a5e8-142">**If you installed only the core API package:**</span></span>

* <span data-ttu-id="9a5e8-143">Set the instrumentation key in code, for example in `main()`:</span><span class="sxs-lookup"><span data-stu-id="9a5e8-143">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="9a5e8-144">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span><span class="sxs-lookup"><span data-stu-id="9a5e8-144">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="9a5e8-145">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-145">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="9a5e8-146">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span><span class="sxs-lookup"><span data-stu-id="9a5e8-146">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="9a5e8-147">Edit ApplicationInsights.config (which was added by the NuGet install).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-147">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="9a5e8-148">Insert this just before the closing tag:</span><span class="sxs-lookup"><span data-stu-id="9a5e8-148">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="9a5e8-149">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="9a5e8-149">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="9a5e8-150">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-150">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="9a5e8-151">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-151">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="9a5e8-152">If you set the key in code, you don't have to set it in the `.config` file.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-152">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <a name="run"></a> <span data-ttu-id="9a5e8-153">Run your project</span><span class="sxs-lookup"><span data-stu-id="9a5e8-153">Run your project</span></span>
<span data-ttu-id="9a5e8-154">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-154">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="9a5e8-155">In Visual Studio, you'll see a count of the events that have been sent.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-155">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Event count in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> <span data-ttu-id="9a5e8-157">View your telemetry</span><span class="sxs-lookup"><span data-stu-id="9a5e8-157">View your telemetry</span></span>
<span data-ttu-id="9a5e8-158">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-158">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="9a5e8-159">Look for data in the Overview charts.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-159">Look for data in the Overview charts.</span></span> <span data-ttu-id="9a5e8-160">At first, you'll just see one or two points.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-160">At first, you'll just see one or two points.</span></span> <span data-ttu-id="9a5e8-161">For example:</span><span class="sxs-lookup"><span data-stu-id="9a5e8-161">For example:</span></span>

![Click through to more data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="9a5e8-163">Click through any chart to see more detailed metrics.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-163">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="9a5e8-164">Learn more about metrics.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-164">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

#### <a name="no-data"></a><span data-ttu-id="9a5e8-165">No data?</span><span class="sxs-lookup"><span data-stu-id="9a5e8-165">No data?</span></span>
* <span data-ttu-id="9a5e8-166">Use the application, opening different pages so that it generates some telemetry.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-166">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="9a5e8-167">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-167">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="9a5e8-168">Sometimes it takes events a little while longer to get through the metrics pipeline.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-168">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="9a5e8-169">Wait a few seconds and click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-169">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="9a5e8-170">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-170">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="9a5e8-171">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-171">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="9a5e8-172">Publish your app</span><span class="sxs-lookup"><span data-stu-id="9a5e8-172">Publish your app</span></span>
<span data-ttu-id="9a5e8-173">Now deploy your application to your server or to Azure and watch the data accumulate.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-173">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Use Visual Studio to publish your app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="9a5e8-175">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-175">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="9a5e8-176">When you deploy your app in Release configuration, data accumulates more slowly.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-176">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

#### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="9a5e8-177">No data after you publish to your server?</span><span class="sxs-lookup"><span data-stu-id="9a5e8-177">No data after you publish to your server?</span></span>
<span data-ttu-id="9a5e8-178">Open ports for outgoing traffic in your server's firewall.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-178">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="9a5e8-179">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span><span class="sxs-lookup"><span data-stu-id="9a5e8-179">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

#### <a name="trouble-on-your-build-server"></a><span data-ttu-id="9a5e8-180">Trouble on your build server?</span><span class="sxs-lookup"><span data-stu-id="9a5e8-180">Trouble on your build server?</span></span>
<span data-ttu-id="9a5e8-181">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-181">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="9a5e8-182">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-182">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="9a5e8-183">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-183">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="9a5e8-184">[Learn about sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9a5e8-184">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="9a5e8-185">Video</span><span class="sxs-lookup"><span data-stu-id="9a5e8-185">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="9a5e8-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a5e8-186">Next steps</span></span>
* <span data-ttu-id="9a5e8-187">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span><span class="sxs-lookup"><span data-stu-id="9a5e8-187">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>









