---
title: Fix 502 bad gateway, 503 service unavailable errors | Microsoft Docs
description: Troubleshoot 502 bad gateway and 503 service unavailable errors in your web app hosted in Azure App Service.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: top-support-issue
keywords: 502 bad gateway, 503 service unavailable, error 503, error 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: a3f75318d054255003c24d7897c68d3b8e73d616
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662256"
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="d6dad-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span><span class="sxs-lookup"><span data-stu-id="d6dad-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="d6dad-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d6dad-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d6dad-106">This article helps you troubleshoot these errors.</span><span class="sxs-lookup"><span data-stu-id="d6dad-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="d6dad-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="d6dad-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="d6dad-108">Alternatively, you can also file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="d6dad-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="d6dad-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="d6dad-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="d6dad-110">Symptom</span><span class="sxs-lookup"><span data-stu-id="d6dad-110">Symptom</span></span>
<span data-ttu-id="d6dad-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span><span class="sxs-lookup"><span data-stu-id="d6dad-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="d6dad-112">Cause</span><span class="sxs-lookup"><span data-stu-id="d6dad-112">Cause</span></span>
<span data-ttu-id="d6dad-113">This problem is often caused by application level issues, such as:</span><span class="sxs-lookup"><span data-stu-id="d6dad-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="d6dad-114">requests taking a long time</span><span class="sxs-lookup"><span data-stu-id="d6dad-114">requests taking a long time</span></span>
* <span data-ttu-id="d6dad-115">application using high memory/CPU</span><span class="sxs-lookup"><span data-stu-id="d6dad-115">application using high memory/CPU</span></span>
* <span data-ttu-id="d6dad-116">application crashing due to an exception.</span><span class="sxs-lookup"><span data-stu-id="d6dad-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="d6dad-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span><span class="sxs-lookup"><span data-stu-id="d6dad-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="d6dad-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span><span class="sxs-lookup"><span data-stu-id="d6dad-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="d6dad-119">Observe and monitor application behavior</span><span class="sxs-lookup"><span data-stu-id="d6dad-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="d6dad-120">Collect data</span><span class="sxs-lookup"><span data-stu-id="d6dad-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="d6dad-121">Mitigate the issue</span><span class="sxs-lookup"><span data-stu-id="d6dad-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="d6dad-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span><span class="sxs-lookup"><span data-stu-id="d6dad-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="d6dad-123">1. Observe and monitor application behavior</span><span class="sxs-lookup"><span data-stu-id="d6dad-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="d6dad-124">Track Service health</span><span class="sxs-lookup"><span data-stu-id="d6dad-124">Track Service health</span></span>
<span data-ttu-id="d6dad-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span><span class="sxs-lookup"><span data-stu-id="d6dad-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="d6dad-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6dad-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d6dad-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="d6dad-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="d6dad-128">Monitor your web app</span><span class="sxs-lookup"><span data-stu-id="d6dad-128">Monitor your web app</span></span>
<span data-ttu-id="d6dad-129">This option enables you to find out if your application is having any issues.</span><span class="sxs-lookup"><span data-stu-id="d6dad-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="d6dad-130">In your web app’s blade, click the **Requests and errors** tile.</span><span class="sxs-lookup"><span data-stu-id="d6dad-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="d6dad-131">The **Metric** blade will show you all the metrics you can add.</span><span class="sxs-lookup"><span data-stu-id="d6dad-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="d6dad-132">Some of the metrics that you might want to monitor for your web app are</span><span class="sxs-lookup"><span data-stu-id="d6dad-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="d6dad-133">Average memory working set</span><span class="sxs-lookup"><span data-stu-id="d6dad-133">Average memory working set</span></span>
* <span data-ttu-id="d6dad-134">Average response time</span><span class="sxs-lookup"><span data-stu-id="d6dad-134">Average response time</span></span>
* <span data-ttu-id="d6dad-135">CPU time</span><span class="sxs-lookup"><span data-stu-id="d6dad-135">CPU time</span></span>
* <span data-ttu-id="d6dad-136">Memory working set</span><span class="sxs-lookup"><span data-stu-id="d6dad-136">Memory working set</span></span>
* <span data-ttu-id="d6dad-137">Requests</span><span class="sxs-lookup"><span data-stu-id="d6dad-137">Requests</span></span>

