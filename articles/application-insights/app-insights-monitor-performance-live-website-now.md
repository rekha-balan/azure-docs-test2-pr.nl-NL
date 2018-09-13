---
title: Monitor a live ASP.NET web app with Azure Application Insights  | Microsoft Docs
description: Monitor a website's performance without re-deploying it. Works with ASP.NET web apps hosted on-premises, in VMs or on Azure.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/08/2017
ms.author: awills
ms.openlocfilehash: eaec3a1e43b8f2b89d4b5ca070729b988d4a40b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564179"
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="387dd-104">Instrument web apps at runtime with Application Insights</span><span class="sxs-lookup"><span data-stu-id="387dd-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="387dd-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span><span class="sxs-lookup"><span data-stu-id="387dd-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="387dd-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="387dd-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="387dd-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span><span class="sxs-lookup"><span data-stu-id="387dd-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="387dd-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span><span class="sxs-lookup"><span data-stu-id="387dd-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![sample charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="387dd-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span><span class="sxs-lookup"><span data-stu-id="387dd-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="387dd-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span><span class="sxs-lookup"><span data-stu-id="387dd-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="387dd-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span><span class="sxs-lookup"><span data-stu-id="387dd-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="387dd-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span><span class="sxs-lookup"><span data-stu-id="387dd-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="387dd-114">Get the best of both options.</span><span class="sxs-lookup"><span data-stu-id="387dd-114">Get the best of both options.</span></span>

