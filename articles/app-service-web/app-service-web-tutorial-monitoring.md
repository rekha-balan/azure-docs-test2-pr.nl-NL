---
title: Monitor a Web App | Microsoft Docs
description: Learn how to set up Monitoring on your Web App
services: App-Service
keywords: ''
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 2dd1c2bfe32a87bdd59a03c9aa971ac59fee5657
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562928"
---
# <a name="monitor-app-service"></a><span data-ttu-id="f3e48-103">Monitor App Service</span><span class="sxs-lookup"><span data-stu-id="f3e48-103">Monitor App Service</span></span>
<span data-ttu-id="f3e48-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span><span class="sxs-lookup"><span data-stu-id="f3e48-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="f3e48-105">Each section of this document goes over a specific feature.</span><span class="sxs-lookup"><span data-stu-id="f3e48-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="f3e48-106">Using the features together let you:</span><span class="sxs-lookup"><span data-stu-id="f3e48-106">Using the features together let you:</span></span>
- <span data-ttu-id="f3e48-107">Identifying an issue in your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="f3e48-108">Determining when the issue is caused by your code or the platform.</span><span class="sxs-lookup"><span data-stu-id="f3e48-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="f3e48-109">Narrow down the source of the problem in your code.</span><span class="sxs-lookup"><span data-stu-id="f3e48-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="f3e48-110">Debugging and fixing the issue.</span><span class="sxs-lookup"><span data-stu-id="f3e48-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f3e48-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f3e48-111">Before you begin</span></span>
- <span data-ttu-id="f3e48-112">You need a Web App to monitor and follow the outlined steps.</span><span class="sxs-lookup"><span data-stu-id="f3e48-112">You need a Web App to monitor and follow the outlined steps.</span></span> 
    - <span data-ttu-id="f3e48-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="f3e48-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="f3e48-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3e48-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span> 
    - <span data-ttu-id="f3e48-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f3e48-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> 
    - <span data-ttu-id="f3e48-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="f3e48-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <a name="metrics"></a> <span data-ttu-id="f3e48-117">Step 1 - View metrics</span><span class="sxs-lookup"><span data-stu-id="f3e48-117">Step 1 - View metrics</span></span>
<span data-ttu-id="f3e48-118">**Metrics** are useful to understand:</span><span class="sxs-lookup"><span data-stu-id="f3e48-118">**Metrics** are useful to understand:</span></span> 
- <span data-ttu-id="f3e48-119">Application health</span><span class="sxs-lookup"><span data-stu-id="f3e48-119">Application health</span></span>
- <span data-ttu-id="f3e48-120">App performance</span><span class="sxs-lookup"><span data-stu-id="f3e48-120">App performance</span></span>
- <span data-ttu-id="f3e48-121">Resource consumption</span><span class="sxs-lookup"><span data-stu-id="f3e48-121">Resource consumption</span></span>

<span data-ttu-id="f3e48-122">When investigating an application issue, reviewing metrics is a good place to start.</span><span class="sxs-lookup"><span data-stu-id="f3e48-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="f3e48-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="f3e48-124">Metrics provide a historical view across several key aggregations for your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="f3e48-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f3e48-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e48-126">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="f3e48-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="f3e48-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="f3e48-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="f3e48-128">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="f3e48-128">App Service plans define:</span></span>
> * <span data-ttu-id="f3e48-129">Region: North Europe, East US, Southeast Asia, etc.</span><span class="sxs-lookup"><span data-stu-id="f3e48-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="f3e48-130">Instance Size: Small, Medium, Large, etc.</span><span class="sxs-lookup"><span data-stu-id="f3e48-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="f3e48-131">Scale Count: one, two, or three instances, etc.</span><span class="sxs-lookup"><span data-stu-id="f3e48-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="f3e48-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="f3e48-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="f3e48-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="f3e48-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="f3e48-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="f3e48-135">Click the tile to edit and configure what metrics to view and the time range to display.</span><span class="sxs-lookup"><span data-stu-id="f3e48-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span> 

