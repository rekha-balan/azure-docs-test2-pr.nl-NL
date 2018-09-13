---
title: SCOM integration with Application Insights | Microsoft Docs
description: If you're an SCOM user, monitor performance and diagnose issues with Application Insights. Comprehensive dashboards, smart alerts, powerful diagnostic tools and analysis queries.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: awills
ms.openlocfilehash: 89bfa92957237c9c9d7e7a41b052aac1a69e6db5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660937"
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="166d3-104">Application Performance Monitoring using Application Insights for SCOM</span><span class="sxs-lookup"><span data-stu-id="166d3-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="166d3-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="166d3-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="166d3-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span><span class="sxs-lookup"><span data-stu-id="166d3-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="166d3-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span><span class="sxs-lookup"><span data-stu-id="166d3-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="166d3-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span><span class="sxs-lookup"><span data-stu-id="166d3-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="166d3-109">Before you start</span><span class="sxs-lookup"><span data-stu-id="166d3-109">Before you start</span></span>
<span data-ttu-id="166d3-110">We assume:</span><span class="sxs-lookup"><span data-stu-id="166d3-110">We assume:</span></span>

* <span data-ttu-id="166d3-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span><span class="sxs-lookup"><span data-stu-id="166d3-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="166d3-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span><span class="sxs-lookup"><span data-stu-id="166d3-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="166d3-113">App framework version is .NET 4.5 or later.</span><span class="sxs-lookup"><span data-stu-id="166d3-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="166d3-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="166d3-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="166d3-115">Your organization may have a subscription, and can add your Microsoft account to it.</span><span class="sxs-lookup"><span data-stu-id="166d3-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="166d3-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span><span class="sxs-lookup"><span data-stu-id="166d3-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="166d3-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="166d3-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="166d3-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span><span class="sxs-lookup"><span data-stu-id="166d3-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="166d3-119">(One time) Install Application Insights management pack</span><span class="sxs-lookup"><span data-stu-id="166d3-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="166d3-120">On the machine where you run Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="166d3-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="166d3-121">Uninstall any old version of the management pack:</span><span class="sxs-lookup"><span data-stu-id="166d3-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="166d3-122">In Operations Manager, open Administration, Management Packs.</span><span class="sxs-lookup"><span data-stu-id="166d3-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="166d3-123">Delete the old version.</span><span class="sxs-lookup"><span data-stu-id="166d3-123">Delete the old version.</span></span>
2. <span data-ttu-id="166d3-124">Download and install the management pack from the catalog.</span><span class="sxs-lookup"><span data-stu-id="166d3-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="166d3-125">Restart Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="166d3-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="166d3-126">Create a management pack</span><span class="sxs-lookup"><span data-stu-id="166d3-126">Create a management pack</span></span>
1. <span data-ttu-id="166d3-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="166d3-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/020.png)
2. <span data-ttu-id="166d3-128">Name the configuration after your app.</span><span class="sxs-lookup"><span data-stu-id="166d3-128">Name the configuration after your app.</span></span> <span data-ttu-id="166d3-129">(You have to instrument one app at a time.)</span><span class="sxs-lookup"><span data-stu-id="166d3-129">(You have to instrument one app at a time.)</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/030.png)
3. <span data-ttu-id="166d3-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span><span class="sxs-lookup"><span data-stu-id="166d3-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="166d3-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span><span class="sxs-lookup"><span data-stu-id="166d3-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="166d3-132">You can reuse the same instance later.)</span><span class="sxs-lookup"><span data-stu-id="166d3-132">You can reuse the same instance later.)</span></span>

    ![In the General Properties tab, type the name of the app.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/040.png)

1. <span data-ttu-id="166d3-136">Choose one app that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="166d3-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="166d3-137">The search feature searches among apps installed on your servers.</span><span class="sxs-lookup"><span data-stu-id="166d3-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![On What to Monitor tab, click Add, type part of the app name, click Search, choose the app, and then Add, OK.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/050.png)
   
    <span data-ttu-id="166d3-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span><span class="sxs-lookup"><span data-stu-id="166d3-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="166d3-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="166d3-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="166d3-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span><span class="sxs-lookup"><span data-stu-id="166d3-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="166d3-142">If the application was configured for Application Insights during development, select its existing resource.</span><span class="sxs-lookup"><span data-stu-id="166d3-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="166d3-143">Otherwise, create a new resource named for the app.</span><span class="sxs-lookup"><span data-stu-id="166d3-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="166d3-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span><span class="sxs-lookup"><span data-stu-id="166d3-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="166d3-145">You can change these settings later.</span><span class="sxs-lookup"><span data-stu-id="166d3-145">You can change these settings later.</span></span>
     
     ![On Application Insights settings tab, click 'sign in' and provide your Microsoft account credentials for Azure.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/060.png)
3. <span data-ttu-id="166d3-148">Complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="166d3-148">Complete the wizard.</span></span>
   
    ![Click Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/070.png)

<span data-ttu-id="166d3-150">Repeat this procedure for each app that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="166d3-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="166d3-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span><span class="sxs-lookup"><span data-stu-id="166d3-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![In Authoring, select .NET Application Performance Monitoring with Application Insights, select your monitor, and click Properties.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="166d3-153">Verify monitoring</span><span class="sxs-lookup"><span data-stu-id="166d3-153">Verify monitoring</span></span>
<span data-ttu-id="166d3-154">The monitor that you have installed searches for your app on every server.</span><span class="sxs-lookup"><span data-stu-id="166d3-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="166d3-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span><span class="sxs-lookup"><span data-stu-id="166d3-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="166d3-156">If necessary, it first installs Status Monitor on the server.</span><span class="sxs-lookup"><span data-stu-id="166d3-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="166d3-157">You can verify which instances of the app it has found:</span><span class="sxs-lookup"><span data-stu-id="166d3-157">You can verify which instances of the app it has found:</span></span>

![In Monitoring, open Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="166d3-159">View telemetry in Application Insights</span><span class="sxs-lookup"><span data-stu-id="166d3-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="166d3-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span><span class="sxs-lookup"><span data-stu-id="166d3-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="166d3-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span><span class="sxs-lookup"><span data-stu-id="166d3-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="166d3-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span><span class="sxs-lookup"><span data-stu-id="166d3-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="166d3-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="166d3-163">Next steps</span></span>
* <span data-ttu-id="166d3-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span><span class="sxs-lookup"><span data-stu-id="166d3-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="166d3-165">Learn about metrics</span><span class="sxs-lookup"><span data-stu-id="166d3-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="166d3-166">Set up alerts</span><span class="sxs-lookup"><span data-stu-id="166d3-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="166d3-167">Diagnosing performance issues</span><span class="sxs-lookup"><span data-stu-id="166d3-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="166d3-168">Powerful Analytics queries</span><span class="sxs-lookup"><span data-stu-id="166d3-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="166d3-169">Availability web tests</span><span class="sxs-lookup"><span data-stu-id="166d3-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)