![monitor web app towards solving HTTP errors of 502 bad gateway and 503 service unavailable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="d6dad-139">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="d6dad-139">For more information, see:</span></span>

* [<span data-ttu-id="d6dad-140">Monitor Web Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d6dad-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="d6dad-141">Receive alert notifications</span><span class="sxs-lookup"><span data-stu-id="d6dad-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="d6dad-142">2. Collect data</span><span class="sxs-lookup"><span data-stu-id="d6dad-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="d6dad-143">Use the Azure App Service Support Portal</span><span class="sxs-lookup"><span data-stu-id="d6dad-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="d6dad-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span><span class="sxs-lookup"><span data-stu-id="d6dad-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="d6dad-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="d6dad-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="d6dad-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span><span class="sxs-lookup"><span data-stu-id="d6dad-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="d6dad-147">Observe current behavior</span><span class="sxs-lookup"><span data-stu-id="d6dad-147">Observe current behavior</span></span>
2. <span data-ttu-id="d6dad-148">Analyze by collecting diagnostics information and running the built-in analyzers</span><span class="sxs-lookup"><span data-stu-id="d6dad-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="d6dad-149">Mitigate</span><span class="sxs-lookup"><span data-stu-id="d6dad-149">Mitigate</span></span>

<span data-ttu-id="d6dad-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span><span class="sxs-lookup"><span data-stu-id="d6dad-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="d6dad-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span><span class="sxs-lookup"><span data-stu-id="d6dad-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="d6dad-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span><span class="sxs-lookup"><span data-stu-id="d6dad-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="d6dad-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="d6dad-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="d6dad-154">Use the Kudu Debug Console</span><span class="sxs-lookup"><span data-stu-id="d6dad-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="d6dad-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span><span class="sxs-lookup"><span data-stu-id="d6dad-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="d6dad-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span><span class="sxs-lookup"><span data-stu-id="d6dad-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="d6dad-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="d6dad-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="d6dad-158">Some of the things that Kudu provides are:</span><span class="sxs-lookup"><span data-stu-id="d6dad-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="d6dad-159">environment settings for your application</span><span class="sxs-lookup"><span data-stu-id="d6dad-159">environment settings for your application</span></span>
* <span data-ttu-id="d6dad-160">log stream</span><span class="sxs-lookup"><span data-stu-id="d6dad-160">log stream</span></span>
* <span data-ttu-id="d6dad-161">diagnostic dump</span><span class="sxs-lookup"><span data-stu-id="d6dad-161">diagnostic dump</span></span>
* <span data-ttu-id="d6dad-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span><span class="sxs-lookup"><span data-stu-id="d6dad-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="d6dad-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span><span class="sxs-lookup"><span data-stu-id="d6dad-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="d6dad-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span><span class="sxs-lookup"><span data-stu-id="d6dad-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="d6dad-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="d6dad-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="d6dad-166">3. Mitigate the issue</span><span class="sxs-lookup"><span data-stu-id="d6dad-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="d6dad-167">Scale the web app</span><span class="sxs-lookup"><span data-stu-id="d6dad-167">Scale the web app</span></span>
<span data-ttu-id="d6dad-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span><span class="sxs-lookup"><span data-stu-id="d6dad-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="d6dad-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span><span class="sxs-lookup"><span data-stu-id="d6dad-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="d6dad-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d6dad-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="d6dad-171">Additionally, you can choose to run your application on more than one instance .</span><span class="sxs-lookup"><span data-stu-id="d6dad-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="d6dad-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span><span class="sxs-lookup"><span data-stu-id="d6dad-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="d6dad-173">If the process goes down on one instance, the other instance will still continue serving requests.</span><span class="sxs-lookup"><span data-stu-id="d6dad-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="d6dad-174">You can set the scaling to be Manual or Automatic.</span><span class="sxs-lookup"><span data-stu-id="d6dad-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="d6dad-175">Use AutoHeal</span><span class="sxs-lookup"><span data-stu-id="d6dad-175">Use AutoHeal</span></span>
<span data-ttu-id="d6dad-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span><span class="sxs-lookup"><span data-stu-id="d6dad-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="d6dad-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span><span class="sxs-lookup"><span data-stu-id="d6dad-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="d6dad-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span><span class="sxs-lookup"><span data-stu-id="d6dad-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="d6dad-179">All you need to do is add some triggers in the root web.config for your web app.</span><span class="sxs-lookup"><span data-stu-id="d6dad-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="d6dad-180">Note that these settings would work in the same way even if your application is not a .Net one.</span><span class="sxs-lookup"><span data-stu-id="d6dad-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="d6dad-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d6dad-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="d6dad-182">Restart the web app</span><span class="sxs-lookup"><span data-stu-id="d6dad-182">Restart the web app</span></span>
<span data-ttu-id="d6dad-183">This is often the simplest way to recover from one-time issues.</span><span class="sxs-lookup"><span data-stu-id="d6dad-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="d6dad-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span><span class="sxs-lookup"><span data-stu-id="d6dad-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![restart app to solve HTTP errors of 502 bad gateway and 503 service unavailable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="d6dad-186">You can also manage your web app using Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="d6dad-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="d6dad-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d6dad-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>



