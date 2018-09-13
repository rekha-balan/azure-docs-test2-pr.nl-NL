---
title: Microsoft Dynamics CRM and Azure Application Insights | Microsoft Docs
description: Get telemetry from Microsoft Dynamics CRM Online using Application Insights. Walkthrough of setup, getting data, visualization and export.
services: application-insights
documentationcenter: ''
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: awills
ms.openlocfilehash: 451a32e2ca18f0b175369a15d9b4f228ede6d013
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550919"
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="2c924-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c924-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="2c924-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="2c924-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="2c924-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span><span class="sxs-lookup"><span data-stu-id="2c924-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="2c924-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="2c924-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="2c924-108">Add Application Insights to new or existing CRM Online instance</span><span class="sxs-lookup"><span data-stu-id="2c924-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="2c924-109">To monitor your application, you add an Application Insights SDK to your application.</span><span class="sxs-lookup"><span data-stu-id="2c924-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="2c924-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span><span class="sxs-lookup"><span data-stu-id="2c924-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="2c924-111">Create an Application Insights resource in Azure</span><span class="sxs-lookup"><span data-stu-id="2c924-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="2c924-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="2c924-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="2c924-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="2c924-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="2c924-114">This is where your data will be processed and displayed.</span><span class="sxs-lookup"><span data-stu-id="2c924-114">This is where your data will be processed and displayed.</span></span>
   
    ![Click +, Developer Services, Application Insights.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="2c924-116">Choose ASP.NET as the application type.</span><span class="sxs-lookup"><span data-stu-id="2c924-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="2c924-117">Open the Getting Started page and open "Monitor and diagnose client side".</span><span class="sxs-lookup"><span data-stu-id="2c924-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Code snippet for insertion in your web page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="2c924-119">**Keep the code page open** while you do the next step in another browser window.</span><span class="sxs-lookup"><span data-stu-id="2c924-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="2c924-120">You'll need the code soon.</span><span class="sxs-lookup"><span data-stu-id="2c924-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="2c924-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="2c924-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="2c924-122">Open your CRM Online instance and login with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="2c924-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="2c924-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span><span class="sxs-lookup"><span data-stu-id="2c924-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Microsoft Dynamics CRM settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/04.png)
   
    ![Settings > Customizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/05.png)

    ![Customize the system option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="2c924-127">Create a JavaScript resource.</span><span class="sxs-lookup"><span data-stu-id="2c924-127">Create a JavaScript resource.</span></span>
   
    ![New Web Resource dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="2c924-129">Give it a name, select **Script (JScript)** and open the text editor.</span><span class="sxs-lookup"><span data-stu-id="2c924-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Open the text editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="2c924-131">Copy the code from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2c924-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="2c924-132">While copying make sure to ignore script tags.</span><span class="sxs-lookup"><span data-stu-id="2c924-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="2c924-133">Refer below screenshot:</span><span class="sxs-lookup"><span data-stu-id="2c924-133">Refer below screenshot:</span></span>
   
    ![Set your instrumentation key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="2c924-135">The code includes the instrumentation key that identifies your Application insights resource.</span><span class="sxs-lookup"><span data-stu-id="2c924-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="2c924-136">Save and publish.</span><span class="sxs-lookup"><span data-stu-id="2c924-136">Save and publish.</span></span>
   
    ![Save and publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="2c924-138">Instrument Forms</span><span class="sxs-lookup"><span data-stu-id="2c924-138">Instrument Forms</span></span>
1. <span data-ttu-id="2c924-139">In Microsoft CRM Online, open the Account form</span><span class="sxs-lookup"><span data-stu-id="2c924-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Account form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="2c924-141">Open the form Properties</span><span class="sxs-lookup"><span data-stu-id="2c924-141">Open the form Properties</span></span>
   
    ![Form properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="2c924-143">Add the JavaScript web resource that you created</span><span class="sxs-lookup"><span data-stu-id="2c924-143">Add the JavaScript web resource that you created</span></span>
   
    ![Add menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/13.png)
   
    ![Add the web resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="2c924-146">Save and publish your form customizations.</span><span class="sxs-lookup"><span data-stu-id="2c924-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="2c924-147">Metrics captured</span><span class="sxs-lookup"><span data-stu-id="2c924-147">Metrics captured</span></span>
<span data-ttu-id="2c924-148">You have now set up telemetry capture for the form.</span><span class="sxs-lookup"><span data-stu-id="2c924-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="2c924-149">Whenever it is used, data will be sent to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="2c924-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="2c924-150">Here are samples of the data that you'll see.</span><span class="sxs-lookup"><span data-stu-id="2c924-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="2c924-151">Application health</span><span class="sxs-lookup"><span data-stu-id="2c924-151">Application health</span></span>
![Example page load time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/15.png)

![Example page views chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="2c924-154">Browser exceptions:</span><span class="sxs-lookup"><span data-stu-id="2c924-154">Browser exceptions:</span></span>

![Browser exceptions chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="2c924-156">Click the chart to get more detail:</span><span class="sxs-lookup"><span data-stu-id="2c924-156">Click the chart to get more detail:</span></span>

![Exceptions list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="2c924-158">Usage</span><span class="sxs-lookup"><span data-stu-id="2c924-158">Usage</span></span>
![Users, sessions and page views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/19.png)

![Sesion charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/20.png)

![Browser versions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="2c924-162">Browsers</span><span class="sxs-lookup"><span data-stu-id="2c924-162">Browsers</span></span>
![Breakdown of page load time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/22.png)

![Count of sessions by browser version](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="2c924-165">Geolocation</span><span class="sxs-lookup"><span data-stu-id="2c924-165">Geolocation</span></span>
![Session count by country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/24.png)

![Sessions and users by country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="2c924-168">Inside page view request</span><span class="sxs-lookup"><span data-stu-id="2c924-168">Inside page view request</span></span>
![Page view summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/26.png)

![Search on page view events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/27.png)

![Similar page views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/28.png)

![Page view properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/29.png)

![Pages per session](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="2c924-174">Sample code</span><span class="sxs-lookup"><span data-stu-id="2c924-174">Sample code</span></span>
<span data-ttu-id="2c924-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="2c924-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="2c924-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="2c924-176">Power BI</span></span>
<span data-ttu-id="2c924-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="2c924-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="2c924-178">Sample Microsoft Dynamics CRM Solution</span><span class="sxs-lookup"><span data-stu-id="2c924-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="2c924-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="2c924-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="2c924-180">Learn more</span><span class="sxs-lookup"><span data-stu-id="2c924-180">Learn more</span></span>
* [<span data-ttu-id="2c924-181">What is Application Insights?</span><span class="sxs-lookup"><span data-stu-id="2c924-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="2c924-182">Application Insights for web pages</span><span class="sxs-lookup"><span data-stu-id="2c924-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="2c924-183">More samples and walkthroughs</span><span class="sxs-lookup"><span data-stu-id="2c924-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)





























