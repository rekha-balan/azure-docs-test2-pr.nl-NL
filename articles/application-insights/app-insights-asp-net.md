---
title: Set up web app analytics for ASP.NET with Azure Application Insights | Microsoft Docs
description: Configure performance, availability, and user behavior analytics tools for your ASP.NET website, hosted on-premises or in Azure.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 01/19/2018
ms.author: mbullwin
ms.openlocfilehash: 73bb1e3d06066c422614bc9d6d3431b49be9c6de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797932"
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="2aa83-103">Set up Application Insights for your ASP.NET website</span><span class="sxs-lookup"><span data-stu-id="2aa83-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="2aa83-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="2aa83-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="2aa83-105">It works for ASP.NET apps that are hosted either in your own IIS server on-premises or in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="2aa83-105">It works for ASP.NET apps that are hosted either in your own IIS server on-premises or in the Cloud.</span></span> <span data-ttu-id="2aa83-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span><span class="sxs-lookup"><span data-stu-id="2aa83-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="2aa83-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span><span class="sxs-lookup"><span data-stu-id="2aa83-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="2aa83-108">Setup takes just a few clicks in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2aa83-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="2aa83-109">You have the option to avoid charges by limiting the volume of telemetry.</span><span class="sxs-lookup"><span data-stu-id="2aa83-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="2aa83-110">This allows you to experiment and debug, or to monitor a site with not many users.</span><span class="sxs-lookup"><span data-stu-id="2aa83-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="2aa83-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span><span class="sxs-lookup"><span data-stu-id="2aa83-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aa83-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2aa83-112">Prerequisites</span></span>
<span data-ttu-id="2aa83-113">To add Application Insights to your ASP.NET website, you need to:</span><span class="sxs-lookup"><span data-stu-id="2aa83-113">To add Application Insights to your ASP.NET website, you need to:</span></span>