<span data-ttu-id="387dd-115">Here's a summary of what you get by each route:</span><span class="sxs-lookup"><span data-stu-id="387dd-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="387dd-116">Build time</span><span class="sxs-lookup"><span data-stu-id="387dd-116">Build time</span></span> | <span data-ttu-id="387dd-117">Run time</span><span class="sxs-lookup"><span data-stu-id="387dd-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="387dd-118">Requests & exceptions</span><span class="sxs-lookup"><span data-stu-id="387dd-118">Requests & exceptions</span></span> |<span data-ttu-id="387dd-119">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-119">Yes</span></span> |<span data-ttu-id="387dd-120">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-120">Yes</span></span> |
| [<span data-ttu-id="387dd-121">More detailed exceptions</span><span class="sxs-lookup"><span data-stu-id="387dd-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="387dd-122">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-122">Yes</span></span> |
| [<span data-ttu-id="387dd-123">Dependency diagnostics</span><span class="sxs-lookup"><span data-stu-id="387dd-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="387dd-124">On .NET 4.6+, but less detail</span><span class="sxs-lookup"><span data-stu-id="387dd-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="387dd-125">Yes, full detail: result codes, SQL command text, HTTP verb</span><span class="sxs-lookup"><span data-stu-id="387dd-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="387dd-126">System performance counters</span><span class="sxs-lookup"><span data-stu-id="387dd-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="387dd-127">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-127">Yes</span></span> |<span data-ttu-id="387dd-128">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-128">Yes</span></span> |
| <span data-ttu-id="387dd-129">[API for custom telemetry][api]</span><span class="sxs-lookup"><span data-stu-id="387dd-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="387dd-130">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-130">Yes</span></span> | |
| [<span data-ttu-id="387dd-131">Trace log integration</span><span class="sxs-lookup"><span data-stu-id="387dd-131">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="387dd-132">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-132">Yes</span></span> | |
| [<span data-ttu-id="387dd-133">Page view & user data</span><span class="sxs-lookup"><span data-stu-id="387dd-133">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="387dd-134">Yes</span><span class="sxs-lookup"><span data-stu-id="387dd-134">Yes</span></span> | |
| <span data-ttu-id="387dd-135">No need to rebuild code</span><span class="sxs-lookup"><span data-stu-id="387dd-135">No need to rebuild code</span></span> |<span data-ttu-id="387dd-136">No</span><span class="sxs-lookup"><span data-stu-id="387dd-136">No</span></span> | |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="387dd-137">Monitor a live Azure web app</span><span class="sxs-lookup"><span data-stu-id="387dd-137">Monitor a live Azure web app</span></span>

<span data-ttu-id="387dd-138">If your application is running as an Azure web service, here's how to switch on monitoring:</span><span class="sxs-lookup"><span data-stu-id="387dd-138">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="387dd-139">Select Application Insights on the app's control panel in Azure.</span><span class="sxs-lookup"><span data-stu-id="387dd-139">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Set up Application Insights for an Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="387dd-141">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="387dd-141">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Click through to Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="387dd-143">[Monitoring Cloud and VM apps](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="387dd-143">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="387dd-144">Monitor a live IIS web app</span><span class="sxs-lookup"><span data-stu-id="387dd-144">Monitor a live IIS web app</span></span>

<span data-ttu-id="387dd-145">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="387dd-145">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="387dd-146">On your IIS web server, sign in with administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="387dd-146">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="387dd-147">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span><span class="sxs-lookup"><span data-stu-id="387dd-147">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="387dd-148">In Status Monitor, select the installed web application or website that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="387dd-148">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="387dd-149">Sign in with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="387dd-149">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="387dd-150">Configure the resource where you want to see the results in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="387dd-150">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="387dd-151">(Normally, it's best to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="387dd-151">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="387dd-152">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span><span class="sxs-lookup"><span data-stu-id="387dd-152">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Choose an app and a resource.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="387dd-154">Restart IIS.</span><span class="sxs-lookup"><span data-stu-id="387dd-154">Restart IIS.</span></span>

    ![Choose Restart at the top of the dialog.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="387dd-156">Your web service is interrupted for a short while.</span><span class="sxs-lookup"><span data-stu-id="387dd-156">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="387dd-157">Customize monitoring options</span><span class="sxs-lookup"><span data-stu-id="387dd-157">Customize monitoring options</span></span>

<span data-ttu-id="387dd-158">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span><span class="sxs-lookup"><span data-stu-id="387dd-158">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="387dd-159">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span><span class="sxs-lookup"><span data-stu-id="387dd-159">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="387dd-160">When you re-publish your app, re-enable Application Insights</span><span class="sxs-lookup"><span data-stu-id="387dd-160">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="387dd-161">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="387dd-161">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="387dd-162">You'll get more detailed telemetry and the ability to write custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="387dd-162">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="387dd-163">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span><span class="sxs-lookup"><span data-stu-id="387dd-163">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="387dd-164">Therefore:</span><span class="sxs-lookup"><span data-stu-id="387dd-164">Therefore:</span></span>

1. <span data-ttu-id="387dd-165">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span><span class="sxs-lookup"><span data-stu-id="387dd-165">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="387dd-166">Republish your app.</span><span class="sxs-lookup"><span data-stu-id="387dd-166">Republish your app.</span></span>
3. <span data-ttu-id="387dd-167">Re-enable Application Insights monitoring.</span><span class="sxs-lookup"><span data-stu-id="387dd-167">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="387dd-168">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span><span class="sxs-lookup"><span data-stu-id="387dd-168">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="387dd-169">Reinstate any edits you performed on the .config file.</span><span class="sxs-lookup"><span data-stu-id="387dd-169">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="387dd-170">Troubleshooting runtime configuration of Application Insights</span><span class="sxs-lookup"><span data-stu-id="387dd-170">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="387dd-171">Can't connect?</span><span class="sxs-lookup"><span data-stu-id="387dd-171">Can't connect?</span></span> <span data-ttu-id="387dd-172">No telemetry?</span><span class="sxs-lookup"><span data-stu-id="387dd-172">No telemetry?</span></span>

* <span data-ttu-id="387dd-173">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span><span class="sxs-lookup"><span data-stu-id="387dd-173">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="387dd-174">Open Status Monitor and select your application on left pane.</span><span class="sxs-lookup"><span data-stu-id="387dd-174">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="387dd-175">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span><span class="sxs-lookup"><span data-stu-id="387dd-175">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Open the Performance blade to see request, response time, dependency and other data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="387dd-177">On the server, if you see a message about "insufficient permissions", try the following:</span><span class="sxs-lookup"><span data-stu-id="387dd-177">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="387dd-178">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span><span class="sxs-lookup"><span data-stu-id="387dd-178">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="387dd-179">In Computer management control panel, add this identity to the Performance Monitor Users group.</span><span class="sxs-lookup"><span data-stu-id="387dd-179">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="387dd-180">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span><span class="sxs-lookup"><span data-stu-id="387dd-180">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="387dd-181">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span><span class="sxs-lookup"><span data-stu-id="387dd-181">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="387dd-182">See [Troubleshooting][qna].</span><span class="sxs-lookup"><span data-stu-id="387dd-182">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="387dd-183">System Requirements</span><span class="sxs-lookup"><span data-stu-id="387dd-183">System Requirements</span></span>
<span data-ttu-id="387dd-184">OS support for Application Insights Status Monitor on Server:</span><span class="sxs-lookup"><span data-stu-id="387dd-184">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="387dd-185">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="387dd-185">Windows Server 2008</span></span>
* <span data-ttu-id="387dd-186">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="387dd-186">Windows Server 2008 R2</span></span>
* <span data-ttu-id="387dd-187">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="387dd-187">Windows Server 2012</span></span>
* <span data-ttu-id="387dd-188">Windows server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="387dd-188">Windows server 2012 R2</span></span>
* <span data-ttu-id="387dd-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="387dd-189">Windows Server 2016</span></span>

<span data-ttu-id="387dd-190">with latest SP and .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="387dd-190">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="387dd-191">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="387dd-191">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="387dd-192">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span><span class="sxs-lookup"><span data-stu-id="387dd-192">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="387dd-193">Automation with PowerShell</span><span class="sxs-lookup"><span data-stu-id="387dd-193">Automation with PowerShell</span></span>
<span data-ttu-id="387dd-194">You can start and stop monitoring by using PowerShell on your IIS server.</span><span class="sxs-lookup"><span data-stu-id="387dd-194">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="387dd-195">First import the Application Insights module:</span><span class="sxs-lookup"><span data-stu-id="387dd-195">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="387dd-196">Find out which apps are being monitored:</span><span class="sxs-lookup"><span data-stu-id="387dd-196">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="387dd-197">`-Name` (Optional) The name of a web app.</span><span class="sxs-lookup"><span data-stu-id="387dd-197">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="387dd-198">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span><span class="sxs-lookup"><span data-stu-id="387dd-198">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="387dd-199">Returns `ApplicationInsightsApplication` for each app:</span><span class="sxs-lookup"><span data-stu-id="387dd-199">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="387dd-200">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="387dd-200">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="387dd-201">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span><span class="sxs-lookup"><span data-stu-id="387dd-201">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="387dd-202">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="387dd-202">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="387dd-203">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span><span class="sxs-lookup"><span data-stu-id="387dd-203">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="387dd-204">Its SDK cannot be updated or stopped.</span><span class="sxs-lookup"><span data-stu-id="387dd-204">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="387dd-205">`SdkVersion` shows the version in use for monitoring this app.</span><span class="sxs-lookup"><span data-stu-id="387dd-205">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="387dd-206">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span><span class="sxs-lookup"><span data-stu-id="387dd-206">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="387dd-207">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="387dd-207">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="387dd-208">`-Name` The name of the app in IIS</span><span class="sxs-lookup"><span data-stu-id="387dd-208">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="387dd-209">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span><span class="sxs-lookup"><span data-stu-id="387dd-209">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="387dd-210">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="387dd-210">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="387dd-211">The cmdlet does not affect an app that is already instrumented.</span><span class="sxs-lookup"><span data-stu-id="387dd-211">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="387dd-212">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="387dd-212">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="387dd-213">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span><span class="sxs-lookup"><span data-stu-id="387dd-213">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="387dd-214">To download the latest version, use Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="387dd-214">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="387dd-215">Returns `ApplicationInsightsApplication` on success.</span><span class="sxs-lookup"><span data-stu-id="387dd-215">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="387dd-216">If it fails, it logs a trace to stderr.</span><span class="sxs-lookup"><span data-stu-id="387dd-216">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="387dd-217">`-Name` The name of an app in IIS</span><span class="sxs-lookup"><span data-stu-id="387dd-217">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="387dd-218">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="387dd-218">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="387dd-219">Stops monitoring the specified apps and removes instrumentation.</span><span class="sxs-lookup"><span data-stu-id="387dd-219">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="387dd-220">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="387dd-220">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="387dd-221">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="387dd-221">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="387dd-222">Returns ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="387dd-222">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="387dd-223">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="387dd-223">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="387dd-224">`-Name`: The name of a web app in IIS.</span><span class="sxs-lookup"><span data-stu-id="387dd-224">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="387dd-225">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span><span class="sxs-lookup"><span data-stu-id="387dd-225">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="387dd-226">This cmdlet:</span><span class="sxs-lookup"><span data-stu-id="387dd-226">This cmdlet:</span></span>
  * <span data-ttu-id="387dd-227">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span><span class="sxs-lookup"><span data-stu-id="387dd-227">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="387dd-228">(Only works if `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="387dd-228">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="387dd-229">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span><span class="sxs-lookup"><span data-stu-id="387dd-229">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="387dd-230">(Works if `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="387dd-230">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="387dd-231">Downloads the latest Application Insights SDK to the server.</span><span class="sxs-lookup"><span data-stu-id="387dd-231">Downloads the latest Application Insights SDK to the server.</span></span>

## <a name="questions"></a><span data-ttu-id="387dd-232">Questions about Status Monitor</span><span class="sxs-lookup"><span data-stu-id="387dd-232">Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="387dd-233">What is Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="387dd-233">What is Status Monitor?</span></span>

<span data-ttu-id="387dd-234">A desktop application that you install in your IIS web server.</span><span class="sxs-lookup"><span data-stu-id="387dd-234">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="387dd-235">It helps you instrument and configure web apps.</span><span class="sxs-lookup"><span data-stu-id="387dd-235">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="387dd-236">When do I use Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="387dd-236">When do I use Status Monitor?</span></span>

* <span data-ttu-id="387dd-237">To instrument any web app that is running on your IIS server - even if it is already running.</span><span class="sxs-lookup"><span data-stu-id="387dd-237">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="387dd-238">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span><span class="sxs-lookup"><span data-stu-id="387dd-238">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="387dd-239">Can I close it after it runs?</span><span class="sxs-lookup"><span data-stu-id="387dd-239">Can I close it after it runs?</span></span>

<span data-ttu-id="387dd-240">Yes.</span><span class="sxs-lookup"><span data-stu-id="387dd-240">Yes.</span></span> <span data-ttu-id="387dd-241">After it has instrumented the websites you select, you can close it.</span><span class="sxs-lookup"><span data-stu-id="387dd-241">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="387dd-242">It doesn't collect telemetry by itself.</span><span class="sxs-lookup"><span data-stu-id="387dd-242">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="387dd-243">It just configures the web apps and sets some permissions.</span><span class="sxs-lookup"><span data-stu-id="387dd-243">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="387dd-244">What does Status Monitor do?</span><span class="sxs-lookup"><span data-stu-id="387dd-244">What does Status Monitor do?</span></span>

<span data-ttu-id="387dd-245">When you select a web app for Status Monitor to instrument:</span><span class="sxs-lookup"><span data-stu-id="387dd-245">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="387dd-246">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span><span class="sxs-lookup"><span data-stu-id="387dd-246">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="387dd-247">Modifies `web.config` to add the Application Insights HTTP tracking module.</span><span class="sxs-lookup"><span data-stu-id="387dd-247">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="387dd-248">Enables CLR profiling to collect dependency calls.</span><span class="sxs-lookup"><span data-stu-id="387dd-248">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="387dd-249">Do I need to run Status Monitor whenever I update the app?</span><span class="sxs-lookup"><span data-stu-id="387dd-249">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="387dd-250">Not if you redeploy incrementally.</span><span class="sxs-lookup"><span data-stu-id="387dd-250">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="387dd-251">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="387dd-251">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="387dd-252">What telemetry is collected?</span><span class="sxs-lookup"><span data-stu-id="387dd-252">What telemetry is collected?</span></span>

<span data-ttu-id="387dd-253">For applications that you instrument only at run-time by using Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="387dd-253">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="387dd-254">HTTP requests</span><span class="sxs-lookup"><span data-stu-id="387dd-254">HTTP requests</span></span>
* <span data-ttu-id="387dd-255">Calls to dependencies</span><span class="sxs-lookup"><span data-stu-id="387dd-255">Calls to dependencies</span></span>
* <span data-ttu-id="387dd-256">Exceptions</span><span class="sxs-lookup"><span data-stu-id="387dd-256">Exceptions</span></span>
* <span data-ttu-id="387dd-257">Performance counters</span><span class="sxs-lookup"><span data-stu-id="387dd-257">Performance counters</span></span>

<span data-ttu-id="387dd-258">For applications already instrumented at compile time:</span><span class="sxs-lookup"><span data-stu-id="387dd-258">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="387dd-259">Process counters.</span><span class="sxs-lookup"><span data-stu-id="387dd-259">Process counters.</span></span>
 * <span data-ttu-id="387dd-260">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="387dd-260">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="387dd-261">Exception stack trace values.</span><span class="sxs-lookup"><span data-stu-id="387dd-261">Exception stack trace values.</span></span>

[<span data-ttu-id="387dd-262">Learn more</span><span class="sxs-lookup"><span data-stu-id="387dd-262">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="387dd-263">Video</span><span class="sxs-lookup"><span data-stu-id="387dd-263">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a><span data-ttu-id="387dd-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="387dd-264">Next steps</span></span>

<span data-ttu-id="387dd-265">View your telemetry:</span><span class="sxs-lookup"><span data-stu-id="387dd-265">View your telemetry:</span></span>

* <span data-ttu-id="387dd-266">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span><span class="sxs-lookup"><span data-stu-id="387dd-266">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="387dd-267">[Search events and logs][diagnostic] to diagnose problems</span><span class="sxs-lookup"><span data-stu-id="387dd-267">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="387dd-268">[Analytics](app-insights-analytics.md) for more advanced queries</span><span class="sxs-lookup"><span data-stu-id="387dd-268">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="387dd-269">Create dashboards</span><span class="sxs-lookup"><span data-stu-id="387dd-269">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="387dd-270">Add more telemetry:</span><span class="sxs-lookup"><span data-stu-id="387dd-270">Add more telemetry:</span></span>

* <span data-ttu-id="387dd-271">[Create web tests][availability] to make sure your site stays live.</span><span class="sxs-lookup"><span data-stu-id="387dd-271">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="387dd-272">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span><span class="sxs-lookup"><span data-stu-id="387dd-272">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="387dd-273">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span><span class="sxs-lookup"><span data-stu-id="387dd-273">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md