<span data-ttu-id="f3e48-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span><span class="sxs-lookup"><span data-stu-id="f3e48-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="f3e48-137">![Monitor App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="f3e48-137">![Monitor App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="f3e48-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="f3e48-139">The high volume of errors is the first indication we need to investigate this application.</span><span class="sxs-lookup"><span data-stu-id="f3e48-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="f3e48-140">Learn more about Azure Monitor with the following links:</span><span class="sxs-lookup"><span data-stu-id="f3e48-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="f3e48-141">Get started with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f3e48-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="f3e48-142">Azure Metrics</span><span class="sxs-lookup"><span data-stu-id="f3e48-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="f3e48-143">Supported metrics with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f3e48-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md#microsoftwebsites-including-functions)
> - [<span data-ttu-id="f3e48-144">Azure Dashboards</span><span class="sxs-lookup"><span data-stu-id="f3e48-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a> <span data-ttu-id="f3e48-145">Step 2 - Configure Alerts</span><span class="sxs-lookup"><span data-stu-id="f3e48-145">Step 2 - Configure Alerts</span></span>
<span data-ttu-id="f3e48-146">**Alerts** can be configured to trigger on specific conditions for your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="f3e48-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span><span class="sxs-lookup"><span data-stu-id="f3e48-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span> 

<span data-ttu-id="f3e48-148">Lets configure an alert to automatically get notified when errors occur.</span><span class="sxs-lookup"><span data-stu-id="f3e48-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="f3e48-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span><span class="sxs-lookup"><span data-stu-id="f3e48-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="f3e48-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="f3e48-152">Provide values for the Alert configuration:</span><span class="sxs-lookup"><span data-stu-id="f3e48-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="f3e48-153">**Resource:** The site to monitor with the alert.</span><span class="sxs-lookup"><span data-stu-id="f3e48-153">**Resource:** The site to monitor with the alert.</span></span> 
- <span data-ttu-id="f3e48-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="f3e48-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="f3e48-155">**Description:** Plain text explanation of what this alert is looking at.</span><span class="sxs-lookup"><span data-stu-id="f3e48-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="f3e48-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span><span class="sxs-lookup"><span data-stu-id="f3e48-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="f3e48-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span><span class="sxs-lookup"><span data-stu-id="f3e48-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="f3e48-158">**Condition:** When to alert, in this case select the *greater than* option.</span><span class="sxs-lookup"><span data-stu-id="f3e48-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="f3e48-159">**Threshold:** What is value to look for, in this case: *400*.</span><span class="sxs-lookup"><span data-stu-id="f3e48-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="f3e48-160">**Period:** Alerts operate over the average value of a metric.</span><span class="sxs-lookup"><span data-stu-id="f3e48-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="f3e48-161">Smaller periods of time yield more sensitive alerts.</span><span class="sxs-lookup"><span data-stu-id="f3e48-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="f3e48-162">in this case we are looking at *5 Minutes*.</span><span class="sxs-lookup"><span data-stu-id="f3e48-162">in this case we are looking at *5 Minutes*.</span></span> 
- <span data-ttu-id="f3e48-163">**Email Owners and contributors:** in this case: *Enabled*.</span><span class="sxs-lookup"><span data-stu-id="f3e48-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="f3e48-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span><span class="sxs-lookup"><span data-stu-id="f3e48-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="f3e48-165">Active alerts can also be reviewed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f3e48-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Triggered Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="f3e48-167">Learn more about Azure Alerts with the following links:</span><span class="sxs-lookup"><span data-stu-id="f3e48-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="f3e48-168">What are alerts in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f3e48-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="f3e48-169">Take Action On Metrics</span><span class="sxs-lookup"><span data-stu-id="f3e48-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="f3e48-170">Create metric alerts</span><span class="sxs-lookup"><span data-stu-id="f3e48-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> <span data-ttu-id="f3e48-171">Step 3 - App Service Companion</span><span class="sxs-lookup"><span data-stu-id="f3e48-171">Step 3 - App Service Companion</span></span>
<span data-ttu-id="f3e48-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span><span class="sxs-lookup"><span data-stu-id="f3e48-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="f3e48-173">Use App Service Companion to:</span><span class="sxs-lookup"><span data-stu-id="f3e48-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="f3e48-174">Review application metrics</span><span class="sxs-lookup"><span data-stu-id="f3e48-174">Review application metrics</span></span>
- <span data-ttu-id="f3e48-175">Review and act on application alerts and recommendations</span><span class="sxs-lookup"><span data-stu-id="f3e48-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="f3e48-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span><span class="sxs-lookup"><span data-stu-id="f3e48-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="f3e48-177">Get push notifications for critical events.</span><span class="sxs-lookup"><span data-stu-id="f3e48-177">Get push notifications for critical events.</span></span>

![App Service Companion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="f3e48-179">[![App Service Companion App Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="f3e48-179">[![App Service Companion App Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="f3e48-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="f3e48-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <a name="diagnose"></a> <span data-ttu-id="f3e48-181">Step 4 - Diagnose and solve problems</span><span class="sxs-lookup"><span data-stu-id="f3e48-181">Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="f3e48-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span><span class="sxs-lookup"><span data-stu-id="f3e48-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="f3e48-183">It can also suggest possible mitigations to get your Web App back to healthy.</span><span class="sxs-lookup"><span data-stu-id="f3e48-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>
 
![Diagnose and Solve Problems](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="f3e48-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span><span class="sxs-lookup"><span data-stu-id="f3e48-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="f3e48-186">In contrast, the platform availability has not moved from 100%.</span><span class="sxs-lookup"><span data-stu-id="f3e48-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="f3e48-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span><span class="sxs-lookup"><span data-stu-id="f3e48-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <a name="logging"></a> <span data-ttu-id="f3e48-188">Step 5 - Logging</span><span class="sxs-lookup"><span data-stu-id="f3e48-188">Step 5 - Logging</span></span>
<span data-ttu-id="f3e48-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span><span class="sxs-lookup"><span data-stu-id="f3e48-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="f3e48-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span><span class="sxs-lookup"><span data-stu-id="f3e48-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="f3e48-191">Application Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f3e48-191">Application Diagnostics</span></span>
<span data-ttu-id="f3e48-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span><span class="sxs-lookup"><span data-stu-id="f3e48-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span> 

<span data-ttu-id="f3e48-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span><span class="sxs-lookup"><span data-stu-id="f3e48-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="f3e48-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f3e48-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="f3e48-195">You can also specify the severity of the trace for easier filtering.</span><span class="sxs-lookup"><span data-stu-id="f3e48-195">You can also specify the severity of the trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="f3e48-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span><span class="sxs-lookup"><span data-stu-id="f3e48-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Monitor App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="f3e48-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span><span class="sxs-lookup"><span data-stu-id="f3e48-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="f3e48-199">For production scenarios, it's recommended to use blob storage.</span><span class="sxs-lookup"><span data-stu-id="f3e48-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3e48-200">Enabling logging has an impact on your application performance and resource utilization.</span><span class="sxs-lookup"><span data-stu-id="f3e48-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="f3e48-201">For production scenarios, error logs are recommended.</span><span class="sxs-lookup"><span data-stu-id="f3e48-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="f3e48-202">Only enable more verbose logging when investigating issues.</span><span class="sxs-lookup"><span data-stu-id="f3e48-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="f3e48-203">Web Server Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f3e48-203">Web Server Diagnostics</span></span>
<span data-ttu-id="f3e48-204">Web Server logs are generated even if your app is not instrumented.</span><span class="sxs-lookup"><span data-stu-id="f3e48-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="f3e48-205">App Service can collect three different types of server logs:</span><span class="sxs-lookup"><span data-stu-id="f3e48-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="f3e48-206">**Web Server Logging**</span><span class="sxs-lookup"><span data-stu-id="f3e48-206">**Web Server Logging**</span></span> 
    - <span data-ttu-id="f3e48-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e48-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> 
    - <span data-ttu-id="f3e48-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span><span class="sxs-lookup"><span data-stu-id="f3e48-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="f3e48-209">**Detailed Error Logging**</span><span class="sxs-lookup"><span data-stu-id="f3e48-209">**Detailed Error Logging**</span></span> 
    - <span data-ttu-id="f3e48-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span><span class="sxs-lookup"><span data-stu-id="f3e48-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> 
    - [<span data-ttu-id="f3e48-211">Learn more about detailed error logging</span><span class="sxs-lookup"><span data-stu-id="f3e48-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="f3e48-212">**Failed Request Tracing**</span><span class="sxs-lookup"><span data-stu-id="f3e48-212">**Failed Request Tracing**</span></span> 
    - <span data-ttu-id="f3e48-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span><span class="sxs-lookup"><span data-stu-id="f3e48-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span> 
    - <span data-ttu-id="f3e48-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span><span class="sxs-lookup"><span data-stu-id="f3e48-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="f3e48-215">Learn more about failed request tracing</span><span class="sxs-lookup"><span data-stu-id="f3e48-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="f3e48-216">To enable Server logging:</span><span class="sxs-lookup"><span data-stu-id="f3e48-216">To enable Server logging:</span></span>
- <span data-ttu-id="f3e48-217">go to **Monitoring** > **Diagnostic Logs**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-217">go to **Monitoring** > **Diagnostic Logs**.</span></span> 
- <span data-ttu-id="f3e48-218">Enable the different types of Web Server Diagnostics using the toggles.</span><span class="sxs-lookup"><span data-stu-id="f3e48-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Monitor App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="f3e48-220">Enabling logging has an impact on your application performance and resource utilization.</span><span class="sxs-lookup"><span data-stu-id="f3e48-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="f3e48-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span><span class="sxs-lookup"><span data-stu-id="f3e48-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="f3e48-222">Accessing Logs</span><span class="sxs-lookup"><span data-stu-id="f3e48-222">Accessing Logs</span></span>
<span data-ttu-id="f3e48-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="f3e48-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="f3e48-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span><span class="sxs-lookup"><span data-stu-id="f3e48-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="f3e48-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="f3e48-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="f3e48-226">This folder contains one or more text files containing information produced by application logging.</span><span class="sxs-lookup"><span data-stu-id="f3e48-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="f3e48-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="f3e48-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span> 
    - <span data-ttu-id="f3e48-228">This folder contains an XSL file and one or more XML files.</span><span class="sxs-lookup"><span data-stu-id="f3e48-228">This folder contains an XSL file and one or more XML files.</span></span> 
- <span data-ttu-id="f3e48-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="f3e48-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span> 
    - <span data-ttu-id="f3e48-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="f3e48-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="f3e48-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span> 
    - <span data-ttu-id="f3e48-232">This folder contains one or more text files formatted using the W3C extended log file format.</span><span class="sxs-lookup"><span data-stu-id="f3e48-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <a name="streaming"></a> <span data-ttu-id="f3e48-233">Step 6 - Log Streaming</span><span class="sxs-lookup"><span data-stu-id="f3e48-233">Step 6 - Log Streaming</span></span>
<span data-ttu-id="f3e48-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span><span class="sxs-lookup"><span data-stu-id="f3e48-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="f3e48-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span><span class="sxs-lookup"><span data-stu-id="f3e48-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span> 

> [!TIP]
> <span data-ttu-id="f3e48-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span><span class="sxs-lookup"><span data-stu-id="f3e48-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="f3e48-237">To stream logs, go to **Monitoring**> **Log Stream**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="f3e48-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span><span class="sxs-lookup"><span data-stu-id="f3e48-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="f3e48-239">From here, you can also pause, restart, and clear the buffer.</span><span class="sxs-lookup"><span data-stu-id="f3e48-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Streaming Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="f3e48-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span><span class="sxs-lookup"><span data-stu-id="f3e48-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <a name="remote"></a> <span data-ttu-id="f3e48-242">Step 7 - Remote Debugging</span><span class="sxs-lookup"><span data-stu-id="f3e48-242">Step 7 - Remote Debugging</span></span>
<span data-ttu-id="f3e48-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span><span class="sxs-lookup"><span data-stu-id="f3e48-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="f3e48-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f3e48-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="f3e48-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span><span class="sxs-lookup"><span data-stu-id="f3e48-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="f3e48-246">To attach the debugger to your app running in the cloud:</span><span class="sxs-lookup"><span data-stu-id="f3e48-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="f3e48-247">Using Visual Studio 2017, open the solution for the app you want to debug</span><span class="sxs-lookup"><span data-stu-id="f3e48-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span> 
- <span data-ttu-id="f3e48-248">Set some brake points just like you would for local development.</span><span class="sxs-lookup"><span data-stu-id="f3e48-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="f3e48-249">Open **cloud explorer** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="f3e48-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="f3e48-250">Log in with your azure credentials as needed.</span><span class="sxs-lookup"><span data-stu-id="f3e48-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="f3e48-251">Find the app you want to debug</span><span class="sxs-lookup"><span data-stu-id="f3e48-251">Find the app you want to debug</span></span>
- <span data-ttu-id="f3e48-252">Select **Attach Debugger** form the **Actions** pane.</span><span class="sxs-lookup"><span data-stu-id="f3e48-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Remote Debugging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="f3e48-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="f3e48-255">Browse through your app to trigger break points and step through the code.</span><span class="sxs-lookup"><span data-stu-id="f3e48-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="f3e48-256">Running in debug mode in production is not recommended.</span><span class="sxs-lookup"><span data-stu-id="f3e48-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="f3e48-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span><span class="sxs-lookup"><span data-stu-id="f3e48-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="f3e48-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="f3e48-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <a name="explorer"></a> <span data-ttu-id="f3e48-259">Step 8 - Process Explorer</span><span class="sxs-lookup"><span data-stu-id="f3e48-259">Step 8 - Process Explorer</span></span>
<span data-ttu-id="f3e48-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span><span class="sxs-lookup"><span data-stu-id="f3e48-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="f3e48-261">Use **Process Explorer** to:</span><span class="sxs-lookup"><span data-stu-id="f3e48-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="f3e48-262">Enumerate all the processes across different instances of your App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f3e48-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="f3e48-263">Drill down and view the handles and modules associated with each process.</span><span class="sxs-lookup"><span data-stu-id="f3e48-263">Drill down and view the handles and modules associated with each process.</span></span> 
- <span data-ttu-id="f3e48-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span><span class="sxs-lookup"><span data-stu-id="f3e48-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="f3e48-265">Find open file handles, and even kill a specific process instance.</span><span class="sxs-lookup"><span data-stu-id="f3e48-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="f3e48-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f3e48-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Process Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> <span data-ttu-id="f3e48-268">Step 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3e48-268">Step 9 - Application Insights</span></span>
<span data-ttu-id="f3e48-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span><span class="sxs-lookup"><span data-stu-id="f3e48-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span> 

<span data-ttu-id="f3e48-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span><span class="sxs-lookup"><span data-stu-id="f3e48-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="f3e48-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="f3e48-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span> 

> [!NOTE]
> <span data-ttu-id="f3e48-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span><span class="sxs-lookup"><span data-stu-id="f3e48-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="f3e48-273">Installing the site extension causes an application restart.</span><span class="sxs-lookup"><span data-stu-id="f3e48-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="f3e48-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span><span class="sxs-lookup"><span data-stu-id="f3e48-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <a name="next"></a> <span data-ttu-id="f3e48-276">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3e48-276">Next steps</span></span>

 - [<span data-ttu-id="f3e48-277">What is Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3e48-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="f3e48-278">Monitor Azure web app performance with Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3e48-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="f3e48-279">Monitor availability and responsiveness of any web site with Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3e48-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)