- <span data-ttu-id="2aa83-114">Install [Visual Studio 2017 for Windows](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="2aa83-114">Install [Visual Studio 2017 for Windows](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="2aa83-115">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="2aa83-115">ASP.NET and web development</span></span>
    - <span data-ttu-id="2aa83-116">Azure development</span><span class="sxs-lookup"><span data-stu-id="2aa83-116">Azure development</span></span>

<span data-ttu-id="2aa83-117">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="2aa83-117">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="ide"></a> <span data-ttu-id="2aa83-118">Step 1: Add the Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="2aa83-118">Step 1: Add the Application Insights SDK</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2aa83-119">The process to add Application Insights varies by ASP.NET template type.</span><span class="sxs-lookup"><span data-stu-id="2aa83-119">The process to add Application Insights varies by ASP.NET template type.</span></span> <span data-ttu-id="2aa83-120">If you are using the **Empty** or **Azure Mobile App** template select **Project** > **Add Application Insights Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-120">If you are using the **Empty** or **Azure Mobile App** template select **Project** > **Add Application Insights Telemetry**.</span></span> <span data-ttu-id="2aa83-121">For all other ASP.NET templates consult the instructions below.</span><span class="sxs-lookup"><span data-stu-id="2aa83-121">For all other ASP.NET templates consult the instructions below.</span></span> 

<span data-ttu-id="2aa83-122">Right-click your web app name in the Solution Explorer, and choose **Configure Application Insights**</span><span class="sxs-lookup"><span data-stu-id="2aa83-122">Right-click your web app name in the Solution Explorer, and choose **Configure Application Insights**</span></span>

![Screenshot of Solution Explorer, with Configure Application Insights highlighted](./media/app-insights-asp-net/0001-configure-application-insights.png)

<span data-ttu-id="2aa83-124">(Depending on your Application Insights SDK version you may be prompted to upgrade to the latest SDK release.</span><span class="sxs-lookup"><span data-stu-id="2aa83-124">(Depending on your Application Insights SDK version you may be prompted to upgrade to the latest SDK release.</span></span> <span data-ttu-id="2aa83-125">If prompted, select **Update SDK**.)</span><span class="sxs-lookup"><span data-stu-id="2aa83-125">If prompted, select **Update SDK**.)</span></span>

![Screenshot: A new version of the Microsoft Application Insights SDK is available.](./media/app-insights-asp-net/0002-update-sdk.png)

<span data-ttu-id="2aa83-128">Application Insights Configuration screen:</span><span class="sxs-lookup"><span data-stu-id="2aa83-128">Application Insights Configuration screen:</span></span>

<span data-ttu-id="2aa83-129">Select **Start Free**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-129">Select **Start Free**.</span></span>

![Screenshot of Register your app with Application Insights page](./media/app-insights-asp-net/0004-start-free.png)

<span data-ttu-id="2aa83-131">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-131">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="2aa83-132">Resource groups are used to control access to data.</span><span class="sxs-lookup"><span data-stu-id="2aa83-132">Resource groups are used to control access to data.</span></span> <span data-ttu-id="2aa83-133">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="2aa83-133">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

 <span data-ttu-id="2aa83-134">Select **Register**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-134">Select **Register**.</span></span> 

![Screenshot of Register your app with Application Insights page](./media/app-insights-asp-net/0005-register-ed.png)

 <span data-ttu-id="2aa83-136">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span><span class="sxs-lookup"><span data-stu-id="2aa83-136">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>
> [!NOTE]
> <span data-ttu-id="2aa83-137">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span><span class="sxs-lookup"><span data-stu-id="2aa83-137">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="2aa83-138">You are able to see telemetry in Visual Studio while you are debugging.</span><span class="sxs-lookup"><span data-stu-id="2aa83-138">You are able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="2aa83-139">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="2aa83-139">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>

## <a name="run"></a> <span data-ttu-id="2aa83-140">Step 2: Run your app</span><span class="sxs-lookup"><span data-stu-id="2aa83-140">Step 2: Run your app</span></span>
<span data-ttu-id="2aa83-141">Run your app with F5.</span><span class="sxs-lookup"><span data-stu-id="2aa83-141">Run your app with F5.</span></span> <span data-ttu-id="2aa83-142">Open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="2aa83-142">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="2aa83-143">In Visual Studio, you will see a count of the events that have been logged.</span><span class="sxs-lookup"><span data-stu-id="2aa83-143">In Visual Studio, you will see a count of the events that have been logged.</span></span>

![Screenshot of Visual Studio.](./media/app-insights-asp-net/0006-Events.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="2aa83-146">Step 3: See your telemetry</span><span class="sxs-lookup"><span data-stu-id="2aa83-146">Step 3: See your telemetry</span></span>
<span data-ttu-id="2aa83-147">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span><span class="sxs-lookup"><span data-stu-id="2aa83-147">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="2aa83-148">Search telemetry in Visual Studio to help you debug your app.</span><span class="sxs-lookup"><span data-stu-id="2aa83-148">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="2aa83-149">Monitor performance and usage in the web portal when your system is live.</span><span class="sxs-lookup"><span data-stu-id="2aa83-149">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="2aa83-150">See your telemetry in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2aa83-150">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="2aa83-151">In Visual Studio, to view Application Insights data.</span><span class="sxs-lookup"><span data-stu-id="2aa83-151">In Visual Studio, to view Application Insights data.</span></span>  <span data-ttu-id="2aa83-152">Select **Solution Explorer** > **Connected Services** > right-click **Application Insights**, and then click **Search Live Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-152">Select **Solution Explorer** > **Connected Services** > right-click **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="2aa83-153">In the Visual Studio Application Insights Search window, you will see the data from your application for telemetry generated in the server side of your app.</span><span class="sxs-lookup"><span data-stu-id="2aa83-153">In the Visual Studio Application Insights Search window, you will see the data from your application for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="2aa83-154">Experiment with the filters, and click any event to see more detail.</span><span class="sxs-lookup"><span data-stu-id="2aa83-154">Experiment with the filters, and click any event to see more detail.</span></span>

![Screenshot of the Data from debug session view in the Application Insights window.](./media/app-insights-asp-net/55.png)

> [!Tip]
> <span data-ttu-id="2aa83-156">If you don't see any data, make sure the time range is correct, and click the Search icon.</span><span class="sxs-lookup"><span data-stu-id="2aa83-156">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="2aa83-157">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="2aa83-157">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="2aa83-158">See telemetry in web portal</span><span class="sxs-lookup"><span data-stu-id="2aa83-158">See telemetry in web portal</span></span>

<span data-ttu-id="2aa83-159">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span><span class="sxs-lookup"><span data-stu-id="2aa83-159">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="2aa83-160">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2aa83-160">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="2aa83-161">The portal also provides alerts.</span><span class="sxs-lookup"><span data-stu-id="2aa83-161">The portal also provides alerts.</span></span>

<span data-ttu-id="2aa83-162">Open your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="2aa83-162">Open your Application Insights resource.</span></span> <span data-ttu-id="2aa83-163">Either sign into the [Azure portal](https://portal.azure.com/) and find it there, or select **Solution Explorer** > **Connected Services** > right-click **Application Insights** > **Open Application Insights Portal** and let it take you there.</span><span class="sxs-lookup"><span data-stu-id="2aa83-163">Either sign into the [Azure portal](https://portal.azure.com/) and find it there, or select **Solution Explorer** > **Connected Services** > right-click **Application Insights** > **Open Application Insights Portal** and let it take you there.</span></span>

<span data-ttu-id="2aa83-164">The portal opens on a view of the telemetry from your app.</span><span class="sxs-lookup"><span data-stu-id="2aa83-164">The portal opens on a view of the telemetry from your app.</span></span>

![Screenshot of Application Insights overview page](./media/app-insights-asp-net/66.png)

<span data-ttu-id="2aa83-166">In the portal, click any tile or chart to see more detail.</span><span class="sxs-lookup"><span data-stu-id="2aa83-166">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="2aa83-167">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="2aa83-167">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="2aa83-168">Step 4: Publish your app</span><span class="sxs-lookup"><span data-stu-id="2aa83-168">Step 4: Publish your app</span></span>
<span data-ttu-id="2aa83-169">Publish your app to your IIS server or to Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa83-169">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="2aa83-170">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span><span class="sxs-lookup"><span data-stu-id="2aa83-170">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="2aa83-171">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="2aa83-171">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="2aa83-172">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span><span class="sxs-lookup"><span data-stu-id="2aa83-172">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="2aa83-173">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="2aa83-173">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2aa83-174">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span><span class="sxs-lookup"><span data-stu-id="2aa83-174">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="2aa83-175">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span><span class="sxs-lookup"><span data-stu-id="2aa83-175">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <a name="land"></a> <span data-ttu-id="2aa83-176">You're all set</span><span class="sxs-lookup"><span data-stu-id="2aa83-176">You're all set</span></span>

<span data-ttu-id="2aa83-177">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="2aa83-177">Congratulations!</span></span> <span data-ttu-id="2aa83-178">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa83-178">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagram of movement of telemetry](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="2aa83-180">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span><span class="sxs-lookup"><span data-stu-id="2aa83-180">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="2aa83-181">You'll find this key in the ApplicationInsights.config file.</span><span class="sxs-lookup"><span data-stu-id="2aa83-181">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="2aa83-182">Upgrade to future SDK versions</span><span class="sxs-lookup"><span data-stu-id="2aa83-182">Upgrade to future SDK versions</span></span>
<span data-ttu-id="2aa83-183">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager**, and filter on installed packages.</span><span class="sxs-lookup"><span data-stu-id="2aa83-183">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager**, and filter on installed packages.</span></span> <span data-ttu-id="2aa83-184">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="2aa83-184">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="2aa83-185">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span><span class="sxs-lookup"><span data-stu-id="2aa83-185">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="2aa83-186">Then, merge your changes into the new version.</span><span class="sxs-lookup"><span data-stu-id="2aa83-186">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="2aa83-187">Video</span><span class="sxs-lookup"><span data-stu-id="2aa83-187">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="2aa83-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="2aa83-188">Next steps</span></span>

<span data-ttu-id="2aa83-189">There are alternative topics to look at if you are interested in:</span><span class="sxs-lookup"><span data-stu-id="2aa83-189">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="2aa83-190">Instrumenting a web app at runtime</span><span class="sxs-lookup"><span data-stu-id="2aa83-190">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="2aa83-191">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2aa83-191">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

### <a name="more-telemetry"></a><span data-ttu-id="2aa83-192">More telemetry</span><span class="sxs-lookup"><span data-stu-id="2aa83-192">More telemetry</span></span>

* <span data-ttu-id="2aa83-193">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span><span class="sxs-lookup"><span data-stu-id="2aa83-193">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="2aa83-194">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span><span class="sxs-lookup"><span data-stu-id="2aa83-194">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="2aa83-195">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span><span class="sxs-lookup"><span data-stu-id="2aa83-195">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="2aa83-196">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span><span class="sxs-lookup"><span data-stu-id="2aa83-196">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="2aa83-197">Analysis</span><span class="sxs-lookup"><span data-stu-id="2aa83-197">Analysis</span></span>

* <span data-ttu-id="2aa83-198">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="2aa83-198">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="2aa83-199">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span><span class="sxs-lookup"><span data-stu-id="2aa83-199">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="2aa83-200">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="2aa83-200">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="2aa83-201">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span><span class="sxs-lookup"><span data-stu-id="2aa83-201">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="2aa83-202">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span><span class="sxs-lookup"><span data-stu-id="2aa83-202">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="2aa83-203">Alerts</span><span class="sxs-lookup"><span data-stu-id="2aa83-203">Alerts</span></span>

* <span data-ttu-id="2aa83-204">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span><span class="sxs-lookup"><span data-stu-id="2aa83-204">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="2aa83-205">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span><span class="sxs-lookup"><span data-stu-id="2aa83-205">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="2aa83-206">They tell you if your app has an unusual rate of failed requests.</span><span class="sxs-lookup"><span data-stu-id="2aa83-206">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="2aa83-207">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span><span class="sxs-lookup"><span data-stu-id="2aa83-207">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="2aa83-208">You can set them on custom metrics that you code into your app.</span><span class="sxs-lookup"><span data-stu-id="2aa83-208">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="2aa83-209">Automation</span><span class="sxs-lookup"><span data-stu-id="2aa83-209">Automation</span></span>

* [<span data-ttu-id="2aa83-210">Automate creating an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="2aa83-210">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
