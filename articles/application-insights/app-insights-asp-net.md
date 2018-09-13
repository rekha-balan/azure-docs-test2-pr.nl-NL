---
title: Set up web app analytics for ASP.NET with Azure Application Insights | Microsoft Docs
description: Configure performance, availability, and usage analytics for your ASP.NET website, hosted on-premises or in Azure.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/04/2017
ms.author: awills
ms.openlocfilehash: bc130c14be7c261c627987c2c6d7f74d02888a42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553058"
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="7c1d5-103">Set up Application Insights for your ASP.NET website</span><span class="sxs-lookup"><span data-stu-id="7c1d5-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="7c1d5-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="7c1d5-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="7c1d5-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="7c1d5-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="7c1d5-108">Setup takes just a few clicks in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="7c1d5-109">You have the option to avoid charges by limiting the volume of telemetry.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="7c1d5-110">This allows you to experiment and debug, or to monitor a site with not many users.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="7c1d5-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7c1d5-112">Before you start</span><span class="sxs-lookup"><span data-stu-id="7c1d5-112">Before you start</span></span>
<span data-ttu-id="7c1d5-113">You need:</span><span class="sxs-lookup"><span data-stu-id="7c1d5-113">You need:</span></span>

* <span data-ttu-id="7c1d5-114">Visual Studio 2013 update 3 or later.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="7c1d5-115">Later is better.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-115">Later is better.</span></span>
* <span data-ttu-id="7c1d5-116">A subscription to [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="7c1d5-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="7c1d5-118">There are alternative topics to look at if you are interested in:</span><span class="sxs-lookup"><span data-stu-id="7c1d5-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="7c1d5-119">Instrumenting a web app at runtime</span><span class="sxs-lookup"><span data-stu-id="7c1d5-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="7c1d5-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="7c1d5-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <a name="ide"></a> <span data-ttu-id="7c1d5-121">Step 1: Add the Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="7c1d5-121">Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="7c1d5-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Screenshot of Solution Explorer, with Add Application Insights Telemetry highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="7c1d5-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span><span class="sxs-lookup"><span data-stu-id="7c1d5-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="7c1d5-125">Continue to the Application Insights configuration page:</span><span class="sxs-lookup"><span data-stu-id="7c1d5-125">Continue to the Application Insights configuration page:</span></span>

![Screenshot of Register your app with Application Insights page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="7c1d5-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-127">**a.**</span></span> <span data-ttu-id="7c1d5-128">Select the account and subscription that you use to access Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="7c1d5-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-129">**b.**</span></span> <span data-ttu-id="7c1d5-130">Select the resource in Azure where you want to see the data from your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="7c1d5-131">Usually you create a separate resource for a each app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-131">Usually you create a separate resource for a each app.</span></span> <span data-ttu-id="7c1d5-132">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-132">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="7c1d5-133">Resource groups are used to control access to data.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-133">Resource groups are used to control access to data.</span></span> <span data-ttu-id="7c1d5-134">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-134">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="7c1d5-135">**c.**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-135">**c.**</span></span> <span data-ttu-id="7c1d5-136">Set a cap at the free data volume limit, to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-136">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="7c1d5-137">Application Insights is free up to a certain volume of telemetry.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-137">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="7c1d5-138">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-138">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="7c1d5-139">**d.**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-139">**d.**</span></span> <span data-ttu-id="7c1d5-140">Click **Register** to go ahead and configure Application Insights for your web app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-140">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="7c1d5-141">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-141">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="7c1d5-142">**e.**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-142">**e.**</span></span> <span data-ttu-id="7c1d5-143">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-143">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="7c1d5-144">You will be able to see telemetry in Visual Studio while you are debugging.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-144">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="7c1d5-145">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-145">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <a name="run"></a> <span data-ttu-id="7c1d5-146">Step 2: Run your app</span><span class="sxs-lookup"><span data-stu-id="7c1d5-146">Step 2: Run your app</span></span>
<span data-ttu-id="7c1d5-147">Run your app with F5.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-147">Run your app with F5.</span></span> <span data-ttu-id="7c1d5-148">Open different pages to generate some telemetry.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-148">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="7c1d5-149">In Visual Studio, you see a count of the events that have been logged.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-149">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Screenshot of Visual Studio.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="7c1d5-152">Step 3: See your telemetry</span><span class="sxs-lookup"><span data-stu-id="7c1d5-152">Step 3: See your telemetry</span></span>
<span data-ttu-id="7c1d5-153">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-153">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="7c1d5-154">Search telemetry in Visual Studio to help you debug your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-154">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="7c1d5-155">Monitor performance and usage in the web portal when your system is live.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-155">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="7c1d5-156">See your telemetry in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c1d5-156">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="7c1d5-157">In Visual Studio, open the Application Insights window.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-157">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="7c1d5-158">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-158">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="7c1d5-159">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-159">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="7c1d5-160">Experiment with the filters, and click any event to see more detail.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-160">Experiment with the filters, and click any event to see more detail.</span></span>

![Screenshot of the Data from debug session view in the Application Insights window.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="7c1d5-162">If you don't see any data, make sure the time range is correct, and click the Search icon.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-162">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="7c1d5-163">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-163">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="7c1d5-164">See telemetry in web portal</span><span class="sxs-lookup"><span data-stu-id="7c1d5-164">See telemetry in web portal</span></span>

<span data-ttu-id="7c1d5-165">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-165">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="7c1d5-166">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-166">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="7c1d5-167">The portal also provides alerts.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-167">The portal also provides alerts.</span></span>

<span data-ttu-id="7c1d5-168">Open your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-168">Open your Application Insights resource.</span></span> <span data-ttu-id="7c1d5-169">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-169">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Screenshot of Visual Studio, showing how to open the Application Insights portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="7c1d5-171">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span><span class="sxs-lookup"><span data-stu-id="7c1d5-171">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="7c1d5-172">In the portal, sign out and sign in again.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-172">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="7c1d5-173">The portal opens on a view of the telemetry from your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-173">The portal opens on a view of the telemetry from your app.</span></span>

![Screenshot of Application Insights overview page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/66.png)

<span data-ttu-id="7c1d5-175">In the portal, click any tile or chart to see more detail.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-175">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="7c1d5-176">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-176">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="7c1d5-177">Step 4: Publish your app</span><span class="sxs-lookup"><span data-stu-id="7c1d5-177">Step 4: Publish your app</span></span>
<span data-ttu-id="7c1d5-178">Publish your app to your IIS server or to Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-178">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="7c1d5-179">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-179">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="7c1d5-180">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-180">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="7c1d5-181">You can also use the powerful [Analytics query language](app-insights-analytics.md) to analyze usage and performance, or to find specific events.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-181">You can also use the powerful [Analytics query language](app-insights-analytics.md) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="7c1d5-182">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d5-182">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7c1d5-183">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-183">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="7c1d5-184">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-184">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <a name="land"></a> <span data-ttu-id="7c1d5-185">You're all set</span><span class="sxs-lookup"><span data-stu-id="7c1d5-185">You're all set</span></span>

<span data-ttu-id="7c1d5-186">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7c1d5-186">Congratulations!</span></span> <span data-ttu-id="7c1d5-187">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-187">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagram of movement of telemetry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="7c1d5-189">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-189">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="7c1d5-190">You'll find this key in the ApplicationInsights.config file.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-190">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="7c1d5-191">Upgrade to future SDK versions</span><span class="sxs-lookup"><span data-stu-id="7c1d5-191">Upgrade to future SDK versions</span></span>
<span data-ttu-id="7c1d5-192">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-192">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="7c1d5-193">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-193">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="7c1d5-194">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-194">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="7c1d5-195">Then, merge your changes into the new version.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-195">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="7c1d5-196">Video</span><span class="sxs-lookup"><span data-stu-id="7c1d5-196">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="7c1d5-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c1d5-197">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="7c1d5-198">More telemetry</span><span class="sxs-lookup"><span data-stu-id="7c1d5-198">More telemetry</span></span>

* <span data-ttu-id="7c1d5-199">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-199">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="7c1d5-200">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-200">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="7c1d5-201">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-201">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="7c1d5-202">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-202">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="7c1d5-203">Analysis</span><span class="sxs-lookup"><span data-stu-id="7c1d5-203">Analysis</span></span>

* <span data-ttu-id="7c1d5-204">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-204">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="7c1d5-205">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-205">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="7c1d5-206">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="7c1d5-206">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="7c1d5-207">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-207">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="7c1d5-208">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-208">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="7c1d5-209">Alerts</span><span class="sxs-lookup"><span data-stu-id="7c1d5-209">Alerts</span></span>

* <span data-ttu-id="7c1d5-210">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-210">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="7c1d5-211">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-211">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="7c1d5-212">They tell you if your app has an unusual rate of failed requests.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-212">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="7c1d5-213">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-213">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="7c1d5-214">You can set them on custom metrics that you code into your app.</span><span class="sxs-lookup"><span data-stu-id="7c1d5-214">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="7c1d5-215">Automation</span><span class="sxs-lookup"><span data-stu-id="7c1d5-215">Automation</span></span>

* [<span data-ttu-id="7c1d5-216">Automate creating an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="7c1d5-216">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)







