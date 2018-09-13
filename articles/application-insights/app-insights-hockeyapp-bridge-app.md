---
title: Exploring HockeyApp data in Azure Application Insights | Microsoft Docs
description: Analyze usage and performance of your Azure app with Application Insights.
services: application-insights
documentationcenter: windows
author: alancameronwills
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: awills
ms.openlocfilehash: 95ba286d3b81efe4f48efaa722cd20ee9aa65f70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550706"
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="26fdc-103">Exploring HockeyApp data in Application Insights</span><span class="sxs-lookup"><span data-stu-id="26fdc-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="26fdc-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="26fdc-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="26fdc-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span><span class="sxs-lookup"><span data-stu-id="26fdc-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="26fdc-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26fdc-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="26fdc-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="26fdc-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="26fdc-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26fdc-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="26fdc-109">The HockeyApp Bridge app</span><span class="sxs-lookup"><span data-stu-id="26fdc-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="26fdc-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span><span class="sxs-lookup"><span data-stu-id="26fdc-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="26fdc-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span><span class="sxs-lookup"><span data-stu-id="26fdc-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="26fdc-112">Let’s see how to set up one of these Bridge Apps.</span><span class="sxs-lookup"><span data-stu-id="26fdc-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="26fdc-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="26fdc-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="26fdc-114">Either create a new token or reuse an existing one.</span><span class="sxs-lookup"><span data-stu-id="26fdc-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="26fdc-115">The minimum rights required are "read only".</span><span class="sxs-lookup"><span data-stu-id="26fdc-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="26fdc-116">Take a copy of the API token.</span><span class="sxs-lookup"><span data-stu-id="26fdc-116">Take a copy of the API token.</span></span>

![Get a HockeyApp API token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="26fdc-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="26fdc-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="26fdc-119">Set Application Type to “HockeyApp bridge application”:</span><span class="sxs-lookup"><span data-stu-id="26fdc-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![New Application Insights resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="26fdc-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span><span class="sxs-lookup"><span data-stu-id="26fdc-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="26fdc-122">The HockeyApp bridge fields appear.</span><span class="sxs-lookup"><span data-stu-id="26fdc-122">The HockeyApp bridge fields appear.</span></span> 

![Enter bridge fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="26fdc-124">Enter the HockeyApp token you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="26fdc-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="26fdc-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span><span class="sxs-lookup"><span data-stu-id="26fdc-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="26fdc-126">Select the one you want to use, and complete the remainder of the fields.</span><span class="sxs-lookup"><span data-stu-id="26fdc-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="26fdc-127">Open the new resource.</span><span class="sxs-lookup"><span data-stu-id="26fdc-127">Open the new resource.</span></span> 

<span data-ttu-id="26fdc-128">Note that the data takes a while to start flowing.</span><span class="sxs-lookup"><span data-stu-id="26fdc-128">Note that the data takes a while to start flowing.</span></span>

![Application Insights resource waiting for data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="26fdc-130">That’s it!</span><span class="sxs-lookup"><span data-stu-id="26fdc-130">That’s it!</span></span> <span data-ttu-id="26fdc-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26fdc-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="26fdc-132">Let’s briefly review each of these features now available to you.</span><span class="sxs-lookup"><span data-stu-id="26fdc-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="26fdc-133">Analytics</span><span class="sxs-lookup"><span data-stu-id="26fdc-133">Analytics</span></span>
<span data-ttu-id="26fdc-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span><span class="sxs-lookup"><span data-stu-id="26fdc-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="26fdc-136">Learn more about Analytics</span><span class="sxs-lookup"><span data-stu-id="26fdc-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="26fdc-137">Continuous export</span><span class="sxs-lookup"><span data-stu-id="26fdc-137">Continuous export</span></span>
<span data-ttu-id="26fdc-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span><span class="sxs-lookup"><span data-stu-id="26fdc-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="26fdc-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26fdc-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="26fdc-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span><span class="sxs-lookup"><span data-stu-id="26fdc-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="26fdc-141">Learn more about Continuous Export</span><span class="sxs-lookup"><span data-stu-id="26fdc-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="26fdc-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="26fdc-142">Next steps</span></span>
* [<span data-ttu-id="26fdc-143">Apply Analytics to your data</span><span class="sxs-lookup"><span data-stu-id="26fdc-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)






